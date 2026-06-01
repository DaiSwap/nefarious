# Blog Post #2 Plan — Editorial Review (C2)
**Reviewer lens**: Medium-experienced editor — sentence rhythm, weak verbs, hedge repetition, structural pacing, closing-line quality.
**Date**: 2026-05-31

---

## §1 Editorial Verdict

**NEEDS-REWORK**

Not a scrap — the bones are solid and the central idea is genuinely interesting. But the plan is carrying three problems that, left unaddressed, will produce a draft that feels procedural and slightly smug even when it's trying to be humble.

**Problem 1 — The hook is a rhythm problem, not a content problem.** The four sentences work logically but land flat emotionally because they're all the same length and the same structure (subject–verb–object, subject–verb–object). The punch never actually lands.

**Problem 2 — §5 is a bullet trap.** The plan lists six things the writer "learned." In draft form, without deliberate intervention, this section will become a listicle inside a prose post. The plan needs a prose-first instruction for this section.

**Problem 3 — The closing teaser is already overwritten at the plan stage.** When the teaser in the plan is already 52 words and includes a hedge-in-hedge ("I'm still investigating, but the pattern is striking enough that I want to share it"), the draft version is going to be worse. The teaser needs to be a single, clean, under-20-word sentence. What's there now is two sentences that are afraid to commit.

The voice-baseline in v0.3 is a meaningful bar. That post's best moments (the "sticky note" passage, "The work is mine. The accelerant is the AI.") work because they're short and undisguised. This plan, in several places, is trying to be humble and clever at the same time. It can't be both in the same sentence.

---

## §2 Per-Question Editorial Feedback

### 2.1 The hook (4-sentence lede): pacing, punch, redundancy

**Current draft:**
> A few weeks ago I asked Claude to check my investing math.
> It told me my math was fine.
> Then I asked five different versions of Claude — each pretending to be a different kind of expert — to check the same math.
> Four of them disagreed with each other. One of them caught a bug that would have lost me real money.

**What works**: The setup is clear. The payoff ("real money") is concrete.

**What doesn't**:

- Sentence 1 and 2 are the same length (11 and 9 words). Sentence 3 is 22 words and takes a detour through mechanics ("each pretending to be a different kind of expert") at exactly the wrong moment — that's the tension beat, not the place to explain the setup. Sentence 4 is actually two sentences split into one, which muddles the punch.
- "A few weeks ago" is throat-clearing. v0.3 opens with "Every investor has done this dance" — no warm-up. This hook needs the same cold start.
- "Different versions of Claude — each pretending to be a different kind of expert" front-loads the mechanism. The reader doesn't need to know how it works in sentence 3. They need to feel the surprise of the result.
- "Would have lost me real money" is close but pulls its punch. Real money isn't specific enough to sting. "Real position-sizing error" or just "money I didn't want to lose" would hit harder.

**Suggested alternative A** (direct, short sentences):
> I asked Claude to check my investing math. It said my math was fine.
> So I asked five different Claudes — each playing a different expert. Four disagreed with each other.
> One caught a mistake that would have made my risk go up exactly when things got dangerous.

**Suggested alternative B** (cold open, faster):
> Five AIs. Same question. Four different answers.
> That's the thing I'm calling a feature now, not a bug.

Alternative B is riskier but more memorable. It earns the follow-up paragraph faster.

---

### 2.2 Section length variance: §1 250 → §2 300 → §3 300 → §4 250 → §5 250 → §6 150

**Is this right rhythm or monotonous?**

Mostly monotonous. The problem isn't the total word count, it's the shape. Four of six sections are within 50 words of each other (250–300), which means the reader will experience the post as a series of same-size containers. Medium readers don't count words, but they feel the cadence — and this cadence doesn't have a valley or a peak.

**Suggested rebalancing:**
- §1 should be shorter, not 250 words. This is the "problem" section. It should feel tight and uncomfortable — 150 words maximum. Don't explain the problem at length; make the reader feel it.
- §3 (the concrete examples section) should be the longest by a meaningful margin. This is where real trust is built. Expand it to 350–400 words. The three examples (ATR bug, BFSI gap, cross-cycle compounding) each deserve a sentence of context and one sentence of consequence — not just a label.
- §5 (what I learned) should be the second shortest after §6 — around 150 words. It's a landing, not a lecture. If it's 250 words, it's going to feel like the writer didn't trust the examples to land on their own.
- §6 at 150 words is correct if those 150 words are tight. Currently the plan's §6 notes feel loose.

**Revised target shape**: §1 150 → §2 300 → §3 380 → §4 250 → §5 150 → §6 120. Total: ~1350 words of prose + diagrams bring it to ~1500. This gives a curve: short opening, steady build, peak at the examples, principle, quick landing.

---

### 2.3 Diagram cadence: 2 diagrams in 1500–1800 words

**Right ratio for Medium?**

Yes. Two diagrams at this length is correct. Medium readers on a methodology post want one diagram to orient them and one to crystallize the insight. More than two risks making it feel like a slide deck.

**One concern**: Diagram 2 (the "one AI = average opinion" vs "five specialists" comparison) is described in the plan as a Venn-diagram-style flowchart. The mermaid draft provided doesn't achieve that — it's a second fan-out diagram that looks nearly identical to Diagram 1. If they look the same, one of them is redundant. Diagram 2 needs to visually communicate a concept (breadth vs depth of sampling), not just repeat the fan-out topology. Worth rethinking the diagram before drafting. One option: a simple two-column table in prose (not a mermaid diagram at all) for the "average vs specialist" comparison.

---

### 2.4 Bullet vs prose balance: sections at risk of becoming listicles

**§2 setup section** — Currently seven bullets defining the five specialists plus two process bullets. The five specialists especially need to be prose in the draft. "The first is a pure numbers person — they don't care whether the formula makes intuitive sense, only whether the math is sound" reads better than a dashed label with a parenthetical. The role descriptions need texture to earn the reader's investment in what happens next. Flag §2 as highest-risk for bullet-creep.

**§4 principle section** — Four bullet points explaining why multiple AI roles work better than one. Each bullet is declarative and assertive ("One AI is trained on a giant average"). The "still learning" constraint will be violated if these stay as bullets in the draft. The principle section also has the "Bonus:" callout — that framing word reads like a tech-product release note, not a personal essay.

**§5 learnings section** — Six bullets. This is the most dangerous section in the plan. "AI is best as a critic, not as a writer" is actually a strong sentence — but if it's a bullet, it disappears. If the draft renders these as a bulleted list, the section will feel like an "in summary" slide. The plan needs an explicit note that §5 must be prose-only, no bullets.

---

### 2.5 Closing teaser to Blog #3: landing as planned, or overwritten?

**Current plan text:**
> "Next post: one of the actual findings the critics surfaced — a number from a famous investing checklist that, on the data I tested, gave the opposite of the right answer for an entire kind of Indian stock. I'm still investigating, but the pattern is striking enough that I want to share it."

**Verdict: Overwritten and hedged into softness.**

Two problems. First, it's two sentences where one will do. Second, "I'm still investigating, but the pattern is striking enough that I want to share it" is a hedge-inside-a-hedge. The writer is simultaneously claiming the finding is interesting and apologizing for sharing it. That construction is a tic that will show up throughout the draft if it's already in the plan.

The teaser's job is to create exactly one clear appetite. It should be a single sentence, declarative, slightly mysterious. The double-hedge drains the mystery.

**Better version (suggestion):**
> "Next up: a formula from one of the most respected investing checklists — that, on Indian data, consistently flagged the wrong moment to act."

That's it. Let the reader wonder which formula. Let the wrongness land without qualification.

---

### 2.6 Repeated phrases or themes: section overlap risk

**§1 and §5 will overlap.** §1's core point ("single AI gives polite agreement, not real pushback") and §5's core point ("AI is best as a critic, not as a writer / it's most useful when you make it disagree with itself") are the same claim from two angles. A reader who remembers §1 will feel §5 is circling back without adding information.

The fix: §1 should frame the problem as a limitation of the input (one question, one AI), not a criticism of AI behavior. §5 should frame the learning as a change in *how the writer works*, not a restatement of why single-AI fails. They need different verbs and different subjects to avoid overlap.

**§4 and §5 also risk blurring.** §4 explains *why* the technique works (mechanism). §5 explains *what the writer learned* (practical takeaways). In draft form, both sections will be tempted to make similar points about specialist framing. The plan should note: §4 owns the mechanism; §5 owns the behavioral shift in how the writer works. No mechanism explanation in §5.

---

### 2.7 Tone consistency with "still learning" constraint: declarative sentences already in the plan

The following sentences in the plan are already declarative in a way that will violate the tone constraint when carried into draft:

**In §4:**
> "One AI is trained on a giant average of the internet. It tends to give the average answer."
> "Five roles = five different slices. Different slices catch different things."

These are stated as facts, not observations. The draft should reframe: "My working theory is that..." or "What I've noticed is..."

**In §5:**
> "AI is best as a critic, not as a writer."
> "It's most useful when you make it disagree with itself."
> "A synthesis step is non-negotiable."

All three are confident generalizations stated as universal truths. "Non-negotiable" is especially egregious — that's the language of someone who has figured something out and is telling others the rule. In a post with a "still learning" constraint, this reads as tone-deaf. Reframe: "For me, at least, skipping the synthesis step has made things worse — I end up with five opinions and no decision."

**In §1:**
> "The AI doesn't push back unless you ask it to."
> "Even when you ask, it gives polite 'considerations' — not 'you're wrong, here's why'."

These are actually fine — they describe a shared experience, not a lesson the writer has drawn. Keep these.

**In the plan overview:**
> "The synthesizer is the trick — without it, you'd just get five conflicting reviews and no decision."

"The trick" is confident and tidy. In the draft, soften to "the synthesizer is what makes it manageable for me."

---

## §3 Top 5 Sentence-Level Rewrites

**Rewrite 1 — Hook sentence 3** (most important fix)

Current:
> Then I asked five different versions of Claude — each pretending to be a different kind of expert — to check the same math.

Problem: The em-dash interruption explains the mechanism mid-tension. The sentence is doing two jobs at once.

Rewrite:
> So I asked the same question five times — to five different Claudes, each playing a different expert.

Shorter. The em-dash now separates the quantity from the method, not the narrative from the explanation.

---

**Rewrite 2 — §5 "non-negotiable" sentence**

Current:
> A synthesis step is non-negotiable. Without it, you drown in conflicting opinions.

Problem: "Non-negotiable" and "drown" in the same two-sentence block is too confident for the "still learning" frame. The generalization ("you drown") also steps outside first person.

Rewrite:
> Without the synthesis step, I just had five opinions and no decision. That's worse than one AI agreeing with me.

The second sentence earns its place by circling back to the hook's premise.

---

**Rewrite 3 — Closing teaser**

Current:
> "Next post: one of the actual findings the critics surfaced — a number from a famous investing checklist that, on the data I tested, gave the opposite of the right answer for an entire kind of Indian stock. I'm still investigating, but the pattern is striking enough that I want to share it."

Problem: 52 words. Two hedges. Explains its own reasoning for existing.

Rewrite:
> Next up: a formula from one of the most respected investing checklists — that, on Indian data, consistently pointed the wrong way.

19 words. No apology for the cliffhanger.

---

**Rewrite 4 — §4 declarative opening pair**

Current:
> One AI is trained on a giant average of the internet. It tends to give the average answer.

Problem: States a contested technical claim as settled fact. Violates "still learning" tone.

Rewrite:
> My working theory is this: ask one AI and you get the averaged-out version of everything it's seen. Ask it to be a specialist, and it pulls from a narrower, more opinionated slice.

Shifts ownership of the claim to the writer's experience. Also removes the flat verb "tends to."

---

**Rewrite 5 — §6 blog-post-conclusion line**

Current plan note:
> "The investing math is getting better, but the bigger learning is about how to work with AI when the stakes matter."

Problem: This is a polished closing-line that feels constructed. The "X is getting better, but the bigger Y is Z" pattern is a Medium-article cliché — the kind of ending that signals "I have now finished my essay." v0.3's closing ("The work is mine. The accelerant is the AI.") earned its brevity because it didn't explain itself. This line explains itself.

Rewrite:
> The math is getting sharper. But I'm more interested in what I keep missing — and why one AI asking itself the same question five different ways keeps finding it.

Still thematic, but the "why" at the end creates a question rather than closing with a bow. Leaves the reader curious rather than satisfied.

---

## §4 What's Strong Editorially

**The central idea is genuinely sticky.** "Teaching AI to argue with itself" is not a claim that requires defense — the hook earns it immediately with the concrete bug example. This is harder than it sounds to pull off.

**The three examples in §3 are the right examples.** The ATR stop bug (risk goes up when things get dangerous), the BFSI gap (a third of the investable universe was invisible), and the cross-cycle compounding issue (two parts of the system working against each other) are three different *kinds* of failure. That variety matters — it shows the technique catches structural problems, not just arithmetic errors. The plan is right to anchor to these.

**The "one-line nod to prior art" risk flag is good editorial self-awareness.** "I didn't invent this — researchers call it AI debate or jury — but I learned it works for personal use too" does exactly what it needs to do: preempts the "this is just MoA" response without making the post about research history. Keep it, and keep it brief.

**The risks/watch section is the strongest part of the plan.** The flag about "too process-y" and "inside-baseball" language ("agent prompts", "tool use", "background mode") is the right editorial instinct. Most of the problems in the hook and §5 stem from exactly this risk — the writer drifting into mechanism-explanation mode when the reader needs story-and-example mode. The risks section should be read again before drafting each section.

**§3 is structurally the best-designed section.** Three concrete examples, each with a named failure mode and a consequence. If those examples are written in first person with a short "here's why this matters" sentence after each one, §3 will carry the whole post. The plan is correct that this is where the work lives.

---

✅ Editorial review complete. 5 sentence rewrites suggested.
