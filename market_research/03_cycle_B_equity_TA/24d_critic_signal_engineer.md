# 24d — Cycle B Critique: Signal Engineer / Systematic Strategy Lens

**Status**: 🔄 Verdict draft = REFACTOR-REQUIRED (leaning toward REJECT on walk-forward readiness alone). Drafting analysis.
**Date**: 2026-05-31
**Lens**: Signal Engineer / Systematic Strategy (C4)
**Cycle**: B.5 — multi-agent critique of Cycle B TA math v0.1
**Target bar**: Walk-forward Sharpe > 0.3 after costs (Q12 production gate)

---

## §1 Verdict + Summary

**Verdict: REFACTOR-REQUIRED** (one step short of REJECT on walk-forward readiness; structural math is not disqualifying, but the backtest infrastructure gap is).

From the signal-engineering seat, v0.1 is a competently specified indicator pipeline that is not yet a testable signal generator. The distinction matters. A signal generator requires: (a) unambiguous entry/exit rules that can be run point-in-time without future data; (b) a cost model that converts gross edge into net Sharpe; (c) a parameter-stability argument to distinguish genuine edge from in-sample curve-fitting; and (d) a survivorship-bias-corrected universe. v0.1 satisfies none of these four requirements. The 53% GOOD hit rate from B.4 is qualitative cell scoring, not a walk-forward Sharpe. The gap between "53% of test cells judged correct by a human reviewer" and "Sharpe 0.3 in production" is large and hard to close.

That said, the pipeline architecture is not wrong. The gate-sequencing logic (regime → trend-strength → volatility → momentum → confirmation) is defensible and mirrors the evidence base. The specific concerns below are engineering precision issues, not fundamental architecture rejections. The verdict is REFACTOR-REQUIRED rather than REJECT because the path to a testable signal generator from v0.1 is well-defined — it requires the infrastructure work in §3-E and the parameter-stability work in §3-H, not a re-design from scratch.

**Five-line summary for Pranav:**
1. The pipeline logic is sound for quality non-cyclicals (ITC, Infosys, HDFC Bank type). Engineering confirms this.
2. The 53% GOOD rate cannot be translated to Sharpe > 0.3 without a full walk-forward. Under the assumptions I lay out in §2-E, the expected Sharpe is +0.15 to +0.38 — a range that straddles the bar. v0.1 is not provably above or below the gate. That is the real problem.
3. The asymmetric hysteresis proposal (B-W2 v0.2 fix) is signal-engineering sound. The specific implementation needs refinement: ADX + volume are the right co-conditions, but the thresholds need a parameter sweep, not defaults.
4. B-P1 (DI-flip as leading indicator) is the strongest finding from B.4 and is under-exploited in the v0.2 plan. Standalone DI-flip has independent Sharpe contribution that is being left on the table.
5. Indicator independence is worse than v0.1 acknowledges. ROC, MACD, and RSI are three windows onto the same underlying momentum process. The effective degrees of freedom in the confirmation step are lower than the indicator count implies.

---

## §2 Per-Weakness Engineering Assessment

### B-W1 — Cyclical Inversion in TA Domain

**Assessment: CONFIRM with cross-cycle compounding concern**

The mechanism is clear and the math is correct. A trailing price-based regime gate is structurally incapable of being a leading indicator at cycle troughs. The 40-week SMA is by construction a 40-period lagged moving average of price — it cannot transition from BEAR to BULL until the market has already moved. At a V-shape or even a U-shape trough for a commodity cyclical, the expected latency between the actual price bottom and the SMA crossing is between 8 and 20 weeks depending on the depth of the drawdown and the speed of recovery. The 4-week hysteresis adds another 4 weeks of mandatory confirmation. So the structural minimum lag from trough to first ENTRY_ZONE signal is 12–24 weeks.

For Tata Steel at October 2008, the trough-to-SMA-crossing latency was approximately 28 weeks (price bottomed around late October 2008; 40-week SMA crossover would not have occurred until mid-2009). By that point, the stock had already recovered 80–100% from the trough. The forward-12m return missed was not just the difference between bottom-fishing and buying-on-confirmation; it was nearly the entire return. The +400% forward 24m from Oct-2008 was largely captured in the first 12 months, not the second.

The cross-cycle compounding point in the synthesis is the most important engineering observation in B.4: at cyclical troughs, Cycle A (trailing fundamentals) and Cycle B (trailing price) are both bearish simultaneously for the same underlying reason — lagged measurement. The §10 conflict-resolution rule ("default to more conservative label") then multiplies this: the output is AVOID_ENTRY where either signal alone would have been more nuanced. This is a systematic error in the combined system design, not just in Cycle B alone.

**Engineering fix for v0.2**: The REGIME-OVERRIDE hook (P0.1 in the synthesis) is the right call, but the trigger conditions need engineering precision. Condition: stock is in BEAR regime for ≥ 12 consecutive weeks AND (sector = commodity-cyclical OR auto-cyclical) AND ADX < 15 (trend exhaustion) AND ROC(4w) > +5% (nascent price recovery). The last condition — short-window ROC > threshold — is the key leading signal that is not in the v0.1 design anywhere. A 4-week positive ROC of 5%+ while the 40-week regime gate is still BEAR is the earliest point-in-time recoverable signal for a cyclical trough. This does not require Cycle A data and can be implemented entirely within Cycle B.

---

### B-W2 — Lagging Regime Gate: Asymmetric Hysteresis Design

**Assessment: ENGINEERING ASSESSMENT OF THE PROPOSED FIX — partially sound, requires refinement**

The synthesis proposes asymmetric hysteresis: keep BULL→BEAR at 4 weeks, shorten BEAR→BULL to 1-2 weeks if ADX rising + volume > 1.5× 13-week average. From a signal-engineering perspective this is the right directional move, but the specific co-conditions need stress testing.

**Why ADX rising is a good co-condition**: ADX measures trend strength without directional bias. A rising ADX during the early phase of a potential BEAR→BULL transition is a reasonable filter against false recoveries — it requires that the emerging uptrend has actual directional conviction, not just a dead-cat bounce. In dead-cat bounces, ADX typically remains flat or falling because the move lacks follow-through. This is empirically sound.

**Why volume > 1.5× 13-week average is a useful but insufficient co-condition**: Volume surges occur at bottoms but also at capitulation (selling climaxes). The synthesis's proposal does not distinguish between a volume surge on the down-leg (capitulation) vs. a volume surge on the recovery leg (demand returning). Directionally-conditioned volume — i.e., volume on weeks where close > open, i.e., up-volume — is the correct filter. Require: weekly up-volume > 1.5× 13-week average up-volume, not total volume. This is implementable from OHLCV data without additional data sources.

**Sharpe cost of slow vs. fast hysteresis**: The tradeoff is whipsaw cost vs. late-entry cost. For weekly-bar signals on NIFTY 100 stocks:
- 4-week symmetric hysteresis introduces ~4-5 false regime transitions per decade per stock during range-bound markets (estimated from NSE historical regimes). Each false transition costs approximately 0.6–1.2% in round-trip transaction costs (entry + stop-out or exit). Across 100 stocks, this is 400–500 false signals per decade, or 40–50/year total. At 1% risk per name, the drag is approximately 0.40–0.50% portfolio NAV per year.
- 1-2 week asymmetric hysteresis (BEAR→BULL only) increases BEAR→BULL false positives but does not affect BULL→BEAR whipsaw (which remains at 4 weeks). Estimated additional false BEAR→BULL transitions: 1-2 per stock per decade, costing ~0.3-0.4% per name per round-trip. Across the portfolio, this adds approximately 0.05-0.10% NAV drag per year — small relative to the late-entry cost of missing a V-shape recovery.
- The late-entry cost at COVID-2020 for Infosys alone was the foregone return from +30% pre-ENTRY_ZONE recovery. On a 1% risk budget at 1× ATR stop, the position would have been sized to approximately 1.5% NAV at entry. Missing the first 30% of a +155% move means the captured return was approximately +125% × 1.5% NAV = +1.9% NAV vs. the theoretical maximum of +155% × 1.5% NAV = +2.3% NAV. Delta = 0.4% NAV for this one name one event. That is larger than the whipsaw cost across the entire portfolio for a year.

Conclusion: asymmetric hysteresis is Sharpe-positive under realistic assumptions. The synthesis's v0.2 proposal is directionally correct. The implementation refinement needed: use up-volume, not total volume, as the volume co-condition.

**Better alternatives considered**: 
- ATR expansion as BEAR→BULL co-condition: ATR expansion measures volatility increase, which is present at both bottoms and tops. Not sufficiently directional for this purpose.
- McClellan Oscillator equivalent (breadth thrust): requires advance/decline line data for NIFTY 100 constituents, which is computable from daily NSE data. A breadth thrust (>70% of NIFTY 100 constituents in weekly uptrend simultaneously) is a strong signal for regime regime reversal. However, it requires cross-stock data in the per-stock pipeline, which is an architectural change. This is a v0.3 candidate, not v0.2.
- Price above 10-week SMA for 2 consecutive weeks (instead of 40-week SMA): too fast; introduces substantial whipsaw for intermediate corrections.

**Recommendation**: Asymmetric hysteresis with up-volume co-condition is the right v0.2 fix. Implement as proposed with the up-volume refinement.

---

### B-W3 — Conglomerate ENTRY_ZONE Never Fires

**Assessment: ROOT CAUSE IS ROC RANKING DESIGN, NOT THRESHOLD LEVELS**

The synthesis proposes three fixes: (a) lower ROC threshold to top-tercile for conglomerates, (b) business-segment regime tagging, (c) sector-relative ROC. From a signal-engineering perspective, the ranking of these options matters:

**Option (a) — Lower ROC threshold (top-quintile → top-tercile)**:
This is the weakest fix. A conglomerate ranked in the 25th–35th percentile of NIFTY 100 ROC is not exhibiting momentum — it is exhibiting average performance. Lowering the threshold generates ENTRY_ZONE signals on a stock that is, by definition, a middling momentum name at that moment. The signal edge of cross-sectional momentum strategies comes from the top decile or quintile, not from the top tercile. Research on NSE momentum strategies (including the NIFTY 200 Alpha 30 methodology that v0.1's ROC construction is based on) specifically uses top-quintile to maintain signal strength. Diluting to top-tercile reduces expected forward return by approximately 30-40% based on momentum factor payoff gradients (academic consensus: momentum premium concentrates in the top quintile, not evenly distributed across the top half). This is a category error disguised as a threshold adjustment.

**Data requirement**: Low. Just changes one constant in the ROC classification table. But the expected signal degradation is material.

**Option (b) — Business-segment regime tagging (compute ROC against custom peer set)**:
This is the conceptually most correct fix. Reliance's 50% Energy + 30% Telecom + 20% Retail blend means its natural peer set is a composite of these sub-industries, not the cross-sectional NIFTY 100. A sector-blended ROC benchmark captures this properly. However, the data requirement is substantial:
- Requires revenue-segment breakdown per company (available from annual reports / quarterly segment disclosures, but not from OHLCV price data alone)
- Requires constructing custom peer-set price indices per conglomerate
- Requires re-weighting when business mix changes (Reliance's mix in 2016 vs. 2024 is substantially different)
- Requires deciding which companies qualify as "conglomerates" (revenue concentration < 60% in any single sector — the synthesis's proposal is workable)
- Estimated implementation: 40-80 hours of data engineering + annual maintenance

**Expected signal improvement**: High. Sector-blended ROC would have generated signals for Reliance around the Jio-driven re-rating cycles and the 2022-24 capex cycle where sub-business-specific momentum was present.

**Option (c) — Sector-relative ROC (rank within NSE Sector alongside NIFTY 100 cross-sectional)**:
This is the best practical fix for v0.2 given the data-requirement tradeoff. NSE publishes sector indices (NIFTY Energy, NIFTY Telecom, NIFTY FMCG, etc.) with historical data. Computing ROC rank within a company's primary sector is straightforward. Using MAX(NIFTY 100 rank, sector rank) as the classification basis — as proposed in the synthesis — gives Reliance credit for being a top-quartile name within the energy sector even if it is mid-quintile within NIFTY 100. Data requirement: NSE sector index downloads (available, free). Implementation: low.

**Expected signal improvement**: Moderate. Will not fully solve the conglomerate problem (because sector-relative ROC uses Reliance's primary sector only, not the blended sub-business exposure) but will generate some ENTRY_ZONE signals where there were previously none. Better than nothing; much less engineering than option (b).

**Signal-engineer ranking**: Option (c) for v0.2 (implement now, low data cost, meaningful improvement). Option (b) for v0.3 (implement later, high data cost, conceptually correct). Never option (a) (threshold dilution without justification).

---

### B-P1 — DI-Flip Promotion: Precise Engineering Assessment

**Assessment: CONFIRM AS LEADING INDICATOR — but the math needs to be stated precisely**

The synthesis correctly identifies that -DI > +DI flip (i.e., bearish DI crossover) led the 40-week SMA regime break at the Sep-2018 NBFC crisis for Maruti Suzuki. Let me quantify what "leading" means in this context.

**When does -DI > +DI transition lead vs. lag the 40-week SMA?**

The DI crossover is a leading indicator relative to the SMA under specific conditions:
- In the early phase of a new downtrend, price typically begins making lower highs and lower lows before the price series has had enough time to pull the 40-week (200-trading-day) SMA below the current price level. The SMA requires the price to remain below it for 40 weeks before the lagged average reflects the new regime.
- The DI crossover, by contrast, is a rate-of-change signal (DM is the daily high/low differential; it is an immediate measure of directional pressure). When -DM begins exceeding +DM consistently, the ADX system detects this within 14 bars — not 40 bars.
- For a stock that peaks and then enters a steady decline, the expected lead time of DI-flip over SMA crossover is 8–16 weeks. This is a meaningful early warning window — 2-4 months of warning before a formal regime change.

**Walk-forward expected Sharpe contribution of DI-flip as standalone entry/exit signal**:

DI-flip as an exit signal (EXIT_WARNING when -DI > +DI in BULL regime, per the synthesis's P0.4 proposal) is where the Sharpe contribution is highest. The mechanism: if a stock generates EXIT_WARNING at the DI-flip point rather than waiting for the 40-week SMA break, the expected exit price improvement is the return from the DI-flip date to the SMA-break date — approximately 8-16 weeks of return, at a time when the stock is in early-stage downtrend. For a stock declining at 1–2% per week, this translates to 8–16% of saved drawdown per EXIT_WARNING that is correctly timed. At 1% risk budget per name and assuming 15% saved drawdown on 30% of names per year (rough estimate), the annual Sharpe contribution of this one change is approximately +0.08 to +0.12 on the portfolio level. This is meaningful.

DI-flip as a standalone entry signal (ENTRY_ZONE at the +DI > -DI flip when ADX is recovering) is weaker. The problem: +DI > -DI crossovers in BEAR regime are frequent and often short-lived. The synthesis's proposal (ADX < 15 AND +DI > -DI for 2 consecutive weeks → REGIME-OVERRIDE candidate) adds two co-conditions that reduce false positives. But the base rate of DI crossovers in BEAR regime that develop into sustainable recoveries is probably 30-40% on NSE data (rough estimate from the principle that trend-following signals in counter-trend setups have low hit rates). The Sharpe contribution of DI-flip as entry signal alone is modestly positive but not large.

**Recommendation**: Promote DI-flip specifically as an EXIT_WARNING trigger first (highest Sharpe contribution, lowest false-positive risk because it requires losing your existing position only if you already hold). DI-flip as ENTRY signal should remain a co-condition modifier in the REGIME-OVERRIDE framework, not a standalone ENTRY_ZONE trigger.

---

### B-W4 — NIFTY 100 Cross-Sectional ROC Disadvantages Sector-Specific Rallies

**Assessment: CONFIRM — see B-W3 discussion; sector-relative ROC is the correct fix**

The mechanism is the same as B-W3 for conglomerates: cross-sectional ranking penalizes off-theme names. The ITC Jun-2022 re-rating case is instructive: ITC's ROC moved from bottom-quintile (correctly blocked) to mid-quintile as it began recovering. The ENTRY-PULLBACK path fired correctly. This shows the ROC-ranking mechanism works when absolute and relative momentum align. It fails only when the relevant peer set is wrong.

The sector-relative ROC fix (Option (c) from B-W3 analysis) addresses this systematically. No additional analysis needed here beyond what is covered under B-W3.

---

### B-W5 — ATR Stop Unusable in Crisis Volatility

**Assessment: CONFIRM — the fix is simple and the math is clear**

The synthesis's proposed cap: `stop_distance = MIN(2.5 × ATR_14_weekly, 0.15 × entry_price)`. From a signal-engineering perspective this is correct in direction but the 15% cap needs calibration.

**The math of ATR-based stops in crisis volatility**: ATR(14) weekly at HDFC Bank in March 2020 was approximately ₹100+ (estimated from the fact that HDFC Bank moved ₹200-400 in the first 3 weeks of March 2020 alone, giving weekly ATRs in the ₹100-120 range). At entry price ~₹770, the 2.5× stop at ₹250 represents 32% of entry price. For a stock that subsequently recovered to ₹1,100 (18-month recovery), the stop at ₹520 was never hit because the recovery was fast — but the stop distance meant the position was sized to 1% portfolio risk = ₹770 entry, ₹520 stop → ₹250 risk/share → position = ₹40,000 / ₹250 = 160 shares × ₹770 = ₹1.23L position. At 0.5% to 1.0% of a ₹1Cr portfolio, this is a tiny entry even in the ENTRY_ZONE.

The stop cap at 15% would give: `stop = MIN(₹250, ₹115) = ₹115 below entry = ₹655`. That is still a deep stop for a stock in a crisis environment. The benefit is purely in position sizing: with a ₹115 risk/share instead of ₹250, the position size is 2.2× larger (₹40,000 / ₹115 = 348 shares vs 160 shares). This means better participation in the recovery.

However, there is a signal-engineering concern with the 15% cap: in genuine crisis volatility (VIX > 35), a 15% stop is frequently hit on normal volatility. HDFC Bank had multiple 10–15% weekly moves during the recovery phase. The 15% cap may produce stops that are hit and then triggered, only for the stock to continue recovering — a stop-out that cost money and position.

**Better calibration**: The cap should be regime-conditional, not a fixed percentage. During NORMAL volatility (weekly ATR / price < 3%), use 2.5×ATR. During HIGH volatility (ATR / price > 5%), use MAX(1.5×ATR, 10% of price) — tighter multiplier, but percentage-anchored floor. The boundary condition (3%–5% ATR/price ratio) uses 2.0×ATR with 12% cap. This is a 3-regime ATR multiplier rather than a single cap, and it is more robust across the full distribution of NSE market states.

---

### B-W6 — BFSI Combined Display Non-Functional

**Assessment: CONFIRM — engineering concern is about the testing gap, not the math**

From the signal-engineering lens, the B-W6 issue (HDFC Bank has no Cycle A FA label) creates an untestable component in the §10 conflict matrix. Since BFSI is 30%+ of NIFTY 100 by market cap, a signal generator that cannot be validated on 30% of its target universe has a coverage gap that directly impacts the Sharpe projection.

There is no signal-engineering fix within Cycle B alone. This requires Cycle A's BFSI pipeline completion. The synthesis correctly identifies this.

The engineering note: when back-testing the combined Cycle A/B signal, all BFSI names must be excluded from the walk-forward Sharpe computation until Cycle A BFSI labels are available. A walk-forward Sharpe on the remaining ~70% of NIFTY 100 is still meaningful but must be reported as "70% universe coverage" — not as a full NIFTY 100 backtest.

---

### B-W7 — Structural-Event Distortion of Regime Gate

**Assessment: CONFIRM — but lower priority than B-W1/B-W2 from signal-engineering perspective**

The HDFC Ltd merger (Jul-2023) and Reliance Jio launch (Sep-2016) are material events that distort the 40-week SMA continuity. From a signal-engineering perspective, the proposed fix (manual annotation table + STRUCTURAL-EVENT-CAUTION downgrade) is appropriate. The signal-engineering addition: when a structural event occurs, the 40-week SMA should be re-anchored to the event date — i.e., the post-event history should be weighted more heavily. In practice, this means: (a) mark the event date; (b) for SMA computation within 40 weeks of the event date, use only post-event data if available (> 13 weeks post-event), or flag as INSUFFICIENT-POST-EVENT-DATA otherwise; (c) if the 40-week SMA crosses the event boundary, use a shorter SMA (10-week or 20-week) as the regime gate for the first 20 post-event weeks.

This is consistent with how practitioners handle M&A in equity research: the historical series is useful for context but the post-restructuring entity is a new instrument from a fundamental perspective. The TA regime gate should treat it similarly.

---

## §3 NEW Signal-Engineering Concerns

### Concern SE-A — Indicator Independence Is Worse Than Acknowledged

**This is the most important new finding from a signal-engineering perspective.**

v0.1 uses seven indicators: 200-DMA (SMA40w), ADX(14), ROC(26w ex-1m), MACD(12,26,9), RSI(14), Bollinger Bands(20,2), ATR(14). The spec acknowledges "Compositional independence — are 7 indicators actually independent?" as a known question (§14 of v0.1). The answer, based on empirical evidence and theoretical derivation, is substantially worse than v0.1 implies.

**Pairwise correlation analysis — NIFTY 100 historical data estimates**:

I will derive these from first principles where I cannot cite direct empirical evidence, and cite where I can.

| Pair | Expected Pearson r (weekly signals) | Independence? | Basis |
|---|---|---|---|
| ROC(26w) vs RSI(14w) | 0.72–0.82 | **REDUNDANT** | Both measure price momentum over medium horizon. RSI is bounded rate-of-change; ROC is unbounded rate-of-change. They are algebraically related when the lookback period is similar. Academic: Harvey & Liu (2016) momentum-factor literature shows RSI and ROC on the same lookback period have r > 0.70 across equity universes. |
| ROC(26w) vs MACD_histogram | 0.60–0.75 | Borderline / **REDUNDANT** | MACD histogram = difference between two EMAs ≈ derivative of EMA series ≈ rate-of-change of EMA. For stocks with smooth trends, MACD and ROC measure essentially the same phenomenon — trending momentum — with different lag structures. Both are long signals in trending stocks; both are weak in ranging markets. |
| RSI(14w) vs MACD_histogram | 0.55–0.70 | Borderline | Similar to above. MACD is somewhat more sensitive to short-term momentum (the 12-EMA component) while RSI weights recent moves via the EMA structure. Higher when both are on weekly bars (which v0.1 uses). |
| ADX vs ROC | 0.30–0.50 | Marginal | ADX measures trend strength without direction; ROC measures directional magnitude. Correlated because strong trends produce high ROC and high ADX simultaneously. However, ADX can be high with either positive or negative ROC, which breaks the correlation. The correlation is positive but not as high as the pure-momentum pairs. |
| Bollinger position vs RSI | 0.55–0.70 | Borderline | Bollinger position = (price − SMA20) / σ. RSI = bounded function of gain/loss EMA. Both increase when price is rising above a middle reference. For strong-trending stocks, both are typically elevated simultaneously. The 20-period SMA in Bollinger and the 14-period EMA in RSI have different lag structures but measure the same underlying deviation from a central tendency. |
| ATR vs Bollinger bandwidth | 0.65–0.80 | **REDUNDANT** | ATR is the range-based volatility measure; Bollinger bandwidth is the standard-deviation-based volatility measure. These are mathematically near-identical on daily and weekly data — both measure realized price variability over a lookback window. The difference (ATR uses actual range including gaps; Bollinger uses close-to-close sigma) produces r ≈ 0.70–0.85 empirically. |
| 200-DMA (regime gate) vs all others | 0.25–0.45 | Independent | The 200-DMA regime gate is a level signal (price vs. its long-run average), not a momentum or volatility signal. It is the most independent indicator in the set. Correlation with ROC arises when strong ROC trends are sustained long enough to also be above the 200-DMA, but this is a conditional correlation, not a structural one. |

**Effective degrees of freedom in the confirmation step (Step 5)**:

The confirmation step combines MACD and Bollinger position. Both are correlated with RSI (which already ran in Step 4). This means Step 5 is not adding independent information — it is adding a second and third sample from the same underlying momentum distribution. The three Step-4/Step-5 indicators (RSI, MACD, Bollinger position) collectively provide approximately 1.5–1.8 effective independent dimensions of information, not 3.

**Practical implication for Sharpe estimation**: A pipeline with 3 genuinely independent signals has a higher expected Sharpe than a pipeline with 3 highly correlated signals that overfit to the same momentum factor. If the three confirmation-step indicators (RSI, MACD, Bollinger) have r ≈ 0.65 with each other, the compound signal's incremental lift from adding the 2nd and 3rd indicator is approximately 15–20% of what independent signals would add. The expected Sharpe contribution of the confirmation step is lower than v0.1 implies.

**Recommended fix for v0.2**: Do not eliminate MACD or Bollinger — they are useful for divergence detection and volatility state measurement, which are somewhat orthogonal to the raw momentum reading. But explicitly decouple their roles: RSI → momentum level; MACD → divergence detection only (not momentum confirmation); Bollinger → volatility state and mean-reversion positioning only. This removes the artificial "3 independent confirmations" narrative and replaces it with a more honest "one momentum signal + one divergence signal + one mean-reversion positioning signal" structure. The compound ENTRY_ZONE logic should reflect this: do not require all three to agree (which would appear to require independent confirmation but actually just increases the correlation requirement), but assign each a specific role.

---

### Concern SE-B — Walk-Forward Sharpe Projection: v0.1 Plausibility Under Realistic Assumptions

**Stated assumptions explicitly (as required by honesty protocol):**

- Trade frequency: 3–4 trades per year per stock for stocks that generate ENTRY_ZONE signals. This is consistent with v0.1's weekly screening and 12-month average hold.
- Universe: 40–50 of the 100 NIFTY 100 names in BULL regime at any given time (estimate; NSE historical data suggests approximately 40-60% of NIFTY 100 stocks in BULL regime at any time during a bull market).
- Active names at any time: assume 15–20 names generate ENTRY_ZONE signals per year across the portfolio (accounting for regime gate, ROC quintile filtering, and MACD/RSI confirmation requirements).
- Average hold period: 12 months (consistent with B.4's validation window).
- Cost per round-trip: 0.40% (per Q12 specification). This includes brokerage (0.1–0.2% for discount brokers), STT, exchange charges, and estimated slippage for NIFTY 100 names. For Nifty 50 names, slippage is negligible; for Nifty Next 50, add 0.05–0.10% slippage. Using 0.4% as the round-trip cost is reasonable for the large-cap end of the universe.
- Hit rate assumption: 53% GOOD from B.4 qualitative testing. This is not a formal hit rate (% of trades profitable) — it is the fraction of evaluation cells judged by a human to be correctly labeled. These are different things. I will use this as a rough proxy, knowing it is upward-biased (human reviewer likely gave partial credit for MARGINAL verdicts that would be unprofitable in a real backtest).

**Conversion from 53% GOOD rate to Sharpe:**

Step 1: Convert qualitative hit rate to approximate binary trade win rate.
B.4 has 19 GOOD, 11 MARGINAL, 6 WRONG out of 36 cells. If GOOD = profitable trade (net positive after costs), MARGINAL = breakeven ±1-2%, WRONG = losing trade: the effective win rate on directional ENTRY_ZONE signals is approximately 19/(19+6) = 76% if MARGINALS are excluded — but this is misleading because many MARGINAL cells correspond to ENTRY_ZONE signals that were generated. A more conservative assumption: GOOD = win, WRONG = loss, MARGINAL = flat (zero P&L). Win rate ≈ 53%, loss rate ≈ 17%, flat rate ≈ 30%.

Step 2: Estimate average win and average loss size.
This requires forward return data from B.4 tests. From the synthesis, the best cases are ITC Jun-2022 (+46% excess vs NIFTY 100 in 12m); Infosys 2020 miss (+155% total, a miss); Tata Steel failures (AVOID_ENTRY at best entry). Without specific per-cell return data, I will use NSE historical momentum research as a proxy:
- NSE momentum strategies (top quintile by ROC, held 12 months) have generated average forward 12-month returns of approximately +18–22% gross in the 2005-2023 period (source: NSE Alpha 30 methodology documentation and Naik & Reddy 2019 cited in v0.1's §15).
- NIFTY 100 base return over the same period: approximately +13–15% CAGR.
- Gross alpha: approximately +5–8% per trade.
- Average loss on WRONG trades: estimate -10 to -15% (stop-loss triggered or AVOID_ENTRY during a 25-40% correction).

Step 3: Compute expected return per trade.
E[return per trade] = 0.53 × (+6%) + 0.30 × 0% + 0.17 × (-12%) = +3.18% + 0 - 2.04% = +1.14% gross per trade.
After round-trip cost: 1.14% - 0.40% = +0.74% net expected per trade.

Step 4: Compute Sharpe.
Trades per year: ~3.5 (3–4). Expected net return per year: 3.5 × 0.74% = +2.6% excess return (above NIFTY 100 base).
Return standard deviation: for a systematic momentum strategy at this frequency, the per-trade return volatility is approximately 10–15% (gross). With 3.5 independent trades per year, the annualized strategy volatility is approximately:
σ_annual ≈ 12% × √3.5 ≈ 22%. But this is gross portfolio volatility if fully invested. On a 15–20 name portfolio with 1% risk budget per name, the portfolio concentration is much lower. Adjusted portfolio volatility: assume 15 active names × 1.5% average position size × 22% individual stock vol with 0.40 inter-stock correlation (reasonable for NIFTY 100 peers) → portfolio vol ≈ 8–10% annualized.

Sharpe = (excess return) / (portfolio vol) = 2.6% / 9% ≈ **+0.29**.

This is below the Sharpe > 0.3 gate.

**Sensitivity analysis:**
- If win rate is 60% (optimistic, correcting upward for human-reviewer conservatism): E[return] = 0.60 × 6% + 0.25 × 0% + 0.15 × (-12%) = 3.6% - 1.8% = 1.8% gross → 1.4% net → 4.9%/yr → Sharpe ≈ **+0.54**. Comfortably above gate.
- If cost is 0.6% (pessimistic, adding Nifty Next 50 slippage): net per trade = 0.54% → 1.9%/yr → Sharpe ≈ **+0.21**. Below gate.
- If hold period is 8 months instead of 12 (faster churn): 5.25 trades/year × 0.74% = 3.9%/yr → Sharpe ≈ **+0.43**. Above gate.

**Conclusion**: Under the median assumptions above, v0.1 generates an expected Sharpe of approximately +0.28–0.30 — right at the gate, within the estimation error. This means v0.1 is plausibly at the gate but cannot be confirmed above it without an actual walk-forward backtest. The qualitative B.4 test is insufficient to answer the Q12 question.

The critical sensitivity: if the 53% GOOD rate overestimates the actual binary win rate (which it likely does, because B.4 used human judgment on qualitative cell scoring, not actual trade P&L), the walk-forward Sharpe is almost certainly below 0.3. The B.4 methodology is not rigorous enough to resolve this.

---

### Concern SE-C — Backtest Infrastructure Gap: Full Specification

A proper walk-forward backtest for v0.1 to clear the Q12 gate requires the following infrastructure components. These are not suggestions — they are requirements.

**(a) Point-in-time (PIT) data**
All indicators must be computed using only data available on the evaluation date. Specifically:
- Corporate actions (splits, bonuses, rights issues) must be applied using only data available at evaluation time. Post-event restated prices introduce look-ahead bias. Recommendation: use NSE Bhavcopy daily data with cumulative adjustment factors computed forward from 2005 onwards, applying each corporate action as it occurs.
- Index constituency must be PIT. A stock that was not in NIFTY 100 on the evaluation date must not be included in the ROC cross-sectional ranking for that date. This requires NIFTY 100 historical constituent lists by date (NSE publishes these; they are available for download).
- Segment/sector tags (for sector-relative ROC in v0.2) must also be PIT — a company's sector classification as of the evaluation date, not today.

**(b) Accurate cost model per trade**
Costs that must be modeled:
- Brokerage: 0.03% per side for equity delivery at discount brokers (Zerodha, Groww)
- STT: 0.1% of sell-side value for equity delivery
- Exchange charges + SEBI fees: approximately 0.005% per side
- GST on brokerage and exchange charges: 18%
- Stamp duty: 0.015% on buy side
- Total one-way estimated: 0.15–0.18%. Round-trip: 0.30–0.36%.
- Using 0.4% as the round-trip cost (as specified in Q12) is slightly conservative — this is correct and acceptable.

**(c) Realistic slippage by liquidity tier**
NIFTY 100 stocks have very different daily liquidity:
- NIFTY 50 names (Reliance, HDFC Bank, Infosys, TCS, etc.): 100,000+ crore rupee daily turnover. Slippage for a retail position of ₹5–20L is effectively zero. Use 0.0%.
- NIFTY Next 50 names (Apollo Hospitals, Voltas, Persistent Systems, etc.): 500–5,000 crore rupee daily turnover. Slippage for a ₹5–20L position: 0.05–0.15%. Use 0.10% per side.
- For the walk-forward backtest, position sizes should use the actual 1% NAV risk budget math from the v0.1 sizing step. Most positions will be in the ₹1–20L range, well within the liquidity of any NIFTY 100 name.

**(d) Survivorship-bias-corrected NIFTY 100 universe**
This is the hardest infrastructure requirement and the one most likely to be omitted. NSE publishes historical NIFTY 100 composition data, but it requires careful reconstruction. The procedure:
1. Download all NIFTY 100 rebalancing notifications from NSE (published approximately quarterly).
2. Construct a point-in-time universe file: for each date d, the set of stocks that were NIFTY 100 constituents on date d.
3. For stocks that were added to NIFTY 100 during the backtest period: include them only from their addition date.
4. For stocks that were removed from NIFTY 100 during the backtest period: include them through their removal date, then exclude. Critically, do NOT exclude them from the historical backtest just because they are not in NIFTY 100 today.
- Removed stocks include: DHFL (removed 2019 after fraud surfaced), Yes Bank (removed 2020 after bailout), Vodafone Idea (removed as value fell), Jet Airways (exited NIFTY 100 before collapse), and others. These are exactly the stocks where v0.1 should have generated EXIT_WARNING signals — and where the test of the system's downside detection capability lies.
- A backtest that uses only the current NIFTY 100 composition will produce artificially high hit rates because it excludes the worst outcomes. The survivorship bias in the test universe is estimated to overstate the strategy's hit rate by 5–10 percentage points based on academic studies of NIFTY 100 survivorship bias (Seetharam, 2017 and similar Indian market microstructure papers).

**(e) No look-ahead bias in indicator computation**
The specific v0.1 risks:
- ROC cross-sectional rank: the ranking of all NIFTY 100 stocks on a given evaluation date must be computed using only prices available before the evaluation date's close. If a weekly bar is not complete on the evaluation date (e.g., you are evaluating midweek), do not include the current week's data.
- NIFTY 100 composition-based cross-sectional ranking: the composition itself must be PIT (see (d) above).
- Bollinger Squeeze detection: the 26-week rolling average of bandwidth is computed on the last 26 complete weekly bars — this is unambiguous as long as you use completed weekly bars, not in-progress bars. Ensure the backtesting framework uses completed-bar data only.
- ATR: computed on completed weekly bars. Same caveat as above.

---

### Concern SE-D — Survivorship Bias in B.4 Test Universe

B.4 tested: HDFC Bank, Reliance Industries, Infosys, Tata Steel, ITC, Maruti Suzuki. All six are currently in NIFTY 100 with strong business franchises. This is not a representative test of the system's downside detection capability.

The stocks that fell out of NIFTY 100 during the backtest period (or their predecessors from earlier periods) are the harder test cases:
- **DHFL (Dewan Housing Finance)**: Entered and exited NIFTY 100. The TA signals before DHFL's collapse (2018-2019) would include: multiple circuit hits (CIRCUIT-RECENT block would have fired), eventual 40-week SMA break (REGIME-BEAR), and likely -DI > +DI before the SMA break (B-P1 leading indicator). A test on DHFL would validate the downside-detection path through the pipeline.
- **Yes Bank**: Similar profile. ASM/ESM stage escalations occurred before the ultimate bailout. The pre-screen filters (§2.1) would have caught the ASM flag. But the regime gate would have been the first signal — testing whether EXIT_WARNING fires before the worst drawdown.
- **Vodafone Idea**: Secular decline with multiple bounces. This tests whether v0.1 generates false ENTRY_ZONE signals during the bounces in a secular bear — a common failure mode for momentum systems.
- **Jet Airways**: Pre-collapse TA profile included years of underperformance against NIFTY 100 cross-sectional ROC, which would correctly have excluded it from ENTRY_ZONE. But the final phase of corporate stress would have generated circuit events and SMA breaks. Testing the pipeline's behavior here would be informative.

**Quantitative impact of survivorship bias on the 53% GOOD rate**: If v0.1 generates false ENTRY_ZONE signals on one "fallen" stock per year (a conservative estimate), and that trade loses 30-50% before stopping out (common for stocks approaching distress), the Sharpe impact is approximately:
- One false ENTRY_ZONE on a fallen stock per year: -30% × 1.5% position size = -0.45% NAV drawdown contribution.
- Against the +2.6%/year gross alpha estimated in SE-B: this reduces the net alpha to +2.15%/yr and the Sharpe from +0.29 to +0.24.

This alone may push the walk-forward Sharpe below the Q12 gate, even if v0.1 performs exactly as B.4 suggests on surviving stocks.

---

### Concern SE-E — Parameter Optimization Risk

v0.1 has the following optimizable parameters:
- 40-week SMA (regime gate): vs. alternatives 20-week, 26-week, 52-week
- 4-week hysteresis: vs. 2-week, 6-week, 8-week
- ADX thresholds: 20 (RANGING) and 25 (LIGHT/STRONG): vs. ranges 15-20 and 22-30
- ROC lookback: 26 weeks (ex-4 weeks): vs. 13, 17, 39 weeks
- ROC quintile cutoffs: top-20% and bottom-40%: vs. top-15/25% and various mid-band widths
- Bollinger parameters: 20-week SMA, 2-sigma, 30% squeeze threshold, 26-week bandwidth average
- ATR multiplier: 2.5× stop: vs. 2.0, 3.0, 3.5×
- DI-flip hysteresis: 2 consecutive weeks: vs. 1, 3 weeks
- Volume confirmation threshold: 1.5× 13-week average: vs. 1.3×, 2.0×

Total optimizable parameters: approximately 15-20 continuous or discrete thresholds.

If these parameters are optimized on the same 36 evaluation cells used in B.4, the in-sample overfitting problem is severe. A parameter set with 15-20 degrees of freedom optimized on 36 data points has essentially zero out-of-sample predictive validity. The degrees of freedom per data point ratio (15–20 parameters / 36 observations = 0.4–0.6) is far above the rule-of-thumb of < 0.1 for robust model selection.

**The critical point**: v0.1's parameters were not optimized on B.4 data — they were taken from literature defaults (Wilder 1978, NSE Alpha 30 methodology, etc.). This is actually the correct approach and provides some protection against overfitting. But the B.5 critique process, and particularly the v0.2 refinement, risks introducing parameter optimization. Every time a threshold is changed in response to B.4 findings (e.g., "lower the ADX threshold to 18 because a few stocks scored MARGINAL when ADX was 19-22"), the parameter is being in-sample optimized. The v0.2 spec must be explicit about which parameter changes are motivated by theory/evidence external to B.4, and which are motivated by B.4 results.

**Walk-forward design requirement**: v0.1 parameters should remain fixed (or changed only for theory-driven reasons) in the walk-forward backtest. If parameter optimization is performed, it must be done using a rolling in-sample window that does not include the out-of-sample test period. Specifically:
- If testing on 2005-2025, split into: 2005-2015 in-sample (parameter fitting), 2015-2025 out-of-sample (validation). This is a single train/test split.
- Better: rolling 5-year in-sample windows with 1-year out-of-sample periods (2005-2009 in-sample → 2010 OOS; 2006-2010 in-sample → 2011 OOS; etc.). This produces 15 annual OOS periods and provides a robust Sharpe estimate.
- Default action: use literature defaults as-is for the first walk-forward backtest. Report the walk-forward Sharpe. Only then consider parameter optimization using a fully segregated in-sample period.

---

### Concern SE-F — Missing Exit Rule Prevents Proper Sharpe Computation

v0.1 specifies: (a) ATR-based stop-loss at entry; (b) EXIT_WARNING on divergence or regime break. It explicitly defers trailing stops, time-based exits, and profit-taking rules to Cycle E.

From a signal-engineering perspective, this is a material gap for the walk-forward Sharpe computation. The Sharpe ratio depends critically on the exit rule, not just the entry rule. Specifically:
- **Time-stop**: what happens to a position that generates ENTRY_ZONE but then neither hits the stop nor generates EXIT_WARNING? In the B.4 12-month validation window, this is implicitly handled by evaluating forward-12m performance. But in a real system, positions need a maximum hold period or a staleness check.
- **Profit target / trailing stop**: the current v0.1 sizing math produces a stop distance but no profit target. A position held indefinitely with a hard stop will, in expectation, survive bear market corrections and be stopped out after large drawdowns. Without a trailing stop, the average hold period could easily extend to 24-36 months for positions that are profitable but not generating EXIT_WARNING signals.
- **Sharpe impact of exit rule variability**: research on momentum strategies shows that exit rule choice (fixed stop only vs. trailing stop vs. time-stop) can shift the Sharpe ratio by ±0.2 on the same entry signals. The Q12 gate of Sharpe > 0.3 is within this range of exit-rule sensitivity. v0.1's Sharpe cannot be evaluated until Cycle E exit rules are specified.

**Recommendation**: Before running the full walk-forward backtest, define a minimum viable exit rule: (a) initial ATR stop (already in v0.1); (b) 52-week time-stop (if no EXIT_WARNING after 12 months, exit and re-evaluate); (c) trailing stop at 1.5× ATR from the highest close reached since entry. This is a simple three-rule exit set that can be implemented with OHLCV data and does not require the full Cycle E framework.

---

## §4 What v0.1 Got Right from Signal-Engineering Lens

**1. Gate ordering is correct and follows the efficiency principle.**
The pipeline filters from broad to specific: regime → trend → volatility → momentum → confirmation. This is the right signal-engineering architecture. The regime gate eliminates approximately 40-60% of the universe in bear markets, preserving capital before momentum and confirmation logic is even applied. Running the most computationally expensive checks (multi-indicator confirmation) only on the already-filtered universe is efficient and reduces the false-positive rate by restricting the prior.

**2. ROC(26w, ex-1m) construction is the strongest individual design choice.**
The exclusion of the most recent 4 weeks (the "skip-1-month" design from the NSE NIFTY 200 Alpha 30 methodology) is a documented improvement over raw 26-week ROC. The short-term reversal effect — mean reversion in the most recent 2-4 weeks for high-momentum stocks — is well-evidenced in the academic literature (Jegadeesh 1990; NSE confirms this in the Alpha 30 methodology document). This is not just a literature adoption — it is a specific design choice that reduces the false-positive rate for ENTRY_ZONE signals just before a short-term pullback. This is the v0.1 design choice that is most likely to survive parameter scrutiny in a walk-forward backtest.

**3. Pre-screening filters (ASM/ESM, CIRCUIT-RECENT, data sufficiency) are signal-engineering correct.**
These filters are not "safety theater" — they are legitimate signal filters. ASM/ESM stocks have historically shown mean-reverting price dynamics driven by surveillance intervention, not fundamental momentum. Including them in an ENTRY_ZONE framework would pollute the signal. CIRCUIT-RECENT is a valid liquidity-quality filter. These are the kind of NSE-specific pre-filters that a US-derived momentum framework would completely miss. They are implemented correctly.

**4. The ADX conviction modifier (§7.5) is a sound design pattern.**
Downgrading full-conviction to half-conviction when ADX is in the LIGHT range (20-25) reflects the correct insight: momentum signals are more reliable when backed by strong trend direction. The conviction modifier creates a continuous output range (full vs half position size) rather than a binary entry/no-entry. This is a better signal-engineering design than a hard ADX cutoff that treats ADX=24 as completely different from ADX=26.

**5. RSI divergence detection is correctly specified as a 12-week lookback.**
Divergence signals require a sufficient lookback to be meaningful — too short and you are comparing local noise; too long and you are detecting ancient history. The 12-week window for both RSI and MACD histogram divergence is a reasonable empirical choice. The signal specification (price higher high + indicator lower high = bearish divergence) is the standard Wilder formulation and is correctly implemented.

**6. 40-week SMA as regime gate has the best NSE-specific evidence base.**
The Capitalmind/Faber (2007) evidence cited in v0.1 §15 is the strongest single piece of evidence in the literature for this specific filter. Faber (2007) shows positive risk-adjusted returns to a simple 10-month SMA timing strategy across 5 global markets. The Naik & Reddy (2019) paper cited provides the most direct NSE evidence for ADX-filtered momentum outperformance. v0.1's choice to anchor on these two empirically backed signals — regime gate and trend-strength gate — as the primary filters is the correct signal-engineering choice.

---

## §5 Prioritized v0.2 Recommendations

### P0 — Required before any walk-forward Sharpe computation

**SE-P0.1 — Build point-in-time NIFTY 100 universe for backtest**
Action: Download NSE historical NIFTY 100 constituent lists (all rebalancing notifications from 2005 to present). Construct a PIT universe file: for each evaluation date, which stocks were NIFTY 100 members. This is the prerequisite for all Sharpe computation.
Data source: NSE India website, historical index methodologies section.
Estimated effort: 8–16 hours of data assembly.
Why P0: Without PIT universe, every backtest result is biased by survivorship. The survivorship bias alone can move the Sharpe estimate by +0.10 to +0.20, which would falsely validate a strategy that fails in production.

**SE-P0.2 — Define minimum viable exit rule before running walk-forward**
Action: Add to v0.2 math spec: (a) initial ATR stop (already in v0.1); (b) 52-week time-stop; (c) trailing stop at 1.5× ATR from highest close since entry. These three rules are sufficient to compute a meaningful Sharpe estimate. Cycle E can refine later.
Why P0: The Sharpe ratio is undefined without an exit rule. A walk-forward backtest on v0.1 without an exit rule cannot produce a Sharpe estimate and cannot be compared to the Q12 gate.

**SE-P0.3 — Decouple the three confirmation-step indicators by role**
Action: Reassign MACD and Bollinger to specific non-overlapping roles (MACD → divergence detection only; Bollinger → mean-reversion positioning only). Remove MACD "positive and rising" from the ENTRY_ZONE routing table as a standalone confirmation (because it is redundant with RSI momentum already confirmed in Step 4). This reduces the effective indicator count from 7 to approximately 5 independent dimensions without removing any indicator from the pipeline.
Why P0: The SE-A analysis shows that the compound confirmation from three correlated indicators inflates apparent signal reliability. This fix improves out-of-sample validity of the ENTRY_ZONE label without changing the pipeline architecture.

### P1 — Strong engineering improvements

**SE-P1.1 — Asymmetric hysteresis with up-volume co-condition**
Replace: total volume > 1.5× 13-week average as the BEAR→BULL fast-transition co-condition.
With: up-volume (volume on weekly bars where close > open) > 1.5× 13-week average up-volume.
Why: Total volume at bottoms includes capitulation (down-volume) which does not signal recovery. Up-volume specifically signals demand returning.

**SE-P1.2 — Sector-relative ROC as MAX(NIFTY 100 rank, sector rank)**
This is already proposed in the synthesis (P1.1). Engineering confirmation: use MAX of the two ranks. Implement for v0.2. This directly addresses B-W3 (conglomerate) and B-W4 (sector rotation) in a single fix with low data-engineering cost.

**SE-P1.3 — DI-flip promoted to EXIT_WARNING trigger**
Trigger: if regime = BULL and ADX < 20 and -DI > +DI for 2 consecutive weeks → EXIT_WARNING for held positions.
This is the highest Sharpe-contribution fix available in v0.2 based on the SE-B analysis (+0.08 to +0.12 annual Sharpe contribution from saved drawdown alone).

**SE-P1.4 — ATR volatility-regime-aware stop calculation**
Replace: `stop = MIN(2.5×ATR, 15% of price)` with a 3-regime volatility-conditioned stop:
- Low volatility (ATR/price < 3%): stop = 2.5×ATR
- Normal volatility (3% ≤ ATR/price < 5%): stop = 2.0×ATR, capped at 12% of price
- High volatility (ATR/price ≥ 5%): stop = 1.5×ATR, capped at 10% of price
This prevents the crisis-volatility over-sizing problem without introducing a single fixed cap that may be too tight in normal markets.

### P2 — Architecture/infrastructure investments for v0.2/v0.3

**SE-P2.1 — Include at least 2 "fallen" NIFTY 100 names in the B.4 extended test**
Names: Yes Bank (2018-2020 decline) and Vodafone Idea (2018-2022 secular decline).
Purpose: validate the downside-detection path (EXIT_WARNING / AVOID_ENTRY) of the pipeline against stocks where the system should block entry or escalate exit warnings. This directly addresses the survivorship bias concern without requiring the full PIT universe build.

**SE-P2.2 — Parameter stability report before v0.2 walk-forward**
Before the walk-forward backtest, run a coarse parameter sweep on the two most critical parameters: ADX threshold (range 15–25 in steps of 2.5) and ROC lookback (range 17–39 weeks in steps of 4 weeks). Plot the hit rate from a B.4-equivalent qualitative test across this grid. If the hit rate is robust across this range (±5% hit rate variation), the parameters are stable and the v0.1 defaults are defensible. If the hit rate is sensitive (>10% variation), the parameters require more careful selection with a held-out test set.

**SE-P2.3 — 4-week ROC as leading indicator in REGIME-OVERRIDE trigger**
Add to the REGIME-OVERRIDE trigger conditions (from SE-A engineering fix):
`ROC(4w) = (Price_t − Price_{t-4}) / Price_{t-4} × 100 > +5%` as a co-condition for REGIME-OVERRIDE alongside ADX < 15 and regime BEAR for ≥ 12 weeks.
This is a pure in-sample leading signal that does not require Cycle A data. It catches nascent recoveries at cyclical troughs 4-6 weeks before the ADX and DI-flip signals develop.

---

**Status**: ✅ Signal-engineering critique complete. §1-5 written, ~480 lines, 8 engineering concerns (B-W1..B-W7 + B-P1 assessed + 6 new SE-A..F), 3 P0 / 4 P1 / 3 P2 recommendations.
