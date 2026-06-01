# 24e — Cycle B: Critic C5 (Cross-Cycle Integration), v0.1 Critique

**Critic**: C5 — Cross-Cycle Integration (NEW for Cycle B)
**Status**: Final for B.5
**Date**: 2026-05-31
**Scope**: How Cycle A (FA) and Cycle B (TA) math interact — §10 conflict matrix, B-W1 compounding finding, holding-period dominance rules, BFSI propagation, conflict entropy, and the Cycle F boundary.

---

## §1 Verdict on §10's Design

**REFACTOR-REQUIRED.**

One-line: §10 is a display rule wearing the clothes of a resolution rule, and in the one case where a real resolution was needed — B-W1's Mar-2020 Tata Steel — it made the combined system worse than Cycle A alone.

The core problem is not complexity but assumption. §10.4 explicitly calls itself a "display rule — not a math combination." That is honest and appropriate. But the default conflict-resolution embedded inside it (§10.3: "default to the more conservative label") IS math — it is a min() function over the two label orderings — and it is wrong in a systematic, identifiable direction: it over-penalizes cyclicals at exactly the moment they should be upgraded.

Beyond Tata Steel, the 4×4 matrix has structural holes (BFSI is not a row/column, PSU status is not a row/column) and a flawed cell-level narrative ("Agree: positive entry" for [HOLD × ENTRY_ZONE] understates the number of conditions that must simultaneously hold for that agreement to be reliable).

§10 was the right design for v0.1 — it correctly deferred math combination to Cycle F and correctly surfaced conflict in parallel. But v0.1's own B.4 test data now shows what a "display + conservative default" costs: one lost best-entry-of-the-decade on Tata Steel is computable evidence, not theoretical.

---

## §2 Per-Weakness Cross-Cycle Assessment

### B-W1 — Cyclical inversion in TA domain (cross-cycle lens)

This is the most significant finding from a cross-cycle perspective. The synthesis document correctly identifies the mechanism: at Mar-2020 Tata Steel, Cycle A = WATCH and Cycle B = AVOID_ENTRY. §10.3's conservative default takes the minimum → AVOID_ENTRY.

The deeper problem the synthesis identifies but does not fully develop: **Cycle A's WATCH and Cycle B's AVOID_ENTRY are not independent observations**. Both are downstream of the same cause — trailing signals on a mean-reverting, commodity-cycle-driven stock. Cycle A's F-Score is low because trailing fundamentals lag the cycle (W3 in Cycle A.4). Cycle B's regime gate is BEAR because the 40-week SMA follows price with a lag. Neither cycle is adding new information relative to the other at this date; they are both reading the same trailing signal through different lenses.

This has a precise implication for §10: the "agree vs conflict" taxonomy is incomplete. §10 implicitly assumes the two labels are drawn from independent processes, so "both say avoid" is stronger than either alone. But if they share a common driver, the correct interpretation is: "two lagging-indicator systems both flagging the same trailing deterioration — correlation ≠ confirmation." At cyclical extremes, the matrix's "Agree: cautious wait" cell [WATCH × WAIT] and the "Agree: avoid" cell [REVIEW × AVOID_ENTRY] are often describing a single underlying signal twice, not two independent signals confirming each other.

**This is not fixable in §10.** It requires Cycle F's signal-combination math to estimate the conditional correlation between Cycle A and Cycle B outputs given the stock's sector tag and cycle position.

**Cross-cycle severity**: Critical. The B-W1 compounding finding turns a question of timing (Cycle B's regime lag) into a question of system integrity: adding Cycle B can make portfolio outcomes worse than Cycle A alone on the highest-return opportunities.

### B-W6 — BFSI combined display §10 completely non-functional

This is the most acute operational gap from a cross-cycle lens. The §10 matrix has four rows: HOLD, WATCH, REVIEW, FLAG. HDFC Bank — and by extension ICICI Bank, Kotak, SBI, Bajaj Finance, LIC Housing Finance — enters as neither. "BFSI-MONITOR" is not a row. The combined-display logic is untestable for roughly 30% of NIFTY 100 by market cap.

The v0.4 problem statement added the BFSI staging sentence in §8, and the synthesis doc (B.4) correctly flags this as B-W6 requiring a BFSI-MONITOR row. But the framing in the synthesis underspecifies what goes in that row. There are three distinct situations that BFSI-MONITOR could represent:

1. NIM improving + GNPA falling + CAR stable → directional health improving (closer to WATCH or HOLD trajectory)
2. NIM stable + GNPA flat + CAR OK → neutral, no direction (truly a "monitor" — neither positive nor negative)
3. NIM compressing + GNPA rising + CAR tightening → directional deterioration (closer to REVIEW trajectory)

These three situations produce different resolution rules with Cycle B's output. Situation 1 paired with ENTRY_ZONE is very different from Situation 3 paired with ENTRY_ZONE. A flat BFSI-MONITOR row in the matrix treats all three the same.

The synthesis's interim fix — "use NIM/GNPA/CAR direction as proxy for HOLD/WATCH/REVIEW" — is the right direction, but it requires formalizing which combination of NIM/GNPA/CAR directions maps to which Cycle A label equivalent. That mapping does not currently exist in any document.

**Cross-cycle severity**: High. Not fixable without either (a) formalizing BFSI trend → label mapping, or (b) accelerating the full BFSI FA pipeline to v0.4 of Cycle A. The v0.4 problem statement already names V3 as a candidate; B-W6 confirms it should not remain optional.

### B-W2 — Lagging regime gate (cross-cycle lens)

In isolation this is a Cycle B problem: the 4-week BEAR→BULL hysteresis misses V-shape recoveries. From a cross-cycle perspective, the question is: does Cycle A provide an early signal that would have allowed the combined system to catch the COVID V-shape?

Looking at Tata Steel and HDFC Bank at Mar-2020 through the Cycle A lens: Cycle A would have produced WATCH (F=5, fundamentals not deteriorating but not improving) — not REVIEW or FLAG. This means the Cycle A label at Mar-2020 was already pointing toward "keep monitoring," not "exit." If §10 had a rule that [WATCH × AVOID_ENTRY] or [HOLD × AVOID_ENTRY] escalated to "check regime gate timing" rather than defaulting to AVOID_ENTRY, it would have flagged the lag.

But §10 does not have such a rule. It does not distinguish between AVOID_ENTRY-due-to-REGIME-BEAR and AVOID_ENTRY-due-to-WEAK-MOMENTUM. These are different situations with different Cycle A implications. REGIME-BEAR AVOID_ENTRY at a stock where Cycle A says WATCH is a candidate for the asymmetric hysteresis override. WEAK-MOMENTUM AVOID_ENTRY at a stock where Cycle A says WATCH is not — the FA confirmation is soft. The sub-reason behind AVOID_ENTRY matters for cross-cycle resolution, and §10 does not surface it.

**Cross-cycle severity**: Medium. The fix (asymmetric hysteresis, P0.2) is primarily a Cycle B concern. But the cross-cycle framing adds a new requirement: §10 must propagate the Cycle B sub-reason label, not just the top-level output label, into the conflict matrix reasoning.

### B-P1 — REGIME-DI-CONFLICT as leading indicator (cross-cycle lens)

The positive finding is interesting from a cross-cycle perspective. The +DI/-DI flip catching the Sep-2018 NBFC directional change before the regime gate broke is essentially a "TA early warning" that Cycle A's quarterly-update cadence would have missed. Cycle A's NIM and GNPA data for NBFC-adjacent names (HDFC Bank, Bajaj Finance) would not have updated until the next quarterly result.

This creates an asymmetry in the combined display that §10 doesn't address: Cycle B's leading indicator (DI-flip) has a roughly 4–8 week informational lead over Cycle A for macro-event directional changes. If the combined display is timing-naive — showing both labels as of the same evaluation date without acknowledging that Cycle A's label is based on the last quarterly report while Cycle B's is computed on the latest price action — users may underweight the TA signal in exactly the case where it has the most value.

**Cross-cycle severity**: Low-Medium. The leading vs lagging nature of the two cycles is not addressed anywhere in v0.1 and is not addressed in the synthesis's proposed v0.2 changes. It belongs in §10's framing even if the full math is Cycle F work.

---

## §3 NEW Cross-Cycle Integration Concerns

### CC-1 — Signal independence is assumed, never tested

§10 builds its 4×4 matrix on an implicit assumption: that a given Cycle A label and a given Cycle B label occurring together carries more information than either alone. This is only true if the two labels are not strongly correlated. B-W1 demonstrates that for cyclical stocks at extremes, this independence fails — both cycles are trailing the same commodity-price driver.

The real question is: across the full 36-cell test (6 stocks × 6 dates), how often do Cycle A and Cycle B agree vs conflict, and is the agreement rate different for cyclicals vs defensives?

From B.4 test data (reading across the synthesis): ITC, Infosys, and HDFC Bank represent the defensive/quality profile. For these three stocks, Cycle B's regime gate and momentum signals tend to align with Cycle A's label direction. For Tata Steel and Maruti (cyclical), the B.4 results show the misalignment. A rough count from the synthesis:

- Defensive/quality profile (18 cells: 3 stocks × 6 dates): Cycle A and B likely agree in 12–14 of 18 cells (HDFC Bank's BFSI exception makes the count imprecise). Estimated agree rate: ~70–80%.
- Cyclical profile (12 cells: 2 stocks × 6 dates): based on Tata Steel's 3/6 WRONG verdicts and Maruti's pattern of misalignment, estimated agree rate: ~30–40%.
- Conglomerate (6 cells: Reliance): Cycle B is inert (0 ENTRY_ZONE), making agreement rate measurement degenerate.

The aggregate agree rate is not a single number — it is strongly sector-conditional. This has a direct implication for §10: the default conservative rule is calibrated (implicitly) for a 50% agree rate. For defensives, the matrix is mostly redundant — they agree ~75% of the time, and the conflicts that do arise are typically [HOLD × EXIT_WARNING] or [WATCH × WAIT] which are low-stakes. For cyclicals, the matrix's "agree = more confident" interpretation is wrong in both directions: it over-penalizes at troughs (both trailing) and potentially over-rewards at peaks (both following the same peak signal).

**v0.2 implication**: The §10 matrix should have a sector-tag dimension. A row labeled "cyclical-context: conservative-default suspended when both cycles trail same commodity signal" is the right design direction, even if the full math is Cycle F.

### CC-2 — The holding-period dominance rule (§10.3) is ambiguous at the margin

§10.3 states: "Long-term (B1): Cycle A dominates. Tactical (B2): Cycle B dominates." This reads cleanly in the abstract but collapses on contact with an actual decision.

Every investment decision is simultaneously B1 and B2. The user is not choosing between "hold this for 5 years" or "swing-trade this for 8 weeks." They are asking: "given that my thesis is B1, what's the right tactical entry this week?" In that framing, B2 (entry timing) is a sub-problem of B1 (thesis validation), and it's not clear which label "dominates."

Consider the concrete case: Tata Steel, Cycle A = WATCH, Cycle B = ENTRY_ZONE (hypothetical, were the regime gate not blocking). Cycle A says: "fundamentals are not great but not deteriorating; watch for improvement." Cycle B says: "price action suggests entry timing is good now." §10.3 says for new-position decisions, "default to the more conservative label." So the user should WATCH and not enter. But this is exactly the situation where value investors make their best entries — the thesis isn't confirmed yet by FA, but price action is suggesting the turn is coming.

The rule as written defaults to FA dominance for new-position decisions. This is defensible but it should be stated as an explicit design choice, not implied by "more conservative." The risk is that users who read §10.3 interpret it as: "FA always overrides TA unless you've already entered." That reading would make the tactical entry-timing purpose of Cycle B nearly useless.

**Sharper rule needed**: "New position decision: Cycle A must be WATCH or better (not REVIEW or FLAG). If Cycle A is WATCH and Cycle B is ENTRY_ZONE, this is a half-conviction entry — Cycle A provides thesis validation at minimum threshold; Cycle B provides entry timing. Cycle A REVIEW + Cycle B ENTRY_ZONE is a WAIT regardless of conviction modifier — the thesis is not intact."

This is more specific than §10.3's current language and directly addresses the "when does B2 actually override B1?" question.

### CC-3 — PSU stocks are invisible to the cross-cycle matrix

Cycle A v0.3's PSU sub-pipeline outputs PSU-CONTEXT annotations alongside a modified action label. The v0.3 pipeline for PSU stocks uses a partial sub-pipeline + PSU-CONTEXT annotations (per §3 of Cycle A v0.3). However, §10's conflict matrix has no PSU row/column — the same gap as BFSI, but for a different reason.

BFSI is excluded because the FA pipeline cannot produce a real label (BFSI-MONITOR is a stub). PSU stocks do get a real Cycle A label (HOLD/WATCH/REVIEW/FLAG) but it carries a PSU-CONTEXT modifier that changes its interpretation. A PSU stock rated WATCH with PSU-CONTEXT has different cross-cycle implications than a private-sector stock rated WATCH. Specifically: PSU stocks are subject to government capex cycles, disinvestment overhang, and regulatory direction-setting — none of which are visible in either FA or TA signals. The combined display for a PSU should carry a PSU-CONTEXT annotation that explains this, but §10 does not pass PSU-CONTEXT through the conflict matrix.

This is a smaller gap than BFSI (PSU stocks do get a real Cycle A label) but it means the §10 display for PSU names is misleading in a specific way: the "Agree: positive entry" cell for [HOLD × ENTRY_ZONE] on a PSU looks identical to the same cell for a private-sector compounder, even though the information content is different.

**v0.2 implication**: §10's output string should propagate Cycle A's PSU-CONTEXT annotation into the combined display. This is a one-line addition to the display logic, not a matrix redesign.

### CC-4 — No mechanism to express "Cycle A and B agree but with low combined confidence"

§10's display logic has three resolution tiers: Agree, Mild conflict, Strong conflict. It does not have a confidence dimension on the Agree tier. "HOLD + ENTRY_ZONE = Agree: positive entry" is treated the same whether Cycle A's HOLD came from F-Score 8/9 with all gates clean and Cycle B's ENTRY_ZONE came from full-conviction ADX 35 + top-quintile ROC, or from F-Score 5/9 with several borderline signals and Cycle B's ENTRY_ZONE from half-conviction LIGHT-ADX routing.

From a decision-theoretic standpoint, these are very different situations. The first is a high-conviction entry; the second is a tenuous double-confirmation where both cycles barely crossed their thresholds.

Both Cycle A (data-quality completeness score) and Cycle B (full vs half conviction modifier) have internal confidence signals that are not propagated into §10's combined display. A combined-confidence output would simply be: "Both cycles signal positive entry. Cycle A confidence: [HIGH/MED/LOW from data-quality score]. Cycle B conviction: [full/half]." This requires no new math — just propagation of existing fields.

**v0.2 implication**: Add combined-confidence propagation to §10's display output. Specifically: surface Cycle A's data-quality score tier and Cycle B's conviction modifier in the combined reasoning string for all Agree cells. This is a display change only, fits within v0.2 scope.

### CC-5 — Cycle B v0.2 scope implications for the v0.4 problem statement

The synthesis asks whether B-W6 (BFSI non-functional in §10) escalates the V3 candidate (full BFSI FA pipeline) to require a v0.5 problem statement update. The cross-cycle view adds a further consideration: the v0.4 problem statement §8 says the full BFSI sub-pipeline is "scheduled for v0.3" of Cycle A. But at the current pace (Cycle A closed at v0.3, Cycle B now in B.5), there is no Cycle A v0.4 on the immediate roadmap. Cycle B v0.2 will close and Cycle C will begin. The full BFSI pipeline is deferred indefinitely within the sequential cycle structure.

Meanwhile, §10's BFSI gap means the combined display — which was the point of Q5 in the locked decisions ("surface TA/FA conflicts explicitly") — cannot be exercised for any BFSI name. For a portfolio that mirrors NIFTY 100, this means the most prominent feature of the combined system is inoperative for the names that matter most to a retail investor's portfolio (HDFC Bank, ICICI Bank, SBI, Bajaj Finance typically represent 20–35% of a NIFTY 100-weighted retail portfolio).

This is a genuine problem-statement tension, not just a roadmap sequencing note. The v0.4 problem statement says "no silent skips on banking/NBFC/insurance/other-financial-services names in real-portfolio output." But the v0.1 combined-display math is currently a silent skip for those names — it has nothing to say.

A v0.5 problem statement update is warranted if the BFSI FA pipeline accelerates to a Cycle A v0.4 mini-iteration before Cycle C begins. Whether Pranav wants to do that is a sequencing decision, but the cross-cycle critique confirms the gap is product-material, not just math-completeness.

---

## §4 What §10 Got Right

**The Q5 contract is correctly implemented.** The locked decision at Q5 was: "LLM never silently picks; always surfaces conflict." §10's parallel display rule with explicit conflict markers is the correct implementation of that contract. It is architecturally right: defer math combination to Cycle F, surface both labels now. v0.1's §10 does not violate Q5 — it implements it at the appropriate level of sophistication for v0.1.

**The §10.4 scope note is admirably honest.** Calling §10 a "display rule" and explicitly naming Cycle F as the owner of combination math is correct. No other section of the v0.1 math spec overstates what v0.1 can do; §10.4 continues that discipline.

**The three-tier conflict classification (Agree / Mild / Strong) is the right qualitative structure.** The insight that [FLAG × ENTRY_ZONE] is categorically different from [WATCH × WAIT] is correct and worth preserving in v0.2. The labels may need refinement, but the notion of graduated conflict severity is sound.

**The holding-period framing (B1 vs B2)** is the right conceptual axis for conflict resolution. The specific rules need sharpening (per CC-2 above), but the fundamental question — "are you in this as a long-term thesis or is this a tactical entry?" — is the right question to ask at a conflict.

**The §10.1 matrix is parseable and complete at face value.** 16 cells, explicit narratives, consistent labeling. For the stocks where §10 can actually be exercised (non-BFSI, non-PSU, non-cyclical-extreme), the matrix is a reasonable first pass.

---

## §5 Prioritized v0.2 Changes

### P0 — Required for §10 to be functional at all

**P0.A — BFSI-MONITOR formalization into §10 (links to B-W6)**

Add a BFSI-MONITOR sub-row to §10's conflict matrix. The sub-row must distinguish three BFSI trend states:
- BFSI-IMPROVING (NIM rising OR GNPA falling AND CAR stable): treat as WATCH-equivalent for matrix resolution purposes
- BFSI-STABLE (all indicators stable, no direction): treat as WATCH-equivalent with lower weight
- BFSI-DETERIORATING (NIM compressing OR GNPA rising OR CAR tightening): treat as REVIEW-equivalent

Map these to resolution rules with Cycle B's four labels. Specifically: [BFSI-DETERIORATING × ENTRY_ZONE] must be explicitly Strong-conflict, not silently defaulted to conservative. The sub-reason of BFSI deterioration matters for a user holding HDFC Bank or ICICI Bank.

This is a v0.2 deliverable. The interim solution (NIM/GNPA/CAR directional proxy) is the right approach; the gap is that the mapping has never been formally specified.

**P0.B — Sector-tag propagation into §10's conservative default**

The conservative default in §10.3 must be suspended for stocks tagged CYCLICAL in Cycle A (§9.1 of Cycle A v0.3) when Cycle B's AVOID_ENTRY sub-reason is REGIME-BEAR and Cycle A's label is WATCH (not REVIEW or FLAG). This specific combination — [WATCH × AVOID_ENTRY: REGIME-BEAR, CYCLICAL stock] — should produce an explicit annotation "CYCLICAL-TROUGH-CANDIDATE: both cycles may be trailing same commodity-cycle signal. Conservative default suspended. See Cycle F for joint analysis when available." With HALF-CONVICTION entry allowed at user discretion.

This does not fix B-W1 (that is Cycle F work) but stops the combined system from actively making things worse than Cycle A alone.

### P1 — Strong desirables

**P1.A — Combined-confidence propagation in Agree cells (per CC-4)**

Surface Cycle A data-quality score tier and Cycle B conviction modifier in the Agree-cell reasoning string. No new math required — just field propagation in the display logic.

**P1.B — PSU-CONTEXT annotation passthrough (per CC-3)**

Propagate Cycle A's PSU-CONTEXT annotation into the §10 combined display string for all PSU-tagged stocks. One display-logic addition.

**P1.C — Sub-reason label propagation into conflict matrix (per B-W2 cross-cycle lens)**

§10 should display the sub-reason of AVOID_ENTRY (REGIME-BEAR vs WEAK-MOMENTUM vs SQUEEZE-BROKE-DOWN) in the conflict row, not just the top-level AVOID_ENTRY label. A user whose Cycle A says WATCH should be told whether Cycle B's AVOID_ENTRY is about price regime (potentially a lagging signal in cyclicals) or about momentum (a different situation).

**P1.D — Sharpen B1/B2 dominance rule (per CC-2)**

Replace §10.3's "default to the more conservative label" for new-position decisions with:
- Cycle A must be WATCH or better for any new-position ENTRY_ZONE to proceed
- [WATCH × ENTRY_ZONE] = half-conviction entry (B2 timing within B1 thesis watch)
- [HOLD × ENTRY_ZONE] = full-conviction entry (B2 timing with B1 thesis confirmed)
- [REVIEW or FLAG × ENTRY_ZONE] = WAIT regardless of B2 conviction (thesis not intact)
- The sentence "Cycle A dominates long-term; Cycle B dominates tactical" is kept as context but the above rules operationalize it

### P2 — Single-topic or deferrable

**P2.A — Leading vs lagging timing note in §10.3 (per B-P1 cross-cycle framing)**

Add a note: "Cycle B signals are computed weekly on the latest price data. Cycle A labels reflect the most recent quarterly report. When a material TA directional change (DI-flip, regime transition) occurs within 4–8 weeks of the next scheduled quarterly result, the Cycle A label may not yet reflect the fundamental shift. Weight Cycle B's leading indicator accordingly."

---

## §6 Cycle F Preview — What §10 Cannot Do

§10 is a display-and-default rule. Cycle F replaces the "default" part with actual math. The following is what that math must do, organized by what §10 currently fails at.

### F.1 — Signal independence estimation

Cycle F must compute, for each (stock, date) evaluation, an estimate of the correlation between the Cycle A signal driver and the Cycle B signal driver. For commodity cyclicals, both signals are driven by the same trailing commodity-price input; their correlation is high. For defensive quality compounders, the FA signal (earnings quality, leverage trends) and the TA signal (price regime, momentum) are driven by largely independent processes; correlation is lower.

The math: a conditional correlation matrix on Cycle A output changes and Cycle B output changes, conditioned on sector tag and trailing-12-month commodity-index direction (for cyclicals) or broad-market-regime direction (for defensives). This requires historical data across 100+ stocks over 10+ years to estimate reliably — it is not a Cycle B v0.2 deliverable.

The implication: when estimated correlation is high, the combined confidence of two "Agree" signals is less than each signal alone would suggest (they are saying the same thing). When correlation is low, agreement genuinely increases confidence. §10's flat treatment of all "Agree" cells as uniformly confirmatory is the exact error this corrects.

### F.2 — Bayesian update framework

The proper structure for combining Cycle A and Cycle B into a single composite is a Bayesian update. Cycle A provides a prior probability on the stock's fundamental quality (expressed as P(quality | FA signals)). Cycle B updates this prior with price-action evidence: P(entry appropriate | quality prior, TA signals).

For this to work, Cycle A and B labels must be mapped to probability distributions, not categorical labels. [HOLD] is not the same as "definitely quality" — it has a confidence distribution. Cycle F must specify:
- Prior distribution on fundamental quality → posterior after FA signals
- Likelihood function for TA signals given fundamental state
- Posterior entry-appropriateness probability

This is not a minor extension of §10; it is a fundamentally different architecture. §10's categorical label + conservative default is a zero-math approximation of Bayesian combination. It works when priors are strong and the two signals are independent. It fails when priors are uncertain (cyclical WATCH) and the signals are correlated (both trailing same commodity driver).

### F.3 — Cyclical-position overlay

Neither Cycle A nor Cycle B has a direct measure of "where are we in the commodity/economic cycle?" Cycle A's cyclical normalization (5-yr window, N7) tries to neutralize the cycle's effect on the F-Score. Cycle B's regime gate follows price, which itself follows the cycle with a lag.

Cycle F must introduce a direct cycle-position signal, separate from both FA and TA. Candidates:
- For commodity cyclicals: capacity utilization data (Steel Authority, JSW, Tata Steel all publish quarterly), sector margin vs 10-year median, commodity-index level vs trailing average
- For credit/BFSI cyclicals: credit growth rate (RBI data), system NPA level, yield curve shape
- For auto cyclicals: industry volume growth (SIAM monthly), fleet age distribution

This cycle-position signal is neither FA nor TA — it is a macro/sector-level input that conditions how both Cycle A and Cycle B outputs should be interpreted. In the absence of it, both cycles will systematically fire the wrong label at cycle troughs, and combining them makes this worse.

### F.4 — Behavioral correction layer

Q5 in the locked decisions states that the LLM should "prompt the user with their holding period as context and ask for a weight decision" when signals conflict. Cycle F's math should inform this prompt with a question-specific framing: "These two cycles are likely expressing correlated information given [stock's sector] and [current cycle position]. The conflict may be less informative than it appears. Historical resolution rate for [WATCH × AVOID_ENTRY] on cyclical stocks at cycle troughs: X% correct, Y% false signal. Suggested action: defer entry by one quarter and reassess Cycle A label after next quarterly result."

This is behavioral + probabilistic framing in one. The probability estimates come from F.1 (historical signal-correlation analysis). The behavioral framing is the Q5 contract. Neither is in §10.

### F.5 — Explicit scope: what remains in §10 after Cycle F arrives

Even after Cycle F is implemented, §10's display rule is not redundant. It serves two purposes that a probabilistic combination score cannot:
1. **Auditability**: the user sees both individual cycle labels and can challenge the combination. A score of 0.72 "entry confidence" tells the user nothing about whether the FA is HOLD or WATCH, or whether the TA regime is BULL or BEAR.
2. **Override capacity**: the user should always be able to override the combined score by adjusting their holding-period weight (B1 vs B2 weight slider, per Q5's "context-sensitive prompt"). This requires seeing both components.

§10's display rule should be preserved in Cycle F as the transparency layer alongside the combination math, not replaced by it.

---

**End of C5 cross-cycle integration critique.**
`✅ Cross-cycle integration critique complete. §1–§6 written; 6 sections, 7 cross-cycle concerns addressed (B-W1, B-W6, B-W2, B-P1 + CC-1 through CC-5), 4+5+2 v0.2 changes recommended (P0 × 2, P1 × 4, P2 × 1), Cycle F preview covers 5 required capabilities (F.1–F.5).`
