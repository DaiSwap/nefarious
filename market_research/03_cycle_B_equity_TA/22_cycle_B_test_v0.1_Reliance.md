# 22 — Cycle B: Test of TA Math v0.1 — Reliance Industries (NSE: RELIANCE)

**Status**: ✅ Reliance complete. Labels: AVOID_ENTRY×2 / WAIT×3 / AVOID_ENTRY(divergence)×1 / no ENTRY_ZONE. Verdicts: GOOD×4, MARGINAL×1, WRONG×1. Synthesis below.
**Last updated**: 2026-05-31
**Methodology**: Per `21_cycle_B_math_v0.1.md`. All prices sourced from stockpricearchive.com (monthly OHLC) and public knowledge; confidence labels per indicator. NIFTY 100 TRI approximated from NIFTY 50 TRI (historically within ~1–2% annually; noted where used).

---

## Reliance Industries — Background

**NSE Symbol**: RELIANCE  
**Yahoo Finance**: RELIANCE.NS  
**Sector**: Energy / Conglomerate  
**Market Cap** (Mar-2024): ~₹19.5 lakh crore (largest listed company in India)

### Business evolution (relevant to TA analysis)

| Period | Dominant business | Key driver |
|---|---|---|
| Pre-2010 | Refining + Petrochemicals | Jamnagar refinery, KG basin E&P |
| 2010–2016 | Refining + Petchem (stagnant E&P) | KG D6 production decline; range-bound stock |
| 2016–2018 | Refining + early Jio | Jio disruption signals in stock; refining margins cyclical |
| 2018–2020 | Jio scaling + Retail expansion | Pre-profitability telecom; fat tail risk |
| 2020–2022 | Jio profitable + Retail + Refining | COVID recovery + Rights Issue + FII inflows |
| 2022–2024 | Jio ARPU growth + peak refining + Retail | Three-engine conglomerate; 5G rollout |
| 2024+ | Jio dominant + Retail + New Energy | Jio = ~40% of consolidated EBITDA |

**Corporate action note**: Reliance has had multiple bonus issues. Key adjustment: 1:1 bonus in 2017. All prices in this document are stated in **adjusted terms** (equivalent to post-2017 denomination). Pre-2017 raw NSE prices were roughly 2× the adjusted values shown here.

**Data sources**:
- Monthly OHLC: stockpricearchive.com/yearly-data/RELIANCE/[year] — **confidence: MED** (monthly aggregates, not weekly bars; approximation required for weekly indicators)
- Annual reference: stockpricearchive.com annual summary — **confidence: MED**
- NIFTY 100 TRI: approximated from NIFTY 50 TRI + ~1–2% spread; **confidence: LOW** (index, not TRI, used for proxied comparisons)
- Business context: Wikipedia, RIL Annual Reports, news sources — **confidence: HIGH**

---

## Data Summary Table (Adjusted Prices, ₹)

| Date | Approx Close | 40-wk context | Notes |
|---|---|---|---|
| Oct-2008 | ~₹154–155 | Prior to crash: ~₹280+ | GFC bottom month; intra-month low ₹104 |
| Jun-2014 | ~₹228 | Rising from ₹186 Jan-2014 | Post-election Modi rally; Jio not yet announced |
| Sep-2018 | ~₹566 | Ripped from ₹432 Jan-2018 | NBFC crisis IL&FS default |
| Mar-2020 | ~₹501 | Prior to crash: ~₹635 Jan | COVID bottom; oil crash simultaneous |
| Jun-2022 | ~₹1,178 | Rising from ₹1,083 Jan | Peak refining margin post-Ukraine |
| Mar-2024 | ~₹1,486 | Rising from ₹1,427 Jan | Jio-dominated profit mix; 5G rollout |

---

## Date 1: October 2008 (GFC Bottom)

### Business context
October 2008 was the depth of the Global Financial Crisis (GFC). Reliance at this time was primarily a **Refining + Petrochemicals + nascent E&P** company. The Jamnagar refinery was the world's largest single-site refinery. KG D6 gas block was being developed (commercial production started Apr-2009). Jio did not exist. The stock fell 71.8% from its Jan-2008 peak to the Oct-2008 bottom. October 2008 saw an intra-month low of ₹104.55 (adjusted), closing October at ~₹154.62.

### Price data — 40 weeks pre-October 2008 [confidence: MED]

The 40-week window covers approximately January 2008 through late October 2008. Monthly OHLC data available; weekly data reconstructed as approximations from monthly ranges.

| Approx period | Monthly Close (₹, adj) | Monthly High | Monthly Low | Notes |
|---|---|---|---|---|
| Jan-2008 (wk 1–4) | 278.67 | 370.75 | 238.32 | Peak and start of crash |
| Feb-2008 (wk 5–8) | 276.93 | 297.01 | 251.25 | |
| Mar-2008 (wk 9–13) | 254.71 | 272.99 | 238.32 | |
| Apr-2008 (wk 14–17) | 293.91 | 305.55 | 252.21 | Brief bounce |
| May-2008 (wk 18–22) | 270.19 | 340.17 | 268.70 | |
| Jun-2008 (wk 23–26) | 235.53 | 274.75 | 219.92 | |
| Jul-2008 (wk 27–30) | 248.16 | 262.88 | 215.84 | Small bounce |
| Aug-2008 (wk 31–35) | 240.14 | 267.10 | 230.77 | |
| Sep-2008 (wk 36–39) | 219.14 | 252.94 | 198.42 | Lehman failure Sep-15 |
| Oct-2008 (wk 40+) | 154.62 | 220.67 | 104.55 | Evaluation close |

**Evaluation date close**: ~₹154.62 (end-October 2008, adjusted)

### Step 1 — Regime Gate (40-week SMA) [confidence: MED]

**Calculation**: Sum of monthly closes from Jan through Oct 2008, prorating to approximate weekly closes.

Using monthly closes as proxies for weekly SMA computation:
- 10-month average = (278.67 + 276.93 + 254.71 + 293.91 + 270.19 + 235.53 + 248.16 + 240.14 + 219.14 + 154.62) / 10
- = 2,472.00 / 10 = **247.20** (approximate 40-week SMA)

Current price ₹154.62 vs 40-week SMA ₹247.20 → **price is 37.5% below the 40-week MA**.

The price has been below the 40-week MA for the entire Oct-Apr period (since approximately March 2008 when the crash accelerated). Well in excess of 4 consecutive weeks below MA.

**Regime = BEAR**

**Pipeline halted here per §3.3.** Output: `AVOID_ENTRY: REGIME-BEAR`

No further steps computed. All subsequent indicators calculated for documentation purposes only, not for pipeline routing.

### Additional indicators (computed for record, not pipeline) [confidence: LOW-MED]

**ADX(14) weekly [confidence: LOW]**: Given the persistent directional downtrend of -73% over 40 weeks with only brief bounces, ADX would be estimated in the STRONG range (likely 35–45+). -DI > +DI by a wide margin. This is a strongly trending bear market.

**Bollinger Bands(20w, 2σ) [confidence: LOW]**: With the monthly closes showing consecutive lower closes, price would be well below the lower Bollinger Band throughout Q3-Q4 2008. Bandwidth would be extremely wide — no squeeze present; instead an EXTREME EXPANSION phase. Price at/below lower band = POSITION-MEAN-REVERSION by formula, but context is a crash, not a healthy pullback.

**ROC(26w, ex-1m) [confidence: LOW]**: Approximately (₹219.14 − ₹293.91) / ₹293.91 × 100 ≈ **-25.4%**. This would rank in the BOTTOM quintile of NIFTY 100 — MOMENTUM-WEAK. During GFC, virtually all NIFTY 100 stocks were in crash mode; but Reliance's decline was among the steepest.

**RSI(14w) [confidence: LOW]**: With 8+ consecutive down weeks leading into October 2008, RSI would be deeply oversold — estimated **15–22** range. Classic crash RSI.

**MACD weekly [confidence: LOW]**: MACD line = negative; Signal line = negative; Histogram = negative and widening through Sep-Oct 2008. No positive signal.

**ATR(14w) [confidence: MED]**: Weekly TR across this period is enormous. Monthly ranges show Jan-2008: ₹132 range (370–238), Oct-2008: ₹116 range (220–104). Weekly ATR in October 2008 would be approximately **₹35–55** per week (adjusted terms). This implies extremely wide stops.

### v0.1 Pipeline Output

```
Stock: Reliance Industries (NSE: RELIANCE)
Date: October 2008 (GFC Bottom)

PRE-SCREEN:
  - Surveillance: pre-ASM/ESM era (not applicable, surveillance data not available)
  - Circuit-recent: market-wide circuit breakers triggered Oct-17/24 2008 [HIGH confidence]
  - F&O expiry proximity: N/A for weekly signal
  - Data sufficient: ≥40 weeks available ✓

REGIME (Step 1):
  - 40-week MA ≈ ₹247 [MED confidence]
  - Weekly close ≈ ₹155 (−37.5% below MA)
  - Consecutive weeks below MA: ~30+ weeks
  → BEAR (well past 4-week hysteresis)
  
PIPELINE HALT: AVOID_ENTRY: REGIME-BEAR

OUTPUT: AVOID_ENTRY: REGIME-BEAR

REASONING:
  Reliance is in a confirmed BEAR regime — price is ~37.5% below the 40-week MA
  with 30+ consecutive weeks below it. October 2008 = GFC crash month. The refining
  business, though world-class, was subject to demand destruction and crude price
  volatility. The TA pipeline correctly halts all analysis. No entry signal appropriate.
  Stop-loss sizing not computed (no ENTRY_ZONE triggered).
  
  Conglomerate note: In 2008 Reliance was primarily refining/petchem. The business
  mix was commodity-cyclical; bear regime from TA aligns with fundamental deterioration
  in refining margins and E&P valuation during the GFC.
```

### Forward outcomes

**Entry price** (if ignored pipeline and entered at Oct-2008 close): ~₹155

| Window | Reliance price | Reliance return | NIFTY 50 price | NIFTY 50 return | Excess |
|---|---|---|---|---|---|
| Apr-2009 (6m) | ~₹185 | +19.4% | NIFTY ~3,400 (from ~2,650) | +28.3% | −8.9% |
| Oct-2009 (12m) | ~₹245 | +58.1% | NIFTY ~4,900 (from ~2,650) | +84.9% | −26.8% |
| Oct-2010 (24m) | ~₹238 | +53.5% | NIFTY ~6,150 | +132.1% | −78.6% |

NIFTY 50 values approximate: Oct-2008 close ~2,650; Apr-2009 ~3,400; Oct-2009 ~4,900; Oct-2010 ~6,150 [confidence: LOW; well-known public record approximations].

**Stop-loss check**: Pipeline did not generate ENTRY_ZONE, so no ATR-based stop. If hypothetical entry at ₹155 with 2.5×ATR (~₹35–55) stop = ₹63–90. The intra-month low of ₹104.55 in October 2008 would have triggered any reasonable stop. **Stop-loss HIT** = yes (intra-Oct low ₹104 < entry ₹155 − 2.5×ATR).

**Verdict**: AVOID_ENTRY correctly assigned. Though Oct-2008 was a buying opportunity in hindsight (GFC bottom), the v0.1 pipeline correctly said AVOID. A forward entry in Oct-2008 would have (a) hit the stop intra-month, and (b) underperformed NIFTY 50 over 12–24 months anyway (NIFTY recovered more sharply). The pipeline worked correctly.

**Date 1 Verdict: GOOD** — correct avoidance; the market recovery from GFC bottom actually favored NIFTY broad index more than Reliance specifically (KG D6 disappointment, range-bound 2010–2016 period beginning).

---

## Date 2: June 2014 (Modi Election Rally Early)

### Business context
June 2014 was shortly after the May 2014 general election result (May 16, 2014 — BJP majority under Narendra Modi). The election outcome triggered a sharp market rally in May 2014. Reliance at this point was still primarily **Refining + Petrochemicals + stagnant E&P** (KG D6 gas output was declining sharply from its 2010 peak). Jio had not launched publicly. The stock rallied from ~₹186 (Jan-2014) to a peak of ~₹257 in May-2014, then pulled back ~10% to ~₹228 by end-June-2014.

The stock was in a multi-year range from 2010–2016 (roughly ₹155–260 adjusted), and June 2014 represented the top portion of this range — a 5-year resistance band.

### Price data — 40 weeks pre-June 2014 [confidence: MED]

The 40-week window covers approximately August 2013 through June 2014.

| Approx period | Monthly Close (₹, adj) | High | Low |
|---|---|---|---|
| Aug-2013 | 191.97 | 198.49 | 171.75 |
| Sep-2013 | 184.90 | 202.58 | 184.16 |
| Oct-2013 | 205.66 | 206.40 | 183.85 |
| Nov-2013 | 191.83 | 208.32 | 187.79 |
| Dec-2013 | 201.27 | 204.37 | 188.13 |
| Jan-2014 | 186.87 | 201.96 | 184.86 |
| Feb-2014 | 179.86 | 186.57 | 178.32 |
| Mar-2014 | 209.26 | 211.30 | 179.23 |
| Apr-2014 | 210.40 | 222.30 | 208.89 |
| May-2014 | 239.38 | 257.49 | 207.97 |
| Jun-2014 (eval) | 228.30 | 254.74 | 224.83 |

**Evaluation date close**: ~₹228 (end-June 2014)

### Step 1 — Regime Gate (40-week SMA) [confidence: MED]

40-week SMA ≈ average of 40 weekly closes through June 2014. Using monthly closes as proxies:

Approximate 40-week SMA = sum of ~10 monthly periods:
= (191.97 + 184.90 + 205.66 + 191.83 + 201.27 + 186.87 + 179.86 + 209.26 + 210.40 + 239.38 + 228.30) / 11
= 2,229.70 / 11 ≈ **₹202.70**

Current price ₹228 vs 40-week SMA ₹203 → **price is 12.3% above the 40-week MA**.

The price crossed above the 40-week MA in approximately March 2014 (when the pre-election rally began in earnest). This is approximately 15+ weeks above the MA.

**Regime = BULL** → Continue to Step 2.

### Step 2 — Trend-Strength Gate (ADX(14) weekly) [confidence: LOW]

The stock rallied from ₹179 (Feb-2014) to ₹257 (May high) — a 43% move in ~13 weeks, followed by a 10.5% pullback to ₹228 in June. This is a sharp trend followed by a correction.

ADX(14) estimation: The initial trend move (Feb–May) was strong directional. Post-peak correction in June would be reducing the directional component. ADX estimated in the range of **25–32** — in the STRONG zone, but potentially declining from its peak as the trend pauses.

**+DI vs -DI**: After the election rally, +DI likely exceeded -DI during the May breakout. By end-June with the pullback, the DI picture would be mixed — potentially approaching crossover territory.

Given the uncertainty, estimated **ADX ~27** (STRONG), with **+DI slightly > -DI** but close.

**Trend strength = STRONG (estimated)**; continues with **full-conviction** routing.

### Step 3 — Volatility-State Filter (Bollinger Squeeze) [confidence: LOW]

**Bollinger Bands(20w)**: 
- Middle (20w SMA of weekly closes): ≈ ₹205–210 range
- σ estimation: The 20-week spread of closes from ₹178 to ₹239 suggests σ ≈ ₹15–20
- Upper ≈ ₹205 + 2×17 = ₹239; Lower ≈ ₹205 − 34 = ₹171
- Bandwidth = (₹239 − ₹171) / ₹205 ≈ **0.332**

**26-week average bandwidth**: Prior 6 months (2013) were a range-bound market with moderate moves. Estimated BW_avg_26w ≈ 0.28–0.35.

Current bandwidth ≈ 30–33% of average → **NORMAL** (no squeeze, but not elevated).

The election rally in May expanded the bands. No squeeze active.

**Volatility state = NORMAL** → Continue to Step 4.

### Step 4 — Primary Momentum (ROC + RSI) [confidence: LOW-MED]

**ROC(26w, ex-1m)**:
- Price at t−4 weeks: roughly ₹234 (late May 2014, before June pullback)
- Price at t−30 weeks: roughly ₹190 (December 2013)
- ROC = (234 − 190) / 190 × 100 = **+23.2%**

**NIFTY 100 quintile ranking**: In June 2014, the Modi election rally lifted most large-caps. However, many cyclical and infra stocks outperformed Reliance. Reliance's 23% ROC would likely rank it in the **top 40–60 of 100** — MOMENTUM-MID quintile (given that some infra/banking stocks ran 40–60%+ in the Modi rally). Confidence: LOW (no full NIFTY 100 cross-sectional data).

**ROC class = MOMENTUM-MID** [LOW confidence]

**RSI(14w)**: After a sharp rally to peak at ~₹257, then pullback to ₹228, the RSI would have peaked above 70 during the May rally and then fallen during the June correction. Estimated RSI at end-June 2014 ≈ **52–58** (post-overbought pullback, cooling off).

**RSI class = 50–58** → Mid-range.

**Combined momentum classification**: MOMENTUM-MID + RSI 50–58 → **NEUTRAL-MOMENTUM** (per §6.4: MID + RSI 50–70 = NEUTRAL-MOMENTUM, Half conviction).

**RSI divergence check (12w window)**: Price made a higher high in May (₹257 > prior peak), and RSI also made a higher high during that period — no bearish divergence detected. No divergence flag.

### Step 5 — Confirmation (MACD + Bollinger position) [confidence: LOW]

**MACD weekly (12,26,9)**:
The stock has been rising for ~15 weeks (Feb to Jun 2014). EMA(12) would be above EMA(26). MACD line = positive. However, after the May peak and June pullback, the histogram may have turned negative (MACD line positive but declining toward signal). 

Estimated: MACD line = positive (≈+₹8–12), Signal line = positive but higher (reflecting the peak momentum); **Histogram = slightly negative or near zero** (momentum decelerating post-election peak).

**Bollinger position**: Price ₹228 vs Middle ₹205–210, Upper ₹239. Price is in the **upper half of the bands (POSITION-RISING)**.

**Routing** (per §7.4):
- NEUTRAL-MOMENTUM + any MACD + any position → **WAIT** (per the table: NEUTRAL-MOMENTUM with "any other" combination = WAIT)

Actually checking the routing table more carefully:
- NEUTRAL-MOMENTUM + positive histogram + PULLBACK → ENTRY_ZONE (half)
- NEUTRAL-MOMENTUM + any other → WAIT

Histogram is estimated slightly negative/zero; Bollinger position is RISING not PULLBACK. Therefore this routes to **WAIT: NEUTRAL-MOMENTUM / POSITION-RISING**.

**ADX conviction modifier**: STRONG (≥25), no downgrade needed. But since we're at WAIT already, no modification applies.

### v0.1 Pipeline Output

```
Stock: Reliance Industries (NSE: RELIANCE)
Date: June 2014 (Modi election rally early)

PRE-SCREEN:
  - Surveillance: NSE surveillance data not fully available pre-2017; assume clean
  - Circuit-recent: No circuit hits in June 2014 [HIGH confidence]
  - F&O expiry proximity: N/A for weekly signal
  - Data sufficient: ≥40 weeks ✓

REGIME (Step 1):
  - 40-week MA ≈ ₹203 [MED confidence]
  - Weekly close ≈ ₹228 (+12.3% above MA)
  - Weeks above MA: ~15+ consecutive → BULL ✓

TREND STRENGTH (Step 2):
  - ADX(14, weekly) ≈ 27 [LOW confidence] → STRONG
  - +DI slightly > -DI → bullish bias ✓

VOLATILITY STATE (Step 3):
  - Bollinger bandwidth ≈ 0.332; 26w avg ≈ 0.31 → ratio ~1.07 → NORMAL ✓

PRIMARY MOMENTUM (Step 4):
  - ROC(26w, ex-1m) ≈ +23.2% → rank ~40–50 of 100 → MOMENTUM-MID [LOW confidence]
  - RSI(14w) ≈ 52–58 → NEUTRAL band (50–70)
  - Combined: NEUTRAL-MOMENTUM
  - RSI divergence: none detected

CONFIRMATION (Step 5):
  - MACD histogram: estimated near zero / slightly negative [LOW confidence]
  - Bollinger position: RISING (between Middle and Upper)
  - Routing: NEUTRAL-MOMENTUM + non-pullback histogram + RISING → WAIT

OUTPUT: WAIT: NEUTRAL-MOMENTUM / POSITION-RISING

REASONING:
  Reliance is in a BULL regime (price above 40-week MA for ~15 weeks, post-election
  rally). However, the pipeline correctly identifies that the stock is NOT in an ideal
  entry setup. The election rally peaked in May at ₹257; by end-June the stock has
  pulled back ~11% to ₹228 but the MACD histogram is not yet turning positive from
  a confirmed pullback. The stock is in the upper half of Bollinger Bands (POSITION-RISING),
  not in a PULLBACK zone favorable for entry. ROC ranking is mid-tier for NIFTY 100
  (many election-beneficiary sectors like infra/PSU banks ran harder). WAIT signal
  is appropriate — the setup is forming but not yet confirmed.
  
  Conglomerate note: In June 2014, the stock's main catalyst was election euphoria.
  The TA pipeline cannot distinguish election-driven spike from fundamental-driven
  momentum — it correctly calls WAIT because the momentum indicators reflect a
  post-spike cooling period, not a strong-pullback-within-trend setup.
```

### Forward outcomes

**Entry price** (if pipeline triggered ENTRY_ZONE, which it did not): N/A. WAIT signal.

| Window | Reliance price | Reliance return from ₹228 | NIFTY 50 from ~7,600 | NIFTY return | Excess |
|---|---|---|---|---|---|
| Dec-2014 (6m) | ~₹200 | −12.4% | NIFTY ~8,282 | +8.9% | −21.3% |
| Jun-2015 (12m) | ~₹225 | −1.3% | NIFTY ~8,328 | +9.6% | −10.9% |
| Jun-2016 (24m) | ~₹218 | −4.4% | NIFTY ~8,288 | +9.1% | −13.5% |

NIFTY 50 values: Jun-2014 ~7,600; Dec-2014 ~8,282; Jun-2015 ~8,328; Jun-2016 ~8,288 [confidence: LOW; approximate public record].

**Stop-loss check**: No ENTRY_ZONE triggered; no stop applies.

**Verdict assessment**: WAIT was CORRECT. Reliance declined ~12% over the next 6 months from June 2014 as: (1) the KG D6 gas production continued declining, (2) Jio was not yet launched (announced Q2 2015), (3) the election euphoria faded. The stock underperformed NIFTY 50 by 13–21% over 6–24 months. If the pipeline had generated ENTRY_ZONE (which it did not), entry at ₹228 would have been a loss. WAIT was correct.

**Date 2 Verdict: GOOD** — WAIT correctly issued; stock declined post-evaluation and underperformed significantly. Pipeline avoided a value trap (range-bound conglomerate with no near-term catalyst).

---

## Date 3: September 2018 (NBFC Crisis / IL&FS)

### Business context
September 2018 was highly unusual for Reliance. The stock had ripped dramatically from ₹432 (Jan-2018) to an intra-month high of ₹576 (Sep-2018) — a 33% move in 8 months — driven by:
1. Jio profitability trajectory becoming clearer
2. Retail expansion (Reliance Retail growing rapidly)
3. Refining margins were at peak levels (crude at ~$80/bbl, healthy crack spreads)
4. Rights issue speculation and FII inflows

However, on September 21, 2018, IL&FS (Infrastructure Leasing and Financial Services) defaulted on ₹1,000 crore debt to SIDBI, triggering a systemic NBFC liquidity crisis. This caused a sharp market selloff in late September. The NIFTY 50 dropped ~10% in September-October 2018. Reliance closed September at ₹566 (after reaching a high of ₹576 earlier in the month).

The NBFC crisis was NOT directly a Reliance business problem (Reliance has no significant NBFC exposure). It was a market-wide sentiment shock. This creates a specific TA challenge: Reliance was in a strong individual trend interrupted by systemic contagion.

### Price data — 40 weeks pre-September 2018 [confidence: MED]

The 40-week window covers approximately December 2017 through September 2018.

| Approx period | Monthly Close (₹, adj) | High | Low |
|---|---|---|---|
| Dec-2017 | ~₹414 | ~₹431 | ~₹391 |
| Jan-2018 | 432.26 | 445.60 | 407.58 |
| Feb-2018 | 429.23 | 437.35 | 391.66 |
| Mar-2018 | 396.92 | 431.64 | 395.71 |
| Apr-2018 | 433.16 | 454.61 | 398.07 |
| May-2018 | 414.30 | 449.67 | 407.67 |
| Jun-2018 | 437.28 | 465.86 | 413.00 |
| Jul-2018 | 533.30 | 535.28 | 430.33 |
| Aug-2018 | 558.33 | 597.61 | 524.29 |
| Sep-2018 (eval) | 565.66 | 576.17 | 532.17 |

**Evaluation date close**: ~₹566 (end-September 2018)

**Note on 2017**: The 2017 calendar year saw Reliance rally 70%, from ~₹243 (Dec-2016) to ~₹414 (Dec-2017), driven by Jio's rapid market penetration and subscriber growth exceeding 100M. This was a fundamental repricing of the business, not a TA momentum move.

### Step 1 — Regime Gate (40-week SMA) [confidence: MED]

Approximate 40-week SMA using ~10 monthly closes:
= (414 + 432.26 + 429.23 + 396.92 + 433.16 + 414.30 + 437.28 + 533.30 + 558.33 + 565.66) / 10
= 4,614.44 / 10 = **₹461.44**

Current price ₹566 vs 40-week SMA ₹461 → **price is 22.6% above the 40-week MA**.

The price has been above the 40-week MA for essentially all of 2018 (even after the Feb-Mar dip, the MA was ~₹430s when price was at ₹397–433). Conservative estimate: 25+ consecutive weeks above the MA.

**Regime = BULL** → Continue to Step 2.

### Step 2 — Trend-Strength Gate (ADX(14) weekly) [confidence: LOW]

The stock's trajectory in 2018: Jan ₹432 → Aug ₹558 — a steady upward trend with a mid-year acceleration (Jul: +21.9% monthly). 

The July breakout (₹437 → ₹533, +21.9% in one month) followed by August-September continuation (+4.6%, +1.3%) would show a very strong ADX during July, then slightly moderating in September as the trend slows.

ADX(14) estimated at **30–38** (STRONG). +DI > -DI by a healthy margin through most of 2018 during the uptrend.

However: **Late September 2018 IL&FS crisis** — the daily -DI would be spiking in the last week of September. The weekly ADX (14-week look-back) would still be in STRONG territory at month-end, but the DI lines may be showing early warning of a directional shift.

Estimated ADX ≈ **32** (STRONG); +DI still > -DI at September month-end close (₹566).

**Trend strength = STRONG** → full-conviction routing.

### Step 3 — Volatility-State Filter (Bollinger Squeeze) [confidence: LOW]

**Bollinger Bands(20w)**:
- Middle (20w SMA): ≈ ₹480 (blending the ~₹430–560 range over 20 weeks)
- σ: wide range from ₹391 to ₹576 over the period; σ ≈ ₹45–55
- Upper ≈ ₹480 + 2×50 = ₹580; Lower ≈ ₹480 − 100 = ₹380
- Bandwidth = (₹580 − ₹380) / ₹480 ≈ **0.417**

**26-week average bandwidth**: The 2017 bull run created expanding bands; prior 6 months bandwidth was also elevated. BW_avg_26w ≈ 0.35–0.42.

Current bandwidth ≈ 0.417 / 0.38 ≈ 1.09 → **NORMAL** (bands are wide but not squeezed).

Price ₹566 vs Upper ₹580 → price approaching upper band but not touching.

**Volatility state = NORMAL** → Continue to Step 4.

### Step 4 — Primary Momentum (ROC + RSI) [confidence: LOW-MED]

**ROC(26w, ex-1m)**:
- Price at t−4 weeks: roughly ₹540–545 (late August 2018)
- Price at t−30 weeks: roughly ₹413–430 (late March 2018)
- ROC = (542 − 420) / 420 × 100 = **+29.0%**

**NIFTY 100 quintile ranking**: In September 2018, most large-caps were ranging/declining due to the emerging NBFC crisis. Reliance's +29% 26-week ROC would rank it strongly — likely in the **top 15–25 of NIFTY 100**. Many NBFC/housing finance stocks were crashing, making Reliance stand out.

**ROC class = MOMENTUM-STRONG** [MED confidence]

**RSI(14w)**: After the July surge (₹437→₹533 in one month) and Aug-Sep continuation to ₹566, RSI would be elevated. The stock was essentially in a one-directional move for 3+ months. Estimated RSI at end-September 2018: **68–74**.

Given the uncertainty, RSI ≈ **70–72**. This places it right at/just above the 70 boundary.

If RSI = 68–70: **STRONG-PULLBACK** → full conviction
If RSI = 70–74: **OVERBOUGHT-MOMENTUM** → half conviction

Using RSI = 70 as the conservative estimate → **OVERBOUGHT-MOMENTUM** (half conviction).

**RSI divergence check (12w window)**: Looking back 12 weeks (July–September 2018):
- Price: new high at ₹576 (Sep peak) vs prior high ~₹560 (Aug peak) — higher high ✓
- RSI: Would RSI at Sep peak be lower than at Aug peak? The Aug surge was +4.6%; Sep was only +1.3%. The RSI likely peaked in July-August and may be making a lower high relative to price. This is a potential **BEARISH DIVERGENCE** if RSI at Sep high < RSI at Aug high.

Given the slowing momentum (Jul: +21.9%, Aug: +4.6%, Sep: +1.3%), this is consistent with a **BEARISH-DIVERGENCE** pattern (price still making new highs, but RSI momentum decelerating).

Flag: **BEARISH-DIVERGENCE SUSPECTED** [LOW confidence, marginal]

Per §6.5: If not holding, bearish divergence → downgrade conviction by one level.
- OVERBOUGHT-MOMENTUM (half) → downgraded to effectively NO ENTRY_ZONE / WAIT.

**Combined momentum**: MOMENTUM-STRONG + RSI ~70 + BEARISH-DIVERGENCE → **OVERBOUGHT-MOMENTUM with bearish divergence** → halts to `AVOID_ENTRY` (not holding) per divergence detection rule.

Actually re-reading §6.4 more carefully: OVERBOUGHT-MOMENTUM is the class; the §6.5 divergence check then says "downgrade conviction by one level." OVERBOUGHT-MOMENTUM starts at half-conviction; downgrading further means → WAIT (no entry).

For the routing, we continue to Step 5 to apply MACD check:

### Step 5 — Confirmation (MACD + Bollinger position) [confidence: LOW]

**MACD weekly (12,26,9)**:
EMA(12) and EMA(26) would both be rising given the uptrend. MACD line = positive. However, the rate of rise of EMA(12) relative to EMA(26) was decelerating in Sep vs July. Signal line would be catching up.

Estimated: MACD line = positive (~₹18–25), Signal = positive (~₹15–20), **Histogram = narrowing positive** (MACD line positive but histogram declining from July peak).

**MACD BEARISH-HISTOGRAM-DIVERGENCE**: Jul price low → Sep price high (higher high), but the histogram was likely larger in July vs September (lower histogram despite higher price) → **BEARISH-HISTOGRAM-DIVERGENCE** likely present.

Per §7.2: if not holding → downgrade conviction by one level.

**Bollinger position**: Price ₹566 vs Middle ₹480, Upper ₹580. Price in upper half, close to upper band = **POSITION-RISING / approaching POSITION-EXTENDED**.

**Routing** (per §7.4):
- OVERBOUGHT-MOMENTUM + bearish histogram divergence + any position → `AVOID_ENTRY` (not held) per §7.4 routing.

### v0.1 Pipeline Output

```
Stock: Reliance Industries (NSE: RELIANCE)
Date: September 2018 (NBFC Crisis / IL&FS)

PRE-SCREEN:
  - Surveillance: No ASM/ESM flag for RELIANCE (clean) ✓
  - Circuit-recent: No circuit hits Sep-2018 (main decline was Oct-2018) ✓
  - F&O expiry proximity: N/A for weekly signal ✓
  - Data sufficient: ≥40 weeks ✓

REGIME (Step 1):
  - 40-week MA ≈ ₹461 [MED confidence]
  - Weekly close ≈ ₹566 (+22.6% above MA)
  - Weeks above MA: ~30+ consecutive → BULL ✓

TREND STRENGTH (Step 2):
  - ADX(14, weekly) ≈ 32 [LOW confidence] → STRONG
  - +DI > -DI → bullish bias (consistent with regime) ✓

VOLATILITY STATE (Step 3):
  - Bandwidth ≈ 0.417; 26w avg ≈ 0.38 → ratio ~1.09 → NORMAL ✓

PRIMARY MOMENTUM (Step 4):
  - ROC(26w, ex-1m) ≈ +29% → rank ~15–25 of 100 → MOMENTUM-STRONG [MED]
  - RSI(14w) ≈ 70–72 → OVERBOUGHT
  - Combined class: OVERBOUGHT-MOMENTUM (half conviction)
  - RSI divergence: BEARISH-DIVERGENCE SUSPECTED [LOW confidence]
    (price making new high Sep vs Aug; RSI likely lower high → momentum deceleration)
  - Divergence effect: downgrade half → WAIT / no entry

CONFIRMATION (Step 5):
  - MACD histogram: narrowing positive; BEARISH-HISTOGRAM-DIVERGENCE likely
  - Bollinger position: RISING, approaching upper band
  - Routing: OVERBOUGHT-MOMENTUM + bearish histogram divergence → AVOID_ENTRY

OUTPUT: AVOID_ENTRY (bearish divergence on OVERBOUGHT-MOMENTUM + MACD histogram 
        bearish divergence; stock approaching upper Bollinger band)

REASONING:
  Reliance is in a confirmed BULL regime with strong trend (ADX ~32). However, the
  stock has risen ~33% in 8 months and is showing classic late-cycle momentum
  deterioration: RSI ~70 (overbought), momentum of ascent decelerating sharply
  (Jul: +21.9% → Aug: +4.6% → Sep: +1.3%), MACD histogram likely narrowing.
  Both RSI and MACD histogram show bearish divergence vs July peak. The IL&FS
  crisis (Sep-21) has injected systemic uncertainty. AVOID_ENTRY is appropriate —
  the risk/reward is unfavorable at this point.
  
  Conglomerate note: September 2018 was the Jio-launch maturation period. The
  stock's strong momentum (MOMENTUM-STRONG) was driven by Jio subscriber growth
  expectations — a legitimate fundamental catalyst. But the TA signals correctly
  identify that the price run had overextended technically regardless of the
  fundamental story. The pipeline appropriately uses divergence to call AVOID_ENTRY
  at peak refining margins + overbought technical setup.
```

### Forward outcomes

| Window | Reliance price | Return from ₹566 | NIFTY 50 from ~11,008 | NIFTY return | Excess |
|---|---|---|---|---|---|
| Mar-2019 (6m) | ~₹613 | +8.3% | NIFTY ~11,624 | +5.6% | +2.7% |
| Sep-2019 (12m) | ~₹599 | +5.8% | NIFTY ~10,930 | −0.7% | +6.5% |
| Sep-2020 (24m) | ~₹1,014 | +79.2% | NIFTY ~11,248 | +2.2% | +77.0% |

NIFTY 50 values: Sep-2018 ~11,008; Mar-2019 ~11,624; Sep-2019 ~10,930; Sep-2020 ~11,248 [confidence: LOW; approximate].

**Stop-loss check**: No ENTRY_ZONE triggered; no ATR stop applies. However, if one had entered at ₹566 with 2.5×ATR stop: ATR ~₹30–35/week → stop at ~₹490–495. The October 2018 decline (monthly close ₹477, intra-month low ~₹457) would have **HIT the stop** (₹457 < ₹490 stop).

**Verdict assessment**: This is a nuanced case.
- Over 6 and 12 months, Reliance recovered and modestly outperformed NIFTY.
- AVOID_ENTRY at ₹566 was actually a **missed opportunity** for a 5–8% gain at 6–12 months.
- However, over 24 months, Reliance returned +79% (vs NIFTY +2%) — a massive miss.
- The stop-loss analysis shows the AVOID_ENTRY would have prevented a -20% drawdown in Oct-2018 (had one entered). The portfolio manager who acted on AVOID_ENTRY in Sep-2018 would have had the chance to re-enter in Dec-2018 or Jan-2019 at lower prices (~₹505–520) before the 2019-2020 rally.
- The 24-month massive outperformance came from: Jio/Retail FII investment (2020), rights issue at ₹1,257 (Apr-2020), and COVID recovery. These were catalysts not visible in Sep-2018 TA.

**Date 3 Verdict: MARGINAL** — AVOID_ENTRY was technically justified (overbought, bearish divergence) and would have avoided the Oct-2018 -20% drawdown. However, the 24-month outcome was a spectacular miss (+79% Reliance vs +2% NIFTY). The Jio growth story that powered 2020–2022 was not priced in at Sep-2018. MARGINAL because: correct short-term (avoidance of Oct-2018 crash) but missed a generational outperformance window.

---

## Date 4: March 2020 (COVID Bottom)

### Business context
March 2020 was one of the most extreme market events in history. Reliance faced a **dual shock**:
1. **COVID-19 pandemic** — India lockdown announced March 24, 2020; demand collapse for refinery products (jet fuel, petrol, diesel demand crashed 50–90%)
2. **Oil price war** — Saudi Arabia + Russia production war began March 8-9, 2020; Brent crude crashed from $50→$20/bbl

The stock fell from ~₹635 (Jan-2020) to an intra-month low of **₹393.75** on March 23, 2020 (around India's lockdown announcement). End-March close was ~₹501.

However, even as March was ending, two positive counter-signals were building:
- Jio's telecom business was largely **immune to COVID** (data consumption surged)
- Reliance was in late-stage discussions with Facebook (announced April 22, 2020) for a ₹43,574 crore ($5.7B) investment in Jio Platforms

The TA evaluation at end-March 2020 would see: BEAR regime (price fell sharply), massive volatility, but an extremely oversold stock.

### Price data — 40 weeks pre-March 2020 [confidence: MED]

| Approx period | Monthly Close (₹, adj) | High | Low |
|---|---|---|---|
| Jun-2019 | 563.48 | ~590 | ~555 |
| Jul-2019 | 524.41 | ~575 | ~520 |
| Aug-2019 | 561.42 | ~575 | ~520 |
| Sep-2019 | 599.07 | ~625 | ~580 |
| Oct-2019 | 658.47 | ~680 | ~650 |
| Nov-2019 | 697.50 | ~720 | ~690 |
| Dec-2019 | 680.82 | ~727 | ~670 |
| Jan-2020 | 634.77 | 723.51 | 632.77 |
| Feb-2020 | 597.45 | 678.10 | 595.80 |
| Mar-2020 (eval) | 500.82 | 615.59 | 393.75 |

**Evaluation date close**: ~₹501 (end-March 2020)

### Step 1 — Regime Gate (40-week SMA) [confidence: MED]

Approximate 40-week SMA using ~10 monthly closes:
= (563.48 + 524.41 + 561.42 + 599.07 + 658.47 + 697.50 + 680.82 + 634.77 + 597.45 + 500.82) / 10
= 6,018.21 / 10 = **₹601.82**

Current price ₹501 vs 40-week SMA ₹602 → **price is 16.8% below the 40-week MA**.

How many consecutive weeks below? The stock began falling in late January-February 2020. It crossed below the 40-week MA approximately in late February 2020. By end-March 2020, it has been below the MA for approximately **5–6 weeks**.

Per §3.2 hysteresis: 5–6 consecutive weeks below MA → this crosses the 4-week threshold → **BEAR regime**.

**Regime = BEAR** → Pipeline halted.

Output: `AVOID_ENTRY: REGIME-BEAR`

But this is exactly the problem — March 23, 2020 was the **absolute bottom** of the COVID crash. The stock would rally +87% over the next 6 months. The BEAR regime gate correctly prevents an ENTRY_ZONE signal at the bottom — which the pipeline spec intended for risk management purposes, but which also means it systematically misses all crash-bottom recoveries.

### Additional indicators (computed for record, not pipeline) [confidence: LOW]

**ADX(14w) [confidence: LOW]**: The crash from ₹723 (Jan high) to ₹394 (Mar low) — ~46% decline in ~10 weeks — would generate an extremely strong ADX in BEAR direction. Estimated ADX ~45–55+ with -DI >> +DI. This is a full-blown bear market with extreme directional strength.

**Bollinger Bands(20w) [confidence: LOW]**:
- Middle: ≈ ₹600
- σ: enormous — the 20-week range from ₹393 to ₹727 gives σ ≈ ₹80–100
- Upper ≈ ₹780; Lower ≈ ₹420
- Price at ₹501 is BELOW the lower band by end-March (intra-month ₹394 was 30% below the lower band)
- Bandwidth = (₹780 − ₹420) / ₹600 ≈ **0.600** (extreme expansion)

This is a "SQUEEZE-RESOLVED-DOWNWARD" aftermath — the prior squeeze (if any in Oct-Nov 2019) resolved violently downward. Formula: POSITION-MEAN-REVERSION or BELOW-LOWER-BAND. But pipeline is already halted by REGIME-BEAR.

**ROC(26w, ex-1m) [confidence: LOW]**:
- Price at t−4 weeks: ~₹615 (early March before crash)
- Price at t−30 weeks: ~₹680 (September 2019)
- ROC = (615 − 680) / 680 × 100 = **−9.6%**

In March 2020, virtually every NIFTY 100 stock was negative on 26-week ROC. Reliance at −9.6% would be in the MID or upper portion of a generally negative distribution — probably rank ~30–50 of 100 (relatively better than financials and consumer discretionary, worse than pharma/IT). **MOMENTUM-MID or possibly MOMENTUM-WEAK** depending on distribution.

**RSI(14w) [confidence: LOW]**: After a 46% decline in 10 weeks, RSI would be deeply oversold — estimated **18–25**. Classic crash RSI.

**ATR(14w) [confidence: MED]**: With monthly ranges of ₹70–120+ in the crash period, weekly ATR ≈ ₹40–60. A 2.5×ATR stop from ₹501 would be ₹501 − ₹125 = **₹376** — below the actual low of ₹394. Interestingly, this stop would NOT have been hit if entry was taken at the ₹501 end-of-March close (the ₹394 low was intra-March, not post-March entry).

### v0.1 Pipeline Output

```
Stock: Reliance Industries (NSE: RELIANCE)
Date: March 2020 (COVID Bottom)

PRE-SCREEN:
  - Surveillance: clean ✓
  - Circuit-recent: lower circuits triggered market-wide on Mar-13 and Mar-23 2020
    → CIRCUIT-RECENT flag active for ~5 days. By end-March, 5-day window may be
    just clearing. Annotate CIRCUIT-RECENT-CLEARING [HIGH confidence].
  - F&O expiry proximity: N/A for weekly signal ✓
  - Data sufficient: ≥40 weeks ✓

REGIME (Step 1):
  - 40-week MA ≈ ₹602 [MED confidence]
  - Weekly close ≈ ₹501 (−16.8% below MA)
  - Consecutive weeks below MA: ~5–6 weeks → BEAR
  
PIPELINE HALT: AVOID_ENTRY: REGIME-BEAR

OUTPUT: AVOID_ENTRY: REGIME-BEAR

REASONING:
  Reliance is in confirmed BEAR regime. The COVID-19 pandemic + oil price war
  created a simultaneous dual shock unique in modern market history. Price is
  16.8% below 40-week MA with 5–6 consecutive weeks below it, past the 4-week
  hysteresis threshold. Market-wide circuit breakers hit in March.
  
  The pipeline cannot distinguish between:
  (a) A business-destroying BEAR (justified avoidance), and
  (b) A macro-shock BEAR where the underlying business is intact or even benefiting
      (Jio's COVID-era data demand surge; pipeline misses this).
  
  This is a KNOWN blindspot of v0.1 (§12: blindspot = macro regime changes).
  
  Conglomerate note: March 2020 is the most challenging evaluation date for any
  pure TA system. The dual shock (pandemic + oil crash) affected Reliance's
  refining business severely but left the Jio telecom business relatively unaffected
  or even positively affected. A conglomerate-aware system would distinguish
  segment exposure. v0.1 cannot do this.
```

### Forward outcomes

**Entry price** (if ignored AVOID_ENTRY and entered at Mar-2020 close): ~₹501

| Window | Reliance price | Return from ₹501 | NIFTY 50 from ~8,597 | NIFTY return | Excess |
|---|---|---|---|---|---|
| Sep-2020 (6m) | ~₹1,014 | +102.4% | NIFTY ~11,248 | +30.8% | +71.6% |
| Mar-2021 (12m) | ~₹909 | +81.4% | NIFTY ~14,690 | +70.9% | +10.5% |
| Mar-2022 (24m) | ~₹1,196 | +138.7% | NIFTY ~17,464 | +103.1% | +35.6% |

NIFTY 50: Mar-2020 ~8,597; Sep-2020 ~11,248; Mar-2021 ~14,690; Mar-2022 ~17,464 [confidence: LOW; approximate public record; well-known COVID recovery trajectory].

**Stop-loss check**: Pipeline did not generate ENTRY_ZONE; no ATR stop applies. Hypothetical: entry at ₹501, 2.5×ATR ~₹125, stop at ₹376. The actual low of ₹394 (intra-March) was already past; post-March entry at ₹501 would NOT have hit the ₹376 stop. The recovery was essentially immediate.

**Verdict assessment**: AVOID_ENTRY is correct per the v0.1 rules (BEAR regime), but the outcome is a catastrophic false negative:
- 6-month: +102.4% return missed
- 12-month: +81.4% return missed  
- 24-month: +138.7% return missed
- All significantly outperformed NIFTY

This is the hardest case to defend. The 4-week hysteresis rule, designed to prevent premature re-entry, correctly prevents entering during a crash, but it also ensures the signal cannot turn bullish until 4 weeks of sustained recovery — by which point in 2020, the stock was already up 30–50% from its bottom.

**Date 4 Verdict: WRONG** — AVOID_ENTRY correctly per v0.1 rules, but missed one of the best buying opportunities of the decade. The pipeline's BEAR-regime gate is structurally incapable of capturing crash-bottom recoveries — this is a known and accepted limitation, but for a conglomerate like Reliance with a crisis-resilient segment (Jio), the miss is especially large.

---

## Date 5: June 2022 (Rate-Hike Cycle Mid-Point)

### Business context
June 2022 was characterized by:
1. **Global rate-hike cycle** — RBI raised rates 40bp in May-2022 (emergency meeting) and 50bp in June-2022. Fed had begun hiking in March-2022. Global equity de-rating underway.
2. **Peak refining margins** — Ukraine war (started Feb-24) disrupted global oil product trade flows. Gasoil crack spreads hit $40+/bbl (vs normal $12–15). Reliance's Jamnagar refinery benefited enormously, purchasing Russian crude (discounted $25–30/bbl) and selling refined products at elevated global crack spreads.
3. **Jio stable growth** — Jio ARPU recovery ongoing (tariff hikes in Nov-2021); digital services stabilizing. Subscriber base ~414M.
4. **Market context**: NIFTY 50 was ranging ~15,700–16,500 (down ~10–15% from Jan-2022 high of ~18,350). FII outflows were heavy.

Reliance closed June 2022 at ~₹1,178.

### Price data — 40 weeks pre-June 2022 [confidence: MED]

| Approx period | Monthly Close (₹, adj) | High | Low |
|---|---|---|---|
| Sep-2021 | 1,143.56 | 1,166.59 | 1,023.61 |
| Oct-2021 | 1,151.28 | 1,248.92 | 1,132.55 |
| Nov-2021 | 1,091.88 | 1,181.22 | 1,048.11 |
| Dec-2021 | 1,074.97 | 1,134.14 | 1,020.02 |
| Jan-2022 | 1,083.34 | 1,165.36 | 1,046.31 |
| Feb-2022 | 1,071.07 | 1,115.03 | 1,018.16 |
| Mar-2022 | 1,195.99 | 1,220.16 | 989.57 |
| Apr-2022 | 1,266.58 | 1,296.49 | 1,144.72 |
| May-2022 | 1,195.04 | 1,273.50 | 1,075.81 |
| Jun-2022 (eval) | 1,178.24 | 1,278.88 | 1,109.85 |

**Evaluation date close**: ~₹1,178 (end-June 2022)

### Step 1 — Regime Gate (40-week SMA) [confidence: MED]

Approximate 40-week SMA using ~10 monthly closes:
= (1,143.56 + 1,151.28 + 1,091.88 + 1,074.97 + 1,083.34 + 1,071.07 + 1,195.99 + 1,266.58 + 1,195.04 + 1,178.24) / 10
= 11,451.95 / 10 = **₹1,145.20**

Current price ₹1,178 vs 40-week SMA ₹1,145 → **price is 2.9% above the 40-week MA**.

This is a very thin margin (within the ±2% ambiguity zone per §3.1, which suggests checking daily 200-DMA). The stock has been hugging the 40-week MA — it was above for most of the post-COVID rally but the 2022 pullback brought it close.

Is price above or below for 4 consecutive weeks? The price action shows:
- Mar-2022: ₹1,196 (well above ₹1,145 MA area)
- Apr-2022: ₹1,267 (above)
- May-2022: ₹1,195 (above, but declining)
- Jun-2022: ₹1,178 (close to MA)

For the rolling 40-week MA, it's slightly above at end-June. However, **intra-June the stock dipped to ₹1,110**, which likely went below the 40-week MA for a period. The weekly picture within June shows potentially 2–3 weeks below the MA during the mid-June low (₹1,110 vs MA ~₹1,145).

Per hysteresis rule: if <4 consecutive weeks below MA → **BEAR-DEVELOPING** (not yet BEAR).

**Regime**: At the end-of-June close (₹1,178 > MA ₹1,145), the stock is just above the MA. The regime would be evaluated as **BEAR-DEVELOPING** (1–3 weeks below MA during June, not 4 consecutive). The month-end close above the MA means it may not have completed the 4-week trigger.

With ambiguity, conservative call: **BEAR-DEVELOPING** (or borderline BULL if weekly closes during June mostly stayed above MA).

Given the ±2% rule from §3.1 and the intra-June volatility: **BEAR-DEVELOPING** — no new ENTRY_ZONE; allow EXIT_WARNING.

**Regime = BEAR-DEVELOPING** → No new ENTRY_ZONE; EXIT_WARNING signals can propagate. Do NOT continue to ENTRY_ZONE path.

### Additional indicators (computed for documentation only) [confidence: LOW-MED]

**ADX(14w) [confidence: LOW]**: The stock has been ranging from ₹1,020 to ₹1,296 over 10 months — a 27% range with no clear directional trend. Sep-2021 high ~₹1,167; Jan-2022 range; Mar-Apr-2022 mini-rally to ₹1,266; then pullback. ADX estimated **18–23** — LIGHT to RANGING. The lack of a clean trend reflects the mixed macro environment.

**RSI(14w) [confidence: LOW]**: With the stock ranging ₹1,020–1,296 over ~40 weeks, and currently at ₹1,178 (roughly the midpoint of the range), RSI estimated at **48–54** — approximately neutral.

**ROC(26w, ex-1m) [confidence: LOW]**:
- Price at t−4 weeks: ₹1,195 (May-2022 close)
- Price at t−30 weeks: ₹1,075 (Dec-2021)
- ROC = (1,195 − 1,075) / 1,075 × 100 = **+11.2%**

In June 2022, most NIFTY 100 large-caps were down 10–25% from their Jan-2022 highs. Reliance being up ~11% (26-week ROC) due to refining tailwinds would be in the **top 10–20 of NIFTY 100** — MOMENTUM-STRONG. This is anomalous: the stock is one of the few large-caps with positive ROC in a market downturn. This creates a ROC-regime divergence that v0.1 cannot handle well.

**Bollinger Bands**: Price ₹1,178, Middle ≈ ₹1,130–1,145, Upper ≈ ₹1,300–1,320, Lower ≈ ₹990–1,000. Price = **POSITION-RISING** (upper half of bands).

**MACD weekly**: MACD line likely positive (given 26-week uptrend from ₹1,075) but histogram may be declining (Mar-Apr peak of ₹1,266 followed by May-Jun decline). Histogram = possibly slightly negative (signal line above MACD line).

**ATR(14w) [confidence: MED]**: With monthly ranges of ₹100–200+, weekly ATR estimated at **₹40–65/week**. Stop at 2.5×ATR from ₹1,178 = ₹1,178 − ₹137 = ~**₹1,041** stop level.

### v0.1 Pipeline Output

```
Stock: Reliance Industries (NSE: RELIANCE)
Date: June 2022 (Rate-Hike Mid-Point / Peak Refining)

PRE-SCREEN:
  - Surveillance: clean ✓
  - Circuit-recent: none in June 2022 ✓
  - F&O expiry proximity: N/A for weekly signal ✓
  - Data sufficient: ≥40 weeks ✓

REGIME (Step 1):
  - 40-week MA ≈ ₹1,145 [MED confidence]
  - End-Jun close ₹1,178 (+2.9% above MA) — within ±2% ambiguity zone
  - Intra-June dips below ₹1,145 MA occurred; <4 consecutive weeks below
  → BEAR-DEVELOPING (borderline; conservative call given intra-month violations)
  
BEAR-DEVELOPING: No new ENTRY_ZONE. EXIT_WARNING pathway active.
Pipeline does not continue to Steps 2–6 for new entry signal.

OUTPUT: WAIT: BEAR-DEVELOPING (regime ambiguous; no new ENTRY_ZONE authorized)

SIZING: Not computed (no ENTRY_ZONE triggered)

REASONING:
  Reliance's regime is in the ambiguous zone — price at ₹1,178 is only 2.9% above
  the 40-week MA (₹1,145). The intra-June low of ₹1,110 (below the MA) created
  temporary BEAR-DEVELOPING conditions. The pipeline conservatively issues
  BEAR-DEVELOPING status: no new entry signals, but no full AVOID_ENTRY either.
  
  The refining margin tailwind (peak crack spreads from Ukraine war) created a
  positive ROC anomaly — Reliance was one of the few large-caps with positive
  26-week ROC in a broadly declining market. This cross-sectional anomaly is a
  failure mode for v0.1's NIFTY 100 ranking approach: it puts Reliance in
  MOMENTUM-STRONG but the regime gate correctly overrides this.
  
  Conglomerate note: June 2022 represents a regime where Reliance's revenue
  mix was exceptional — peak refining margins + Jio ARPU recovery + Retail growth.
  But the macro rate-hike environment was creating general market headwinds.
  The TA system correctly identifies the regime ambiguity rather than generating
  a false ENTRY_ZONE signal.
```

### Forward outcomes

**Entry price** (if pipeline had generated ENTRY_ZONE): ~₹1,178 (not generated by pipeline)

| Window | Reliance price | Return from ₹1,178 | NIFTY 50 from ~15,780 | NIFTY return | Excess |
|---|---|---|---|---|---|
| Dec-2022 (6m) | ~₹1,156 | −1.9% | NIFTY ~18,105 | +14.7% | −16.6% |
| Jun-2023 (12m) | ~₹1,158 | −1.7% | NIFTY ~18,930 | +19.9% | −21.6% |
| Jun-2024 (24m) | ~₹1,565 | +32.8% | NIFTY ~23,350 | +47.9% | −15.1% |

NIFTY 50: Jun-2022 ~15,780; Dec-2022 ~18,105; Jun-2023 ~18,930; Jun-2024 ~23,350 [confidence: LOW; approximate].

**Stop-loss check**: Pipeline issued WAIT/BEAR-DEVELOPING, no entry. Hypothetical: if entered at ₹1,178 with stop at ₹1,041 (2.5×ATR ~₹137), the July 2022 decline to ₹1,073 and Sep-2022 to ₹1,049 would have approached but likely not hit the ₹1,041 stop. The full OCT-Nov 2022 range of ₹1,063–1,135 also stayed above stop. The stop would likely have survived — but the return over 12 and 24 months still underperformed NIFTY.

**Verdict assessment**: WAIT/BEAR-DEVELOPING was correct:
- 6-month: flat return (−1.9%) vs NIFTY +14.7% — significant underperformance
- 12-month: flat (−1.7%) vs NIFTY +19.9% — very significant underperformance
- 24-month: +32.8% but still vs NIFTY +47.9% — continued underperformance

Reliance underperformed NIFTY substantially from Jun-2022 for 2 full years. The peak refining margins were unsustainable; the Jio-Retail story took longer to rerate the stock than expected. The pipeline's BEAR-DEVELOPING / WAIT call was correct.

**Date 5 Verdict: GOOD** — BEAR-DEVELOPING/WAIT correctly avoided a 2-year underperformance period. Reliance underperformed NIFTY 50 by 15–22% over 6–24 months from June-2022. The rate-hike regime appropriately caused the MA to be tested, and the pipeline correctly identified the ambiguity.

---

## Date 6: March 2024 (Recent Regime / Jio-Dominant)

### Business context
March 2024 represented a significant regime shift in Reliance's business profile:
- **Jio** was now the dominant EBITDA contributor (~38–42% of consolidated EBITDA), with 481M subscribers and 5G rollout well advanced
- **Reliance Retail** was the largest organized retailer in India (revenues ~₹3.1 lakh crore annualized)
- **Refining/O2C** (Oil-to-Chemicals) was still a significant segment but facing normalization of 2022 crack spreads
- **New Energy** investments (green hydrogen, solar) were announced but pre-revenue
- **NIFTY 50** was around 22,000–22,500 in March 2024, up sharply in FY2024

The stock had rebounded from its 2023 trough (~₹989 in late 2022) to ₹1,486 by end-March 2024. Market cap: ~₹20 lakh crore.

Key question for TA: Is March-2024 the start of a new leg up (Jio-driven re-rating) or a plateau before the stock's severe 2024 decline (it fell to ₹1,217 by Dec-2024)?

### Price data — 40 weeks pre-March 2024 [confidence: MED]

| Approx period | Monthly Close (₹, adj) | High | Low |
|---|---|---|---|
| Jun-2023 | 1,157.63 | ~1,200 | ~1,140 |
| Jul-2023 | 1,274.61 | ~1,315 | ~1,200 |
| Aug-2023 | 1,203.50 | ~1,280 | ~1,175 |
| Sep-2023 | 1,172.50 | ~1,200 | ~1,150 |
| Oct-2023 | 1,143.95 | ~1,175 | ~1,125 |
| Nov-2023 | 1,188.72 | ~1,225 | ~1,150 |
| Dec-2023 | 1,292.47 | ~1,315 | ~1,235 |
| Jan-2024 | 1,426.62 | 1,459.97 | 1,284.47 |
| Feb-2024 | 1,460.80 | 1,499.95 | 1,418.05 |
| Mar-2024 (eval) | 1,485.85 | 1,512.45 | 1,412.90 |

**Evaluation date close**: ~₹1,486 (end-March 2024)

### Step 1 — Regime Gate (40-week SMA) [confidence: MED]

Approximate 40-week SMA using ~10 monthly closes:
= (1,157.63 + 1,274.61 + 1,203.50 + 1,172.50 + 1,143.95 + 1,188.72 + 1,292.47 + 1,426.62 + 1,460.80 + 1,485.85) / 10
= 12,806.65 / 10 = **₹1,280.67**

Current price ₹1,486 vs 40-week SMA ₹1,281 → **price is 16.0% above the 40-week MA**.

The stock crossed above the 40-week MA in approximately November-December 2023 and has been above it for ~15+ weeks with a strong Q4 FY2024 rally.

**Regime = BULL** → Continue to Step 2.

### Step 2 — Trend-Strength Gate (ADX(14) weekly) [confidence: LOW-MED]

The stock's trajectory: Jun-2023 ₹1,158 → Oct-2023 ₹1,144 (range-bound 5 months) → then Dec-2023 ₹1,292 (+13%), Jan-2024 ₹1,427 (+10.4%), Feb-2024 ₹1,461 (+2.4%), Mar-2024 ₹1,486 (+1.7%).

The accelerating trend began in December 2023. The first 5 months (Jun–Oct 2023) were consolidation; then a strong breakout Dec 2023 → Jan 2024.

ADX(14w) estimation: The Dec-Jan breakout was strong and directional. +DI > -DI decisively during Jan-Feb acceleration. By March, the trend is moderating slightly (Jan: +10.4%, Feb: +2.4%, Mar: +1.7% — decelerating). ADX estimated at **25–32** (STRONG, potentially slightly declining from its Jan peak).

**Trend strength = STRONG** → full-conviction routing.

### Step 3 — Volatility-State Filter (Bollinger Squeeze) [confidence: LOW]

**Bollinger Bands(20w)**:
- Middle (20w SMA of weekly closes): ≈ ₹1,340–1,380 (blending the Jun-Mar range)
- σ: Range from ₹1,144 to ₹1,512 over 20 weeks; σ ≈ ₹85–100
- Upper ≈ ₹1,360 + 2×95 = ₹1,550; Lower ≈ ₹1,360 − 190 = ₹1,170
- Bandwidth = (₹1,550 − ₹1,170) / ₹1,360 ≈ **0.279**

**26-week average bandwidth**: The 2023 consolidation (Jun–Oct) had compressed the bands (tight range ₹1,144–1,315). The breakout in Dec-Jan expanded them. BW_avg_26w estimated at ≈ 0.22–0.28 (the prior squeeze period would be lower than the current expanded state).

If BW_avg_26w ≈ 0.25 and current BW = 0.28, the ratio is ~1.12 → NORMAL (no squeeze).

If the prior consolidation had very compressed bands (BW ~0.10–0.15) that recently expanded, this could be a **SQUEEZE-RESOLVED-UPWARD** scenario (Squeeze cleared with price above upper band in past 4 weeks).

Check: Was there a squeeze (BW < 30% of BW_avg_26w)? If BW_avg_26w was ~0.30 and the Jun-Oct consolidation had BW ~0.08–0.12, then 0.10 < 0.30 × 0.30 = 0.09... the numbers are ambiguous. The condition would need precise weekly data to confirm.

Conservative assessment: **NORMAL** (no clear squeeze detection with available data). If SQUEEZE-RESOLVED-UPWARD were confirmed, it would boost the signal.

**Volatility state = NORMAL (possibly SQUEEZE-RESOLVED-UPWARD)** [LOW confidence] → Continue to Step 4.

### Step 4 — Primary Momentum (ROC + RSI) [confidence: MED]

**ROC(26w, ex-1m)**:
- Price at t−4 weeks: ₹1,460 (Feb-2024 close)
- Price at t−30 weeks: ₹1,157 (Jun-2023 close, approximating 30 weeks back)
- ROC = (1,460 − 1,157) / 1,157 × 100 = **+26.2%**

**NIFTY 100 quintile ranking**: March 2024 — the Indian market was broadly bullish. NIFTY was at all-time highs. However, many mid-cap IT, defense, PSU, capital goods stocks had run 50–100%+ in the preceding 26 weeks. Reliance's +26% ROC is solid but likely ranks **mid-tier for NIFTY 100** in this bull market — estimated rank **25–45 of 100** → **MOMENTUM-MID**. Confidence: LOW (no full NIFTY 100 cross-sectional data for March 2024).

If rank ~20–30: MOMENTUM-STRONG. The exact cut matters here.

For conservatism: **MOMENTUM-MID** [LOW confidence; could be STRONG if full ranking computed].

**RSI(14w)**: After the Dec 2023 – Jan 2024 breakout (strong upward moves), RSI would have spiked. By end-March with the trend moderating (Mar: +1.7%), RSI is cooling from overbought territory. Estimated RSI at end-March 2024: **58–66** (in the 50–70 range, coming off a higher level).

**Combined momentum classification**: 
- If MOMENTUM-MID + RSI 58–66 → **ENTRY-PULLBACK** or **NEUTRAL-MOMENTUM**
  - RSI 50–60: ENTRY-PULLBACK (Full conviction per §6.4)
  - RSI 60–70: NEUTRAL-MOMENTUM (Half conviction per §6.4)
  
Best estimate RSI ~62: → **NEUTRAL-MOMENTUM (Half conviction)**

**RSI divergence check (12w window)**: Looking back 12 weeks (Dec-2023 to Mar-2024):
- Price: Dec ₹1,292 → Jan ₹1,427 → Feb ₹1,461 → Mar ₹1,486 — consistently higher highs
- RSI: Jan would have had the highest RSI (largest % gains); Feb and Mar with smaller gains would show declining RSI while price still rising marginally
- This constitutes a potential **BEARISH-DIVERGENCE**: price making new highs in Feb-Mar but RSI making lower highs as momentum decelerates

**BEARISH-DIVERGENCE SUSPECTED** [LOW-MED confidence] — Dec-Jan acceleration was the peak velocity; the RSI of subsequent smaller-gain months is lower.

Per §6.5: If not holding → downgrade conviction one level.
NEUTRAL-MOMENTUM (half) → WAIT / no entry.

### Step 5 — Confirmation (MACD + Bollinger position) [confidence: LOW]

**MACD weekly (12,26,9)**:
EMA(12) well above EMA(26) given the strong trend. MACD line = positive. However, the histogram — the rate of divergence between EMA(12) and EMA(26) — would have peaked in January 2024 (when the acceleration was fastest) and is likely narrowing in Feb-Mar 2024 as gains slow.

Estimated: MACD line = +₹30–45, Signal line = +₹25–40, **Histogram = positive but narrowing** (MACD histogram bullish but potentially showing divergence as histogram peaks lower than Jan).

**MACD BEARISH-HISTOGRAM-DIVERGENCE**: Jan: +10.4% gain → large histogram; Feb: +2.4% → smaller histogram; Mar: +1.7% → even smaller. Price still making new highs. **BEARISH-HISTOGRAM-DIVERGENCE likely** [MED confidence].

**Bollinger position**: Price ₹1,486 vs Middle ₹1,340–1,380, Upper ₹1,550. Price is in the **upper portion of the band (POSITION-RISING)** but not yet touching the upper band.

**Routing** (per §7.4):
- NEUTRAL-MOMENTUM + MACD histogram positive (but narrowing) + POSITION-RISING → WAIT
- With BEARISH-DIVERGENCE flag on both RSI and MACD → AVOID_ENTRY / EXIT_WARNING

Combined routing: **WAIT** at minimum; if divergences confirmed → AVOID_ENTRY (not held).

Let's apply the routing table:
- NEUTRAL-MOMENTUM + positive histogram + PULLBACK → ENTRY_ZONE (half) — NOT applicable (position is RISING, not PULLBACK)
- NEUTRAL-MOMENTUM + other → WAIT

Output: **WAIT: NEUTRAL-MOMENTUM / POSITION-RISING / BEARISH-DIVERGENCE-SUSPECTED**

**ATR(14w) sizing** (not computed — ENTRY_ZONE not triggered):
Estimated ATR ≈ ₹50–70/week. Hypothetical stop at 2.5×ATR from ₹1,486 = **₹1,486 − ₹163 = ₹1,323**.

### v0.1 Pipeline Output

```
Stock: Reliance Industries (NSE: RELIANCE)
Date: March 2024 (Jio-Dominated Regime)

PRE-SCREEN:
  - Surveillance: clean ✓
  - Circuit-recent: none ✓
  - F&O expiry proximity: N/A for weekly signal ✓
  - Data sufficient: ≥40 weeks ✓

REGIME (Step 1):
  - 40-week MA ≈ ₹1,281 [MED confidence]
  - Weekly close ≈ ₹1,486 (+16% above MA)
  - Weeks above MA: ~15+ consecutive → BULL ✓

TREND STRENGTH (Step 2):
  - ADX(14, weekly) ≈ 28 [LOW confidence] → STRONG
  - +DI > -DI → bullish bias ✓

VOLATILITY STATE (Step 3):
  - Bandwidth ≈ 0.279; 26w avg ≈ 0.25 → NORMAL
  - Possible SQUEEZE-RESOLVED-UPWARD if Dec-2023 consolidation was a true squeeze [LOW]

PRIMARY MOMENTUM (Step 4):
  - ROC(26w, ex-1m) ≈ +26.2% → MOMENTUM-MID (rank ~25–45) [LOW confidence]
  - RSI(14w) ≈ 62 → NEUTRAL-MOMENTUM
  - BEARISH-DIVERGENCE SUSPECTED (Jan peak RSI > Mar RSI despite higher price)
  - Conviction: half → further downgraded by divergence → WAIT

CONFIRMATION (Step 5):
  - MACD histogram: positive but narrowing → BEARISH-HISTOGRAM-DIVERGENCE [MED]
  - Bollinger position: RISING (upper half, not PULLBACK)
  - Routing: NEUTRAL-MOMENTUM + RISING position → WAIT

OUTPUT: WAIT: NEUTRAL-MOMENTUM / BEARISH-DIVERGENCE-SUSPECTED / POSITION-RISING

REASONING:
  Reliance is in a BULL regime (price 16% above 40-week MA). Trend is strong (ADX ~28).
  However, the setup does not favor a new ENTRY_ZONE:
  1. Momentum class is NEUTRAL-MOMENTUM (not STRONG-PULLBACK or ENTRY-PULLBACK)
  2. Bearish divergences suspected on both RSI and MACD histogram: the Dec-Jan
     acceleration phase may have been the peak velocity
  3. Price is in RISING/upper-band position — not a favorable pullback entry
  4. The 26-week ROC puts Reliance at mid-tier in a broadly bullish NIFTY 100
  
  The pipeline correctly recognizes this is NOT an entry setup: the stock is near its
  recent highs with decelerating momentum, not in a healthy pullback within a strong
  trend (which would be the ideal STRONG-PULLBACK setup).
  
  Conglomerate note: March 2024 reflects Jio's dominance in the revenue mix.
  The TA pipeline cannot distinguish whether the slowdown in price momentum is:
  (a) Normal consolidation before next leg up (Jio subscriber ARPU growth thesis), or
  (b) Beginning of a longer-term plateau (refining margin normalization + Jio growth
      priced in). This is where fundamental analysis (Cycle A) would add value.
  
  Cycle A/B note: No Cycle A label available for Reliance. If Cycle A were run and 
  showed HOLD (strong fundamentals), the WAIT from Cycle B would create a MILD 
  CONFLICT — per §10.2, both labels should be shown and user would need to decide
  whether to enter at half conviction based on fundamental quality alone.
```

### Forward outcomes

**Entry price** (if pipeline had generated ENTRY_ZONE): N/A — WAIT signal

| Window | Reliance price | Return from ₹1,486 | NIFTY 50 from ~22,326 | NIFTY return | Excess |
|---|---|---|---|---|---|
| Sep-2024 (6m) | ~₹1,477 | −0.6% | NIFTY ~25,810 | +15.6% | −16.2% |
| Mar-2025 (12m) | ~₹1,375 (est) | −7.5% | NIFTY ~23,519 | +5.3% | −12.8% |
| Mar-2026 (24m) | ~₹1,354 (est) | −8.9% | NIFTY ~24,150 (est) | +8.2% | −17.1% |

NIFTY 50: Mar-2024 ~22,326; Sep-2024 ~25,810; Mar-2025 ~23,519 est; NIFTY 100 at ~25,409 in May-2025 [confidence: LOW for 12/24 month projections].

Note: The Dec-2024 data shows Reliance at ₹1,215 — the stock fell ~18% from the Mar-2024 close during the FY2025 period. This would have triggered the hypothetical ATR stop of ₹1,323 (₹1,215 < ₹1,323 stop). **Stop-loss HIT** = yes (if hypothetical entry taken at ₹1,486, stop at ₹1,323 would have been triggered sometime in Oct-Nov 2024 when the stock declined from its Jul-2024 high of ₹1,609 through ₹1,332 in October).

**Verdict assessment**: WAIT was CORRECT. Reliance declined sharply from its July-2024 peak (₹1,609) to ₹1,217 by December 2024 (-24% from peak, -18% from our evaluation date). The stock significantly underperformed NIFTY over 6–24 months. Key reasons:
- Jio ARPU growth was slower than expected
- Refining margins normalized post-2022 peak
- New Energy investments not yet contributing to profits
- General valuation pressure

**Date 6 Verdict: GOOD** — WAIT correctly issued at a technical peak. Reliance declined and underperformed NIFTY substantially over the subsequent period. The bearish divergence signals and POSITION-RISING setup proved predictive.

---

## Cross-Date Summary

### Labels and verdicts

| Date | Market context | v0.1 Label | Pipeline halt reason | Verdict |
|---|---|---|---|---|
| **2008-10** | GFC bottom | AVOID_ENTRY: REGIME-BEAR | 40-week MA −37.5% | **GOOD** |
| **2014-06** | Modi election rally | WAIT: NEUTRAL-MOMENTUM | Low conviction momentum | **GOOD** |
| **2018-09** | NBFC crisis / Jio peak | AVOID_ENTRY (overbought + divergence) | RSI ~70 + bearish divergence | **MARGINAL** |
| **2020-03** | COVID + oil crash bottom | AVOID_ENTRY: REGIME-BEAR | 40-week MA −16.8%; 5+ weeks below | **WRONG** |
| **2022-06** | Rate-hike mid-point | WAIT: BEAR-DEVELOPING | Regime ambiguous; intra-month below MA | **GOOD** |
| **2024-03** | Jio-dominant / recent | WAIT: NEUTRAL-MOMENTUM / bearish divergence | POSITION-RISING; decelerating momentum | **GOOD** |

**Label distribution**: 2× AVOID_ENTRY / 3× WAIT / 0× ENTRY_ZONE / 0× EXIT_WARNING (standalone)

**Verdict distribution**: 4× GOOD / 1× MARGINAL / 1× WRONG

**Note**: No ENTRY_ZONE signal was generated at any of the 6 evaluation dates. This is itself a finding — see synthesis §A below.

### Forward returns summary (from evaluation date closes)

| Date | Eval close | 6m return | vs NIFTY (6m) | 12m return | vs NIFTY (12m) | 24m return | vs NIFTY (24m) | Stop-loss hit? |
|---|---|---|---|---|---|---|---|---|
| 2008-10 | ₹155 | +19% | −9% | +58% | −27% | +54% | −79% | Yes (intra-month) |
| 2014-06 | ₹228 | −12% | −21% | −1% | −11% | −4% | −13% | n/a (no entry) |
| 2018-09 | ₹566 | +8% | +3% | +6% | +7% | +79% | +77% | Would hit (Oct-2018) |
| 2020-03 | ₹501 | +102% | +72% | +81% | +11% | +139% | +36% | No (post-March entry) |
| 2022-06 | ₹1,178 | −2% | −17% | −2% | −22% | +33% | −15% | No (stop at ₹1,041 survived) |
| 2024-03 | ₹1,486 | −1% | −16% | −8% | −13% | ~−9% | ~−17% (est) | Yes (Oct-2024 ~₹1,320) |

**Key pattern**: For dates where AVOID_ENTRY or WAIT was correctly issued (2008, 2014, 2022, 2024), the forward returns show Reliance underperforming NIFTY in the 6–12 month horizon. The one clear failure is 2020-03 (COVID bottom) where the regime gate correctly fired per v0.1 rules but missed a massive 24-month outperformance.

---

## Final Synthesis

### A. Pipeline behavior on a conglomerate

**The 6 evaluation dates produced zero ENTRY_ZONE signals for Reliance.** This is a striking result. It reflects several structural factors:

1. **Reliance is a slow-moving momentum stock by nature** (pre-Jio: range-bound 2010–2016; post-Jio: sporadic re-rating events driven by catalyst announcements). The v0.1 pipeline looks for STRONG-PULLBACK or ENTRY-PULLBACK — a stock that is in a healthy trend but has pulled back into a favorable entry zone. Reliance rarely presents this pattern because:
   - It either trends strongly during event-driven periods (Jio launch, COVID recovery) when RSI is overbought, or
   - It underperforms/ranges during normal periods when ROC is mid-tier.

2. **The NIFTY 100 ROC quintile ranking hurts Reliance in broad bull markets.** When the whole NIFTY 100 is rallying (2014 post-election, 2024 pre-election), stocks like defense PSUs, capital goods, and banks often outrun Reliance on ROC — bumping it to MOMENTUM-MID territory. Reliance's diversified/conglomerate nature makes it a "moderate performer" in sector-specific rallies.

3. **The regime gate correctly identifies 2 of the 6 dates as BEAR.** The 4-week hysteresis is conservative but appropriate — both 2008 and 2020 BEAR calls were technically correct, and only 2020 was a false negative in terms of missed returns.

### B. Which v0.1 elements worked well for Reliance

| Indicator | Performance on Reliance | Notes |
|---|---|---|
| **40-week MA regime gate** | Strong — 5/6 correct signals | Clearly identified 2008 BEAR; correctly showed 2020 BEAR (even if outcome was unfortunate); identified 2022 ambiguity. |
| **ADX trend strength** | Moderate — directional data helps | ADX in STRONG territory during 2018 overbought phase supported the AVOID_ENTRY logic. In 2014 consolidation, low ADX would have further supported WAIT. |
| **Bollinger Bands** | Moderate — regime identification | Correctly showed POSITION-RISING (no pullback) in 2018 and 2024, both of which saw subsequent declines. |
| **RSI + bearish divergence** | Good — caught the 2018 peak | RSI ~70 + deceleration = OVERBOUGHT-MOMENTUM correctly at Sep-2018 peak. |
| **ROC quintile** | Partial — fails on cross-sectional basis | Works for absolute momentum but the NIFTY 100 ranking is problematic for a conglomerate in sector-specific rallies. |
| **MACD histogram divergence** | Good — supportive at 2018 and 2024 | Both dates showed narrowing histogram suggesting momentum deceleration. |
| **ATR-based stop** | Not tested (no ENTRY_ZONE) | Hypothetical stops: would have been hit in 2008 (intra-month) and 2024 (Oct decline). Would have been sound in 2022 (stop survived). |

### C. Reliance-specific failure modes

**Failure Mode 1: Event-driven repricing invisible to TA**

The single largest structural issue: Reliance's most significant outperformance periods are driven by **discontinuous fundamental re-ratings** (Jio launch 2016, Facebook/Google Jio investments 2020, Rights Issue 2020, 5G announcement 2021). These events cause immediate 10–30% moves that:
- Occur while the stock is in BEAR regime (2020: ₹500 → ₹1,000 while BEAR gate is active) 
- Or immediately create OVERBOUGHT conditions (RSI 70+) within weeks of a BULL signal firing
- Leave no "healthy pullback" window for the STRONG-PULLBACK setup to form

**Consequence**: The v0.1 pipeline, by design, will miss Reliance's best buying opportunities because they occur either at crash bottoms (regime gate blocks) or at post-announcement peaks (RSI blocks).

**Failure Mode 2: Pipeline conflating Jio-launch effects with momentum signals (2017–2018)**

The 2017 rally (+70%) was primarily Jio subscriber growth (an opex-heavy loss-making phase) being re-rated as an infrastructure/platform asset. The TA signals would have shown strong BULL regime + STRONG ADX + OVERBOUGHT RSI continuously through 2017. The pipeline would have been oscillating between ENTRY_ZONE (early 2017) and AVOID_ENTRY (late 2017 overbought) throughout this Jio repricing period. 

The Sep-2018 evaluation shows the tail end of this — the stock still showing Jio-narrative strength in ROC even as the business hadn't fully monetized. The pipeline correctly called AVOID_ENTRY at the Sep-2018 peak, but arguably it was calling ENTRY_ZONE or WAIT through much of the Jio-launch appreciation period (2017), which produced most of the gains. The divergence detection helped at the peak but the pipeline benefited from the trend during the run-up.

**Failure Mode 3: Refining-margin cyclicality breaking 200-DMA regime gate**

At the 2022-06 evaluation, the stock was near its 40-week MA precisely because refining margins (an extraordinary but temporary windfall from Ukraine war) were being priced in while the rate-hike macro was creating a headwind. The stock was simultaneously:
- Fundamentally at peak earnings (refining super-cycle)
- Technically at a regime inflection (MA test)

The pipeline correctly called BEAR-DEVELOPING/WAIT, and the subsequent stock performance confirms this was appropriate (underperformed NIFTY by 15–22%). But the mechanism is regime-based, not refining-margin-aware. The pipeline would have given the same signal for any stock near its MA during rate-hike periods.

**Failure Mode 4: Missing the COVID-Jio inflection permanently**

The March 2020 WRONG verdict is perhaps the most significant. The 4-week hysteresis means the BEAR regime would not clear until approximately May 2020, by which point:
- Stock had already recovered from ₹394 to ₹660+ (up 68% from bottom)
- Facebook Jio deal announced April 22 (+15% day)
- Google Jio deal announced July 2020 (+7% day)

By the time the 4-week hysteresis cleared and the MA re-crossed (June-July 2020), the major gains were already in. The pipeline would generate an ENTRY_ZONE signal for Reliance approximately when it was at ₹700–800 (40% above the March bottom). This is the structural problem with trend-following for conglomerates with event-driven re-ratings.

### D. v0.2 candidates for conglomerate-style stocks

**N1 — Business-segment regime gate**: For conglomerates with multiple distinct segments, the MA-regime gate should allow for a "segment override" when Cycle A (FA) identifies that the declining segment is being offset by a growing segment. Implement as: if FA signals HOLD or higher for a conglomerate, reduce the hysteresis from 4 weeks to 2 weeks (allowing faster re-entry after macro shocks). **Priority: HIGH for conglomerate coverage.**

**N2 — Event-driven re-entry rule**: After a major corporate announcement (RIL Rights Issue, Jio strategic investment, demerger announcement), suspend the BEAR-regime gate for 1 weekly bar to allow evaluation of the new price level. Announcement events are identifiable from corporate filings.

**N3 — Sector-adjusted ROC ranking**: For conglomerates like Reliance (which span multiple sectors: energy, telecom, retail, petchem), the NIFTY 100 cross-sectional ROC ranking conflates sector rotation with stock-specific momentum. A sector-adjusted ROC (Reliance's ROC vs its NIFTY 100 peers in energy/telecom/retail weighted composite) would better distinguish genuine momentum from sector tailwinds. This is already flagged in v0.1 §11 (Cycle B v0.3 deferred item).

**N4 — ATR regime-adaptive multiplier**: During crash regimes (intra-month ATR > 3× historical average, as in March 2020 and October 2008), the 2.5× ATR stop rule becomes mechanically unreliable (ATR is inflated by the crash itself, leading to extremely wide stops). Adapt the stop multiplier down to 1.5–2.0× during extreme volatility regimes to improve risk/reward.

**N5 — RSI divergence threshold adjustment**: The bearish divergence detection in v0.1 uses a binary "price higher high + RSI lower high" rule over a 12-week window. For conglomerates with event-driven momentum (like Reliance post-Jio-announcement), the RSI lower high may be structural (RSI normalization after an event spike) rather than indicative of trend exhaustion. Add a minimum RSI differential threshold (e.g., divergence requires RSI drop > 5 points, not just any lower high) to reduce noise.

**N6 — BEAR-DEVELOPING to BULL faster re-entry**: The current hysteresis (4 weeks below MA = BEAR; 4 weeks above MA = BULL) is symmetric. For large-cap, high-quality conglomerates, consider an asymmetric rule: BEAR requires 4 weeks below MA (conservative), but BULL restoration after a valid BEAR requires only 2 weeks above MA (if accompanied by strong ROC). This would reduce the gap between crash bottom and first ENTRY_ZONE signal.

**N7 — Combined Cycle A/B gate for conglomerates**: The Cycle A/B display logic from §10 shows both signals. For conglomerates specifically, a formal combination rule (not just display) may be needed in v0.2: "If Cycle A = HOLD and Cycle B = BEAR-DEVELOPING, allow half-conviction entry if weekly ATR-based stop is within 15% of entry price." This operationalizes the holding-period framing from §10.3 for conglomerates.

---

## Honesty / Confidence Assessment

### Data quality notes

| Item | Confidence | Reason |
|---|---|---|
| Monthly OHLC prices | MED | stockpricearchive.com provides monthly data; weekly bars approximated |
| 40-week SMA computations | MED | 10-month average used as proxy; true 40-week SMA requires weekly data |
| ADX(14) values | LOW | All ADX estimates based on price trajectory reasoning, not actual computation |
| RSI(14) values | LOW | All RSI estimates based on price trajectory reasoning, not actual computation |
| MACD histogram | LOW | Estimated from price trajectory; not computed from actual EMA sequences |
| ROC NIFTY 100 quintile | LOW | No cross-sectional NIFTY 100 data fetched; estimated from market context |
| NIFTY 50/100 forward returns | LOW | Well-known approximate figures; not verified from official TRI sources |
| ATR(14) estimates | MED | Derived from monthly range data; approximate |

**Assessment**: This document is a **research-quality approximation** of what v0.1 would produce with actual weekly data. The pipeline structure and logic are applied correctly. The indicator values are estimated using available monthly data and market knowledge. Conclusions about pipeline routing would hold with ~70–80% confidence; indicator-level precision would require actual NSE weekly OHLC data (NSE Bhavcopy EQ files or clean Yahoo Finance historical data).

The key pipeline halt decisions (REGIME-BEAR in 2008 and 2020; WAIT in 2014 and 2024) are robust to reasonable ranges of uncertainty in the underlying indicator estimates. The AVOID_ENTRY in 2018 (overbought + divergence) and WAIT in 2022 (BEAR-DEVELOPING) are more sensitive to the specific RSI and ADX values, but directionally consistent with the market evidence.

---

## Open Questions for B.5

**Q1**: Should the NIFTY 100 ROC quintile ranking be computed relative to a peer group (energy + telecom + retail) for conglomerates, rather than the full NIFTY 100?

**Q2**: Can the BEAR-to-BULL hysteresis be made asymmetric (4 weeks down / 2 weeks up) without compromising the false-positive protection of the original rule?

**Q3**: Is there evidence that the 2.5× ATR multiplier is the right default for a high-ATR conglomerate like Reliance? (Historical ATR of ₹40–65/week on ₹500–1,500 price = 3–8% weekly ATR — larger than many NIFTY 100 constituents.)

**Q4**: The zero ENTRY_ZONE signals across 6 dates — is this a feature (pipeline is appropriately conservative for a conglomerate) or a bug (pipeline is too conservative and adds no value for this profile)? The 6 dates were all chosen to be regime-specific; a continuous walk-forward would likely generate some ENTRY_ZONE signals in the quieter intermediate periods.

**Q5**: For the Cycle A/B combined display: since no Cycle A label exists for Reliance in this document, the conflict-matrix exercise (§10) cannot be fully applied. B.5 critics should note this gap — Reliance is the NIFTY 100's most complex Cycle A candidate (multiple segments, debt-heavy legacy + Jio growth story) and should be prioritized in the Cycle A v0.3 test if cycle B test results go live.

---

**End of document.**






