# 21 — Cycle B: Equity TA Math Specification, v0.1

**Status**: Draft — B.3 output
**Date**: 2026-05-31
**Version**: v0.1 (first iteration; will be refined to v0.2 after B.4 test + B.5 critique)
**Scope**: Indian NSE direct equity, NIFTY 100 universe. No mutual funds (no MF TA, Cycle C). No FA (Cycle A). No position sizing beyond per-stock risk (Cycle D). No exit math beyond initial stop-loss (Cycle E).
**Source**: Distilled from `20_cycle_B_research.md` + Pranav's B.2 picks (all defaults).

---

## 0. v0.1 picks (recap from B.2)

| # | Decision | Pick |
|---|---|---|
| 1 | Indicator count | **7** (200-DMA, ADX, ROC, MACD, RSI, Bollinger, ATR) |
| 2 | Primary timeframe | **Weekly throughout** (daily as confirmation only) |
| 3 | 52-week breakout | **Deferred to v0.2** |
| 4 | Per-stock risk budget | **1% of portfolio NAV** |
| 5 | Output labels | **4** — ENTRY_ZONE / WAIT / AVOID_ENTRY / EXIT_WARNING |
| 6 | Cycle A/B combined display | **Yes** (locked by Q5 in v0.4 problem statement) |

---

## 1. The pipeline

For every NIFTY 100 stock the bot evaluates, the math runs in this exact order:

```
[0] Pre-screening filters
    [0.1] ASM / ESM / T+T surveillance check
    [0.2] Circuit-limit recent-event check (5 trading days)
    [0.3] F&O monthly-expiry proximity check (±2 trading days, daily-chart only)
    [0.4] Data sufficiency (≥ 200 trading days)

[1] Regime gate            — 200-DMA (4-week hysteresis)        → BULL / BEAR / BEAR-DEVELOPING
[2] Trend-strength gate    — ADX(14) weekly                     → RANGING / LIGHT / STRONG
[3] Volatility-state filter — Bollinger Squeeze on weekly        → NORMAL / SQUEEZE / SQUEEZE-RESOLVED
[4] Primary momentum       — ROC(26w, ex-1m) + RSI(14) weekly    → STRONG / PULLBACK / NEUTRAL / WEAK
[5] Confirmation           — MACD weekly + Bollinger position    → CONFIRMED / DIVERGENT / EXTENDED
[6] Sizing (ENTRY_ZONE only) — ATR(14) weekly                    → stop + position-size
[7] Output label + reasoning string
```

Pre-screen failures and gate halts produce specific labels (`SURVEILLANCE-HALT`, `REGIME-BEAR`, `RANGING-WAIT`, `SQUEEZE-PENDING`, etc.) with reasoning strings; the pipeline does not silently default to `WAIT`.

---

## 2. Pre-screening filters (Step 0)

### 2.1 ASM / ESM / T+T surveillance check
Source: NSE Surveillance (`https://nseindia.com/regulations/exchange-surveillance`).
- **T+T** (Trade-to-Trade) or **ESM Stage II** or **ASM Stage II** → halt with `SURVEILLANCE-HALT`. No ENTRY_ZONE signal generated.
- **ASM Stage I** or **ESM Stage I** → annotate `SURVEILLANCE-CAUTION`; continue pipeline.

### 2.2 Circuit-limit recent-event check
Source: NSE Bhavcopy EQ file — circuit-limit hits flagged per stock per day.
- IF any upper or lower circuit hit in the last 5 trading days → annotate `CIRCUIT-RECENT`; do NOT generate new ENTRY_ZONE signals for ≥ 5 days after the circuit hit. EXIT_WARNING signals are unaffected.

### 2.3 F&O monthly-expiry proximity check
- Applies only to daily-chart B2 confirmation signals (not weekly-chart B1 signals).
- IF daily-chart RSI / MACD / Stochastic signal generated within ±2 trading days of monthly F&O expiry Thursday → annotate `EXPIRY-PROXIMITY` and discard the daily signal; rely on weekly-chart equivalents only.

### 2.4 Data sufficiency
- Require ≥ 200 trading days (≈ 40 weeks) of price history for 200-DMA + 26-week ROC + 14-week ADX to be computable.
- IF insufficient → `INSUFFICIENT-DATA`. No signal output.

---

## 3. Step 1 — Regime gate (200-DMA, with 4-week hysteresis)

### 3.1 Formula
- Primary: SMA(200) on daily closes (or equivalent: SMA(40) on weekly closes).
- For consistency with the rest of v0.1, use the **40-week SMA on weekly closes** as the operative regime gate. Daily 200-DMA is computed as a tie-breaker if weekly-chart regime is ambiguous (price within ±2% of MA).

### 3.2 Decision logic + hysteresis

| Current regime | Condition | New regime |
|---|---|---|
| BULL or initial | Weekly close < 40-week MA for **4 consecutive weeks** | **BEAR** (transition) |
| BULL or initial | Weekly close < 40-week MA for 1–3 weeks | **BEAR-DEVELOPING** (no new ENTRY_ZONE; allow EXIT_WARNING) |
| BEAR | Weekly close > 40-week MA for **4 consecutive weeks** | **BULL** (transition) |
| BULL | Weekly close > 40-week MA | **BULL** (continue) |

### 3.3 Output actions
- **BEAR** → halt pipeline; output `AVOID_ENTRY: REGIME-BEAR`
- **BEAR-DEVELOPING** → no new ENTRY_ZONE; allow EXIT_WARNING signals to propagate
- **BULL** → continue to Step 2

### 3.4 Cycle A override hook (deferred to Cycle F)
For stocks where Cycle A's FA pipeline flags `FA-TURNAROUND` or `REVIEW-RECOVERY` (labels not yet defined; placeholder for Cycle F's signal combination), a `REGIME-OVERRIDE` annotation could allow ENTRY_ZONE generation despite BEAR regime. **v0.1 does NOT implement this** — it is a v0.2/Cycle-F design hook.

---

## 4. Step 2 — Trend-strength gate (ADX(14) weekly)

### 4.1 Formula
Wilder (1978) ADX(14) construction on weekly OHLC bars:
- `+DM = max(0, High_t − High_{t-1})`, suppressed if `+DM ≤ -DM`
- `-DM = max(0, Low_{t-1} − Low_t)`, suppressed if `-DM ≤ +DM`
- `TR = max(High − Low, |High − Close_{t-1}|, |Low − Close_{t-1}|)`
- `+DI = 100 × EMA(+DM, 14) / EMA(TR, 14)`
- `-DI = 100 × EMA(-DM, 14) / EMA(TR, 14)`
- `DX = 100 × |+DI − -DI| / (+DI + -DI)`
- `ADX = EMA(DX, 14)`

### 4.2 Decision logic

| ADX | Trend strength | Routing |
|---|---|---|
| < 20 | RANGING | Halt pipeline; output `WAIT: RANGING` |
| 20 ≤ ADX < 25 | LIGHT | Continue with **half-conviction** routing in Steps 4–5 |
| ≥ 25 | STRONG | Continue with **full-conviction** routing |

### 4.3 Directional consistency check
- IF `+DI > -DI` → bullish bias (consistent with BULL regime); continue.
- IF `-DI > +DI` AND regime = BULL → flag `REGIME-DI-CONFLICT`; continue but downgrade conviction by one level (FULL → HALF; HALF → no ENTRY_ZONE / WAIT).

---

## 5. Step 3 — Volatility-state filter (Bollinger Squeeze on weekly)

### 5.1 Formula
Standard Bollinger Bands on weekly closes:
- `Middle = SMA(20, weekly closes)`
- `σ = stdev(20, weekly closes)`
- `Upper = Middle + 2σ`, `Lower = Middle − 2σ`
- `Bandwidth = (Upper − Lower) / Middle`

### 5.2 Squeeze detection
- Compute 26-week rolling average of Bandwidth: `BW_avg_26w`
- **SQUEEZE active** when `Bandwidth < 0.30 × BW_avg_26w` (current bandwidth less than 30% of 6-month average)

### 5.3 Decision logic

| Squeeze state | Routing |
|---|---|
| Active (current week) | Halt pipeline; output `WAIT: SQUEEZE-PENDING` (annotate "large move expected in either direction") |
| Resolved upward (Squeeze cleared with weekly close above Upper band in past 4 weeks) | Continue with **annotated boost**: STRONG-MOMENTUM candidates get full-conviction even at LIGHT ADX |
| Resolved downward (Squeeze cleared with weekly close below Lower band in past 4 weeks) | Halt pipeline; output `AVOID_ENTRY: SQUEEZE-BROKE-DOWN` |
| NORMAL (no recent squeeze) | Continue to Step 4 normally |

---

## 6. Step 4 — Primary momentum (ROC + RSI confluence)

### 6.1 ROC(26-week, ex-last-4-weeks)
Following NSE Nifty 200 Alpha 30 methodology — exclude the most recent month to avoid short-term reversal contamination:

```
ROC_26w = (Price_{t - 4 weeks} − Price_{t - 30 weeks}) / Price_{t - 30 weeks} × 100
```

### 6.2 ROC ranking within NIFTY 100
Each evaluation date: rank all NIFTY 100 stocks by `ROC_26w` (descending). Categorize:

| Rank within NIFTY 100 | Class |
|---|---|
| 1–20 (top quintile) | **MOMENTUM-STRONG** |
| 21–60 (mid quintiles) | **MOMENTUM-MID** |
| 61–100 (bottom 2 quintiles) | **MOMENTUM-WEAK** |

### 6.3 RSI(14) weekly
Standard Wilder construction on weekly closes:
- `Gain_t = max(0, Close_t − Close_{t-1})`, `Loss_t = max(0, Close_{t-1} − Close_t)`
- `AvgGain_t = EMA(Gain, 14)`, `AvgLoss_t = EMA(Loss, 14)`
- `RS = AvgGain / AvgLoss`
- `RSI = 100 − 100 / (1 + RS)`

### 6.4 Combined momentum classification

| ROC class | RSI(14, weekly) | Combined class | Conviction default |
|---|---|---|---|
| MOMENTUM-STRONG | 40 ≤ RSI ≤ 70 | **STRONG-PULLBACK** | Full |
| MOMENTUM-STRONG | RSI > 70 | **OVERBOUGHT-MOMENTUM** | Half (check divergence) |
| MOMENTUM-STRONG | RSI < 40 | **INCONSISTENT-MOMENTUM** | Half |
| MOMENTUM-MID | 40 ≤ RSI ≤ 50 | **ENTRY-PULLBACK** | Full |
| MOMENTUM-MID | 50 < RSI ≤ 70 | **NEUTRAL-MOMENTUM** | Half |
| MOMENTUM-MID | RSI < 40 or RSI > 70 | **NOISY-MOMENTUM** | Halt → `WAIT: NOISY-MOMENTUM` |
| MOMENTUM-WEAK | Any | **WEAK-MOMENTUM** | Halt → `AVOID_ENTRY: WEAK-MOMENTUM` |

### 6.5 RSI divergence detection (12-week window)
For all classes except WEAK-MOMENTUM, look back 12 weeks:
- **BEARISH-DIVERGENCE**: price made a higher high but RSI made a lower high → if currently holding the stock, escalate to `EXIT_WARNING`; if not holding, downgrade conviction by one level.
- **BULLISH-DIVERGENCE**: price made a lower low but RSI made a higher low → maintain ENTRY candidate; annotate `BULLISH-DIVERGENCE` (modest positive signal, not used for upgrading conviction).

---

## 7. Step 5 — Confirmation (MACD weekly + Bollinger position)

### 7.1 MACD weekly (12, 26, 9)
- `MACD_line = EMA(12, weekly closes) − EMA(26, weekly closes)`
- `Signal_line = EMA(9, MACD_line)`
- `Histogram = MACD_line − Signal_line`

### 7.2 MACD histogram divergence (12-week window)
Same logic as RSI divergence in §6.5:
- **BEARISH-HISTOGRAM-DIVERGENCE**: price higher high + Histogram lower high → escalate to `EXIT_WARNING` (if held) or downgrade conviction one level (if not).
- **BULLISH-HISTOGRAM-DIVERGENCE**: price lower low + Histogram higher low → annotate; maintain candidate.

### 7.3 Bollinger position

| Where price sits relative to Bollinger Bands | Class |
|---|---|
| Between Middle and Lower (lower half of bands) | **POSITION-PULLBACK** (favorable for ENTRY) |
| Touches or below Lower band | **POSITION-MEAN-REVERSION** (favorable in confirmed BULL regime) |
| Between Middle and Upper (upper half) | **POSITION-RISING** (favorable only with STRONG-PULLBACK or ENTRY-PULLBACK) |
| Touches or above Upper band | **POSITION-EXTENDED** (no new ENTRY_ZONE; allow EXIT_WARNING) |

### 7.4 Combined routing (full conviction path)

| Momentum class | MACD histogram | Bollinger position | Output |
|---|---|---|---|
| STRONG-PULLBACK | positive and rising | PULLBACK or MEAN-REVERSION | `ENTRY_ZONE (full)` |
| STRONG-PULLBACK | positive and rising | RISING | `ENTRY_ZONE (full)` if no bearish divergence; else `WAIT` |
| STRONG-PULLBACK | positive and rising | EXTENDED | `WAIT: POSITION-EXTENDED` |
| STRONG-PULLBACK | negative or bearish divergence | any | `EXIT_WARNING` (if held); `AVOID_ENTRY` (if not) |
| ENTRY-PULLBACK | positive and rising | PULLBACK or MEAN-REVERSION | `ENTRY_ZONE (full)` |
| ENTRY-PULLBACK | positive | RISING | `ENTRY_ZONE (half)` |
| ENTRY-PULLBACK | negative | any | `WAIT: PULLBACK-CONTINUING` |
| OVERBOUGHT-MOMENTUM | positive (no divergence) | PULLBACK | `ENTRY_ZONE (half)` |
| OVERBOUGHT-MOMENTUM | bearish divergence | any | `EXIT_WARNING` (held); `AVOID_ENTRY` (not held) |
| INCONSISTENT-MOMENTUM | positive | PULLBACK or MEAN-REVERSION | `ENTRY_ZONE (half)` |
| INCONSISTENT-MOMENTUM | negative | any | `WAIT` |
| NEUTRAL-MOMENTUM | positive | PULLBACK | `ENTRY_ZONE (half)` |
| NEUTRAL-MOMENTUM | any other | any | `WAIT` |

### 7.5 ADX conviction modifier
- ADX = LIGHT (20 ≤ ADX < 25): any `ENTRY_ZONE (full)` is downgraded to `ENTRY_ZONE (half)`.
- ADX = STRONG (≥ 25): no modification.
- Special case: Bollinger Squeeze RESOLVED-UPWARD (§5.3) upgrades LIGHT-ADX full-conviction back to full.

---

## 8. Step 6 — Sizing (ATR(14) weekly)

Applied **only when output = ENTRY_ZONE (full or half)**.

### 8.1 ATR(14) on weekly
- `TR_t = max(High − Low, |High − Close_{t-1}|, |Low − Close_{t-1}|)` per weekly bar
- `ATR(14) = EMA(TR, 14)` (Wilder smoothing — equivalent to simple average for the first 14 periods, then `ATR_t = (13 × ATR_{t-1} + TR_t) / 14`)

### 8.2 Stop-loss placement
- `stop_multiplier` = 2.5 (default; B.4 will sweep 2.0 / 2.5 / 3.0)
- `stop_loss_price = entry_price − stop_multiplier × ATR_14_weekly`

### 8.3 Position size

```
risk_per_share = entry_price − stop_loss_price = stop_multiplier × ATR_14_weekly
per_stock_risk_budget = portfolio_NAV × 0.01    (1% per name, locked B.2)
position_size_shares = floor(per_stock_risk_budget / risk_per_share)
position_size_value = position_size_shares × entry_price
```

### 8.4 Half-conviction adjustment
- `ENTRY_ZONE (half)` → use half the per-stock risk budget: `per_stock_risk_budget = portfolio_NAV × 0.005`

### 8.5 Concentration cap
- IF `position_size_value > 0.05 × portfolio_NAV` (5% of NAV per name cap) → reduce `position_size_shares` to `floor(0.05 × portfolio_NAV / entry_price)`; annotate `CONCENTRATION-CAPPED`.
- This applies particularly to low-ATR stocks where 1% risk math otherwise allows excessive exposure.

---

## 9. Step 7 — Output label + reasoning string

### 9.1 Label set (4 labels, parallel to Cycle A)

| Label | Meaning |
|---|---|
| **ENTRY_ZONE (full)** | All gates passed; STRONG-PULLBACK or ENTRY-PULLBACK; favorable confirmation; full-size position recommended |
| **ENTRY_ZONE (half)** | Conditions favor entry but at reduced conviction; half-size position |
| **WAIT** | Some gate fails (RANGING / SQUEEZE / NOISY-MOMENTUM / POSITION-EXTENDED / PULLBACK-CONTINUING); no action |
| **AVOID_ENTRY** | REGIME-BEAR / WEAK-MOMENTUM / SQUEEZE-BROKE-DOWN / SURVEILLANCE-HALT |
| **EXIT_WARNING** | If currently holding: bearish divergence (RSI or MACD); regime transitioning to bear; POSITION-EXTENDED with overbought RSI |

### 9.2 Output structure (per stock per week)

```
Stock: HDFC Bank (NSE: HDFCBANK)
Date: 2024-03-29

PRE-SCREEN:
  - Surveillance: clean ✓
  - Circuit-recent: none in past 5 days ✓
  - F&O expiry proximity: 9 days from monthly expiry (no impact on weekly signal) ✓
  - Data sufficient: 1,247 days ✓

REGIME (Step 1):
  - 40-week MA = ₹1,612 ; weekly close = ₹1,700
  - Weeks above MA: 18 consecutive → BULL ✓

TREND STRENGTH (Step 2):
  - ADX(14, weekly) = 27 → STRONG
  - +DI = 28.4 ; -DI = 19.1 → bullish bias (consistent with regime) ✓

VOLATILITY STATE (Step 3):
  - Bollinger bandwidth = 0.087 ; 26-week avg = 0.092 → ratio 0.95 → NORMAL ✓

PRIMARY MOMENTUM (Step 4):
  - ROC(26w, ex-1m) = 18.4% → rank 18 of 100 → top quintile → MOMENTUM-STRONG
  - RSI(14, weekly) = 52 → in 40–70 band
  - Combined: STRONG-PULLBACK
  - RSI divergence check: no divergence detected in 12-week window

CONFIRMATION (Step 5):
  - MACD histogram = +0.34 ; rising (vs. +0.21 prior week) ✓
  - Bollinger position: price ₹1,700 between Middle (₹1,680) and Lower (₹1,562) → POSITION-PULLBACK
  - MACD divergence: no
  - Routing: STRONG-PULLBACK + positive rising MACD + POSITION-PULLBACK → ENTRY_ZONE (full)
  - ADX conviction modifier: STRONG, no downgrade

SIZING (Step 6):
  - ATR(14, weekly) = ₹48
  - stop_loss = ₹1,700 − 2.5 × ₹48 = ₹1,580
  - risk_per_share = ₹120
  - per_stock_risk_budget = 1% × ₹1,00,00,000 = ₹1,00,000
  - position_size_shares = floor(₹1,00,000 / ₹120) = 833
  - position_size_value = 833 × ₹1,700 = ₹14.16 lakhs (1.42% NAV — within 5% cap ✓)

OUTPUT: ENTRY_ZONE (full conviction)

REASONING:
  HDFC Bank is in a confirmed BULL regime (price above 40-week MA for 18 weeks). The trend is
  strong (ADX 27 with bullish DI bias). Volatility is normal — no squeeze pending. Momentum
  is at the top of NIFTY 100 by 26-week ROC (rank 18), and the weekly RSI at 52 indicates a
  healthy pullback within the uptrend (not overbought). MACD histogram is positive and rising,
  confirming the momentum, and price sits in the lower half of the Bollinger Bands, favorable
  for entry. ATR-based stop at ₹1,580; position sized to ₹14.16 lakhs representing 1% portfolio
  risk per name.
```

---

## 10. Combined display with Cycle A FA output

Per Q5 locked in v0.4 problem statement: when Cycle A (FA) and Cycle B (TA) outputs disagree, surface both labels side-by-side with reasoning. Do NOT silently combine into a single label.

### 10.1 Conflict matrix (4 × 4 — Cycle A label × Cycle B label)

|  | Cycle B: ENTRY_ZONE | Cycle B: WAIT | Cycle B: AVOID_ENTRY | Cycle B: EXIT_WARNING |
|---|---|---|---|---|
| **Cycle A: HOLD** | Agree: positive entry | Mild conflict | Conflict | Mild conflict |
| **Cycle A: WATCH** | Mild conflict | Mild conflict | Agree: cautious wait | Agree: warning |
| **Cycle A: REVIEW** | **Strong conflict** | Mild conflict | Agree: avoid | Agree: review for exit |
| **Cycle A: FLAG** | **Strong conflict** | Conflict | Agree: avoid | Conflict: exit candidate |

### 10.2 Display logic
- **Agree**: present unified action with both labels in the reasoning.
- **Mild conflict**: surface both labels with holding-period framing per Q5.
- **Strong conflict** (e.g., Cycle A FLAG + Cycle B ENTRY_ZONE): explicit conflict marker; default behavior = HALF-CONVICTION entry only with explicit user confirmation; both reasoning strings shown.

### 10.3 Holding-period framing (locked Q5 default)
For any conflict case:
- **Long-term (B1, multi-year hold)**: Cycle A dominates. FA labels are about company quality; ignoring REVIEW/FLAG for technical reasons is the classic value-trap mistake.
- **Tactical (B2, swing entry within an already-fundamentals-validated position)**: Cycle B dominates for entry timing only; not for thesis.
- **New position decision**: default to the more conservative label. WATCH + ENTRY_ZONE → take ENTRY_ZONE at half conviction. WATCH + AVOID_ENTRY → AVOID_ENTRY.

### 10.4 v0.1 scope note
The combined display in v0.1 is a **display rule** — not a math combination. The actual math for combining Cycle A and Cycle B signals into a single composite (e.g., weighted scoring, conditional logic) is **Cycle F (signal combination)** work. v0.1 surfaces both labels in parallel with a default conflict-resolution rule; Cycle F replaces this with formal math.

---

## 11. What v0.1 explicitly does NOT do (deferred)

| Deferred to | Item |
|---|---|
| Cycle B v0.2 | 52-week breakout / Donchian channel as separate signal (overlaps with ROC; defer until B.4 shows whether ROC alone is sufficient) |
| Cycle B v0.2 | OBV / delivery-volume divergence overlay |
| Cycle B v0.2 | AVWAP anchored to events as data-enrichment reference |
| Cycle B v0.2 | Supertrend (redundant with ATR + EMA in v0.1; revisit if v0.1 underperforms in B.4) |
| Cycle B v0.3 | Sector-relative ROC (rank within sector vs rank within NIFTY 100) |
| Cycle D | Portfolio-level concentration math (no two correlated NIFTY 100 names enter ENTRY_ZONE simultaneously) |
| Cycle E | Exit rule formalization beyond initial stop (trailing stop framework, time-based exits, fundamental-deterioration exits) |
| Cycle F | Math for combining Cycle A + Cycle B into a single composite (currently a display rule + holding-period default) |

---

## 12. What v0.1 explicitly does NOT see (acknowledged blindspots)

Same kind of disclosure as Cycle A's W6 meta-finding. TA can't see:

| Blindspot | Should be handled in |
|---|---|
| Fundamental deterioration that hasn't yet shown in price | Cycle A (FA) — that's its job |
| Corporate-event surprises (results miss, fraud, regulatory action) | Out of scope for systematic math; rapid EXIT_WARNING when price reacts |
| Macro regime changes (rate cycle inflection, currency stress, geopolitics) | Future Cycle (not currently planned); manual overlay |
| Liquidity-event flows (FII selling, MF redemption pressure) | Partially in Cycle D (sizing); fully visible only with order-book data (out of scope) |
| Forward earnings expectations | Cycle A v0.2 candidate (P/E percentile, forward estimates) |

---

## 13. Open questions for B.4 testing

### Q1 — Test universe
Default: **6 NIFTY 100 stocks across regime + sector dimensions**:
- HDFC Bank (large bank, bull-trending)
- Reliance Industries (conglomerate, multiple regimes)
- Infosys (IT, secular growth + cyclical)
- Tata Steel (commodity cyclical — also tested in Cycle A; cross-cycle interaction)
- ITC (defensive consumer staple)
- Maruti Suzuki (auto cyclical, large-cap)

Alternative: Pranav suggests 4–6 specific stocks instead.

### Q2 — Test time-points
Default: **6 regime-distinct windows**:
- 2008-10 (GFC bottom)
- 2014-06 (election rally early)
- 2018-09 (NBFC crisis / IL&FS)
- 2020-03 (COVID bottom)
- 2022-06 (rate-hike cycle mid-point)
- 2024-03 (recent regime)

Apply the v0.1 pipeline at each date; observe forward 6 / 12 / 24-month price action.

### Q3 — Pass / fail criteria
- ENTRY_ZONE signals should be net positive on forward 6–12 month basis (~60% hit rate target — same bar as a strong-discretionary investor; not Sharpe > 0.3, that's the Q12 walk-forward bar reserved for productionization).
- AVOID_ENTRY signals on regime-bear should avoid the worst drawdowns.
- Stop-loss-out frequency should average < 25% of ENTRY_ZONE entries (>35% would indicate stops are too tight).
- The label sequence over each regime window should match the actual regime trajectory (e.g., signals should turn AVOID_ENTRY before March 2020 crash, then ENTRY_ZONE by mid-2020 recovery).

This is a *qualitative* sanity check, not a full walk-forward backtest.

### Q4 — Compute method
- (a) Hand-compute from NSE bhavcopy + corporate-action data — slow, high-fidelity, ~2 stocks per hour
- (b) Python + pandas + ta-lib for indicator math — fast, fidelity depends on data source

Default: **(b)** with spot-check against (a) for 1–2 stocks to validate data accuracy.

### Q5 — Cycle A integration in B.4 tests
At each evaluation date for each test stock, also look up the Cycle A label and exercise the combined-display logic from §10. Verify conflict cases produce sensible output. No math combination is being tested — only the display + default resolution rule.

---

## 14. What we expect critics to attack in B.5

Pre-empting the multi-agent critique step:

### Quant lens
- Thresholds (200-DMA confirmation = 4 weeks; ADX zones at 20/25; ROC quintile cutoffs; ATR multiplier 2.5) are defaults from B.1 literature, not optimized on NSE data. Need parameter-sensitivity analysis.
- Compositional independence — are 7 indicators actually independent, or do ROC / MACD / RSI all measure overlapping momentum?
- No walk-forward Sharpe evidence yet — Q12 gate is unaddressed by v0.1 design.
- Boundary cases at threshold edges (RSI = 40 vs 41; ROC rank 20 vs 21) — discrete labeling on continuous signals.

### Behavioral lens
- ENTRY_ZONE label invites action; WAIT will be ignored; EXIT_WARNING will be acted on with urgency. Same Cycle A label-incites-action problem.
- 4 labels × 100 stocks × weekly = 400 outputs/week is visual overload. Delta-view (per Cycle A v0.2) probably needed for v0.2.
- Cycle A/B conflict surfacing assumes thoughtful user engagement — most retail investors will pick the label that supports their existing bias.
- Stop-loss at 2.5 × ATR can be a 7–10% drop before stopping out; retail psychology may not tolerate this drawdown without intervention.

### Retail-user lens
- "ENTRY_ZONE (half)" — what does the user actually do with half-conviction? Mental model is binary.
- For already-held positions: v0.1 only generates EXIT_WARNING on divergence/regime transition. There's no "manage existing position" mode (trailing-stop adjustment, partial-profit-take) — that's Cycle E.
- "1% per-name risk budget" expressed as a stop-distance and share count is not intuitive for retail; needs UX explanation.
- Cycle A's "WATCH (3 quarters stable)" alongside Cycle B's "ENTRY_ZONE (full)" — investor lacks the framework to integrate, may default to whichever is more emphatic.

### Signal-engineer lens
- Walk-forward Sharpe > 0.3 requires real backtest infrastructure; v0.1 math has no hooks for this. Cycle E or a separate cross-cycle infrastructure cycle will need to address.
- Parameter ranges — single-point math; need methodical sweep design for B.4.
- Indicator inter-correlation analysis is absent — should compute pairwise correlation of the 7 signals on a NIFTY 100 historical sample to verify they're not redundant.
- Survivorship bias: testing on current NIFTY 100 constituents misses companies that fell out of the index (which often coincides with TA-detectable deterioration).

### NSE-specific lens
- Corporate action handling (splits / bonuses / demergers) — ROC and 200-DMA depend on adjusted prices; verify data source quality.
- FII / DII block deals — distort weekly OBV/volume signals (not in v0.1 but principle applies to RSI/MACD on heavy block-deal days).
- NIFTY 100 composition changes — when a stock enters NIFTY 100 mid-period, does its ROC-quintile rank get re-baselined or held constant against the historical NIFTY 100?
- Bollinger Squeeze threshold (30% of 6-month average) — purely heuristic; not validated on NSE data.
- ASM/ESM/T+T data sourcing — NSE publishes these but the historical record is incomplete pre-2017.

---

## 15. Sources

All citations in `20_cycle_B_research.md`. Key for v0.1 specifically:
- **Wilder (1978)** — primary for RSI, ATR, ADX/DMI construction
- **Appel (1979)** — primary for MACD
- **Bollinger (1983)** — primary for Bollinger Bands
- **Faber (2007), J. Wealth Mgmt** — 200-DMA as tactical regime filter
- **Naik & Reddy (2019, SSRN)** — only NSE walk-forward Sharpe > 0.3 evidence on ADX-filtered momentum
- **NSE Nifty 200 Alpha 30 methodology** — ROC(26w, ex-1m) construction
- **Capitalmind (Deepak Shenoy, 2016)** + **Freefincal** — 200-DMA NSE practitioner evidence
- **Bhat & Naik (2020, IIM Kozhikode)** — multi-timeframe alignment evidence (basis for B1/B2 framing)

---

**End of v0.1 spec.** Awaiting Pranav's approval on B.4 testing scope (Q1–Q5 in §13) before launching B.4.
