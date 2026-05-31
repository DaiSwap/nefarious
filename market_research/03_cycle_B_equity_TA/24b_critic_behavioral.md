# 24b — Cycle B Critique: Behavioral Finance Lens

**Status**: Complete
**Date**: 2026-05-31
**Cycle**: B.5 multi-agent critique of v0.1 TA math
**Lens**: Behavioral Finance — how Pranav (experienced Indian retail investor) will actually interpret and act on v0.1 outputs when making B1 (long-term hold) and B2 (entry timing) decisions.
**Source files read**: `21_cycle_B_math_v0.1.md`, `23_cycle_B_test_synthesis_v0.1.md`
**Format reference**: `15c_critic_behavioral.md` (Cycle A.5 behavioral critic)

---

## 1. Verdict

**REFACTOR-REQUIRED.**

The v0.1 math is technically coherent but behaviorally miscalibrated in two structural ways that can exceed the quant failures in real-world damage. First: the system will be held responsible for every high-profile miss at the bottom of a V-shape, and a handful of those misses (Infosys +155% foregone, HDFC Bank +85% foregone at Mar-2020) will permanently damage trust in a way that is disproportionate to the signal's overall accuracy. Second: the stop-loss math produces numbers that retail intuition will either ignore or follow in ways that make it worse than not having a stop at all. A system that generates correct labels but unusable stops, and that gets the two most emotionally salient moments (recovery entries and stop decisions) behaviorally wrong, will be abandoned — or, worse, selectively used in the worst possible way.

The label architecture is recoverable. The stop design needs a hard cap before v0.2 ships.

---

## 2. Per-weakness analysis (behavioral lens)

### B-W1 — Cyclical inversion in TA domain

**Position**: CONFIRM, with an important behavioral extension the synthesis understates.

The synthesis correctly identifies that the regime gate fires AVOID_ENTRY at commodity-cycle troughs (Tata Steel Oct-2008 blocked, Mar-2020 blocked), and that this compounds Cycle A's W3 Piotroski inversion rather than correcting it. The behavioral extension the synthesis does not address: this compounding produces a specific and very damaging interaction with Pranav's existing mental model.

When a retail investor holds a cyclical stock through a trough (which the disposition effect ensures they often do — they won't sell the loser), they are typically in a state of anxious holding: "I should hold through the cycle, but I'm not sure." They look to the bot for permission to hold conviction or permission to add. The bot gives neither — Cycle A says WATCH, Cycle B says AVOID_ENTRY, §10 combines them to "more conservative = AVOID_ENTRY." The investor receives a label that says, in effect: "don't buy more of this thing you're already holding." This is psychologically incoherent with holding the existing position. It will produce one of two behaviors: (a) the investor ignores the bot entirely for cyclicals (correct, but now the bot has no utility for 20–25% of a NIFTY 100 portfolio), or (b) the investor sells the existing position to resolve the cognitive dissonance between "the bot says AVOID_ENTRY" and "I still hold this." Option (b) is a genuine behavioral failure mode caused by the interaction of B-W1 with the disposition effect reversal — the bot can actually push the investor into selling at the trough.

The REGIME-OVERRIDE hook (§3.4 placeholder) is the right direction. But its absence from v0.1 means that for cyclicals, the bot currently instructs the investor to do the wrong thing at the most important moments. That is a worse behavioral outcome than having no signal at all.

---

### B-W2 — Lagging regime gate misses V-shape recoveries

**Position**: CONFIRM as critical. The behavioral cost exceeds the quant cost, and the trust damage will be cumulative.

The synthesis quantifies the return miss (Infosys +155%, HDFC +85%, Maruti +90% over 12 months from the Mar-2020 low). The behavioral framing that the synthesis misses: these are not quiet misses. V-shape recoveries are the most emotionally salient events in an investor's mental diary. They are the moments everyone talks about ("did you buy the COVID bottom?"). An investor who was actively using a signal system that said WAIT throughout March and April 2020, while the market was recovering around them, will remember that for years.

The mechanism of trust destruction is not symmetric with the mechanism of trust building. The bot can correctly call 20 good entry points, and one high-profile miss at a V-shape bottom will dominate the investor's confidence assessment. This is the availability heuristic: easily recalled, emotionally charged events are overweighted in assessments of system reliability. Infosys rising from ₹570 to ₹1,450 while the bot said WAIT is an easily recalled, emotionally charged event.

The trust damage has a practical consequence that goes beyond the immediate miss: after a high-profile miss, the investor becomes selectively skeptical of future WAIT signals. They start overriding WAIT specifically when they feel the market has bottomed — which is exactly the moment they are most likely to be wrong about the bottom call (markets often double-dip). The bot's WAIT signal becomes the trigger for the investor's counter-signal: "bot says WAIT, so this is probably the bottom, I should buy." This is worse than if the investor never had the bot at all.

The synthesis proposes asymmetric hysteresis as a fix (keep BULL→BEAR at 4 weeks; shorten BEAR→BULL to 1–2 weeks with ADX expansion + volume confirmation). From a behavioral standpoint, this is the right direction, but not sufficient. An investor who missed +155% on Infosys in 2020 because the bot said WAIT will require explicit acknowledgment in the output when the regime flips: "REGIME TRANSITIONING TO BULL: Prior signal was WAIT following V-shape recovery. Entry opening now." The absence of this acknowledgment leaves the investor in a state of: "the bot was wrong for 6 weeks and now it says ENTRY_ZONE — should I trust it?" The transition moment needs its own communicative design, not just a math fix.

**The 5-day CIRCUIT-RECENT interaction**: This compounds B-W2 in a particularly costly way for Pranav's specific decision profile. CIRCUIT-RECENT suppresses ENTRY_ZONE signals for 5 days after any circuit hit. During a V-shape recovery, circuit hits are dense in the crash phase and then stop. By the time CIRCUIT-RECENT clears and the regime gate is approaching its BEAR→BULL confirmation, the stock has already recovered 20–30%. The investor sees 5 days of CIRCUIT-RECENT followed by 4–8 weeks of REGIME-BEAR, and then by the time ENTRY_ZONE fires, the opportunity has passed. This sequential blockage from two separate filters — each individually defensible — compounds into a near-total blockage of V-shape recovery entries. Neither filter knows the other is also blocking. The output shows each block individually; the investor does not see "you are being triple-blocked here."

---

### B-W3 — Conglomerate ENTRY_ZONE never fires

**Position**: CONFIRM, with a specific behavioral harm that the synthesis understates.

Zero ENTRY_ZONE labels across 6 dates for Reliance means the bot has given the investor no actionable output for one of the largest, most-held stocks in any Indian equity portfolio. But the behavioral harm is not just "missed opportunity." The harm is the asymmetric label output.

When the bot never produces ENTRY_ZONE for Reliance but regularly produces WAIT or occasionally AVOID_ENTRY, the investor updates their prior about the stock in the direction the bot is pointing. Even if the investor consciously knows "the bot seems to not like conglomerates," the repeated exposure to non-positive labels will produce affect-based contamination. After 6 months of WAIT labels on a stock that has been rising, the investor has accumulated 26 WAIT signals and 0 ENTRY_ZONE signals. Their gut assessment of the stock has been nudged toward skepticism regardless of what their conscious reasoning says about "the bot doesn't model conglomerates well."

The fix (lower ROC threshold for conglomerate-tagged stocks or add sector-relative ROC) is correct math. The behavioral corollary that needs to go in the output: when no ENTRY_ZONE has fired for a given stock in a trailing 12-month window, the output should explicitly annotate: "ENTRY_ZONE has not fired for this stock in the past 12 months — this may indicate model limitations for multi-segment businesses rather than a negative thesis on the company." Without this annotation, repeated WAIT on a rising stock trains the investor to be wrong.

---

### B-W4 — NIFTY 100 cross-sectional ROC disadvantages off-theme stocks

**Position**: CONFIRM, but the behavioral harm is secondary to B-W1, B-W2, B-W3.

The mechanism is real — ITC during ESG overhang correctly penalized (good); Reliance during sector-rotation periods incorrectly penalized (bad). The behavioral cost is specifically about investor calibration: when the bot produces WAIT for a stock that is rising (even slowly), the investor does not know whether WAIT means "fundamentally weak" or "low relative momentum vs NIFTY 100." These are very different reasons for WAIT with very different action implications.

The current output structure (§9.2 reasoning string) would show "ROC rank 45 of 100 → MOMENTUM-MID" which is interpretable. This is a partial mitigation. The behavioral damage is bounded if the reasoning string is visible and legible. But the synthesis found ITC during 2014-2022 underperformance "correctly avoided ENTRY_ZONE" — from Pranav's behavioral standpoint, sitting on the sidelines of ITC for 8 years because of relative ROC is not a defensible behavior instruction for a long-term investor.

The deeper issue: NIFTY 100 cross-sectional ROC is a momentum signal, not a quality signal. A long-term investor (B1 frame) should not be avoiding a high-quality stock because its 6-month relative performance is in the middle quintile. The ROC ranking is the correct filter for B2 (timing an entry into a stock already validated by B1) — but it should not be the primary gate for whether to hold a stock at all. In v0.1, there is no clean separation between "don't enter" and "don't hold." AVOID_ENTRY and WAIT both have the behavioral effect of "stay away," even though the system only intends them for entry timing. For a stock the investor already holds, a sustained WAIT signal will eventually trigger anxiety-driven exit. The label set needs a "HOLD-THROUGH" category for already-held positions that are in the mid-momentum band but have not triggered EXIT_WARNING.

---

### B-W5 — ATR stop unusable in crisis volatility

**Position**: CONFIRM as critical. This is the most operationally damaging behavioral failure in v0.1. Whichever way the investor goes on an unusable stop, they lose.

The synthesis correctly identifies the math: HDFC Bank Mar-2020, 2.5 × ATR weekly = 32% stop. The behavioral analysis needs to go further: there are two possible investor responses to a 32% stop, and both are wrong.

**Response A — Follow the stop.** The investor sees ENTRY_ZONE (once the regime flips), entry price ~₹770, stop at ₹520. They place the stop or commit to it mentally. The stock then recovers with volatility — it drops from ₹770 to ₹640 before recovering to ₹1,400. At ₹640 (a 17% drop from entry), the investor who placed the stop at ₹520 is still in the position but deeply uncomfortable. They see a 17% mark-to-market loss and override the stop manually at ₹650 ("I'll stop out here since I'm already down 17%"). They crystallize a loss of 17% at a stock that goes on to return +80% from entry. Following the spirit of the stop but not the letter is the worst outcome: it combines the anxiety of the "stop" frame with an arbitrary override that happens to be at the worst moment.

**Response B — Ignore the stop.** The investor sees 32% stop and correctly identifies it as meaningless ("a stop at ₹520 on a ₹770 stock does nothing for me"). They invest without any stop. Now the system's risk management — the one mathematical contribution of Step 6 — has been discarded. The position sizing also becomes wrong: if the stop is ignored, the formula `position_size = risk_budget / risk_per_share` is no longer operative. The investor either sizes by feel (usually too large, since they're buying at what feels like a bottom) or uses some other heuristic. The 1% per-name risk budget, which the system locked in B.2, becomes completely decoupled from the actual position taken.

**The credibility cascade**: Once an investor overrides or ignores a stop in one case, the mental model for stops in general degrades. The next time the bot provides an ATR stop, even at a reasonable 7%, the investor applies the same "stops from this bot are advisory only" frame. The 32% stop in a single edge case has contaminated the stop framework for all future cases.

**The specific asymmetry with Pranav**: Pranav is an experienced investor. He will immediately notice the 32% stop and flag it as wrong. But "experienced" in this context also means he has a strong prior on what a stop should look like (~10%). Any stop that deviates significantly from ~10% will be overridden regardless of direction. A 32% stop gets overridden upward ("I'll stop out at 15%"). A 5% stop on a calm stock also gets overridden downward ("5% is too tight; I'll mentally use 12% instead"). The ATR-based stops produce a distribution of outcomes that are almost entirely outside retail intuition's comfort zone, so the stop guidance is discarded in most cases.

The P0.3 fix from the synthesis (cap stop at 15%) is the minimum viable fix. Even this may not be enough — a 15% stop on HDFC Bank at ₹770 means ₹655 stop, and the stock did touch ₹640 before recovering. The investor on a 15% cap would still have been stopped out 2 months before the major recovery. The behavioral problem with any stop in crisis conditions is that the recovery drawdown can exceed any reasonable stop by construction (because the market doesn't know where the stop is). For v0.2, the cap is essential, but it should also come with explicit communication: "In current crisis-volatility conditions (ATR > 3× historical average), stop placement is indicative only — wider stops are a feature, not a flaw."

---

### B-W6 — BFSI combined display §10 completely non-functional

**Position**: CONFIRM as high severity, with a behavioral dimension the synthesis does not explicitly address.

The synthesis frames B-W6 as a math coverage gap: HDFC Bank has no Cycle A FA label, so §10's conflict matrix can't run. The behavioral cost is different: the investor sees ENTRY_ZONE (or WAIT) for HDFC Bank from Cycle B with no corresponding Cycle A label. The conflict matrix that was supposed to protect against overconfidence (by showing both FA and TA perspectives) simply does not appear. The investor receives a single-lens signal without knowing it is single-lens.

HDFC Bank is routinely 10–15% of a typical Indian retail equity portfolio. The absence of the combined display for this stock means the safety-net feature (§10) is missing for the investor's largest position. They don't know it's missing. This is the worst kind of blind spot: not an acknowledged gap, but an unacknowledged single-lens output that looks identical to a dual-lens output.

The fix is correctly identified (add BFSI-MONITOR row to conflict matrix, or accelerate Cycle A's BFSI pipeline). The behavioral requirement that should be added: until the full BFSI FA pipeline exists, the HDFC Bank output must explicitly state: "FA LENS: Not available (BFSI-specific FA pipeline not yet implemented). Cycle B TA signal only — treat with additional caution." The investor should never receive what looks like a complete signal when it is structurally incomplete.

---

### B-W7 — Structural-event distortion of regime gate

**Position**: CONFIRM at medium severity. The behavioral harm is about signal legitimacy, not decision direction.

HDFC Ltd merger (Jul-2023) means the 40-week SMA computed through that window is based on a hybrid entity. The investor does not know this from the output. They receive REGIME=BULL or REGIME=BEAR without knowing the MA is computed on a mixed pre/post-merger price series. If the regime classification is wrong due to this distortion, the investor receives a bad signal. If it happens to be correct, they receive a correct signal for the wrong reasons. Neither outcome is good for calibration.

The behavioral damage here is to the investor's mental model of what the regime gate means. The gate is supposed to be a clean measure of "is this stock's price trend above its long-term mean?" When that long-term mean is computed across a corporate discontinuity, the answer is mathematically defined but economically meaningless. An investor who understands what the 40-week SMA is supposed to do will find the merger-distorted value confusing, not useful.

The STRUCTURAL-EVENT-CAUTION annotation (proposed fix) is the right approach. The v0.2 priority should be: any date range where a structural event falls within the 40-week lookback window must carry the annotation. The conviction should be downgraded to half regardless of what the regime gate says. This is a conservatism appropriate to genuine uncertainty.

---

### B-P1 — DI-flip as leading indicator (the positive finding)

**Position**: EXTEND — this positive finding has a specific behavioral value that the synthesis undersells.

B-P1 shows that the +DI/-DI flip precedes the 40-week SMA regime signal in detected regime changes (Maruti Sep-2018 being the canonical case). The synthesis recommends promoting this to a standalone entry/exit signal. From a behavioral standpoint, the value here is more specific: it provides early warning that allows the investor to act on a leading signal rather than a lagging one.

The behavioral value of a leading signal is not just about timing. It is about the investor's emotional state during the decision. When the 40-week SMA eventually confirms REGIME-BEAR (weeks after the DI-flip already fired), the investor is typically already down 10–15% from peak. They are in a loss frame. Decisions made in a loss frame are affected by loss aversion and anchoring to the prior high — the investor is more likely to hold and hope than to act on an exit signal. The DI-flip fires before significant losses have accumulated. The investor is still in a near-breakeven or modest-loss frame. Action-taking in this psychological state is substantially easier than action-taking after a confirmed regime break when the loss is already large.

In other words: the DI-flip is not just a better leading indicator mathematically — it fires at the moment when the investor's psychology is most amenable to acting on it. Promoting it to a standalone EXIT_WARNING signal (as B-P1 proposes) is correct and should be a P0 priority specifically because it addresses the behavioral window for action-taking.

---

## 3. NEW behavioral concerns

### BC-A — Label ambiguity on WAIT: the investor needs to know whether to monitor or forget

The synthesis flags the WAIT-paralysis concern in passing. The deeper behavioral issue: the four output labels (ENTRY_ZONE, WAIT, AVOID_ENTRY, EXIT_WARNING) have three distinct intended user actions — act, monitor, forget. The current label set does not distinguish between "monitor actively" and "forget until conditions change." All four WAIT sub-reasons (RANGING / SQUEEZE-PENDING / NOISY-MOMENTUM / POSITION-EXTENDED / PULLBACK-CONTINUING) have different monitoring requirements:

- WAIT: RANGING → the stock has no trend. Nothing to monitor. Come back in 4–6 weeks. Forget it.
- WAIT: SQUEEZE-PENDING → the Bollinger Squeeze is active. A large move is imminent. Monitor daily.
- WAIT: PULLBACK-CONTINUING → the downward move is ongoing. Watch for the turn. Monitor weekly.

These are not the same action instruction. An investor who monitors RANGING stocks daily is generating noise anxiety about a stock that by definition has no signal. An investor who forgets a SQUEEZE-PENDING stock misses the resolution event that the squeeze is designed to anticipate. The label WAIT plus a sub-reason is not enough behavioral guidance. Each WAIT variant needs its own "what to do now" instruction:

- RANGING → "No action required. Re-check in 4 weeks."
- SQUEEZE-PENDING → "Monitor this stock daily. A breakout (up or down) is likely within 4–8 weeks. When it resolves, re-run the pipeline."
- PULLBACK-CONTINUING → "Check weekly. Entry may be available in 2–4 weeks if MACD histogram turns positive."

Without these distinctions, WAIT becomes a uniform anxiety-inducer: the investor checks WAIT stocks weekly regardless of sub-reason, generates noise, and loses confidence in the system for providing unhelpful repeated outputs.

---

### BC-B — Half-conviction is not an actionable mental model for retail investors

v0.1 produces ENTRY_ZONE (half) as a distinct output with defined sizing math (0.5% risk budget instead of 1%). The synthesis notes this as a retail-user concern. The behavioral analysis needs to be explicit: most retail investors do not have a cognitive category for "half conviction." Their mental model of a stock position is binary: I own it or I don't. The decision to buy is binary. The quantity is determined by a feel for "how much I like it" plus account balance constraints, not by a derived half-risk-budget formula.

Consider the sequence: investor receives ENTRY_ZONE (half). The output says "position size: 416 shares at ₹1,700 = ₹7.07 lakhs (0.5% portfolio risk)." The investor now faces: should I buy exactly 416 shares, approximately 400 shares, round up to 500 shares because 416 seems oddly specific? The precision of the half-conviction sizing creates an implicit authority — the number looks calculated and therefore exact. But it is exactly half of an arbitrary 1% risk budget, calibrated to a stop that may be ignored (B-W5), derived from an ATR that varies with crisis volatility. The precision is false. The investor either follows it exactly (treating a noisy number as authoritative) or rounds it to a non-system number (wasting the sizing math entirely).

The v0.2 output for half-conviction should acknowledge this explicitly: "ENTRY_ZONE (half): consider 400–450 shares (half of a full position). This is approximate — the key is to size smaller than usual, not to hit a specific number." This converts the precise-but-noisy number into a range that the investor can act on with appropriate confidence.

A deeper issue: the entry/exit symmetry breaks at half conviction. If the investor enters at half size and the stock performs well, they need a subsequent signal to "add the other half." v0.1 has no mechanism for this. The investor is left holding a half position in a stock that is performing well, with no system guidance on when to complete the position. They will either add on impulse (at a worse price) or never add (leaving performance on the table). v0.2 should define an explicit "add to half position" trigger: when a stock that entered as ENTRY_ZONE (half) subsequently achieves ENTRY_ZONE (full) conditions, the output should explicitly say "POSITION COMPLETE: add to full size."

---

### BC-C — Confirmation bias amplification in the Cycle A/B conflict display

§10 surfaces Cycle A and Cycle B labels side by side with a default conflict-resolution rule. The assumption embedded in this design: the investor will read both labels, understand the tension, apply the holding-period frame, and make a considered decision. This assumption will fail in practice.

Confirmation bias research (Nickerson, 1998; and specifically for investment context, Hilton, 2001) shows that investors presented with conflicting signals do not apply a neutral integration algorithm. They selectively attend to the signal that confirms their prior. Pranav's "prior" for any stock is his existing position (if held) or his last mental model update (if not held). Given the disposition effect, for a held stock, the prior is typically "I should continue holding." ENTRY_ZONE from Cycle B + REVIEW from Cycle A → the investor sees ENTRY_ZONE and interprets it as confirmation of their hold. The REVIEW is noticed but not acted on ("TA looks fine, FA is just being conservative").

For a not-held stock with a positive narrative ("I've been watching this stock"): ENTRY_ZONE from Cycle B + WATCH from Cycle A → investor sees ENTRY_ZONE and ignores WATCH. The §10.3 note that "for new positions, default to more conservative label" is correct but will not be followed in practice. It is a static rule in documentation; the investor's in-the-moment decision is driven by the more salient label, which is whichever one they want to see.

The "strong conflict" marker (Cycle A FLAG + Cycle B ENTRY_ZONE: requires explicit user confirmation) is the right behavioral intervention for edge cases. But mild conflicts — which represent the majority of the conflict matrix — have no such intervention. The investor receives two labels, reads the one they prefer, and acts on it.

A partial fix: for every Cycle A/B conflict case (not just strong conflicts), the output should include a mandatory single-sentence "friction question" the investor must answer before the action label appears. Example: Cycle B says ENTRY_ZONE (full), Cycle A says WATCH → "Before entering: what has changed in [company]'s fundamental profile since your last review that makes this an acceptable entry?" The question does not prevent the entry. It forces explicit engagement with the tension rather than selective attention to the preferred signal. This is the "implementation intention" technique from behavioral science (Gollwitzer, 1999) — it works by interrupting the automatic response and requiring a deliberate one.

---

### BC-D — Label oscillation will create anxiety rather than information

The ADX conviction modifier (§7.5) means that ENTRY_ZONE (full) can be downgraded to ENTRY_ZONE (half) simply by the ADX crossing from 25 to 23 in a given week. The ROC rank boundary (stocks at rank 19/20 or 21/22 of NIFTY 100) can flip MOMENTUM-STRONG to MOMENTUM-MID and vice versa with one week's price change. The combined routing table (§7.4) has multiple cells where small threshold crossings produce large label changes.

In a weekly output cadence, this means a stock can legitimately oscillate: ENTRY_ZONE (full) → ENTRY_ZONE (half) → ENTRY_ZONE (full) → WAIT across a 4-week period without any meaningful change in the underlying investment thesis. From the investor's standpoint, these are not information updates — they are noise. But the labels carry behavioral weight. ENTRY_ZONE → WAIT creates a "should I have exited?" anxiety. WAIT → ENTRY_ZONE creates a "should I have entered last week?" regret. ENTRY_ZONE (full) → ENTRY_ZONE (half) creates a "is my conviction actually right?" doubt.

Each of these transitions takes the investor through a decision-making episode that has no corresponding real-world event. The cumulative effect of weekly label oscillation at threshold boundaries is learned helplessness: the investor stops trusting the signal because it keeps changing without apparent reason. The exact same dynamic was identified in the Cycle A behavioral critique (NC1: label oscillation with weekly cadence on quarterly signals), but for different reasons. In Cycle A, the oscillation comes from quarterly data timing. In Cycle B, it comes from continuous signals at discrete thresholds.

The fix is threshold hysteresis at the label level — already proposed in the synthesis for the regime gate. The same principle needs to apply across all threshold boundaries in the pipeline. A label transition should require the crossing condition to persist for at least 2 consecutive weekly evaluations before the label changes. This prevents single-week threshold crossings from generating label changes. The output for a transitioning label should say: "ENTRY_ZONE (half): ADX has been in LIGHT range for 1 week (confirmation pending — full conviction if STRONG for 2 consecutive weeks)."

---

### BC-E — The stop-loss intuition gap is wider than B-W5 describes

B-W5 identifies the crisis-volatility case (32% stop on HDFC Bank at Mar-2020) as the canonical failure. The behavioral problem extends beyond crisis. The distribution of 2.5×ATR weekly stops across NIFTY 100 stocks has two tail problems, not one:

**Tail 1 — Crisis volatility (the B-W5 case)**: ATR spikes → stops at 25–35% → ignored or followed perversely. Fix: cap at 15%.

**Tail 2 — Calm stocks**: ITC in 2020-22, HDFC Bank in a low-volatility period. ATR(14) weekly for a calm defensive stock might be ₹10–15 on a ₹250 stock (4–6%). 2.5×ATR = ₹25–37 stop distance = 10–15%. This seems fine for a technical stop. But: the investor buys at ₹250, sets stop at ₹225, and the stock enters a slow drift to ₹235 over 6 weeks (routine mid-cycle consolidation). Stop at ₹225 is 40 points away. The investor watches the stock drift from ₹250 to ₹235 and thinks: "I'm down 6%, the stop is at ₹225, should I tighten?" This is a stop-override impulse in the other direction — not because the stop is too wide, but because the mark-to-market loss creates urgency that the system's stop doesn't validate.

**The retail intuition problem is not just about 30% stops**. Retail investors don't trust stops of any size because they've been trained (by experience and by market commentary) to associate stops with "getting stopped out and then watching the stock recover." The typical Indian retail investor's prior on stops is: "I've set stops before and they always triggered right at the bottom before the stock went up." This prior is epistemically reasonable — in trending markets, 10% stops on quality stocks do trigger at local bottoms during normal corrections. The ATR-based stop framework doesn't address this prior at all. For the stop to be trusted, the reasoning string needs to explain why this stop placement should be followed even when it triggers, and what the investor should do after being stopped out (re-enter signal, wait for regime confirmation).

The reasoning string in §9.2 shows the stop calculation but not the rationale for following it. "ATR-based stop at ₹1,580" is a number, not a reason. The behavioral requirement: every stop output must include a one-sentence "why this stop works" explanation: "This stop is placed below 2.5× weekly volatility — a routine correction in a bull trend is unlikely to breach this level. If it does, the trend has likely broken."

---

## 4. What v0.1 got right behaviorally

**The reasoning string design in §9.2 is correct and should be preserved.** The HDFC Bank example output shows a full causal chain: regime confirmed → trend strength → volatility state → momentum → confirmation → sizing. The investor can argue with the label because they can trace exactly what produced it. This is the central behavioral design requirement for any signal system: the investor's ability to disagree with a specific step rather than receiving an oracle decision. Cycle A's critique made the same point. The Cycle B reasoning string implements this well.

**The pipeline halt pattern (specific sub-reason labels) is good behavioral design.** The system does not silently default to WAIT when a gate halts — it says `WAIT: RANGING` or `WAIT: SQUEEZE-PENDING` or `AVOID_ENTRY: REGIME-BEAR`. This specificity matters for the investor's ability to understand what changed when a label transitions. "WAIT" tells you nothing. "WAIT: RANGING → WAIT: SQUEEZE-PENDING → ENTRY_ZONE (half)" tells a story the investor can follow. This pattern is the correct approach and should be extended to the new WAIT subcategories proposed in BC-A.

**EXIT_WARNING as a distinct label is correct and well-targeted.** The synthesis found that bearish RSI and MACD divergence correctly escalate to EXIT_WARNING (the ITC Jun-2022 case being the ideal example). Behaviorally, EXIT_WARNING is the right register — not FLAG (too alarming), not REVIEW (too vague), but a specific directional nudge for held positions. The label correctly implies "something has changed, time-limited action is appropriate" without the affective contamination of FLAG. The trigger conditions (bearish divergence, regime transition, position extended with overbought RSI) are conservative enough to avoid false EXIT_WARNINGs and specific enough to be actionable.

**The CIRCUIT-RECENT pre-screen serves a real behavioral function beyond its technical purpose.** In the immediate aftermath of a circuit hit, retail sentiment is maximally reactive. Investors buying on day 1 after a circuit hit are almost never making calm thesis-based decisions — they are reacting to the circuit event itself. The 5-day suppression of ENTRY_ZONE signals after a circuit prevents the investor from being inadvertently pushed into a reactivity-driven entry by a signal that happens to fire in that window. This is an implicit behavioral design choice (even if it wasn't framed that way) and it should be kept even as the V-shape miss problem (B-W2) is addressed through asymmetric hysteresis.

**The 4-label + (full)/(half) set is recoverable.** Unlike Cycle A's 4-label set (HOLD/WATCH/REVIEW/FLAG) which has REVIEW as an unactionable label, Cycle B's labels are all directional. ENTRY_ZONE tells you to enter. WAIT tells you to wait. AVOID_ENTRY tells you to avoid. EXIT_WARNING tells you to exit or at least tighten. The behavioral problem is not the labels themselves — it is the calibration of when they fire (B-W2 fires too late, B-W1 fires in the wrong direction) and the usability of the sizing output (B-W5). Fixing the math calibration and stop cap should recover the behavioral utility of the label set without needing a label redesign.

---

## 5. Prioritized v0.2 recommendations

### P0 — Must fix before v0.2 ships

**P0-BEH.1 — Hard cap on stop-loss distance (15% of entry price)**
Fix: MIN(2.5 × ATR_14_weekly, 0.15 × entry_price) — use the stop that is CLOSER to entry. Position size recalculates from the effective stop.
Behavioral basis: a 32% stop will be ignored or followed perversely, in either case damaging the stop credibility framework for all future entries. A 15% cap preserves the ATR-relative insight while staying within retail intuition's tolerance range.
Add to every stop output: a one-sentence rationale for following the stop: "This stop is below [N]× normal weekly volatility — routine corrections are unlikely to breach it. A breach indicates trend failure."
Priority source: B-W5 canonical + BC-E extension.

**P0-BEH.2 — WAIT sub-reasons must include "what to do now" instructions**
Fix: each WAIT variant (RANGING / SQUEEZE-PENDING / PULLBACK-CONTINUING / POSITION-EXTENDED / NOISY-MOMENTUM) must carry a distinct monitoring instruction in the output.
- RANGING → "No action. Re-check in 4 weeks."
- SQUEEZE-PENDING → "Monitor daily. Breakout expected within 4–8 weeks. Re-run pipeline when Bollinger Bandwidth expands."
- PULLBACK-CONTINUING → "Check weekly. Entry possible in 2–4 weeks if MACD histogram turns positive."
- POSITION-EXTENDED → "Already-held positions: watch for EXIT_WARNING. Not-held: no action."
- NOISY-MOMENTUM → "ROC and RSI signals conflict. Re-check after 2 weekly closes."
Behavioral basis: undifferentiated WAIT creates uniform anxiety regardless of sub-reason. BC-A.

**P0-BEH.3 — Label transition hysteresis (2 consecutive weekly confirmations required)**
Fix: any label change requires the new label's conditions to hold for 2 consecutive weekly evaluations. The output during the first confirmation week displays: "[NEW LABEL] (pending: 1 of 2 weekly confirmations)."
Exception: EXIT_WARNING fires immediately (one-observation stop, same logic as knockout gates in Cycle A). AVOID_ENTRY: SURVEILLANCE-HALT fires immediately.
Behavioral basis: single-week threshold crossings generating label changes produce oscillation that destroys investor confidence without conveying information. BC-D.

**P0-BEH.4 — Explicit "FA lens unavailable" annotation for BFSI stocks in combined display**
Fix: until BFSI FA pipeline is implemented, every BFSI stock output in the combined display (§10) must say: "FA LENS: Not available — BFSI-specific FA pipeline not yet implemented. This is a Cycle B (TA) signal only. Treat with additional caution."
Behavioral basis: an investor should never receive a signal that appears to be dual-lens when it is structurally single-lens for their largest holdings. B-W6 extension.

### P1 — Strong desirables (behavioral value is high; not blocking but should be in v0.2)

**P1-BEH.1 — DI-flip as standalone EXIT_WARNING (promote B-P1)**
Fix: promote the +DI/-DI flip to a standalone signal per the synthesis P0.4 proposal, with the specific behavioral framing: the DI-flip fires earlier in the loss cycle when the investor is most amenable to acting. EXIT_WARNING from DI-flip should say: "Directional strength weakening (−DI > +DI) — trend may be transitioning. If this persists 2 weeks, consider tightening stop or taking partial profits." The 2-week confirmation is important here: one-week DI flip is noisy; 2-week persistence is signal.
Behavioral basis: B-P1 behavioral extension — leading signal fires in the right emotional window.

**P1-BEH.2 — Half-conviction output with explicit size range and "add to full" trigger**
Fix: ENTRY_ZONE (half) output should express position size as a range (+/− 10% of calculated value) with explicit instruction: "This is a half-position. Full position trigger: if the stock achieves ENTRY_ZONE (full) conditions in a subsequent evaluation, add the remaining half." Without this, half-conviction entries leave the investor stranded without system guidance for completion.
Behavioral basis: BC-B.

**P1-BEH.3 — "No ENTRY_ZONE in 12 months" annotation for structural model-limitation stocks**
Fix: when a stock has received 0 ENTRY_ZONE signals in the trailing 52-week window, append to the output: "NOTE: No ENTRY_ZONE signal has fired for this stock in the past 12 months. This may indicate model limitations (e.g., conglomerate ROC penalty, sector-rotation dynamics) rather than a negative thesis on the company."
Behavioral basis: repeated WAIT on a rising stock trains the investor toward negative prior on the stock without causal basis. B-W3 extension.

**P1-BEH.4 — Friction question on Cycle A/B mild conflicts**
Fix: for every Cycle A/B conflict cell in §10 (not just strong conflicts), the output must include a mandatory "friction question" before the action recommendation: "Before [action]: [specific question about the tension between the two signals]." Example: Cycle B ENTRY_ZONE (full) + Cycle A WATCH → "Before entering: Is the fundamental concern that produced WATCH (see Cycle A output) a thesis-breaking risk or a temporary setback?"
This question does not block action — it requires deliberate engagement with the conflict. The implementation-intention design (Gollwitzer, 1999) makes automatic confirmation-bias responses less likely.
Behavioral basis: BC-C.

### P2 — Useful for calibration; defer if v0.2 scope is tight

**P2-BEH.1 — Regime transition acknowledgment message for BEAR→BULL flip**
Fix: when the regime transitions from BEAR to BULL (or BEAR-DEVELOPING to BULL), the output for the first ENTRY_ZONE signal should include explicit acknowledgment: "REGIME TRANSITIONING TO BULL: Prior WAIT/AVOID_ENTRY signals reflected BEAR or transitional regime. Entry opening now."
This directly addresses the trust damage from B-W2 by closing the loop on the WAIT period rather than silently presenting a new ENTRY_ZONE as if the prior period didn't happen.
Behavioral basis: B-W2 trust damage mechanism.

**P2-BEH.2 — Cyclical-sector AVOID_ENTRY advisory note**
Fix: for cyclical-sector stocks (Metals, Oil & Gas, Chemicals, Power) receiving AVOID_ENTRY: REGIME-BEAR, append: "CYCLICAL-SECTOR NOTE: For cyclical stocks, REGIME-BEAR at a sector trough may coincide with the best entry opportunity. This signal prevents new entry on trend-following grounds — it does not address valuation timing. See Cycle A (FA) output for fundamental context."
This does not change the math. It breaks the automatic "AVOID_ENTRY = stay away" heuristic for the one class where the signal inverts.
Behavioral basis: B-W1 behavioral extension.

**P2-BEH.3 — Stop-loss narrative for investor commitment**
Fix: the sizing output (§9.2 SIZING block) should include a final line: "Stop-loss commitment: If [stock] closes a weekly bar below ₹[stop price], the trend assumption underlying this entry has been invalidated. Exit at or near this price — do not wait for a bounce."
Behavioral basis: BC-E — stop-loss requires a reason to be followed, not just a number.

---

## One sentence to the synthesizer

The behavioral cost of this system's failure is concentrated in two moments — the V-shape bottom and the stop-loss decision — and if those two moments go wrong, the investor will find ways to rationalize abandoning the entire system; fix the stop cap (P0-BEH.1) and add WAIT monitoring instructions (P0-BEH.2) before v0.2 ships, and the rest of the signal architecture is worth keeping.

---

**Status**: Complete.
**Last updated**: 2026-05-31
**Counts**: §1 verdict + §2 per-weakness (B-W1 through B-W7 + B-P1 = 8 entries) + §3 new behavioral concerns (BC-A through BC-E = 5 entries) + §4 what got right (4 findings) + §5 prioritized recommendations (4 P0 + 4 P1 + 3 P2 = 11 items).
