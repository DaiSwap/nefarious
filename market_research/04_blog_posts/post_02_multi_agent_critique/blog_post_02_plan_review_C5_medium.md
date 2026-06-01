# Blog Post #2 — Medium Platform Fit Review (Reviewer C5)

**Plan reviewed**: `blog_post_02_plan.md`
**Blog #1 tone reference**: `blog_post_01_draft_v0.3.md`
**Reviewer lens**: Medium-specific — curation logic, bounce window, title patterns, subhead quality, diagram rendering, tags, CTA mechanics.

---

## §1 — Medium-Fit Verdict

**NEEDS-OPTIMIZATION**

Not a write-off. The raw material here is strong: a concrete personal story, a real technique with measurable results ("20+ specific things wrong" vs "looks good"), and a tone that fits Medium's first-person confessional register. Blog #1 set the right precedent. This post can follow it into curation — but not in the current planned form.

The specific blockers:

1. **Title candidate #1 (recommended title) is good for click-through but structured in a way that Medium curators deprioritize.** The verb "taught" is past tense and resolved — it implies the story is over and packaged. Medium's curation team favors titles that feel like the author is mid-journey, not delivering a lesson.

2. **The hook survives the bounce window on narrative grounds, but fails the "number in sentence 1 or 2" test.** Medium's 30-second bounce is beaten most reliably by a number, a loss, or a named specific in the first two sentences. The draft hook opens with "a few weeks ago" — vague time — and "my investing math" — vague stake. The concrete number (20+ things wrong, or the money-losing bug) arrives too late.

3. **At 1500–1800 words (~7–8 min read), this post sits just above Medium's curated sweet spot of 4–7 min.** Marginal overrun, but it matters for curation scoring. Fixable.

4. **Two mermaid diagrams in a post this length will cause problems.** Mermaid does not render reliably on Medium when copy-pasted from markdown. Unrendered diagram blocks look like raw code, which spikes bounce rate and signals low quality to the curation algorithm. This is a known Medium friction point.

These are all fixable before drafting begins. The verdict would upgrade to CURATED-CANDIDATE with the four changes outlined in §4.

---

## §2 — Per-Question Medium Analysis

### Q1 — Title ranking for Medium curation

**Ranking (best to worst for Medium curation probability):**

**1st: "One AI agrees with you. Five AIs catch your mistakes."** (Candidate #2)

This is the strongest curation candidate. Reasons:
- Two short declarative sentences. Medium curators and the algorithm both favor this sentence rhythm for tech/investing crossover posts.
- "Agrees with you" is a mild confrontation — it puts the reader in the story immediately.
- "Five AIs" is a specific number. Numbers in titles outperform vague claims on Medium's click-through data in AI-adjacent categories.
- The structure is a before/after tension. Medium curators are trained to read this as "there's a technique inside."
- It does NOT have the word "I" in it, which paradoxically performs better in curation (feels less like a personal diary, more like a useful observation).

**2nd: "How I taught my AI to argue with itself"** (Candidate #1, current recommendation)

This is the better Twitter/LinkedIn title — it is playful, clever, and works for warm audiences already following the project. On Medium cold-discovery (which is what curation unlocks), it underperforms because:
- "How I" constructions are overrepresented in Medium's AI category. Curators actively weight against them now.
- "Taught ... to argue with itself" is abstract without a concrete payoff in the title itself. The reader has to infer that the result is useful.
- It is a good title for a post that already has a following. It is a weak title for cold acquisition, which is what curation is for.

**3rd: "Why I stopped trusting one AI for one answer"** (Candidate #3)

Weakest for curation. "Why I stopped" is the most saturated construction in Medium's personal-essay AI category. Search it: thousands of posts with this exact pattern. Curators skip over it automatically. It also promises a negative (stopping a behavior) rather than a positive (a technique that works), which underperforms in Medium's tech/investing crossover readership.

**Click-through ranking** (warm audiences, existing followers, social shares): Candidate #1 > #2 > #3.
**Curation likelihood ranking** (cold discovery, algorithm, editorial team): Candidate #2 > #1 > #3.

If the goal is Medium curation (which is the main platform-fit question), the answer is Candidate #2.

---

### Q2 — The hook (first 30-second bounce window)

**Verdict: Survives on narrative. Fails on the number-in-sentence-1-or-2 test.**

The current four-sentence hook:

> A few weeks ago I asked Claude to check my investing math. It told me my math was fine. Then I asked five different versions of Claude — each pretending to be a different kind of expert — to check the same math. Four of them disagreed with each other. One of them caught a bug that would have lost me real money.

What works:
- Sentence 3 is excellent. "Five different versions of Claude, each pretending to be a different kind of expert" is specific enough to create curiosity. This is Medium-grade writing.
- Sentence 5 ("would have lost me real money") is the right emotional note. It is stakes without melodrama.
- The voice is first-person and honest. That matches what Medium curators are looking for in this category.

What fails:
- Sentence 1 ("A few weeks ago") is a time-vague opener. Medium analytics show that vague temporal openers ("recently," "a few weeks ago," "last year") correlate with faster bounces than openers that begin with a concrete number, a loss value, or a named action. The reason is simple: vague time signals that the writer is warming up, not already inside the story.
- Sentence 2 ("It told me my math was fine") is good, but the implied risk is not yet visible. The reader does not know whether "my math" is about groceries or a ₹50 lakh portfolio position.
- The concrete number (20+ things wrong) is buried in §3, not the hook. It should be in sentence 1 or 2.

One possible fix that keeps the voice: "I asked Claude to check an investing formula. It said the formula was fine. It would have made my position sizes go up during the most volatile periods — the exact opposite of what I wanted. I only found the bug when I asked five different versions of Claude, each playing a different expert. Four of them disagreed with each other. One of them caught it." This moves the concrete failure to sentence 3, before the technique reveal. The original draft reveals the technique before the failure, which slightly weakens the tension.

This is a draft note, not a requirement for the plan. But the plan should flag: do not let the hook open with a vague time marker.

---

### Q3 — Subhead quality (Medium table of contents / skimmability)

Medium's table of contents shows on desktop for posts with 4+ subheads. Skimmers who hit the TOC decide within 5 seconds whether to read. The current section titles:

| Current title | Problem | Punchier alternative |
|---|---|---|
| §1 — The problem with asking one AI for one answer | Descriptive, 9 words, no hook | "The AI Said Fine. It Wasn't." |
| §2 — The setup: five specialists, one question | Adequate. "Setup" is weak. | "Five Versions of Claude. One Question." |
| §3 — What changed when I started doing this | Vague ("this"), process-feel | "The Bug Single Claude Missed. The One That Would Have Cost Me." |
| §4 — Why this works (the principle) | Parenthetical "(the principle)" reads like a textbook | "Why Five Opinions Beat One (Even When They Disagree)" |
| §5 — What I learned about working with AI this way | Long, generic | "What I'd Tell Anyone Who Trusts One AI" |
| §6 — What this means for my project | Inward-facing, reader-excluded | "What I'm Doing With This Now" |

The alternatives above are suggestions, not mandates. The main note for the plan: §3 is currently the most generic title and it contains the most valuable content (the three real catches). Its title should surface the stakes, not describe the process.

---

### Q4 — Diagram pacing (2 mermaid diagrams, 1500–1800 words)

**Verdict: The diagrams will hurt unless exported as PNG before upload.**

The specific Medium problem with mermaid:
- Medium's editor does not render mermaid natively. If you paste raw mermaid markdown, it appears as a code block. Code blocks inside a personal-essay post signal "this is a technical doc, not a story." The bounce rate on posts that open with raw code blocks is measurably higher than posts that lead with prose.
- Even if mermaid is rendered in an external tool and embedded as an image, Medium's image sizing is unpredictable on mobile (where >60% of Medium reads happen). A complex flowchart with 6 nodes and labeled arrows often becomes unreadable below 375px width.

The two specific diagrams:
- **Diagram 1 (fan-out + synthesizer)**: Genuinely useful. The five-critic-to-synthesizer structure is the core technique. A reader who sees this diagram understands the post's value proposition in 3 seconds. Worth keeping — but export as PNG at 2x resolution, add a caption, and center it. On mobile, consider whether the node labels are readable at 300px width. The current node text ("Consolidated review + priority list of fixes") will be unreadable at mobile scale.
- **Diagram 2 (one AI vs five AI comparison)**: Lower marginal value. The concept it illustrates ("one AI = average answer, five AI = different slices") is already clear in prose in §4. A diagram that restates text adds visual bulk without adding comprehension. Recommendation: cut Diagram 2, replace with a single bolded pull-quote or a two-column text comparison (which Medium renders reliably). Save the mermaid budget for Diagram 1, which is doing real work.

Net recommendation: keep Diagram 1 as PNG export, cut Diagram 2. This also reduces word count and tightens the post toward the 4–7 min sweet spot.

---

### Q5 — Tags strategy (top 5 ranked)

Medium's tag system determines which topic feeds the post appears in. Each tag is a feed with its own subscriber base and editorial attention level. The goal is to maximize feed coverage while staying relevant enough that readers who arrive do not immediately bounce.

**Recommended top 5 tags, ranked:**

1. **Artificial Intelligence** — Highest subscriber base in Medium's tech category. This post qualifies because the technique (multi-agent critique, role-playing specialists) is genuinely about AI methodology, not just AI as a tool. Do not use "Machine Learning" — that feed skews toward academic/research posts and this is not one.

2. **Investing** — Medium's investing feed has strong curation attention from editors. Posts that combine a personal story with a technique that readers can use tend to get picked up. This post fits that profile.

3. **India** — The Indian retail investor angle is the post's most specific differentiator vs. the sea of generic AI-and-finance posts. The India tag puts it in front of the audience most likely to share it. It also gives the curation team a hook: "AI investing technique, written from an Indian retail investor perspective" is a specific angle editors like.

4. **Personal Finance** — Broader than Investing. This tag catches readers who are AI-curious but not investing-focused. The post's §5 ("What I learned about working with AI this way") and §4 principle are relevant to anyone using AI for any decision with stakes, not just investing. The "Personal Finance" tag expands reach without misrepresenting the post.

5. **Productivity** — Counter-intuitive but defensible. The multi-agent-critique technique is fundamentally a productivity/workflow improvement: you get better output from AI by restructuring how you ask. Medium's productivity feed has readers who are looking for exactly this type of "here's a specific system I built" post. "Personal Development" (from the original candidate list) is too soft for this post — it reads as self-help, which this is not.

**Tags to avoid**: Machine Learning (too academic), Indian Stock Market (too niche, low subscriber base on Medium), Data Science (wrong register for this post's voice).

---

### Q6 — CTA and closing structure

**Verdict: The closing teaser is good but incomplete as a Medium CTA.**

The current closing:

> "Next post: one of the actual findings the critics surfaced — a number from a famous investing checklist that, on the data I tested, gave the opposite of the right answer for an entire kind of Indian stock. I'm still investigating, but the pattern is striking enough that I want to share it."

What this does well:
- Concrete promise. "The opposite of the right answer for an entire kind of Indian stock" is genuinely interesting — it is not a vague "more next time."
- "I'm still investigating" matches the locked tone perfectly ("still learning, not done").
- It functions as a good story-bridge to Blog #3.

What it does not do:
- It does not ask the reader to follow. Medium's recommendation engine weights "follows gained per post" as a quality signal. A post that ends with a compelling teaser but no "follow" ask leaves conversion on the table.
- It does not ask a question of the reader. Blog #1's closing ("I'd like to hear one thing: what's the one decision you keep making that you wish a tool would help you stop making?") was a specific, answerable question. Specific questions generate responses. Responses are a curation signal. Blog #2's current closing has no equivalent.
- It does not acknowledge the reader's situation. The best Medium CTAs make the reader feel seen, then ask something of them. This one only advertises the next post.

Recommended addition (after the teaser, two sentences): "If you've tried getting AI to push back on your own work — investing or otherwise — I'd genuinely like to know what broke first. And if you want to see what the critics surfaced in blog #3, following here is the easiest way to catch it."

This adds ~35 words and adds a question, a follow-ask, and a reason to follow — all of which Medium's recommendation engine can read.

---

### Q7 — Read time vs Medium sweet spot

**Verdict: Slightly long. Fixable without structural cuts.**

1500–1800 words at Medium's standard reading speed (265 wpm) = 5.7–6.8 min.
Medium's curation-favored range: 4–7 min (medium.com's own editorial guidance, still current).

At the plan's target length, this post is inside the curation window — but only barely, and only if the draft lands at the lower end (1500 words). If the draft runs long on examples (§3 has three detailed examples, each with explanatory prose), it will push into 7–8 min, which is outside the sweet spot.

The single most effective lever is §4: cutting Diagram 2 saves ~150–200 words of surrounding prose (intro to diagram, explanation of diagram, transition out). That alone keeps the post inside the window even if the examples in §3 run slightly long.

Secondary lever: §5 ("What I learned about working with AI this way") lists 5 bullet-style learnings. On Medium, bullet lists in personal essays often read as padding. Converting §5 from a list to 2–3 tight paragraphs, each built around one insight with a sentence of personal experience, typically reads as 20% shorter and feels more like essay than process doc.

---

## §3 — Title Recommendation

**Single best pick: "One AI agrees with you. Five AIs catch your mistakes."**

Reasoning:

This is the only candidate that works for cold Medium discovery (curation + algorithmic distribution) *and* tells the reader exactly what the technique is. A reader who has never heard of this project, never read Blog #1, and stumbles on this in the AI feed knows in 9 words what the post is about and why it is relevant to them.

"How I taught my AI to argue with itself" is the better title for the Nefarious project as a series — it has personality, it is playful, it signals continuity with Blog #1. It should be repurposed as the subtitle or as the opening line of §4 (where the "arguing with itself" framing actually fits the explanation of why the technique works).

One concern with Candidate #2: "Five AIs" may confuse readers who do not know that you are using the same AI with different role prompts, not five different AI products. The body copy should clarify this early — something like: "Not five different AI products. One AI, five different roles. Each one asked to care about a different thing." This prevents the most likely misread.

---

## §4 — Specific Medium-Platform Tweaks for the Draft

These are platform-mechanics recommendations, not voice or content changes.

**1. Move a concrete number into sentence 1 or 2.**
The 30-second bounce window is won or lost on the first two sentences. "A few weeks ago" should become something with a number or a specific loss. Options: "I nearly built a formula that would have made my position sizes go up during the most volatile days." Or: "Twenty-three things were wrong with my investing math. One AI found none of them." Either version beats a vague time opener.

**2. Export Diagram 1 as PNG at 2x resolution. Cut Diagram 2.**
Mermaid blocks in Medium look like code, not diagrams. PNG export with a descriptive caption is the correct workflow. Diagram 2 is redundant with the prose in §4 — cut it and save the 150+ words for sharpening the three examples in §3.

**3. Bold the three concrete catches in §3, each on its own line, before the explanation.**
Medium readers who skim (majority) will land on bold text. If the three big finds — the position-sizing bug, the BFSI gap, the compounding problem — are bolded as 1-line summaries before the paragraph explanations, skimmers get the value without reading every word. Non-skimmers get the same value with more context. This is a structural skim-proofing technique that Medium's top-performing posts use consistently.

**4. Add a follow-ask to the closing CTA.**
Two sentences after the Blog #3 teaser (see §2 Q6 above). Medium's recommendation engine reads follow-rate as a quality signal. Not asking for a follow is leaving a curation signal unconverted.

**5. Revise §3's subhead to surface the stakes.**
"What changed when I started doing this" describes a process. "The Bug One Claude Missed" (or a variant) describes a result with stakes. Skimmers who see the TOC and land on §3 via a subhead click should know before they click that something went wrong and was caught. That subhead revision alone will improve in-post scroll depth.

**6. Tags order in the Medium editor.**
Medium uses the first tag listed as the "primary" tag for its recommendation engine. Set "Artificial Intelligence" as tag 1. The AI feed has the highest subscriber count and the most active curation team for posts in this space. Set "India" as tag 2 — it is the most differentiating signal.

**7. Subtitle (Medium shows this in previews).**
The plan does not specify a subtitle. Blog #1 had one: "I'm not trying to beat the market. I'm trying to stop getting in my own way." That subtitle was doing real work — it pre-answered the "why should I care?" question before the reader clicked. Blog #2 needs an equivalent. Suggested draft: "A technique for making AI push back harder — and what it found in my own investing math." This fits Medium's subtitle character limit and tells the reader there is a personal story plus a transferable technique.

---

*Reviewer: C5 — Medium Platform Fit*
*Plan version reviewed: blog_post_02_plan.md (initial)*
*Blog #1 tone reference: blog_post_01_draft_v0.3.md*
