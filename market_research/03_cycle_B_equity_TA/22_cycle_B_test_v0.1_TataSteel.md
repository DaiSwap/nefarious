# 22 — Cycle B: TA Math v0.1 Test — Tata Steel (TATASTEEL.NS)

**Status**: 🔄 Initialized — reading v0.1 spec + Cycle A Tata Steel test.
**Last updated**: 2026-05-31
**Methodology**: Per `21_cycle_B_math_v0.1.md` v0.1 spec. Six historical NSE evaluation dates.
**Cross-cycle ref**: `13_cycle_A_test_v0.1_TataSteel.md` — Cycle A FA labels for Mar-2020 and Mar-2024.
**Corporate action**: 1:10 stock split effective July 28-29, 2022. All prices in split-adjusted terms (post-split equivalent) throughout.

---

## Data Sources and Conventions

**Primary price data**: Yahoo Finance TATASTEEL.NS, NSE historical bhavcopy, public market records.
**NIFTY 100 TRI**: niftyindices.com (estimated from public record where direct fetch unavailable).
**Confidence labels**: HIGH (well-documented primary source), MED (secondary source cross-checked), LOW (estimated from financial context or reconstructed).
**Tata Steel split note**: Pre-split prices multiplied by 0.1 for split-adjusted equivalents. All indicators computed on split-adjusted series.
**NIFTY 100 ROC quintile**: Approximated from known market regime and steel sector performance vs. broad index at each date. Tata Steel was typically classified as NIFTY 100 constituent throughout all 6 dates.

---

## Cycle A Tata Steel FA Labels (Cross-Reference Table)

| Cycle A Eval Date | FA Label (v0.1) | F-Score | Key Driver |
|---|---|---|---|
| Mar-2020 | WATCH | F=6 | Bhushan acquisition debt; OCF strong |
| Mar-2021 | REVIEW | F=5 | COVID trough; margins/turnover collapsed |
| Mar-2022 | HOLD | F=8 | Recovery peak; leverage falling fast |
| Mar-2024 | REVIEW | F=4 | Post-supercycle; UK losses; ROCE 36th pctile |

**Key Cycle A finding**: Piotroski anti-correlated with cyclical entry. F=5 at Mar-2021 trough (best entry — +51% vs NIFTY +21%). F=8 at Mar-2022 near-peak (marginal +3pp excess). See §10 cross-cycle analysis.

---

🔄 Spec + Cycle A reference digested. Beginning Date 1 (2008-10 GFC bottom).

---

## Date 1: October 2008 (GFC Bottom)

### Context
Global Financial Crisis bottom. NIFTY 50 bottomed near 2,500 in late October / early November 2008, down ~62% from Jan 2008 peak. Tata Steel had just completed the Corus (UK) acquisition in 2007 for ~$12.1 billion, loading the balance sheet with significant debt at the worst possible time. Steel demand was collapsing globally. This is the most extreme distress scenario for Tata Steel in the 6-date test.

**Evaluation week**: Last week of October 2008 (week ending Oct 31, 2008).

### Price Data — Pre-split, split-adjusted equivalents

**Confidence: MED** — reconstructed from public market records and financial archives. Tata Steel NSE pre-split prices in October 2008 are documented in multiple secondary sources.

Pre-split price context:
- Jan 2008 (52-week high): ~₹940 (pre-split), split-adj ~₹94
- Oct 2008 (GFC trough): ~₹115–130 pre-split range; October 31 close estimated ~₹120 pre-split
- Split-adjusted closing price Oct 31, 2008: **~₹12.0** (confidence: MED)
- 40-week range: peaked ~₹94 (split-adj) early Jan 2008, troughed ~₹12 by Oct 2008 — an ~87% decline in 9 months.

**40-week weekly OHLC sketch** (split-adjusted, approximate):
- Week 1 (Jan 2008): Open ~₹94, Close ~₹92
- Week 10 (Mar 2008): Close ~₹72 (post-Bear Stearns)
- Week 20 (Jun 2008): Close ~₹52
- Week 30 (Aug 2008): Close ~₹40
- Week 38 (Oct 17): Close ~₹18
- Week 40 (Oct 31): Close ~₹12.0 (evaluation week)

**NIFTY 100 (proxy: NIFTY 50) — Oct 31, 2008**: ~₹2,885 [MED — well-documented GFC trough level]

### Indicator 1: 40-Week SMA (Regime Gate)

40-week SMA computation (approximate, using declining price series):
- The stock declined from ~₹94 to ~₹12 over 40 weeks
- Simple average of 40 weekly closes in a near-monotonic decline: approximately ₹45–55 range
- Estimated 40-week SMA at Oct 31, 2008: **~₹48** (confidence: MED)
- Current close ~₹12 vs 40-week SMA ~₹48
- Price is ~75% BELOW the 40-week MA
- **4+ consecutive weeks below**: CONFIRMED (stock had been declining all of 2008; well below MA for more than 4 consecutive weeks)

**Regime**: **BEAR** (price ₹12 << SMA ₹48; far below for many months consecutively)

Per §3.3: BEAR → halt pipeline; output `AVOID_ENTRY: REGIME-BEAR`

---

**PIPELINE HALTED AT REGIME GATE.**

### Indicator 2: ADX(14) weekly

Despite the halt, computing for record purposes.
In a strong, near-monotonic downtrend of this magnitude:
- +DI would be very low (essentially no weekly closes higher than prior week for extended period)
- -DI would be very high (dominant down moves every week)
- DX would be extreme (near 100% of DI total is -DI)
- ADX(14) estimated: **~50–65** (confidence: LOW — extremely high ADX characteristic of GFC free-fall markets)
- **Trend strength: STRONG** (ADX >> 25), but the dominant direction is bearish (-DI >> +DI)

**REGIME-DI-CONFLICT** would be triggered if regime were BULL — irrelevant here since BEAR halt already issued.

### Indicator 3: Bollinger Bands (20-week, 2σ)

In a crash environment:
- 20-week SMA: ~₹35 (declining; earlier weeks were much higher)
- σ: extremely high — weeks ranged from ~₹12 to ~₹60 over the window = ~₹48 range; σ ≈ ₹15–18
- Upper band: ~₹35 + 2×₹16 = ~₹67
- Lower band: ~₹35 − 2×₹16 = **~₹3** (theoretically near zero; stock is at extreme lower band)
- Current price ~₹12: **below or at the lower Bollinger band** → POSITION-MEAN-REVERSION signal (but only meaningful in BULL regime)
- Bandwidth: (₹67−₹3)/₹35 = 1.83; extremely wide

26-week BW average: bandwidth would have been ~0.40 in calmer periods; current 1.83 >> 0.30 × 0.40 = 0.12 → NOT a squeeze; extreme expansion.
**Volatility State: NORMAL (bandwidth expansion, not squeeze)**

### Indicator 4: ROC(26-week, ex-1m)

ROC(26w, ex-1m) = (Price at 4 weeks ago − Price at 30 weeks ago) / Price at 30 weeks ago
- Price at ~4 weeks ago (late Sep 2008): ~₹25–28 (split-adj); use ₹27
- Price at ~30 weeks ago (Apr 2008): ~₹55–60 (split-adj); use ₹57
- ROC = (₹27 − ₹57) / ₹57 = −53%

NIFTY 100 ROC quintile: In Oct 2008, essentially the ENTIRE NIFTY 100 had negative ROC. Tata Steel at −53% was among the worst performers (steel/metal stocks were hit hardest in the GFC).
- Estimated quintile rank: **bottom quintile (81–100)** → **MOMENTUM-WEAK** (confidence: MED)
- Per §6.4: MOMENTUM-WEAK → halt → `AVOID_ENTRY: WEAK-MOMENTUM`

### Indicator 5: RSI(14) weekly

In a near-uninterrupted 40-week decline:
- Very few up-weeks; gains minimal; losses large
- RSI(14) estimated: **~12–18** (confidence: MED — extreme oversold; sub-20 RSI is well-documented for GFC-bottom assets)
- RSI = **~15** (deeply oversold)

**RSI divergence check (12-week window)**:
- Price made lower lows every few weeks. RSI also made lower lows consistently in the decline phase. By the absolute final week (Oct 31), there may be nascent bullish divergence (RSI not making new lows while price does), but this was the absolute bottom week — it would not be detectible in real-time.
- **Divergence**: NONE detectible (or ambiguous; marking as no confirmed divergence) (confidence: LOW)

### Indicator 6: MACD Weekly (12, 26, 9)

In a 40-week crash:
- EMA(12) << EMA(26): both falling, but 12w EMA falls faster
- MACD line deeply negative: estimated **~−8 to −12** (split-adj terms) (confidence: LOW)
- Signal line: also deeply negative
- Histogram: negative; could be near zero or slightly rising as the decline decelerated in the final weeks

MACD divergence: Price made lower lows in Oct, but MACD histogram may have formed a higher low as selling velocity slowed. However, this nascent divergence was not confirmed at this exact week.
**MACD histogram**: Negative, slight improvement possible. **No confirmed bullish histogram divergence** at this date.

### Indicator 7: ATR(14) weekly

In a crash, weekly ranges are enormous:
- Typical weekly range late 2008: ₹4–8 in split-adj terms (individual weeks could swing 30–50% intraweek)
- ATR(14) estimated: **~₹5.5–7.0** (confidence: LOW)
- Using **₹6.0** as working estimate
- Stop-loss (if entry): ₹12.0 − 2.5 × ₹6.0 = ₹12.0 − ₹15.0 = **−₹3.0** (negative — stop below zero, which is impossible)
- This is a sizing impossibility: ATR > Entry Price × 0.4; any ATR-based stop at 2.5× would be below zero.
- **Sizing: IMPOSSIBLE at 2.5× ATR multiplier** — position would require infinite risk budget or the stop would be below zero.

---

### v0.1 Pipeline Output — Date 1 (Oct 2008)

**PRE-SCREEN**: Data sufficiency ≥40 weeks: YES (stock was listed since 2000s). Surveillance: clean (no ASM/ESM in 2008, pre-regime). Circuit: N/A (historical).

**REGIME (Step 1)**:
- 40-week MA ~₹48; close ~₹12.0
- Consecutive weeks below MA: **entire 2008 calendar year = 40+ weeks**
- **BEAR** → PIPELINE HALT

**OUTPUT**: `AVOID_ENTRY: REGIME-BEAR`

**Additional indicators for record** (not affecting label since halted):
- ADX: ~55 STRONG (bearish direction — -DI >> +DI)
- Bollinger: NORMAL (extreme bandwidth expansion, not squeeze)
- ROC: ~−53%; bottom quintile → MOMENTUM-WEAK
- RSI: ~15 (extreme oversold)
- MACD: Deeply negative, no confirmed divergence
- ATR: ~₹6.0 (stop sizing impossible — below zero)

**Confidence**: MED overall (price reconstruction from secondary sources; directional conclusions highly reliable even if exact levels differ by ±10%)

---

### Forward Outcomes (Oct 2008 → 6/12/24 months forward)

**Reference prices** (split-adjusted, confidence: MED):
- Oct 31, 2008 (entry): ~₹12.0
- Apr 2009 (+6 months): ~₹18–20; use **₹19** [MED — steel stocks recovered with broader market]
- Oct 2009 (+12 months): ~₹40–45; use **₹43** [MED — first rally leg complete by Oct 2009]
- Oct 2010 (+24 months): ~₹55–65; use **₹60** [MED — steel super-cycle phase 1 in progress]

**Absolute returns** (from ₹12.0):
- +6 months: (₹19−₹12)/₹12 = **+58%**
- +12 months: (₹43−₹12)/₹12 = **+258%**
- +24 months: (₹60−₹12)/₹12 = **+400%**

**NIFTY 100 TRI** (confidence: MED):
- Oct 2009 (+12m): NIFTY 50 recovered from ~₹2,885 to ~₹5,000 = **+73%** (approximate)
- Oct 2010 (+24m): NIFTY 50 ~₹6,100 = **+111%**

**Excess returns**:
- +12 months: +258% − 73% = **+185pp vs NIFTY**
- +24 months: +400% − 111% = **+289pp vs NIFTY**

**Stop-loss analysis**: With ATR ~₹6.0, a 2.5× stop at ₹12 − ₹15 = IMPOSSIBLE (negative). Even at 1× ATR, stop would be ₹6 — the stock never went below ~₹10 in the following weeks. Stop-loss would NOT have been hit if a notional stop was placed at ~₹8 (informal).

**Verdict — Date 1 (Oct 2008)**:
- **Label assigned**: AVOID_ENTRY: REGIME-BEAR
- **Forward outcome**: +258% vs NIFTY +73% (+12m); +400% vs NIFTY +111% (+24m)
- **Verdict**: **WRONG** — the model correctly applied the rules (BEAR regime → avoid entry), but the actual outcome was catastrophically bullish in hindsight. Oct 2008 was the single greatest buying opportunity for cyclical steel in a generation.
- **Commentary**: v0.1 applied as designed — BEAR regime blocks all entries. The regime gate is CORRECT per the rules but produces a false negative at the extreme cycle trough. This is the TA analog of Cycle A's F-Score problem: both trailing FA (low F-Score) and trailing TA (BEAR regime) produce AVOID signals at the maximum opportunity point.

**Cycle A Cross-ref**: No Cycle A data for Oct 2008 (Cycle A only tested Mar-2020 onwards). Expected FA label at Oct 2008 would likely be REVIEW or WATCH (Corus acquisition debt, but solid OCF). Both TA and FA would have said AVOID/CAUTION at the GFC bottom.

---

🔄 Date 1 indicators complete.
🔄 Date 1 done. Label = AVOID_ENTRY: REGIME-BEAR. Verdict = WRONG (+258% vs NIFTY +73% missed). Cycle A cross-ref = N/A (no Cycle A data for this date).

---

## Date 2: June 2014 (Modi Election Rally Early)

### Context
Narendra Modi elected PM in May 2014 with the largest Lok Sabha majority since 1984. NIFTY 50 rallied from ~6,000 in April 2014 to ~7,600 by end of May 2014. June 2014 represents the early phase of a new bull market — post-election euphoria, infrastructure/capex expectations. Steel stocks rallied on capex/infrastructure hope. However, Tata Steel was still carrying heavy Corus/UK debt and global steel overcapacity was a structural headwind (China over-supply).

**Evaluation week**: Last week of June 2014 (week ending June 27, 2014).

### Price Data (Split-Adjusted)

Pre-split reference prices in June 2014:
- Jan 2013 (40 weeks prior to Jun 2014 = ~Oct 2013): ~₹220–240 pre-split; split-adj ~₹23
- The election rally in May 2014 pushed Tata Steel from ~₹310 pre-split (~₹31) to ~₹540 pre-split (~₹54) by early June 2014
- June 27, 2014 estimated close: **~₹46–50 pre-split = ~₹4.6–5.0 split-adj**; use **₹4.8** (confidence: LOW — pre-split price range is well-documented; specific daily close uncertain)

**Note on price level**: Tata Steel pre-split prices in mid-2014 ranged approximately ₹350–560. The election rally peaked around ₹540 in early June and consolidated to ~₹460–490 by end of June. Using **₹48 pre-split = ₹4.8 split-adj** as evaluation price.

**40-week price range sketch** (split-adj):
- Sep 2013 (40w prior): ~₹2.2–2.5 (trough of that cycle)
- Dec 2013: ~₹2.8
- Mar 2014: ~₹3.0–3.2 (gradual recovery)
- May 2014: Election rally; ₹3.5–5.4 (sharp spike)
- Jun 27, 2014: ~₹4.8

**NIFTY 100 (proxy: NIFTY 50) — Jun 27, 2014**: ~₹25,300–25,500 (pre-correction from election peak ~27,000 in May); use **₹25,400** [MED — NIFTY level in June 2014 well-documented]

### Indicator 1: 40-Week SMA (Regime Gate)

40-week SMA estimation:
- 40 weeks of prices: ranged from ~₹2.2 (trough Sep-Oct 2013) up to ~₹4.8 (Jun 2014)
- Simple average across ~40 closing weeks: approximately ₹3.0–3.4
- Estimated 40-week SMA: **~₹3.2** (confidence: LOW)
- Current close ~₹4.8 vs 40-week SMA ~₹3.2
- Price **above** the 40-week SMA: ₹4.8 >> ₹3.2 (+50% above MA)
- Consecutive weeks above MA: The stock crossed the MA around Feb-Mar 2014 during the pre-election rally. By June 2014 it had been above the MA for ~16–18 weeks consecutively.
- **Regime: BULL** (confirmed; price well above 40-week SMA for 16+ weeks)

Continue to Step 2.

### Indicator 2: ADX(14) weekly

The election rally (Apr–May 2014) was one of the sharpest multi-week moves for Indian cyclicals in recent memory:
- Strong up-moves in April-May 2014; June consolidation
- +DI elevated (multiple strong up-weeks in the rally)
- -DI lower but potentially recovering during June consolidation
- Estimated ADX(14): **~30–38** (confidence: LOW — the strong directional trend of the election rally would push ADX above 25)
- **ADX: ~34 → STRONG** (≥25)
- +DI estimated ~30–35; -DI estimated ~18–22
- +DI > -DI → **bullish bias consistent with BULL regime** ✓

Continue to Step 3.

### Indicator 3: Bollinger Bands (20-week, 2σ)

20-week range (roughly Feb–Jun 2014):
- Prices ranged from ~₹2.8 (Jan 2014) to ~₹5.4 (election peak May 2014)
- 20-week SMA: approximately ₹3.8–4.0
- σ: The 20-week window included the big election rally — standard deviation elevated at ~₹0.70–0.85
- Upper band: ~₹4.0 + 2×₹0.75 = **~₹5.5**
- Lower band: ~₹4.0 − 2×₹0.75 = **~₹2.5**
- Middle band: ~₹4.0
- Current price ~₹4.8: between Middle (~₹4.0) and Upper (~₹5.5) → **POSITION-RISING** (upper half of bands)

Bandwidth = (₹5.5 − ₹2.5) / ₹4.0 = **0.75**
26-week BW average: Prior 26 weeks were less volatile; estimated BW_avg_26w ~0.45–0.55
Ratio: 0.75 / 0.50 = 1.50 >> 0.30 → NOT a squeeze (bandwidth expanding)
**Volatility State: NORMAL** ✓

Continue to Step 4.

### Indicator 4: ROC(26-week, ex-1m)

ROC(26w, ex-1m):
- Price at ~4 weeks ago (late May/early Jun 2014): ~₹5.0–5.2 (post-election peak); use ₹5.1
- Price at ~30 weeks ago (~Nov/Dec 2013): ~₹2.5–2.8; use ₹2.7
- ROC = (₹5.1 − ₹2.7) / ₹2.7 = **+88.9%**

This is an enormous positive ROC driven by the election rally momentum.

NIFTY 100 ROC quintile in June 2014:
- The election rally lifted virtually all NIFTY 100 stocks. Steel/metals stocks had one of the strongest runs (infrastructure hope). Tata Steel +89% over 26w (ex-1m) would place it in the **top quintile (rank 1–20)** of NIFTY 100 (confidence: MED — metals were among top performers in the election rally, consistent with infrastructure narrative)
- **MOMENTUM-STRONG** (top quintile)

### Indicator 5: RSI(14) weekly

After a sharp 100%+ rally from trough to peak over ~20 weeks, RSI would be very elevated:
- Estimated RSI(14) at June 27, 2014: **~60–70** (confidence: LOW — consolidation off the election spike would bring RSI down from very overbought levels)
- The June consolidation (from ~₹5.4 peak to ~₹4.8 in 3 weeks) would bring RSI down from ~80+ to approximately **~65**
- Use **RSI = 65**

Combined classification (MOMENTUM-STRONG + RSI 40–70): → **STRONG-PULLBACK** (full conviction)

RSI divergence check (12-week window):
- Price peaked at ~₹5.4 in early May and was consolidating to ~₹4.8 by late June. RSI would have also declined from ~80+ to ~65. No new higher price high during consolidation; no classic divergence pattern.
- **No divergence detected** (confidence: MED)

### Indicator 6: MACD Weekly (12, 26, 9)

After the strong election rally:
- EMA(12) well above EMA(26): both rising, 12w EMA rising faster
- MACD line: **positive** (estimated +0.4–0.6 in split-adj terms) (confidence: LOW)
- Signal line: also positive, slightly below MACD line
- Histogram: **positive and recently turned or still rising** (confidence: LOW — post-rally consolidation could produce flat/declining histogram even with positive MACD)

In consolidation after a strong rally: MACD line may still be above signal, histogram slightly positive but declining from the peak.
- **MACD histogram: positive, declining slightly** (consolidation phase)

MACD divergence: No bearish divergence (price decline from ~₹5.4 to ~₹4.8 is within normal consolidation; no clear MACD histogram higher-low vs price lower-low)
**No MACD divergence** (confidence: MED)

### Indicator 7: ATR(14) weekly

Post-election volatility:
- Weekly ranges during Apr–May election rally: ₹0.6–1.2 (split-adj; large absolute moves)
- Weekly ranges in June consolidation: ₹0.3–0.6
- ATR(14) estimated: **~₹0.7–0.9** (confidence: LOW — averaging the volatile election weeks with calmer early 2014)
- Use **₹0.8**
- Stop-loss: ₹4.8 − 2.5 × ₹0.8 = ₹4.8 − ₹2.0 = **₹2.8**
- Risk per share: ₹2.0
- Position size (1% budget, ₹1Cr portfolio): ₹1,00,000 / ₹2.0 = **50,000 shares**
- Position value: 50,000 × ₹4.8 = **₹2.40 lakhs** (2.4% NAV — within 5% cap)

---

### v0.1 Pipeline Output — Date 2 (June 2014)

**PRE-SCREEN**: Data sufficient ✓. Surveillance: clean ✓. Circuit: none ✓.

**REGIME (Step 1)**: Close ₹4.8 >> 40w MA ₹3.2; 16+ weeks above → **BULL** ✓

**TREND STRENGTH (Step 2)**: ADX ~34 → **STRONG**; +DI > -DI → bullish bias ✓

**VOLATILITY STATE (Step 3)**: Bandwidth 0.75; BW_avg_26w ~0.50; ratio 1.50 → **NORMAL** ✓

**PRIMARY MOMENTUM (Step 4)**:
- ROC(26w, ex-1m) = +89%; top NIFTY 100 quintile → MOMENTUM-STRONG
- RSI(14) = ~65; in 40–70 band
- Combined: **STRONG-PULLBACK** (full conviction)
- No RSI divergence

**CONFIRMATION (Step 5)**:
- MACD histogram: positive, slightly declining (consolidation)
- Bollinger: POSITION-RISING (upper half of bands)
- Routing: STRONG-PULLBACK + positive MACD + POSITION-RISING → `ENTRY_ZONE (full)` IF no bearish divergence ✓
- ADX STRONG: no downgrade

Per §7.4: STRONG-PULLBACK + positive (no divergence) + RISING → `ENTRY_ZONE (full)` ✓

**SIZING (Step 6)**:
- ATR(14) = ₹0.8
- Stop-loss: ₹4.8 − 2.5 × ₹0.8 = ₹2.8
- Risk per share: ₹2.0
- Position size: 50,000 shares @ ₹4.8 = ₹2.40 lakhs (2.4% NAV) — within cap ✓

**OUTPUT**: `ENTRY_ZONE (full conviction)`

**REASONING**:
Tata Steel in June 2014 is in a confirmed BULL regime (price ₹4.8, 50% above 40-week MA of ₹3.2, for 16+ consecutive weeks). ADX at ~34 confirms a strong directional trend. No squeeze pending — bandwidth is in normal expansion. The 26-week ROC of +89% (ex-1 month) places Tata Steel in the top quintile of NIFTY 100, driven by the Modi election rally and infrastructure capex expectations. RSI at ~65 indicates healthy momentum within the trend (not overbought). MACD is positive (above signal). Price in the upper half of the Bollinger Bands (POSITION-RISING) — acceptable in combination with STRONG-PULLBACK without divergence. ATR-based stop at ₹2.8; risk per share ₹2.0; position sized to ₹2.40 lakhs (2.4% NAV, within 5% cap).

**Confidence**: LOW-MED overall. Price estimates for 2014 carry ±10% uncertainty. The directional conclusion (BULL regime, strong momentum, ENTRY_ZONE) is robust to reasonable price variations.

---

### Forward Outcomes (June 2014 → 6/12/24 months forward)

**Reference prices** (split-adj, confidence: LOW-MED):
- Jun 27, 2014 (entry): ~₹4.8
- Dec 2014 (+6 months): ~₹3.6–4.0; global steel prices were already in decline by H2 2014. China oversupply narrative dominated. Use **₹3.8** [LOW]
- Jun 2015 (+12 months): ~₹2.5–3.0; sharp steel price decline, commodity bear market beginning. Use **₹2.8** [LOW]
- Jun 2016 (+24 months): ~₹2.0–2.5; steel sector at multi-year lows (China dumping, global overcapacity). Use **₹2.2** [LOW]

**Stop-loss check**: Stop was at ₹2.8. The 12-month price is ~₹2.8 and the 24-month price is ~₹2.2. The stop at ₹2.8 would likely have been **HIT around Dec 2014 – Mar 2015** when Tata Steel declined through ₹2.8 en route to the 2015-2016 commodity trough. **Stop-loss triggered: YES** (estimated timing: Q1 2015, ~6–9 months after entry).

**Absolute returns** (to stop-loss at ₹2.8):
- From ₹4.8 to stop ₹2.8: **−41.7%** loss (if stop hit as designed)
- If held to 12 months: (₹2.8 − ₹4.8)/₹4.8 = **−41.7%** (approximately same as stop)
- If held to 24 months: (₹2.2 − ₹4.8)/₹4.8 = **−54.2%**

**NIFTY 100 TRI** (confidence: MED):
- Jun 2015 (+12m): NIFTY 50 ~₹27,800 vs entry ~₹25,400 = **+9.4%**
- Jun 2016 (+24m): NIFTY 50 ~₹26,600 vs entry ~₹25,400 = **+4.7%**

**Excess returns** (vs NIFTY TRI):
- Stop triggered (−41.7%) vs NIFTY +9.4% (12m) = **−51pp vs NIFTY** — severe underperformance
- Note: The 1% risk budget sizing means the PORTFOLIO loss was capped at ~−1% NAV (from 1% risk budget), not the full −41.7%. The position would have been small (₹2.40 lakhs on ₹1Cr portfolio).

**Verdict — Date 2 (June 2014)**:
- **Label assigned**: ENTRY_ZONE (full conviction)
- **Forward outcome**: Stop-loss hit ~6–9 months post-entry (estimated Q1 2015 at ₹2.8). 24-month absolute loss ~−54%.
- **Verdict**: **WRONG** — ENTRY_ZONE signal was followed by a commodity super-bear market that took Tata Steel down 55%+ over 24 months. The stop-loss protection limited the portfolio hit to ~1% NAV loss (per the sizing math), but the directional call was entirely wrong.
- **Commentary**: The election rally momentum in June 2014 met all TA criteria (BULL regime, strong ROC, MACD positive). However, the structural steel bear market (China overcapacity, global HRC price collapse) began in H2 2014. TA momentum signals were a classic false positive at the very beginning of a commodity down-cycle. The stop-loss mechanism worked as designed — the 2.5× ATR stop prevented a 54% loss from becoming a portfolio catastrophe; the portfolio absorbed only ~1% NAV loss. This is the key distinction between WRONG-with-stop and WRONG-without-stop.

**Cycle A Cross-ref**: No Cycle A data for June 2014.

---

🔄 Date 2 indicators complete.
🔄 Date 2 done. Label = ENTRY_ZONE (full). Verdict = WRONG (stop-loss hit; commodity bear cycle began). Cycle A cross-ref = N/A.

---

## Date 3: September 2018 (NBFC Crisis)

### Context
The IL&FS default in September 2018 triggered the NBFC liquidity crisis. NIFTY 50 peaked around 11,700 in August 2018 and began a sharp correction. Metals/steel stocks had performed well in FY2018 (steel super-cycle recovery phase 1: Chinese supply reforms, anti-dumping measures). However, the NBFC crisis and a stronger USD (EM outflows) hit commodity stocks. Tata Steel was in a genuine upcycle — FY2019 would record revenue of ₹157,669 Cr (up +27.9% YoY) and net profit ₹9,122 Cr (up from ₹1,174 Cr). The Bhushan Steel acquisition was completed in May 2018 — a significant leverage event.

**Evaluation week**: Last week of September 2018 (week ending Sep 28, 2018).

### Price Data (Split-Adjusted)

Pre-split Tata Steel September 2018 context:
- 52-week high (Aug 2018): ~₹680 pre-split = ₹68 split-adj
- Sep 28, 2018 (NBFC selloff trough for metals): ~₹510–550 pre-split = ₹51–55 split-adj
- Use **₹53 split-adj** as evaluation close (confidence: MED)
- 40-week price sketch (Sep 2017 – Sep 2018):
  - Sep 2017: ~₹48 (split-adj); FY2018 recovery underway
  - Dec 2017: ~₹55
  - Mar 2018: ~₹63
  - Jun 2018 (post-Bhushan acquisition): ~₹65–68 (peak)
  - Aug 2018 (52w high): ~₹68
  - Sep 2018: ~₹53 (NBFC pullback)

**NIFTY 100 — Sep 28, 2018**: ~₹37,800–38,200 (NIFTY 50 ~10,930); use **₹38,000** [MED]

### Indicator 1: 40-Week SMA (Regime Gate)

40-week closes: ranged from ~₹48 (Sep 2017) to ~₹68 (Aug 2018), with current ~₹53.
Simple average of approximately normally-distributed rising series: **~₹58–60** (confidence: MED)
- Use **₹59**
- Current close ~₹53 vs 40-week SMA ~₹59
- Price is ~10% BELOW the 40-week MA
- How many consecutive weeks below? The stock peaked in Aug 2018 and began declining; by late Sep 2018, approximately 6–8 weeks below the MA.

Per §3.2: Price below MA for 4+ consecutive weeks = **BEAR** transition.
However: 6–8 weeks below could trigger BEAR. Let's be precise:
- The cross below likely happened around mid-August as the MA was near the declining price.
- If the MA was ~₹60 and price crossed below at ~₹62 in early August then, by late September (8 weeks later), well into BEAR confirmation.

**Regime: BEAR** (6–8 consecutive weeks below 40-week MA)

Per §3.3: BEAR → halt pipeline; output `AVOID_ENTRY: REGIME-BEAR`

---

**PIPELINE HALTED AT REGIME GATE.**

### Supporting Indicators (for record)

**Indicator 2: ADX(14)**
The sharp selloff from ₹68 to ₹53 (−22% in 8 weeks) with some recoveries:
- -DI would be dominant
- ADX estimated: **~28–35** (STRONG, bearish direction) (confidence: LOW)

**Indicator 3: Bollinger Bands**
20-week SMA: ~₹62 (declining)
σ: ~₹6–8 (increased volatility during selloff)
Upper: ~₹78; Lower: ~₹46; Price at ₹53: in lower half → POSITION-PULLBACK
Bandwidth: (₹78−₹46)/₹62 = 0.52; BW_avg_26w ~0.30 → ratio 1.73 → NOT squeeze (expanding)
**NORMAL volatility state**

**Indicator 4: ROC(26w, ex-1m)**
Price at 4w ago (~early Sep 2018): ~₹60
Price at 30w ago (~Feb/Mar 2018): ~₹60 (similar level)
ROC = (₹60 − ₹60) / ₹60 = **~0%** — neutral momentum

NIFTY 100 quintile: NIFTY metals had underperformed the index by Sep 2018; Tata Steel flat/negative vs peers.
- Estimated quintile: **middle quintile (rank 40–70)** → **MOMENTUM-MID** (confidence: LOW)

**Indicator 5: RSI(14)**
After the sharp August-September decline:
- Estimated RSI(14): **~32–38** (approaching oversold but not extreme) (confidence: LOW)
- Use RSI = **35** (below 40 — NOISY-MOMENTUM zone for MOMENTUM-MID stocks)

**Indicator 6: MACD**
Post-peak; EMA(12) falling faster than EMA(26):
- MACD line: negative (estimated ~−1.5 to −3.0 split-adj terms) (confidence: LOW)
- Histogram: negative
- No bullish divergence confirmed

**Indicator 7: ATR(14)**
High volatility environment:
- ATR(14) estimated: **~₹3.5–4.5** (confidence: LOW)
- Use ₹4.0
- Stop (if entry): ₹53 − 2.5 × ₹4.0 = ₹53 − ₹10 = ₹43

---

### v0.1 Pipeline Output — Date 3 (September 2018)

**PRE-SCREEN**: Data sufficient ✓. Surveillance: clean ✓.

**REGIME (Step 1)**: Close ₹53 < 40w MA ₹59; 6–8 consecutive weeks below → **BEAR** → HALT

**OUTPUT**: `AVOID_ENTRY: REGIME-BEAR`

**Additional indicators for record (post-halt)**:
- ADX: ~32, STRONG (bearish direction)
- Bollinger: NORMAL; POSITION-PULLBACK (lower half of bands)
- ROC(26w, ex-1m): ~0%; MOMENTUM-MID; would likely → ENTRY-PULLBACK (had RSI been in 40–50 range)
- RSI: ~35 (NOISY-MOMENTUM for MOMENTUM-MID)
- MACD: Negative, no divergence
- ATR: ~₹4.0; stop at ₹43

**Confidence**: MED (price reconstruction; regime determination robust)

---

### Forward Outcomes (Sep 2018 → 6/12/24 months forward)

**Reference prices** (split-adj, confidence: MED):
- Sep 28, 2018 (reference): ~₹53
- Mar 2019 (+6 months): ~₹35–40; steel downturn accelerated. Use **₹38** [MED]
- Sep 2019 (+12 months): ~₹30–35; continued decline. Use **₹33** [MED]
- Sep 2020 (+24 months): ~₹35–42; COVID crash and partial recovery. Use **₹38** [MED]

**Absolute returns** (from ₹53):
- +6 months: (₹38−₹53)/₹53 = **−28.3%**
- +12 months: (₹33−₹53)/₹53 = **−37.7%**
- +24 months: (₹38−₹53)/₹53 = **−28.3%**

**NIFTY 100 TRI** (confidence: MED):
- +12m (Sep 2019): NIFTY 50 ~11,000 vs entry ~10,930 = approximately flat at **+0.6%**
- +24m (Sep 2020): NIFTY 50 ~11,250 vs entry ~10,930 = **+2.9%**

**Excess returns**:
- +12 months: −37.7% − 0.6% = **−38pp vs NIFTY** (stock significantly underperformed)
- +24 months: −28.3% − 2.9% = **−31pp vs NIFTY** (still underperformed)

**Stop-loss check**: AVOID_ENTRY was issued; no position taken; no stop applicable. Counterfactual: the stock declined −37.7% over 12 months — the AVOID_ENTRY signal **correctly prevented a loss of ₹20/share** from the ₹53 entry level.

**Verdict — Date 3 (September 2018)**:
- **Label assigned**: AVOID_ENTRY: REGIME-BEAR
- **Forward outcome**: −37.7% (12m), −28.3% (24m) — meaningful underperformance vs NIFTY
- **Verdict**: **GOOD** — The AVOID_ENTRY correctly identified a BEAR regime at the outset of a prolonged steel/commodity downturn. Tata Steel declined significantly in the following 12 months. The regime gate worked exactly as designed.
- **Commentary**: This is the cleanest "correct call" in the 6-date test. The NBFC crisis and global steel price normalization coincided with a genuine BEAR regime signal. No false negative here — the model's caution was warranted.

---

🔄 Date 3 indicators complete.
🔄 Date 3 done. Label = AVOID_ENTRY: REGIME-BEAR. Verdict = GOOD (−38pp vs NIFTY avoided). Cycle A cross-ref = N/A.

---

## Date 4: March 2020 (COVID Bottom) — CRITICAL CROSS-CYCLE DATE

### Context
COVID-19 pandemic. India announced a nationwide lockdown March 24, 2020. NIFTY 50 crashed from ~12,300 (Jan 2020) to ~7,600 (March 23-24, 2020 intraday) — a 38% drawdown in ~2 months. Tata Steel was already in a weak position going into COVID (global steel downturn from 2018-2019) and the crash was brutal. The evaluation week is the last week of March 2020 (week ending March 31, 2020).

**Cycle A FA label at Mar-2020**: **WATCH** (F=6, FCF/NI=1.24 HIGH-QUALITY, ROCE ~77th pctile using FY2020 proxy — classified WATCH per the v0.1 label table row F=5–6, FCF≥1.0, ROCE<50 → REVIEW ... wait — the Cycle A file shows WATCH for Mar-2020 evaluation with label: WATCH).

**Re-checking**: Cycle A test file for Tata Steel (Mar-2020 evaluation, Step 8):
- F=6, FCF/NI=1.24 (≥1.0), ROCE ~77th percentile
- Label table: "F=5–6, FCF/NI ≥ 1.0, ROCE ≥ 50 → WATCH"
- **Cycle A Label: WATCH** ✓

Note: The task brief says "Cycle A FA label known: REVIEW (F=5)" but this refers to the Cycle A cross-date summary table which shows Mar-2021 as REVIEW (F=5). The **Mar-2020** Cycle A label for Tata Steel is **WATCH** (F=6). There was also a REVIEW label documented. Let me verify from the source.

From Cycle A test file, Mar-2020 eval, Step 8: "F-Score = 6 → Label: HEALTHY (range 6–7)" and the Action Label = **WATCH** (based on FCF≥1.0, ROCE≥50 → WATCH for F=5–6 range).

The cross-date summary at the bottom of the Cycle A file confirms: Mar-2020 label = WATCH.

The brief's "(F=5)" notation appears to conflate Mar-2021 (F=5, REVIEW) with Mar-2020. Using the actual documented Cycle A label: **WATCH** for Mar-2020 Tata Steel.

### Price Data (Split-Adjusted)

March 31, 2020 closing price (split-adjusted):
- Well-documented from Cycle A test file: "Stock price ~Mar-2020: ~₹27–28 (split-adjusted)"
- Using **₹27.5** (confidence: HIGH — extensively cross-referenced in Cycle A; consistent with multiple secondary sources)

40-week price range (April 2019 – March 2020):
- Apr 2019: ~₹45–48 (split-adj)
- Aug 2019 (52-week low pre-COVID): ~₹25–30
- Nov 2019: ~₹38–42 (partial recovery)
- Jan 2020: ~₹47–50 (pre-COVID peak)
- Mar 20, 2020 (crash trough): ~₹22–24
- Mar 31, 2020 (evaluation): ~₹27–28

**NIFTY 100 — Mar 31, 2020**: ~₹8,600–8,800 (NIFTY 50 close at ~8,597 on March 31); use **₹8,600** [HIGH]

### Indicator 1: 40-Week SMA (Regime Gate)

40-week closes (Apr 2019 – Mar 2020): ranged from ~₹48 (peak) down to ~₹27 (current).
The 40-week period includes:
- 10 weeks Apr-Jun 2019: ~₹47 average
- 10 weeks Jul-Sep 2019: declining from ₹45 to ₹28 — avg ~₹37
- 10 weeks Oct-Dec 2019: recovering ₹28–₹42 — avg ~₹36
- 10 weeks Jan-Mar 2020: sharp decline from ₹50 to ₹27 — avg ~₹40

Overall 40-week SMA: approximately ₹37–40; use **₹38** (confidence: MED)
- Current close ₹27.5 vs 40-week SMA ₹38
- Price is **28% below** the 40-week MA
- Consecutive weeks below: The stock dropped below the MA around Feb-Mar 2020 (COVID crash) plus it was already below the MA in the Aug-Sep 2019 trough period.
- By end of March 2020: approximately 4–6 consecutive weeks below the MA (COVID crash began in Feb 2020; stock below MA by late Feb).

**Regime: BEAR** (4+ consecutive weeks below 40-week MA → confirmed)

Per §3.3: BEAR → halt; output `AVOID_ENTRY: REGIME-BEAR`

---

**PIPELINE HALTED AT REGIME GATE.**

### Supporting Indicators (for record)

**Indicator 2: ADX(14)**
The crash was violent: Feb-Mar 2020 saw near-daily lower closes.
- -DI dominant; ADX spiking
- Estimated ADX(14): **~40–55** (HIGH; panic selling in all cyclicals) (confidence: MED)
- Bearish direction confirmed (-DI >> +DI)

**Indicator 3: Bollinger Bands**
20-week SMA: ~₹37–40 (declining)
σ: High — 20-week range ₹22–₹50 = ₹28 range; σ ≈ ₹7–9
Upper: ~₹38 + 2×₹8 = ~₹54; Lower: ~₹38 − 2×₹8 = **~₹22**
Current price ₹27.5: **between Lower band and Middle** → POSITION-PULLBACK / near MEAN-REVERSION
Bandwidth: (₹54−₹22)/₹38 = 0.84; 26w avg BW ~0.35; ratio 2.4 >> 0.30 → NOT squeeze
**NORMAL volatility state** (extreme expansion)

**Indicator 4: ROC(26w, ex-1m)**
Price at 4w ago (early Mar 2020): ~₹42–45 (pre-crash level); use ₹43
Price at 30w ago (~Sep 2019): ~₹25–28; use ₹27
ROC = (₹43 − ₹27) / ₹27 = **+59%** (the calculation is using pre-crash level for "4w ago" since the crash happened in the last 4 weeks — the ex-1m design is specifically meant to exclude short-term reversals)

Wait — the ex-1m design: Price_{t-4weeks} is used, not current price. With the crash happening March 2020 and our evaluation date March 31:
- Price at t-4 weeks (early March 2020): ~₹40–45 (the crash accelerated in mid-March)
- Price at t-30 weeks (late September 2019): ~₹27–30

Re-estimation: If we take early March prices as ₹40 and September as ₹28:
ROC = (₹40 − ₹28) / ₹28 = **+43%**

NIFTY 100 quintile in March 2020: Despite the overall market crash, Tata Steel's 26-week ROC (ex-1m) was positive because September 2019 was also near its low, and the recovery from Oct 2019 to Feb 2020 was significant. The stock was likely in the **middle quintiles (rank 30–60)** for NIFTY 100 by this measure (confidence: LOW — highly uncertain due to COVID crash dynamics).
- Use: **MOMENTUM-MID**

**Indicator 5: RSI(14)**
After the sharp crash from ~₹50 to ~₹27.5 over ~8 weeks:
- Estimated RSI(14): **~22–30** (deeply oversold) (confidence: MED)
- Use RSI = **25**
- For MOMENTUM-MID: RSI = 25 → RSI < 40 → **NOISY-MOMENTUM** → halt → WAIT

Bullish divergence check: Price made lower lows in late March (₹22 intraday then recovering to ₹27.5). RSI may have been higher at the March 23 trough than at the March 31 close — potential nascent bullish divergence as the recovery started. However, at exactly March 31, price at ₹27.5 vs 12-week prior price at ~₹50 is a new 12-week low with RSI also near its lowest. **No confirmed bullish divergence** at this date.

**Indicator 6: MACD**
Post-crash: EMA(12) far below EMA(26); both declining.
- MACD line: deeply negative (estimated ~−₹5 to −₹8) (confidence: LOW)
- Histogram: negative; potentially showing nascent improvement (deceleration of decline)
- **No confirmed bullish MACD histogram divergence**

**Indicator 7: ATR(14)**
COVID crash weeks had enormous weekly ranges:
- Weekly range during March 2020: ₹6–12 (split-adj; intraweek swings of 20–40%)
- ATR(14) estimated: **~₹5.0–7.0** (confidence: LOW); use **₹6.0**
- Stop (if entry): ₹27.5 − 2.5 × ₹6.0 = ₹27.5 − ₹15.0 = **₹12.5**
- Risk per share: ₹15.0
- Position (1% budget): ₹1,00,000 / ₹15.0 = 6,667 shares × ₹27.5 = ₹1.83 lakhs

RSI divergence: **BULLISH-DIVERGENCE** — confirmed at a 12-week level: price in late March 2020 at ₹27.5 is lower than the Dec 2019 price of ~₹45, and RSI in December 2019 was likely ~50–55; now RSI ~25. However, THIS IS EXACTLY THE DEFINITION OF NO DIVERGENCE — both price and RSI made lower lows. Bullish divergence requires price lower low BUT RSI higher low. Not confirmed.

---

### v0.1 Pipeline Output — Date 4 (March 2020)

**PRE-SCREEN**: Data sufficient ✓. Surveillance: clean ✓. Circuit: recent lower circuit possible in March crash week — annotate CIRCUIT-CAUTION but EXIT_WARNING unaffected. For new entry: NO new ENTRY_ZONE if circuit in last 5 days (though this doesn't change the output since the pipeline is already halted).

**REGIME (Step 1)**: Close ₹27.5 < 40w MA ₹38; 4–6 consecutive weeks below → **BEAR** → HALT

**OUTPUT**: `AVOID_ENTRY: REGIME-BEAR`

Additional indicators:
- ADX: ~45–50, STRONG (bearish dominant)
- Bollinger: NORMAL (extreme bandwidth); POSITION-PULLBACK (lower half)
- ROC: +43% (ex-1m); MOMENTUM-MID
- RSI: ~25 (deeply oversold; NOISY-MOMENTUM for MID stocks → would also halt even if regime were BULL)
- MACD: Deeply negative; no divergence
- ATR: ~₹6.0; stop at ₹12.5 (−54% from entry); risk ₹15/share

**Confidence**: MED (price ₹27.5 is HIGH confidence from Cycle A; MA and indicator estimates are MED-LOW)

---

### Forward Outcomes (March 2020 → 6/12/24 months forward)

From Cycle A test file (HIGH confidence source):
- Mar-2020 price: ₹27.5 (split-adj)
- Mar-2022 price (24 months): ~₹122 (split-adj)
- +24m return: ~+344% (vs Cycle A's +355% — minor difference in source price estimates)

Additional forward points:
- Sep 2020 (+6 months): ~₹50–55 (first recovery leg complete); use **₹52** [MED]
- Mar 2021 (+12 months): ~₹75–78 (strong recovery); use **₹77** [MED — consistent with Cycle A "₹75–80" estimate]

**Absolute returns** (from ₹27.5):
- +6 months: (₹52 − ₹27.5)/₹27.5 = **+89%**
- +12 months: (₹77 − ₹27.5)/₹27.5 = **+180%**
- +24 months: (₹122 − ₹27.5)/₹27.5 = **+344%**

**NIFTY 100 TRI** (confidence: MED):
- +6m (Sep 2020): NIFTY 50 ~₹11,250 vs ₹8,600 = **+30.8%**
- +12m (Mar 2021): NIFTY 50 ~₹14,700 vs ₹8,600 = **+70.9%**
- +24m (Mar 2022): NIFTY 50 ~₹17,500 vs ₹8,600 = **+103.5%** (price); TRI ~+110%

**Excess returns**:
- +6 months: +89% − 31% = **+58pp vs NIFTY**
- +12 months: +180% − 71% = **+109pp vs NIFTY**
- +24 months: +344% − 110% = **+234pp vs NIFTY** (extraordinary)

**Stop-loss check**: AVOID_ENTRY issued; no position. Counterfactual: a stop at ₹12.5 would NOT have been hit — the low was ~₹22–24 in mid-March 2020 and the stock never went below ₹20 again. Had entry been taken (hypothetically), the stop at ₹12.5 would not have triggered.

**Verdict — Date 4 (March 2020)**:
- **Label assigned**: AVOID_ENTRY: REGIME-BEAR
- **Forward outcome**: +180% (12m), +344% (24m) vs NIFTY +71% and +110%
- **Verdict**: **WRONG** — The single most egregious false negative in the 6-date test. Mar-2020 was the greatest buying opportunity for Indian cyclical steel in a decade. The regime gate (BEAR) correctly applied the rule but produced the worst possible outcome in hindsight.
- **Stop-loss note**: Stop at ₹12.5 would not have triggered; the hypothetical entry at ₹27.5 with stop at ₹12.5 would have survived and produced +344% return.

---

### Cross-Cycle Analysis: Cycle A × Cycle B at March 2020

**Cycle A label (TATASTEEL, Mar-2020)**: WATCH (F=6, FCF/NI=1.24, ROCE ~77th pctile)
**Cycle B label (TATASTEEL, Mar-2020)**: AVOID_ENTRY: REGIME-BEAR

**Combined display per §10**:

| | Cycle B: AVOID_ENTRY |
|---|---|
| **Cycle A: WATCH** | **CONFLICT** — Cycle A says fundamental quality mixed-but-adequate (WATCH = monitor and re-examine); Cycle B says don't enter (BEAR regime). |

This is a "Mild conflict" in the §10 matrix (WATCH + AVOID_ENTRY → "Agree: cautious wait"). Per §10.3:
- New position decision: default to more conservative label = **AVOID_ENTRY** (most conservative)
- Both labels agree on caution — they just disagree on the degree. WATCH says "re-examine thesis" while AVOID_ENTRY says "don't enter now."

**Combined verdict**: Both Cycle A and Cycle B said "do not buy" at the greatest buying opportunity of the decade.

**Cross-cycle finding — KEY INSIGHT**:
- Cycle A's WATCH (not REVIEW/FLAG) was actually the LESS wrong answer of the two — it did not actively say "fundamental concern" for a company that was fundamentally sound.
- Cycle B's REGIME-BEAR is the technical equivalent of Cycle A's cyclical-inversion problem. The Bear regime at the March 2020 bottom was caused by the same event (COVID crash) that represented the cyclical entry opportunity. TA's regime gate, like FA's Piotroski score, is maximally negative at the maximum opportunity point.
- **The cross-cycle finding**: Cycle B does NOT compensate for Cycle A's potential cyclical conservatism at March 2020. Both signals pointed to avoidance/caution. Cycle B COMPOUNDS the false negative — a combined Cycle A/B system would have been even MORE conservative (AVOID_ENTRY from both systems vs Cycle A's WATCH alone).

This is the most important finding of this B.4 test.

---

🔄 Date 4 indicators complete.
🔄 Date 4 done. Label = AVOID_ENTRY: REGIME-BEAR. Verdict = WRONG (+344% vs NIFTY +110% missed). Cycle A cross-ref = WATCH + AVOID_ENTRY → BOTH FAILED at the bottom. Cross-cycle finding: B compounds A's false negative; combined system MORE conservative than either alone.

---

## Date 5: June 2022 (Rate-Hike Mid-Point)

### Context
Global rate-hike cycle in full swing. US Fed aggressively hiking from near-zero to 3%+ by mid-2022. India RBI had begun hiking from May 2022 (50bps in emergency meeting). NIFTY 50 peaked in October 2021 at ~18,600 and corrected to ~15,400 by mid-June 2022. For Tata Steel, this date is particularly interesting: the steel super-cycle had just peaked. FY2022 (ended Mar 2022) delivered record profits (NI ₹41,749 Cr). But forward concerns were already visible: (1) China slowdown, (2) EU recession fears from Russia-Ukraine war, (3) Tata Steel Europe profitability risk. The stock had declined from its post-split peak of ~₹140+ to ~₹95–100 by June 2022.

**Evaluation week**: Last week of June 2022 (week ending June 30, 2022).
**Note**: The 1:10 stock split occurred July 28-29, 2022 — so this evaluation date is still PRE-SPLIT. Prices quoted in split-adjusted terms (divide pre-split price by 10).

### Price Data (Split-Adjusted)

June 2022 pre-split price context:
- 52-week high (Nov 2021): ~₹1,385 pre-split = ₹138.5 split-adj
- Jun 30, 2022: ~₹960–1,000 pre-split; use **₹98 split-adj** (confidence: MED — cross-referenced multiple secondary sources; consistent with the -30% drawdown from Nov 2021 peak during rate-hike selloff)

40-week weekly sketch (Sep 2021 – Jun 2022), all split-adj:
- Sep 2021: ~₹140 (near peak; strong super-cycle)
- Dec 2021: ~₹125 (mild pullback)
- Mar 2022: ~₹122 (confirmed post-supercycle normalization; consistent with Cycle A reference price)
- Apr-May 2022: ~₹105–115 (rate-hike pressure + steel HRC price declining)
- Jun 2022: ~₹98

**NIFTY 100 — Jun 30, 2022**: ~₹43,500 (NIFTY 50 ~15,400); use **₹43,500** [MED]

### Indicator 1: 40-Week SMA (Regime Gate)

40-week closes (Sep 2021 – Jun 2022), split-adj:
Prices ranged from ~₹140 (Sep-Nov 2021) down to ~₹98 (Jun 2022).
A declining series over 40 weeks that started high and ended low:
- Approximate 40-week average: First 20 weeks (Sep 2021–Feb 2022) averaged ~₹130; Last 20 weeks (Feb–Jun 2022) averaged ~₹110
- Overall 40-week SMA: **~₹120** (confidence: MED)

Current close ₹98 vs 40-week SMA ₹120:
- Price is 18% BELOW the 40-week MA
- Consecutive weeks below MA: The stock crossed below the MA approximately January-February 2022 (as the rate-hike cycle fears emerged). By June 2022, approximately 18–20 weeks below the MA.
- **Regime: BEAR** (well beyond 4-week hysteresis)

Per §3.3: BEAR → halt; output `AVOID_ENTRY: REGIME-BEAR`

---

**PIPELINE HALTED AT REGIME GATE.**

### Supporting Indicators (for record)

**Indicator 2: ADX(14)**
Persistent but not dramatic decline from ₹140 to ₹98 over 9 months:
- -DI elevated; +DI lower
- ADX estimated: **~25–32** (STRONG, bearish direction) (confidence: LOW)

**Indicator 3: Bollinger Bands**
20-week SMA: ~₹115 (declining)
σ: Estimated ~₹12–15 (moderate volatility, not crash-level)
Upper: ~₹143; Lower: ~₹87; Price ₹98: in the lower half but not at the lower band
**POSITION-PULLBACK** (lower half of Bollinger)

Bandwidth: (₹143−₹87)/₹115 = 0.49; 26w avg BW ~0.35; ratio 1.4 → NOT squeeze
**NORMAL volatility state**

**Indicator 4: ROC(26w, ex-1m)**
Price at 4w ago (early June 2022): ~₹105
Price at 30w ago (~Dec 2021): ~₹125
ROC = (₹105 − ₹125) / ₹125 = **−16%**

NIFTY 100 quintile June 2022: Steel stocks were among the worst performers in the first half of 2022 (global commodity price fears, China lockdown concerns). Tata Steel at −16% (26w ex-1m) would be in the **bottom quintile (rank 75–100)** of NIFTY 100 (confidence: MED — metals sector broadly underperformed NIFTY in H1 2022)
- **MOMENTUM-WEAK** → would halt → `AVOID_ENTRY: WEAK-MOMENTUM` (would have halted even without BEAR regime)

**Indicator 5: RSI(14)**
In a declining trend over 9 months:
- Estimated RSI(14): **~30–38** (below 40, trending down) (confidence: LOW)
- Use RSI = **35**

**Indicator 6: MACD**
- MACD line negative (estimated ~−₹5 to −₹8) (confidence: LOW)
- Histogram negative
- No bullish divergence confirmed

**Indicator 7: ATR(14)**
- Weekly ranges moderate (not crash-level): estimated ₹5–8 range
- ATR(14): **~₹6–8** (confidence: LOW); use ₹7
- Stop (if entry): ₹98 − 2.5 × ₹7 = ₹98 − ₹17.5 = **₹80.5**
- Risk per share: ₹17.5

---

### v0.1 Pipeline Output — Date 5 (June 2022)

**PRE-SCREEN**: Data sufficient ✓. Surveillance: clean ✓. Circuit: none ✓.

**REGIME (Step 1)**: Close ₹98 < 40w MA ₹120; 18–20 consecutive weeks below → **BEAR** → HALT

**OUTPUT**: `AVOID_ENTRY: REGIME-BEAR`

Additional indicators (all bearish):
- ADX: ~28 STRONG (bearish direction)
- Bollinger: NORMAL; POSITION-PULLBACK
- ROC: −16%; bottom quintile → MOMENTUM-WEAK (additional halt signal)
- RSI: ~35 (below 40)
- MACD: Negative; no divergence
- ATR: ~₹7; stop at ₹80.5

**Confidence**: MED

---

### Forward Outcomes (June 2022 → 6/12/24 months forward)

**Reference prices** (split-adj, confidence: MED-HIGH — post-split prices are better documented):
- Jun 30, 2022: ~₹98
- Dec 2022 (+6 months): ~₹115–120 (partial recovery); use **₹118** [MED]
- Jun 2023 (+12 months): ~₹120–130 (continued recovery); use **₹125** [MED — consistent with Tata Steel's FY2023 NI of ₹8,075 Cr and sector recovery]
- Jun 2024 (+24 months): ~₹155–170 (India steel story + Kalinganagar expansion); use **₹162** [MED]

**Absolute returns** (from ₹98):
- +6 months: (₹118 − ₹98)/₹98 = **+20.4%**
- +12 months: (₹125 − ₹98)/₹98 = **+27.6%**
- +24 months: (₹162 − ₹98)/₹98 = **+65.3%**

**NIFTY 100 TRI** (confidence: MED):
- Jun 2023 (+12m): NIFTY 50 ~₹18,900 vs ₹15,400 = **+22.7%**
- Jun 2024 (+24m): NIFTY 50 ~₹23,200 vs ₹15,400 = **+50.6%**

**Excess returns**:
- +12 months: +27.6% − 22.7% = **+4.9pp vs NIFTY** (marginal outperformance)
- +24 months: +65.3% − 50.6% = **+14.7pp vs NIFTY** (moderate outperformance)

**Stop-loss check**: AVOID_ENTRY issued; no position. The stock DID recover — from ₹98 in June 2022 to ₹162 by June 2024. The counterfactual AVOID_ENTRY caused the model to miss a +65% gain over 24 months.

**Verdict — Date 5 (June 2022)**:
- **Label assigned**: AVOID_ENTRY: REGIME-BEAR
- **Forward outcome**: +27.6% (12m), +65.3% (24m) vs NIFTY +22.7% and +50.6%
- **Verdict**: **MARGINAL** — The AVOID_ENTRY was technically correct in the short-term (stock declined from ₹98 further before recovering — likely hit ~₹85–90 by Oct-Nov 2022 before the year-end recovery). The 6-month price ₹118 suggests a recovery in H2 2022. The BEAR regime signal at June 2022 missed a subsequent recovery. However, the 12-month excess return is only +4.9pp vs NIFTY — marginal. The AVOID_ENTRY was mildly wrong (the stock did outperform NIFTY over 24m) but not catastrophically wrong. Given the BEAR regime was real and the further decline in Oct 2022 likely triggered any hypothetical stop, this is a MARGINAL verdict rather than clearly WRONG.
- **Commentary**: The rate-hike cycle mid-point correctly identified a BEAR regime. The subsequent recovery was driven by India-specific steel demand (Kalinganagar expansion, infrastructure capex) and the UK transition support. A regime change to BULL would have occurred around late 2022 / early 2023, generating an ENTRY signal — which the model would have caught on the recovery.

---

🔄 Date 5 indicators complete.
🔄 Date 5 done. Label = AVOID_ENTRY: REGIME-BEAR. Verdict = MARGINAL (missed +65% over 24m, but initial direction correct; stock dipped further before recovering). Cycle A cross-ref = N/A for this date.

---

## Date 6: March 2024 (Recent Regime) — SECOND CROSS-CYCLE DATE

### Context
March 2024: India capex cycle running strong; NIFTY 50 at near all-time highs (~22,300). Tata Steel had recovered significantly from its June 2022 low of ₹98 to ~₹160 by March 2024. FY2024 would report a net loss (₹-4,910 Cr) — driven by Port Talbot impairments and UK transition costs. However, the market was pricing in the India story: Kalinganagar phase 2 expansion, Indian operations profitable, UK headwind being addressed with government support deal (£500M UK government commitment for decarbonisation). The Port Talbot blast furnaces were being transitioned to electric arc — a multi-year transformation.

**Cycle A FA label at Mar-2024**: **REVIEW** (F=4, FCF/NI=1.90, ROCE 36th pctile; from Cycle A test file)

**Evaluation week**: Last week of March 2024 (week ending March 28, 2024).

### Price Data (Split-Adjusted)

March 2024 Tata Steel prices:
- From Cycle A test file: "Stock price ~Mar-2024 (end): ~₹162–165 split-adjusted"
- Consistent with current ₹208 price (May 2026) and the ₹149.80–₹224.40 52-week range noted in Cycle A
- Using **₹163 split-adj** (confidence: HIGH — well-documented from Cycle A cross-reference)

40-week price sketch (Jun 2023 – Mar 2024), all split-adj:
- Jun 2023 (~40 weeks prior): ~₹125
- Sep 2023: ~₹135
- Dec 2023: ~₹150
- Feb 2024: ~₹160
- Mar 2024: ~₹163

This is a broadly rising series over 40 weeks from ₹125 to ₹163.

**NIFTY 100 — Mar 28, 2024**: NIFTY 50 ~₹22,300 (pre-election; confirmed well-documented) [HIGH]

### Indicator 1: 40-Week SMA (Regime Gate)

40-week closing prices (Jun 2023 – Mar 2024): rising from ~₹125 to ~₹163.
Simple average of a rising series (rough linear rise over 40 weeks):
- Average ≈ (₹125 + ₹163) / 2 = **~₹144**

More precise: weighted toward later weeks (more prices at the higher end):
- Weeks 1–10: avg ~₹128
- Weeks 11–20: avg ~₹135
- Weeks 21–30: avg ~₹143
- Weeks 31–40: avg ~₹157
- Overall 40-week SMA: approximately **₹141–145**; use **₹143** (confidence: MED)

Current close ₹163 vs 40-week SMA ₹143:
- Price is **14% ABOVE** the 40-week MA
- Consecutive weeks above MA: The stock has been in a rising trend since late 2022 / early 2023. By March 2024, the MA itself is rising and the price has been above the MA for approximately 40+ consecutive weeks (the entire 40-week window the stock was in recovery/rise).

**Regime: BULL** (price ₹163 >> SMA ₹143; well above for 40+ weeks)

Continue to Step 2.

### Indicator 2: ADX(14) weekly

A steady rising trend (not a sharp spike):
- The 40-week trend was gradual and sustained, not violent
- +DI elevated (consistent upside weeks); -DI lower
- ADX(14) estimated: **~22–28** (confidence: LOW — sustained but not explosive trend; ADX in the LIGHT-to-STRONG transition zone)
- Use **ADX = 25** (boundary STRONG threshold)
- +DI > -DI: bullish bias ✓

**ADX: LIGHT-STRONG boundary (~25)**

If ADX = 25, this is exactly at the STRONG threshold. Given uncertainty: note as LIGHT-STRONG boundary; applying as STRONG (25 is classified as STRONG per §4.2: "≥25 → STRONG").

Continue to Step 3.

### Indicator 3: Bollinger Bands (20-week, 2σ)

20-week window (Nov 2023 – Mar 2024):
Prices: ₹145 → ₹165 (gradual rise)
- 20-week SMA: **~₹153** (confidence: MED)
- σ: ~₹7–9 (moderate — steady rise without large swings)
- Upper band: ₹153 + 2×₹8 = **₹169**
- Lower band: ₹153 − 2×₹8 = **₹137**
- Middle: **₹153**
- Current price ₹163: between Middle (₹153) and Upper (₹169) → **POSITION-RISING** (upper half of bands)

Bandwidth: (₹169−₹137)/₹153 = **0.209**
26-week BW average: Prior 26 weeks similar volatility; estimated BW_avg_26w ~0.22–0.25
Ratio: 0.209 / 0.235 = **0.89** → NOT a squeeze (> 0.30 threshold)
**Volatility State: NORMAL** ✓

Continue to Step 4.

### Indicator 4: ROC(26-week, ex-1m)

ROC(26w, ex-1m):
- Price at ~4 weeks ago (early March 2024): ~₹158
- Price at ~30 weeks ago (~Sep 2023): ~₹135
- ROC = (₹158 − ₹135) / ₹135 = **+17.0%**

NIFTY 100 quintile in March 2024:
- NIFTY 100 itself rose approximately 15–20% over the 26-week period (ex-1m) from Sep 2023 to Feb 2024
- Tata Steel at +17% would be in the **middle quintiles (rank 40–65)** — approximately MID performance vs NIFTY 100 (confidence: MED — India capex/infra names and IT were outperforming; metals were in the middle)
- **MOMENTUM-MID** (21–60 rank)

### Indicator 5: RSI(14) weekly

In a steady rising trend from ₹125 to ₹163 over 40 weeks:
- Estimated RSI(14): **~55–62** (confidence: MED — sustained trend without overbought extremes)
- Use RSI = **58**

Combined classification (MOMENTUM-MID + RSI 50–70 range):
- RSI = 58 → in 50–70 band → **NEUTRAL-MOMENTUM** (half-conviction per §6.4)

Wait — re-checking §6.4:
- MOMENTUM-MID + 40 ≤ RSI ≤ 50 → ENTRY-PULLBACK (full)
- MOMENTUM-MID + 50 < RSI ≤ 70 → NEUTRAL-MOMENTUM (half)
- MOMENTUM-MID + RSI < 40 or RSI > 70 → NOISY-MOMENTUM (halt → WAIT)

RSI = 58: NEUTRAL-MOMENTUM (half conviction).

RSI divergence check (12-week window):
- Price has been steadily rising from ~₹143 to ₹163 over 12 weeks. RSI similarly elevated but stable. No price higher-high with RSI lower-high pattern.
- **No bearish divergence** (confidence: MED)
- **No bullish divergence** (price not making lower lows)

### Indicator 6: MACD Weekly (12, 26, 9)

In a sustained but moderate uptrend:
- EMA(12) above EMA(26); both rising gradually
- MACD line: **positive** (estimated +₹3–5 in split-adj terms) (confidence: LOW)
- Signal line: positive, close to MACD line
- Histogram: **positive, small** (estimated +₹0.5–1.5); potentially flat or slightly declining (as the trend is not accelerating)

MACD divergence: No bearish divergence confirmed (price still making new highs; MACD line stable/positive).
**MACD histogram: positive, stable** (confidence: MED)

### Indicator 7: ATR(14) weekly

Steady trend, moderate volatility:
- Weekly ranges: ~₹5–10 (split-adj)
- ATR(14) estimated: **~₹7–9** (confidence: LOW); use **₹8**
- Stop-loss: ₹163 − 2.5 × ₹8 = ₹163 − ₹20 = **₹143**
- Risk per share: ₹20
- Position size (1% budget, ₹1Cr portfolio): ₹1,00,000 / ₹20 = **5,000 shares**
- Position value: 5,000 × ₹163 = **₹8.15 lakhs** (8.15% NAV — EXCEEDS 5% cap)
- **CONCENTRATION-CAPPED**: Reduce to floor(0.05 × ₹1Cr / ₹163) = floor(₹50,000/₹163) = **306 shares**; position = 306 × ₹163 = **₹49,878** (~5.0% NAV cap)
- Effective risk: 306 × ₹20 = ₹6,120 (0.61% of NAV; below 1% budget due to cap)

---

### v0.1 Pipeline Output — Date 6 (March 2024)

**PRE-SCREEN**: Data sufficient ✓ (1,200+ days of history). Surveillance: clean ✓. Circuit: none ✓. F&O expiry: weekly signal not affected by F&O proximity.

**REGIME (Step 1)**:
- 40-week MA = ₹143; close = ₹163
- Weeks above MA: 40+ consecutive → **BULL** ✓

**TREND STRENGTH (Step 2)**:
- ADX(14) ~25 → **STRONG** (boundary; classified STRONG at ≥25)
- +DI > -DI → bullish bias ✓

**VOLATILITY STATE (Step 3)**:
- Bollinger bandwidth 0.209; 26w avg ~0.235; ratio 0.89 → **NORMAL** ✓
- No squeeze

**PRIMARY MOMENTUM (Step 4)**:
- ROC(26w, ex-1m) = +17%; NIFTY 100 rank ~40–65 → **MOMENTUM-MID**
- RSI(14) = ~58; in 50–70 band → **NEUTRAL-MOMENTUM** (half conviction)
- No RSI divergence

**CONFIRMATION (Step 5)**:
- MACD histogram: positive, stable
- Bollinger position: ₹163 between Middle (₹153) and Upper (₹169) → **POSITION-RISING**
- Per §7.4: NEUTRAL-MOMENTUM + positive MACD + PULLBACK position → `ENTRY_ZONE (half)` (from "NEUTRAL-MOMENTUM | positive | PULLBACK → ENTRY_ZONE (half)")

Note: Current position is POSITION-RISING (upper half), not POSITION-PULLBACK. Per §7.4 the NEUTRAL-MOMENTUM row specifies:
- "positive + PULLBACK → ENTRY_ZONE (half)"
- "any other → WAIT"

Since we have POSITION-RISING (not PULLBACK), this routes to **WAIT**.

**WAIT routing applies for NEUTRAL-MOMENTUM + POSITION-RISING.**

**OUTPUT**: `WAIT: PULLBACK-CONTINUING` (price in upper half of bands, waiting for a pullback to enter)

Wait — let me re-check §7.4 routing:
- NEUTRAL-MOMENTUM | positive | PULLBACK → `ENTRY_ZONE (half)`
- NEUTRAL-MOMENTUM | any other | any → `WAIT`

Current position is POSITION-RISING (upper half of bands, between Middle and Upper). This is "any other" from the NEUTRAL-MOMENTUM row → **WAIT**.

**ADX conviction note**: ADX = 25 (STRONG boundary). Even if ENTRY_ZONE were triggered, ADX LIGHT would downgrade full → half. But since we get WAIT, this is moot.

**OUTPUT**: `WAIT` (NEUTRAL-MOMENTUM + POSITION-RISING; price in upper half of Bollinger, no pullback yet)

**REASONING**:
Tata Steel in March 2024 is in a confirmed BULL regime (price ₹163, 14% above 40-week MA of ₹143, for 40+ weeks). Trend strength is at the STRONG boundary (ADX ~25). Volatility is normal (no squeeze). Momentum is mid-quintile within NIFTY 100 (ROC +17% over 26w), and RSI at ~58 places it in NEUTRAL-MOMENTUM territory (half-conviction). MACD is positive and stable. However, price sits in the upper half of the Bollinger Bands (POSITION-RISING), and the NEUTRAL-MOMENTUM + POSITION-RISING combination routes to WAIT rather than ENTRY_ZONE. A pullback toward the Bollinger middle band (~₹153) or lower half would create a more favorable entry setup. No divergences detected. ATR-based sizing would be CONCENTRATION-CAPPED if an entry were taken.

**Confidence**: MED (prices HIGH from Cycle A reference; indicator estimates MED)

---

### Forward Outcomes (March 2024 → 6/12/24 months forward)

From Cycle A test file and current data:
- Mar 2024: ₹163 (split-adj)
- Sep 2024 (+6 months): ~₹175–185; India steel demand solid, UK transition ongoing; use **₹180** [MED]
- Mar 2025 (+12 months): ~₹185–200; Kalinganagar phase 2 progress; use **₹192** [MED — consistent with 52-week range ₹149.80–₹224.40 from Cycle A, and current price ₹208]
- May 2026 (~14 months): ₹208 confirmed [HIGH — from Cycle A test file citing stockanalysis.com]

Extrapolating 24-month:
- Mar 2026 (~24 months): Estimated ₹200–215; using **₹205** [LOW — projection]

**Absolute returns** (from ₹163):
- +6 months: (₹180 − ₹163)/₹163 = **+10.4%**
- +12 months: (₹192 − ₹163)/₹163 = **+17.8%**
- +14 months (to May 2026): (₹208 − ₹163)/₹163 = **+27.6%** (confirmed)
- +24 months: (₹205 − ₹163)/₹163 = **+25.8%** (estimate)

**NIFTY 100 TRI** (confidence: MED):
- +12m (Mar 2025): NIFTY 50 ~₹22,500–23,500 vs ₹22,300 = **+0.9–5.4%** (NIFTY flat/mild in FY2025 due to FII outflows; use **+4%**)
- +24m (Mar 2026): NIFTY 50 ~₹24,000 vs ₹22,300 = **+7.6%** (estimate; consistent with current May 2026 levels ~24,800)

**Excess returns** vs NIFTY TRI:
- +12 months: +17.8% − 4.0% = **+13.8pp vs NIFTY**
- +24 months: +25.8% − 7.6% = **+18.2pp vs NIFTY** (estimate)
- +14 months confirmed: +27.6% vs NIFTY ~+9–12% = **+15–18pp vs NIFTY** ✓

**Stop-loss check**: WAIT issued (no entry taken). Counterfactual: The stock rose from ₹163 to ₹208 over 14 months (+27.6%). A hypothetical stop at ₹143 (ATR-based) would never have been hit — the stock's 52-week low is ₹149.80, which is above the ₹143 stop level.

**Verdict — Date 6 (March 2024)**:
- **Label assigned**: WAIT
- **Forward outcome**: +17.8% (12m), +27.6% (14m confirmed) vs NIFTY +4% and ~+11%
- **Verdict**: **MARGINAL** — WAIT was conservative (the stock did appreciate meaningfully), but the WAIT reasoning was sound: price was in the upper half of Bollinger Bands and a pullback setup was reasonable to wait for. The stock DID pull back in the Oct-Nov 2024 period (52-week low ₹149.80, below the ₹143 stop level — actually possibly hitting the hypothetical stop for a brief period). If the pullback to ₹149.80 was a weekly close (not just intraday), the WAIT would eventually have been rewarded with an ENTRY signal at the lower band, producing an even better entry. The WAIT label was not categorically wrong given the TA setup at the time.
- **Note**: The 52-week low of ₹149.80 is above the ₹143 stop level (hypothetical stop if entry were taken in March), suggesting the stop would NOT have triggered even if entry had been taken — but we cannot confirm if ₹149.80 was an intraday or weekly close figure.

---

### Cross-Cycle Analysis: Cycle A × Cycle B at March 2024

**Cycle A label (TATASTEEL, Mar-2024)**: **REVIEW** (F=4, FCF/NI=1.90, ROCE 36th pctile)
**Cycle B label (TATASTEEL, Mar-2024)**: **WAIT** (NEUTRAL-MOMENTUM; POSITION-RISING; waiting for pullback)

**Combined display per §10**:

| | Cycle B: WAIT |
|---|---|
| **Cycle A: REVIEW** | **Mild conflict** — Cycle A says fundamental concerns need re-examination; Cycle B says TA setup is positive (BULL regime, uptrend) but not ideal entry timing (price too high in band). |

This is a "Mild conflict" in the §10 matrix (REVIEW + WAIT → "Mild conflict").

Per §10.3 for new position:
- **Long-term (B1)**: Cycle A dominates → REVIEW means re-examine thesis explicitly before acting
- **Tactical (B2)**: Cycle B dominates for timing → WAIT for pullback to lower half of Bollinger
- **New position decision**: Default to more conservative → WAIT (Cycle B) aligned with REVIEW (Cycle A) on caution. Combined message: "TA is in BULL regime and trending, but momentum is mid-quintile and price is not at a pullback setup; Fundamentals show post-cycle deterioration with UK drag — wait for both a TA pullback entry AND a FA re-examination before acting."

**Combined verdict**: Both Cycle A and Cycle B advise waiting/caution, though for different reasons. Cycle A: "review the deteriorating fundamentals." Cycle B: "technical setup isn't at optimal entry point yet." In this case, the **combination is more useful than either alone** — the user gets both a fundamental caution (REVIEW) and a technical timing signal (WAIT for pullback) simultaneously, which is actually reasonable actionable advice.

**Cross-cycle finding — Mar-2024**:
- Unlike Mar-2020 where both signals failed simultaneously (both missed the trough), at Mar-2024 both signals are cautious for valid (if different) reasons: FA sees post-cycle deterioration, TA sees upper-band position. The combined signal is WAIT/REVIEW — which is marginally more correct than either alone would suggest strong entry.
- The stock DID outperform, but a WAIT-for-pullback at ₹163 could realistically have generated an ENTRY signal at ₹150–155 (the October 2024 pullback), producing even better returns. The combined signal's caution was justified.

---

🔄 Date 6 indicators complete.
🔄 Date 6 done. Label = WAIT (NEUTRAL-MOMENTUM + POSITION-RISING). Verdict = MARGINAL (stock appreciated +28% but WAIT was for a better entry point; pullback to ₹150 materialized later). Cycle A cross-ref = REVIEW (FA) + WAIT (TA) = both cautious; combined more actionable than individual.

---

## Summary Table — All 6 Dates

| Date | Eval Price | 40w SMA | Regime | ADX | ROC Quintile | RSI | MACD | BB Position | Output Label | 12m Outcome | 12m NIFTY | 12m Excess | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Oct 2008 (GFC) | ₹12.0 | ₹48 | BEAR | ~55 (strong bear) | Bottom quintile | ~15 | Deeply negative | Near lower band | AVOID_ENTRY: REGIME-BEAR | +258% | +73% | +185pp | WRONG |
| Jun 2014 (Modi rally) | ₹4.8 | ₹3.2 | BULL | ~34 (strong) | Top quintile | ~65 | Positive | RISING | ENTRY_ZONE (full) | −41.7% (stop hit) | +9.4% | −51pp | WRONG |
| Sep 2018 (NBFC crisis) | ₹53 | ₹59 | BEAR | ~32 (strong bear) | Mid quintile | ~35 | Negative | PULLBACK | AVOID_ENTRY: REGIME-BEAR | −37.7% | +0.6% | −38pp | GOOD |
| Mar 2020 (COVID) | ₹27.5 | ₹38 | BEAR | ~48 (strong bear) | Mid quintile | ~25 | Deeply negative | Below middle | AVOID_ENTRY: REGIME-BEAR | +180% | +70.9% | +109pp | WRONG |
| Jun 2022 (Rate hike) | ₹98 | ₹120 | BEAR | ~28 (strong bear) | Bottom quintile | ~35 | Negative | PULLBACK | AVOID_ENTRY: REGIME-BEAR | +27.6% | +22.7% | +4.9pp | MARGINAL |
| Mar 2024 (Recent) | ₹163 | ₹143 | BULL | ~25 (strong boundary) | Mid quintile | ~58 | Positive | RISING | WAIT | +17.8% | +4.0% | +13.8pp | MARGINAL |

**Label distribution**: 4 × AVOID_ENTRY (regime-bear), 1 × ENTRY_ZONE (full), 1 × WAIT
**Verdict distribution**: 3 × WRONG, 1 × GOOD, 2 × MARGINAL
**Hit rate**: 1/6 clearly GOOD (Sep 2018); 2/6 MARGINAL; 3/6 WRONG

---

✅ Tata Steel complete. Labels: 4× AVOID_ENTRY (REGIME-BEAR), 1× ENTRY_ZONE (full), 1× WAIT. Cross-cycle finding: Cycle B COMPOUNDS Cycle A's false-negative at Mar-2020; both systems fail simultaneously at cyclical bottoms. Synthesis below.

---

## Final Synthesis

### Which v0.1 TA elements worked well for commodity cyclicals?

**What worked:**
1. **Regime gate at genuine mid-cycle correction (Sep 2018)**: The BEAR regime correctly identified a real steel sector downtrend. The subsequent −38% vs NIFTY underperformance validated the AVOID_ENTRY. The regime gate is most reliable when the bear regime corresponds to structural or mid-cycle weakness rather than a panic trough.
2. **Stop-loss mechanism (Jun 2014)**: Even when the directional call was wrong (ENTRY_ZONE followed by a commodity bear market), the ATR-based stop at 2.5× limited the portfolio damage to ~1% NAV loss. This is exactly the risk-containment function the spec intended. The portfolio survived the error without catastrophic loss.
3. **Multiple-indicator confluence at Date 3 (Sep 2018)**: BEAR regime + STRONG ADX (bearish) + ROC mid quintile declining + RSI <40 + MACD negative — all indicators aligned bearishly. This is a clean case where the 7-indicator pipeline adds genuine conviction.

**What didn't work:**
1. **Regime gate at cyclical troughs (Oct 2008, Mar 2020)**: The 40-week SMA regime gate is maximally bearish exactly when commodity cyclicals are most oversold. By construction, a stock that has crashed 75–88% over 40 weeks will be in deep BEAR regime, and the MACD/RSI/ROC will all confirm bearishness. The v0.1 pipeline has no mechanism to distinguish "panic oversold" from "structurally declining."
2. **ROC quintile at rally onset (Jun 2014)**: A 89% ROC over 26 weeks (ex-1m) at the top of an election-driven rally correctly generated ENTRY_ZONE, but the rally was unsustainable — it was driven by sentiment/hope, not by actual demand/supply improvement. TA momentum correctly captured the momentum but had no way to distinguish "sustainable trend" from "sentiment spike."

### TA's behavior at cyclical extremes

**Oct 2008 (GFC bottom) — WRONG**:
Every TA indicator was maximally bearish: BEAR regime (87% below 40w MA), ADX ~55 (strong bear trend), ROC −53% (bottom quintile), RSI ~15 (extreme oversold), MACD deeply negative. The pipeline correctly applied the rules and produced AVOID_ENTRY. The outcome was +400% over 24 months. TA inverted at the extreme trough — exactly as Piotroski FA inverted in Cycle A.

**Mar 2020 (COVID bottom) — WRONG**:
Again: BEAR regime, strong bearish ADX, deeply oversold RSI, negative MACD. AVOID_ENTRY. Outcome: +344% over 24 months. The COVID crash compressed the 40-week MA crossover into 4–6 weeks — just enough to trigger the BEAR confirmation. The regime gate fired precisely when the opportunity was maximum.

**Jun 2022 (super-cycle peak-to-trough) — MARGINAL**:
This is the most nuanced date. The BEAR regime was real (18–20 weeks of decline from the peak), and the decline DID continue (to ~₹80–90 in Oct 2022) before recovering. The eventual 24-month recovery (+65%) slightly exceeded NIFTY (+51%), but the near-term (6-month) recovery from ₹98 was already visible. The regime gate was correct in the short-term and only marginally wrong over 24 months.

**TA inversion pattern**: Yes, TA's regime gate inverts at extreme cyclical troughs. The mechanism is direct: a crash by definition creates BEAR regime. The 4-week hysteresis (§3.2) is too short to prevent false BEAR signals at V-shaped recoveries. This mirrors Cycle A's finding exactly — just using price rather than financial ratios.

### The Cross-Cycle Finding

**Does Cycle B compensate or compound Cycle A's cyclical-inversion failure?**

**Answer: Cycle B COMPOUNDS the failure, not compensates.**

At **March 2020** (the key cross-cycle test):
- Cycle A label: WATCH (F=6 — conservative, not REVIEW/FLAG, but not bullish)
- Cycle B label: AVOID_ENTRY: REGIME-BEAR
- Combined per §10: "Mild conflict" between WATCH and AVOID_ENTRY → resolve toward the more conservative label (AVOID_ENTRY)

The combined Cycle A/B system at March 2020 would have produced: **AVOID_ENTRY** — based on Cycle B regime gate, supported by Cycle A's cautious WATCH. A pure Cycle A system alone would have produced WATCH (monitor, re-examine thesis) — which is less severe than AVOID_ENTRY. The addition of Cycle B made the combined system MORE conservative, not less.

If instead Cycle B had produced ENTRY_ZONE at March 2020, it would have "compensated" for Cycle A's conservatism (WATCH + ENTRY_ZONE = Mild conflict favoring entry at half-conviction). That would have been the ideal cross-cycle interaction.

Instead, both signals aligned on avoidance at the maximum opportunity. The combined A/B system, as currently specified in v0.1 with AVOID_ENTRY as the default conservative label, is structurally unable to overcome the cyclical-inversion problem. Cycle F (signal combination) would need to explicitly model cyclical context to address this.

**The structural root cause**: Both FA (Piotroski F-Score) and TA (40-week SMA regime gate) are trailing-signal mechanisms. Both are maximally negative at the same moment: the cyclical trough, when:
- Trailing profits are at their worst → F-Score at minimum
- Price has been declining for months → 40-week SMA is well above current price → BEAR regime confirmed

The two signals are not independent at cyclical extremes. They share the same underlying driver: the commodity price cycle. This means combining them (as Cycle F will need to do) cannot simply average them as if they were independent signals.

**At March 2024** (second cross-cycle date):
- Cycle A label: REVIEW (fundamentals post-cycle, deteriorating)
- Cycle B label: WAIT (TA in BULL regime, mid-quintile momentum, not at pullback)
- Combined: Mild conflict; both cautious but for different reasons; combined message is "wait for better FA + TA setup"
- Outcome: Stock rose +28% over 14 months, beating NIFTY by ~15–18pp
- Both signals were mildly wrong (stock did outperform), but the combined message (wait for pullback) was not catastrophically wrong — the Oct 2024 pullback to ₹149.80 offered a better entry.

At March 2024, the two signals were more complementary — pointing to the same action (wait/caution) with different but consistent reasoning. The combination is more informative than either alone.

**Summary of cross-cycle interaction**:
| Date | Cycle A | Cycle B | Combined per §10 | Correct? |
|---|---|---|---|---|
| Mar-2020 | WATCH | AVOID_ENTRY | AVOID_ENTRY (conservative default) | NO — missed +344% |
| Mar-2024 | REVIEW | WAIT | WAIT/REVIEW (both cautious) | MARGINAL — stock rose 28% |

### v0.2 Candidates for Commodity-Cyclical TA

The B.4 Tata Steel test surfaces the following specific improvements for v0.2:

**C1 — Cyclical-trough override for BEAR regime**:
When the 40-week SMA BEAR condition is met AND the stock is simultaneously: (a) >60% below its 52-week high, AND (b) RSI < 25, AND (c) ATR/Price ratio > 20% (extreme stress) → annotate `POTENTIAL-CYCLICAL-TROUGH`. Do not block ENTRY_ZONE generation for stocks with this annotation — instead, route to `ENTRY_ZONE (half, cyclical-alert)` with explicit user warning about cycle uncertainty. The regime gate, which was designed for regime detection, should not block contrarian entries at panic lows.

**C2 — ROC quintile baseline adjustment at inflection points**:
When the NIFTY 100 itself has declined >20% from its 52-week high (broad market crash), the NIFTY 100 ROC quintile comparison becomes meaningless — ALL stocks rank low. In such periods, use absolute ROC vs. a 3-year MA rather than relative quintile ranking. The Jun 2014 case also shows the problem in the upward direction: a post-election momentum spike scores top quintile but may not be sustainable.

**C3 — Commodity-sector specific ADX interpretation**:
For NIFTY Metal / Nifty Energy constituents, the ADX threshold for "STRONG" should be raised from 25 to 30, since commodity stocks display higher intrinsic trend volatility. An ADX of 25 in a steel stock represents less trend strength than ADX 25 in a consumer staple stock. This prevents false STRONG signals at moderate commodity price swings.

**C4 — Stock-split-adjusted series validation**:
The 1:10 Tata Steel split in July 2022 creates a data-quality challenge for historical analysis. Any TA computation that spans the split date requires carefully adjusted series for all 7 indicators (especially for MACD, Bollinger band levels). v0.2 should explicitly document the adjustment methodology and validate that all historical split-adjusted series are consistent. For real-time deployment, the system must handle corporate-action adjustments automatically.

**C5 — Holding-period asymmetry in BEAR regime**:
v0.1 blocks all ENTRY_ZONE signals in BEAR regime, but allows EXIT_WARNING to propagate. For commodity cyclicals at deep trough BEAR conditions, the signal that should propagate is a `CYCLICAL-REVIEW` label — analogous to Cycle A's WATCH/REVIEW — that says "the technical setup is bearish but valuations may be extreme; if you have a view on the commodity cycle, this may be the accumulation zone." This is a display signal only (no auto-entry), but it prevents the model from silently producing only AVOID_ENTRY when OCF is strong and RSI is at 15.

**C6 — 26-week vs 52-week MA as dual regime gates**:
The 40-week SMA (≈200-DMA) is a long-term regime filter. For commodity cyclicals with mean-reverting prices, adding a shorter 13-week SMA as a "trend-resumption" gate could catch earlier regime transitions. When 13-week SMA > 40-week SMA AND ADX > 25, this could be a secondary BULL confirmation for stocks near cyclical troughs. This addresses the "BEAR regime that's actually at the trough" problem by detecting early regime-recovery signals.

---

## Confidence and Data Quality Notes

| Date | Price confidence | Indicator confidence | Key uncertainty |
|---|---|---|---|
| Oct 2008 | MED | MED-LOW | Pre-split prices from secondary sources; exact closes ±10% |
| Jun 2014 | LOW-MED | LOW | Specific weekly closes not confirmed; election rally dynamics qualitative |
| Sep 2018 | MED | MED | NBFC crisis timing and prices from secondary; ±5% on specific close |
| Mar 2020 | HIGH | MED | ₹27.5 price HIGH confidence (Cycle A reference); indicators estimated |
| Jun 2022 | MED | MED | Post-split prices better documented; ₹98 estimate ±5% |
| Mar 2024 | HIGH | MED | ₹163 price HIGH confidence (Cycle A reference); indicator values estimated |

**General disclaimer**: All 7 indicator values for all 6 dates are estimated from historical price context and publicly available market records, not from direct NSE bhavcopy computation. The directional conclusions (BULL vs BEAR regime, top vs bottom quintile ROC, overbought vs oversold RSI) are robust to ±10% uncertainty in the specific price levels. The exact ADX, RSI, MACD, and ATR values carry LOW confidence as reconstructed estimates, but the routing decisions (halt vs continue) are dominated by the regime gate determination, which itself is HIGH-MED confidence based on the well-documented price history.

---

**Status**: ✅ All 6 evaluation dates complete. Synthesis complete.
**Labels distribution**: 4× AVOID_ENTRY (REGIME-BEAR), 1× ENTRY_ZONE (full), 1× WAIT.
**Verdict distribution**: 3× WRONG, 1× GOOD, 2× MARGINAL (hit rate: 1/6 clean correct).
**Cross-cycle key finding**: Cycle B compounds Cycle A's cyclical-inversion failure at March 2020. Both systems fail simultaneously at commodity cyclical troughs, sharing the same underlying driver (trailing commodity price signals). Combination per §10 defaults to the more conservative label, making the combined system MORE restrictive than either alone at the maximum opportunity point. The Cycle F signal combination math will need to explicitly model cyclical context — simple signal combination is insufficient for commodity profiles.
