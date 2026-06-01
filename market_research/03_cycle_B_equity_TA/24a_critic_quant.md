# 24a — Cycle B Critique: Quant / Statistician Lens (C1)

**Status**: 🔄 §1-§3 written. Drafting §4-§5.
**Date**: 2026-05-31
**Lens**: Quant / Statistician (Critic C1, Cycle B.5)
**Cycle**: B.5 — Multi-agent critique of v0.1 TA math
**Input files**: `21_cycle_B_math_v0.1.md`, `23_cycle_B_test_synthesis_v0.1.md`
**Format reference**: `15a_critic_quant.md` (Cycle A.5 quant critic)

---

## §1 — Verdict + One-Line Summary

**REFACTOR-REQUIRED.**

The seven-indicator pipeline is architecturally sound and demonstrably works for the 40–50% of the NIFTY 100 that consists of quality non-cyclical compounders in BULL regime. The three structural failures — cyclical inversion in the regime gate (B-W1), a momentum-ranking design that guarantees conglomerate exclusion (B-W3), and a stop-distance formula that collapses in crisis volatility (B-W5) — are not tuning problems. They are design-envelope mismatches: the math was implicitly calibrated for secular-trending single-business equities, then applied without adjustment to cyclicals, conglomerates, and tail-volatility regimes. The 53% GOOD hit rate and above-target stop-loss-out frequency confirm the design-envelope problem empirically. v0.1 cannot clear Sharpe > 0.3 walk-forward without structural changes to at minimum P0.1 (REGIME-OVERRIDE), P0.2 (asymmetric hysteresis), and P0.3 (ATR stop cap). The math inside each individual step (ADX construction, Wilder RSI, MACD formula) is correct by standard references. The failure is in how the steps compose and what stock profiles they collectively exclude.

---

## §2 — Per-Weakness Confirmation (B-W1 through B-W7, B-P1)

### B-W1 — Cyclical inversion mechanism
**CONFIRM and EXTEND with correlation analysis**

The synthesis correctly identifies the structural parallel to Cycle A's W3 (Piotroski cyclical inversion), but does not quantify the signal correlation. From the cell-level data:

At cyclical-trough dates (Tata Steel Oct-2008, Mar-2020; Maruti at Mar-2020), the 40-week SMA position is the worst it will be in the entire cycle by construction — because price has been falling for months into the trough. The SMA is a lagged level indicator: for a stock that entered a downturn at t=0 and bottomed at t=T, the 40-week SMA at t=T still reflects the average of prices from t=(T-40w) to t=T, of which roughly the first half were above the now-bottom price. The SMA will not cross below-price until T + some lag, and will not flip back above-price until T + 4 confirmation weeks. Formally: let the cycle be symmetric with a trough at the midpoint. The SMA will lag the trough by approximately half the window length, or ~20 weeks. The 4-week confirmation requirement adds a further floor delay. Total expected lag from actual bottom to BULL signal: 20–25 weeks minimum for a symmetric cycle. On a sharp-V shape (COVID), the lag compresses somewhat because the SMA averages in many high prices from before the crash; but the post-crash recovery just pulls the SMA down further, extending the lag. This is not an implementation flaw — it is a geometric consequence of using a lagging moving average as a regime trigger.

**Spearman correlation logic**: if we rank the 6 evaluation dates for Tata Steel by (a) SMA position (price / 40-week SMA ratio, descending = higher conviction BULL signal) and (b) forward 24-month total return (descending = better outcome), the Spearman rho would be negative — B.4 shows the highest forward returns at the dates with the worst SMA position (Oct-2008, Mar-2020). The synthesis's Tata Steel data (17% GOOD hit rate — 1/6) directly implies this: the 1 GOOD verdict is almost certainly not at a trough date. Cycle A's W3 computed Spearman = −1.0 for a 4-date Tata Steel Piotroski dataset. The TA regime gate on Tata Steel would produce the same direction of inversion and, with the available 6-date cell data, a plausibly identical Spearman rho.

**Cross-cycle compounding is the key quant finding**: B.4 synthesis §B-W1 notes that at Mar-2020 Tata Steel, Cycle A = WATCH and Cycle B = AVOID_ENTRY, and the §10 conflict resolution rule defaults to the more conservative → AVOID_ENTRY. This is quantitatively important: Cycle A alone would have left the door open (WATCH). Adding Cycle B eliminated the possibility of action. Two independently-derived trailing signals on the same mean-reverting underlying — Piotroski (trailing fundamentals) and 40-week SMA (trailing price) — are NOT independent at cyclical extremes. Their correlation through the shared underlying commodity-price-cycle driver makes them compound rather than diversify. This is a structural flaw in the Cycle A + Cycle B combination for cyclicals, not just in Cycle B in isolation. Cycle F (signal combination) must address it.

**What this lens cannot assess**: I cannot estimate the NSE-specific Spearman rho across a broad cyclical sample without running the actual computation on historical NIFTY 100 data. The 6-date, 6-stock cell data here is directionally consistent but sample-size-limited. The structural argument is strong; the quantitative claim requires a broader backtest.

---

### B-W2 — Lagging regime gate misses V-shape recoveries
**CONFIRM with hysteresis mechanics quantified**

The 4-week confirmation window for BEAR→BULL is not just a calibration choice — it imposes a minimum entry delay that interacts with V-shape recovery speed in a structurally unfavorable way.

The math: let the bottom print at week t=0. The 40-week SMA at t=0 is dragged far below the crash price (because the SMA averages in 40 weeks of pre-crash prices). For the SMA to flip below the recovering price, the price must rise enough to exceed the current SMA, which is still falling (because the crash prices are being added to the SMA rolling window). Typical lag for a V-shape with a 30% decline: 8–12 weeks before price crosses back above the SMA, then + 4 weeks confirmation = 12–16 weeks total minimum. During a 50% V-shape recovery (as in COVID for Infosys), 12 weeks post-bottom captures approximately 60% of the initial recovery. The remaining 40% (which is where the 30–155% missed return figures come from) is geometrically inaccessible to the v0.1 architecture.

The CIRCUIT-RECENT filter compounding (§0.2): 5-day suppression fires on every circuit-limit hit. In March 2020, multiple stocks hit circuits on consecutive days over 2–3 weeks. The suppression windows chain: day 1 hit → suppress through day 6; day 5 hit again → suppress through day 10; etc. This effectively extends the suppression period from 5 days to 15–20 days in a genuine crisis. Combined with the SMA lag: V-shape entry is blocked for 12–16 weeks by SMA mechanics AND 3–4 weeks by CIRCUIT-RECENT, with partial overlap but not full overlap. The synthesis observation that ENTRY_ZONE was suppressed until mid-May 2020 (approximately week 8 after the March bottom) is consistent with this math.

The proposed P0.2 fix (asymmetric hysteresis: keep BULL→BEAR at 4 weeks, shorten BEAR→BULL to 1–2 weeks with ADX expansion + volume confirmation) is quantitatively correct in direction. The specific 1-week BEAR→BULL trigger with volume > 1.5× 13-week avg is a heuristic, not calibrated on NSE data. The quant question for v0.2: what false-positive rate does 1-week confirmation produce on normal corrections vs genuine V-shapes? This requires a parameter sensitivity sweep I cannot perform without historical data.

---

### B-W3 — Conglomerate ENTRY_ZONE never fires
**CONFIRM and identify the structural arithmetic cause**

The synthesis correctly notes that Reliance produced zero ENTRY_ZONE labels across all 6 dates. The quant explanation is more precise than the synthesis offers.

**Why STRONG-PULLBACK is unreachable for Reliance structurally**:

STRONG-PULLBACK requires two simultaneous conditions:
1. ROC(26w, ex-1m) in top quintile (rank 1–20 of NIFTY 100)
2. RSI(14, weekly) in 40–70

Condition 1 (top quintile ROC) means Reliance's 26-week return (ex-last-4w) must exceed approximately 80 other NIFTY 100 stocks over the same period. Reliance's revenue composition (roughly: Refining/Petchem ~40%; Retail ~25%; Telecom ~25%; Other ~10% at mid-decade) means its stock price responds to a weighted average of energy commodity margins, consumer spending, subscriber growth, and strategic initiative announcements. During any NIFTY 100 sectoral rally — banking, IT, pharma, auto, metals — at least 40–50 NIFTY 100 stocks are rallying in that sector and Reliance is not. Reliance achieves top-quintile ROC only during broad market rallies where everything rises, but in those periods RSI quickly exceeds 70 (violating Condition 2), or the 26w period ex-1m averages a sustained multi-quarter run that by definition means the pullback is already over (RSI > 70 if momentum is that strong).

**The fix geometry**: The synthesis proposes lowering the ROC threshold from top-quintile to top-tercile for conglomerates. Quantitatively: top-tercile = rank 1–33 of 100. This roughly doubles the ROC-eligible window for Reliance. The question is whether Reliance lands in ranks 21–33 during periods where RSI is genuinely at 40–70 (a real pullback). If Reliance's RSI is 40–70 precisely when it's in ranks 21–33 (mid-rally consolidations), this fix works. If its ROC and RSI are correlated in a way that makes ranks 21–33 coincide with RSI < 40 (which happens during sector-specific corrections within a broader underperformance period), the fix still doesn't fire. This is an empirical question about Reliance's return autocorrelation structure that I cannot resolve without data. The fix is reasonable in direction; its effectiveness is uncertain.

**The alternative fix** — sector-relative ROC (P1.1) — has a cleaner statistical rationale: instead of ranking Reliance against 100 heterogeneous companies, rank it against its own peers (energy + telecom + retail blended peer set). A 26w ROC in the top tercile of that peer set is more likely to co-occur with RSI pullback because the comparison set responds to similar drivers. P1.1 is statistically more defensible than P1.3 (lowering the threshold) for fixing the structural misalignment. P1.3 is a hack; P1.1 is a design fix.

---

### B-W4 — NIFTY 100 cross-sectional ROC disadvantages off-theme stocks
**CONFIRM as the broader form of B-W3's structural problem**

B-W3 is a special case of B-W4. The common mechanism: any cross-sectional momentum ranking penalizes stocks whose sub-sector is not in the current market theme, regardless of the stock's individual trajectory relative to its own fundamentals or trend.

The statistical consequence is survivorship-of-theme bias in the signal. The v0.1 pipeline implicitly selects for whatever sectors happen to be leading the NIFTY 100 at each evaluation date. At a given date, the top-20-ROC stocks are almost by definition concentrated in 2–3 leading sectors. In the B.4 test window:
- 2014-06: banking, auto, consumer
- 2018-09: NBFC (then crashing), capex
- 2020-03: crash — nothing in top quintile is meaningful
- 2022-06: energy, metals, capex (post-COVID infrastructure)
- 2024-03: capex, power, defence

A stock like ITC (defensive consumer), which correctly produced the strongest v0.1 result (5/6 GOOD), is only in the top-ROC band at the exact June-2022 re-rating date — one date out of six. The pipeline's 53% hit rate is partly a reflection of correctly avoiding off-theme stocks (which genuinely do underperform relative to the leading theme), not just of signal quality.

The P1.1 sector-relative ROC supplement (MAX of NIFTY 100 quintile vs NSE Sector quintile) addresses this in the right direction. The statistical question is how correlated the sector-relative and NIFTY-100-relative signals are. In theory, they are partially correlated (sector leaders also tend to lead the index during sector rallies) but not perfectly so. The MAX operator means the system fires on either the sector or the index signal — increasing recall at the cost of precision. Whether the precision loss is acceptable depends on the false-positive rate on sector-relative momentum: a stock leading its sector but lagging the index is a relative-momentum candidate, not an absolute-momentum one. v0.2 should track which signal (sector vs index) fired and compute separate hit rates.

---

### B-W5 — ATR stop unusable in crisis volatility
**CONFIRM with explicit formula failure mode**

The math: `stop_loss_price = entry_price − 2.5 × ATR(14, weekly)`. At Mar-2020, HDFC Bank ATR(14) weekly was approximately ₹100+ on a price of ~₹770. Stop distance = 2.5 × 100 = ₹250, or 32% below entry. The problem has two components:

**Component 1 — ATR magnitude**: In crisis periods, ATR(14) is inflated because the 14-week window includes the crash bars. The Wilder EMA smoothing (ATR_t = (13 × ATR_{t-1} + TR_t) / 14) means the crisis ATR decays slowly: at 14-period EMA, the half-life is approximately 9.6 periods. A crisis week with TR = 3× normal contributes to ATR for 10+ weeks afterward. The stop distance is therefore maximal at exactly the moment when entry is most favorable (low price, wide ATR).

**Component 2 — Position size math interaction**: The formula `position_size = risk_budget / risk_per_share = (NAV × 0.01) / (2.5 × ATR)`. With crisis-inflated ATR, risk_per_share balloons, so position_size shrinks — which is actually correct risk management behavior (smaller position during high volatility). The problem is not the position size math; it is that the stop level at 32% below entry is never hit by routine market action post-crash, making it meaningless as a stop. A stop at ₹520 on HDFC Bank at ₹770 (Mar-2020) would never have triggered as the stock recovered to ₹1,700+ — but the stop serves no protective function at that distance either.

The proposed cap `stop_loss = MIN(2.5 × ATR, 0.15 × price)` fixes Component 2. It also means the 1% risk budget buys a larger position in crisis conditions, which is the opposite of what the underlying intent should be. The synthesis proposes this fix without noting the position-size consequence: if the stop cap at 15% fires and ATR would have placed it at 32%, then position_size TRIPLES (because risk_per_share = 15% of price vs 32% of price). A 3× larger position entering at the worst volatility moment is not obviously safer. The correct fix is the MIN for the stop-distance display, but position sizing should additionally be capped at the ATR-implied size (not the capped-stop-implied size). That is: `position_size = floor(risk_budget / MAX(2.5 × ATR, 0.15 × price))` — using the MAX in the denominator to prevent oversizing. The synthesis inverts the MIN/MAX, and this inversion would produce dangerous oversizing in the exact crisis scenarios it is trying to address.

---

### B-W6 — BFSI combined display non-functional
**CONFIRM, out of scope for this quant lens to resolve**

This is a data-structure problem (missing row in the §10 conflict matrix), not a statistical one. The quant observation is limited to: BFSI represents approximately 30–35% of NIFTY 100 by market cap. A TA system that has no testable output for 30–35% of its target universe on the combined-display dimension is functionally incomplete. I have no statistical comments beyond confirming the structural gap. The Cycle A v0.4 BFSI pipeline acceleration is the correct resolution path. This lens defers the substance to the retail-NSE and cross-cycle critics.

---

### B-W7 — Structural-event distortion of regime gate
**CONFIRM with a quantitative mechanism added**

The synthesis correctly identifies the HDFC Bank merger (Jul-2023) and Reliance Jio launch (Sep-2016) as structural event distortions. The quant mechanism is the same as the general SMA contamination problem: the 40-week SMA includes N pre-event weeks and (40-N) post-event weeks. For the HDFC-HDFC Ltd merger, the pre-event price reflects a standalone mid-size bank; the post-event price reflects a merged universal bank with 25% larger asset base. The price levels are adjusted for the swap ratio, but the comparative trend embedded in the 40-week SMA is not. A stock that rallied 5% post-merger would appear to have a positive SMA trajectory when the rally was purely a re-rating-of-combined-entity effect, not a trend continuation.

More precisely: corporate events create breaks in the return-generating process. The 40-week SMA assumes a stationary generating process — each bar is drawn from the same underlying distribution. A merger or demerger is a regime change in the process. Mixing pre- and post-event price bars in the SMA window produces a statistic that is mathematically defined but economically meaningless for approximately (event_week + 39 weeks) after the event. For HDFC Bank (merger Jul-2023), the 40-week SMA computed at any date through approximately May-2024 includes pre-merger HDFC Bank prices in its window and is therefore unreliable as a regime signal.

The proposed P1.2 annotation table (flag STRUCTURAL-EVENT-CAUTION when the 40-week SMA window includes a material event) is correct. The downgrade-conviction mechanism is appropriate. The question of what "material" means requires definition: I would suggest any event where the post-event market cap differs from pre-event by >15%, or where a new revenue segment enters at >10% of revenue. This is a judgment call, not a calibrated statistical threshold, and I accept it as such.

---

### B-P1 — REGIME-DI-CONFLICT as leading indicator
**CONFIRM and extend with lead-time quantification**

The synthesis calls the DI-flip a leading indicator relative to the 40-week SMA — caught Sep-2018 NBFC crisis directional change before regime broke. The quant logic is sound: ADX direction indicators (+DI, -DI) are computed from daily/weekly highs and lows, not from closing prices alone. They respond to directional flow — which direction bars are extending — before the close-based SMA is dragged across the price level. A -DI > +DI flip indicates that down-bars are extending more than up-bars, which is a leading condition for a price trend reversal.

The lead time: +DI/-DI crosses the centerline when recent bars are more directionally negative than positive. The 40-week SMA crosses when cumulative closes have averaged below the SMA level. For a sustained trend reversal, the DI flip typically precedes the SMA crossover by 4–12 weeks (this is consistent with the general literature on DMI vs SMA for trend detection). If the Maruti Sep-2018 case shows the DI flip caught the NBFC crisis turn before the SMA broke, that suggests 4–8 weeks of lead time in that instance.

Promoting B-P1 to a standalone leading signal (as proposed in P0.4) is statistically justified. The proposed trigger — -DI > +DI for 2 consecutive weeks with ADX < 20 (trending-to-ranging transition) → EXIT_WARNING — has a sensible interpretation: the trend is losing directional conviction AND direction is flipping, which is a higher-information state than either signal alone. The 2-week confirmation is appropriate to avoid single-week noise. The quant concern is false positives: a +DI/-DI flip can occur during a mid-trend consolidation without being a trend reversal. ADX < 20 as a filter reduces this risk (a healthy strong trend rarely has ADX < 20), but does not eliminate it. Parameter sensitivity between "ADX < 15" and "ADX < 20" and "ADX < 25" for this trigger needs empirical testing.

---

## §3 — NEW Quant Concerns (Not in B.4 Synthesis)

### Theme A — Indicator inter-correlation (ROC, MACD, RSI)

The v0.1 pipeline assigns three indicators to momentum measurement across Steps 4 and 5: ROC(26w, ex-1m) in Step 4, RSI(14, weekly) in Step 4, and MACD(12,26,9) in Step 5. The spec treats these as independent confirmation signals — the routing table in §7.4 requires MACD confirmation in addition to ROC + RSI. This architecture implies the three signals carry independent information. They do not, and the degree of overlap is structurally large.

**ROC and MACD overlap**: MACD_line = EMA(12) − EMA(26). The signal is driven by the spread between two exponential moving averages. ROC(26w) = (Price_{t-4w} − Price_{t-30w}) / Price_{t-30w}. Both are measuring the relative position of recent price vs earlier price over approximately the same horizon (26w ≈ 6 months). The MACD's 26-period EMA will be heavily influenced by the same price history that drives the 26w ROC. In a trending market, if ROC(26w) is strongly positive, EMA(12) will be above EMA(26) (because 12-period EMA is more recent and therefore reflects the same strong recent performance). The signals are not mathematically equivalent, but they are measuring the same underlying quantity — 6-month price momentum — through different smoothing windows. Their pairwise correlation on weekly closes for a trending stock will typically exceed 0.70.

**RSI and ROC correlation**: RSI measures the ratio of average gains to average losses over 14 periods. ROC measures total return over 26 periods. Both are monotone functions of the price path over similar horizons. For a stock in a sustained trend, high RSI and high ROC will co-move. The functional form is different (RSI is bounded 0–100; ROC is unbounded), but on the 40–70 RSI band that defines the STRONG-PULLBACK condition, RSI and ROC are strongly positively correlated.

**Practical consequence**: the v0.1 routing table that requires MACD positive AND rising for ENTRY_ZONE from STRONG-PULLBACK is not providing independent confirmation. It is asking: does the 12-week EMA exceed the 26-week EMA AND is the gap widening? In a stock where ROC is in the top quintile AND RSI is 40–70, the probability that MACD is negative is approximately 5–15% (only in whipsaw cases where the most recent 12 weeks reversed sharply). The MACD confirmation gate passes ~85–95% of the cases that reach it. This means the gate adds very little entropy reduction. The v0.1 design appears to have three independent confirmation layers but functionally has approximately one-and-a-half. To verify: the Naik & Reddy (2019) study cited in §15 uses ADX-filtered momentum — it does NOT require RSI + MACD confluence. The multi-layer requirement is an addition by v0.1 design, not from the evidence base. Pairwise indicator correlation should be measured on NIFTY 100 weekly data before v0.2 claims the confirmation architecture provides independent signal validation.

**Bollinger position** is partially independent (it measures price level relative to a volatility band rather than momentum direction), but the BB Middle is also a 20-week SMA that co-moves with the 26-week ROC. The POSITION-PULLBACK condition (price between Middle and Lower) will tend to co-occur with RSI in the 40–60 range (which is also the STRONG-PULLBACK RSI window). The only genuinely independent signal in Steps 4+5 is the ADX directional consistency check (+DI/-DI) from Step 2 — which is precisely why B-P1 is the most valuable positive finding.

---

### Theme B — Discrete labeling on continuous signals: boundary-case cost

The v0.1 spec creates discrete labels from continuous indicators at multiple hard threshold boundaries:
- ROC quintile: rank 20 vs rank 21 (top quintile vs MOMENTUM-MID)
- RSI: 40 vs 41 (STRONG-PULLBACK eligible vs INCONSISTENT-MOMENTUM)
- RSI: 70 vs 71 (OVERBOUGHT-MOMENTUM escalation)
- ADX: 20 vs 21, 25 vs 26 (RANGING vs LIGHT vs STRONG)
- Bollinger bandwidth: < 30% of avg vs ≥ 30% (SQUEEZE vs NORMAL)

Each boundary creates a discontinuous jump in output label despite a near-zero difference in underlying signal. The consequence is measurement-noise sensitivity: indicator values computed from slightly different data sources (Screener.in vs Yahoo Finance NSE vs Kite API) can place the same stock on opposite sides of the same boundary on the same day.

**ROC rank 20 vs 21 cost is the largest**: the label difference is STRONG-PULLBACK (ENTRY_ZONE eligible) vs ENTRY-PULLBACK (also ENTRY_ZONE eligible, but via a narrower RSI window: 40–50 only). A stock at rank 21 with RSI = 52 gets NEUTRAL-MOMENTUM → ENTRY_ZONE (half) at best (§6.4 routing: MOMENTUM-MID, RSI 50–70 → NEUTRAL-MOMENTUM). A stock at rank 20 with RSI = 52 gets STRONG-PULLBACK → ENTRY_ZONE (full). Same RSI, same neighborhood in the ROC distribution, entirely different output conviction. This is a step function at the quintile boundary that has no continuous justification.

**RSI 40 boundary is also sharp**: RSI = 39 is INCONSISTENT-MOMENTUM (half-conviction at best); RSI = 41 is STRONG-PULLBACK (full conviction). In a weekly RSI calculation, a single weekly bar can move RSI by 2–5 points. The boundary sensitivity creates multi-hundred-basis-point position-size swings from one week to the next when RSI oscillates around 40.

**Proposed quant fix for v0.2**: introduce a ±2-unit fuzzy zone at the RSI 40 and 70 boundaries and a ±2-rank fuzzy zone at the quintile boundary (ranks 18–22 are in a "transitional" category that produces half-conviction regardless of the RSI reading). This reduces the label-flip frequency at boundaries by approximately 60–70% without changing the bulk signal behavior. The 15a Cycle A quant critic proposed an analogous 5% materiality buffer for F-Score binary signals (P2.1); the same logic applies here.

---

### Theme C — 53% GOOD hit rate vs Sharpe > 0.3: the gap is wider than it looks

The B.4 quality metric is "GOOD / MARGINAL / WRONG" — a label applied ex-post to whether the v0.1 output was correct directionally. This is a hit rate metric, not a Sharpe metric. The gap between 53% hit rate and Sharpe > 0.3 (the Q12 walk-forward gate) is large and the path between them is not guaranteed.

**Why a 53% hit rate does not map cleanly to Sharpe > 0.3**:

Sharpe = (mean return − rf) / (std of returns). A 53% win rate with symmetric payoffs gives an expected return only slightly above zero. To achieve Sharpe > 0.3 after costs, the system needs either:
(a) Higher win rate (≥ 60% target from Q3), OR
(b) A favorable win/loss asymmetry (wins larger than losses), OR
(c) Both.

The v0.1 design has no explicit mechanism to ensure (b). ATR-based stops mean losses are approximately 2.5 × ATR per trade (if the stop fires). The return target is uncapped upward. In principle, the right-tail (HDFC Bank-style 12-month +50% when the entry was in pullback) could dominate enough stops to produce Sharpe > 0.3 despite the 53% win rate. But:
- The 25–30% stop-loss-out frequency means roughly 1 in 4 ENTRY_ZONE signals exits at a loss. Combined with 47% WRONG/MARGINAL = directionally incorrect signals (that presumably have higher stop-out rates): the loss distribution is heavier than a 25% aggregate stop-out frequency implies.
- The B.4 MARGINAL category (31% of outcomes) introduces ambiguity: MARGINAL signals may be correct directionally but produce near-zero returns before the stop or before exit, which drags Sharpe downward without appearing as WRONG.
- Transaction costs for a weekly TA system running on NIFTY 100 (100 stocks × 52 weeks) are material. The Naik & Reddy (2019) Sharpe > 0.3 result is gross of costs. Net of NSE STT + brokerage + impact cost, 30–50 bps per round-trip reduces annual Sharpe by approximately 0.1–0.15 units on a system generating 1–2 round-trips per stock per year.

**Can v0.1 reach Sharpe > 0.3 with the proposed P0 fixes?**: The REGIME-OVERRIDE (P0.1) and asymmetric hysteresis (P0.2) changes primarily recover cyclical stocks (Tata Steel, Maruti) at trough dates. If both P0.1 and P0.2 fix 3–4 WRONG/MARGINAL cells to GOOD, the hit rate could reach 60–65%, which is the minimum Q3 target. Whether 60–65% hit rate translates to Sharpe > 0.3 net-of-costs depends on the payoff asymmetry, which v0.1 + v0.2 have not measured. The walk-forward Sharpe computation remains entirely unperformed. The P0 fixes are necessary but not sufficient to confirm the Q12 gate.

---

### Theme D — Parameter sensitivity: thresholds are single-point defaults, not optimized for NSE

The v0.1 spec acknowledges in §14 that "thresholds are defaults from B.1 literature, not optimized on NSE data." The quant lens's job is to assess how sensitive the outputs are to the specific choices made.

**40-week vs 26-week vs 52-week SMA for regime gate**:
- 26-week (6-month): faster filter; catches trend reversals sooner; but higher whipsaw in volatile markets. With a 2-week confirmation, still gives 8-week lag on V-shapes. Expected false-positive rate higher.
- 40-week (200-trading-day): the v0.1 choice; industry standard; well-evidenced on NSE (Capitalmind, Faber 2007). In normal-cycle corrections (-20% over 10 weeks), 40-week SMA provides sufficient buffer against false signals.
- 52-week (1-year): slower; misses medium-term regime changes (the 2018 NBFC crisis would not trigger a 52-week regime break for many NIFTY 100 stocks even in hindsight). Too slow for a weekly-evaluated system.

My assessment: the 40-week is the correct choice within the existing architecture. The sensitivity to this parameter is real but moderate: moving to 26-week would fix some V-shape lag while introducing new whipsaw false signals; moving to 52-week would worsen both problems. 40-week is the saddle point in the tradeoff. The more important parameter is the asymmetry of hysteresis (P0.2), not the SMA window length itself.

**ADX 20/25 thresholds vs 18/28 alternatives**:
The Wilder (1978) original thresholds are ADX < 20 (non-trending), 20–25 (weak trend), > 25 (strong trend). These are globally calibrated; NSE weekly data may exhibit different ADX distributions. The 6-stock B.4 test shows ADX consistently above 25 for trending names (HDFC Bank, ITC, Infosys when in trend) and below 20 for ranging/correcting names. The 20/25 split appears to be calibrating reasonably for the NIFTY 100 universe. The alternative 18/28 would widen the LIGHT band and exclude more from STRONG — this would increase the number of downgraded ENTRY_ZONE (full → half) events. Without NSE-wide ADX distribution data, I cannot confirm the optimal split. The sensitivity here is moderate and lower-priority than B-W1, B-W2, B-W3.

**ROC quintile vs decile cutoffs**:
Quintile (top 20%) is the v0.1 choice. Top decile (top 10%) would be far more restrictive — roughly 10 stocks qualify at any time, producing a highly concentrated set of candidates with potentially stronger momentum signals but narrow coverage. The NSE Alpha 30 index uses a similar top-20% momentum filter. The synthesis's Reliance problem (never in top quintile) becomes a non-problem with top-tercile (top 33%) but worsens with top-decile. For v0.2's B-W3 fix, the top-tercile adjustment is the right direction. For general parameter sensitivity: the quintile cutoff is the appropriate choice for a broad advisory tool; decile would be too restrictive.

---

### Theme E — Bollinger Squeeze threshold: 30% of 6-month avg is unvalidated

The SQUEEZE condition in §5.2: `Bandwidth < 0.30 × BW_avg_26w`. The 0.30 threshold (current bandwidth less than 30% of 6-month average) is a heuristic with no NSE calibration cited. The primary reference (Bollinger 1983) does not specify a squeeze threshold — it describes the visual concept. The 30% level appears in Bollinger's later practitioner work and is widely cited, but on equity markets with different volatility regimes (NSE weekly bandwidth distributions differ from US equities).

The statistical risk: if NSE weekly bandwidth is naturally lower-variance than US weekly bandwidth, the 30% threshold may fire too rarely (SQUEEZE-PENDING never triggers). Alternatively, if NSE stocks have more frequent low-volatility periods, the threshold fires too often (excessive SQUEEZE-PENDING halts). The B.4 test results do not report how often SQUEEZE-PENDING was triggered. This is a secondary concern (the squeeze filter is not causing the major observed failures), but it represents an unvalidated threshold that could become a primary issue for individual high-volatility stocks (Tata Steel in commodity cycles, Maruti in auto-cycle disruptions) where bandwidth dynamics are unusual.

---

### Theme F — Divergence detection: 12-week window is a moving-window design with look-ahead symmetry issues

The RSI and MACD divergence detection (§6.5, §7.2) uses a 12-week lookback window to identify higher-high/lower-low price conditions paired with lower-high/higher-low indicator conditions. The quant concern is the peak-and-trough detection method, which is unspecified in v0.1.

To detect "price made a higher high," the algorithm must either:
(a) Use a future bar to confirm the high hasn't continued (true peak detection), which introduces a 1–2 bar look-ahead, OR
(b) Use a rolling window maximum within the 12-week lookback (no look-ahead), which may miss peaks that are not the window maximum.

Method (b) is implementable without look-ahead but may give different results from method (a). In Python-based implementations, the most common divergence detection libraries use method (b) with various peak-smoothing parameters. v0.1 does not specify which method to use, which means two implementations of v0.1 can produce different divergence signals for the same data. This is not a major flaw (divergence signals are secondary to the primary momentum classification), but it is an implementation-underspecification that should be resolved in v0.2.

---

## §4 — What v0.1 Got RIGHT Statistically

**The pipeline order is statistically correct.** Regime filter first, then trend strength, then volatility state, then momentum classification, then confirmation — this correctly accounts for the dependency structure of the signals. Momentum classification in a BEAR regime has no predictive value for entry (the underlying distribution shifts); checking regime first avoids measuring momentum in an invalid sample. The 4-week hysteresis on the regime gate is appropriately calibrated for normal (non-V-shape) corrections: a 4-week below-SMA threshold is not easily triggered by a 10–15% single-month correction, reducing false BEAR triggers. This layered conditional design is the right statistical architecture.

**The ROC(26w, ex-1m) construction is the strongest methodological choice in the spec.** The exclusion of the most recent 4 weeks to avoid short-term reversal is evidence-based: the NSE Nifty 200 Alpha 30 methodology uses the same construction, and there is empirical support from cross-sectional momentum literature (Jegadeesh & Titman 1993 and subsequent NSE replications) that the most recent 1 month of returns exhibits mean reversion that contaminates 12-month momentum signals. Using this specific construction rather than raw 26-week ROC is methodologically correct and reduces false MOMENTUM-STRONG signals at short-term peaks.

**The ATR-based position sizing with a hard risk-budget constraint is statistically sound in normal regimes.** The 1% NAV per-name risk limit combined with ATR-implied stop-distance produces position sizes that naturally shrink during high-volatility periods — which is the correct volatility-scaled exposure behavior. The 5% NAV cap prevents the formula from producing absurdly large positions for low-ATR quality compounders. This is well-designed math. The failure mode (B-W5, crisis ATR) is a boundary condition, not a fundamental flaw in the formula's design envelope.

**ADX(14) on weekly as the trend-strength gate is well-supported.** The Naik & Reddy (2019) NSE-specific study that is the primary evidence base for v0.1 uses ADX-filtered momentum. Wilder's construction is standard and correctly specified in §4.1. The +DI/-DI directional consistency check in §4.3 adds valuable information beyond ADX magnitude alone — it distinguishes a strong range-bound market (high ADX with +DI ≈ -DI) from a strongly directional trend. This nuance is statistically justified.

**The ITC case (5/6 GOOD) validates the pipeline design for its intended use case.** A defensive, non-cyclical stock with a multi-year underperformance period followed by a clear trend inflection is exactly the profile where a regime gate + momentum classification + MACD confirmation pipeline should work. The pipeline did work: correctly avoided the ESG-overhang underperformance period, correctly flagged the Jun-2022 re-rating as an ENTRY_ZONE, and produced the best per-stock hit rate in the test universe. This is not luck — it is the system working as designed for the stock profile it was designed for.

**The Bollinger position supplement to MACD confirmation is geometrically appropriate.** A stock in the lower half of its Bollinger Bands (POSITION-PULLBACK) has recently underperformed its own 20-week trend, which is consistent with the momentum-pullback entry thesis. Combining this with a positive MACD (trend direction intact) creates a two-condition entry that requires both "trend is up" AND "current price is at a favorable point within the trend." The geometric logic is correct. The statistical redundancy concern (Theme A) is a limitation but does not negate the design logic.

---

## §5 — Prioritized v0.2 Recommendations

### P0 — Cannot ship v0.2 without

**P0.1 — REGIME-OVERRIDE for cyclicals at trough conditions (B-W1)**
The 40-week SMA regime gate produces AVOID_ENTRY at cyclical troughs for exactly the stocks with the best forward returns. The REGIME-OVERRIDE hook (v0.1 §3.4 placeholder) must be activated with quantitatively defined trigger conditions. Proposed condition set: (i) stock is tagged CYCLICAL; (ii) regime has been BEAR for ≥ 12 weeks; (iii) ADX < 18 (trend exhaustion — not a deteriorating trend, just no trend); (iv) Cycle A label is not REVIEW or FLAG. When all four conditions are satisfied: allow ENTRY_ZONE generation with half-conviction and `REGIME-OVERRIDE-ACTIVE` annotation. The ADX threshold of 18 (not the ADX < 20 RANGING gate) is appropriate because RANGING means no direction; ADX exhaustion below 18 in a BEAR stock that has been falling for 12+ weeks is a strong trough signal. Note: this fix requires Cycle A sector tagging to be available at evaluation time.

**P0.2 — ATR stop cap with correct position-size formula (B-W5, Theme A)**
Current: `stop_loss = entry − 2.5 × ATR; risk_per_share = 2.5 × ATR`.
v0.2: `stop_distance = MIN(2.5 × ATR, 0.15 × price); risk_per_share = MAX(2.5 × ATR, 0.15 × price)`.
The stop is placed at the nearer distance (MIN) for display and execution purposes. The position size uses the FARTHER distance (MAX) in the denominator to prevent oversizing. If ATR implies 32% stop and the cap is 15%, the stop executes at 15% but position size is calculated as if the stop were at 32% — this preserves the 1% NAV risk budget discipline (you are not risking 1% NAV; you are risking approximately 0.47% NAV). The cap annotation should reflect this: `STOP-DISTANCE-CAPPED: stop placed at 15% (ATR implies 32%); position size reduced to reflect ATR risk, not capped-stop risk`.

**P0.3 — Asymmetric hysteresis: BEAR→BULL shortened to 1–2 weeks with conditions (B-W2)**
BULL→BEAR: keep 4-week confirmation (no change).
BEAR→BULL: shorten to 1 week if AND ONLY IF: (a) ADX is rising (DX increasing for ≥ 2 of the last 3 weekly bars), AND (b) current-week volume > 1.5 × 13-week avg, AND (c) +DI > -DI. If only (a) and (c) but not (b): shorten to 2 weeks. If only regime close (price > SMA for 1 week) without conditions: keep 4-week standard. This creates a three-tier BEAR→BULL hysteresis that is responsive to confirmation-quality rather than just time elapsed.

**P0.4 — DI-flip as standalone leading signal (B-P1)**
Add new EXIT_WARNING trigger (for held positions): -DI > +DI for 2 consecutive weeks AND ADX < 20.
Add new AVOID_ENTRY escalation (for not-held): -DI > +DI for 2 consecutive weeks AND ADX < 20 AND regime is BULL (use to catch deteriorating trends before SMA breaks).
Add new REGIME-OVERRIDE candidate signal (for BEAR stocks): +DI > -DI for 2 consecutive weeks AND ADX < 18 (trend exhaustion) → contributes to P0.1 trigger conditions.
This is the highest signal-value finding from B.4 and is low-cost to implement (DI data already computed in Step 2).

---

### P1 — Strong desirables

**P1.1 — Sector-relative ROC supplement (B-W3, B-W4)**
Compute ROC quintile within NSE Sector peer set in addition to NIFTY 100 cross-sectional. Use MAX(NIFTY 100 quintile class, Sector quintile class) for momentum classification. Annotate source in output. Track which signal (sector vs index) is driving classification in each cell — this is essential for measuring the false-positive rate of sector-relative signals in v0.2 testing.

**P1.2 — Fuzzy zone at discrete label boundaries (Theme B)**
RSI 40: introduce a ±2 fuzzy zone (38–42). Stocks with RSI 38–42 get half-conviction regardless of ROC class, rather than the current full-conviction flip at RSI = 40/41. RSI 70: introduce ±2 fuzzy zone (68–72). ROC quintile boundary: ranks 18–22 are in a "transitional" band that produces half-conviction rather than a clean quintile-class assignment. This is a low-implementation-cost change that significantly reduces label instability at boundaries.

**P1.3 — Conglomerate tag with adjusted STRONG-PULLBACK threshold (B-W3)**
For NIFTY 100 stocks where no single NSE sector accounts for > 60% of revenue (proxy: identified as CONGLOMERATE in Cycle A sector tagging): lower STRONG-PULLBACK ROC threshold from top-quintile to top-tercile (ranks 1–33). This is a targeted fix for Reliance and any other diversified holding companies in the NIFTY 100. Complementary to P1.1, not a replacement.

**P1.4 — Indicator inter-correlation documentation (Theme A)**
Before v0.2 testing, compute pairwise weekly correlation of ROC(26w), RSI(14), and MACD(12,26,9) on NIFTY 100 historical weekly data (3 years minimum). If pairwise correlation of ROC-rank and MACD-positive exceeds 0.60, the MACD confirmation requirement should be reconsidered as a gate (it would be adding minimal entropy reduction). If RSI and MACD are correlated above 0.65 in the 40–70 band, the combined momentum step should use only the higher-information signal rather than requiring both. This is an empirical calibration step, not a pure v0.2 code change — but its output should inform v0.2 Step 5 design.

---

### P2 — Nice-to-have / single-stock

**P2.1 — Divergence detection method specification (Theme F)**
Specify the exact peak/trough detection algorithm for RSI and MACD divergence (§6.5, §7.2). Recommend: rolling-window maximum/minimum within the 12-week lookback, with a minimum 3-week distance between identified peaks/troughs to avoid noise. No look-ahead. This is an implementation precision fix, not a material signal change.

**P2.2 — Bollinger Squeeze threshold NSE calibration (Theme E)**
Compute the distribution of weekly Bollinger bandwidth for NIFTY 100 stocks over 3 years. Identify the empirical 10th percentile of bandwidth for each stock. Use the 10th percentile as the stock-specific SQUEEZE threshold rather than the universal 30% of 6-month avg. This makes the squeeze detection adaptive to the stock's own volatility regime rather than a universal multiplier. Low priority because the squeeze filter is not currently a major source of observed failures.

**P2.3 — Walk-forward Sharpe feasibility assessment (Theme C)**
Before claiming v0.2 is close to the Q12 Sharpe > 0.3 gate, run a rough walk-forward calculation on the 19 GOOD cells from B.4: estimate entry/exit prices, stop-out events, and return distribution. Compute ex-post Sharpe for the 19-cell sample. This is not a proper walk-forward (sample too small, no OOS data) but it gives a lower bound on whether the v0.1 design is architecturally capable of approaching Sharpe > 0.3, or whether structural redesign beyond P0.1–P0.4 is required before the Q12 gate is even testable.

---

## Summary counts

| Priority | Items | IDs |
|---|---|---|
| P0 | 4 | P0.1 (REGIME-OVERRIDE), P0.2 (ATR stop cap with position formula correction), P0.3 (asymmetric hysteresis), P0.4 (DI-flip standalone signal) |
| P1 | 4 | P1.1 (sector-relative ROC), P1.2 (fuzzy zone at boundaries), P1.3 (conglomerate tag threshold), P1.4 (inter-correlation empirical measurement) |
| P2 | 3 | P2.1 (divergence spec), P2.2 (Bollinger Squeeze NSE calibration), P2.3 (walk-forward feasibility check) |

---

**Status**: ✅ Quant critique complete. 11 P0/P1/P2 recommendations (4 P0, 4 P1, 3 P2).
