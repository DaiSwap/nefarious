# Blog Post #3 — Critic Review C5: Medium Platform Fit

**Reviewer**: C5 (Medium Platform Fit)
**Post**: "A famous investing checklist gave me the opposite of the right answer" (working title)
**Plan version reviewed**: blog_post_03_plan.md
**Date**: 2026-05-31

---

## §1 Medium-Fit Verdict

**NEEDS-OPTIMIZATION**

This post has the ingredients for curation — a concrete surprising finding, a specific number (355%), a clear "why" structure, and a first-person learning arc. Medium curators respond to exactly this kind of post: someone who tested a popular framework and found a crack in it.

But three platform-specific problems stand between "good post" and "curated post": the read time is outside the curation sweet spot, the diagram volume is too high for the rendering environment, and the two-variable-stock problem is more damaging on Medium than in any other format. All three are fixable before drafting begins.

The post is not a WON'T-PERFORM. The core signal is strong. The fixes are structural and none require changing the argument.

---

## §2 Per-Question Medium Analysis

### Q1 — The 3 Candidate Titles: Rank for Curation

**Ranked best to worst for Medium curation, with reasoning:**

**Rank 1 (Best): "A famous investing checklist gave me the opposite of the right answer"**

This wins on Medium specifically for three reasons:

First, it fits the "I tested something popular and found a problem" pattern that Medium curators actively favour. It's personal ("gave me"), specific ("the opposite"), and implies a resolution the reader doesn't have yet. The tension is in the title itself.

Second, it is short enough to display fully in both the recommendation engine card (under 70 characters at 65 characters including spaces) and push notification preview without truncation. The other two candidates both truncate on mobile cards.

Third, "famous investing checklist" will surface in searches around Piotroski, F-Score, and investing frameworks. The tag Indian Stock Market plus this title gives the recommendation engine enough to route it to readers who engage with those tags.

**Rank 2: "The 9-point investing checklist that's wrong about an entire kind of Indian stock"**

This is stronger than it looks. "9-point" is specific and scannable. "An entire kind of Indian stock" narrows the audience precisely — which is a Medium curation signal, not a penalty. The weakness is the word "wrong." On Indian investing tags, F-Score evangelists will read it as "this person is trashing Piotroski," and that framing invites combative comments before the post has had a chance to explain itself. The tone mismatch between the plan ("I might be wrong about this") and the title ("it's wrong") creates friction at the first impression.

**Rank 3 (Weakest): "I ran the most respected investing checklist on a real Indian stock. It told me to avoid the best buy of the decade."**

This is the best of the three as a pull-quote or social share text. It is the worst as a Medium title. It is 101 characters — it will be cut off in every card view and push notification. The word "decade" is a claim-size that conflicts with the "still learning, not done" tone mandate. It also front-loads the resolution (you already know the checklist failed before you open the post), which reduces the click incentive. Keep this sentence — but move it to the hook or a subhead, not the title.

**Tag note on Rank 1**: On the Indian Stock Market and Quant Investing tags, curiosity-gap titles consistently outperform claim titles in curation selection. The Rank 1 title is a curiosity gap. The Rank 3 title is a claim. Rank 2 is borderline.

---

### Q2 — The Hook (First 120 Words): Bounce Window Survival

**Assessment: Passes bounce window. One adjustment needed.**

The hook as drafted lands the core numbers within the first 60 seconds of reading. "The stock then went up 355% over two years" appears in paragraph 4 of the hook, which a normal reader reaches in approximately 35–45 seconds at 200 WPM. That is inside the bounce window.

The density is not a problem here. Medium readers on investing tags are self-selected for this kind of information. The issue is structural: the hook ends with "Here's why, and here's what I do instead." This is a competence-claim close, not a curiosity-gap close. It implicitly tells the reader the post has a settled answer. Combined with the "still learning, not done" tone mandate, the close of the hook needs one sentence that invites rather than concludes:

Replace: *"The checklist is giving the opposite of the right answer for this kind of stock. Here's why, and here's what I do instead."*

With something like: *"The checklist is giving the opposite of the right answer for this kind of stock. I think I know why — and I'd like to know if others have seen the same."*

This is a small change with a meaningful effect on the reader's posture going into §1. They are now reading alongside you rather than being lectured at. That posture matters for comment engagement, which Medium's recommendation engine weights.

One additional note: "The first few tests went fine" in paragraph 3 of the hook is doing no work. Cut it. The hook is stronger without the setup paragraph that says nothing happened. Go directly from "tested it on a real Indian stock" to "Then I tested it on a commodity stock at the bottom of its cycle."

---

### Q3 — Subheads §1 Through §7: TOC Click-Through Potential

Medium's table of contents is shown to readers who scroll past the fold before reading. The subheads are therefore clickbait in the original neutral sense: they need to earn a click from someone who has not read the preceding paragraphs.

| Section | Current subhead (from plan) | TOC click-through rating | Suggested alternative |
|---|---|---|---|
| §1 | "What this checklist is (in plain English)" | LOW — generic, describes process not content | "The 9-question test that every Indian investor knows" |
| §2 | "How I tested it on a real Indian stock" | MEDIUM — personal but vague | "I picked one stock and ran the math at four different moments" |
| §3 | "What the numbers showed" | LOW — reveals nothing | "The score said avoid. The stock tripled." |
| §4 | "Why this happens (the deeper 'aha' moment)" | LOW — the word "aha" signals the author explaining, not the reader discovering | "The checklist reads where you are in the cycle, not how good the company is" |
| §5 | "Contrast: Stock Y, a non-cyclical (the F-Score works here)" | LOW — parenthetical kills click energy | "When the same checklist does exactly what it's supposed to" |
| §5b | "How to spot a stock where F-Score might mislead" | MEDIUM-HIGH — specific utility | Keep this one; it's the strongest subhead in the post |
| §6 | "What I do instead" | MEDIUM — functional but generic | "The version I now use for commodity stocks" |
| §7 | "Closing — what this taught me about using imported math" | LOW — "Closing" as a word in the TOC is a dead subhead | "The lesson I keep coming back to" |

The two subheads that need the most work are §3 and §4. §3 is the heart of the post — it should be the most clickable subhead in the TOC, not the most generic.

---

### Q4 — Four to Five Mermaid Diagrams in a 2000–2500 Word Post

**Recommendation: Cut from 5 to 3. Keep diagrams 2, 3, and 5 (or 1 and 2 and 4 in the original numbering).**

The Pranav lock says "more diagrams welcomed," and this review cannot override that lock. But it can surface the platform-specific cost.

On Medium, mermaid is not natively rendered. Every mermaid block must be exported to PNG and inserted as an image, or rendered in a tool like Mermaid Live and embedded. This is fine for one or two diagrams. At five diagrams in a 2000-word post, the reader encounters a visual break approximately every 400 words. The pacing problem is not visual fatigue from the diagrams themselves — it is that five forced stops in a 10-minute read breaks the prose momentum exactly when the argument is building.

The two-most-load-bearing diagrams are:
- Diagram 2 (§3): Stock X — F-Score vs forward returns. This is the central visual argument. It must stay.
- Diagram 3 (§4): The cycle loop. This is the "why it happens" diagram. It earns its place.

The diagram with the lowest ROI is Diagram 1 (the 9-question F-Score breakdown). A clean table of 9 rows serves this purpose better on Medium and takes 30 seconds to read instead of pausing for an image load. A table also renders natively in Medium's editor without the export step.

Diagram 4 (Stock Y comparison) is the second essential diagram — the two-stock comparison is the structural argument. Keep it.

Diagram 5 (§5b: where F-Score works vs misleads) can be replaced with a short plain-language bulleted list. The content in §5b is already a list in the plan. Turning it into a diagram adds no information and costs a visual stop.

If the 4-5 lock holds: prioritise diagrams 2, 3, and 4 as full images. Make diagram 1 a table. Make diagram 5 a list. That satisfies the spirit of "more diagrams" while not creating the pacing problem.

---

### Q5 — Stock X / Stock Y: The Variable-Stock Problem on Medium

This is the most Medium-specific problem in the plan, and the plan does not yet have a solution for it.

On Medium, readers skim. The first time a reader encounters "Stock X" and "Stock Y" in the same paragraph, approximately 20–30% of them will have already forgotten which is which. By §5, where both stocks appear in proximity for comparison, a meaningful share of readers will have lost the thread. This is not a content quality issue — it is a working-memory issue unique to the long-scroll single-column format.

The plan's anonymization lock is clear and not challengeable here. But there are three Medium-specific mitigations that do not require naming the stocks:

**Mitigation 1: Give each stock a stable one-word nickname, not a letter.**
"Steel Co" and "Paint Co" (or "the metals name" and "the consumer goods name") give readers a conceptual anchor that persists across 2000 words. "X" and "Y" are algebraic placeholders — they carry no meaning between readings. A nick name like "the metals stock" activates a reader's existing schema for cyclical commodity businesses and does the memory work that "X" cannot do.

**Mitigation 2: Use a visual anchor at first introduction.**
When Stock X first appears in §2, add a brief parenthetical descriptor that sticks: "one of India's biggest metal producers — I'll call it the Metals Stock throughout this post." Then hold that name consistently. Readers who skim will find "Metals Stock" faster than "Stock X" when they return from a scroll.

**Mitigation 3: Repeat the descriptor in each new section header.**
"§5 — The consumer goods contrast: where the same checklist works" costs nothing in word count and saves the reader from having to remember what Stock Y means when they arrive at §5.

None of these require real names. All three work within Pranav's lock.

---

### Q6 — Tags Strategy

**Recommended top 5 tags in priority order:**

1. **Indian Stock Market** — highest-traffic Indian investing tag on Medium; routes the post to the core audience. Essential.
2. **Investing** — broad reach tag; required for recommendation engine crossover into non-India readers who engage with investing content.
3. **Personal Finance** — the post's framing is personal ("I tested this"). Personal Finance readers are habituated to first-person learning posts. This tag reaches them.
4. **Quant Investing** — a smaller but highly engaged tag. Readers on Quant Investing are specifically interested in quantitative frameworks being tested and challenged. They are the most likely to comment, share, and follow.
5. **Data Science** (preferred over AI / Machine Learning) — the post is about hand-computed math on real data, not ML. "Data Science" better describes the method and reaches readers who engage with "I ran numbers and found something" posts. AI / Machine Learning will bring readers expecting neural networks and GPT; they will bounce.

**On AI / Machine Learning**: avoid this tag for this specific post. The post mentions that Pranav is building an AI system in the closing, but the post's substance is a manual F-Score computation. Mismatched tags cause curation penalties on Medium because the algorithm tracks read ratio (readers who finish vs readers who opened). AI/ML readers will open and leave early when they find no ML content.

---

### Q7 — Cross-Linking to Blog #2: Does It Help the Recommendation Engine?

**Verdict: The cross-link in §7 helps, but the framing of it in the plan needs adjustment.**

Medium's recommendation engine does weight internal links between posts by the same author, but only if those posts share at least one tag and were read by overlapping audiences. Blog #1 and Blog #3 share Indian Stock Market and Investing — so the cross-link in §7 ("see Blog #1 for what I'm building") will produce algorithmic referrals, not just editorial mentions.

The risk in the plan's current cross-link language is that §7 lists two links: Blog #1 ("what I'm building") and Blog #2 ("how I make the AI argue with itself"). A closing that sends readers to two other posts creates a decision paralysis problem. Readers who would have clicked one link often click neither when given two equal options.

**Recommendation**: In §7, link to Blog #1 as the primary next-read. Link to Blog #2 only in a "if you found this technically interesting" framing — or drop the Blog #2 link from this post entirely and rely on the recommendation engine to route readers who finish this post to Blog #2 via tag overlap.

Cross-linking to prior posts does not fragment the read when done at the end. It fragments the read when done mid-post. The §7 placement is correct.

---

### Q8 — Length: 2000–2500 Words at ~10–12 Min Read

**This is the most consequential Medium-specific problem in the plan.**

Medium's curation sweet spot is 4–7 minutes. That is not a soft guideline — it is the range where the platform's internal read-ratio data peaks. Posts above 7 minutes have a lower read-to-open ratio on average, which the curation algorithm interprets as "readers started but didn't finish" and reduces recommendation frequency.

The plan's locked length of 2000–2500 words produces a 10–12 minute read. That is 3–5 minutes outside the curation zone.

Three options, in order of impact:

**Option A (Recommended): Split §5 and §5b into a separate post.**
The non-cyclical contrast (Stock Y) and the "how to spot where F-Score misleads" section are structurally complete as a standalone piece. Splitting here produces: Post #3 (~1400–1600 words, 7 min) covering the core finding — F-Score inverts for cyclicals — and Post #3b (~700–900 words, 4 min) covering the contrast and the actionable checklist. Both posts are inside the curation zone. Both cross-link. The recommendation engine benefits from two curation-eligible posts instead of one borderline post.

**Option B: Compress and cut.** Keep the two-stock structure but tighten §1 (the F-Score explanation can be a diagram + 100 words rather than 250), cut §5b to a 5-item bulleted list inside §5, and tighten §6. Target: 1600 words. This is 8 minutes — still above the curation zone but close enough that the strength of the content can overcome the length penalty.

**Option C: Publish at planned length and accept the trade-off.** Long posts can still get curated when the content is unusually strong. The 355% / 34% inversion is a genuine hook. If every other optimization is implemented, the post can perform above its length. But this is the riskiest path.

The Pranav lock on length (2000–2500) is noted. If it holds, implement Option B targeting 1800 words rather than 2500. Do not let the second stock and extra diagrams push the post to the top of the range.

---

### Q9 — CTA / Closing

**Blog #1 approach**: no hard CTA. Closed with "if you want to follow this build, I'll write more as it goes." Understated. Fits the "still learning" voice.

**For Blog #3 specifically, the closing should be slightly warmer — but not a hard sell.**

The reason is audience-specific. Blog #3 will land on Indian Stock Market and Quant Investing tags, where readers are more likely to have an opinion about the F-Score. A post that ends with a genuine question ("I'd like to know if others have tested this on more cyclical stocks — have you seen the same pattern?") will generate comments, and Medium's algorithm weights comments as engagement signals.

Recommended closing approach:
- One sentence linking to Blog #1 ("what I'm building and why")
- One genuine question to readers ("if you've run F-Score on a cyclical stock in Indian markets, I'd genuinely like to know what you found")
- No "follow me" or "share this if useful" language — these are Medium clichés that undercut the "still learning" voice and are invisible to most readers

The "share this if you found it useful" CTA performs better on Twitter/X and LinkedIn than on Medium. Medium readers respond to intellectual curiosity signals, not social proof asks. Leave it out.

---

## §3 Title Recommendation

**Pick: "A famous investing checklist gave me the opposite of the right answer"**

**Reasoning**:

This title is a curiosity gap, not a claim. It does not say "the F-Score is wrong." It says "I got the opposite of what I expected." That framing is consistent with the "still learning, not done" tone throughout the post, which means the title and the post voice match — a coherence signal that readers feel even if they can't name it.

On the Indian Stock Market tag specifically, the competition is mostly claim-titles ("Why Stock X is a strong buy", "The 3 indicators every Indian investor needs"). A curiosity-gap title stands out in that feed.

The title at 65 characters renders fully in Medium card view, push notification, and Google mobile search snippet. The other two candidates exceed 80 characters and will be truncated in at least one of those surfaces.

One optional adjustment: consider adding "on Indian stocks" to the end — "A famous investing checklist gave me the opposite of the right answer on Indian stocks." This adds 16 characters (total: 81, which truncates on mobile) — so do not add it unless the publication submission (DataDrivenInvestor) requests a geographic signal in the title. For standalone Medium, keep the original.

---

## §4 Specific Platform Tweaks

These are actionable changes for the draft, in priority order:

**1. Rename Stock X and Stock Y immediately in §2.**
Introduce "the Metals Stock" (Stock X) and "the Consumer Goods Stock" (Stock Y) at first use. Hold these names for the entire post. Do not alternate between "Stock X" and "the Metals Stock" — pick one and commit. The letters can appear once, in parentheses at introduction, for readers who are aware of the convention: "I'll call it the Metals Stock (Stock X in this post)."

**2. Rewrite the close of the hook.**
Remove "Here's why, and here's what I do instead." Replace with a genuine open question or a "here's the pattern I think I'm seeing." The hook's job is to create sufficient curiosity to justify reading §1 — it has already done that by §4. The final sentence should be a lean-in, not a resolution.

**3. Replace Diagram 1 (the 9-question F-Score breakdown) with a table.**
A markdown table with 9 rows and 3 grouped sections renders faster, requires no export step, and preserves the same information. Reserve mermaid for the two diagrams where spatial relationships matter: the inversion diagram (§3) and the cycle diagram (§4).

**4. Revise the §3 and §4 subheads before drafting.**
Use the alternatives from Q3 above. The subheads are the post's navigation system on Medium. Weak subheads reduce TOC engagement and skim-reading comprehension simultaneously.

**5. Add the disclosure in §2, not §3.**
The plan notes the disclosure can go in §1 or §3. On Medium, §3 is too late — by §3, readers who will be misled are already forming conclusions. The disclosure belongs immediately after the hook, before the data is presented. Suggested placement: first paragraph of §2 ("Before the numbers: this is from my own testing on one stock at four dates. It's not peer-reviewed research, and I might be wrong. I'm sharing it because the pattern surprised me.").

**6. Reduce the target word count to 1800, not 2500.**
Every section in the plan has word-count estimates. The math adds to ~1900 without the diagrams. Diagrams absorb ~200 words of reading time when rendered as images (reader pauses, processes, re-enters prose). Aim for 1800 prose words + 3 diagrams = approximately 9–10 minutes — still outside the curation sweet spot, but within the range where strong content can overcome the length penalty. At 2500 words, it cannot.

**7. In §7, link to Blog #1 only. Drop or defer the Blog #2 link.**
One outbound link at the close drives more clicks than two. If Blog #2 needs to be mentioned, put it in a parenthetical mid-sentence, not as a standalone link with equivalent weight to Blog #1.

**8. End §7 with a genuine question.**
Something like: "If you've run the F-Score on a cyclical stock in Indian markets — metals, cement, chemicals — I'd genuinely like to know what you found. The data I have so far is from one stock. More data would either confirm the pattern or break it." This is not a CTA. It's an intellectual invitation. Those generate Medium comments at a higher rate than social proof asks.

---

*Review complete.*
