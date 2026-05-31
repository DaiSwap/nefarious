# 15c3 — Blog Draft Review: Skeptical Reader

**Status**: ✅ Skeptic review complete.
**Date**: 2026-05-31
**Lens**: Skeptical Reader
**Last updated**: 2026-05-31T00:18

---

## 1. Verdict (top-line)

NEEDS-MINOR-EDITS — the bones are honest and the framing is better than 90% of "I built an AI" posts, but three specific claims don't survive a hard stare: the "nobody is building this," the "60 percent" pull-quote, and the AI-as-challenger section tip into either unsupported assertion or quiet humble-brag. Fix those three and the post earns its confidence.

---

## 2. Strengths (3–4 specific bullets — what survives skepticism)

- **The problem list in "What I'm actually trying to solve" is the best paragraph in the post.** Six concrete, embarrassing, personal admissions (selling winners, holding losers, forgetting own thesis). A skeptic cannot call that manufactured — it reads like a real investor's notebook. This is the post's anchor.

- **The explicit "does not trade, does not predict" constraints box is credible.** Most "AI investing" posts never say what the thing won't do. The ❌/✅ table near the end is one of the few places where under-promising is the honest move, and it lands.

- **The admission that standard formulas failed on Indian data survives scrutiny — if framed correctly.** A one-month builder discovering that Piotroski/Beneish have NSE-specific failure modes is a real finding. The post doesn't over-claim what the finding means. That restraint is earned.

- **"I'm trying to stop being my own worst enemy" closes the problem section cleanly.** It's a one-line thesis that a skeptic can't puncture — it's a personal goal, not a market prediction.

---

## 3. Weaknesses (specific claims that fail hard scrutiny)

**W1. "Nobody is building this" — §2, final paragraph.**
The post names ChatGPT, Claude, Gemini and dismisses them as general-purpose. Fine. But it completely ignores the Indian fintech ecosystem. INDmoney does portfolio aggregation with AI-generated plain-English explanations. Smallcase wraps thematic rules around holdings with curator logic. Streak.tech and Sensibull do rule-based strategy building. Capitalmind Premium publishes explicit sell rules and behavior-focused commentary for retail investors. The claim "nobody is building it" is at best "nobody has shipped a finished version of the full stack I want," which is a very different sentence. As written, it will be the first thing a skeptical Indian fintech reader uses to dismiss the whole post.

**W2. "Even if it's only right 60 percent of the time" — §4, reason Two.**
This number arrives from nowhere. There's no footnote, no stated methodology, no "I'm guessing" qualifier. In a post that correctly emphasizes verifiability ("any number the bot uses must be one I can verify"), the author slides in an unverified percentage as rhetorical scaffolding. A skeptic immediately asks: right 60 percent compared to what baseline? A coin flip is 50%. If "right" means "the behavioral flag it raised was a flag you'd have agreed with in hindsight," that's a different claim than "60% of the time acting on it improved returns." The number does the author's intended work — sounds humble and specific — but it's doing that work without evidence, which is exactly what the post positions itself as being against.

**W3. "I tested those formulas on real Indian companies, going back five years, by hand" — §4, reason Three.**
"By hand" signals rigor. But testing two companies (the underlying project files confirm it was Asian Paints and Tata Steel) over five years on a handful of ratios is illustration, not validation. "Going back five years, by hand" implies something closer to systematic backtesting than it delivers. A quant-leaning reader will immediately ask: how many companies? Which years? What selection methodology? Were those two companies chosen to surface failure modes, or were they representative? The sentence claims more credibility than the underlying work can bear at this stage.

**W4. "AI doesn't know more than I do about what I want to build" — §5, second-to-last paragraph.**
This is a humble-brag wearing a disclaimer. It's unfalsifiable — it can't be tested, and it preemptively deflects the "did the AI just do this for you?" challenge without engaging it honestly. A skeptic reads it as brand protection. The more credible version would describe one specific moment where the author overrode an AI suggestion and why. Without that, the claim is asserted, not demonstrated.

**W5. The closing CTA — §6.**
The ask is framed as genuine user research, but "I'd genuinely like to hear" is the tell — "genuinely" is the word you add when you suspect the reader doesn't believe you. The rest of the post is usefully unpolished. This line is the most optimized sentence in the piece, and it reads that way. The mismatch undercuts the candor that earned the reader's trust up to that point.

---

## 4. Specific line edits (5–10 rows)

| Section | Original (the claim) | Problem | Suggested fix |
|---|---|---|---|
| §2, final line | "Nobody is building it. So I am." | Ignores INDmoney, Smallcase, Capitalmind, Streak — a well-read Indian fintech reader will reject the whole post on this line alone. | Narrow the claim: "Nobody is building *this exact combination* — rules-you-set + behavioral pattern detection + your-own-investment-thesis memory — for Indian retail. So I am." |
| §4, reason Two | "even if it's only right 60 percent of the time" | Fabricated precision — no source, no methodology, and the post otherwise demands verifiable numbers. | Remove the percentage entirely, or replace with: "even if it catches only some of the worst behavioral mistakes in time." |
| §4, reason Three | "I tested those formulas on real Indian companies, going back five years, by hand." | "Companies" (plural) and "by hand" over-claim the scope. It was two companies and a handful of years of ratios. | "I tested those formulas on two real Indian companies — Asian Paints and Tata Steel — year by year, by hand." The specificity actually strengthens credibility rather than weakening it. |
| §5, AI section | "The AI doesn't know more than I do about what I want to build." | Unfalsifiable claim that reads as defensive brand-management. | Cut it, or replace with a single concrete example: "When I tried to shortcut the Piotroski scoring, Claude pushed back with three counterexamples. I kept the scoring. That's the dynamic." |
| §2, para 3 | "That gap is enormous, and almost nobody is building for it." | Same problem as "nobody is building it" two paragraphs later — redundant, and doubly vulnerable. | Cut one of the two instances. Keep the more specific version. |
| §4, reason Three | "None of that was learnable by reading about it. The only way to find it was to actually do the work" | Slightly grandiose — implies the author discovered something no textbook mentions, when the finding is actually "US-derived formulas have NSE-specific failure modes" which IS documented (Piotroski applicability papers on BSE/NSE exist). | Soften to: "None of that was apparent until I computed the numbers on actual Indian data." |
| §6, CTA | "I'd genuinely like to hear..." | "Genuinely" performs sincerity instead of expressing it. | Drop "genuinely." "I'd like to hear: what's the one decision you keep making that you wish a tool would help you stop?" |

---

## 5. Big-picture skepticism concerns (max 4)

**1. The post is one step ahead of the project.**
The project is at "v0.1 math is broken in 6 identifiable ways." The post describes a tool that "reasons about your behavioural patterns," "flags when you're drifting," and "pushes back when you're about to break your own rules." Those capabilities don't exist yet in the described form — the author is writing about a destination, not a current artifact. A skeptic reading carefully will notice this. The post is not dishonest, but it describes the intended tool and the current stage in the same tonal register, which obscures the gap.

**2. The personal-disclosure framing is real but partial.**
The opening anecdotes (selling early, holding too long, WhatsApp tips) feel earned and specific. But the author never discloses anything that's genuinely uncomfortable — no "I lost X lakh on Y because of Z mistake." The framing implies rawness without delivering it. That's a mild version of performed vulnerability. For the skeptic, it signals "this person has thought about how to come across, not just what to say."

**3. The project name "Nefarious" does no work for the post's thesis.**
A skeptical reader notices the name exactly once ("I'm calling it Nefarious") and then moves on confused. Is it ironic? Self-deprecating? A reference to "the enemy within"? The post never connects the name to any theme. This is a minor craft concern — but a skeptic filing away "is this for real?" signals will count it.

**4. No evidence the behavioral-pattern detection actually works yet.**
The most interesting capability the post describes — "it tells me when I'm anchoring on my entry price" or "flags that I'm about to sell a winner because I'm anxious" — is also the capability furthest from being real. The project is at Cycle A (fundamental analysis math), and even that math is described as broken. The behavioral layer is Cycles D–F in the roadmap. A skeptic who asks "has this ever actually caught a real behavioral mistake in real time?" gets no answer from this post.

---

## 6. One sentence to Pranav

"If you change ONE thing about this post, change the 'nobody is building this' claim — a single Indian fintech reader who knows INDmoney or Capitalmind will use it to dismiss everything else, and you've given them the ammunition yourself."
