# Blog Post #2 Plan — Voice Review C4: Voice Authenticity (Human vs AI Tells)

**Reviewer**: C4 — Voice Authenticity (meta-detector for AI-generated prose)
**Plan reviewed**: `blog_post_02_plan.md`
**Voice reference**: `blog_post_01_draft_v0.3.md` (published)
**Date**: 2026-05-31

---

## §1 — Voice Verdict

**NEEDS-VOICE-WORK**

The plan is not AI-dominant. It shows clear evidence that a real person shaped the content — the example choices are specific, the self-deprecating framing ("that was suspicious") is present, the meta-risk list at the bottom is unusually honest. But the draft sentences embedded in the plan carry AI rhythmic signatures that will compound into a draft that reads like a blog post about a human, rather than a blog post by one. The hook has one structural tell that's easy to fix. The closing sentences have two that are harder. The tone constraint (locked: "still learning, not done") is correctly stated but will be the single hardest thing to execute — the plan's own language for describing that constraint is already slightly hedged in the wrong direction.

Left unaddressed, this will pass the other critics and fail the reader's gut check somewhere around §4 or §5.

---

## §2 — Per-Question Voice Analysis

### Q1. The Hook: "I asked X. It said Y. Then I did Z." — human-rhythmic or LLM-rhythmic?

The cadence is:

> A few weeks ago I asked Claude to check my investing math.
> It told me my math was fine.
> Then I asked five different versions of Claude — each pretending to be a different kind of expert — to check the same math.
> Four of them disagreed with each other. One of them caught a bug that would have lost me real money.

This is an extremely common LLM narrative scaffold. The "I did X. It said Y. Then I did Z. One of them [verb] [dramatic outcome]." four-beat structure is recognizable to anyone who reads a lot of AI-generated content. The rhythm is too clean. Each sentence is the same approximate length. The drama escalates in exactly the right increments. The final sentence lands with a neat financial consequence ("real money") that feels placed rather than remembered.

The specific tell is the last sentence: "One of them caught a bug that would have lost me real money." This is the shape of an AI-written reveal. A human writing from memory would be more specific (they'd remember the bug, not just that it was bad) or less neat (they wouldn't land the sentence so squarely on "real money" as the kicker). See §3 for rewrites.

The "a few weeks ago" opening is fine — it's grounding. The "It told me my math was fine" is actually good: it's slightly flat and that flatness is human. The problem is sentences three and four.

**Verdict**: Three sentences are fine. One sentence (the final) is an AI-cadence tell.

---

### Q2. Em-dash count and load-bearing vs decorative

Em-dashes found in the plan:

1. `each pretending to be a different kind of expert —` (hook, §2) — **decorative**. This is a parenthetical that doesn't need an em-dash; a comma or a period-restart would be more natural. The em-dash makes the sentence feel like it was typeset rather than typed.

2. `each one gets the same input. Each one writes their review independently. / Then a sixth one (the synthesizer) reads all five and decides who's right when they disagree.` — no em-dash here, this section is clean.

3. `a risk-sizing formula that, on closer reading, would have made things worse when things got volatile` — no em-dash, also clean.

4. Closing teaser: `I'm still investigating, but the pattern is striking enough that I want to share it.` — no em-dash, but the sentence has a different problem (see Q7).

**Comparison to Blog #1**: The published v0.3 uses zero em-dashes in the main body. There is one stylistic dash-adjacent construction ("Not in the context of *our* rules") but no em-dashes as punctuation. This was not an accident — it was a voice choice. The plan introduces one decorative em-dash in the hook itself, which is the highest-visibility sentence in the post.

**Verdict**: One em-dash in the hook, decorative, should be removed. The rest of the plan is clean. Flag for the drafter: the draft will likely introduce more em-dashes in §4 and §5 (the explanatory sections) because those sections require the most scaffolding and em-dashes are an LLM's default scaffolding tool.

---

### Q3. "The thing is / It's worth noting / Look, ..." tics

These exact phrases don't appear in the plan. But the **functional equivalents** do:

- `"Bonus: forcing the AI to commit to a verdict..."` — the word "Bonus:" is an LLM-explanatory mode label. It means "I am now adding supplementary information that the reader should treat as positive." Humans write "the other thing I noticed was" or just start the sentence. "Bonus:" is a listicle signal.

- `"The cost is: more rounds, more time. The benefit is: the real catches, not vibes."` — this is a structured parallel that an LLM reaches for when it wants to seem balanced. It has the "I'm being fair-minded" shape that is almost always AI-generated in casual prose. A human would not write "The cost is: ... The benefit is: ..." unless they were filling out a form.

- `"What I'm actually trying to solve"` and `"What I'm building, in plain English"` — these are from Blog #1, not the plan, so they don't need flagging here. But note: Blog #1 uses them as section headers. The plan's §4 header is "Why this works (the principle)" — the parenthetical "(the principle)" is an LLM-explanatory label, the same mode as "Bonus:". It telegraphs the section's conclusion before the section runs. Humans rarely subtitle their own sections with what the section is going to prove.

**Verdict**: "Bonus:" and "The cost is: ... The benefit is: ..." are the two phrases to replace. The parenthetical labels in section headers are a softer flag — worth discussing whether the draft keeps them.

---

### Q4. Parallel constructions: "Not X, but Y" / "I'm not trying to X. I'm trying to Y."

The plan contains one explicit parallel that will almost certainly reproduce in the draft:

> `"The bigger picture: I'm not building an investing system as a product. I'm building it to learn"`

This is the canonical AI parallel construction. Subject + "I'm not [A]." Subject + "I'm [B]." It appears in the closing section (§6), which means it will be in the last 150 words of the post — exactly where a human writer's energy drops and an AI's polish increases.

Blog #1's published version contains an echo of this pattern in the subtitle: *"I'm not trying to beat the market. I'm trying to stop getting in my own way."* That line is in the subtitle, where a certain amount of construction is forgivable. Repeating the same skeleton in §6's body copy will feel like a verbal tic the author uses every post.

A second parallel lives in §5:

> `"AI is best as a critic, not as a writer. / It's most useful when you make it disagree with itself."`

These two sentences are syntactically parallel ("AI is best as X" / "It's most useful when Y"). That's fine on its own. The problem is what follows them — three more sentences that continue the same subject-predicate-evaluation pattern. Five consecutive evaluative statements in a row is a list padded out into prose, which is another LLM tell. A human would break the streak with a specific memory or an aside.

**Verdict**: One explicit "I'm not X, I'm Y" construction in §6 — replace it. The §5 evaluation-list needs one human interruption (a specific example or a moment of honest uncertainty) to break the rhythm.

---

### Q5. Polished closing lines: "One of them caught a bug that would have lost me real money."

This is the most important single flag in the plan.

The line is polished in the wrong way. "Real money" is an abstraction performing as a concrete detail. It tells the reader what emotional weight to attach (this was serious) without giving them the thing that would actually make them feel it. A human writer who caught a real bug in their own investing math would write about what the bug was, what they thought when they saw it, or — if they're being brief — something more specific than "real money."

AI-generated prose defaults to "real money" because it's the highest-credibility shorthand for financial stakes. But it's also the most frictionless way to gesture at stakes without committing to them. Any experienced reader of financial content (which is the target audience here) will feel the abstraction even if they can't name it.

**Suggested replacements** (see also §3 for full rewrites):

- "One of them found a formula that was supposed to size down my position when a stock got volatile — and instead it was sizing up. I wouldn't have caught that."
- "One of them flagged something in my risk formula. I checked. It was wrong in the direction that hurts most — the more volatile the stock, the bigger position I'd have taken."
- "One of them found a bug. Not a rounding error — a directional error in my position sizing. I'd have been adding to my riskiest positions right when they were moving hardest."

All three are more specific, less chiseled, and — crucially — they give the reader the bug, not just the consequence. The plan's anonymization guide (§3 examples table) already has the right content: "a risk-sizing formula that, on closer reading, would have made things worse when things got volatile." The hook just needs to use that language instead of "real money."

---

### Q6. The "tone constraint" (LOCKED, still-learning): performed humility vs genuine uncertainty

The tone constraint is stated correctly in the plan:

> `"The post must NOT sound like 'I figured this out, here's the answer.' It should sound like 'I'm trying this, here's what I'm seeing so far, would love input.'"`

The problem is in how the plan then executes on this instruction. The sentence-level cues listed as guidance are:

> `"I think", "early signs", "I'm still figuring out", "open to feedback", "would love to hear from anyone who's tried this differently"`

These are the right intentions but the wrong implementation strategy. When a draft is told to insert "I think" and "I'm still figuring out" at intervals, those phrases become vocal fry — technically present, functionally empty. Readers, especially smart ones, can feel the difference between a writer who is genuinely uncertain and a writer who has been instructed to hedge.

Genuine uncertainty looks like: the writer doesn't know how to end a sentence, so they stop early. The writer contradicts themselves slightly and doesn't fix it. The writer gives a number and then immediately second-guesses it.

Performed humility looks like: "I think this approach works, but I'm still learning." The sentence is structurally complete, the hedge is inserted at a grammatically clean position, and the overall meaning is still confident.

**Prediction**: The draft will use performed humility in §5 and §6. Specifically, the §5 bullet list ("AI is best as a critic, not as a writer. / It's most useful when you make it disagree with itself.") will sound confident throughout — because it's a list of conclusions — and then the draft will insert "I'm still figuring out where this technique works best" as a trailing sentence to balance it out. That trailing sentence will read as performed humility because the eight confident sentences before it make it feel like a disclaimer, not a belief.

**The fix is structural, not lexical**: don't put the uncertainty at the end of confident paragraphs. Put it in the middle of a confident observation, where it actually interrupts the argument.

---

### Q7. The closing teaser: "the pattern is striking enough that I want to share it."

> "I'm still investigating, but the pattern is striking enough that I want to share it."

"Striking" is an AI word in this context. It's the adjective that an LLM picks when it needs to convey "significant but not proven." It's technically precise, it's slightly elevated, and it creates a clean cadence at the end of the sentence. That's exactly why it reads as written rather than said.

A human writing about something they've noticed in their own investing data would not call it "striking." They'd call it "weird," "off," "doesn't add up the way it should," "something I keep seeing," or they'd give up on adjectives and just describe the pattern.

**Suggested replacements**:
- "I'm still checking the numbers, but what I'm seeing is strange enough that I don't want to sit on it."
- "I'm still going through this. But it keeps showing up the same way, so I'm going to write about it."
- "I'm not sure what to make of it yet. But it keeps coming up. Next post."
- "The data keeps pointing the same direction and I don't have an explanation yet. That's what the next post is."

The best replacement is whichever one Pranav would actually say aloud, slightly edited. "Striking" is not a word most people use in conversation about their own work. If he'd say "weird," use "weird."

---

## §3 — Phrase-by-Phrase Rewrite Suggestions

### Hook — sentence 3 (em-dash removal + rhythm fix)

**Current**:
> Then I asked five different versions of Claude — each pretending to be a different kind of expert — to check the same math.

**Problem**: Double em-dash construction. The interrupting clause is too long and too clean. The em-dashes make it feel typeset.

**Suggested rewrites**:
> Then I asked five different versions of Claude to check the same math. Each one was playing a different role — numbers person, behavioral person, someone thinking only about Indian markets.

> Then I asked five versions of Claude the same question. I gave each one a different job: check this like a statistician, check this like someone who only cares about Indian companies, check this like an engineer.

The split into two sentences removes the em-dash problem and adds specificity that makes the setup feel remembered rather than designed.

---

### Hook — sentence 4 (the "real money" tell)

**Current**:
> Four of them disagreed with each other. One of them caught a bug that would have lost me real money.

**Problem**: "Real money" is an abstraction performing as a detail. The cadence is too tidy.

**Suggested rewrites**:
> Four of them disagreed with each other. One found a formula error in my position sizing — the kind where the more volatile the stock, the bigger the position I'd have taken. That's backwards.

> Four of them disagreed. One found something I'd gotten backwards in how I was sizing positions. The more risk, the more I'd have put in. Not less.

The first rewrite adds specificity from the plan's own anonymization guide. The second breaks the sentence into three short pieces, which is more human under pressure (you explain the bad thing, then you say what's bad about it, then you react).

---

### §5 — "The cost is: ... The benefit is: ..." parallel

**Current**:
> The cost is: more rounds, more time. The benefit is: real catches, not vibes.

**Problem**: Structured label-colon-content parallel is a listicle format wearing casual prose clothing.

**Suggested rewrites**:
> It takes more time than asking one AI once. But the catches are real — not "you might want to consider" polite hedging, actual bugs.

> More rounds. More time. That's the real cost. But I haven't gotten "looks fine" from the five-critic version yet on anything that actually had a problem.

The second rewrite is more personal and slightly less tidy. "I haven't gotten 'looks fine' from the five-critic version yet on anything that actually had a problem" is the kind of sentence a person writes when they're still slightly amazed at the result. It reads as observed, not concluded.

---

### §6 — "I'm not building X. I'm building it to Y." parallel

**Current**:
> I'm not building an investing system as a product. I'm building it to learn — and the multi-AI-critique loop is teaching me more than the work itself.

**Problem**: Canonical AI parallel construction. Appears in Blog #1's subtitle in the same skeleton. Two uses of the same pattern within two posts is a tell.

**Suggested rewrites**:
> The investing math is getting better. But I keep noticing that the more useful thing is the pattern itself — ask five, let them fight, read the synthesis. I use it for everything now, not just this.

> I started this to get better at investing. Somewhere in the process the thing I got better at was how to use AI when I actually care about the answer. That wasn't in the plan.

The second rewrite has a natural slight surprise at the end ("That wasn't in the plan") that sounds like a real reflection, not a constructed disclosure.

---

### §6 — Closing teaser: "striking"

**Current**:
> I'm still investigating, but the pattern is striking enough that I want to share it.

**Problem**: "Striking" is elevated LLM vocabulary for this context. The sentence cadence is closed and polished.

**Suggested rewrites** (listed in order of naturalness):
> I'm still going through the data. But it keeps pointing the same direction, so I'm going to write about it.

> Still checking this one. The pattern doesn't go away when I look harder, which is the interesting part.

> I don't have a clean explanation yet. But it keeps showing up the same way — so next post.

> The numbers keep coming out the same way and I don't know why yet. That's the next one.

The best choice is whichever of these would survive an editing pass by someone who knows Pranav's speaking voice. "Striking" would not survive that pass.

---

### §4 — "(the principle)" parenthetical in section header

**Current**:
> ### §4 — Why this works (the principle) (~250 words)

**Problem**: The parenthetical telegraphs the section's conclusion before it runs. It's an LLM's outline-speak leaking into prose structure. If this header survives into the draft as a subhead, it signals the author is explaining rather than sharing.

**Suggested alternatives**:
> ### §4 — The reason it works

> ### §4 — Why it's different from asking one AI

> ### §4 — What I think is actually happening here

The third option ("What I think is actually happening here") is the most human and also does the most voice work — it signals genuine speculation rather than settled explanation.

---

### §5 — "Bonus:" label

**Current**:
> Bonus: forcing the AI to commit to a verdict (ACCEPT / NEEDS REWORK / REJECT) makes it less mushy. "There are some considerations" becomes "this is broken because X".

**Problem**: "Bonus:" is a listicle/tutorial label. It signals that the writer is itemizing value-adds, which is a content-marketing mode, not a personal-learning mode.

**Suggested rewrites**:
> The other thing I didn't expect: asking it to give a verdict — accept, rework, reject — instead of "thoughts" changes the output completely. "There are some considerations" becomes "this formula is broken because X." Same AI, different question shape.

> One thing I didn't see coming: when I forced each reviewer to give a verdict (not just feedback, but accept / needs work / reject), the outputs got sharper. Less hedging. More actual decisions.

Both remove the "Bonus:" framing and replace it with a surprise register ("I didn't expect," "I didn't see coming") which is more consistent with the "still learning" tone constraint.

---

## §4 — What Rings Authentically Human in the Plan

This section matters as much as the flags. The plan has real human moments that the draft should preserve and amplify.

**1. "That was suspicious. So I changed how I asked."**

This is the best sentence in the entire plan. It's short. The logic is implicit. "That was suspicious" is a real cognitive reaction, not an explained one. The draft should find ways to give the reader more of this — reactions without full explanations. Blog #1 does this well in the "I sell winners too early. I tell myself I'm 'booking profits.' I'm getting nervous." sequence.

**2. The three concrete examples in §3 are genuinely specific.**

The ATR stop bug, the BFSI gap, the cross-cycle compounding issue — these are the kind of details that are only in the plan because they actually happened. They're messy, they have specific numbers (a third of the investable universe), and they're not symmetrical with each other. AI-generated examples tend to be tidier. These aren't. Preserve that asymmetry in the draft.

**3. The risk list is unusually honest.**

> "Self-congratulatory: 'look how clever I am' is the wrong tone."
> "Pretending it's new: this technique is widely used in AI research."

These risk flags are the writer policing their own tendencies. An AI plan would not include "Pretending it's new" as a risk — it would just not make that mistake, or it would make it and not notice. The fact that this is flagged explicitly suggests the author has thought about the audience's likely objection. That's human metacognition.

**4. The title options.**

Option 2 ("One AI agrees with you. Five AIs catch your mistakes.") is the most human of the three candidates — it sounds like something you'd say to a friend to explain why this matters, not something you'd write for a headline. Option 1 is playful but slightly workshopped. Option 3 is the most AI-cadence of the three ("Why I stopped trusting one AI for one answer" is a classic LLM title structure: "Why I stopped X" = performed epiphany).

**5. The "I'll add a one-line" self-awareness.**

> "I'll add a one-line 'I didn't invent this — researchers call it AI debate or jury — but I learned it works for personal use too'."

This is a good human instinct and a good voice move. It's low-key, it gives credit, and it preempts the "this is nothing new" objection without a defensive paragraph. The draft should keep this and probably expand it slightly — one sentence in the post body, positioned before §4's explanation, would do more work than one at the end.

---

## Summary: AI-Tell Phrase Count

**Total flagged**: 9 specific phrases or constructions requiring rewrite

| # | Location | Phrase / Construction | Type of tell |
|---|---|---|---|
| 1 | Hook, sentence 3 | Double em-dash parenthetical | Typeset rhythm |
| 2 | Hook, sentence 4 | "would have lost me real money" | Abstraction-as-detail |
| 3 | §5 bullets | "The cost is: ... The benefit is: ..." | Label-colon parallel |
| 4 | §6 | "I'm not building X. I'm building it to Y." | Canonical AI parallel |
| 5 | §6, closing teaser | "the pattern is striking enough" | Elevated AI vocabulary |
| 6 | §4 header | "(the principle)" parenthetical | Outline-speak leaking into prose |
| 7 | §5 | "Bonus:" label | Listicle/tutorial mode signal |
| 8 | §5, evaluation list | Five consecutive evaluative statements | Rhythm tell — list padded into prose |
| 9 | §6, uncertainty trailing | "I'm still figuring out where this works best" as trailing disclaimer | Performed humility tell (structural) |

The draft will need a voice pass after the first complete draft is written. The pass should happen sentence by sentence on §4, §5, and §6 — the explanatory sections are where the rhythm standardizes. §1 through §3 have enough specific detail to anchor the human voice if the examples are handled well. The closing 300 words are the highest-risk zone.

---

`✅ Voice review complete. 9 AI-tell phrases flagged.`
