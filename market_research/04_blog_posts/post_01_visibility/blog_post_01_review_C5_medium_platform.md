# 15c5 — Blog Draft Review: Medium Platform / Discovery

**Status**: ✅ Medium platform review complete.
**Date**: 2026-05-31
**Lens**: Medium Platform / Discovery
**Last updated**: 2026-05-31T00:05

## 1. Verdict (top-line)

NEEDS-MINOR-EDITS. The post is substantively strong and the right length for Medium's recommendation engine, but the title undersells itself in a crowded feed, the opening section buries the sharpest hook, and the CTA asks a question better suited to a community forum than a Medium comment section.

## 2. Title evaluation

- Current title: "I'm building an AI to argue with me about my own stock portfolio. Here's why."
- Would you click it in a feed? MAYBE — "argue with me" is the best phrase in the title and does real work; "Here's why" is a reflex ending that Medium readers have been trained to ignore. The title is conversational but loses urgency in a feed where 15 other posts are shouting adjacent things. The Indian-market specificity is missing entirely, which hurts distribution to the most relevant niche (Indian retail investors on Medium) while also failing to signal anything distinctive to a global reader.
- 2–3 alternative titles to A/B against:
  1. "I built an AI that argues back when I'm about to make a bad stock decision" — leads with the behaviour (arguing back), which is the emotional hook; implies a live outcome rather than a plan
  2. "My investing brain lies to me. So I built a bot to call it out." — shorter, punchy, self-deprecating in a way Medium audiences respond to; hints at behavioural angle immediately
  3. "Why I stopped trusting myself with my own portfolio — and built an AI instead" — classic Medium confessional structure; "stopped trusting myself" is a strong emotional entry point

## 3. Opening 100 words evaluation

- Does it hook? PARTIAL
- The section header "The dance every retail investor knows" is strong framing — but the first sentence ("If you hold Indian stocks, you've probably done this dance.") addresses only Indian readers and may cause 70%+ of a global Medium feed audience to self-select out in the first two seconds. Medium's recommendation engine serves this post to investors broadly; the lede should land before it narrows.
- The best line in the opening is buried at line 13: "The gap between what AI is genuinely good at today, and what a retail investor actually needs *in the moment of deciding*." That sentence is the thesis and it should be sentence one or two — not the payoff of a four-paragraph setup.
- The opening 100 words describe a familiar pain (selling too early, holding too long) that every investing post describes. The differentiating idea — that AI still fails at *personalized, rules-based pushback* — doesn't arrive until paragraph 3. On Medium, that's already past the bounce point.

## 4. Subheads evaluation

**"The dance every retail investor knows"**
Verdict: Pulls weakly. "Dance" is evocative but not specific enough to be a standalone read in a table-of-contents skim. Someone skimming subheads won't know if this is about volatility, trading habits, or market timing.
Suggested rewrite: "The part every investing app ignores" or "The moment AI stops being useful"

**"What today's AI is good at — and what it isn't"**
Verdict: Pulls well. Clear contrast structure, sets up expectation of a reveal. Reads cleanly as a standalone. Keep.

**"What I'm actually trying to solve"**
Verdict: Weak. The word "actually" signals authenticity but doesn't create curiosity or forward motion. A Medium reader skimming subheads needs a reason to enter the section — "actually" is a hedge, not a hook.
Suggested rewrite: "The six mistakes I keep making that no app catches" (mirrors the six bullet points in the section)

**"What I'm building, in plain English"**
Verdict: Functional but flat. This subhead is where the product reveal lives — the most important section for Medium's "Member Story" surface — and "in plain English" slightly undersells it.
Suggested rewrite: "Meet Nefarious: what it does, what it refuses to do" — uses the product name (which is distinctive and memorable) and the refusal framing which is one of the post's most original moves.

**"Why this problem statement actually makes sense"**
Verdict: Weak. Two hedging words in five words ("actually makes sense") — the subhead is apologising before the reader arrives. On Medium, subheads that defend themselves lose readers; subheads that intrigue them win.
Suggested rewrite: "Four things the fintech industry won't build — and why"

**"Where I am right now, honestly"**
Verdict: Works well for Medium's confessional register. "Honestly" is a trust signal. The vulnerability framing is effective here and appropriate for Medium's audience expectations around founder/builder narratives. Keep.

**"What's next"**
Verdict: Weakest subhead in the post — pure utility, zero pull. Every newsletter and blog post ends with "What's next." On Medium this is where readers decide whether to follow.
Suggested rewrite: "What I still don't know — and what I'm building toward"

## 5. Specific recommendations for Medium (8–12 rows)

| Element | Current | Suggested | Why for Medium |
|---|---|---|---|
| Title tail | "Here's why." | Remove or replace with a specific tension: "...even though it keeps telling me I'm wrong." | "Here's why" is a cliché finisher Medium readers have been trained to scroll past; a specific, surprising continuation holds the eye longer in a feed |
| Opening sentence | "If you hold Indian stocks, you've probably done this dance." | Lead with the universal problem before the geographic narrowing: "Every investor has a version of this." Then introduce Indian context in sentence two. | Medium's distribution algorithm serves the post to a global investing audience first; a geographic qualifier in sentence one signals "not for you" to ~80% of feed impressions |
| Lede payoff line | Appears at line 13: "The gap between what AI is genuinely good at today, and what a retail investor actually needs in the moment of deciding." | Move this to sentence two or three of the post. | This is the thesis — it's the single best hook in the post and it arrives too late to prevent bounce |
| ASCII diagram | Code block, lines 64–77 | Add a caption below: "This is the whole loop. No trading. No predictions. Just a weekly report." | Medium de-prioritises posts without inline images in Member Story recommendations; a captioned diagram is not a substitute for an image but adds scannability that the algorithm rewards |
| Inline image | None | Add one image: a mock screenshot of a Nefarious weekly report output, even a rough one. | Medium's recommendation engine rewards posts with at least one inline image; posts with zero images underperform in the "Stories for you" surface vs comparable posts with one image |
| "Here's why" CTA / post ending | "follow along" (line 127) | Replace with: "Follow this publication [or profile] to get the next post the day it drops — the next one is about what five years of Indian company data broke in my assumptions." | "Follow along" is the weakest possible CTA on Medium. Specific follow prompts with a preview of the next post convert 2–4x better for series retention. |
| Series framing | Not established | Add a series header at the top: e.g., "Building Nefarious — Post 1 of ?" | Medium readers who see a numbered series are significantly more likely to follow for future posts; sets expectation that this is a journey, not a one-off |
| Subtitle (sub-headline) | None present in draft | See §6 | Subtitle is surfaced in Medium feeds alongside the title — it's a second headline and most writers waste it |
| Word "Nefarious" introduction | Bold, line 53: "I'm calling it Nefarious." | Keep the bold; consider adding a one-line parenthetical: "*(the name felt right — this thing is supposed to be adversarial)*" | Medium readers engage with personality signals; the name is memorable and unusual; a one-line acknowledgement of the name choice makes it stick |
| Tags | Not set in draft | See §6 | Tags are the primary distribution mechanism on Medium; wrong tags = wrong audience |
| Post length | ~1,800 words | Keep — this is the optimal 7-minute read range for Medium's recommendation algorithm | Medium data consistently shows 5–9 min reads outperform both shorter and longer posts for distribution; do not cut material to hit a lower word count |

## 6. Tags / topics

- Recommended tags (Medium allows up to 5, in priority order):
  1. **Investing** — broadest distribution surface; highest-traffic investing tag on Medium
  2. **Artificial Intelligence** — captures the AI-curious reader who is not primarily an investor; cross-audience discovery
  3. **Personal Finance** — captures retail investor audience; strong Medium publication overlap
  4. **Behavioral Finance** — niche but well-engaged; the post's strongest differentiator lives here
  5. **India** — narrows to the most directly relevant geographic audience; surfaces in Indian Medium reader feeds

- Recommended publication submissions:
  - **DataDrivenInvestor** — best fit; specifically covers AI + investing + retail finance; active editor team; accepts builder narratives
  - **The Startup** — second choice; broad tech/founder audience; less investing-specific but high distribution
  - **Towards Data Science** — viable if the next post (with actual data/test results) comes out quickly and cross-links; this post is slightly light on data for TDS standards

- Recommended subtitle (sub-headline below title):
  "The AI tools that exist are great at conversation. They're useless at knowing *your* rules and holding you to them. So I built one that does."
  — This subtitle does the work the title can't: it names the specific problem (your rules, not generic advice), signals the solution, and creates a curiosity gap. At ~30 words it fits Medium's subtitle length range.

## 7. CTA evaluation

- Current CTA: "what's the one decision you keep making that you wish a tool would help you stop making?"
- Does it work? PARTIALLY. The question is genuinely good — specific, self-reflective, directly relevant to the post's argument. It would work well on Twitter/X, in a newsletter, or at the end of a Substack post where the audience has already opted in. On Medium, it has two platform-specific problems:
  1. Medium comment engagement on new posts is low unless the post goes viral or the writer has an existing following. Asking a thoughtful research question of a first-time audience sets up a high-effort interaction that most readers won't make.
  2. It doesn't ask readers to do the one thing that compounds on Medium: follow. You get one shot at converting a first-time reader into a follower; the current CTA uses that shot on a comment prompt.
- Suggested alternative: Split the CTA into two parts.
  - Part 1 (comment): Keep the question — "If you invest in Indian markets: what's the one decision you keep making that you wish something would make harder to execute?" — but frame it as optional: "If that question resonates, drop it in the comments — it's going directly into what gets built next."
  - Part 2 (follow): "I'm writing this series as it happens, mistakes and all. Follow to get the next post — on what five years of Indian company data broke in my assumptions — the day it goes up."
  - Ordering matters: put the follow ask before the comment ask on Medium.

## 8. One sentence to Pranav

"If you change ONE thing about this post for Medium specifically, change the opening: move the line 'The gap between what AI is genuinely good at today, and what a retail investor actually needs in the moment of deciding' to sentence two, and make sentence one universal before it's Indian — because everything else in this post is strong, but Medium gives you five seconds and you're currently spending them on setup."
