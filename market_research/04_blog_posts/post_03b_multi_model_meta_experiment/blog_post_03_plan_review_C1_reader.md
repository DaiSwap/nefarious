# Blog Post #3 Plan — Review C1 (Target Reader: Indian Retail Investor)

**Reviewer role**: Returning reader, Indian retail investor, 30s, white-collar. NIFTY 100 + MFs. Read Blogs #1 and #2. Not a builder or AI researcher.
**Date**: 2026-06-06
**Plan reviewed**: `blog_post_03_plan.md` v0.3

---

## §1 — Bottom-line verdict

**KEEP — but with one structural fix required and several clarity adjustments.**

The plan is worth executing. The topic is legitimate, the framing is honest, and the engagement with the senior critique is genuinely useful to a returning reader. But §2 (open questions from prior blogs) has a placeholder problem that, if unresolved, will make the post feel incomplete or slightly dishonest. And the plan risks losing me — a non-builder reader — twice: once in §3–§5 if the methodology language gets too technical, and again in §7 if it feels like the author is accepting the critique intellectually but not actually changing anything I can observe.

The post reads like it was written for a builder audience with a retail reader in the footnotes. That's the wrong ratio for this arc.

---

## §2 — Per-question responses

### Q1 — Does it read as a natural continuation of Blogs #1 and #2, or does it feel like a tangent?

**Mostly yes — but the thread is thinner than it looks.**

Blogs #1 and #2 had a clear anchor: the investing project. Blog #1 was "here is my problem and why I'm solving it." Blog #2 was "here is a technique that made the AI actually useful." Both posts gave me something tangible about the project itself — a bug that was caught, a formula that was wrong, a real gap about HDFC Bank and ICICI being excluded.

Blog #3's plan is primarily about the method, not the project. The question it answers — "is the multi-agent technique sound?" — is meaningful to a builder. For me, as a retail investor, it's interesting only because I care about whether the tool Pranav is building is actually reliable. If the critique undermines the technique, I want to know. If he's fixing it, I want to see what that means in practice.

The plan addresses this, but §6 (the experiment I'd run) and §7 (what I'm changing now) are where the investing relevance lives — and they're buried at section 6 and 7 of 8. The structural risk is that a retail reader arrives expecting progress on the investing project and encounters 600 words of AI methodology critique before getting there. The continuation is real, but the plan needs to pull the "so what for my trust in this tool" thread forward, not leave it as an implicit conclusion.

One thing that helps: the critique is not abstract. It's about the specific pipeline Pranav used to catch a bug in a risk formula I read about in Blog #2. That makes it feel like the arc is continuing, not stalling.

### Q2 — Does the 5-sentence hook make you keep reading?

**Yes — barely. But the fifth sentence is doing all the work.**

The first two sentences are recap. I already know what Blogs #1 and #2 were about. If I've read both, I don't need to be reminded in the lede. This is the classic "Part N" problem: the explicit callback signals continuation but delays payoff.

The third and fourth sentences are where it starts to matter to me: "a thoughtful comment... pointed out something I hadn't quite let myself see." That's the opening I'd want to read. The admission that he hadn't quite let himself see something is honest and not precious — it makes me want to know what the thing was.

The fifth sentence — "The technique might be doing less work than I'd claimed" — is the best sentence in the lede. As someone who trusted his description of the technique in Blog #2, this lands. It's a direct acknowledgment that what I was told might have been overstated.

If I were editing: collapse sentences 1–2 into one clause, move the actual critique ("same blind spots") into the lede itself rather than saving it for §3. The hook currently front-loads recap and delays the hook. A non-builder reader needs to know what the structural problem is in the first paragraph, not just that a problem exists.

The Part 3 framing is helpful, not off-putting — but only because Blog #2 ended with a clear "next post" promise, and this delivers on a related theme. The arc holds.

### Q3 — Does §2 (answering open questions from prior blogs) feel earned or self-indulgent?

**It can't be evaluated yet — and that's a real risk.**

The plan explicitly flags that Blog #1 reader feedback content is a placeholder. §2 as described in the plan asks Pranav to surface "3–4 specific concerns/suggestions that came back across both blogs," and the Blog #1 examples are marked "(placeholder — needs Pranav's input on actual reader feedback)."

This is an honesty problem in the plan, not the post — but it matters for the review.

If the Blog #1 feedback content is real and specific, §2 will feel earned. A returning reader likes being told "here's what other people asked, and here's what I think." It makes the series feel responsive.

If the "feedback" is generic or invented to fill the section — people asked whether I'm using this on my real portfolio, people asked what the bot can see that I can't — then §2 will feel like the author is having a conversation with an imaginary reader. That's self-indulgent, and an Indian retail investor who has been around bloggers and influencers will spot it immediately.

The fix is simple: don't write §2 until Pranav has the actual feedback. If there isn't enough specific feedback from Blog #1 to fill a section, compress §2 to one paragraph of genuine synthesis and move on. A short honest section beats a long constructed one.

The Blog #2 material for §2 is fine — the senior comment is real, and smaller suggestions like adversarial prompts are directly referenced in the feedback file.

### Q4 — Are §3–§5 accessible to a non-builder reader, or does methodology lose me?

**§3 is accessible. §4 is borderline. §5 is where I start to skim.**

The plan's framing for §3 is good: "Three concerns spelled out plainly." And the concerns as listed are plain: same model = same blind spots; synthesizer is also the same model; role prompting creates false confidence. None of those require me to understand AI training pipelines to follow the logic. The "different slices, same well" analogy in §4 is exactly the right level.

§4 holds up on the nuance point — "the question isn't 'useless or useful.' It's 'how much of the value is real, and how much is theatre.'" That's a sentence a retail reader can carry. It's the framing I'd use to explain this post to someone who hadn't read it.

§5 is where I start to feel the builder-audience pull. "Cross-model diversity," "adversarial framing," "output-format normalization," "catch rate" — these are engineer's terms dressed in plain words but still oriented at someone building something. What I need from §5 is not a technical evaluation of three fixes. I need one clear answer: is the tool Pranav is building trustworthy enough that I should believe the catches it reports? That's my question as a retail reader, and §5 doesn't answer it directly.

The plan should add a one-sentence retail translation at the end of each fix in §5. Something like: "For you as a reader: this means the bug it caught in my risk formula was still a real catch, even with this limitation." That one sentence per fix keeps me in the post.

### Q5 — Does "I haven't actually run the experiment yet" feel honest or weak?

**Honest. Genuinely.**

This is the strongest call in the plan. The alternative — running a fake experiment or a small experiment and overclaiming — would be worse. Blog #1 was credible because Pranav did the math by hand and showed the work. Blog #2 was credible because the catches he described were specific and falsifiable (the risk formula bug, the HDFC gap). If Blog #3 had claimed empirical data it didn't have, a careful reader would notice.

"Here is the experiment I would run, here is its design, I haven't run it yet" is honest and still useful. The Mermaid diagram of the three-arm design gives me something concrete to look at. The invitation to someone with multi-model access to run it is the right move.

The only risk is if this section runs long. The design is simple — three arms, a human reads all three, count the overlapping catches. That's it. Don't pad it. 200 words and a clear diagram is better than 300 words and a diagram.

### Q6 — Does §7 ("what I'm changing now without empirical data") feel actionable or like the author is moving on without evidence?

**Borderline. Two of the four changes feel real. Two feel like placeholders.**

Change 1 (adversarial framing for the synthesizer specifically) is real and specific. A prompt that says "find the disagreement between these five reviews" instead of "synthesize them" is a concrete change. I can picture it.

Change 2 (a written checklist for the human-as-arbiter step) is real. "I write down what I'm looking for" is a practice change I can understand.

Change 3 ("cross-model is on the 'as soon as practical' list") is the weakest of the four. "As soon as practical" is the thing you say when you're not doing it yet and don't know when you will. I understand why it's there — the budget/access constraint is real — but as written it reads as a non-commitment. It would help to add one sentence about what "practical" means: "Once I have access to the Gemini and GPT APIs, this is the first thing I'm testing." A date, even approximate, would be better than "as soon as practical."

Change 4 (the original Blog #2 advice still stands with caveats) is important for the arc but feels slightly defensive. It's the author reassuring himself more than informing me. Keep it brief.

For a retail reader, §7 works if changes 1 and 2 are concrete and visible in the work he shares next. If Blog #4 shows a synthesis that uses adversarial framing and Pranav's checklist, this section will be validated retroactively. If Blog #4 doesn't reference it, §7 will look like good intentions.

### Q7 — Does the "still learning" tone sound genuine or performed?

**Genuine — with one specific risk.**

The "still learning" tone in the plan's voice constraints is correctly calibrated: "I think," "as far as I can tell," "I haven't actually run this yet." These hedges are appropriate because the post explicitly doesn't have empirical data. The plan is right to lean into them.

The risk the plan itself identifies — "self-flagellation tone: thanking the commenter once at the end is fine; multiple times = performative humility (an AI tell)" — is exactly right, and it applies beyond just the thank-you. Anywhere the post hedges more than twice in a single paragraph, it will read as the AI writing itself into a corner. The draft should be checked for clustering of hedges.

The one moment that could tip into performance is §8 (what I still don't know). Four consecutive "I don't know" statements followed by an open invitation risks reading as the author performing intellectual humility rather than stating a genuine limit. Fix: frame §8 as "here are the specific things I want to find out next" rather than "here are all the things I don't know." It's the same content but it reads as forward-looking rather than self-deprecating.

The thank-you at the close is fine. One sentence. Keep it.

### Q8 — Is 1500–1800 words the right length for Part 3?

**Yes, 1500 words. Not 1800.**

Blog #1 established the project. Blog #2 introduced the technique and showed specific catches. Blog #3 is an accountability post — it engages with a critique and reports on updates. That's a narrower mandate than Blog #2, which had the original technique to explain plus three specific catches to walk through.

At 1800 words, Blog #3 risks overstaying its welcome. The post doesn't have a "the formula was wrong and here is the moment I realized it" beat — it has reasoning and design. Reasoning and design compress more tightly than narrative.

Target the lower end: 1500 words, maybe 1600. If the actual draft runs to 1750, it's fine. But don't pad §2 or §8 to hit 1800.

---

## §3 — What's missing that a returning reader would expect

**1. What happened to the next post that was promised in Blog #2.**

Blog #2 ended with: "Next post: one of the actual findings the critics pushed me toward. A famous investing checklist that, on the data I tested, gave me the opposite of the right answer for one kind of Indian stock. I'm still digging into it."

That was a direct promise of a specific investing post. Blog #3 is not that post. The plan doesn't acknowledge this pivot. A returning reader who remembered that promise will notice immediately that Blog #3 is not what was teased, and might wonder whether the Piotroski/F-Score finding was abandoned.

The fix is one sentence in §1: "I said the next post would be about a specific investing finding. I'm getting to that — but this came first." That's enough. Don't over-explain. Just acknowledge the redirect.

**2. Whether the catches from Blog #2 still hold up.**

Blog #2 described three specific catches: the risk formula bug, the HDFC/ICICI coverage gap, and the echo problem between two signals. Readers who trusted those catches on the strength of the five-agent technique might now wonder: if the technique is flawed, were those catches real? Were they confirmed by a method that was doing less work than claimed?

The plan doesn't address this directly. §4 has the right idea with "the technique still does something" — but it needs to make this explicit: "The three things I told you about in Blog #2 — yes, those were real catches. The limitation I'm describing now is about the technique's ceiling, not about whether those specific findings were wrong."

This is the most important missing piece for a retail reader who took the Blog #2 content seriously.

**3. Concrete forward motion on the investing project itself.**

Blog #1 and Blog #2 both ended with the project moving. Blog #1: "The next phase is fixing the parts that failed and adding the parts I haven't built yet." Blog #2: "Next post" with a specific content promise. Blog #3 as planned ends with "I don't know / open invitation." That's honest — but it leaves a retail reader with no sense of where the project is going.

One sentence in §8 about what Phase 3 of the project looks like — even vague — would close the loop. "While I figure out the technique question, I'm continuing to build the technical analysis piece of the tool. More on that next." The retail reader doesn't need a roadmap. Just a signal that the project is alive.

---

## §4 — What's strong

**The one-thing framing is right.** "A model critiquing itself five times is not the same as five different perspectives" is a sentence a retail investor can carry out of the post and repeat to someone else. It's the kind of formulation that makes a blog post worth reading. Keep it central.

**The commitment to honesty about the experiment is strong.** The plan explicitly tables "what is and isn't claimed in this post" — that table belongs in the plan but not the blog, but having it in the plan means the draft will stay honest. The decision not to fake empirical data is correct and will read as credibility-building to anyone who remembers Blog #1's approach of testing formulas by hand before trusting them.

**"How much is real, how much is theatre."** This phrase from §4 is the best articulation in the plan. It's precise, it's non-technical, and it's honest about the ambiguity without being self-deprecating. Draft should keep this close to the surface.

**The "human-as-arbiter" elevation is exactly right for a retail reader.** In Blog #2, I noticed that Pranav was the final decision-maker and the AI was advisory — but that was a footnote in §4, not the headline. Making it explicit in Blog #3 that human judgment is non-negotiable is reassuring. As a retail investor who was worried about blindly trusting the AI's priority list, this is the most useful thing Blog #3 could say. The plan elevates it. Good.

**The diagram for the experiment is appropriately simple.** Three arms, one human, one comparison. It's the right level of specificity for a post that is describing a design rather than reporting results. Don't add the optional "same-well" diagram — one diagram is the right call for this post.

**The risk section in the plan is unusually self-aware.** "Sounds like a retraction," "sounds like we're proving the critic right just to look thoughtful," "self-flagellation tone" — these are exactly the failure modes a returning reader would notice. The plan is correctly worried about the right things.

---

*Review complete.*
