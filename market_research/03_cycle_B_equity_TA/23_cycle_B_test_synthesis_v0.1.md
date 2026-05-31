# 23 — Cycle B: Test Synthesis v0.1 (across 6 NIFTY 100 stocks)

**Status**: Final for v0.1; input to B.5 critique
**Date**: 2026-05-31
**Scope**: Synthesizes findings from 6 stock-level B.4 tests (`22a–22f`): HDFC Bank, Reliance, Infosys, Tata Steel, ITC, Maruti Suzuki. Each tested at 6 historical NSE evaluation dates (2008-10 / 2014-06 / 2018-09 / 2020-03 / 2022-06 / 2024-03) → 36 evaluation cells total.

---

## TL;DR — v0.1 verdict

**REFACTOR-REQUIRED**, parallel to Cycle A.4's verdict on FA v0.1.

| Metric | v0.1 result | Q3 target (from `21_cycle_B_math_v0.1.md` §13) | Pass? |
|---|---|---|---|
| GOOD verdicts | 19 / 36 (53%) | ≥ 60% on net | ❌ Below target |
| WRONG verdicts | 6 / 36 (17%) | Tolerable up to ~20% | ✅ Marginal pass |
| MARGINAL verdicts | 11 / 36 (31%) | Indicator of ambiguity, not failure | n/a |
| Stop-loss out frequency | 25–30% est. | < 25% target | ❌ Above target |

**v0.1 is empirically broken in five identifiable structural ways**, plus two stock-profile-specific failure modes:

| # | Structural weakness | Surfaced in | Severity |
|---|---|---|---|
| **B-W1** | **Cyclical inversion in TA domain** — 40-week SMA regime gate fires AVOID_ENTRY at commodity-cycle troughs, mirroring Cycle A's W3 Piotroski inversion. The two cycles do NOT compensate; they compound. | Tata Steel, Maruti Suzuki | **Critical** |
| **B-W2** | **Lagging regime gate misses V-shape recoveries** — 4-week BEAR→BULL hysteresis + CIRCUIT-RECENT block means entries come 30–50% after the actual crash bottom on V-shaped events (COVID being the cleanest case). | Infosys, HDFC Bank, Maruti, Reliance | **Critical** |
| **B-W3** | **Conglomerate ENTRY_ZONE never fires** — Reliance produced ZERO ENTRY_ZONE labels across all 6 dates because STRONG-PULLBACK setup is overspecified for event-driven, multi-segment businesses. | Reliance (canonical) | **Critical** |
| **B-W4** | **NIFTY 100 cross-sectional ROC disadvantages sector-specific rallies** — defensives during cyclical rallies, conglomerates during sector rotations, cyclicals during defensive bids all penalized for the wrong reason. | Reliance, ITC, Maruti | High |
| **B-W5** | **ATR-based stop unusable in crisis volatility** — Mar-2020 ATR(14) weekly produces 2.5× stop at ~25–30% below entry. Practically meaningless as a risk-management gate. | HDFC Bank (canonical), all stocks in Mar-2020 | High |
| **B-W6** | **BFSI combined display §10 completely non-functional** — HDFC Bank has no Cycle A FA label (SKIPPED-BFSI in v0.1); Cycle A/B integration cannot be exercised. | HDFC Bank | High (known from v0.4) |
| **B-W7** | **Structural-event distortion of regime gate** — HDFC Ltd merger (Jul-2023) crossed the 40-week SMA window; Jio launch (Sep-2016) caused multi-quarter momentum distortion not captured. No mechanism in v0.1 to annotate. | HDFC Bank, Reliance | Medium |

Plus one significant **positive finding** worth promoting:

| # | What worked | Source |
|---|---|---|
| **B-P1** | **REGIME-DI-CONFLICT (+DI/-DI flip) is a LEADING indicator** relative to the 40-week SMA — caught Sep-2018 NBFC crisis directional change before regime broke. Currently a downgrade flag in v0.1; should be promoted to its own entry/exit signal in v0.2. | Maruti Suzuki (canonical), Reliance |

---

## Test results in compact form

### Per-stock verdict distribution

| Stock | Profile | GOOD | MARGINAL | WRONG | Hit rate (GOOD/6) | Key finding |
|---|---|---|---|---|---|---|
| **HDFC Bank** | BFSI / structural compounder | 3 | 2 | 1 | 50% | Regime gate worked; ATR crisis unusable; BFSI combined display broken |
| **Reliance** | Conglomerate | 4 | 1 | 1 | 67% | **Zero ENTRY_ZONE across 6 dates** — STRONG-PULLBACK structurally misaligned |
| **Infosys** | IT services / secular growth | 4 | 1 | 1 | 67% | Regime gate worked; COVID V-shape missed (+155% / 12m foregone) |
| **Tata Steel** | Commodity cyclical | 1 | 2 | 3 | 17% | **Cyclical inversion in TA confirmed**; Cycle B compounds Cycle A failure |
| **ITC** | Defensive consumer staple | 5 | 1 | 0 | 83% | Pipeline caught Jun-2022 re-rating (+46% excess) — v0.1 ideal case |
| **Maruti Suzuki** | Auto cyclical | 2 | 4 | 0 | 33% | Cyclical defended on relative basis; DI-flip is leading indicator |
| **Total** | — | **19** | **11** | **6** | **53%** | — |

### Pattern by stock profile

| Profile | Stocks | Pattern |
|---|---|---|
| **Defensive / Quality non-cyclical** | ITC, Infosys, HDFC Bank | v0.1 works well overall (4–5 GOOD / 6). Regime gate is the MVP. Single failure mode = V-shape recovery miss. |
| **Commodity / Auto cyclical** | Tata Steel, Maruti | v0.1 is **structurally broken** for this profile (1–2 GOOD / 6). Regime gate inverts at troughs. Same root failure as Cycle A's W3 Piotroski inversion. |
| **Conglomerate** | Reliance | v0.1 is **functionally inert** — never fires ENTRY_ZONE. Cross-sectional ROC ranking + multi-segment regime make STRONG-PULLBACK setup impossible to satisfy. |

---

## The 7 weaknesses — in depth

### B-W1 — Cyclical inversion in TA domain (mirrors Cycle A's W3)

**What happened (Tata Steel, Maruti at 2008-10 and 2020-03)**:
- At commodity-cycle and economic-cycle troughs, the 40-week SMA is necessarily below price (because price has been falling for months/quarters into the trough).
- The 4-week BEAR→BULL hysteresis ensures the gate stays in BEAR mode for 4+ more weeks after the actual bottom prints.
- Combined: cyclicals get AVOID_ENTRY at the moment they're cheapest. Tata Steel Oct-2008 forward 24m = +400%; Mar-2020 forward 24m = +344%. Both blocked.
- This is **structurally identical** to Cycle A's W3 (Piotroski high at peak, low at trough). The mechanism is different (level-of-price vs. YoY-change-in-fundamentals) but the failure mode is the same: trailing signals on a mean-reverting underlying.

**The cross-cycle implication**:
- At Mar-2020 Tata Steel: Cycle A = WATCH (F=5/9 was already low); Cycle B = AVOID_ENTRY. §10 conflict-resolution rule defaults to "more conservative" → AVOID_ENTRY.
- Pure Cycle A alone would have produced WATCH (softer caution, leaving the door open).
- **Adding Cycle B made the combined system more restrictive at the best entry of the decade.**
- The §10 display rule assumes Cycle A and Cycle B are independent. **They are not at cyclical extremes** — both are trailing the same underlying commodity-price-cycle driver.

**For v0.2**: REGIME-OVERRIDE hook (already a placeholder in v0.1 §3.4) must be implemented. Trigger conditions to specify: combination of FA-deterioration that's reached a stable bottom + valuation-mean-reversion-ready + cycle-position indicator (capacity utilization, margin-vs-10yr-median, etc.). This is fundamentally a **Cycle F problem** (signal combination), not solvable in TA alone.

### B-W2 — Lagging regime gate misses V-shape recoveries

**What happened (Infosys, HDFC, Maruti, Reliance at Mar-2020)**:
- COVID crash was a V-shape — sharp drop in Feb-Mar 2020, sharp recovery from late Mar 2020 onwards.
- 40-week SMA gate took 4 weeks to flip from BEAR→BULL after the actual bottom.
- CIRCUIT-RECENT filter (§0.2) suppressed signals for 5+ days after each circuit hit. Multiple stocks hit circuits in mid-March.
- Combined: most stocks had no ENTRY_ZONE signal until mid-May 2020 — by which point Infosys had already rallied ~30% off the low.
- Forward 12m returns missed: Infosys +155% missed; HDFC +85% missed; Maruti +90% missed (relative underperformed NIFTY but absolute positive).

**Why this is hard**:
- A faster regime gate (1-week confirmation instead of 4) would fix V-shapes but introduce whipsaw on normal corrections.
- The fundamental tradeoff: a regime gate optimized for U-shape recessions can't be optimal for V-shape recoveries.
- Two-track approach (separate fast + slow gates) was deferred to v0.2 by all 4 affected agents.

**For v0.2**: Asymmetric hysteresis — BULL→BEAR remains 4-week (slow, avoid whipsaw on corrections); BEAR→BULL becomes 1–2 weeks if accompanied by ADX expansion AND volume confirmation. OR: macro-event tag table (COVID-2020, GFC-2008, demonetization-2016, etc.) where regime gate is suspended in favor of a "macro-crisis-bottom" override.

### B-W3 — Conglomerate ENTRY_ZONE never fires

**What happened (Reliance at all 6 dates)**:
- Reliance's business is Refining + Petchem + Telecom Jio + Retail — four very different sub-businesses with different demand cycles.
- The stock's price reflects a weighted average of these — but the 26-week ROC compares this weighted average against single-business NIFTY 100 peers.
- During sector-specific rallies (banks in 2014, IT in 2020-22, capex in 2022-24), Reliance's ROC ranks mid-quintile because none of its sub-businesses lead the specific rally.
- STRONG-PULLBACK setup requires top-quintile ROC. Reliance never satisfies it.
- ENTRY-PULLBACK setup requires MOMENTUM-MID + RSI in 40-50 pullback zone — Reliance does qualify on ROC, but MACD histogram + Bollinger position rarely line up due to event-driven repricing (Jio launch, Rights Issues, strategic investments).
- Net: 0 / 6 ENTRY_ZONE signals.

**For v0.2**: Business-segment regime tagging for conglomerates — compute ROC against a custom peer set (e.g., 50% Energy + 30% Telecom + 20% Retail for Reliance) rather than cross-sectional NIFTY 100. Or: lower STRONG-PULLBACK ROC threshold from top-quintile to top-tercile for conglomerate-tagged stocks.

### B-W4 — NIFTY 100 cross-sectional ROC disadvantages off-theme stocks

**What happened (Reliance, ITC, Maruti)**:
- ITC during 2014-2022 ESG overhang: never in top quintile of NIFTY 100 ROC (correctly avoided ENTRY_ZONE — this is a "good" example of the same mechanism).
- ITC at Jun-2022 (re-rating start): jumped to mid-quintile, MOMENTUM-MID. Pipeline correctly gave ENTRY_ZONE via the ENTRY-PULLBACK path.
- But: at later dates when broader bull resumed (2023-24), ITC's relative ROC dropped again even as absolute price rose — pipeline correctly downgraded.
- The mechanism works **only for stocks where absolute price and relative-vs-NIFTY-100 are correlated**. Breaks for sector-rotation periods and theme-driven names.

**For v0.2**: Add sector-relative ROC (rank within NSE Sector) alongside the NIFTY 100 cross-sectional ROC. Use higher of the two for momentum classification. This was deferred to Cycle B v0.3 in §11 of the math spec; B.4 evidence promotes it to v0.2.

### B-W5 — ATR stop unusable in crisis volatility

**What happened (HDFC Bank at Mar-2020, multiple agents flagged)**:
- ATR(14) weekly at Mar-2020 = ₹100+ for HDFC Bank (price ~₹770 split-adjusted).
- 2.5 × ATR = ₹250 below entry → stop at ₹520.
- Stop distance = 32% below entry. Even a "successful" trade with 50% recovery in 6 months would have crossed the stop on the way up if there was any volatility (which COVID-recovery had).
- Generalized: in crisis volatility regimes (VIX > 35), ATR-based stops produce risk-budget math that's mathematically reasonable but practically unusable.

**For v0.2**: Cap stop-distance at max(2.5 × ATR, 15% of price) → use the MIN. Equivalent: position-size cap based on max acceptable stop distance, not min acceptable. This was not anticipated in v0.1 — it's a NEW failure mode.

### B-W6 — BFSI combined display §10 completely non-functional

**What happened (HDFC Bank at all 6 dates)**:
- Cycle A v0.3 still treats HDFC Bank as SKIPPED-BFSI (BFSI stub is just NIM/GNPA/PCR/CAR trends, no formal FA label).
- §10 of Cycle B math says "if Cycle A label is X and Cycle B label is Y, then..."
- For HDFC Bank: Cycle A label is "BFSI-MONITOR" (effectively N/A). §10's 4×4 conflict matrix doesn't have a row/column for this.
- v0.1's combined-display logic is **untestable** for the largest sector in NIFTY 100 by market cap.

**For v0.2**: Add an explicit "BFSI-MONITOR" row to the §10 conflict matrix. Decide whether to use the BFSI trend indicators (NIM/GNPA/PCR/CAR direction) as a proxy for HOLD/WATCH/REVIEW labels. **OR**: accelerate Cycle A's v0.4-candidate "full BFSI FA pipeline" so HDFC, ICICI, Kotak, SBI, Bajaj Finance can get real Cycle A labels. This is a known limitation flagged in v0.4 problem statement §8.

### B-W7 — Structural-event distortion of regime gate

**What happened (HDFC Bank merger Jul-2023; Reliance Jio launch Sep-2016)**:
- HDFC Bank merged with parent HDFC Ltd in Jul-2023. The merged-entity stock has different fundamentals from pre-merger HDFC Bank. The 40-week SMA computed across this date is "mixed" — pre-merger price + post-merger price.
- Reliance Jio launch in Sep-2016 changed the business mix materially. Forward ROC after Sep-2016 reflects Jio's contribution, not pre-Jio Reliance.
- v0.1 has no mechanism to annotate or adjust for structural corporate events.

**For v0.2**: Manual annotation table for material corporate events (mergers, demergers, divestitures, large strategic investments). When 40-week SMA crosses an event date, flag `STRUCTURAL-EVENT-CAUTION` in the output and downgrade conviction. This is the TA-side equivalent of Cycle A's ACQUISITION-YEAR addition to the Regime-Shift Calendar in v0.3.

---

## What v0.1 math DID get right (consensus across agents)

1. **The 40-week SMA regime gate is the dominant signal for defensive / quality non-cyclical names.** ITC, Infosys, HDFC Bank all show the gate working as intended. Multi-year BEAR regimes correctly identified. Bull-regime ENTRY_ZONE candidates correctly surfaced. The architecture is sound for the median NIFTY 100 stock.

2. **The pipeline structure (pre-screen → regime → trend strength → volatility → momentum → confirmation → sizing → label) is logically coherent.** Same finding as Cycle A.4 — the issue is the contents of each box, not the composition order.

3. **ITC Jun-2022 ENTRY_ZONE is the v0.1 ideal case.** Multi-year underperformance correctly avoided; re-rating inflection correctly caught; forward 12m +46% excess vs NIFTY 100 with stop never hit. This is what v0.1 was designed to do, and it does it.

4. **CIRCUIT-RECENT pre-screen worked for downside protection.** Multiple stocks hit circuits in Mar-2020; pre-screen correctly suppressed false ENTRY_ZONE signals during the early V-shape that would later have been failed by deeper crash. Side effect: blocked the eventual recovery entry (see B-W2).

5. **+DI/-DI directional check from §4.3 is a leading indicator** (B-P1 above). Currently only a downgrade modifier; agent evidence (Maruti Sep-2018) shows it's stronger than that.

6. **The label set (ENTRY_ZONE full/half / WAIT / AVOID_ENTRY / EXIT_WARNING) maps cleanly to the test cases.** No fundamental reshape needed; only the routing into the labels needs work.

---

## What v0.1 math fundamentally cannot see (acknowledged blindspots)

| Blindspot | Should be handled in |
|---|---|
| Cyclical position (where are we in the commodity / economic cycle?) | Cycle F (signal combination with FA), not solvable in TA alone |
| V-shape vs U-shape recovery distinction | Cycle B v0.2 (asymmetric hysteresis or macro-event override) |
| Conglomerate sub-business mix | Cycle B v0.2 (business-segment regime tagging) |
| Structural corporate events (mergers, demergers, strategic investments) | Cycle B v0.2 (manual annotation table) |
| Sector-rotation regimes (theme-driven outperformance) | Cycle B v0.2 (sector-relative ROC supplement) |
| BFSI fundamental state | Cycle A v0.4+ (full BFSI FA pipeline) |
| Government / regulatory event shocks | Out of scope; manual overlay |
| FII / DII positioning data | Out of scope (Cycle D may revisit) |

---

## Implications for B.5 (multi-agent critique)

The critique should ideally include lenses for:

1. **Quant** — focus on B-W1 (cyclical inversion mechanism), B-W3 (conglomerate STRONG-PULLBACK overspecification), parameter sensitivity across thresholds (40-week vs 26-week SMA; ADX 20 vs 25; ROC quintile cutoffs).
2. **Behavioral** — focus on B-W2 (V-shape recovery miss = "feeling sidelined at the bottom" behavioral cost), B-W5 (ATR stop unusable = "stops are not stops" credibility cost), the 4-label structure.
3. **Retail-NSE** — focus on B-W6 (BFSI gap when ~30% of retail portfolios are HDFC/ICICI/Bajaj), B-W7 (mergers/demergers/Jio-style events are common in NIFTY 100), liquidity-tier interaction across Nifty 50 vs Nifty Next 50.
4. **Signal-engineer** — focus on B-W2 (asymmetric hysteresis design), B-P1 (DI-flip promotion), walk-forward Sharpe-readiness of the 7 indicators given B.4 hit rate (53% GOOD is not Sharpe > 0.3 — that's a separate empirical test).
5. **Cross-cycle integration** (NEW lens for Cycle B) — focus on B-W1's cross-cycle compounding finding; the §10 conflict matrix structural soundness; whether Cycle B can add information conditional on Cycle A label, or whether the two need joint math (Cycle F).

---

## Implications for v0.2 math (Cycle B B.6 refinement)

Concrete proposed changes for v0.2, prioritized:

### P0 — Cannot ship v0.2 without

**P0.1 — REGIME-OVERRIDE hook implementation** (§3.4 placeholder activated)
Trigger conditions for activating REGIME-OVERRIDE on a stock currently in REGIME=BEAR:
- Cycle A label indicates fundamental valuation-mean-reversion candidate (specific labels TBD with Cycle F)
- Stock is in CYCLICAL sector tag (from Cycle A v0.3 §9.1) AND has been in BEAR regime for ≥ 12 weeks
- ADX dropping below 15 (indicating trend exhaustion, not deteriorating trend)
When triggered: allow ENTRY_ZONE generation despite BEAR regime; annotate `REGIME-OVERRIDE-ACTIVE` in output; reduce position size by 50% (half conviction).
Raised by: Tata Steel, Maruti (both cyclical inversion). Critical for cyclicals.

**P0.2 — Asymmetric hysteresis (BULL→BEAR vs BEAR→BULL)**
Current: 4-week confirmation both directions.
Proposed v0.2:
- BULL→BEAR: keep 4-week (avoid whipsaw on routine corrections)
- BEAR→BULL: shorten to 1-2 weeks IF accompanied by (a) ADX rising AND (b) volume in current week > 1.5× 13-week avg
Raised by: 4 of 6 stocks (Infosys, HDFC, Maruti, Reliance) — V-shape recovery miss.

**P0.3 — ATR stop cap (max 15% of price)**
Stop distance = MIN(2.5 × ATR_14_weekly, 0.15 × entry_price). Whichever is closer. Position size recalculates accordingly.
Raised by: HDFC Bank canonical; all stocks at Mar-2020 affected.

**P0.4 — DI-flip as standalone leading signal** (promote from §4.3 downgrade flag)
Add new entry trigger: if regime is BULL and ADX < 20 and -DI > +DI for 2 consecutive weeks → EXIT_WARNING for held positions; AVOID_ENTRY for not-held.
Add new exit-of-bear signal: if regime is BEAR and ADX < 15 and +DI > -DI for 2 consecutive weeks → REGIME-OVERRIDE candidate (combined with P0.1).
Raised by: Maruti Sep-2018 canonical. The strongest positive finding from B.4.

### P1 — Strong desirables (3+ stocks)

**P1.1 — Sector-relative ROC supplement** (was v0.3 deferral; promoted to v0.2)
Compute both NIFTY 100 cross-sectional ROC quintile AND NSE Sector cross-sectional ROC quintile. Use MAX of the two for momentum classification. Annotate which one drove the classification.
Raised by: Reliance, ITC, Maruti.

**P1.2 — Structural-event annotation table**
Manual lookup table for material corporate events: mergers (HDFC-HDFC Ltd 2023), demergers (Reliance Jio Financial 2023), large strategic investments (Reliance Jio launch 2016), large divestitures, business model changes. When 40-week SMA window includes such an event: flag `STRUCTURAL-EVENT-CAUTION` and downgrade conviction.
Raised by: HDFC Bank, Reliance.

**P1.3 — Conglomerate STRONG-PULLBACK adjustment**
For stocks tagged CONGLOMERATE (revenue concentration < 60% in any single sector): lower STRONG-PULLBACK ROC requirement from top-quintile to top-tercile.
Raised by: Reliance (canonical — zero ENTRY_ZONE without this).

**P1.4 — BFSI conflict-matrix completion** (links to Cycle A v0.4 candidate)
Add BFSI-MONITOR row/column to §10 conflict matrix with explicit resolution rules. As interim until full BFSI FA pipeline arrives: use BFSI trend indicators (NIM improving / stable / deteriorating; GNPA same; CAR same) as proxy for HOLD/WATCH/REVIEW.
Raised by: HDFC Bank (canonical). High priority because BFSI is 30%+ of NIFTY 100 by market cap.

### P2 — Single-stock or specialist findings

**P2.1 — Macro-event override table** (alternative form of P0.2)
Pre-defined macro-crisis bottoms (GFC Mar-2009; demonetization Nov-2016; COVID Mar-2020; future): suspend regime gate; switch to short-window momentum + volume-confirmation for ENTRY_ZONE generation.
Raised by: Infosys, HDFC, Maruti at Mar-2020.

**P2.2 — Liquidity-tier-aware slippage in stop calculation**
For Nifty Next 50 names: increase stop-distance slippage allowance vs Nifty 50.
Raised by: Cycle B research §4.6.

**P2.3 — Dividend yield floor for sizing** (defensive bias)
For stocks with dividend yield > 4%: scale up position size by 25% (recognizes margin of safety from yield).
Raised by: ITC.

**P2.4 — Thematic-overhang manual annotation**
For stocks under known thematic pressure (ITC ESG, tobacco; PSU regulatory overhang; large pharma price-control): annotate with confidence downgrade until thematic resolves.
Raised by: ITC 2014-2022 underperformance.

### Open question for Pranav (B.6 idea-review)

The B-W6 finding (BFSI combined display §10 non-functional) directly intersects with Cycle A v0.4 candidate V3 (full BFSI FA pipeline). Does B-W6 escalate V3's priority? If yes, B.6 may produce a v0.5 problem-statement update (vs v0.4 from Cycle A — would put us at v0.5).

---

## File map of Cycle B artifacts so far

| File | Purpose | Status |
|---|---|---|
| `20_cycle_B_research.md` | B.1 research (TA survey + shortlist) | Locked |
| `21_cycle_B_math_v0.1.md` | B.3 v0.1 math spec | Locked (historical) |
| `22_cycle_B_test_v0.1_HDFCBank.md` | B.4 test on HDFC Bank | Locked |
| `22_cycle_B_test_v0.1_Reliance.md` | B.4 test on Reliance | Locked |
| `22_cycle_B_test_v0.1_Infosys.md` | B.4 test on Infosys | Locked |
| `22_cycle_B_test_v0.1_TataSteel.md` | B.4 test on Tata Steel | Locked |
| `22_cycle_B_test_v0.1_ITC.md` | B.4 test on ITC | Locked |
| `22_cycle_B_test_v0.1_MarutiSuzuki.md` | B.4 test on Maruti | Locked |
| **`23_cycle_B_test_synthesis_v0.1.md`** | This file | Final for v0.1 |
| Next: `24_cycle_B_critiques_v0.1.md` | B.5 multi-agent critique synthesis | Pending |
| Next: `25_cycle_B_math_v0.2.md` | B.6 refined math | Pending |
