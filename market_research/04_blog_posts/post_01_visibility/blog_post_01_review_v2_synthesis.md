# Blog Draft v0.2 — Cross-critic synthesis

**Status**: ✅ All 5 v0.2 reviews complete. This consolidates them into a revision plan for v0.3.
**Date**: 2026-05-31
**Inputs**: 5 critic outputs reviewing v0.2 against their own v0.1 priorities
**Output target**: An integrated edit plan → drives `blog_post_01_draft_v0.3.md`

---

## 1. Cross-critic v0.2 verdicts

| Critic | v0.1 verdict | v0.2 verdict | Direction |
|---|---|---|---|
| C1 — Retail reader | NEEDS-MINOR-EDITS | NEEDS-MINOR-EDITS | Improved |
| C2 — Editorial | NEEDS-MINOR-EDITS | NEEDS-MINOR-EDITS | Improved |
| C3 — Skeptic | NEEDS-MINOR-EDITS | NEEDS-MINOR-EDITS | Net improvement, but new overclaims introduced |
| C4 — Voice authenticity | PART-HUMAN-PART-AI | **PART-HUMAN-PART-AI** | Improved, but ~40% of AI scaffolding remains |
| C5 — Medium platform | NEEDS-MINOR-EDITS | NEEDS-MINOR-EDITS | "Biggest single improvement" was the universal opener |

**Net read**: v0.2 is materially stronger than v0.1 on every dimension, but **3 critics flag the same 2–3 unresolved issues** that prevent SHIP-AS-IS.

---

## 2. Big wins from v0.1 → v0.2

| Win | Critic(s) |
|---|---|
| Tata Steel + Asian Paints anchor for "textbook math failed" claim | C1 (best section), C3 (honest fix) |
| 10-bullet wall in §What I'm trying to solve broken into prose | C2 (biggest win) |
| Numbered bold structure in §Why dropped → reads as argument | C2, C4 |
| Em-dash count: 21 → 2 | C4 |
| Title fix (dropped "Here's why.") + universal opener + subtitle added | C5 (biggest single improvement) |
| "60 percent right" cleanly removed | C3 (best fix in the draft) |
| "Genuinely" removed from CTA | C3, C4 |

---

## 3. Issues that survived v0.2 → must fix in v0.3

### Multi-critic flags (priority P0)

| # | Issue | Critics | Recommended v0.3 fix |
|---|---|---|---|
| **P0.1** | **"the moment of deciding"** appears verbatim in subtitle AND §0 ¶1 (also in §1 once) — 4 total uses in the first half of the post | C2, C5 (independent catches); C4 (noted "moment of deciding" phrase seeded 4×) | Vary the subtitle. Use "the moment of deciding" once, in §0, and not in subtitle. |
| **P0.2** | **"The work is unmistakably mine. The accelerant is the AI."** — C2 still wants these as the *literal* last two sentences of the post (currently §What's next CTA comes after). C3 calls them marketing copy + flags "unmistakably" as a defensive adverb. | C2 (wants placement change), C3 (wants tone change) | Two-part fix: (a) drop "unmistakably" → "The work is mine. The accelerant is the AI." (resolves C3); (b) move the CTA above these lines or merge §Where I am + §What's next so these are the actual close (resolves C2) |
| **P0.3** | **"Perfectly inverted"** in Tata Steel paragraph overclaims (N=4 on 1 stock = observation, not pattern) | C3 explicit; C4 doesn't catch directly | Soften: "the signal pointed the wrong direction at every data point I tested" |
| **P0.4** | **"None of that was learnable by reading about it"** — Piotroski-on-cyclicals IS in academic literature, just not in retail textbooks | C3 explicit | Rephrase: "none of that showed up in the textbooks most retail investors actually read" |

### Single-critic flags (priority P1 — strongly recommend)

| # | Issue | Critic | Fix |
|---|---|---|---|
| **P1.1** | Generic three-sentence opener (screeners / YouTube / WhatsApp) is "the only thing still sounding like every other investing blog" | C1 | Cut to one sentence |
| **P1.2** | "Something that..." ×4 anaphora at end of §What I'm trying to solve | C4 (also Claude's own review) | Vary openings: "Something that knows my portfolio. One that reasons in plain English. One that pushes back when I drift. The opposite, basically, of what most apps optimise for." |
| **P1.3** | "actually" used 8 times (target 3) | C4 | Sweep — most can become "really" or be cut |
| **P1.4** | "What it explicitly does not do" is a 9-sentence run-on paragraph | C2 | Paragraph breaks. Each "no X" or "no Y" gets its own short paragraph or visual list |
| **P1.5** | "Nobody is building it / Almost nobody is building that" — still hedged universal, twice | C3 | Narrow to specific feature combination: e.g., "I haven't seen one that ingests *my* rules and pushes back on *my* drift in plain English" |
| **P1.6** | "Anthropic, OpenAI, Google" named — inside-baseball for retail audience | C1 (NEW concern in v0.2) | Revert to "the major AI labs" — was C2's v0.1 ask, but C1 says it's wrong for the audience |
| **P1.7** | Naming line conflict resolution | C1 vs C2 | Side with C1 (audience > craft) |
| **P1.8** | Line 3 ("*Draft v0.2 — incorporates feedback from all 5 reviewers...*") will render as visible italicized text on Medium | C5 | Delete before publishing |
| **P1.9** | No inline image — distribution penalty on Medium | C5 | Add at least one (rough mock of the weekly report = enough) |
| **P1.10** | Follow-ask was removed when CTA was simplified | C5 | Restore: "If you'd like to follow this build, I'll write more as it goes." above the comment question |
| **P1.11** | "The bot is the opposite of that" — vague | C2 | Specify what the opposite IS |
| **P1.12** | "plain English" used 3 times — tic | C2 | Vary in 2 of 3 places |
| **P1.13** | "honestly" subhead ("Where I am right now, honestly") | C2 | Drop "honestly" — the section title is doing the work |
| **P1.14** | Double antithesis in §5: "The point isn't X, it's Y" followed by "The value isn't X, the value is Y" in same passage | C4 | Break one of the two |
| **P1.15** | Title doesn't capture behavioural-rules angle ("stock portfolio" undersells) | C5 | Test alt: e.g., "I'm building an AI to argue with me about my own investing rules." Or keep current — minor. |

### Claude's own additional flags (not flagged by critics, but worth doing)

- Contraction inconsistency: ~6 lines uncontracted (*"I am using Claude" / "That is how they earn" / "There is a long road" / "It is about who avoided" / "That is a useful thing" / "That kind of answer is exactly what is going to shape"*). Sweep to *I'm / it's / that's*.
- Opening line *"Every investor has done this dance."* — slightly clichéd. Optional alt with more bite: *"There's a moment, after you sell a stock and watch it triple, when you realise the problem isn't the stock. The problem is you."*

---

## 4. Critic divergences to resolve

| Issue | Position A | Position B | Recommended resolution |
|---|---|---|---|
| Naming "Anthropic, OpenAI, Google" | C2 (v0.1) said NAME THEM | C1 (v0.2) says inside-baseball, revert to "major AI labs" | Revert per C1 — the audience is retail investors, not tech readers |
| The 2 "best sentences" / closing | C2 says LITERALLY end on them | C3 says marketing copy | Drop "unmistakably" (resolves C3); merge §Where I am + §What's next so the lines do close (resolves C2) |

---

## 5. v0.3 revision plan — concrete

If you greenlight, this is what changes in v0.3. ~12–15 edits + 1 structural move. Estimated 30 min focused work.

### Structural
1. **Merge §Where I am + §What's next** so *"The work is mine. The accelerant is the AI."* is the actual close, with the CTA appearing inline just above.
2. **Break the 9-sentence "explicitly does not do" run-on** into short visual paragraphs.

### Content / claim
3. **Soften "perfectly inverted"** → *"the signal pointed the wrong direction at every data point I tested"*
4. **Rephrase "none of that was learnable by reading about it"** → *"none of that showed up in the textbooks most retail investors actually read"*
5. **Narrow "I haven't seen anyone building it"** + **"Almost nobody is building that"** → specific feature combination
6. **Specify "the bot is the opposite of that"** — say what the opposite IS
7. **Cut the screeners/YouTube/WhatsApp sequence** to one sentence
8. **Restore "major AI labs"** in place of named companies (revert per C1)

### Voice
9. **Drop "unmistakably"** → *"The work is mine. The accelerant is the AI."*
10. **Vary the "Something that..." ×4 anaphora**
11. **Cut "actually" hard** (8 → 3 max)
12. **Break one of the double antithesis pair** in §5
13. **Contraction sweep** — *I'm / it's / that's* throughout
14. **Vary "plain English"** in 2 of 3 places
15. **Drop "honestly"** from §Where I am subhead

### Medium-platform
16. **Delete line 3 metadata** (the "*Draft v0.2 —*" line)
17. **Vary the subtitle** so it doesn't restate §0 ¶1
18. **Restore follow-ask** above the comment CTA
19. **Identify one inline image** (description, not the file itself — you'd produce it)

### Optional (your call)
20. **Replace opening "Every investor has done this dance."** with a sharper alternative
21. **Sharpen title** to capture behavioural-rules angle (or keep current — minor)

---

## 6. Predicted verdicts after v0.3

| Critic | Predicted v0.3 verdict |
|---|---|
| C1 — Retail reader | SHIP-AS-IS or minor |
| C2 — Editorial | SHIP-AS-IS — if the close is fixed |
| C3 — Skeptic | NEEDS-MINOR-EDITS or SHIP — if overclaims softened |
| C4 — Voice authenticity | **The risk** — "actually", "Something that...", and double antithesis must all be fixed to get to SOUNDS HUMAN |
| C5 — Medium platform | SHIP-AS-IS — once the metadata line and inline image are handled |

C4 is the gating critic. If we don't fix the 3 things C4 flagged (actually count, anaphora block, double antithesis), the post still sounds part-AI.

---

**End of synthesis. Awaiting Pranav's review + decisions before writing v0.3.**
