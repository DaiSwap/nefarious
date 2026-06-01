# 24 — Cycle B: B.5 Critique Synthesis — v0.2 Refactor Brief

**Status**: ✅ Synthesis complete. v0.2 brief ready for B.6. Idea-review verdict: v0.5 update recommended (BFSI cross-cycle dependency).
**Date**: 2026-05-31
**Inputs**: `21_cycle_B_math_v0.1.md` (v0.1 spec), `23_cycle_B_test_synthesis_v0.1.md` (B.4 synthesis), `24a–24e` (5 critics)
**Output**: This document → drives B.6 (v0.2 math spec in `25_cycle_B_math_v0.2.md`)
**Format reference**: `15_cycle_A_critiques_v0.1.md` (A.5 synthesizer)

---

## §1 — Cross-critic verdict on v0.1 (top-line)

| Critic | Lens | Verdict | One-line rationale |
|---|---|---|---|
| C1 Quant | Statistician | **REFACTOR-REQUIRED** | Design-envelope mismatch: math calibrated for secular-trending single-business equities; structurally fails cyclicals, conglomerates, and tail-volatility regimes. 53% GOOD / 25–30% stop-out frequency empirically confirms failure. MIN/MAX inversion in ATR stop formula adds a safety error. |
| C2 Behavioral | Behavioral Finance | **REFACTOR-REQUIRED** | Two structural behavioral failures dominate: V-shape miss creates trust-destroying highly memorable salient loss ("bot was wrong at the COVID bottom"); ATR stop produces numbers retail either ignores or follows perversely — both outcomes destroy stop-credibility for all future signals. |
| C3 Retail+NSE | Indian Retail + NSE Specialist | **REFACTOR-REQUIRED** | Operationally broken for 50–60% of a real NIFTY 100 retail portfolio: BFSI combined display dead for 33% of index by weight, cyclical inversion compounds rather than compensates, weekly BANKNIFTY/FINNIFTY expiry not filtered for weekly bars, add-timing use case (most common retail need) completely unsupported. |
| C4 Signal Engineer | Systematic Strategy | **REFACTOR-REQUIRED** | Not yet a testable signal generator: no PIT universe, no exit rule, no survivorship-bias correction, indicator independence far worse than acknowledged (ROC/MACD/RSI r > 0.70), estimated walk-forward Sharpe ≈ +0.28–0.30 — right at the Q12 gate under median assumptions, confirmed below gate once survivorship bias accounted for. |
| C5 Cross-Cycle | FA/TA Integration | **REFACTOR-REQUIRED** | §10 is a display rule wearing a resolution rule's clothes; conservative default (§10.3 min()) is a wrong function — systematically over-penalizes cyclicals at troughs; BFSI has no row/column; PSU-CONTEXT not propagated; signal independence assumed never tested; combined system demonstrably worse than Cycle A alone on the best entry of the decade (Tata Steel Mar-2020). |
| **Synthesized** | All lenses | **REFACTOR-REQUIRED — UNANIMOUS** | Pipeline structure is the one area of cross-critic strength. Every substantive component — regime gate behavior for cyclicals, V-shape recovery handling, conglomerate exclusion by design, ATR stop formula, BFSI display gap, §10 resolution logic — requires targeted modification. v0.1 is usable as proof-of-architecture for quality non-cyclical names (ITC/Infosys/HDFC Bank); it is not usable as a live signal for any real NIFTY 100 portfolio that includes cyclicals, conglomerates, or BFSI. |

---

## §2 — Per-weakness consensus (B-W1 through B-W7 + B-P1)

### B-W1 — Cyclical inversion in TA domain

**Individual critic positions:**

- **C1 Quant: CONFIRM + EXTEND.** The inversion is geometric, not a calibration error: the 40-week SMA at a trough reflects the average of 40 weeks ending at bottom-price — the worst possible SMA position by construction. Expected lag = ~20 weeks structural minimum + 4-week confirmation = 24 weeks minimum from actual bottom to BULL signal. The critical finding is cross-cycle compounding: at Mar-2020 Tata Steel, Cycle A's Piotroski (trailing fundamentals) and Cycle B's 40-week SMA (trailing price) are both bearish for the same reason — both are lagged measurements on a mean-reverting commodity-cycle-driven stock. Their correlation through the shared commodity-price driver makes them compound rather than diversify. §10's "agree = stronger signal" interpretation inverts at cyclical extremes: two lagging signals on the same underlying are NOT two independent confirmations.

- **C2 Behavioral: CONFIRM + EXTEND (behavioral dimension).** The synthesis understates a specific disposition-effect failure mode: a retail investor holding a cyclical through its trough (which disposition effect ensures they often do) looks to the bot for permission to hold conviction or add. The bot gives neither — both cycles say avoid. One of two behavioral outcomes: (a) investor ignores the bot for cyclicals (bot utility = zero for 20–25% of portfolio), or (b) investor sells the existing position to resolve cognitive dissonance between "bot says AVOID_ENTRY" and "I still hold this." Option (b) is the bot actively causing a bad sell at the worst time — worse than no signal at all.

- **C3 Retail+NSE: CONFIRM + NSE SCOPE EXTENSION.** The same compounding failure applies to PSU capex names (NTPC, Power Grid, BHEL) and infrastructure-adjacent companies (L&T, Adani Ports) — the B.4 test universe (Tata Steel, Maruti) covers steel and auto but the actual NIFTY 100 has a much wider swath of cyclicals. Infrastructure capex cycle should be named explicitly as a third cyclical profile alongside commodity-cyclical and auto-cyclical.

- **C4 Signal Engineer: CONFIRM.** REGIME-OVERRIDE trigger conditions need one additional co-condition not in the synthesis proposal: `ROC(4w) > +5%` (nascent price recovery visible in a 4-week window while 40-week gate is still BEAR). This is a pure TA leading signal that does not require Cycle A sector data and can be computed within Cycle B alone.

- **C5 Cross-Cycle: CONFIRM + STRUCTURAL IMPLICATION.** §10's "agree = more confident" interpretation fails specifically for cyclicals because the two cycles are not independent. The correct interpretation: "two lagging-indicator systems both flagging the same trailing deterioration — correlation ≠ confirmation." The §10 conservative-default (min()) is wrong as a function. It must be suspended for CYCLICAL-tagged stocks when sub-reason is REGIME-BEAR and Cycle A label is WATCH.

**Consensus**: UNANIMOUS, strongest cross-critic agreement. The cyclical inversion is not a tuning problem — it is a structural design-envelope mismatch with compounding cross-cycle implications.

**Key divergence**: C4 adds a 4w ROC co-condition for REGIME-OVERRIDE trigger that other critics do not mention. C5 goes further than other critics in saying §10's conservative-default function must be changed, not just noted. No substantive disagreement — these are complementary.

**Synthesized recommendation**: REGIME-OVERRIDE hook (v0.1 §3.4 placeholder) must be activated with: (i) stock tagged CYCLICAL or INFRA-CAPEX-CYCLE; (ii) BEAR regime for ≥ 12 weeks; (iii) ADX < 18 (trend exhaustion); (iv) ROC(4w) > +5% (C4 addition); (v) Cycle A label not REVIEW or FLAG. On activation: ENTRY_ZONE (half) with `REGIME-OVERRIDE-ACTIVE` annotation. §10 conservative default suspended when [WATCH × AVOID_ENTRY: REGIME-BEAR, CYCLICAL stock] — output flags `CYCLICAL-TROUGH-CANDIDATE` explicitly.

**B.4 priority floor → Synthesized priority**: P0 (B.4 synthesis) → **P0 confirmed**. Full resolution is Cycle F (signal correlation estimation). Cycle B v0.2 implements the REGIME-OVERRIDE hook and §10 suspension as stopgaps.

---

### B-W2 — Lagging regime gate misses V-shape recoveries

**Individual critic positions:**

- **C1 Quant: CONFIRM + QUANTIFIED.** In a sharp-V recovery, the price must rise above the still-declining SMA (which is dragged down by crash-period bars), then hold for 4 confirmation weeks. Typical lag for a V-shape with 30% decline: 12–16 weeks total. During COVID, Infosys +155% / 12m: approximately 60% of the initial recovery was geometrically inaccessible to v0.1 architecture. CIRCUIT-RECENT chaining compounds: multiple circuit hits in March 2020 suppress signals for 15–20 days cumulatively. The proposed P0.2 fix is directionally correct but the specific volume threshold (1.5× 13-week avg) needs calibration — false-positive rate of 1-week BEAR→BULL trigger on normal corrections is not yet measured.

- **C2 Behavioral: CONFIRM AS CRITICAL.** The behavioral cost exceeds the quant cost: V-shape recoveries are the most emotionally salient market events. An investor who watched the bot say WAIT while the market rallied 30% will remember this for years. The trust destruction is not symmetric with trust-building: 20 correct calls do not undo one high-profile miss at the COVID bottom. The sequential-blockage problem: CIRCUIT-RECENT blocks for 3–4 weeks → REGIME-BEAR blocks for 8–12 more weeks → by the time ENTRY_ZONE fires, the opportunity has largely passed. Neither filter knows the other is also blocking; the investor sees them as separate legitimate blocks. Additionally, the regime-transition moment needs its own communicative design: when BEAR→BULL flips, the output must explicitly acknowledge "Prior WAIT/AVOID_ENTRY reflected BEAR regime. Entry opening now" to close the trust loop.

- **C3 Retail+NSE: CONFIRM + DELIVERY VOLUME ADDITION.** The volume confirmation for BEAR→BULL should reference NSE bhavcopy delivery volume (delivery-to-traded ratio), not just absolute volume. V-shape recoveries on NSE are accompanied by high delivery volume (genuine demand), distinguishing them from short-covering recoveries. Also: the F&O expiry proximity filter (§0.3) additionally suppresses daily signals within ±2 days of monthly expiry — in a V-shape environment, the first genuine recovery week often coincides with expiry week, creating a third block (CIRCUIT-RECENT + REGIME-BEAR + EXPIRY-PROXIMITY).

- **C4 Signal Engineer: ENGINEERING ASSESSMENT — asymmetric hysteresis with up-volume co-condition.** Total volume at bottoms includes capitulation (selling climaxes). The correct filter is up-volume (volume on weeks where close > open) > 1.5× 13-week average up-volume, not total volume. This is implementable from OHLCV without additional data sources. Sharpe cost analysis: whipsaw cost of faster BEAR→BULL adds approximately 0.05–0.10% NAV drag per year; late-entry cost from missing V-shapes is approximately 0.4% NAV on one stock in one event. Asymmetric hysteresis is Sharpe-positive under realistic assumptions.

- **C5 Cross-Cycle: MEDIUM CROSS-CYCLE SEVERITY.** At Mar-2020, Cycle A would have produced WATCH (not REVIEW/FLAG) for most affected stocks. If §10 had a rule distinguishing AVOID_ENTRY-REGIME-BEAR from AVOID_ENTRY-WEAK-MOMENTUM, [WATCH × AVOID_ENTRY: REGIME-BEAR] could have flagged the regime-gate lag explicitly. This requires §10 to propagate Cycle B sub-reasons, not just top-level labels.

**Consensus**: UNANIMOUS. The fix direction (asymmetric hysteresis) is agreed by all five critics. The up-volume refinement (C4) improves the proposal vs the B.4 synthesis's total-volume specification.

**Key divergence**: C3 adds delivery percentage; C4 adds up-volume (close > open). These are different metrics measuring similar things. Recommendation: use up-volume (C4's formulation, implementable from OHLCV) as primary; delivery percentage (C3's formulation, requires bhavcopy delivery column) as supplementary annotation. The two together are stronger than either alone.

**Synthesized recommendation**: BULL→BEAR: keep 4-week. BEAR→BULL: shorten to 1 week if AND ONLY IF: (a) ADX rising (DX increasing ≥ 2 of last 3 weekly bars), AND (b) weekly up-volume > 1.5× 13-week avg up-volume, AND (c) +DI > -DI. If only (a) and (c) but not (b): shorten to 2 weeks. Standard 4-week otherwise. §10 must propagate AVOID_ENTRY sub-reason to distinguish regime-lag from momentum failure.

**B.4 priority floor → Synthesized priority**: P0 (B.4 synthesis) → **P0 confirmed**.

---

### B-W3 — Conglomerate ENTRY_ZONE never fires

**Individual critic positions:**

- **C1 Quant: CONFIRM + ARITHMETIC CAUSE.** STRONG-PULLBACK requires simultaneous top-quintile ROC AND RSI 40–70. During any NIFTY 100 sectoral rally, 40–50 stocks in the leading sector outrank Reliance in cross-sectional ROC. Reliance achieves top-quintile ROC only during broad market rallies — but in those periods RSI quickly exceeds 70 (violating condition 2) or the 26w ex-1m period averages a sustained multi-quarter run that means the pullback is already over. The proposed fix of lowering threshold to top-tercile is "a hack, not a design fix" — a conglomerate at ROC rank 25–33 is exhibiting average performance, not momentum. Sector-relative ROC (option c) is statistically more defensible.

- **C2 Behavioral: CONFIRM + ASYMMETRIC LABEL HARM.** Zero ENTRY_ZONE labels across 6 dates means the bot generates repeated WAIT on a name that a retail investor likely holds. After 6 months of WAIT on a rising Reliance, the investor's affect-based prior on the stock has been nudged negative regardless of conscious reasoning. Annotation needed: when no ENTRY_ZONE has fired for a stock in a trailing 12-month window, explicitly flag "Model limitation: conglomerate ROC penalty may prevent signal generation regardless of price performance."

- **C3 Retail+NSE: CONFIRM + SCOPE EXPANSION.** Not just Reliance: ITC (diversifying), Mahindra & Mahindra (auto + agri + finserv + IT), L&T (construction + defense + IT + finance), Bajaj group names, Adani group names, Tata Consumer Products (separated mid-cycle) all share the structural property. At least 6–7 NIFTY 100 names face this. The mechanism is not that conglomerates are slow — it is that their cross-sectional ROC is a structural artifact of diversification, not a signal about business quality.

- **C4 Signal Engineer: RANKS THE FIX OPTIONS.** Three options ranked: (a) lower ROC threshold → weakest, degrades signal (momentum premium concentrates in top quintile, not top tercile — academic consensus); (b) business-segment regime tagging → conceptually correct, 40–80 hours of data engineering + annual maintenance; (c) sector-relative ROC → best practical fix for v0.2, low data cost (NSE sector index downloads available free), moderate signal improvement. Recommendation: option (c) for v0.2, option (b) for v0.3, never option (a).

- **C5 Cross-Cycle: CONF, not specifically extended.** Cross-cycle implications are secondarized under B-W4 treatment.

**Consensus**: UNANIMOUS on the problem. Agreement on sector-relative ROC as the v0.2 fix. C4 provides the definitive ranking of fix options; C1 agrees on the same ranking.

**Key divergence**: C1 explicitly says lowering the threshold to top-tercile is a "category error disguised as threshold adjustment" and should not be implemented. The B.4 synthesis proposed top-tercile as P1.3. Based on C1 and C4's analysis, **top-tercile threshold lowering should be removed from the v0.2 plan** and replaced entirely with sector-relative ROC.

**Synthesized recommendation**: Implement sector-relative ROC (MAX of NIFTY 100 quintile rank vs NSE Sector quintile rank) as the v0.2 fix. Annotate which signal drove the classification. Do NOT lower the ROC quintile threshold — this degrades signal quality without fixing the structural problem. Add "ENTRY_ZONE has not fired in 12 months — possible conglomerate ROC limitation" annotation. Business-segment regime tagging deferred to v0.3.

**B.4 priority floor → Synthesized priority**: P1 (B.4 synthesis) → **Escalated to P0** given C1/C4 cross-confirmation that sector-relative ROC is the minimum fix and the conglomerate exclusion is a 0-ENTRY_ZONE design failure for a class of 6–7 NIFTY 100 names.

---

### B-W4 — NIFTY 100 cross-sectional ROC disadvantages off-theme stocks

**Individual critic positions:**

- **C1 Quant: CONFIRM as broader form of B-W3.** B-W3 is a special case of B-W4. The sector-relative ROC fix (P1.1 in synthesis, now sector-relative as primary fix for B-W3) addresses both simultaneously. The MAX operator increases recall at the cost of precision — v0.2 should track which signal (sector vs index) drove the classification per cell to measure the sector-relative false-positive rate empirically.

- **C2 Behavioral: CONFIRM, secondary severity.** The behavioral harm is bounded if the reasoning string explicitly shows "ROC rank 45 of 100 → MOMENTUM-MID" — the investor can understand why the signal is what it is. The deeper issue: ITC during 2014–2022, the pipeline correctly avoided ENTRY_ZONE for 8 years because of relative ROC — which is defensible for a cross-sectional screening tool but questionable for a long-term investor's add-timing question. Requires the use-case-mode distinction (SCREEN vs ADD_TIMING).

- **C3 Retail+NSE: EXTEND.** Most Indian retail investors use TA for single-stock add-timing ("should I add to my ICICI Bank position now?"), not for cross-sectional screening ("which of 100 stocks should I enter?"). The cross-sectional ROC ranking is irrelevant for add-timing. v0.2 needs a formal mode distinction: SCREEN mode (cross-sectional ROC appropriate) vs ADD_TIMING mode (absolute ROC vs own 52-week percentile substituted for cross-sectional rank).

- **C4 Signal Engineer: CONFIRM.** Same root cause as B-W3. Sector-relative ROC fix addresses both. No additional engineering observations beyond B-W3 analysis.

- **C5 Cross-Cycle: Not specifically extended.** Addressed within B-W1/B-W3 framing.

**Consensus**: Unanimous confirmation. The sector-relative ROC fix (primary fix for B-W3) directly addresses B-W4 as well. The mode distinction (C3's SCREEN vs ADD_TIMING) is a new design element not in the B.4 synthesis.

**Key divergence**: C2 says "WAIT for 8 years on ITC was correct for the screening use case." C3 says "8 years of WAIT trains the investor wrong if they're asking an add-timing question." Both are right — the difference is use case. The mode distinction resolves the tension.

**Synthesized recommendation**: Sector-relative ROC covers the cross-sectional screening failure. For v0.2, add a formal mode parameter (SCREEN / ADD_TIMING). In ADD_TIMING mode: suppress NIFTY 100 cross-sectional ROC ranking; replace with stock's absolute ROC vs own 52-week percentile for momentum classification. Document which mode is active in every output.

**B.4 priority floor → Synthesized priority**: P1 (B.4 synthesis) → **P1 confirmed** but partially addressed by the B-W3 sector-relative ROC fix.

---

### B-W5 — ATR stop unusable in crisis volatility

**Individual critic positions:**

- **C1 Quant: CONFIRM + CRITICAL FORMULA CORRECTION.** The B.4 synthesis proposed: `stop_loss = MIN(2.5 × ATR, 0.15 × price)` for the stop, with position size recalculating from the capped stop. **This inverts the MIN/MAX and produces dangerous oversizing in crisis conditions.** Correct formula: stop is placed at MIN(2.5 × ATR, 0.15 × price) — the closer stop. But position size must use MAX(2.5 × ATR, 0.15 × price) in the denominator to prevent oversizing. If ATR implies 32% stop and the cap is 15%, the stop executes at 15% but position sizing uses the 32% distance — so the portfolio risks approximately 0.47% NAV (not 1%). Without the MAX in the denominator, position size TRIPLES in crisis conditions (risk_per_share = 15% vs 32%), and a 3× larger position entering at worst-volatility moment is not safer. **This is a safety-critical math correction for v0.2.**

- **C2 Behavioral: CONFIRM AS MOST OPERATIONALLY DAMAGING.** Two failure modes, both wrong: Response A (follow the stop) → investor places stop at ₹520 on HDFC Bank at ₹770, watches stock drop to ₹640, overrides at ₹650 crystallizing a 17% loss before the +80% recovery. Response B (ignore the stop) → stop discarded as meaningless, position sizing decoupled from risk budget, 1% per-name discipline abandoned. The 32% stop in one edge case contaminates the stop framework for all future signals ("stops from this bot are advisory only"). Also: the distribution of 2.5×ATR stops has two tails, not one — crisis (too wide) AND calm-market (7% stop triggers on normal quarterly-miss corrections, prompting manual override).

- **C3 Retail+NSE: CONFIRM + TAX HOOK.** A 2.5×ATR stop on a HDFC Bank position held 11 months would trigger STCG (15% flat). The same position held 1 more month is LTCG (10% above ₹1L threshold). The bot has no mechanism to flag this — stop math runs without reference to holding period. Cycle E hook required: if stop triggers within X trading days and the position approaches 12-month LTCG threshold, flag `LTCG-THRESHOLD-PROXIMITY`.

- **C4 Signal Engineer: CONFIRM + VOLATILITY-REGIME-CONDITIONAL CAP.** The 15% flat cap may be too tight in genuine crisis volatility (VIX > 35) — HDFC Bank had multiple 10–15% weekly moves during COVID recovery, meaning a 15% cap would have been hit and triggered, only for the stock to continue recovering. Better: 3-regime volatility-conditioned stop: LOW (ATR/price < 3%) = 2.5×ATR; NORMAL (3–5%) = 2.0×ATR capped 12%; HIGH (≥5%) = 1.5×ATR capped 10%.

- **C5 Cross-Cycle: CONFIRM, secondary from cross-cycle lens.** Defers substance to the quant and behavioral critics.

**Consensus**: Unanimous. **The C1 MIN/MAX formula correction is the most critical safety finding in the entire B.5 critique — it must be explicitly fixed in v0.2 before the formula creates oversized crisis positions.**

**Key divergence**: C1 says use MAX in the denominator (ATR-implied distance) for position sizing. C4 says use a 3-regime conditional multiplier rather than a flat cap. These are compatible: the 3-regime system determines the stop distance; the MAX in the denominator prevents oversizing. Combined approach is safer than either alone.

**Synthesized recommendation**: Three-regime ATR stop:
- Low volatility (ATR/price < 3%): `stop = 2.5 × ATR`
- Normal (3–5%): `stop = 2.0 × ATR, cap 12% of price`
- High (≥5%): `stop = 1.5 × ATR, cap 10% of price`

Position sizing: `position_size = floor(risk_budget / MAX(regime_stop_distance, ATR-implied_distance))` — always uses the FARTHER of the two distances in the denominator, preventing oversizing regardless of which regime fires. Annotate when cap fires: "STOP-DISTANCE-CAPPED: stop placed at [X%] (ATR implies [Y%]); position size reflects ATR risk, not capped-stop risk." Add Cycle E tax hook for LTCG threshold proximity.

**B.4 priority floor → Synthesized priority**: P0 (B.4 synthesis) → **P0 confirmed, with added urgency on the MIN/MAX formula safety correction**.

---

### B-W6 — BFSI combined display §10 completely non-functional

**Individual critic positions:**

- **C1 Quant: CONFIRM, defers to other lenses.** BFSI is 30–35% of NIFTY 100 by market cap. A system that cannot be validated on 30–35% of its target universe for the combined-display dimension is functionally incomplete. When running the walk-forward Sharpe computation, all BFSI names must be excluded from the combined Cycle A/B backtest until Cycle A BFSI labels are available — the backtest must be reported as "70% universe coverage."

- **C2 Behavioral: CONFIRM + SINGLE-LENS MASQUERADE.** The worst behavioral risk: the investor sees ENTRY_ZONE for HDFC Bank with no Cycle A counterpart — it looks like a complete dual-lens signal but is structurally single-lens. The safety-net feature (§10) is missing for the investor's largest holding without them knowing it's missing. Until BFSI FA pipeline is built, the output must explicitly say: "FA LENS: Not available — BFSI-specific FA pipeline not yet implemented. Cycle B TA signal only — treat with additional caution."

- **C3 Retail+NSE: CONFIRM — STRONGEST POSITION OF ALL FIVE CRITICS.** BFSI = 33–36% of NIFTY 100 by free-float market cap as of 2025–2026. A retail investor's portfolio typically has higher-than-index BFSI weight (HDFC Bank + ICICI Bank are the first two "safe" large-cap names retail is told to hold; 20–40% BFSI is normal retail). The combined display — the most important user-facing feature of the combined system — is dead for the largest sector. **This is a product-breaking omission, not a minor v0.1 limitation.** Escalates Cycle A v0.4 candidate V3 (full BFSI FA pipeline) to cross-cycle blocker for Cycle B v0.2. The BFSI-MONITOR directional flag (IMPROVING / STABLE / DETERIORATING on NIM + GNPA composite) is the minimum interim fix — a flat BFSI-MONITOR with no sub-classification is not sufficient.

- **C4 Signal Engineer: CONFIRM.** Engineering concern is the testing gap — cannot validate the combined signal on 30%+ of the universe.

- **C5 Cross-Cycle: CONFIRM + FORMALIZES THE SUB-ROW.** The §10 BFSI-MONITOR row must distinguish three sub-states: BFSI-IMPROVING (NIM rising OR GNPA falling AND CAR stable) → treat as WATCH-equivalent; BFSI-STABLE (all indicators stable) → treat as WATCH-equivalent with lower weight; BFSI-DETERIORATING (NIM compressing OR GNPA rising OR CAR tightening) → treat as REVIEW-equivalent. Specifically: [BFSI-DETERIORATING × ENTRY_ZONE] must be Strong-conflict, not silently conservative-defaulted. The mapping from NIM/GNPA/CAR direction to Cycle A label equivalent has never been formally specified in any document — this is the gap.

**Consensus**: Unanimous, and C3's escalation to "cross-cycle blocker" is the strongest single statement in any critique. C5 provides the most specific fix: the three BFSI sub-states and their mapping to Cycle A label equivalents.

**Key divergence**: C2 says explicit "FA lens unavailable" annotation is sufficient as interim. C3 says BFSI-MONITOR directional flag is the minimum. C5 says the three sub-states + resolution mapping must be specified. These are complementary layers: C2's annotation is the floor; C3's directional flag is the middle layer; C5's sub-state resolution is the ceiling. All three should be in v0.2.

**Synthesized recommendation**: Three-layer BFSI v0.2 fix: (1) explicit "FA LENS INCOMPLETE" annotation on all BFSI outputs; (2) BFSI-MONITOR directional flag (IMPROVING / STABLE / DETERIORATING on NIM + GNPA composite) as interim proxy; (3) formal §10 BFSI-MONITOR sub-row with resolution rules per C5's three sub-states. Formally escalate Cycle A V3 (full BFSI FA pipeline) to cross-cycle blocker — if V3 is not built before Cycle C begins, the combined display remains dead for 33% of NIFTY 100 indefinitely.

**B.4 priority floor → Synthesized priority**: High (B.4 synthesis) → **P0 confirmed**.

---

### B-W7 — Structural-event distortion of regime gate

**Individual critic positions:**

- **C1 Quant: CONFIRM + MECHANISM.** Corporate events create breaks in the return-generating process. The 40-week SMA assumes a stationary generating process; a merger or demerger is a regime change in the process. For HDFC Bank (merger Jul-2023), any 40-week SMA computed through approximately May-2024 includes pre-merger prices and is economically meaningless. Post-event: if > 13 weeks of post-event data exist, use only post-event data for SMA; otherwise flag INSUFFICIENT-POST-EVENT-DATA. Materiality threshold: any event where post-event market cap differs from pre-event by > 15%, or a new revenue segment enters at > 10% of revenue.

- **C2 Behavioral: CONFIRM at medium severity.** The behavioral harm is to the investor's mental model of what the regime gate means. An investor who understands the 40-week SMA as a "clean measure of price trend vs long-term mean" will find a merger-distorted value confusing. Any date range where a structural event falls within the 40-week lookback must carry `STRUCTURAL-EVENT-CAUTION` annotation; conviction should be downgraded to half regardless of regime gate reading.

- **C3 Retail+NSE: CONFIRM + EXPANDED CATALOG.** The synthesis names 2 events. The last 5 years alone have 8–10 significant events requiring annotation: HDFC-HDFC Ltd merger (Jul-2023), Jio Financial Services demerger from Reliance (Jul-2023), ITC Hotels demerger (Jul-2024), LIC IPO entry into NIFTY 100 (May-2022), Adani governance crisis (Jan-2023), Reliance Jio launch (Sep-2016), Paytm inclusion/exclusion cycle, Wipro buyback/split series (2020–2022). The annotation table scope must cover all of these, not just the 2 originally named. Also: if evaluation date is within 26 weeks (not just 40 weeks) of the event, the 26-week ROC is also contaminated — suppress ROC quintile classification as well as SMA regime signal.

- **C4 Signal Engineer: CONFIRM, lower engineering priority.** The annotation table + conviction downgrade is appropriate. Priority is lower than B-W1/B-W2 from a Sharpe perspective. When a structural event occurs, the 40-week SMA should be re-anchored: post-event prices weighted more heavily; if > 13 weeks post-event, use only post-event data; if < 13 weeks, use a 10-week or 20-week SMA as interim regime gate.

- **C5 Cross-Cycle: CONFIRM.** PSU-CONTEXT annotation passthrough into §10 (analogous gap, different cause): PSU stocks do get a real Cycle A label but it carries PSU-CONTEXT modifiers that change its interpretation — §10 does not propagate these into the conflict matrix display. Similarly, structural events should propagate into the §10 display string.

**Consensus**: Unanimous. C3's expanded catalog is a significant practical extension beyond the 2-event synthesis.

**Key divergence**: None material. C3's scope expansion and C4's re-anchoring mechanism are complementary additions, not alternatives.

**Synthesized recommendation**: Build structural-event annotation table covering at minimum the 8–10 events from C3's catalog. Rule: when evaluation date is within 40 weeks of a structural event, annotate `STRUCTURAL-EVENT-CAUTION` and downgrade conviction; when within 26 weeks, also suppress ROC quintile classification. Post-event re-anchoring: if > 13 weeks post-event, use only post-event data for SMA computation. Materiality: C1's 15% market-cap-change or 10% new-revenue-segment threshold.

**B.4 priority floor → Synthesized priority**: Medium / P1 (B.4 synthesis) → **P1 confirmed** (scope expanded from 2 to 8–10 events).

---

### B-P1 — REGIME-DI-CONFLICT (+DI/-DI flip) is a LEADING indicator

**Individual critic positions:**

- **C1 Quant: CONFIRM + LEAD-TIME QUANTIFIED.** +DI/-DI crosses when recent bars are more directionally negative than positive; the 40-week SMA crosses when cumulative closes have averaged below the SMA level. For a sustained trend reversal, DI flip typically precedes SMA crossover by 4–12 weeks (consistent with general DMI vs SMA literature). Maruti Sep-2018 canon shows 4–8 weeks lead. The P0.4 proposed trigger (−DI > +DI for 2 consecutive weeks AND ADX < 20 → EXIT_WARNING) is statistically justified. False-positive risk: DI flip can occur during mid-trend consolidation — ADX < 20 filter reduces but does not eliminate this. Parameter sensitivity between ADX < 15, < 20, and < 25 needs empirical testing.

- **C2 Behavioral: EXTEND — the lead timing has specific behavioral value.** The DI-flip fires before significant losses have accumulated; the investor is in a near-breakeven or modest-loss frame. Action-taking in this psychological state is substantially easier than action-taking after a confirmed regime break when losses are already large. The DI-flip is not just a better leading indicator mathematically — it fires in the right emotional window. EXIT_WARNING from DI-flip should explicitly say "Directional strength weakening — trend may be transitioning" rather than just the label.

- **C3 Retail+NSE: CONFIRM + RELAXED THRESHOLD.** DI flips are visible in Zerodha Kite's standard charting — retail investors can verify this manually, which is rare for TA pipeline signals. One refinement: the 2-consecutive-weeks threshold should be relaxed to "1 week with MACD histogram confirmation" as alternative path: -DI > +DI in current week AND (2nd consecutive week OR MACD histogram turns negative). This reduces the false-absence cost on fast-moving crises (NBFC Sep-2018) while maintaining confirmation discipline.

- **C4 Signal Engineer: CONFIRM — HIGHEST SHARPE CONTRIBUTION.** DI-flip as EXIT_WARNING for held positions: saves approximately 8–16% drawdown per correctly timed EXIT_WARNING, contributing +0.08 to +0.12 annual Sharpe. DI-flip as standalone entry signal: weaker (base rate of DI crossovers in BEAR regime developing into sustainable recoveries is 30–40%). Recommendation: promote DI-flip specifically as EXIT_WARNING first (highest impact, lowest false-positive risk); as entry signal, keep it as REGIME-OVERRIDE co-condition only, not standalone.

- **C5 Cross-Cycle: EXTEND — timing asymmetry in the combined display.** Cycle B's DI-flip has a 4–8 week informational lead over Cycle A for macro-event directional changes (Cycle A's quarterly-update cadence would not catch the NBFC crisis turn until the next quarterly result). The combined display in §10 is timing-naive — showing both labels as of the same evaluation date without acknowledging Cycle A's label is based on the last quarterly report while Cycle B's is computed on latest price action. This is a cross-cycle framing gap that should be noted in §10.3 even if the full math is Cycle F.

**Consensus**: Unanimous promotion recommended. C4 provides the definitive case for DI-flip specifically as EXIT_WARNING (not standalone entry signal).

**Key divergence**: C4 says DI-flip as standalone entry is weak (30–40% base rate in BEAR); C3 says relaxing to 1-week + MACD confirmation reduces false absences. Synthesized: EXIT_WARNING trigger uses the C3 relaxed threshold (1 week + MACD confirmation as alternative to 2 consecutive); entry use stays as REGIME-OVERRIDE co-condition per C4.

**Synthesized recommendation**: Promote DI-flip to standalone EXIT_WARNING trigger with C3's threshold: trigger if regime = BULL AND ADX < 20 AND [(-DI > +DI for 2 consecutive weeks) OR (-DI > +DI this week AND MACD histogram turns negative)]. For BEAR-regime entry, retain as co-condition in REGIME-OVERRIDE framework (C4's guidance). Add to §10.3: timing note that Cycle B's DI-flip has a 4–8 week informational lead over Cycle A's quarterly-updated label.

**B.4 priority floor → Synthesized priority**: P0 (B.4 synthesis P0.4) → **P0 confirmed**, EXIT_WARNING promotion is the primary application.

---

## §3 — NEW concerns surfaced by critics (beyond B-W1 to B-W7)

### Consolidated new-concern table

| ID | Theme | Raised by | Others echo | Severity | Synth priority |
|---|---|---|---|---|---|
| **QUANT-A** | Indicator inter-correlation: ROC/MACD/RSI are not 3 independent signals | C1 | C4 (SE-A) | High | **P1** |
| **QUANT-B** | Discrete labeling on continuous signals: boundary cost at RSI 40/70 and ROC quintile edge | C1 | C2 (BC-D) | High | **P1** |
| **QUANT-C** | 53% GOOD hit rate does not map cleanly to Sharpe > 0.3 — gap is wider than synthesis acknowledges | C1 | C4 (SE-B) | High | **P1** |
| **QUANT-D** | Parameter sensitivity: all thresholds are single-point defaults, not NSE-calibrated | C1 | C4 (SE-E) | Medium | **P2** |
| **QUANT-E** | Bollinger Squeeze threshold (30% of 6m avg) is unvalidated on NSE data | C1 | — | Low | **P3** |
| **QUANT-F** | Divergence detection: 12-week peak/trough method unspecified — two valid implementations produce different results | C1 | — | Low | **P2** |
| **BC-A** | WAIT sub-reasons: investor needs distinct monitoring instructions per sub-reason, not just a label | C2 | — | High | **P0** |
| **BC-B** | Half-conviction is not an actionable mental model: ENTRY_ZONE (half) needs size range + "add to full" trigger | C2 | — | Medium | **P1** |
| **BC-C** | Confirmation bias amplification in §10 conflict display: mild conflicts need friction questions, not just strong conflicts | C2 | C5 (CC-2) | Medium | **P1** |
| **BC-D** | Label oscillation at thresholds creates anxiety rather than information — needs label-level hysteresis (2-week confirmation) | C2 | C1 (QUANT-B) | High | **P1** |
| **BC-E** | Stop intuition gap extends beyond crisis: calm-stock 7% stops also get overridden; stop needs a "why this works" narrative | C2 | — | Medium | **P1** |
| **NEW-R1** | Weekly expiry (BANKNIFTY/FINNIFTY) creates weekly chart distortion not covered by monthly F&O filter in §0.3 | C3 | — | High | **P0** |
| **NEW-R2** | ASM/ESM historical data unavailable pre-2017 — pre-screen silently passes stocks with unknown surveillance status for 2008-10 and 2014-06 test dates | C3 | — | Medium | **P1** |
| **NEW-R3** | Nifty Next 50 vs Nifty 50 liquidity tier: 1% risk budget not comparable across tiers; slippage eats 15% of risk budget on ₹20L portfolio for Next 50 | C3 | C4 (SE-C cost model) | Medium | **P1** |
| **NEW-R4** | NSE bhavcopy data quality: 2008-10 test window is on uncertain ground; pre-2007 adjusted prices are inconsistently adjusted on commercial platforms | C3 | — | Medium | **P1** |
| **NEW-R5** | ESG/thematic overlays: ITC tobacco ESG discount, PSU fuel pricing, pharma NPPA, Adani governance — TA generates ENTRY_ZONE despite known thematic headwinds | C3 | C2 (B-P1 mention of BC-E) | Medium | **P1** |
| **NEW-R6** | Use-case mismatch: pipeline designed for cross-sectional screening; most retail use cases are single-stock add-timing | C3 | C2 (B-W4 discussion) | High | **P0** |
| **SE-A** | Indicator independence worse than v0.1 implies: ROC/MACD/RSI pairwise r = 0.60–0.82; ATR/Bollinger bandwidth r = 0.65–0.80 | C4 | C1 (QUANT-A) | High | **P1** |
| **SE-B** | Walk-forward Sharpe projection: +0.28–0.30 under median assumptions — right at the Q12 gate; confirmed below gate with survivorship bias | C4 | C1 (QUANT-C) | High | **P1** |
| **SE-C** | Backtest infrastructure gap: PIT universe, cost model, slippage by tier, survivorship-bias-corrected universe — none exist | C4 | — | High | **P0** (pre-walk-forward) |
| **SE-D** | Survivorship bias in B.4 test universe: all 6 stocks are survivors; falling stocks (DHFL, Yes Bank, Vodafone Idea) test the downside-detection path | C4 | — | High | **P1** |
| **SE-E** | Parameter optimization risk: 15–20 optimizable parameters vs 36 test cells — any v0.2 threshold change motivated by B.4 data is in-sample overfitting | C4 | — | Medium | **P2** |
| **SE-F** | Missing exit rule prevents Sharpe computation: without trailing stop or time-stop, average hold period may extend to 24–36 months | C4 | — | High | **P0** (pre-walk-forward) |
| **CC-1** | Signal independence assumed, never tested: agree rate is sector-conditional (70–80% for defensives, 30–40% for cyclicals) — §10 "agree = stronger" is wrong for cyclicals | C5 | C1 (QUANT-A) | High | **P1** |
| **CC-2** | B1/B2 dominance rule (§10.3) is ambiguous at the margin — every investment is simultaneously B1 and B2; the rule needs operational sharpening | C5 | — | Medium | **P1** |
| **CC-3** | PSU stocks invisible to §10 conflict matrix: PSU-CONTEXT from Cycle A not propagated into combined display | C5 | — | Low | **P2** |
| **CC-4** | §10 "Agree" cells have no confidence dimension: HOLD + ENTRY_ZONE from marginal signals treated identically to HOLD + ENTRY_ZONE from strong signals | C5 | — | Low | **P2** |
| **CC-5** | Cycle B v0.2 scope implications for problem statement: BFSI gap means the combined display cannot be exercised for 30%+ of NIFTY 100 indefinitely within sequential cycle structure | C5 | C3 (NEW-R1) | High | **v0.5 candidate** |

**Safety callout — QUANT-A / SE-A (Indicator Inter-Correlation):**
C1 and C4 both independently identify ROC/MACD/RSI pairwise correlation at r = 0.60–0.82 (redundant level). The v0.1 routing table that requires MACD confirmation after RSI confirmation is not adding independent information — it is requiring agreement between two measures of the same underlying momentum phenomenon. The MACD confirmation gate passes approximately 85–95% of the cases that reach it. The effective degrees of freedom in the confirmation step are 1.5–1.8, not 3. For v0.2: decouple the three indicators by role — RSI → momentum level; MACD → divergence detection only; Bollinger → mean-reversion positioning only. Remove MACD "positive and rising" from ENTRY_ZONE routing as a standalone confirmation gate.

**Safety callout — B-W5 MIN/MAX inversion (C1):**
Already covered in §2 B-W5. Re-stated here for emphasis: the B.4 synthesis inverts the MIN/MAX in the ATR stop cap formula in a way that triples position size in crisis conditions. This is the most critical safety-math finding in B.5. The correct formula uses MIN for the stop price and MAX for the denominator in position size. This must be explicitly corrected in the v0.2 spec.

---

## §4 — Ranked v0.2 priorities — synthesized

### P0 — Unanimous or near-unanimous (≥3 critics); cannot ship v0.2 without

| # | Title | Exact specification | Raised by | B.4 floor → Final |
|---|---|---|---|---|
| **P0.1** | REGIME-OVERRIDE hook with correct trigger conditions | CYCLICAL/INFRA-CAPEX tagged + BEAR ≥ 12wk + ADX < 18 + ROC(4w) > +5% + Cycle A not REVIEW/FLAG → ENTRY_ZONE (half), REGIME-OVERRIDE-ACTIVE annotation. §10 conservative default suspended for [WATCH × AVOID_ENTRY: REGIME-BEAR, CYCLICAL]. | C1, C2, C3, C4, C5 | P0 → **P0** |
| **P0.2** | Asymmetric hysteresis with up-volume confirmation | BULL→BEAR: 4-week (unchanged). BEAR→BULL: 1 week if ADX rising + up-volume > 1.5× 13-wk avg up-volume + +DI > -DI; 2 weeks if only (a) and (c); 4 weeks otherwise. | C1, C2, C3, C4, C5 | P0 → **P0** |
| **P0.3** | ATR stop: 3-regime cap + **corrected MIN/MAX position formula** | Low (ATR/P < 3%): 2.5×ATR. Normal (3–5%): 2.0×ATR cap 12%. High (≥5%): 1.5×ATR cap 10%. Position size denominator = MAX(regime_stop_distance, ATR-implied_distance) — prevents crisis oversizing. | C1, C2, C3, C4 | P0 → **P0 (safety)** |
| **P0.4** | DI-flip as standalone EXIT_WARNING | Trigger: BULL + ADX < 20 + [(-DI > +DI 2 consecutive wks) OR (-DI > +DI this week AND MACD histogram negative)]. EXIT_WARNING for held positions. As REGIME-OVERRIDE co-condition for BEAR regime entry only. | C1, C2, C3, C4, C5 | P0 → **P0** |
| **P0.5** | Sector-relative ROC supplement | Compute ROC quintile within NSE Sector peer set + NIFTY 100 cross-sectional. Use MAX of the two for momentum classification. Annotate source. Track per cell which signal drove classification. Do NOT lower quintile threshold for conglomerates (C1/C4 consensus: degrades signal). | C1, C2, C3, C4 | P1 → **Escalated to P0** |
| **P0.6** | WAIT sub-reasons: monitoring instructions | Each WAIT variant requires distinct monitoring instruction: RANGING → "No action. Re-check in 4 weeks." SQUEEZE-PENDING → "Monitor daily. Breakout expected 4–8 weeks." PULLBACK-CONTINUING → "Check weekly. Entry possible 2–4 weeks if MACD histogram turns positive." POSITION-EXTENDED → "Held positions: watch for EXIT_WARNING. Not held: no action." NOISY-MOMENTUM → "ROC and RSI conflict. Re-check after 2 weekly closes." | C2 (primary), C3 | Not in B.4 → **P0** |
| **P0.7** | BFSI combined display: three-layer fix | (1) "FA LENS INCOMPLETE" annotation on all BFSI outputs. (2) BFSI-MONITOR directional flag (IMPROVING / STABLE / DETERIORATING on NIM + GNPA composite). (3) Formal §10 BFSI-MONITOR sub-row with C5's three-state resolution rules. Escalate Cycle A V3 (full BFSI FA pipeline) to cross-cycle blocker. | C1, C2, C3, C4, C5 | High → **P0** |
| **P0.8** | Weekly expiry distortion annotation (BANKNIFTY/FINNIFTY) | Extend §0.3 to weekly chart signals for BFSI names that are BANKNIFTY/FINNIFTY constituents. Flag weekly bars closing within 1 day of weekly expiry as WEEKLY-EXPIRY-DISTORTION. Downgrade conviction by one level on ENTRY_ZONE generated in such weeks. | C3 | Not in B.4 → **P0** |
| **P0.9** | Mode split: SCREEN vs ADD_TIMING | Add formal mode parameter. SCREEN mode: current pipeline (cross-sectional ROC). ADD_TIMING mode: suppress cross-sectional ROC; replace with absolute ROC vs own 52-week percentile for momentum classification. Document in every output which mode is active. | C3 (primary), C2 | Not in B.4 → **P0** |
| **P0.10** | Minimum viable exit rule for Sharpe computation | (a) Initial ATR stop (already in v0.1). (b) 52-week time-stop (if no EXIT_WARNING after 12 months, exit and re-evaluate). (c) Trailing stop at 1.5×ATR from highest close reached since entry. Required before any walk-forward Sharpe computation can be run. | C4 | Not in B.4 → **P0** (backtest prerequisite) |
| **P0.11** | §10 B1/B2 dominance rule: operational sharpening | Replace "default to more conservative" with: Cycle A must be WATCH or better for ENTRY_ZONE to proceed. [WATCH × ENTRY_ZONE] = half-conviction. [HOLD × ENTRY_ZONE] = full-conviction. [REVIEW or FLAG × ENTRY_ZONE] = WAIT regardless. | C5 (primary), C2 | Not in B.4 → **P0** |

### P1 — Strong desirables (2–3 critics)

| # | Title | Spec summary | Raised by | Priority |
|---|---|---|---|---|
| **P1.1** | Structural-event annotation table (expanded) | 8–10 events from C3's catalog. Within 40wk: STRUCTURAL-EVENT-CAUTION + conviction downgrade. Within 26wk: also suppress ROC quintile. Post-event re-anchoring: > 13 weeks post-event, use only post-event data for SMA. | C1, C2, C3, C4 | P1 (was P1 in B.4, scope expanded) |
| **P1.2** | Label-level hysteresis (2-week confirmation for transitions) | Any non-knockout label transition requires 2 consecutive weekly evaluations. Output during first confirmation week: "[NEW LABEL] (pending: 1 of 2 weekly confirmations)." Exception: EXIT_WARNING and SURVEILLANCE-HALT fire immediately. | C2 (primary), C1 | Not in B.4 → P1 |
| **P1.3** | Indicator role decoupling (RSI/MACD/Bollinger) | RSI → momentum level. MACD → divergence detection ONLY (remove "positive and rising" from ENTRY_ZONE routing as standalone gate). Bollinger → mean-reversion positioning ONLY. Reduces false independence of confirmation step. | C1, C4 | Not in B.4 → P1 |
| **P1.4** | Fuzzy zones at discrete threshold boundaries | RSI 40: ±2 fuzzy zone (38–42) → half-conviction regardless of ROC class. RSI 70: ±2 fuzzy zone (68–72). ROC quintile: ranks 18–22 in transitional band → half-conviction. Reduces label-flip frequency at boundaries by 60–70%. | C1 | Not in B.4 → P1 |
| **P1.5** | Half-conviction: size range + "add to full" trigger | ENTRY_ZONE (half) expresses size as ±10% range (not single precise number). Add "Full position trigger: if stock achieves ENTRY_ZONE (full) conditions in subsequent evaluation, add remaining half." | C2 | Not in B.4 → P1 |
| **P1.6** | Friction question on Cycle A/B mild conflicts | For every §10 conflict cell, mandatory one-sentence friction question before action label: "Before [action]: [specific question about the tension between the two signals]." Implements behavioral implementation-intention design. | C2, C5 | Not in B.4 → P1 |
| **P1.7** | "No ENTRY_ZONE in 12 months" annotation | When a stock has received 0 ENTRY_ZONE signals in trailing 52-week window: append "NOTE: No ENTRY_ZONE signal in past 12 months. This may indicate model limitations (conglomerate ROC penalty, sector-rotation dynamics) rather than a negative thesis." | C2, C3 | Not in B.4 → P1 |
| **P1.8** | Thematic-overhang annotation layer | NEW-R5. Initial table: ITC tobacco ESG (resolved 2022), PSU fuel pricing (ongoing), pharma NPPA (ongoing), Adani governance (ongoing). Confidence downgrade on ENTRY_ZONE for affected names. Disclosure, not filter. | C3 | Not in B.4 → P1 |
| **P1.9** | Nifty Next 50 slippage adjustment | One-time lookup (which 50 names are Nifty Next 50). 0.15% round-trip slippage adjustment to effective stop price for Next 50 names. Annotate NEXT50-SLIPPAGE-ADJUSTED. | C3, C4 | P2 in B.4 → P1 |
| **P1.10** | Survivorship-bias test extension | Include at least Yes Bank (2018–2020) and Vodafone Idea (2018–2022) in B.4 extended test to validate downside-detection path without requiring full PIT universe build. | C4 | Not in B.4 → P1 |
| **P1.11** | Combined-confidence propagation in §10 Agree cells | Surface Cycle A data-quality score tier and Cycle B conviction modifier (full/half) in the Agree-cell reasoning string. No new math — field propagation only. | C5 | Not in B.4 → P1 |
| **P1.12** | Data quality annotations for pre-2017 test windows | ASM/ESM/T+T unavailable pre-2017 → SURVEILLANCE-DATA-UNAVAILABLE (not PASS). 2008-10 test data → DATA-QUALITY-UNCERTAIN on all computed signals. | C3 | Not in B.4 → P1 |
| **P1.13** | CYCLICAL-SECTOR advisory note on AVOID_ENTRY | For cyclical-sector stocks receiving AVOID_ENTRY: REGIME-BEAR, append: "CYCLICAL-SECTOR NOTE: For cyclical stocks, REGIME-BEAR at a sector trough may coincide with the best entry opportunity. This signal prevents new entry on trend-following grounds — it does not address valuation timing. See Cycle A (FA) output for fundamental context." | C2 | Not in B.4 → P1 |

### P2 — Specialist findings; defer if scope-constrained

| # | Title | Spec summary | Raised by | Priority |
|---|---|---|---|---|
| **P2.1** | Walk-forward Sharpe feasibility rough estimate | Run a rough walk-forward on the 19 GOOD cells from B.4: estimate entry/exit prices, stop-out events, return distribution, ex-post Sharpe. Not a proper walk-forward but gives a lower bound on architectural Sharpe capability. | C1 | P2 |
| **P2.2** | Bollinger Squeeze threshold NSE calibration | Compute distribution of weekly Bollinger bandwidth for NIFTY 100 stocks over 3 years. Use empirical 10th percentile per stock as stock-specific SQUEEZE threshold rather than universal 30% multiplier. | C1 | P3 deferred |
| **P2.3** | Divergence detection method specification | Specify peak/trough detection: rolling-window maximum/minimum within 12-week lookback, minimum 3-week distance between identified peaks/troughs, no look-ahead. Two valid implementations currently produce different results from same data. | C1 | P2 |
| **P2.4** | Tax interaction note on stop (Cycle E hook) | If estimated holding period to stop-out < 12 months: STCG-APPLICABLE annotation. If position is 10–12 months old: LTCG-THRESHOLD-PROXIMITY annotation. Lookup of entry date vs 12-month LTCG threshold; no math change. | C3 | P2 |
| **P2.5** | Parameter stability report before walk-forward | Sweep ADX threshold (15–25, steps 2.5) and ROC lookback (17–39wk, steps 4wk). Plot hit rate across grid. If > 10% hit-rate variation across range, parameters require careful selection with held-out test set. | C4 | P2 |
| **P2.6** | PSU-CONTEXT annotation passthrough to §10 | Propagate Cycle A PSU-CONTEXT annotation into the §10 combined display string for all PSU-tagged stocks. One display-logic addition. | C5 | P2 |
| **P2.7** | Regime-transition acknowledgment message | When BEAR→BULL flip produces first ENTRY_ZONE: "REGIME TRANSITIONING TO BULL: Prior WAIT/AVOID_ENTRY signals reflected BEAR or transitional regime. Entry opening now." Addresses trust damage from B-W2 V-shape miss. | C2 | P2 |

### P3 — Defer to v0.3 or beyond

| # | Item | Reason for deferral |
|---|---|---|
| **P3.1** | Business-segment regime tagging for conglomerates | 40–80 hours data engineering + annual maintenance; v0.3 after sector-relative ROC (P0.5) is validated |
| **P3.2** | Bollinger Squeeze NSE calibration (P2.2) | Not a material source of observed failures; address in v0.3 |
| **P3.3** | Breadth thrust (advance/decline line) as BEAR→BULL co-condition | Requires cross-stock data in per-stock pipeline — architectural change for v0.3 |
| **P3.4** | Indicator independence empirical measurement (pairwise correlation computation) | Should precede full walk-forward; schedule as data task before B.7 |
| **P3.5** | Full BFSI FA pipeline (Cycle A V3) | Cross-cycle blocker — schedule as dedicated Cycle A v0.4 mini-iteration |

---

## §5 — What v0.1 got RIGHT (cross-critic consensus)

**1. Pipeline architecture (pre-screen → regime → trend-strength → volatility → momentum → confirmation → sizing → label) is logically correct and statistically sound.**
All five critics separately praised the gate-sequencing logic. The architecture correctly accounts for the dependency structure of the signals: measuring momentum in a BEAR regime is measuring the wrong thing; checking regime first restricts the prior before momentum logic is applied. This is the "one area of consensus strength" across all five lenses. (C1, C2, C3, C4, C5 all confirm.)

**2. ROC(26w, ex-1m) construction is the strongest individual methodological choice.**
The exclusion of the most recent 4 weeks (NSE Nifty 200 Alpha 30 methodology) to avoid short-term reversal contamination is evidence-based and empirically validated on NSE. This is the v0.1 design choice most likely to survive parameter scrutiny in a walk-forward backtest. (C1, C4 explicitly confirm; others implicitly.)

**3. ITC Jun-2022 ENTRY_ZONE is the v0.1 ideal case — validating the architecture works for its intended purpose.**
Multi-year ESG-overhang underperformance correctly avoided (no ENTRY_ZONE). Re-rating inflection correctly caught via ENTRY-PULLBACK path. Forward 12m +46% excess vs NIFTY 100 with stop never hit. 5/6 GOOD per-stock hit rate. This is the pipeline working exactly as designed for the stock profile it was designed for. (C1, C3, C4 explicitly confirm; C2 endorses reasoning-string design via this example.)

**4. Pre-screening filters (ASM/ESM, CIRCUIT-RECENT, data sufficiency) are the most NSE-specific, highest-precision additions in the spec.**
Western TA frameworks miss these entirely. Commercial Indian TA tools (TradingView, Chartink, Zerodha Kite) do not surface these systematically. The CIRCUIT-RECENT filter correctly prevented false ENTRY_ZONE during the early V-shape that would have been failed by deeper crash. The ASM/ESM check catches surveillance manipulation. These are genuine NSE idiosyncrasies that are correctly implemented. (C3 explicitly praises; C4 confirms as signal-engineering correct; C1 endorses pre-screen sequence.)

**5. ADX(14) weekly + +DI/-DI directional check is well-supported and the most independent signal in the set.**
The Naik & Reddy (2019) NSE-specific study uses ADX-filtered momentum — v0.1's primary evidence base. The +DI/-DI directional consistency check in §4.3 adds valuable information beyond ADX magnitude alone (distinguishes strong range-bound from strongly directional). The 40-week SMA is the most independent indicator in the seven-indicator set (C1 confirms r = 0.25–0.45 with momentum signals vs 0.60–0.82 within the momentum group). (C1, C4 explicitly confirm; all five critics preserve the ADX gate.)

**6. ATR-based position sizing framework is the correct design in normal regimes.**
The 1% NAV per-name risk limit combined with ATR-implied stop-distance produces positions that naturally shrink during high-volatility periods. The 5% NAV concentration cap prevents absurdly large positions for low-ATR quality compounders. The failure mode (B-W5) is a boundary condition (crisis ATR), not a fundamental flaw in the framework's design logic. (C1 explicitly confirms; C3 endorses framework concept even while flagging retail intuition gap.)

**7. The 4-label + (full)/(half) output set maps cleanly to retail investor actions.**
ENTRY_ZONE tells you to enter. WAIT tells you to wait. AVOID_ENTRY tells you to avoid. EXIT_WARNING tells you to exit or tighten. All four labels are directional — no non-actionable label (contrast: Cycle A's REVIEW was flagged as non-actionable). EXIT_WARNING is specifically identified as the highest-behavioral-value label: it fires when action is hardest (in a loss frame) but most needed. (C2, C3 explicitly confirm; others implicitly.)

**8. The reasoning string design (§9.2 full derivation chain) is the correct behavioral architecture.**
The investor can argue with the label because they can trace exactly what produced it — each step's output and routing decision is visible. This is the central behavioral design requirement for any signal system: the investor's ability to disagree with a specific step rather than receiving an oracle decision. (C2 strongly endorses; C3 praises it via ITC example; all critics assume this transparency structure in their fix proposals.)

---

## §6 — Specific math changes for B.6 — the v0.2 refactor brief

B.6 should read this section and produce `25_cycle_B_math_v0.2.md`. Each sub-section is a prescription.

### 6.1 Pre-screen (Step 0) changes

**§0.2 CIRCUIT-RECENT**: Keep as-is. The 5-day suppression is behaviorally valuable (C2 explicitly endorses keeping it). The V-shape miss problem (B-W2) is addressed by asymmetric hysteresis in §0.1/§3.2, not by weakening the circuit filter.

**§0.3 F&O expiry — extend to weekly bars for BANKNIFTY/FINNIFTY constituents** (NEW-R1, P0.8):
- Current: applies to daily-chart signals only, monthly expiry ±2 days.
- v0.2 addition: for stocks that are BANKNIFTY or FINNIFTY constituents (lookup table: HDFC Bank, ICICI Bank, Kotak Mahindra Bank, Axis Bank, IndusInd Bank, SBI, State Bank of India, Bajaj Finance, Bajaj Finserv, and any others on the constituent list), also flag weekly bars where the bar closes within 1 trading day of BANKNIFTY expiry (Wednesday) or FINNIFTY expiry (Tuesday) with `WEEKLY-EXPIRY-DISTORTION`.
- Do not discard the weekly signal entirely; downgrade conviction by one level on any ENTRY_ZONE generated in the flagged week.

**New §0.5 — Data quality annotation** (NEW-R2, P1.12):
- For evaluation dates before 2017-01-01: set surveillance check to SURVEILLANCE-DATA-UNAVAILABLE rather than PASS. Append to output: "ASM/ESM/T+T machine-readable data unavailable for this evaluation date."
- For evaluation dates using data from 2008 or earlier: append DATA-QUALITY-UNCERTAIN to all computed signals.

**New §0.6 — Structural-event annotation lookup** (B-W7 expanded, P1.1):
Maintain a lookup table: each row = stock + event date + event type + SMA-contamination flag.

| Stock | Event | Event date | SMA window contamination rule | ROC contamination rule |
|---|---|---|---|---|
| HDFCBANK | HDFC-HDFC Ltd merger | 2023-07-01 | CAUTION through 2024-05-01 (40wk) | SUPPRESS ROC through 2023-12-31 (26wk) |
| RELIANCE | Jio Financial Services demerger | 2023-07-20 | CAUTION through 2024-05-21 | SUPPRESS ROC through 2024-01-20 |
| ITC | ITC Hotels demerger | 2024-07-01 | CAUTION through 2025-05-01 | SUPPRESS ROC through 2025-01-01 |
| RELIANCE | Jio launch (business mix change) | 2016-09-01 | CAUTION through 2017-07-01 | SUPPRESS ROC through 2017-03-01 |
| ADANIENT / ADANIPORTS | Hindenburg crisis | 2023-01-24 | CAUTION through 2023-11-24 | SUPPRESS ROC through 2023-07-24 |
| LIC | IPO / NIFTY 100 entry | 2022-05-17 | ROC rank baseline reset on entry date | — |
| WIPRO | Buyback/split series | 2020-01-01 to 2022-12-31 | CAUTION during window; review each event | — |

When an evaluation date falls within the SMA contamination window: annotate `STRUCTURAL-EVENT-CAUTION`, downgrade conviction by one level. When within the ROC contamination window: additionally suppress ROC quintile classification and use ADX/DI signals only for momentum routing.

### 6.2 Regime gate (Step 1) — asymmetric hysteresis + REGIME-OVERRIDE

**§3.2 — Replace symmetric hysteresis with three-tier asymmetric system:**

```
BULL→BEAR: unchanged (4-week confirmation)

BEAR→BULL (fast path — 1 week):
  Conditions:
    (a) ADX rising (DX increasing in ≥ 2 of the last 3 weekly bars)
    (b) Up-volume (closes-above-open weeks) > 1.5× 13-week average up-volume
    (c) +DI > -DI in current week
  If all (a), (b), (c) met in week 1 after price crosses SMA: BULL immediately

BEAR→BULL (moderate path — 2 weeks):
  Conditions:
    (a) ADX rising
    (c) +DI > -DI
    but NOT (b) volume confirmation
  If (a) and (c) but not (b): confirm after 2 weeks above SMA

BEAR→BULL (standard path — 4 weeks):
  No additional conditions met: keep 4-week confirmation
```

Annotate in output which path triggered the BULL transition.

**§3.4 — REGIME-OVERRIDE activation (replace placeholder with live math):**

Trigger conditions (ALL must be met simultaneously):
1. Stock carries a CYCLICAL or INFRA-CAPEX-CYCLE sector tag (lookup table maintained in Cycle A v0.3 §9.1; INFRA-CAPEX-CYCLE tag to be added covering: EPC/construction-revenue > 40%, regulated infrastructure utilities, captive commodity processors)
2. Current regime = BEAR for ≥ 12 consecutive weeks
3. ADX < 18 (trend exhaustion — not accelerating deterioration, just no directional trend)
4. ROC(4w) = (Price_t − Price_{t-4}) / Price_{t-4} × 100 > +5% (nascent price recovery detectable in short-window ROC)
5. Cycle A label is not REVIEW or FLAG

On activation:
- Output: ENTRY_ZONE (half) with `REGIME-OVERRIDE-ACTIVE` annotation
- Position size: 50% of half-conviction budget (i.e., 25% of full budget = 0.25% NAV per name)
- Reasoning string must include: "REGIME-OVERRIDE: All five trigger conditions met. Entry generated despite BEAR regime for CYCLICAL/INFRA-CAPEX stock at possible trough. Position sized to 25% of normal."

§10 modification: When a CYCLICAL-tagged stock has [WATCH × AVOID_ENTRY: REGIME-BEAR] in the §10 matrix, suspend the conservative default and output `CYCLICAL-TROUGH-CANDIDATE: Both cycles may be trailing the same commodity-cycle signal. Conservative default suspended. Half-conviction entry at user discretion. Full resolution requires Cycle F signal-combination math.`

### 6.3 Beneish-equivalent

**N/A for Cycle B** — the TA pipeline has no Beneish equivalent. The structural-event annotation table in §6.1 is the TA-side analog of Cycle A's regime-shift calendar.

### 6.4 ADX + DI-flip promotion (Step 2)

**§4.3 — Upgrade DI-flip from downgrade modifier to standalone leading signal (P0.4):**

Add to Step 2 output logic:

```
DI-flip EXIT_WARNING trigger (for held positions):
  IF regime = BULL
  AND ADX < 20
  AND [(-DI > +DI for 2 consecutive weeks)
       OR (-DI > +DI this week AND MACD histogram < 0)]
  → EXIT_WARNING: DI-FLIP-CAUTION
  Output: "Directional strength weakening (-DI > +DI): trend may be transitioning.
           If this persists 2 weeks, consider tightening stop or taking partial profits.
           Monitor weekly."

DI-flip AVOID_ENTRY escalation (for not-held positions in BULL regime):
  IF regime = BULL
  AND ADX < 20
  AND above conditions met
  → AVOID_ENTRY (new position): DI-FLIP-AVOID
  Output: "Directional bias has turned bearish despite BULL regime.
           Avoid new entry. Re-evaluate when +DI > -DI is restored."

REGIME-OVERRIDE contribution (for BEAR stocks):
  IF regime = BEAR
  AND +DI > -DI for 2 consecutive weeks
  AND ADX < 18
  → This contributes to REGIME-OVERRIDE trigger (condition 3 and partially 4)
  (Not a standalone ENTRY_ZONE trigger — only as co-condition in §3.4)
```

Add to §10.3: "Note: Cycle B's DI-flip EXIT_WARNING may precede Cycle A's next quarterly label update by 4–8 weeks. When DI-flip fires and Cycle A label has not yet updated, weight the TA directional signal with appropriate deference to the informational lag."

### 6.5 ROC + sector-relative supplement (Step 4)

**§6.2 — Add sector-relative ROC classification:**

```
Compute two ROC quintile rankings for each stock:
  ROC_rank_N100 = quintile within NIFTY 100 cross-sectional (existing v0.1 logic)
  ROC_rank_sector = quintile within NSE Sector peer set (new v0.2 addition)
    - Peer set: all NIFTY 100 stocks in the same NSE Sector as the evaluated stock
    - If NSE Sector peer set N < 5: fall back to NSE Super-Sector (broader grouping)
    - If even Super-Sector N < 5: use NIFTY 100 cross-sectional only and annotate SECTOR-PEER-TOO-SMALL

Final ROC class = MAX(ROC_rank_N100_class, ROC_rank_sector_class)
  where class mapping: {ranks 1–20 → MOMENTUM-STRONG, 21–60 → MOMENTUM-MID, 61–100 → MOMENTUM-WEAK}

Annotate in output which ranking drove the classification:
  "Momentum classification: MOMENTUM-STRONG (driven by sector-relative ROC rank 8/18;
   NIFTY 100 cross-sectional rank 34)"
```

Do NOT lower the STRONG-PULLBACK ROC threshold from top-quintile to top-tercile for conglomerates. Sector-relative ROC fixes the structural problem; threshold dilution degrades signal quality (C1, C4 consensus).

**ADD_TIMING mode momentum classification:**
```
In ADD_TIMING mode (§6.9):
  Suppress ROC_rank_N100 and ROC_rank_sector entirely
  Replace with: absolute_ROC_percentile = percentile of current ROC(26w, ex-1m) within
    the stock's own 52-week history of ROC(26w, ex-1m) values
  Classification:
    absolute_ROC_percentile ≥ 70th: MOMENTUM-STRONG (absolute basis)
    40th–70th: MOMENTUM-MID (absolute basis)
    < 40th: MOMENTUM-WEAK (absolute basis)
  Annotate: "ADD_TIMING mode: Momentum measured against own historical ROC, not NIFTY 100 cross-section."
```

### 6.6 ATR stop + corrected MIN/MAX position-size formula (Step 6)

**§8.2 — Replace single ATR stop with three-regime system:**

```
volatility_regime = ATR(14, weekly) / entry_price
  LOW:     volatility_regime < 0.03 (ATR < 3% of price)
  NORMAL:  0.03 ≤ volatility_regime < 0.05
  HIGH:    volatility_regime ≥ 0.05

stop_distance:
  LOW:    2.5 × ATR(14, weekly)
  NORMAL: MIN(2.0 × ATR(14, weekly), 0.12 × entry_price)
  HIGH:   MIN(1.5 × ATR(14, weekly), 0.10 × entry_price)

stop_loss_price = entry_price - stop_distance
```

**§8.3 — CORRECTED position size formula (critical safety fix from C1):**

```
risk_per_share_display = stop_distance          ← distance used for stop placement
risk_per_share_sizing  = MAX(stop_distance,
                             ATR-implied_distance)
  where ATR-implied_distance = 2.5 × ATR(14, weekly)
  (always uses the LARGER of actual stop distance and full-ATR distance in the denominator)

position_size_shares = floor(per_stock_risk_budget / risk_per_share_sizing)
position_size_value  = position_size_shares × entry_price

Annotation when stop cap fires:
  "STOP-DISTANCE-CAPPED: Stop placed at [stop_distance] (ATR implies [2.5×ATR]).
   Position sized to ATR-risk equivalent — actual portfolio risk < 1% NAV.
   Current effective NAV risk: [risk_per_share_display × position_size_shares / NAV × 100]%"
```

**§8.5 — Half-conviction output format:**
```
ENTRY_ZONE (half) position size output format:
  "Calculated: [X] shares (±10% range acceptable: [0.9X]–[1.1X] shares)
   This is a half-position. Full position trigger: if [stock] achieves ENTRY_ZONE (full)
   conditions in a subsequent weekly evaluation, add remaining [X] shares."
```

**§8.6 — Tax and LTCG hook (new for v0.2, Cycle E preview):**
```
If entry_date is known and (current_date − entry_date) ∈ [330, 365] days:
  Append: "LTCG-THRESHOLD-PROXIMITY: This position is approaching the 12-month LTCG threshold.
           If stop triggers before [entry_date + 366 days], STCG applies (15% flat)."
If entry_date is known and (current_date − entry_date) < 270 days:
  Append: "STCG-APPLICABLE: Position is < 9 months old. Any exit generates STCG."
```

**§8.7 — Stop-loss narrative (required on every sizing output):**
```
Every sizing output must include:
  "Stop-loss commitment: If [stock] closes a weekly bar below ₹[stop_price], the trend
   assumption underlying this entry has been invalidated. Exit at or near this price —
   do not wait for a bounce. This stop is placed [N]× normal weekly volatility below entry;
   a routine correction in a bull trend is unlikely to breach this level."
```

### 6.7 §10 combined-display redesign

**§10.1 — Extend conflict matrix to include BFSI sub-states and cyclical override:**

Extended rows (new in v0.2):

| | Cycle B: ENTRY_ZONE | Cycle B: WAIT | Cycle B: AVOID_ENTRY | Cycle B: EXIT_WARNING |
|---|---|---|---|---|
| **BFSI-IMPROVING** | ENTRY_ZONE (half, BFSI-pending): TA favorable; FA layer incomplete. Manual check: NIM + GNPA direction before full size. | WAIT — TA neutral; BFSI improving but no TA trigger. | AVOID_ENTRY — TA unfavorable. Sufficient to avoid regardless of BFSI state. | EXIT_WARNING — TA deteriorating. BFSI improving is insufficient to override TA exit signal. |
| **BFSI-STABLE** | ENTRY_ZONE (half, BFSI-pending): treat same as BFSI-IMPROVING but with lower confidence note. | WAIT | AVOID_ENTRY | EXIT_WARNING |
| **BFSI-DETERIORATING** | **STRONG CONFLICT** — FA deteriorating; TA favorable. Do not enter at full size. Requires explicit user acknowledgment. "BFSI fundamental deterioration in progress. TA signal may be lagging." | Mild conflict | Agree: avoid | Agree: exit review — check GNPA direction before acting |
| **CYCLICAL-TROUGH-CANDIDATE** | (activated by REGIME-OVERRIDE) ENTRY_ZONE (half): "Both cycles may trail same commodity signal — conservative default suspended. Full analysis pending Cycle F." | N/A | N/A | N/A |

**§10.2 — BFSI annotation on every BFSI-stock output:**
```
"FA LENS: BFSI-MONITOR (interim). Full BFSI FA pipeline not yet implemented.
 NIM: [IMPROVING / STABLE / DETERIORATING]
 GNPA: [IMPROVING / STABLE / DETERIORATING]
 Combined BFSI trend: [BFSI-IMPROVING / BFSI-STABLE / BFSI-DETERIORATING]
 Cycle B TA signal stands; treat with additional caution — single-lens output."
```

**§10.3 — Replace "more conservative label" with operational dominance rules:**
```
New position decision:
  Cycle A HOLD + Cycle B ENTRY_ZONE → full-conviction entry (B2 timing with B1 thesis confirmed)
  Cycle A WATCH + Cycle B ENTRY_ZONE → half-conviction entry + friction question
  Cycle A REVIEW + Cycle B ENTRY_ZONE → WAIT regardless of conviction modifier
  Cycle A FLAG + Cycle B ENTRY_ZONE → WAIT + explicit STRONG-CONFLICT marker

Cyclical exception (CYCLICAL-TROUGH-CANDIDATE):
  Cycle A WATCH + Cycle B AVOID_ENTRY: REGIME-BEAR + CYCLICAL-tagged stock
  → CYCLICAL-TROUGH-CANDIDATE: Conservative default suspended. Half-conviction entry at user discretion.

Friction question (added to every mild-conflict cell):
  Before action: [specific question about the tension between the two signals]
  Examples:
    WATCH + ENTRY_ZONE: "Before entering: Is the fundamental concern producing WATCH
                          a thesis-breaking risk or a temporary setback?"
    HOLD + WAIT: "Before waiting: Is the TA-based WAIT due to trend absence (RANGING)
                   or a setup forming (SQUEEZE-PENDING)? These require different monitoring."
```

**§10.4 — Combined-confidence propagation in Agree cells:**
```
For all Agree cells, reasoning string must include:
  "Cycle A confidence: [HIGH/MED/LOW from data-quality score in last FA evaluation]
   Cycle B conviction: [full/half]
   Combined confidence: [HIGH if both HIGH/full; MED if one is lower; LOW if either is low/half]"
```

**§10.5 — Sub-reason propagation:**
```
In all conflict cells involving Cycle B AVOID_ENTRY:
  Surface the sub-reason: AVOID_ENTRY: REGIME-BEAR vs AVOID_ENTRY: WEAK-MOMENTUM
  vs AVOID_ENTRY: SQUEEZE-BROKE-DOWN
  Different sub-reasons have different Cycle A implications.
  REGIME-BEAR in a CYCLICAL context is a candidate for the CYCLICAL-TROUGH-CANDIDATE
  override. WEAK-MOMENTUM is not.
```

### 6.8 Action labels (WAIT sub-reasons; ENTRY_ZONE (half) sharpening)

**§9.1 — ENTRY_ZONE (half) clarification:**
- ENTRY_ZONE (half) is a defined label in the output set.
- Every ENTRY_ZONE (half) must include: (a) the size range (±10% of calculated shares); (b) the "add to full" trigger: "Full position trigger: if [stock] achieves ENTRY_ZONE (full) in a subsequent weekly evaluation, add remaining [X] shares."; (c) the ENTRY_ZONE (full) conditions that are currently not met (the specific sub-reason for half vs full conviction).

**§9.1 — WAIT sub-reason monitoring instructions (P0.6):**
```
WAIT: RANGING         → "No action required. Re-check in 4 weeks."
WAIT: SQUEEZE-PENDING → "Monitor daily. A breakout (up or down) is likely within 4–8 weeks.
                          When Bollinger Bandwidth expands past 30% of 26-week average,
                          re-run the full pipeline."
WAIT: PULLBACK-CONTINUING → "Check weekly. Entry possible in 2–4 weeks if MACD histogram
                              turns positive and +DI > -DI."
WAIT: POSITION-EXTENDED → "Already-held positions: watch for EXIT_WARNING trigger.
                             Not-held: no new entry. Monitor for price return to Bollinger middle band."
WAIT: NOISY-MOMENTUM  → "ROC and RSI signals conflict. Re-check after 2 weekly closes
                           when direction may clarify."
```

**§9.1 — Label-level transition hysteresis (P1.2):**
```
Any label transition (ENTRY_ZONE → WAIT, WAIT → ENTRY_ZONE, AVOID_ENTRY → WAIT, etc.)
requires 2 consecutive weekly evaluations confirming the new label.
During the first confirmation week, output:
  "[NEW LABEL] (pending: 1 of 2 weekly confirmations required)"

Exceptions — fire immediately on first occurrence:
  EXIT_WARNING (any trigger)
  AVOID_ENTRY: SURVEILLANCE-HALT
  REGIME-OVERRIDE activation
```

**§9.1 — "No ENTRY_ZONE in 12 months" annotation (P1.7):**
```
When a stock has received zero ENTRY_ZONE signals in the trailing 52-week window:
  Append: "NOTE: No ENTRY_ZONE signal has fired for this stock in the past 12 months.
           This may indicate model limitations (conglomerate ROC penalty, sector-rotation
           dynamics, or BFSI coverage gap) rather than a negative fundamental thesis.
           Evaluate whether this is a SCREEN-mode limitation or a genuine avoidance signal."
```

### 6.9 New components for v0.2

**ADD_TIMING pipeline mode (P0.9):**
```
Add mode parameter to pipeline call: mode = SCREEN | ADD_TIMING (default: SCREEN)

SCREEN mode (default): current v0.1 pipeline; cross-sectional ROC ranking active.
ADD_TIMING mode modifications:
  - Suppress NIFTY 100 cross-sectional ROC ranking
  - Replace with absolute_ROC_percentile vs own 52-week history (see §6.5)
  - All other steps (regime gate, ADX, Bollinger, MACD, RSI, ATR) unchanged
  - Output header: "MODE: ADD_TIMING — Momentum measured against own history, not NIFTY 100."
  - Recommended use: "Use ADD_TIMING to evaluate whether [stock you hold or are specifically
                       interested in] is at a favorable entry point. Use SCREEN to identify
                       new position candidates across the NIFTY 100."
```

**Structural-event annotation table** (§6.1, §0.6 above): implemented as a maintenance lookup table, not a calculation.

**Thematic-overhang annotation layer (P1.8, NEW-R5):**
```
Maintain a lookup table: stock + thematic description + status + start date + resolution date (if resolved).

Initial table:
  ITC | Tobacco ESG discount (global institutional ESG exclusions) | Partially resolved 2022 | 2014 → 2022
  BPCL/IOC/HPCL | PSU fuel pricing freeze (government-mandated price caps) | Ongoing
  Multiple pharma | NPPA price control orders | Ongoing (monitor NPPA releases)
  ADANIENT/ADANIPORTS | Governance uncertainty (Hindenburg allegations, ongoing legal) | Ongoing | 2023-01 → ?

When evaluation date falls within an active thematic overhang for a stock AND the pipeline
generates ENTRY_ZONE:
  Append: "THEMATIC-OVERHANG-ACTIVE: [Description].
           Consider reducing entry size or deferring until overhang resolution.
           This is a disclosure, not a signal filter — the TA analysis stands."
```

---

## §7 — Idea-review trigger check

Per the cycle convention (Cycle A.5 synthesizer §7 did the same), does B.5 surface anything that should update the v0.4 problem statement to v0.5?

### Candidate 1: B-W6 BFSI gap escalation (primary candidate)

**What the critics say:**
- C3 (Retail+NSE) explicitly states: "B-W6 should escalate V3 (full BFSI FA pipeline) to cross-cycle blocker for Cycle B v0.2."
- C5 (Cross-Cycle) adds: the v0.4 problem statement §8 says full BFSI pipeline is "scheduled for v0.3" of Cycle A, but at the current sequential cycle pace, Cycle B v0.2 will close and Cycle C will begin before Cycle A v0.3 is done — so the full BFSI pipeline is deferred indefinitely within the existing structure. Meanwhile, §10's combined display — the point of Q5 in the locked decisions ("surface TA/FA conflicts explicitly") — cannot be exercised for any BFSI name. The v0.4 problem statement says "no silent skips on banking/NBFC/insurance names in real-portfolio output" but the combined-display math is currently a silent skip for those names.

**What the v0.4 problem statement currently says:**
§8: "Cycle A FA pipeline covers NIFTY 500 including BFSI; v0.2 delivers a BFSI stub (trend indicators: NIM, GNPA, PCR, CAR) with a full BFSI sub-pipeline scheduled for v0.3."

**Analysis:** The v0.4 language covers Cycle A's obligation. The new finding is cross-cycle: Cycle B v0.2 cannot exercise §10's combined display for 33% of NIFTY 100 until Cycle A's BFSI pipeline is built. This creates a dependency between Cycle B and Cycle A that is not expressed in the current problem statement. Cycle C (MF analytics) and further cycles will also have BFSI-related gaps in combined display if Cycle A's BFSI pipeline remains at stub stage.

**VERDICT: v0.5 update recommended.** Add one sentence to §8: "Cycle A BFSI sub-pipeline is a cross-cycle dependency for Cycle B's combined display (§10): Cycle B v0.2 combined display for BFSI names will use an interim BFSI-MONITOR directional flag until the full BFSI pipeline is built. The full BFSI pipeline is escalated from 'scheduled for v0.3' to 'cross-cycle blocker' — it should be built as a Cycle A v0.4 mini-iteration before Cycle C begins."

---

### Candidate 2: NEW-R6 use-case mismatch (screening vs add-timing)

**What C3 says:** The v0.1 pipeline was designed as a cross-sectional screening tool. The most common retail use case is single-stock add-timing. These are different questions requiring different pipeline modes.

**What the v0.4 problem statement currently says:** §2 lists "Action label with 2–3 sentence reasoning" as the weekly report output. §8 specifies "NIFTY 100 restricted for TA signals in v1." Neither specifies which mode (screening vs add-timing) the pipeline operates in.

**Analysis:** The SCREEN vs ADD_TIMING mode distinction is an architectural addition to the pipeline (already prescribed in §6.9 above as P0.9). It does not require a problem-statement update — it is a v0.2 math change implementable within the existing problem-statement framing. The problem statement says "identify action labels per holding" which is consistent with add-timing mode.

**VERDICT: No v0.5 update needed.** The mode split is a B.6 math deliverable (§6.9), not a problem-statement-level design decision.

---

### Candidate 3: B-W1 cyclical inversion compounding (cross-cycle structural finding)

**What the critics say:** The cyclical inversion is not just a Cycle B problem — it is a combined-system problem. Adding Cycle B to Cycle A makes the output WORSE than Cycle A alone at the most important entries (Tata Steel Oct-2008, Mar-2020). This is a structural flaw in the Cycle A + Cycle B combination that requires Cycle F (signal combination math) to address.

**What the v0.4 problem statement currently says:** Q5 = "context-sensitive prompt with holding-period framing" for TA/FA conflicts. §8 of problem statement: "surfaces TA/FA conflicts explicitly." Neither addresses the case where TA and FA are not independent signals but are measuring the same trailing driver.

**Analysis:** The cyclical inversion compounding is a Cycle F math problem at root. The Cycle B v0.2 fix (REGIME-OVERRIDE hook + §10 cyclical-trough suspension) is a targeted mitigation, not a full solution. The finding does not require a problem-statement update — it requires Cycle F work that was already planned. The existing Q5 language ("context-sensitive prompt with holding-period framing") is still the right design; the math for making that prompt intelligent about signal correlation is Cycle F's job.

**VERDICT: Cycle F deferral.** No v0.5 update. The cyclical inversion is a known limitation that v0.2's REGIME-OVERRIDE hook mitigates; the full fix is explicitly Cycle F work.

---

### Candidate 4: SE-C backtest infrastructure (PIT universe requirement)

**What C4 says:** Full walk-forward Sharpe computation requires PIT NIFTY 100 universe (historical constituent lists), cost model, survivorship-bias-corrected universe. Without these, no Sharpe > 0.3 validation is possible.

**What the v0.4 problem statement says:** Q12: "Walk-forward, 3yr NSE data, Sharpe > 0.3 after costs." This is the gate. The how is not specified.

**Analysis:** The backtest infrastructure requirement is an implementation-level specification, not a problem-statement-level design decision. Q12 is already specific enough. The infrastructure work is a Cycle B v0.2/v0.3 deliverable.

**VERDICT: Cycle B v0.2 math fix (infrastructure task to be scheduled for B.7 pre-walk-forward).** No v0.5 update.

---

### Summary of §7 verdicts

| Candidate | Verdict |
|---|---|
| B-W6 BFSI gap escalation | **v0.5 problem-statement update** — add cross-cycle dependency sentence to §8 |
| NEW-R6 screening vs add-timing use case | Cycle B v0.2 math fix (§6.9 ADD_TIMING mode) — no problem-statement change needed |
| B-W1 cyclical inversion compounding | Cycle F deferral — REGIME-OVERRIDE hook mitigates in v0.2; full fix is Cycle F |
| SE-C backtest infrastructure gap | Cycle B infrastructure task (schedule before B.7 walk-forward) — no problem-statement change |

**Idea-review trigger check result: v0.5 update warranted on one item (BFSI cross-cycle dependency).**

---

## §8 — Open questions for Pranav before B.6 starts

These are the 7 binary or short-answer decisions that Pranav must make for B.6 to proceed. Recommended defaults in brackets.

---

**Q1: SCREEN mode vs ADD_TIMING mode — which is the PRIMARY design target for v0.2?**

The v0.1 pipeline was built for SCREEN mode (cross-sectional screening). C3 argues ADD_TIMING (single-stock timing for existing holdings) is the more common retail use case. Both modes are prescribable in §6.9, but the primary design target affects which test cases are written for B.4/B.7.

- Option A: SCREEN mode is primary; ADD_TIMING is secondary/additive. Tests written against cross-sectional screening.
- Option B: ADD_TIMING mode is primary; SCREEN mode is secondary. Tests focus on "should I add to [held stock] now?"
- Option C: Both modes at parity; v0.2 spec defines both fully and B.7 tests both.

**Recommended default: Option A.** SCREEN mode is already partially validated by B.4. ADD_TIMING mode is a v0.2 addition that requires its own testing (B.7). Build SCREEN fully first; ADD_TIMING as documented addition.

---

**Q2: REGIME-OVERRIDE trigger — should the ROC(4w) > +5% condition (C4 addition) be included?**

The B.4 synthesis P0.1 proposed 3 trigger conditions (CYCLICAL tag + BEAR ≥ 12wk + ADX < 18). C4 added a 4th: ROC(4w) > +5% (nascent price recovery in short-window ROC). Including it tightens the trigger (fewer REGIME-OVERRIDE activations, higher precision); excluding it means more overrides fire but potentially earlier in the recovery.

**Recommended default: Include ROC(4w) > +5%.** The additional precision is worth the cost of occasional false absences at early recoveries — the REGIME-OVERRIDE is already a conservative half-position entry, so a slightly later but more reliable trigger is better.

---

**Q3: ENTRY_ZONE (half) — keep as a distinct label, or consolidate all half-conviction cases into a single ENTRY_ZONE label with a conviction modifier in the sub-reason?**

v0.1 has two explicit ENTRY_ZONE labels: ENTRY_ZONE (full) and ENTRY_ZONE (half). C2 (behavioral) argues the binary-entry mental model of retail investors means ENTRY_ZONE (half) is not actionable. The §6.8 prescription addresses this with size-range and "add to full" trigger. But the fundamental label question remains open.

**Recommended default: Keep ENTRY_ZONE (half) as a distinct label.** The full/half distinction is genuinely informative — it tells the investor something meaningful about conviction level. The behavioral problem is in the presentation of the sizing output (addressed by §6.8's range format and add-to-full trigger), not in the label itself.

---

**Q4: BFSI interim fix — implement BFSI-MONITOR directional flag (IMPROVING / STABLE / DETERIORATING) as a Cycle B v0.2 deliverable, or wait for Cycle A to provide it as part of a Cycle A v0.4 mini-iteration?**

The three-layer BFSI fix in §6.7 requires: (1) explicit annotation (Cycle B can do this now); (2) BFSI-MONITOR directional flag (requires NIM/GNPA data — Cycle B can surface the flag if Cycle A's BFSI stub already computes it); (3) §10 BFSI sub-row with resolution rules (Cycle B can implement the matrix logic once the flag is defined).

**Recommended default: Cycle B v0.2 implements the §10 matrix logic and the annotation; the NIM/GNPA directional flag computation stays in Cycle A (it is already in Cycle A v0.2's BFSI-MONITOR stub). The two cycles coordinate on the data format of the directional flag before B.6 begins.** This splits the work correctly: Cycle A provides the signal, Cycle B uses it in §10.

---

**Q5: Parameter changes motivated by B.4 findings — how strict should the "no in-sample optimization" rule be for v0.2?**

C4 (SE-E) raises the overfitting concern: changing thresholds in response to B.4 findings is in-sample optimization on 36 data points. The v0.2 spec will change several thresholds (ADX < 18 for REGIME-OVERRIDE, ROC(4w) > 5%, volume 1.5× multiplier). Which changes are theory-motivated vs B.4-motivated?

- Theory-motivated (acceptable): ADX < 18 threshold for trend exhaustion (Wilder's own description of ADX < 20 as "non-trending" — the 18 sub-threshold for exhaustion has a principled basis); up-volume vs total volume (conceptually cleaner signal for demand vs capitulation); sector-relative ROC (addresses a structural misalignment, not a threshold optimization).
- B.4-motivated (potential overfitting risk): ROC(4w) > +5% threshold; exact ADX expansion thresholds for asymmetric hysteresis; volume 1.5× multiplier.

**Recommended default: Flag all B.4-motivated threshold changes in v0.2 as "tentative — requires walk-forward sensitivity sweep before production." Theory-motivated changes are incorporated without special flagging. The walk-forward backtest (pre-B.7 infrastructure task) will provide OOS validation.**

---

**Q6: Cycle A V3 (full BFSI FA pipeline) — trigger a Cycle A v0.4 mini-iteration before Cycle C begins, or defer until after all six cycles are complete?**

B.5's B-W6 finding and the §7 idea-review verdict recommend escalating V3 to "cross-cycle blocker." The v0.5 problem statement update (§7 verdict) formally documents the dependency. But the sequencing question — when to build V3 — is a planning decision.

- Option A: Cycle A v0.4 mini-iteration (BFSI only) runs in parallel with or immediately after Cycle B v0.2 is closed. Cycle C begins only after BFSI pipeline is available.
- Option B: Continue sequential cycle structure (Cycle C next); BFSI pipeline becomes the first task of Cycle A's next iteration in the eventual second-round pass.
- Option C: BFSI stub (already in v0.2) serves as the permanent interim; combined display for BFSI names operates in reduced mode indefinitely until all six cycles are complete and a second round begins.

**Recommended default: Option A — Cycle A v0.4 mini-iteration on BFSI only, scoped narrowly.** The BFSI gap is product-breaking for a realistic retail portfolio (33% of NIFTY 100). Deferring it means the combined system cannot exercise its most visible feature for the investor's largest sector for the duration of Cycles C through F.

---

**Q7: v0.5 problem-statement update — approve the single addition to §8 recommended in §7?**

The recommended addition to v0.4 §8: "Cycle A BFSI sub-pipeline is a cross-cycle dependency for Cycle B's combined display (§10): Cycle B v0.2 combined display for BFSI names will use an interim BFSI-MONITOR directional flag until the full BFSI pipeline is built. The full BFSI pipeline is escalated from 'scheduled for v0.3' to 'cross-cycle blocker' — it should be built as a Cycle A v0.4 mini-iteration before Cycle C begins."

This is a one-sentence scope update, parallel to the v0.3 → v0.4 update that added the BFSI staging sentence. No other problem-statement changes are recommended.

**Recommended default: Approve.** This is a factual update that reflects what B.5 established. Not approving it leaves a gap between what the problem statement says ("no silent skips on banking/NBFC names") and what the combined display actually does (silent skip in the §10 matrix for the entire BFSI sector).

---

**Status**: ✅ Synthesis complete. v0.2 brief ready for B.6.
**Idea-review verdict: v0.5 update recommended on one item (BFSI cross-cycle dependency). All other B.5 findings are Cycle B v0.2 math fixes or Cycle F deferrals.**

**Line count**: This document spans §1–§8. Priority items: 11 P0 / 13 P1 / 7 P2 / 5 P3 / 28 new themes from 5 critics consolidated.
