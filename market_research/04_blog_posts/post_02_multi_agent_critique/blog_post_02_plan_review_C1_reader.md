# Blog Post #2 Plan — Reader Review
**Reviewer**: C1 — Target Reader (Indian retail investor, 30s)
**Date**: 2026-05-31
**Plan reviewed**: `blog_post_02_plan.md`
**Reference**: `blog_post_01_draft_v0.3.md` (published predecessor)

---

## §1 — Bottom-line verdict

**KEEP** — with two structural fixes before drafting.

The plan is stronger than most "AI + investing" content I'd skim past on Medium. The hook is earned, the examples are real, and the one-takeaway framing is unusually disciplined. But §4 (why this works) is a real skim-risk, and the "still learning" tone will evaporate the moment a draft writer defaults to explaining mode. Those two things need solving at the plan stage, not after the draft is written.

---

## §2 — Per-question responses

### Q1: Does the hook make you keep reading past sentence 4?

Yes — barely, and "barely" is fine for Medium.

The four sentences work because they move: "I asked" → "it agreed" → "I changed the question" → "one of them caught a real bug." That's a cause-effect chain, not a preamble. The phrase "bug that would have lost me real money" is the right kind of specific. It doesn't tell me the math. It tells me the consequence, which is what I care about.

The one risk: sentence 3 ("five different versions of Claude — each pretending to be a different kind of expert") is doing a lot of work. "Pretending to be" might make a skeptical reader stop and roll their eyes — it sounds like a party trick. Blog #1 handled the AI-tool framing more matter-of-factly. Recommend swapping "pretending to be" for "each playing a different role" or just "five different reviewers, each with a different job." Keep the concept; lose the word "pretending."

### Q2: Will you understand "5 specialists, one question" by §2 — or is it too abstract?

Clear enough, but the five roles as currently named are uneven. "The numbers person" and "the Indian-market person" land immediately — I understand what they care about without needing an explanation. "The integrator" is opaque on first read. An integrator of what? The plan says "how this new thing connects to what I built earlier" — but if I'm coming from Blog #1, "what I built earlier" means the Nefarious project broadly, and I'm not sure what I'm integrating into.

The diagram helps. Mermaid fan-out is the right visualization for this — it makes the independence of the five reviewers visually obvious. But the diagram lands better if each node has a one-line descriptor of what that role catches, not just its name. "Indian-market person" is clearer than "C3" in the diagram, so the naming is already good; just make sure the descriptions in the prose for each role are one sentence each, not two.

The synthesizer explanation ("reads all five and decides who's right when they disagree") is the clearest sentence in §2. Keep that exact phrasing in the draft.

### Q3: Are the 3 anonymized examples in §3 compelling — or too vague?

Two of three land. One doesn't.

**Risk-sizing bug (B-W5 ATR stop)**: This is the strongest example. "Position size goes UP when volatility goes UP — the exact opposite of what I wanted" — that's a concrete, intuitive failure. I don't need to know what ATR is to understand why this is bad. The anonymization is fine because the failure is described in plain cause-effect terms. Keep it.

**BFSI gap (B-W6)**: "A third of the big Indian companies I actually care about were being silently skipped" — this is good. "Silently skipped" is the right phrase, because it captures the hidden-failure quality of the bug. Every Indian retail investor knows what BFSI companies are; you don't need to name them. The anonymization works here.

**Compounding-parts (B-W1, cross-cycle)**: This one loses me. "Two parts of my system, when combined, were worse than either part alone — because they were both reading the same delayed signal from underneath." The phrase "from underneath" does nothing for me. What does "from underneath" mean? The concept being described — two signals that look independent but are correlated, so combining them adds noise not signal — is real and interesting. But the current phrasing sounds like technical inside-baseball even with the anonymization. The example needs a plain-English analogy. Something like: "I was using two different sensors that both turned out to measure the same thing. Combining them didn't give me more information — it just counted the same mistake twice." Then say that's what happened to two parts of my investing system.

### Q4: Does the "still learning, not final" tone come through in the structure — or will the draft default to authoritative?

It's structurally fragile. The plan names the tone constraint correctly and gives good sentence-level cues ("I think", "early signs", "I'm still figuring out"). But the structure of §3 and §5 creates an authority drift problem.

§3 is written as a discovery narrative ("here's what changed when I did X") — that's fine, discovery is first-person and humble. But the three bullet examples are framed as findings, not observations. "The numbers person caught a dangerous bug" reads as a verified result, not an in-progress learning. In the draft, every example in §3 needs a cue like "what struck me was..." or "I hadn't noticed that..." before the technical description. Otherwise the section reads as a proof of concept, not a learning journal.

§5 (what I learned) is the highest structural risk. A list of five lessons about working with AI — even if each is stated tentatively — will read as an authoritative guide in draft form unless the writer is actively fighting against that frame. The plan should either add a tone constraint at the top of §5 ("each of these is provisional — I'm seeing early evidence, not confirmed patterns") or restructure §5 as a running reflection rather than a numbered takeaway list. A numbered list is the enemy of the "still learning" tone.

### Q5: Is §4 (why this works) too theoretical — would you skim it?

Yes, I would skim it, and I'm exactly the target reader.

The core explanation — "one AI gives the average answer; five specialists give five different slices" — is genuinely interesting and I'd want to read it. But the plan bundles it with a second diagram and a technical detour about "ACCEPT / NEEDS REWORK / REJECT" verdicts. The verdict framing is inside-baseball. I don't need to know the AI was forced to commit to a verdict type — I need to understand why five opinions are more valuable than one.

The fix: cut §4 to 150 words maximum. Keep the "average of the internet" framing — that's a useful mental model for a ChatGPT user. Cut the verdict-category explanation entirely (or fold it into a single clause in §5). Use the second diagram only if it adds something the prose doesn't already say; right now the two-subgraph diagram in the plan restates the prose without adding visual information.

If §4 is tight and concrete, I'll read it. If it runs to 250 words, I'll scroll past.

### Q6: Does §5 (what I learned about working with AI) feel like real reflection or filler?

In the plan it reads as both. The bullet list has a real insight ("AI is best as a critic, not as a writer") and a non-insight ("the cost is: more rounds, more time") packed side by side without hierarchy. The last bullet ("I'm using this same pattern for everything serious now — not just investing") is the most interesting and least developed. That sentence implies I can use this for work, for writing, for decisions — and then doesn't go anywhere with it.

The section will feel like real reflection if: the draft picks the two strongest learnings and develops them with a specific moment, not a generalization. "AI is best as a critic, not a writer" is interesting only if there's a one-sentence memory attached: what happened when I tried to use it the other way. The plan leaves this as a summary claim. The draft needs a scene.

"I'm using this same pattern for everything serious now" — if this sentence has one real example outside investing (a decision, a piece of writing, a professional judgment call), it broadens the post's relevance without changing its focus. Worth adding to the plan as a note.

### Q7: Does the closing teaser to Blog #3 make you want to wait for the next post?

Yes. This is the strongest structural decision in the plan.

"A number from a famous investing checklist that, on the data I tested, gave the opposite of the right answer for an entire kind of Indian stock" — that's a setup I'd read. "Famous investing checklist" + "opposite of the right answer" + "an entire kind of Indian stock" is specific enough to be credible and vague enough to leave a gap. I know enough from Blog #1 to guess this is about Piotroski or one of the similar signals; that prior knowledge makes the tease more compelling, not less.

The only thing to watch: "I'm still investigating, but the pattern is striking enough that I want to share it." That's the right tone. Make sure the draft doesn't smooth this into "here's what I found" — the uncertainty is the point.

### Q8: 1500-1800 words — right length, or adjust?

Right length. Do not cut to 1200.

Blog #1 established a reader expectation of depth. The audience that came from Blog #1 via Medium recommendation is not skimming — they followed through a specific topic and they're willing to read. 1500-1800 with two diagrams and three concrete examples is justified by the content density.

The caveat: length only works if §4 is cut (as recommended in Q5) and the words are redistributed to develop §5 and flesh out the third example (compounding-parts). The total word count stays the same; the weight shifts toward reflection and away from theory.

---

## §3 — What's missing from the plan that I'd expect as a reader

**1. A moment of doubt.**
Blog #1 earned trust by admitting that the textbook math pointed the wrong direction on Tata Steel. That's the kind of admission that separates Saurabh Mukherjea-style credibility from generic AI hype content. Blog #2's plan is mostly structured around "here's what the multi-agent critique caught." But did this process ever catch something that turned out to be wrong? Did a critic agent flag a problem that I investigated and concluded wasn't actually a problem? One false-positive from the critique process, named and explained, would make the rest of the findings more believable.

**2. Cost and time — with a real number.**
The plan mentions "more rounds, more time" as a cost. But I'm a retail investor reading this on a Sunday morning. I want to know: does this take 20 minutes or two hours? One sentence with a real estimate ("each full critique round takes me about X") would make this feel like a tool I could actually use, not an AI researcher's workflow.

**3. What triggered the switch to multi-agent.**
The hook implies the switch happened because single-AI agreed with me and that was suspicious. That's a good hook. But somewhere in §1, I'd want one more sentence: what made the "it agreed" moment feel wrong? Was it that the math was obviously non-trivial and I expected pushback? Was it that I knew I'd made a shortcut somewhere? The switch from "one AI" to "five specialists" was a decision. Give me the moment of doubt that preceded the decision, not just the description of the new method.

**4. How replicable is this for me.**
I use ChatGPT casually. Can I replicate "five specialists + synthesizer" in ChatGPT without building anything? Or does this require something technical that I, as a retail investor, can't run? The plan never answers this. Even one sentence — "this runs in Claude's project feature, not in any special software; you can try it in a standard chat window" (or "this requires X") — would resolve the implicit question I'd be carrying through the whole post.

---

## §4 — What's strong in the plan from a reader's perspective

**The one-sentence takeaway is exactly right.**
"When AI agrees with you, you've learned nothing. The trick is to make it disagree — with itself." That's a sentence I'd screenshot and send to someone. It's punchy, it's counter-intuitive, and it doesn't require context from Blog #1 to land. Whatever else changes in the draft, that framing needs to survive verbatim.

**The hook structure is disciplined.**
Four sentences, one cause-effect chain, consequence in the last sentence. The plan is right to treat this as non-negotiable. Blog #1's opening paragraph ("every investor has done this dance") worked because it opened with a universal scene. Blog #2's hook is stronger because it opens with a specific failure and a resolution — it's a more active structure.

**The risks section is honest and actionable.**
"Too process-y", "inside-baseball", "self-congratulatory", "over-anonymized", "pretending it's new" — every one of these is a real failure mode for this kind of post, and naming them in the plan is the right move. The plan catches itself before the draft can make those mistakes. The note about "AI debate / jury / MoA" existing as a research pattern, with a one-line credit, is particularly good — it preempts the "this isn't novel" criticism without making the post about the research literature.

**The synthesizer framing is the best idea in the plan.**
Most people who try multi-agent AI stop at "I got five different answers and they conflicted." The synthesizer — a sixth agent that reads all five and decides — is the part that makes this actually usable. The plan foregrounds this correctly. The draft should make the synthesizer feel like the insight, not an afterthought.

**Blog #3 teaser is earned.**
The teaser works because Blog #1 established a reader who trusts the author's process. "I'm still investigating" signals intellectual honesty. "Famous investing checklist" narrows the inference space just enough to make the tease credible. This is the right hook for continuity — it rewards loyal readers without requiring context to land for new ones.

---

✅ Reader review complete. Verdict = KEEP (with two structural fixes: cut §4 to 150 words; restructure §5 away from a numbered list before drafting).
