# Reviewer C5 — Medium Platform Fit
# Blog Post #3 (replacement) Plan Review

**Reviewer lens**: Medium-specific — bounce window, title mechanics, subhead quality, image pacing, tags strategy, CTA structure, recommendation engine, series treatment.
**Date**: 2026-06-06
**Plan reviewed**: `blog_post_03_plan.md` v0.3

---

## §1 — Medium-Fit Verdict

**NEEDS-OPTIMIZATION**

The bones are strong. The word-count target (1500–1800, ~7–8 min) lands squarely in Medium's curation sweet spot. The voice — first-person, honest, builder-learning-in-public — is a template for what Medium curators reward in technology writing. The subject matter (AI methodology critique from a commenter, public accountability) maps well to Medium's "working openly" genre, which performs better than pure explainers in the AI tag.

The problem is distribution. This plan is optimized for a reader who has already read Blogs #1 and #2. On Medium, the recommendation engine does not deliver posts in series order. A reader arriving from Medium's home feed or the AI tag will encounter this post cold. Several structural choices — the lede, §1 and §2 subheads, the recommended title — assume prior acquaintance and will cost cold reads within the first 30 seconds. Those choices are fixable without touching the substance.

One structural issue is not fixable by edits alone: this is a reasoning-and-design post without empirical data, and it is the third post in a row. Medium curators have low tolerance for "part N of series" when the post does not close a loop on its own. This post closes loops (it accepts a critique, proposes fixes, describes an experiment) but its standalone readability depends on how aggressively the author rewrites the entry points.

The verdict is NEEDS-OPTIMIZATION, not WON'T-PERFORM. The path to CURATED-CANDIDATE is specific and achievable.

---

## §2 — Per-Question Analysis

### Q1. The 5 candidate titles: rank for Medium curation likelihood

Curation rankings, from most to least likely to be picked up:

**Rank 1 — Candidate #4: "The unfixable problem with one model critiquing itself — and what I'm doing about it"**

This is the strongest title for Medium curation. It is standalone-readable: a new reader understands the subject, the tension, and the promise of a resolution without having read anything prior. It names a specific problem ("one model critiquing itself"), applies a provocative adjective ("unfixable"), and qualifies it with action ("what I'm doing about it"). The em-dash construction is a proven Medium pattern — it sets up a tension and immediately signals the post resolves it. The title works for the AI tag, the Productivity tag, and the Personal Finance adjacent reader who is curious about the methodology under the investing application.

**Rank 2 — Candidate #3: "A senior pushed back on my AI agent post. Here's what I think about it."**

Close second. The word "senior" signals there is a real person with authority involved, which creates human stakes. "Here's what I think about it" signals opinion, which Medium's recommendation engine favours over pure explainers. The weakness: "my AI agent post" is vague. Someone arriving cold does not know what that post was about, and the ambiguity may not be enough to pull the click. But the story shape — someone credible challenged me, I responded honestly — is a reliable Medium performer.

**Rank 3 — Candidate #2: "I wrote two posts about my investing-bot project. Then the real feedback started."**

The narrative hook works. "Then the real feedback started" is a punchy pivot. The weakness for curation is the explicit series framing ("two posts about my investing-bot project") — it tells a new reader this is a continuation before giving them a reason to care. Curators will notice this. Still performs better than the recommended #1 and #5.

**Rank 4 — Candidate #1: "Two posts in, here's what the comments taught me" (plan's recommended choice)**

This is the plan's recommended title and it is the fourth-strongest for Medium specifically. "Two posts in" is a continuation signal in the opening phrase, which is a structural problem on Medium. A reader on the home feed or a tag page sees "Two posts in" and immediately calculates that they are missing context. Medium's first-read audience is not Series followers — it is tag-discovery readers. The accountability tone ("what the comments taught me") is appealing, but the access cost is front-loaded. This title will perform well on an email list or a Substack where subscribers know the arc. On Medium, it undercuts discoverability.

**Rank 5 — Candidate #5: "Update on the project — and the critique I had to take seriously"**

Weakest title. "Update on the project" is pure continuation language with no hook for a new reader. "The critique I had to take seriously" is strong but arrives as an afterthought after the least interesting phrase. Do not use this title on Medium.

**Summary table**:

| Rank | Candidate | Curation score | Standalone-readable |
|------|-----------|---------------|---------------------|
| 1 | #4 — "The unfixable problem with one model critiquing itself..." | Highest | Yes |
| 2 | #3 — "A senior pushed back on my AI agent post..." | High | Mostly |
| 3 | #2 — "I wrote two posts about my investing-bot project..." | Medium | Partial |
| 4 | #1 — "Two posts in, here's what the comments taught me" | Medium-low | No |
| 5 | #5 — "Update on the project..." | Low | No |

---

### Q2. The hook (5-sentence lede): Does it survive the 30-second bounce window for a NEW reader?

**Short answer: No, not as written.**

The lede as drafted:

> I've written two posts about this project so far — one about why I'm building a personal AI to argue with me about my own portfolio, and one about the technique I use to make the AI actually push back. Both posts got real feedback. A thoughtful comment on the second post in particular pointed out something I hadn't quite let myself see: when all five agents I describe run on the same model, they share the same blind spots. The technique might be doing less work than I'd claimed. This post is me sitting with that — and with the other questions both posts left open.

Sentence 1 is entirely about establishing that this is a continuation. For a returning reader, this is reassuring. For a first-time reader, it is two clauses of "you should have read other things before this." By the time the reader reaches the actual insight — "when all five agents I describe run on the same model, they share the same blind spots" — they have already been told they are missing context twice.

Medium's bounce window is roughly 30 seconds before a non-committed reader closes the tab. That is long enough to read approximately 100 words with normal scan behaviour. The first 100 words of this lede spend 60 words on series positioning and 40 words on the actual idea.

The insight itself — same model, same blind spots, five agents is not five perspectives — is immediately gripping to any reader who has used AI for anything. It does not require knowledge of Blogs #1 or #2. It requires only that the reader has ever tried to use AI to check their own work, which is a large portion of Medium's AI-tag readership. The lede buries this.

The fix is sequencing, not substance. Lead with the insight. Then explain the context. The commenter's critique and the series backstory can arrive as sentence 4 and 5. This does not change the plan's content — it changes the order in which the reader encounters it.

---

### Q3. Subheads — §1 ("Where we are in the project arc") and §2 ("The open questions from the first two posts")

**Both subheads are explicit-continuation markers and will hurt for first-time readers.**

On Medium, readers who have not read previous posts will scan subheads before committing to body text. "Where we are in the project arc" signals three things to a cold reader: (1) there is an arc, (2) you are not at the beginning of it, (3) this subhead is not written for you. Many cold readers will scan past §1 entirely as a result, missing the summary of Blogs #1 and #2 that the plan intends as orientation material.

"The open questions from the first two posts" has the same problem. "The first two posts" is a hard signal that the reader has homework to do.

These subheads are also in the wrong order for a cold reader. A cold reader needs the insight first, then the context. The plan runs context (§1, §2) before insight (§3, §4). This is correct for a newsletter subscriber who already wants the update. It is incorrect for a Medium discovery reader who needs to be sold on why they should care before being oriented.

Proposed alternative subheads that preserve the content but change the signal:

- §1: "What this project is about, in 200 words" — explicitly acknowledges the reader may not know, and promises brevity.
- §2: "Three questions that came back from readers" — removes the series-dependency language while keeping the accountability framing.

The difference is that the proposed versions invite a cold reader in rather than signal that they are already behind.

---

### Q4. Diagrams — 1-2 mermaid diagrams in a 1500-1800 word methodology post

**Right cadence, but with one critical rendering caveat.**

For a 7-8 minute post about methodology, one diagram is almost mandatory and two is the ceiling. The three-arm experimental design diagram (Arm 1 / Arm 2 / Arm 3 feeding into a human arbiter) is the right diagram to include — it converts a 300-word description into something scannable in 5 seconds, which is valuable for the builder-audience who will be looking for the experiment structure.

The optional "same-well" diagram for §3/§4 is worth including only if it is simple enough to land at first glance. If it requires the reader to study it, drop it. The writing in §4 (same training data, same compression, same blind spots) is clear enough to stand alone.

The critical caveat: the plan already notes that Mermaid renders weakly on Medium and recommends exporting as PNG. This is correct and essential. The Medium editor accepts image uploads; Mermaid code blocks do not render as diagrams in the published post unless the publication is using a custom integration. PNG exports from the Mermaid live editor (mermaid.live) are the right path. Without this step, both diagrams will appear as code blocks, which breaks the reading experience and signals technical naivety to the curators who review posts for the AI tag.

---

### Q5. Tags strategy — same set as Blog #2, or different?

**Blog #2's tag set (AI / Investing / India / Personal Finance / Productivity) should be partially replaced.**

This post is materially different from Blog #2 in subject matter. Blog #2 is primarily about an investing application with an AI methodology underneath. Blog #3 is primarily about AI methodology — the investing application is context, not the subject. The tags should shift accordingly.

Recommended tags for Blog #3:

1. **Artificial Intelligence** — non-negotiable. The primary subject is AI critique methodology.
2. **Machine Learning** — Blog #3 discusses model training, blind spots, and cross-model diversity at a level that warrants this tag. The AI and Machine Learning tags on Medium reach partially different audiences.
3. **Software Development** or **Programming** — the post is about agent pipeline design. This reaches the builder audience the plan explicitly targets.
4. **Productivity** — the self-improvement angle (a human using AI critique to make fewer mistakes) maps to this tag. Retaining from Blog #2.
5. **Investing** or **Personal Finance** — retain one of these. The investing context is specific enough that Personal Finance readers will not feel misled, but drop one of the two to make room for the AI-methodology tags.

Tags to drop: **India** for this post. The methodology content is not India-specific. The India tag may limit discovery to India-focused readers when the AI methodology audience is global. Blog #1 and Blog #2 had strong India-specific content (NSE gap, HDFC Bank example). Blog #3 does not.

Tags to consider adding: **AI Agents** is a Medium tag with growing traffic as of 2025-2026. The post's explicit subject — multi-agent critique pipelines and their limitations — maps directly to this tag. Add it if the publication allows five tags; it should take the Investing or Personal Finance slot.

---

### Q6. CTA / closing — thanks to commenter + invitation to feedback

**The closing structure is correct in shape; the CTA is under-specified.**

Thanking the commenter once, sincerely, at the close is the right call. The plan flags the "self-flagellation" risk explicitly and correctly. One thank-you at the end, not multiple.

The invitation to feedback ("anyone running cross-model pipelines in production — what have you found?") is the right CTA for Medium. It is specific (not "let me know your thoughts"), it targets the builder audience who is most likely to have real data, and it creates a reason for a reader to comment rather than just like. Comments drive Medium's recommendation algorithm more than reads. A specific, answerable question performs better than an open invitation.

The under-specification: the plan does not mention a Follow CTA or a newsletter link. On Medium, the standard structure for series posts is: content CTA (the question) → follow CTA ("if you want to see the experiment when I run it, follow or subscribe") → series link (links to Blogs #1 and #2 at the close, not just inline). The plan only has the content CTA. Adding a two-sentence follow CTA and explicit series links at the close will improve subscriber conversion, which is what Medium's algorithm weights for distributing series posts to existing followers.

---

### Q7. Read-time vs Medium sweet spot

**No issues here. 1500-1800 words = ~7-8 minutes. This is correct.**

Medium's curation team has publicly indicated preference for 5-10 minute reads. The plan's target is well-positioned. No changes recommended on length. If the draft runs long (as methodology posts tend to), cut from §2 (the smaller feedback items) before cutting from §4 (the structural analysis) or §5 (the three fixes). The structural reasoning is why a builder reader clicks; the open-questions inventory is orientation material that can be shorter.

---

### Q8. Series treatment — explicit "Part 3" in title/subtitle, or implicit?

**Stay implicit in the title. Use the subtitle for the series signal, not the title.**

Medium's series feature exists and is underused, as the plan notes. The mechanics: Medium allows authors to add posts to a named series from the post settings. When a post is in a series, Medium displays a "Part N of X" badge and navigation arrows. This is separate from the title.

The recommendation: do not put "Part 3" in the title. Do not put it in the subtitle either. Use Medium's native series feature to handle the "Part 3" signal for returning readers. The title and subtitle should be written as if the post stands alone.

If the author has not used Medium's series feature for Blogs #1 and #2, retroactively adding all three is straightforward — Medium allows adding any post to a series from the post settings after publication. The series feature also gives a small algorithmic boost to "what to read next" recommendations for readers who finish Blog #1 or #2.

For the subtitle specifically: the plan does not draft a subtitle for Blog #3. Medium recommends subtitles under 140 characters. A strong subtitle for this post would be something like: "When all five agents run on the same model, do you actually have five perspectives — or one?" This is standalone-readable, creates tension, and tells a new reader the core question without requiring series context.

---

## §3 — Title Recommendation

**Recommended: Candidate #4 — "The unfixable problem with one model critiquing itself — and what I'm doing about it"**

Reasoning specific to Medium:

1. **Standalone-readable from the first word.** No series signalling in the opening phrase. A reader encountering this post cold in the AI tag or the home feed understands the subject, the problem, and that the post will attempt a resolution.

2. **The word "unfixable" does calibrated work.** It is not clickbait — the post actually argues that the single-model blind-spot problem is unfixable within the same-model constraint, requiring a structural change (cross-model). The adjective is accurate, not inflated. This matters because Medium curators and AI-tag readers are sophisticated enough to punish titles that over-promise.

3. **Em-dash construction is a proven Medium title pattern.** "X — and what I'm doing about it" signals: (a) there is a real problem, (b) the author is not just describing the problem but taking action. This is accountability framing, which is what the plan wants, and it is delivered in the title rather than requiring the reader to reach the lede.

4. **Serves the recommendation engine.** The title contains "model" and "critiquing" which will be picked up by Medium's topic classification for the AI and Machine Learning tags. Candidate #1 ("Two posts in, here's what the comments taught me") contains none of the subject matter keywords.

5. **The plan already describes this as the substance.** Section §3-§4 is the heart of the post — the structural critique and why it lands. The title should name that substance, not the meta-story around it (comments, two posts in, continuation). Candidate #4 does this. Candidate #1 does not.

**If candidate #4 is rejected**: Candidate #3 ("A senior pushed back on my AI agent post. Here's what I think about it.") is the fallback. It is slightly weaker on standalone readability but stronger on human stakes, which Medium's algorithm also rewards via engagement signals.

---

## §4 — Specific Platform Tweaks

The following changes are specific to Medium publication. They do not require structural changes to the plan's content.

**Tweak 1 — Reorder the lede (high impact, low effort)**
Move the core insight — "when all five agents run on the same model, they share the same blind spots" — to sentence 1 or 2. Let the series context follow. The plan's insight is strong enough to be the entry point; it does not need to be earned by reading two sentences of backstory. Target: cold reader should hit the real idea within the first 50 words.

**Tweak 2 — Rename §1 and §2 subheads (low impact, low effort)**
Replace "Where we are in the project arc" with "What this project is about" or "The short version of posts 1 and 2." Replace "The open questions from the first two posts" with "Three things readers pushed back on." These changes keep the content identical while removing the series-dependency signal from the scannability layer.

**Tweak 3 — Add a subtitle to the post (high impact, low effort)**
The plan does not specify a subtitle. Draft: "When all five agents run on the same model, do you actually have five perspectives — or one?" This is 80 characters, standalone-readable, and creates the tension the post resolves. The subtitle appears under the title on Medium's card previews in the home feed — it is often more important than the title for click-through on discovery.

**Tweak 4 — Export Mermaid diagrams as PNG before publishing (critical, one-time effort)**
Confirmed in plan notes, confirming here with priority level CRITICAL. Mermaid code blocks in the Medium editor do not render as diagrams. The flowchart TB experimental design diagram is the post's single most useful visual; if it publishes as a code block, it fails. Use mermaid.live → export PNG → upload to Medium as image. Add a caption: "Three review arms, one human comparing outputs."

**Tweak 5 — Add follow CTA and series links at the close (medium impact, low effort)**
After the commenter thank-you and the open question ("what have you found?"), add two sentences: "If you want to see the experiment when I actually run it — follow me here or subscribe for updates. All three posts in this series are linked below." Then add hyperlinks to Blogs #1 and #2 by title. This increases subscriber conversion and gives the Medium algorithm explicit links to treat these posts as related content.

**Tweak 6 — Use Medium's series feature retroactively (medium impact, one-time effort)**
In post settings for all three posts, add them to a named series (e.g., "Building Nefarious" or "AI for Indian Investing"). Medium will display a "Part N of 3" navigation badge on each post. This handles the series continuity signal for returning readers without putting series language in the title, which is the correct separation of concerns for the platform.

**Tweak 7 — Update the tags to reflect the methodology shift (medium impact, low effort)**
Remove the India tag for this post. Add Artificial Intelligence, Machine Learning, and AI Agents. Retain Productivity. Keep one of Investing / Personal Finance. This better matches the post's actual subject and opens it to a global AI-methodology audience the current tag set would miss.

**Tweak 8 — The §2 open-questions inventory will need placeholder resolution before publication (plan-level note)**
The plan explicitly marks §2 as depending on feedback from Pranav about what readers actually said on Blog #1, and on the content of two referenced tweets. If these remain as placeholders at draft time, §2 will underdeliver on the accountability framing. The section is worth keeping in the plan, but publication should be contingent on having the actual reader questions, not synthetic ones.

---

`✅ Medium-fit review complete. Title pick = Candidate #4 — "The unfixable problem with one model critiquing itself — and what I'm doing about it".`
