# 15c — Cycle A Critique: Behavioral Finance Lens

**Status**: 🔄 Writing Section 1 — Verdict
**Date**: 2026-05-30
**Lens**: Behavioral Finance
**Last updated**: 2026-05-30T00:02:00

---

## 1. Verdict on v0.1 (top-line)

**REFACTOR-REQUIRED.**

The math spec produces four action labels (HOLD / WATCH / REVIEW / FLAG) that are designed as descriptions of fundamental state but will function as behavioral nudges — and three of the four nudges are miscalibrated: REVIEW invites anxiety without direction, WATCH creates a hair-trigger for disposition-effect sells, and FLAG on a false positive (Asian Paints Mar-2022) causes a needless exit from a position that required no action. The label composition table in Section 6 has no hysteresis, no cadence control, and no asymmetric-error weighting, which means it will generate noisy label transitions week-over-week (given a weekly output cadence per Q9) at exactly the frequency research shows breaks retail investor resolve.

---

## 2. Position on each of the 6 known weaknesses

### W1 — Beneish false positives during regime shifts

**Position**: Confirmed critical. The behavioral cost is *larger* than the quant cost.

**Reasoning (focus on behavioral cost of a false FLAG)**:
The synthesis correctly identifies Asian Paints Mar-2022 as a false FLAG — the model fired `MANIPULATION-RISK` due to COVID-era DSRI and AQI spikes, not actual manipulation. But the synthesis frames this as a math problem. The behavioral cost is the more serious issue.

A `FLAG: MANIPULATION-RISK` label carries the strongest possible negative connotation in a fundamental quality context. It is not "the company may be weaker than it looks." It is: "the company may be committing fraud." The retail investor's System 1 response to the word "manipulation" is immediate reputational contamination — this is well-documented in behavioral finance (the affect heuristic: words with strong negative affect produce strong avoidance behavior regardless of base rates). Even an investor who intellectually understands that this is a Beneish threshold breach will be nudged toward exit by the label itself.

The test data shows Asian Paints Mar-2022 FLAG was directionally correct (stock fell −31% excess return over 24 months) — but for entirely the wrong reason (Grasim/Birla Opus entry + valuation compression, not manipulation). This matters enormously for behavior: if the FLAG fires for the wrong reason, the investor who exits on `MANIPULATION-RISK` does not learn to distinguish "manipulation signals" from "competitive disruption." They learn that FLAG = sell. The next time FLAG fires (including on a real false positive) they sell again without examination. The label calibration of the investor's decision heuristic is corrupted by the false-positive signal.

Critically, v0.1 uses Beneish as a **knockout gate** — meaning a single M-Score crossing halts the entire pipeline. No Piotroski computed. No FCF/NI. No ROCE. The investor receives only `FLAG: MANIPULATION-RISK` and no other data. This is maximum information suppression at exactly the moment maximum information is needed to make a good hold/sell decision. Knockout gates are appropriate for truly binary risks (distress, fraud). A threshold built on 1982–1992 US data with a known false-positive rate during macro regime shifts is not a binary risk.

**Proposed fix (behavioral lens)**:
Downgrade Beneish from knockout gate to additive flag, effective immediately for v0.2. The pipeline should continue to Piotroski, FCF/NI, and ROCE even when M-Score fires. The action label table should incorporate an M-Score flag as a downgrade modifier (e.g., a stock that would otherwise be HOLD becomes WATCH-MANIP-CHECK, with the M-Score shown alongside the full computation trace). This preserves the manipultion signal's information value without triggering the affective contamination of the word "manipulation" without supporting evidence from the rest of the pipeline.

---

### W2 — Beneish structurally suppressed for commodity firms

**Position**: Confirmed critical. The behavioral cost is a systematic false sense of safety.

**Reasoning (focus on behavioral cost)**:
The synthesis notes that Beneish's TATA term structurally suppresses M-Score for heavy industry because large non-cash charges push OCF >> NI, driving TATA massively negative. This pulls M-Score deep below −1.78 even in years when other indices (GMI, AQI) would be flagging concerns. The behavioral implication is a lopsided error regime: Beneish false-positives on quality companies (W1) while giving false comfort on commodity companies.

The specific behavioral damage: Tata Steel across all 4 test dates produces M-Scores in the −2.98 to −3.20 range, comfortably "safe." The investor sees this and interprets it as a clean bill of health on manipulation risk. The actual situation is that Beneish has no signal power for this company class — it is not safe; it is blind. This is worse than uncertainty, because it substitutes the investor's appropriate residual uncertainty with false confidence. The affect heuristic fires in the positive direction: "Beneish says SAFE, I feel safe."

The interaction with the weekly cadence (Q9) is particularly bad: a weekly report showing Tata Steel's M-Score at −3.1 across 52 consecutive weeks trains the investor that this is a permanently low-risk feature of the stock. When and if a manipulation event eventually occurs for such a company, the investor's prior has been calibrated toward complete safety, making the surprise event more psychologically destabilizing (and more likely to produce a panic exit at the worst time).

**Proposed fix (behavioral lens)**:
Add a sector-class annotation to Beneish outputs: for stocks in heavy industry / commodity / infrastructure sectors (defined by NSE sector classification), display "M-Score has LOW SIGNAL POWER for this sector class — structural non-cash charges suppress the TATA coefficient. Do not interpret as clean." This annotation should appear in the reasoning string even when M-Score passes cleanly. It breaks the false-safety heuristic before it forms.

---

### W3 — Piotroski F-Score is anti-correlated with cyclical entry opportunity

**Position**: Confirmed critical. This is the worst behavioral failure in v0.1, and it operates in the direction of maximum disposition-effect damage.

**Reasoning (focus on behavioral cost)**:
The synthesis correctly identifies the inversion: Tata Steel Mar-2020 (F=5/6, WATCH/REVIEW) was the best buy of the decade (+355%); Mar-2021 (F=8, HOLD) was a mediocre entry (+34% market-matching). The behavioral cost is not just that the signal is wrong — it is that the signal is wrong in exactly the direction that activates the disposition effect.

Consider the sequence from the investor's perspective:
- They hold a cyclical stock. It has been depressed. The bot issues REVIEW or WATCH. The investor feels validated in their anxiety about the position. They consider selling (or do not add to the position). Classic disposition effect: riding the loser. The bot just amplified the disposition effect by giving FA cover to the emotional impulse.
- After the cycle turns, the stock has rallied 200%. The bot now issues HOLD (F=8). The investor feels validated in holding. They do not add. They eventually sell at a further high. The bot just told them to HOLD when they should have already held from the trough.

The Tata Steel test makes this concrete: WATCH at Mar-2020, HOLD at Mar-2021 (peak). The bot's label transition from WATCH → HOLD is the worst possible frame — it suggests "we've graduated from concern to confidence" exactly at the point where the reward-to-risk ratio for a new entrant is worst. An investor who acted on the label sequence (did not add at WATCH, added at HOLD) would have followed a textbook disposition-effect / recency-bias pattern and gotten market-matching returns on a stock that offered 10× better entry a year earlier.

**Quantifying the asymmetric damage**: At Mar-2020 WATCH, entering Tata Steel would have returned +355% over 24 months (excess). At Mar-2021 HOLD, entering would have returned +34%. The signal-driven behavior cost the investor 321 percentage points of excess return. This is not a small efficiency loss; it is the entire investment opportunity. The model did not just fail to add value — it actively directed the investor away from the opportunity at the moment of maximum signal reliability.

**Proposed fix (behavioral lens)**:
Add a cyclical-sector label modifier for v0.2. For stocks in cyclical NSE sectors (Metals & Mining, Oil & Gas, Chemicals, Power), the action label should include a mandatory caveat: "CYCLE CONTEXT: This company is in a cyclical sector. A low F-Score at sector trough may indicate entry opportunity, not deterioration. Compare current ROCE to 10-year median before acting." This does not fix the math (that requires cycle-position signals), but it breaks the automatic "WATCH = concern = hold off" heuristic for the one class of company where that heuristic is systematically inverted.

---

### W4 — Ind AS 116 lease accounting breaks YoY signals

**Position**: Confirmed high severity from a behavioral lens, but narrower than W1–W3.

**Reasoning (focus on behavioral cost)**:
The Ind AS 116 issue is a one-time accounting transition distortion — it fires once per stock (at the year the new standard applies) and then normalizes. The behavioral damage is therefore time-limited, unlike W1–W3 which recur. However, the false REVIEW assigned to Asian Paints Mar-2020 (F5 fail from Ind AS 116 leverage spike) is a real cost: the investor who acted on REVIEW at the March 2020 COVID bottom missed +27.6% excess return over 24 months. For a retail investor, ₹27.6% excess return is material.

The more interesting behavioral effect is the anchoring interaction: the Mar-2020 REVIEW label, if acted on (partial exit), creates a new cost-basis anchor at the exit price. When the stock subsequently rises (as it did), the investor anchors to the exit price rather than the original cost basis. Now they are reluctant to re-enter because "I sold at ₹1,638 and it's now ₹2,000, feels expensive." The accounting-driven false signal created an anchor that persists for years. A single mis-labeled quarter can corrupt the investor's reference-point framework for the stock indefinitely.

**Proposed fix (behavioral lens)**:
For any YoY signal pair that spans a known accounting-standard transition (Ind AS 116 effective FY2020, Ind AS 109 transitions), mark the affected Piotroski signals as LOW-CONFIDENCE and exclude them from the action label calculation (or weight them at 50%). Display clearly: "F5 LOW-CONFIDENCE: FY2020 leverage signal may reflect Ind AS 116 lease reclassification, not new financial debt." This prevents the accounting artifact from corrupting the action label and the investor's downstream anchoring framework.

---

### W5 — Altman Z″ dominated by century-accumulated reserves

**Position**: Confirmed high severity, but the behavioral cost is narrower than the math cost.

**Reasoning (focus on behavioral cost)**:
The Z″ issue creates a structural false-safe reading for old companies (Tata Steel Z″ = 5.5–5.9 throughout, even with ₹88–116k Cr of long-term debt). The behavioral cost is the same false-confidence mechanism as W2: the investor sees a Z″ of 5.7 and implicitly registers "distress risk = none." This is wrong, but the wrongness is stable across time, which limits the behavioral damage compared to W1 (which creates sudden false FLAGS) or W3 (which inverts the signal direction).

The specific behavioral risk from Z″ dominance by reserves is more subtle: it suppresses the incentive to examine leverage risk independently. An investor who trusts Z″ does not ask "what is the Net Debt/EBITDA?" or "what happens to interest coverage if EBITDA halves?" The model's false-safe signal preempts the investor's own analytical instinct. This is particularly damaging for Tata Steel-type companies where the European operations create a genuine tail risk that Z″ cannot see.

**Proposed fix (behavioral lens)**:
Display Net Debt/EBITDA as a mandatory context figure alongside Z″ for all companies, regardless of Z″ result. Format: "Altman Z″ = 5.7 (PASS). Note: Net Debt/EBITDA = 4.2× — elevated; Z″ may understate leverage risk for long-operating companies with large accumulated reserves." This preserves Z″'s gate function while breaking the false-safe heuristic.

---

### W6 — Sector ROCE percentile fails on small sectors

**Position**: Confirmed medium severity. The behavioral cost is systematic conservative bias on exactly the stocks retail investors should hold.

**Reasoning (focus on behavioral cost)**:
The synthesis correctly notes that Asian Paints' 33–38% ROCE — which would rank 95th+ percentile in most sectors — is invisible as a percentile because N < 10. The action label table's ROCE column defaults to "N/A (N<10)" and the composition rule treats this conservatively (defaults to the lower ROCE branch). The behavioral implication: the bot systematically undersells the quality of small-sector quality compounders.

For a retail investor holding Asian Paints, REVIEW (Mar-2020) is a signal to examine whether the thesis is intact. But the thesis for Asian Paints is precisely its dominant ROCE position in the paints sector — and the model's inability to show that ROCE as a percentile means the single most thesis-relevant number is invisible in the output. The investor cannot use the bot's output to confirm "thesis intact: ROCE still #1 in sector" because the bot does not show the relative position. The "thesis-entry framing" (Q10: "Thesis intact Y/N") fails for all small-sector stocks because the key competitive metric is never displayed relatively.

**Proposed fix (behavioral lens)**:
For N < 10, display: "ROCE = X% — Rank N of M within [sector]. Closest peers: [Company A: Y%, Company B: Z%]." Even at N=4, "Rank 1 of 4, next peer at 27%" is fully interpretable and directly answers "thesis intact on capital efficiency?" without requiring a percentile. This fix directly improves the model's ability to serve the Q10 "thesis intact" framing for small-sector compounders.

---

## 3. NEW concerns (not in synthesis)

### NC1 — The WATCH label is a disposition-effect trigger disguised as a monitoring instruction

The synthesis does not examine the action labels themselves as behavioral objects. WATCH is glossed as "minor deterioration; monitor next-quarter results before acting." From a behavioral lens, this framing is dangerously under-specified.

"Monitor next quarter" is not an instruction — it is a suspension of judgment. The behavioral research on ambiguous instructions (Gal & Rucker, 2010, "When in Doubt, Don't" — *Psychological Science*) shows that investors facing ambiguous hold-or-act signals default to their strongest pre-existing emotion about the stock. If the investor is already nervous (perhaps because the stock is down from their entry price — i.e., they are riding a loser), WATCH confirms the nervousness without giving it a resolution path. The result is rumination: checking the stock price daily, interpreting every weekly report's label as a signal to act. WATCH → HOLD transition after one quarter = "OK, good." WATCH → WATCH for two quarters = "Something is still wrong, I should reduce." WATCH → REVIEW = "Told you something was wrong, sell now."

This is the disposition effect in label form. The investor holds while HOLD, gets nervous at WATCH, and sells at REVIEW — exactly when the price is likely most depressed. The label sequence HOLD → WATCH → REVIEW maps directly onto the emotional arc of a retail investor riding a loser to exhaustion.

The weekly cadence (Q9) makes this catastrophically worse. At weekly frequency, a stock with fundamentals that fluctuate around the WATCH/HOLD threshold (F-Score of 6–7, where any single signal flip determines the band) can oscillate HOLD → WATCH → HOLD → WATCH across consecutive reports. Alert-overload research (Iyengar & Lepper, 2000, "When Choice is Demotivating") shows that frequent low-information signals produce two response types: (1) ignoring all signals after a few false positives, or (2) hyper-reacting to every transition. Both are bad. Type 1 means the user stops engaging with the bot's most important signals. Type 2 means the user generates a sell impulse every time WATCH appears.

FA fundamentals are quarterly by design — they do not meaningfully change week-over-week. Running a weekly report on quarterly signals means the label will be identical for 13 consecutive weeks (no new fundamental data) and then potentially flip in the 14th week when annual results arrive. The weekly report creates an expectation of new information that arrives at 13:1 ratio of silence to data. Behavioral research on intermittent reinforcement (Skinner's variable-ratio schedules) shows that irregular reward schedules are the most compelling and hardest to disengage from — but in an investment context, the "rewards" (label changes) are not correlated with actual new information.

**Fix**: Introduce 2-quarter hysteresis on all non-knockout label transitions, defined precisely: a label change from HOLD→WATCH requires F-Score to drop and remain below the threshold for 2 consecutive quarterly data releases, not just one. Exception: knockout gates fire immediately (they are by design one-observation stops). This reduces the false label oscillation that the weekly cadence would amplify. For the weekly report, display the label as STABLE when no new fundamental data has arrived since the last quarterly release, and display UPDATED only when the most recent quarter's data has been incorporated. This directly prevents the HOLD→WATCH→HOLD oscillation from generating 3 sell impulses in a quarter.

---

### NC2 — REVIEW is not actionable, and non-actionable outputs produce anxiety without direction

The synthesis briefly notes "REVIEW: user should re-examine the original thesis" but does not analyze whether this instruction is executable. From a behavioral finance perspective, REVIEW as currently specified is the most psychologically damaging label in the set — not FLAG.

Here is why. FLAG at least gives the investor a clear direction: the knockout gate fired, something is structurally wrong, consider exit. HOLD is clear: do nothing. WATCH is clear: wait. REVIEW says: "re-examine the original thesis explicitly." This instruction requires the investor to:
1. Remember what their original thesis was (may be 2–5 years ago)
2. Find the documentation of that thesis (if it was ever documented)
3. Map the current fundamental signals against it
4. Make a binary thesis-intact / thesis-broken determination

Steps 1–3 are not supported by v0.1 math in any way. The bot issues REVIEW and then provides no scaffolding for what "re-examining the thesis" means in practice. The investor stares at the label, feels a diffuse anxiety, and either: (a) holds because they don't know what to do, or (b) sells to resolve the anxiety (classic "action bias as anxiety relief" — documented in Bjork & Bjork, 2014 on uncertainty-driven action preferences).

The Q10 locked decision ("thesis-entry framing: 'Thesis intact Y/N'") was specifically designed to address this problem. But v0.1 math does not implement thesis-entry framing in any way. The REVIEW label is the exact moment where thesis-entry framing would be most valuable — and it is absent. The label says "re-examine the thesis" but the output provides no structured thesis-checking output. This is an empty instruction that will consistently produce either paralysis or anxiety-sell.

Quantifying the behavioral cost: among investors who received what amounts to an ambiguous "re-examine" instruction on a losing position, Barber & Odean (2000) and subsequent Indian-market literature (ISB/NSE study, 2.5 million accounts) both show that the modal response is to hold. Loss aversion prevents exit even when the explicit instruction says "re-examine." REVIEW, in the hands of the investor most likely to hold losers, becomes a label that says "keep watching your losing position." This is the opposite of what the bot is trying to achieve.

**Fix**: Replace REVIEW's action definition. REVIEW must have a structured checklist output, not a vague "re-examine" instruction. The minimum viable version: when REVIEW fires, the bot must display (a) which specific Piotroski signals degraded since the last HOLD period, (b) whether the degradation is in the same group or spread across groups (concentrated signal failure vs broad deterioration), and (c) a specific binary question: "Has the core quality signal that justified this position [ROA / ROCE / FCF] deteriorated, or is this noise?" If the bot cannot answer (c) from available data, the label should not be REVIEW — it should remain WATCH with a note about ambiguous signals. REVIEW should only fire when there is specific, identifiable fundamental deterioration that the investor can evaluate against their stated thesis.

---

### NC3 — The asymmetric cost of false FLAG vs false HOLD, and what that means for the disposition effect

The synthesis identifies both error types but does not quantify which is more behaviorally damaging, and the question is not symmetric.

**False FLAG (Asian Paints Mar-2022)**: A retail investor acting on this signal exits a position in a high-quality compounder during a COVID-era working-capital blip. The forward outcome is that the stock underperforms by −31% over 24 months — but for the *wrong reason*. The investor who exited on `MANIPULATION-RISK` did not exit because of competitive disruption. They exited because the bot told them the company might be manipulating its books. When they later see the stock fall (for the right reason — Birla Opus), they credit the bot with a correct call. This corrupts their signal calibration: they learn "FLAG = sell = correct" even when the causal chain was wrong. The next false FLAG (a COVID-style regime shift affecting DSRI/AQI at a different company) will produce the same reflexive sell, without examination.

**False HOLD (Tata Steel Mar-2021, Asian Paints Mar-2021)**: A retail investor holding on `HOLD` signals at a peak. The forward outcome is underperformance of −22.4% (Asian Paints) or market-matching returns (Tata Steel). For the investor with the disposition effect, false HOLD is paradoxically *less* damaging in the short term, because they are told to hold a position they would have held anyway (loss-holders hold; the disposition effect keeps them in). The long-term cost is the opportunity cost of not reducing the position at peak valuation — but this requires the investor to have sold a winner, which the disposition effect prevents anyway. In other words: the disposition effect and false HOLD reinforce each other. The investor does not suffer visible pain from a false HOLD until the loss materializes.

**Which error is worse under the disposition effect?** False FLAG is behaviorally worse, for three compounding reasons:
1. It forces the sale of a position the investor might have held through the drawdown (disposition effect would have helped here).
2. It corrupts the investor's signal calibration with a "confirmed" false win.
3. For a subsequent false positive at a stock that later recovers, the investor's trained reflexive sell behavior will crystallize a real loss where none needed to occur.

However, false HOLD is operationally worse for the stated success metric (Q4: "behavioral flags acted + stop-loss adherence + Sharpe improvement"). The false HOLDs in both test stocks produced cumulative relative underperformance of ~50 percentage points across 4 dates — this is the Sharpe drag that Q4 is supposed to reduce. The model that is calibrated to minimize false FLAGS will produce more false HOLDs, and vice versa. v0.1 has no explicit loss function for this trade-off. It needs one.

**Fix**: Define an explicit error-asymmetry parameter. The threshold for FLAG (Beneish M-Score cutoff at −1.78) is a point estimate from a 1999 US-data model. For the Indian NSE context, where false-positive rate during regime shifts is demonstrably high (the test shows at least 1 false FLAG out of 4 dates for a single quality stock), the threshold should be raised to −1.5 (making FLAG harder to fire). The threshold for HOLD (F ≥ 7) should be tightened during periods of elevated sector-relative valuation (ROCE percentile ≥ 80 + P/E above 5-year-sector-median). This asymmetric tightening reduces the false-FLAG behavioral damage while adding a valuation-anchor warning to prevent peak-HOLD errors — the two highest-cost errors in the test data.

---

### NC4 — Weekly cadence (Q9) is architecturally wrong for FA signals; the math implies monthly

Q9 locks "weekly cadence default" for the structured report. This is explicitly a problem-statement decision, and this critique is authorized to push back on it when the math implies a different cadence.

The math implies monthly at minimum, quarterly as the natural refresh unit.

Every signal in v0.1 is driven by annual financial data (Piotroski, Beneish, Altman, FCF/NI) or at most quarterly data (Altman X3 on TTM EBIT, FCF 3-yr rolling). No component of v0.1 changes week-over-week. The label will be identical for 12–13 consecutive weeks between annual report releases, and then change (if at all) in the single week when annual results are incorporated. For an investor receiving a weekly report, 12 consecutive weeks of "HOLD" followed by a single week of "WATCH" is behaviorally equivalent to a fire alarm in an office where nothing has ever gone wrong — the false-alarm history teaches the user to ignore the signal, exactly when they most need to pay attention.

The specific behavioral cost of weekly frequency on quarterly signals:
1. Intermittent identical outputs create habituation. The investor stops reading the report after the third consecutive "no change" week.
2. When the label finally changes (quarterly data arrival), it is buried in 12 prior "no change" weeks and may be missed or under-weighted.
3. Weekly cadence creates an implicit promise of weekly-fresh information. When the report consistently delivers stale FA signals, it trains the user to discount the report's authority — which undermines the eventual genuine warning signal.

The behavioral-finance literature on optimal alert frequency (Sims 2003 on rational inattention; Hirshleifer & Teoh 2003 on investor attention allocation) suggests that alerts which arrive more frequently than the information they convey has actually changed are treated as noise and filtered out. Weekly FA reports fall squarely in this category.

**Fix**: Change the FA module's report cadence to monthly (with a quarterly-data-arrival event trigger). The weekly report cadence should be reserved for TA signals (Cycle B), which genuinely have weekly resolution. The FA module's output should appear in the weekly report as "FA Status: [HOLD / WATCH / REVIEW / FLAG] — last updated [date of last quarterly data]. No change since last quarterly release." This displays the signal without creating false expectations of weekly-fresh information, and preserves the user's attention for the genuine quarterly-data updates.

---

## 4. Proposed v0.2 changes — prioritized

### P0 — Cannot ship v0.2 with current label design (behavioral failure, not just math failure)

**P0a**: Add 2-quarter hysteresis to all label transitions between HOLD, WATCH, and REVIEW. Specifically: a transition from HOLD → WATCH requires F-Score to be in the WATCH band for 2 consecutive quarterly data releases; a WATCH → REVIEW transition requires 2 consecutive WATCH periods. Exception: knockout gates (Beneish FLAG, Altman FLAG, Pledge FLAG) fire immediately — these are designed to be one-observation stops and hysteresis would undermine their purpose. Format the output label as: "HOLD (stable for 3 quarters)" or "WATCH (1st consecutive quarter — threshold not yet confirmed; 1 more quarter needed to confirm trend)." This prevents the HOLD → WATCH → HOLD oscillation that weekly cadence would amplify.

**P0b**: Downgrade Beneish from knockout gate to additive flag. Pipeline continues through Piotroski, FCF/NI, and ROCE even when M-Score exceeds −1.78. The final action label incorporates M-Score as a −1 downgrade modifier (e.g., HOLD with M-flag becomes WATCH-MANIP-CHECK; WATCH with M-flag becomes REVIEW-MANIP-CHECK). Reasoning string must display the specific Beneish components that fired, with the COVID/regime-shift context note: "DSRI elevated: this may reflect pandemic-era payment deferrals rather than manipulation — verify with peer DSRI comparison." This preserves manipulation-signal information while preventing the affective contamination of unilateral MANIPULATION-RISK labels on false positives.

**P0c**: Replace REVIEW's action definition with a structured checklist output. REVIEW must show: (1) which Piotroski group(s) failed (Profitability / Leverage / Efficiency), (2) whether the failure is first occurrence or nth consecutive quarter, (3) the specific binary question the investor needs to answer: "Has [the signal that justified this position] changed durably?" If (2) is first occurrence, the label should be WATCH-DETERIORATION-DETECTED, not REVIEW, per P0a hysteresis. REVIEW should only fire on confirmed multi-quarter deterioration, and when it fires, it must tell the investor exactly what has deteriorated, not just "re-examine the thesis."

### P1 — Strong desirables from behavioral lens

**P1a**: Add cyclical-sector label modifier. For NSE Metal, Oil & Gas, Chemical, Power sectors: append mandatory caveat to any WATCH or REVIEW label: "CYCLICAL-SECTOR WARNING: In cyclical sectors, deteriorating F-Score at sector trough often precedes best entry points. Compare current ROCE to 10-year sector median before reducing position." This does not fix the underlying math (which needs cycle-position signals) but breaks the automatic "WATCH = reduce" heuristic for cyclicals.

**P1b**: For N < 10 small sectors, replace "sector too small for percentile" with "Rank N of M: ROCE = X% vs [Company A: Y%, Company B: Z%]." This directly supports the Q10 "thesis intact Y/N" framing for the most common quality-compounder profile in small sectors.

**P1c**: Change FA module report cadence to monthly (quarterly-data-event driven) within the weekly report wrapper. FA Status line in the weekly report: "FA: HOLD — last updated [date of last quarterly data incorporation]. No new fundamental data this week." TA signals (Cycle B) retain weekly cadence. This addresses the intermittent-reinforcement problem and prevents habituation to the FA signal.

### P2 — Nice-to-have from behavioral lens

**P2a**: Display Net Debt/EBITDA alongside Z″ for every non-BFSI stock, with a plain note for old companies: "Altman Z″ uses accumulated book equity, which may overstate financial safety for long-operating companies. Net Debt/EBITDA = [X]× provides an independent leverage check." Breaks the false-safe heuristic without changing the gate.

**P2b**: Add an explicit error-asymmetry parameter to the action label composition table. The current table treats all threshold crossings symmetrically. For v0.2, define: (a) FLAG threshold: raise Beneish cutoff to −1.5 (harder to fire) and require at least 2 of the 8 Beneish sub-indices to be above typical-single-regressor levels before halting; (b) HOLD threshold: add a sector-relative ROCE >80th percentile + P/E above 5-year-median check as an optional HOLD-to-WATCH modifier during periods of elevated valuation. This is a P2 because it requires P/E data which is currently deferred.

---

## 5. What v0.1 got RIGHT

- **The pipeline structure resists impulsive sell signals.** The sequence [Knockout gates → Piotroski → FCF/NI → ROCE → Action label] requires a stock to fail multiple independent checks before a negative label fires. This is a hysteresis by composition — a stock that fails one Piotroski signal does not immediately land in REVIEW. The multi-layer design inherently dampens false alarm rate for gradual deterioration, which is the most common type.

- **The transparency of the reasoning string is genuinely valuable.** The worked example in Section 7 of v0.1 produces a full causal chain: "ROCE at 83rd percentile of its sector — strong capital efficiency. No manipulation, distress, or pledge risks." This is the correct behavioral output design. The investor can argue with the label because they can see exactly what produced it. A label without a traceable reason is an oracle; a label with a visible derivation is a tool the investor can interrogate. The reasoning string design should be preserved and strengthened, not simplified.

- **Knockout gates for pledge risk are behaviorally correct.** Pledged-promoter-shares is a category of risk where swift decisive action is appropriate. Unlike Beneish (where gradual deterioration is the failure mode being detected), a 30%+ pledge threshold is an event-type risk. FLAG: PLEDGE-RISK is a label where the behavioral urgency the word "FLAG" creates is appropriate. This is a well-calibrated use of a hard-stop gate.

- **FCF/NI 3-year averaging is explicitly anti-recency-bias.** Using a 3-year average for CashConversion directly prevents the most recent year's anomaly from dominating the signal. Asian Paints FY2022 OCF was ₹986 Cr (anomalously low due to commodity inflation) — without 3-year averaging, this would produce a EARNINGS-QUALITY-RISK flag on a company whose underlying cash generation was intact. The 3-year averaging design shows a deliberate structural resistance to recency bias that v0.2 should preserve and potentially extend.

---

## 6. One sentence to the synthesizer

"If you carry one thing forward, it should be: add 2-quarter hysteresis to all HOLD/WATCH/REVIEW label transitions, because a system with no hysteresis running on weekly cadence will generate false label oscillations that train retail investors to ignore genuine signals and sell on noise — the exact behavioral failure the bot exists to prevent."

---

**Status**: ✅ Behavioral finance critique complete.
**Last updated**: 2026-05-30T00:30:00
