# Blog Post #3 Plan — Editorial Review (C2)
**Reviewer**: C2 — Editorial / Writing Quality
**Date**: 2026-05-31
**Status**: 🔄 Initialized — reading plan + Blog #1.

---

🔄 Read complete. Drafting editorial verdict.

---

## §1 — Editorial Verdict

**NEEDS-REWORK** (plan, not draft)

The bones are good. The core idea — a famous checklist misfires on cyclicals, here is why, here is what I do instead — is a publishable argument. The data point (F=5 → +355% versus F=8 → +34%) is the kind of single, concrete, memorable reversal that Medium's better investing readers will screenshot and share.

But the plan has structural writing problems that will produce a flat draft unless they are fixed at the plan stage. The hook needs tightening. The §5 / §5b split is an editorial awkwardness that will read as a seam. The "Stock X / Stock Y" naming convention is a memory tax on the reader. The §4 reframe carries a tonal risk that requires a deliberate editorial choice, not an accidental one. And the closing to Blog #1 + #2 is currently written as a signpost, not a landing.

Fix these in the plan now. The draft should not carry these ambiguities into v0.1.

---

🔄 §1-§2 done. Drafting §3-§4.

---

## §2 — Per-Question Feedback

### Q1 — The hook (6 sentences): punch and pacing

**Verdict: Cut to 5 sentences. One sentence is dead weight.**

The hook currently runs:

> 1. If you read Indian investing books or watch the popular YouTube channels, you've probably heard about the Piotroski F-Score.
> 2. It's a 9-point checklist. Score 8 or 9, and the company is supposedly a strong buy. Score 3 or below, and it's a sell.
> 3. A few months ago I built it into my own investing system and tested it on real Indian stocks. The first few tests went fine.
> 4. Then I tested it on a commodity stock at the bottom of its cycle. The score said: avoid this. The stock then went up 355% over two years.
> 5. I tested it at the peak of the same cycle a year later. The score said: strong buy. The stock then matched the market — boring.
> 6. The checklist is giving the opposite of the right answer for this kind of stock. Here's why, and here's what I do instead.

Problems:

- **Sentence 1** is obligatory scene-setting. It does not create tension. A Medium reader with enough investing literacy to know the F-Score does not need to be told they've heard of it. Consider cutting entirely or folding into sentence 2. The hook should start with something surprising, not something affirming.
- **Sentence 2** is fine — compact and factual.
- **Sentence 3's second clause ("The first few tests went fine")** is throat-clearing. It tells the reader "nothing interesting is coming yet." Delete it. The sentence should end at "real Indian stocks" and the next beat should be the surprise.
- **Sentences 4–5** are the strongest two sentences in the entire plan. The parallel structure (score said X / stock did Y) is exactly right. The em-dash on "boring" works.
- **Sentence 6** is a competent closer but slightly bland. "Here's why, and here's what I do instead" is functional, not compelling.

Revised hook (5 sentences, cuts the dead weight):

> The Piotroski F-Score is a 9-point checklist. Score 8 or 9 and the company is a strong buy. Score 3 or below and it's a sell.
> A few months ago I tested it on a commodity stock at the bottom of its cycle. The score said: avoid this. The stock went up 355% over the next two years.
> A year later I tested the same stock at the top of its cycle. The score said: strong buy. The stock matched the market — boring.
> The checklist was giving the opposite of the right answer. And I had nearly built it into my investing system as-is.
> Here's what I figured out — and what I do differently now.

This version: starts with the rule (not the reader's assumed knowledge), delivers the contradiction in sentence 4, adds a personal-stakes beat in sentence 4b ("nearly built it in as-is"), and closes with forward motion.

---

### Q2 — §3 table: prose paragraph, table, or both?

**Verdict: Keep the table. Add one prose paragraph before it, not after.**

The table is the right call for this specific argument. Four rows, four columns, one clear inversion — it lets the reader see the pattern in a single eye-movement. On Medium, a clean, scannable table is more compelling than the same information embedded in paragraphs.

But the plan currently drops the reader into the table cold. The risk: readers who skim will read the numbers and miss the frame. Before the table, the draft should include one short paragraph (3 sentences maximum) that tells the reader what they are about to see. Something like:

> I computed the F-Score by hand from annual reports at four historical dates. I also noted what the stock actually did over the following two years. The table shows what the checklist said — and what happened next.

After the table, the prose should name the pattern explicitly, which the plan already does ("the score was most excited at the worst moment"). That sequencing — brief frame → table → explicit pattern naming — is solid editorial structure for number-heavy claims.

One concern: the §3 table has a row ("March 2024 — F=6 — incomplete window, lagging") that is functionally a footnote. Including an unresolved data point in the central evidence table weakens the argument. Two options for the draft: (a) cut the March 2024 row and note in prose that the four-year window is still open; (b) move it to a footnote below the table. Do not leave it as a row-peer of the other three.

---

### Q3 — Math-prose integration: keeping numbers from killing read-flow

**Verdict: The plan is correctly cautious here, but two specific traps need naming.**

The plan already calls for "no Greek symbols, no Σ" — that is the right instinct. But the plan also includes a section (§6) that describes a 5-year-average modification to the F-Score. That section risks introducing a second numerical framework mid-post without enough narrative bridge.

Two specific rules for the draft:

**Rule A — One number at a time.** Each number should appear in a sentence where it is the only number, or at most one of two. "The score at March 2020 was 5 out of 9" is one number (5). "The score was 5, the stock was at ₹400, the PE was 8" is three numbers in a single sentence — readers stop processing and start scanning. The draft should enforce one-number-per-sentence in prose sections; save multiple numbers for table cells.

**Rule B — Anchor numbers to outcomes, not to formulas.** The plan does this well in §3 (F=5 → +355%). The risk is §6, where the modification is explained numerically ("5-year average instead of year-on-year") without an accompanying outcome number to make it concrete. The draft should include at least one illustrative calculation: "Using the 5-year average, the March 2020 score for Stock X comes out as X — which would have said [buy/hold/sell]." If this calculation is not yet available, note it as a drafting gap.

---

### Q4 — The 7-section structure: rhythm and the §5 + §5b split

**Verdict: The §5 / §5b split is an editorial seam. Merge or rename.**

The word counts as planned:

| Section | Planned words |
|---|---|
| §1 What is the F-Score | 250 |
| §2 How I tested it | 300 |
| §3 What the numbers showed | 400 |
| §4 Why this happens | 250 |
| §5 The non-cyclical contrast | 300 |
| §5b How to spot stocks where F-Score misleads | 150 |
| §6 What I do instead | 250 |
| §7 Closing | 150 |

Overall rhythm is fine. The 400-word §3 as the heaviest section is correct — the evidence should get the most space. The 150-word §7 closing is tight but workable given the tone constraint ("still learning, not done").

The problem is §5b. It is 150 words on a new subpoint stitched beneath §5 because it fits thematically there, but it is not logically a continuation of §5 (which is a worked example of Stock Y). §5b is a reader-assistance device: "how do you know if you're looking at a cyclical?" That is a different job from showing Stock Y's numbers.

Two options:
- **Merge §5b into §6**: The transition from "here are cyclical industries" to "here is what I do differently for those industries" is natural. §5b's checklist becomes the opening of §6, and §6 expands to ~350–400 words.
- **Rename §5b as §6 and renumber §6 → §7 and §7 → §8**: This makes the section count 8, which is slightly long but more honest about the architecture.

The merge (option 1) is cleaner. The combined §5b+§6 at ~400 words matches §3 in weight, which would give the post two heavy sections — the evidence and the so-what — which is the right shape.

---

### Q5 — The "F-Score never said this was for cyclicals" reframe (§4): tone

**Verdict: As written in the plan, it skirts snarky. The draft needs one careful sentence.**

The plan's §4 key line:

> It's not that Piotroski is wrong. It's that **he never said this was for cyclicals.** The original paper was about value stocks. The Indian investing community quietly extended it to all stocks. That extension is where the problem lives.

The word "quietly" is the tonal risk. It implies the Indian investing community knew it was an extension and did it anyway — i.e., that there was some kind of concealment. That is an uncharitable read that is probably not what is meant. But "quietly extended" reads as: "they slipped it past us." That framing will trigger defensiveness in the exact readers who use the F-Score.

Replacing "quietly extended it" with something that attributes the extension to honest enthusiasm rather than concealment changes the tone completely:

> The original paper worked on US value stocks. Indian books picked it up — reasonably — because it makes sense as a quality filter. But they applied it across all stocks, and cyclicals were never part of the original test.

This version says the same thing ("extension = the problem") without the insinuation. The tone should be: "the tool traveled further than its testing." Not: "someone was careless or misleading."

The plan's voice constraint ("I'm still learning, not the authority") makes this even more important. The "quietly extended" framing is the voice of someone who has caught the community out. That conflicts with the "learner sharing a pattern" posture the post is trying to hold.

---

### Q6 — Closing chain to Blog #1 + #2: self-promotional or natural?

**Verdict: Natural if executed as context, not as traffic links.**

The plan's closing:

> "If you want to follow along: [link to blog #1] explains what I'm building and why. [Blog #2 link] is about how I make the AI argue with itself to find these things."

This is fine in principle. The links are earned — Blog #3 is a product of the same project, and the reader deserves to know there are predecessors. The risk is execution: if the links appear in a final paragraph that reads like a newsletter footer, they feel promotional. If the link to Blog #1 appears naturally as context *within* the post — "this came out of a system I'm building [link], which I wrote about here [link]" — they feel like citations.

The specific editorial recommendation: move the Blog #1 link to §1 (where the post is introducing the personal project context) and the Blog #2 link to §4 or §6 (where the "AI arguing with itself" methodology is relevant). Do not save both links for the final paragraph. Final paragraphs on Medium get skimmed or skipped; links buried there generate low clickthrough and feel like afterthoughts.

The §7 closing should end on the learning, not on the links.

---

### Q7 — "Stock X" / "Stock Y" variable naming: will readers remember?

**Verdict: No. Rename with a descriptor, not a variable.**

"Stock X" and "Stock Y" are programmer notation, not reader notation. A Medium reader will not reliably remember which is the cyclical and which is the stable business by the time they reach §5. The forgetting happens at the section break, which in a 2000-word post comes around the 1000-word mark.

The plan is correct to anonymize. But anonymization does not require opacity. Two options:

**Option A — Descriptive short-names**: "the metals stock" and "the paints stock." These are plausible without being identifying (there are multiple metals and paints companies). The reader carries the characteristic, not an arbitrary letter.

**Option B — Industry-role labels**: "the cyclical" and "the compounder." These are analytically honest and the post uses both terms anyway. The reader is reminded of the distinction every time the name appears.

Option A is more natural for a Medium readership. Option B is more precise but risks sounding like a finance lecture. Either is better than Stock X / Stock Y. The draft should pick one and be consistent.

One additional note: the plan already uses "Company A" and "Company B" in Blog #1 for the same two stocks (Tata Steel / Asian Paints). Stock X / Stock Y in Blog #3 introduces a new naming convention for what appears to be the same underlying companies. If Blog #3 readers have read Blog #1, this is confusing. The naming convention should be consistent across the series, or Blog #3 should acknowledge the re-labeling.

---

## §3 — Top 5 Sentence Rewrites

All rewrite targets are from the plan text.

---

**Rewrite 1 — Hook sentence 1 (remove the scene-setting, start with the rule)**

Original:
> If you read Indian investing books or watch the popular YouTube channels, you've probably heard about the Piotroski F-Score.

Problem: Reader-flattery opener. Assumes shared familiarity as a bonding device. Does not create tension.

Replacement:
> The Piotroski F-Score is a 9-point checklist used to judge whether a company is financially improving or deteriorating.

Why: This works for the reader who knows the F-Score (reminder, not insult) and the reader who doesn't (clean one-sentence intro). It does not presuppose the reader's media consumption habits.

---

**Rewrite 2 — Hook sentence 3 (cut the throat-clearing clause)**

Original:
> A few months ago I built it into my own investing system and tested it on real Indian stocks. The first few tests went fine.

Problem: "The first few tests went fine" defers the surprise and signals to the reader that nothing interesting has happened yet.

Replacement:
> A few months ago I built it into my own investing system and tested it on real Indian stocks.

Why: Hard stop. The next sentence delivers the contradiction immediately. No buffer needed.

---

**Rewrite 3 — §4 "quietly extended" (remove the insinuation)**

Original:
> The Indian investing community quietly extended it to all stocks. That extension is where the problem lives.

Problem: "Quietly" reads as either stealth or negligence. Both are uncharitable and will produce defensive comments.

Replacement:
> Indian investing books picked it up — reasonably — and applied it across all types of stocks. Cyclicals were never part of the original test. That's the gap.

Why: Attributes extension to good-faith adoption, not concealment. Puts the word "reasonably" in the sentence, which signals the author is not condemning the community. "That's the gap" is a short, factual landing — no sarcasm.

---

**Rewrite 4 — §5b / §6 transition (currently absent — needs a bridging sentence)**

Current plan implies a hard section break between §5 (Stock Y worked example) and §5b (which cyclicals mislead the F-Score). No transition is specified.

The draft will need something like:

Replacement (bridging sentence at the top of merged §5b/§6):
> The difference between these two stocks comes down to one question: does the company's business have a cycle?

Why: One sentence, no jargon, carries the reader from "here is the contrast" to "here is how to think about it." It also reinforces the central argument without restating it.

---

**Rewrite 5 — §7 closing link sentence (move the ask, sharpen the landing)**

Original plan:
> "If you want to follow along: [link to blog #1] explains what I'm building and why. [Blog #2 link] is about how I make the AI argue with itself to find these things."

Problem: "If you want to follow along" is a weak CTA phrasing. The two-link dump at the end turns the closing into a nav menu.

Replacement (final sentence of §7, after links are moved earlier in the post):
> I tested this checklist expecting it to work. It didn't — not here, not on this kind of stock. That gap is what I'm building toward closing.

Why: Ends on the project's emotional logic, not on a link. Quiet, first-person, consistent with the "still learning" voice constraint. Does not ask the reader to do anything — which is the correct posture for a learner's post.

---

## §4 — What Is Editorially Strong

**1. The central data point is genuinely surprising and memorable.**
F=5 → +355% versus F=8 → +34% in a parallel table is the kind of inversion that makes a reader stop scrolling. This is not manufactured — it is real data from the hand-compute work — and the plan handles it with appropriate restraint (one stock, four dates, "not statistical proof"). The combination of real surprise plus honest scope-limiting is editorially mature.

**2. The "coincident indicator, not leading indicator" framing is precise without being jargon-heavy.**
The plan's core reframe — "the F-Score tells you how things are today; for cyclicals, today is already too late" — is a clean, correct, and accessible way to explain a genuinely non-obvious insight. It does not require the reader to know what "coincident indicator" means; the post explains it in ordinary language.

**3. The voice constraint ("still learning, not final") is built into the plan at the right level.**
The plan does not just say "be humble." It gives specific sentence-level cues ("from what I'm seeing," "I might be wrong about this," "would love feedback from anyone who's tested this"). That specificity will survive into the draft and will keep the post from reading as a contrarian takedown, which is the primary tonal risk for this material.

**4. The two-stock structure is the right architecture for this argument.**
Showing the F-Score failing on Stock X and then showing it working on Stock Y is a stronger argument than showing it failing alone. The contrast proves the point is surgical — the checklist is not broken everywhere — which preempts the most obvious pushback. The plan locks this correctly.

**5. The diagram plan is well-scoped.**
Four to five mermaid diagrams for a 2000-word post is the right density. Diagrams 2 and 4 (the parallel timelines for Stock X and Stock Y) are the high-value visuals, and the plan correctly identifies them as the "central visual argument." The optional Diagram 5 (two-column F-Score works / doesn't work) is the one that risks being redundant with the prose in §5b — worth evaluating during drafting rather than committing to it now.

---

✅ Editorial review complete. 5 sentence rewrites.
