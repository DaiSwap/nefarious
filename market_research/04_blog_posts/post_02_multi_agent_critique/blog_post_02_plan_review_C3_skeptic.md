# Blog Post #2 Plan — Skeptic Review (C3)

**Reviewer**: C3 — Skeptic / Counter-argument lens
**Plan reviewed**: `blog_post_02_plan.md`
**Date**: 2026-05-31
**Claims flagged**: 7 (structural) + 7 specific claims (A–G)
**Verdict**: NEEDS-WALK-BACK

---

> This review's job is to find what doesn't hold up, not to affirm what does. Where a claim is solid, it's noted briefly. Most words go to the gaps — that's the assignment.

---

## §1 — Skeptic Verdict

**NEEDS-WALK-BACK**

The plan has a tight structure and a clear takeaway. Several of the voice and framing decisions are genuinely good. But the three central empirical claims — that multi-agent review catches things single-AI misses, that the five-roles design is the mechanism behind that improvement, and that the synthesizer "decides who's right" — are stated with more confidence than the evidence in the plan supports. The post, as planned, will read to a careful reader as: "I ran an experiment once, it worked, here's the principle." That's not what the "still learning" tone promises, and the gap between what's asserted and what's demonstrated is wide enough to undermine credibility with exactly the audience (builders, investors who do their own research) that would be most valuable to reach.

The three anonymized examples are real. The catches were real. That's the post's genuine asset. The problem is the causal and comparative claims wrapped around those examples. Those need to be hedged more precisely, not just in tone but in the actual structure of the argument.

There is also a structural tension between the plan's stated voice constraint ("still learning, not done") and the post's actual arc, which delivers a resolved, lesson-complete narrative. The plan acknowledges the "self-congratulatory" risk in its own "risks" section — but the prescribed fix (hedging language like "I think" and "early signs") is cosmetic. The deeper fix requires adding genuine uncertainty to the substance, not just the phrasing.

That said: the post is not in "RECONSTRUCT-ARGUMENT" territory. The core idea — that prompting an AI into different specialist roles produces different and collectively more useful critiques — is plausible and worth writing about. The walk-back needed is on the comparison claim (§1 / Q1), the necessity claim (§3 / Q3), and the synthesizer claim (§2 / Q5). Fix those three and the rest of the post holds.

---

## §2 — Per-Question Skepticism

### Q1: "Single-AI agrees; multi-AI disagrees" — empirically supported or asserted?

Asserted. The plan does not describe a controlled test. The hook reads: "I asked Claude to check my investing math. It told me my math was fine. Then I asked five different versions — one of them caught a bug." But this is not an apples-to-apples comparison. The single-AI check and the five-AI check are presented as sequential, not simultaneous. There is no indication that the single-AI was given the same level of instruction, the same role specificity, or the same mandate to find faults. The single-AI check sounds like it was a casual "does this look right?" while the five-AI check was a structured critique with domain-specific framing.

The claim the post needs to make: "When you ask a single AI in the same structured, fault-finding mode, it still misses things the five-specialist setup catches."

The claim the post actually makes: "I asked it one way and it agreed; I asked it another way with five roles and it disagreed."

That's a comparison of prompting strategies, not of single vs. multi-agent architecture. The reader who notices this will conclude the real finding is "better prompting gets better results" — which is true but far less interesting than the framing implies. The post needs to either (a) acknowledge this explicitly, or (b) run a quick comparison: ask one AI in the same structured critic mode and show it still misses the bugs the five specialists caught. Without that, the core comparison does not hold.

### Q2: "This is widely used in AI research (debate, jury, MoA)" — is the one-liner enough?

Barely, and only if the claim is modest. The plan flags this as a single line: "I didn't invent this — researchers call it AI debate or jury." That's honest, which is good. But it introduces a new problem: it implies the post's technique is a faithful implementation of those research paradigms, and it isn't obviously so.

"AI debate" (Irving et al., 2018) is a specific safety-research setup where two agents argue and a judge rules — not five specialists plus a synthesizer. "Mixture-of-Agents" (MoA) is a specific architecture where agents propose and a final model aggregates. The post's setup is closer to a panel review or a structured red-team. If the one-liner lands as "I'm doing what researchers do," a reader who knows those papers will find that overclaiming. If it lands as "this general idea has precedent," it's fine.

Recommendation: the one-liner needs one more sentence specifying the parallel is loose — "the spirit is the same, my setup is simpler and more informal." As written, it risks sounding like a credential-by-association claim.

### Q3: The three examples — were they necessary catches or sufficient ones?

This is the sharpest gap in the plan. The plan states: "None of these would have surfaced from one AI looking at the same work."

That's a strong causal claim. But the plan doesn't establish it. What it shows is that the bugs were caught by the five-specialist setup. That's sufficiency. Necessity is a separate question: would a careful manual review by a human have caught the ATR stop inversion? Would a second pass with better prompting have caught the BFSI gap? Would a domain expert (not AI) reviewing the system have caught the compounding signal overlap?

For each of the three examples:

**ATR stop bug (risk-sizing formula inversion)**: This is a formula-level sign error — the formula was making position size go up when volatility went up. That's the kind of bug a quant with domain experience would spot in a code review. It's also the kind of thing a single AI asked specifically "check whether this formula behaves correctly under high-volatility conditions" might catch. The post implies the multi-agent structure was necessary. It might just be that the right question wasn't asked the first time.

**BFSI gap**: A third of the investable universe being silently skipped is a large and visible gap. This would likely surface the first time the system was run on real data and someone noticed the BFSI names were absent. It is plausible that the multi-agent setup caught it early, but "early" is not the same as "uniquely."

**Compounding parts / overlapping signal**: This is the most legitimately subtle catch — two components that look independent but are reading the same lagging signal. This one is a stronger candidate for "would have been hard to catch without the integrator framing." But the plan treats all three as equivalent evidence, when they have meaningfully different strength.

The post should differentiate the catches rather than treating them as a homogeneous set. One of the three is genuinely strong evidence for the multi-agent structure being necessary. Present it that way.

### Q4: Counterfactual — would the same prompt run five times catch the same bugs?

The plan doesn't address this at all, which is a significant gap. The five-specialist framing claims value comes from role differentiation. But large language models have non-trivial sampling variance. Running the same "find problems in this" prompt five times, with different random seeds, would produce five different critiques — some of which might overlap substantially with what the five specialists produced.

If the answer to "does role differentiation matter, versus just sampling diversity?" is "we don't know," the post should say so. If the author has a prior belief that roles matter independently of sampling variance, that should be stated as a belief, not as a mechanism.

This matters because it changes the practical advice. If roles don't matter and sampling does, the takeaway is "run it multiple times." That's simpler and potentially more useful than "build five specialist personas." The plan implicitly makes the stronger claim (roles are the mechanism) without testing the weaker alternative (sampling is sufficient).

There is a reasonable intuitive argument for why roles matter beyond sampling: a "numbers person" is instructed to look at a specific dimension, so its probability of noticing a formula sign error is higher than a generic reviewer's, regardless of sampling. That argument can be made briefly in the post. But it needs to be made — not assumed. The mechanism cannot be left implicit when the post is structured as an argument for why the technique works.

### Q5: The synthesizer "decides who's right" — how?

The plan says the synthesizer "reads all five and decides who's right when they disagree." This is presented as the solution to the "five conflicting reviews" problem. But it isn't a solution — it's a restatement of the problem one level up. Now instead of the human adjudicating five opinions, an AI is adjudicating five AI opinions.

The question the post doesn't answer: on what basis does the synthesizer adjudicate? If two specialists disagree with equal apparent confidence, what does the synthesizer do? Does it go with the majority? Does it weight by perceived expertise? Does it generate a new view that differs from all five? The plan doesn't specify, which means the reader has no way to evaluate whether the synthesizer is actually resolving disagreements or just producing a new, blended opinion that sounds more confident than the inputs.

This is the hardest conceptual problem in the post. "The synthesizer decides" is the weakest point in the argument because it presupposes the synthesizer has access to ground truth that none of the specialists had — but it doesn't. It has the same training, the same limitations, and the same tendency to sound confident when it isn't. The post needs either (a) a concrete example of how the synthesizer adjudicated a specific disagreement, or (b) honest acknowledgment that this is an open problem and the synthesizer's output still requires human review.

The plan mentions the synthesizer produces a "priority list of fixes." That's a more honest and accurate description than "decides who's right." If the draft uses the priority-list framing throughout rather than the "decides" framing, this problem is largely resolved. The concern is the word "decides" specifically — it implies the synthesizer has access to correctness, which it doesn't.

### Q6: "Still learning" tone vs. implicit authority — does this contradict?

Yes, and the tension is embedded in the plan itself. The lede paragraph ends with: "This is the technique that's making it actually useful." That's not "I'm trying this." That's "I found the thing that works."

The plan acknowledges this risk in the "voice constraints" section and lists "still learning, not done" as locked. But the structural design of the post argues against it. The post moves from problem (§1) to setup (§2) to evidence-it-works (§3) to explanation-of-why (§4) to lessons-I've-internalized (§5) to implications (§6). That's the structure of a "here's what I learned and why it's right" post, not an "I'm trying this" post.

A genuine "still learning" post would include at least one place where the technique failed, or where the synthesizer got it wrong, or where the post-multi-agent version still had problems. The plan contains none of that. Every example is a success story. If those are cherry-picked wins from a larger set that included failures, the post is misleading. If there were no failures, that itself is suspicious and worth addressing.

The "still learning" framing, without any counterexample, reads as false modesty that's actually self-promotion. The plan should either include a failure case or drop the "still learning" framing and own the stronger claim it's actually making.

One concrete option: add a single sentence in §5 or §6 that names something the five-specialist setup has not resolved. For example: "The synthesizer still doesn't tell me which bugs to fix first — that prioritization is still mine to make." Or: "I've run this on system design problems, but I haven't yet tested it on something where I was deeply wrong and the specialists were split." Either sentence would make the "still learning" claim credible without undermining the examples that came before it.

### Q7: Selection bias on the three examples

The plan describes the three examples as coming from specific sessions (B-W5, B-W6, B-W1 from session notes). The question is whether these were selected because they were the strongest, most vivid catches, or because they were representative.

The plan presents them as representative ("what changed when I started doing this"). But if these were selected from a larger pool of critique outputs because they were the most dramatic catches, the post overstates the expected value of the technique. A reader who runs five specialists and gets 20 items back — as the plan mentions — will find that most of those items are not dramatic bugs but minor suggestions, edge-case considerations, or questions that don't require fixes. The post should acknowledge that the three examples are the standout catches from a session that also produced many lower-value outputs. That's honest and doesn't weaken the argument — it makes it more credible.

There is also a subtler version of selection bias worth flagging: the plan notes that the technique produced "20+ specific things wrong" but then selects three. The reader may reasonably wonder: what were the other 17+? Were they also valid? Were many of them wrong? Were they contradictory? A note on the signal-to-noise ratio of the full output — even something like "of the 20+ items, I'd say about half were actionable" — would give the reader a more accurate picture of what running this technique actually produces.

The three chosen examples also happen to span three different kinds of failure (formula error, coverage gap, architectural flaw). That's a good selection for illustrative breadth. But it means they are not a random sample — they are selected for variety. The post should be transparent that the examples were chosen to illustrate different types of catch, not to represent the average catch.

---

## §3 — Specific Claims Needing Sourcing or Hedging

The following claims appear in the plan and will presumably appear in the draft. Each needs a fix before the draft ships.

A note on the ordering: Claims A and B are structural — they affect the credibility of the post's entire argument. Claims C through E are local — they weaken individual sections but don't collapse the post if left unaddressed. Fix A and B first.

**Claim A**: "None of these would have surfaced from one AI looking at the same work."
Fix needed: Either run the comparison (same structured critic prompt, single AI) and report results, or hedge to "I don't think these would have surfaced from a single-pass review, though I haven't run that comparison directly."

**Claim B**: "Single-AI review: 'looks good.' Five-AI review: average of 20+ specific things wrong."
Fix needed: This comparison is measuring two different prompting modes, not two different agent counts. Acknowledge this or restructure the comparison. Without the acknowledgment, this is the most likely line for a skeptical reader to reject the whole post.

**Claim C**: "The synthesizer is the trick — without it, you'd just get five conflicting reviews and no decision."
Fix needed: This overstates the synthesizer's capability. The synthesizer produces a prioritized view, not a verified correct answer. Change to something like: "The synthesizer is useful for forcing a priority order — it doesn't guarantee the right answer, but it reduces the 'five opinions with no direction' problem."

**Claim D**: "Five roles = five different slices. Different slices catch different things."
Fix needed: This is the mechanism claim. It needs either a brief argument for why role differentiation produces meaningfully different outputs (beyond sampling variance) or an acknowledgment that the role-differentiation mechanism is a hypothesis, not an established fact.

**Claim E**: "Pretending to be a specific kind of expert is more useful than just asking 'what do you think?'"
Fix needed: "More useful" compared to what? A well-structured single prompt with a clear mandate? This claim needs a baseline to be falsifiable. As written it compares a specific, structured approach (role + mandate) to an unspecific, casual approach ("what do you think?"). That's not a fair comparison.

**Claim F**: "AI is best as a critic, not as a writer."
This appears in §5 as a lesson learned and is probably the most quotable line in the post. It's also the most underexplained. "Best" at what — precision, actionability, reliability, cost? This is a genuinely interesting observation and deserves more than a throwaway line. Either expand it slightly (one sentence of why) or cut it. As a standalone claim with no support, it invites the reader to challenge it rather than accept it.

**Claim G**: "The cost is: more rounds, more time. The benefit is: real catches, not vibes."
This is the clearest honest moment in the plan. It should be expanded rather than compressed. How much more time? Is it 2x the work, 5x? If the reader is going to replicate this, they need a rough estimate of the overhead. "More time" without any quantification signals that the author hasn't thought rigorously about the cost side of the tradeoff — which undermines the "I'm doing this carefully" framing the post is trying to establish.

---

## §4 — What the Post Does Support Well

These are genuine strengths and should be preserved:

**The three examples are real and specific.** The ATR stop inversion is a concrete, verifiable bug type (sign error in a formula). The BFSI gap is a coverage failure that's plausible and large. The compounding/overlap catch is subtle enough to be interesting. These give the post its credibility floor. Don't over-anonymize them — the specificity is the point.

**The fan-out + synthesizer structure is clearly communicated.** The mermaid diagram and the §2 description of the five roles are clean and genuinely useful for a reader who wants to replicate the approach. The names chosen (numbers person, behavior person, Indian-market person) are accessible without being dumbed down.

**The acknowledgment that the technique has research precedent is the right call.** "I didn't invent this" is harder to say than it sounds, and it's the right thing to say. It should stay.

**The one-AI sycophancy observation is the strongest grounded claim in the post.** The observation that "even when you ask for critique, it gives polite considerations rather than 'you're wrong, here's why'" is a real phenomenon that many readers will have noticed. This is the one place where the post doesn't need more evidence — it's well-understood behavior and the reader will nod along.

**The closing teaser for Blog #3 is well-placed.** It suggests the methodology actually produced a finding worth following up on. That builds credibility for the series even if this post leaves methodological questions open.

**The five role names are well-chosen for the target audience.** "The Indian-market person" and "the behavior person" are grounded in terms a retail investor reader will understand without needing a glossary. This is harder to get right than it looks and the plan gets it right.

**The "risks" section in the plan is honest.** The plan explicitly names the risks of being "too process-y," "inside-baseball," and "self-congratulatory." The fact that those risks are named means the writer is aware of them. The question is whether the prescribed mitigations (concrete examples, accessible language, humble tone) are sufficient — this review argues some are not sufficient without structural changes, but the self-awareness is a genuine asset.

**The audience scoping is clear and the secondary audience is correctly identified.** Indian retail investors who use AI tools are the primary audience; builders are the secondary. The post's practical, pattern-focused framing serves both without trying to please both at once. That's a harder balance than it looks, and the plan maintains it.

---

## §5 — Priority Fixes for the Draft (Ranked)

These are fixes the writer should make before putting a word in the draft — not after. Fixing these at the plan stage is much cheaper than fixing them in a v0.2 draft review.

If the writer can only address three things before writing the draft, these are the three:

**Priority 1 — Reframe the core comparison (Q1 / Claim B).**
The hook works emotionally but it's logically weak. The single-AI check and the five-AI check need to be described as different prompting strategies, not different "counts" of AI. The simplest fix: add one sentence in §1 that acknowledges the comparison isn't perfectly controlled and that the real claim is about structured critique, not agent count. This preserves the hook while removing the false premise.

**Priority 2 — Add one failure case or open question to §5 or §6 (Q6).**
The "still learning" framing is the plan's stated tone lock, but there is zero evidence of it in the structure. One concrete moment where the synthesizer got it wrong, or where the five-specialist setup produced contradictory advice that required human judgment to resolve, would do more work for credibility than five more success examples. If no such failure exists in the actual sessions, that is worth saying explicitly — and worth treating as a finding in itself ("the technique hasn't failed me yet, which is either a good sign or a sign I'm not testing it hard enough").

**Priority 3 — Differentiate the three examples by evidential strength (Q3).**
Don't present them as equivalent. The compounding-signal overlap catch is the strongest evidence for the multi-agent structure being necessary. The ATR stop bug and the BFSI gap are real catches but are easier to explain away as "a more careful single review would have found these." Acknowledge the gradient. This makes the post more honest and, counterintuitively, more persuasive — a writer who ranks their own evidence is more credible than one who presents all evidence as equally compelling.

**Lower priority but worth noting:**

- Synthesizer adjudication (Q5): add one sentence about what happens when specialists disagree and the synthesizer can't resolve it. Even "I still have to make the final call" is enough.
- Counterfactual (Q4): add one sentence acknowledging you haven't tested whether sampling variance alone would produce the same catches. Frame it as an open question.
- Research precedent (Q2): add one sentence clarifying the parallel is loose and informal, not a claimed implementation of the academic techniques.

---

## §6 — The One Structural Choice That Could Fix Most of This

The plan's structure is: problem → technique → evidence-it-worked → explanation-of-why → lessons → implications.

An alternative structure that would resolve most of the skeptic's concerns: problem → technique → evidence-it-worked → **what could explain this** (including the weaker explanations: better prompting, sampling variance, novelty effect) → **why I think the five-roles framing is the right explanation despite the alternatives** → lessons → implications.

That structure forces the post to engage with the counterfactuals rather than ignore them. It transforms the post from "here's a technique that worked" to "here's a technique that worked, and here's how I'm thinking about whether it's really the technique or something else." That's a more honest and more intellectually interesting post — and it's compatible with the "still learning" tone that the plan has locked in.

It is a harder post to write. But it's the post the plan is promising.

The current structure will produce a good read for people who don't push back on it. The alternative structure will produce a post that survives a skeptical reader — and given that the target secondary audience includes people who build AI tools, skeptical readers are exactly who the post needs to survive.

---

---

*Skeptic review complete. 7 structural claims interrogated, 7 specific claim fixes identified (A–G), 3 priority fixes ranked for draft stage, 6 genuine strengths noted. Net verdict: the post has a real story to tell — it needs to stop overclaiming around it.*
