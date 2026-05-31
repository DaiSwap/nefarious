# Blog Post #3 Plan — Review Synthesis (all 5 critics)

**Status**: 🔄 Initialized — reading 6 input files.
**Date**: 2026-05-31
**Inputs**: `blog_post_03_plan.md` + 5 critic reviews (C1–C5)
**Output target**: Revision brief → drives `blog_post_03_draft_v0.1.md`

This synthesis is longer than Blog #2's because the critics found bigger structural issues. The math claim is higher-stakes, the sample-size problem is real, and the reframing in §4 has a factual gap. None of these require scrapping the post — the mechanism is independently strong. But they do require specific fixes at the plan stage, not patch-fixes in draft.

---

## §1 — Cross-critic verdict

| Critic | Verdict | One-line summary |
|---|---|---|
| C1 — Target reader | REWORK | Data surprised me; four-date sample almost lost me; the §6 fix is only for programmers. Fix those three and I'll share it. |
| C2 — Editorial | NEEDS-REWORK | Bones are good; hook needs tightening; §5/§5b split is a structural seam; Stock X/Y is a memory tax; "quietly extended" carries an accusation. |
| C3 — Skeptic | NEEDS-WALK-BACK | The mechanism is strong and independent; the N=4 evidence framing is overextended and the Mar-2020 data point is confounded by COVID macro. |
| C4 — Voice | NEEDS-VOICE-WORK | Not AI-dominant, but 8 specific AI-tell phrases will show if carried into draft unchallenged; two "It's not X. It's Y." constructions are the highest-severity items. |
| C5 — Medium fit | NEEDS-OPTIMIZATION | Strong curation ingredients; three platform problems: read time outside sweet spot, diagram volume high, Stock X/Y naming causes scroll-amnesia. |

**Direction**: No critic says SHIP-AS-IS. No critic says FULL-REWRITE. The verdicts are heavier than Blog #2 (two critics use "WALK-BACK" or "REWORK" language) because the structural issues are deeper — specifically the sample-size framing and the §4 factual gap. Fix those in the plan stage, and the draft writes itself.

---

## §2 — Cross-critic AGREEMENTS (3 or more critics flagged independently)

### Agreement 1 — N=4 sample-size concern (P0)
**Critics**: C1 (explicit P0), C3 (explicit, called it "an anecdote dressed in humility"), C5 (implicit — "one-stock problem is the most Medium-specific problem in the plan")

All three flag the same structural issue from different angles. C1 notes the four dates are not independent — they are all readings on the same stock's single cycle, giving one effective degree of freedom, not four. C3 adds the selection-bias vector: the post chose the stock it already had data on, which is likely the stock that motivated the hypothesis. C5 notes this is damaging on Medium specifically because skeptical comments land in the recommendation algorithm's engagement scoring.

The plan's proposed hedge ("I tested it on one stock at 4 dates. That's not statistical proof. But the pattern lines up with how cyclicals work in theory, so I think the finding will hold") was explicitly judged by C3 as insufficient: "That sentence is how post-hoc rationalization sounds when dressed in humility."

**Consensus fix**: Add one or two additional cyclical stocks as companion data points — even one sentence each ("I checked JSPL at March 2020 and saw the same inversion") converts the evidence from anecdote to pattern. C1 named JSPL, SAIL, Hindalco specifically. C3 noted the March 2021 and March 2022 data points are the cleanest because they don't carry the COVID-dislocation explanation — lead with those.

---

### Agreement 2 — "It's not X. It's Y." AI construction (P0)
**Critics**: C4 (explicit, two instances flagged as High severity), C2 (flags "quietly extended" framing in §4 as a tonal risk — the same underlying sentence pattern), C3 (indirectly — calls the §4 claim "factually incomplete")

C4 identified two specific instances:
- §4: *"It's not that Piotroski is wrong. It's that he never said this was for cyclicals."*
- §6: *"It's not perfect. But it's better than the textbook version for this class of stock."*

C4 labels both High severity because this is the single most recognizable AI rhythmic pattern in writing — clean parallel structure that protects the cited source and sets up a nuanced distinction. A human writer who has actually been burned by the F-Score would be less lawyerly. C2 flags the same §4 sentence for the word "quietly" (different facet, same sentence). C3 flags the underlying §4 claim as factually incomplete (see Agreement 4 below).

**Consensus fix**: Rewrite both instances before drafting. C4 provides three options for each (§3 of the Voice review). The best options are quoted in §6 of this synthesis.

---

### Agreement 3 — §5/§5b structural split awkwardness (P1)
**Critics**: C2 (explicit — "the §5/§5b split is an editorial seam; merge §5b into §6"), C4 (implicit — §5b checklist is authentic but its placement makes the post feel 7.5 sections long), C5 (recommends cutting either §5b to a 5-item list or splitting the post into two)

C2's diagnosis is sharpest: §5b is not a continuation of §5 (which is a worked example of Stock Y). §5b is a reader-assistance device — "how do you know if you're looking at a cyclical?" — and belongs adjacent to the solution, not to the contrast. The merge option (§5b + §6 = one combined ~400-word section) gives the post two heavy sections — the evidence and the so-what — which is the right structural shape.

**Consensus fix**: Merge §5b into §6 with a bridge sentence. C2 suggests: "The difference between these two stocks comes down to one question: does the company's business have a cycle?" C3 agrees the §5b checklist has value independent of the empirical question and should be kept. The question is placement, not existence.

---

### Agreement 4 — March 2020 confounded by COVID macro (P0)
**Critics**: C3 (explicit, dedicated section — "Mar-2020 is doing a lot of work, and it is not doing what the post thinks"), C1 (implicit — flags selection bias for "why March 2020"), C2 (does not flag this directly, but the "one careful sentence" note on §4 points adjacent)

C3's argument is decisive: the +355% from March 2020 can be explained entirely by "everything was cheap in March 2020, and leveraged cyclicals gave 3-4x the market return in COVID recovery." The post attributes the return to cyclical-specific F-Score inversion. Without ruling out the macro explanation, the data point does not cleanly support the cyclical-specific argument.

The cleanest evidence for the cyclical argument is March 2021 (F=8, +34%) and March 2022 (F=7, ~0%) — where the F-Score was high and the stock was at or past the cycle peak. Those data points do NOT carry a COVID explanation.

**Consensus fix**: Lead with March 2021 + March 2022 as the core evidence. Demote March 2020 to a supporting data point with an explicit note: "March 2020 was also a global macro dislocation — the cyclical argument is harder to isolate there." Also: cut the March 2024 row from the table (C1 explicit, C2 explicit — incomplete window gives sceptics a free shot).

---

### Agreement 5 — §6 is not actionable for retail investors (P0)
**Critics**: C1 (explicit P0 — "this is the 'you need a programmer to do this' problem"; score 4/10), C2 (flags the "5-year-average" as requiring an illustrative calculation to be concrete), C4 (implicit — the smoothness of "It's not perfect. But it's better" closes off the substance before it can appear)

The 5-year-average version of the F-Score is only accessible if you can write Screener.in formula syntax or export to Excel. Retail investors on Tickertape cannot run this with existing tools. The plan does not address this gap.

C1 offers two options: (A) be explicit this is a programmatic fix and give a manual proxy ("if you're looking at a metal or fertiliser stock, scroll back five years on Screener.in and eyeball whether this year's margins are high or low relative to that history"); (B) give a P/B-based proxy ("if P/B is near a 5-year high and the F-Score is above 7, that combination has historically been the worst time to enter"). Option A is more honest; Option B is more actionable. Either is better than the current plan.

**Consensus fix**: Add a manual proxy for retail investors who cannot run the 5-year-average version. Frame the 5-year-average as "what I do in my system" (programmatic) and the manual proxy as "what you can approximate on Screener.in without custom formulas."

---

### Agreement 6 — Stock X / Stock Y naming (P0/P1)
**Critics**: C2 (explicit — "programmer notation, not reader notation"; recommends descriptive short-names), C5 (explicit — the variable-stock problem on Medium is most damaging; recommends "the Metals Stock" / "the Consumer Goods Stock"), C1 (implicit — "any NIFTY-100 investor who was around in 2020-2022 knows exactly which metal stock you're talking about" suggests descriptive anchoring is possible)

C2 and C5 agree on the problem but diverge slightly on the solution. See §3 (Disagreements) for the full resolution.

---

## §3 — Cross-critic DISAGREEMENTS

### Disagreement 1 — Naming convention: "Company A/B" vs "the Metals Stock" vs "the Consumer Goods Stock"

C2 notes that Blog #1 used "Company A" and "Company B" for the same underlying companies (Tata Steel / Asian Paints). Introducing "Stock X / Stock Y" in Blog #3 creates a naming inconsistency for readers who have read Blog #1. C2 recommends either matching Blog #1 ("Company A/B") or using descriptive short-names ("the metals stock", "the paints stock").

C5 goes further: recommends "the Metals Stock" and "the Consumer Goods Stock" specifically, with the letters appearing once in parentheses at introduction ("I'll call it the Metals Stock — Stock X in this post") as a concession to convention. C5's reasoning is Medium-specific: descriptive names activate the reader's schema and persist across 2000 words; algebraic letters do not.

**Recommendation: Use "the Metals Stock" / "the Consumer Goods Stock" (C5 pick).** Reasoning: (a) memorability wins on Medium's long-scroll format; (b) Blog #1's "Company A/B" convention doesn't have to be carried forward — the series is still early enough to retire it; (c) "the Metals Stock" does the same anonymization work as "Stock X" while giving the reader a cognitive anchor they can hold across sections. The parenthetical letter at first introduction ("I'll call it the Metals Stock throughout this post") serves readers who noticed the Blog #1 convention.

**Pranav's call**: If Blog #1 consistency matters more than memorability, use "Company A/B" and note the re-labeling from Blog #3. Default is Metals Stock / Consumer Goods Stock.

---

### Disagreement 2 — Cut Stock Y or keep it

C1 and C5 both indicate Stock Y is expendable under certain conditions. C1: "if Stock Y uses illustrative numbers, cut it to a single prose paragraph — the post becomes a 1500-word piece with one stock, a tighter argument, and no credibility risk." C5: Option A (split Stock Y into a separate post) as the primary length-reduction strategy.

C3 (Skeptic) implies Stock Y is structurally necessary but must use real data: "you cannot compare a real failure against a hypothetical success and draw a conclusion about the failure mode." If Stock Y uses illustrative numbers, keeping it is worse than cutting it.

C2 (Editorial) treats Stock Y as architecturally correct — "showing the F-Score failing on Stock X and then working on Stock Y is a stronger argument than showing it failing alone. The contrast proves the point is surgical." C4 (Voice) agrees implicitly — "the two-stock comparison structure is structurally honest in a way that does not require hedging language."

**Recommendation: Keep Stock Y, but only with real data.** The contrast is architecturally necessary. C3's "illustrative is a broken positive control" concern is decisive: illustrative numbers in §5 actively undermine the real data in §3, because readers who notice the asymmetry will question both. Real Asian Paints pre-2021 data (which exists in the project files at `12_cycle_A_test_v0.1.md`) should be used. If the data is messy, one prose paragraph ("I ran the same check on a large consumer-goods business and the F-Score tracked the stock direction much more closely") is better than an illustrative table.

**Pranav's call**: Does the Asian Paints pre-2021 hand-compute data tell a clean enough "F-Score worked" story at 4 dates? If yes, use it. If no, cut the Stock Y table to prose — one paragraph, no table, no illustrative numbers.

---

### Disagreement 3 — Real vs illustrative data for Stock Y

This is the same disagreement as above, resolved the same way. The Skeptic's concern is the most structurally serious finding in any of the five reviews: **illustrative numbers as a positive control invalidate the post's inference**. This is not a style note — it is a logical error. See §5 (P0 list) for the full action item.

---

## §4 — Per-critic standout findings

### C1 — Target reader: key findings beyond cross-critic agreements

**Sample-size: add a second metal stock.** C1 is the most specific critic on this: one sentence per additional stock (JSPL or SAIL) is enough. "I ran the same check on JSPL at March 2020 and saw F=4 and +280% forward" — that changes the evidence from one stock to two, which is qualitatively different. C1 also notes the most trust-building move in the post would be admitting one case where the inversion did NOT hold: "I looked at Hindalco at the March 2020 trough and the F-Score was 6 — the inversion was there but smaller." Acknowledging a messy data point does more for credibility than a clean table.

**Gantt chart is the wrong diagram type.** Gantt charts communicate duration and sequence, not direction. Diagram 2 needs to show inversion — the mismatch between F-Score signal direction and stock price direction. A Gantt chart cannot do this. C1 flags the plan's own note ("could use a flowchart with up/down arrows instead") as the right call. The flowchart alternative is confirmed as the correct choice.

**§5b sector checklist is underrated.** C1 explicitly names §5b as the section most likely to force retail readers to confront whether they have ever applied the F-Score to a cyclical. "If the post names something I own — auto-ancillary, fertiliser — I'll go and check my own holding." This is the highest-quality engagement outcome for the post. §5b should be kept even if Stock Y is cut.

**The specific temporal gap.** C1 asks for "the specific month when the stock price started moving vs when the F-Score moved." If Stock X's price started moving in October 2020 and the F-Score only crossed 7 in March 2021, that five-month gap concretises the lag argument more than the table does. One sentence with two specific dates.

---

### C2 — Editorial: key findings beyond cross-critic agreements

**Drop the March 2024 row.** The "(incomplete window, lagging)" notation in the March 2024 row makes the dataset look incomplete and gives sceptics a free shot. Two options: cut the row and note in prose that the four-year window is still open, or move it to a single sentence below the table. Do not leave it as a row-peer of the other three.

**Merge §5b into §6.** Detailed in Agreement 3 above. The combined section at ~400 words becomes the second heavy section of the post, matching §3's weight. Right structural shape.

**"Quietly extended" carries an accusation.** Replacing it with "Indian investing books picked it up — reasonably — and applied it across all types of stocks. Cyclicals were never part of the original test. That's the gap." attributes the extension to good-faith adoption, not concealment. Puts "reasonably" in the sentence.

**Links in the closing.** C2 recommends moving Blog #1's link to §1 (where the post introduces the personal project context) and Blog #2's link to §4 or §6. Final paragraphs on Medium get skimmed; links buried there generate low clickthrough. §7 should end on the learning, not on the navigation.

**Hook: five sentences, not six.** Cut sentence 1 (reader-flattery setup) and cut "The first few tests went fine" (throat-clearing). The remaining five sentences are clean and the contradiction lands immediately in sentence 3.

---

### C3 — Skeptic: key findings beyond cross-critic agreements

**March 2020 is confounded by COVID macro — see Agreement 4.** The cleanest cyclical evidence is March 2021 + March 2022. The post should lead with those two data points.

**"Piotroski never said this was for cyclicals" is factually incomplete.** This is C3's highest-severity structural finding. The full argument: Piotroski (2000) targeted high B/M stocks — value stocks. Cyclicals at the bottom of their cycle frequently trade at distressed valuations with high B/M ratios. Tata Steel in March 2020 was almost certainly trading at high B/M — exactly Piotroski's intended universe. So the claim "he never said this was for cyclicals" is wrong in an important way: cyclicals at troughs ARE the high-B/M universe Piotroski was targeting. The counter-argument a technically literate reader will make is: "Piotroski's design actually covers cyclicals at troughs."

The sharper and more precise reframe: "Cyclicals at cycle troughs often look like the high-B/M stocks Piotroski was studying. But within that universe, the F-Score still fires at the wrong time for cyclicals — because the B/M is elevated due to price collapse, not because the business is permanently distressed. The recovery of a cyclical is cycle mean-reversion, not value realization. Piotroski's alpha came from separating genuinely improving distressed businesses from deteriorating ones — cyclicals at troughs are genuinely deteriorating by every YoY metric, and they will still recover because the cycle turns." This is a stronger argument, and it preempts the technically literate reader's counter.

**TA corroboration sentence.** The project apparently found that technical analysis shows the same inversion pattern for cyclicals (same mean-reverting-asset logic). One sentence in §4 or §6 noting this cross-validation would materially strengthen the N=4 evidence: "When I tested momentum indicators on the same stock, the inversion was there too — momentum was lowest at entry and highest at the peak. That made me more confident I wasn't seeing something specific to the F-Score." Does not make the blog about TA; uses TA as cross-validation.

**The 5-year-average fix is hypothesis, not validated improvement.** C3 flags five specific claims that are overextended (detailed in §5 P1 items). The "it's better" claim about the 5-year version is one of them. Replace with "I think it might be better, but I haven't tested that yet."

**The +355% number needs a data-source statement.** What index date? BSE/NSE adjusted closing? Price return or total return including dividends? One line in a footnote or parenthetical is enough. Steel companies pay variable dividends during cycle peaks — if dividends are excluded, the post should say so.

---

### C4 — Voice: key findings beyond cross-critic agreements

**Two "It's not X. It's Y." constructions — see Agreement 2.** Both are High severity. The §4 instance ("It's not that Piotroski is wrong. It's that he never said this was for cyclicals") is the most AI-sounding sentence in the entire plan. The §6 instance ("It's not perfect. But it's better") closes off detail before it can appear. Both require rewrites before drafting begins.

**"(No shortcuts. Real numbers.)" is the best voice moment in the plan.** Keep verbatim. C4 flags this as "the best sentence in the plan" — it is specific, slightly defensive in the right way, and does not perform humility. It asserts something the writer earned.

**"That second part is the kicker."** Keep. Short, unpolished, Blog #1 energy.

**Performed humility vs genuine learning-voice.** C4 distinguishes: genuine learning-voice has a specific shape of uncertainty (knows what it found, knows the limits, asks specific questions). Performed humility hedges everything uniformly. Specific phrases to avoid as blanket qualifiers: "from what I'm seeing" (weakens every sentence), "I might be wrong about this" (epistemically hollow — too general), "would love feedback from anyone" (Community-Building Language, not a real question). Specific uncertainty is more honest and more confident than general hedging.

**The §5b sector checklist reads as field notes.** C4 agrees with C1: the list is concrete, not exhaustively manicured, and recognisable to the target reader. It will not need voice fixes.

**"This is what I'm doing for the whole system I'm building."** AI-tell: thesis-statement texture, too complete. Human alternative: "That's kind of become the pattern for this whole project — find where the imported math breaks, figure out why, patch it or flag it. Repeat."

---

### C5 — Medium fit: key findings beyond cross-critic agreements

**Rename Stock X/Y to "the Metals Stock" / "the Consumer Goods Stock."** See Disagreement 1. C5 is the strongest advocate for this change. Descriptive names activate reader schema; algebraic letters do not persist across 2000 words of scrolling.

**Diagram 1 as markdown table, not mermaid.** A clean 9-row markdown table renders natively in Medium's editor without an export step, preserves the same information, and takes 30 seconds to read. Reserve mermaid for diagrams where spatial relationships matter — the inversion diagram (§3) and the cycle loop (§4). This effectively makes the diagram count 3 mermaid + 1 table, satisfying the spirit of "4-5 visuals" within the Pranav lock.

**Length cut to 1800 words.** The 2000–2500 range produces a 10–12 minute read. Medium's curation sweet spot is 4–7 minutes; posts above 7 minutes have lower read-to-open ratios. Option B (compress and cut, target 1600 words) is the most practical without restructuring the post. The Pranav lock on length notes 1800–2200 as the original target — aiming for 1800 is achievable and keeps the post in range.

**Disclosure moves to §2, not §3.** By §3, readers who will be misled are already forming conclusions. The disclosure belongs immediately after the hook, before the data: "Before the numbers: this is from my own testing on one stock at four dates. It's not peer-reviewed research, and I might be wrong. I'm sharing it because the pattern surprised me."

**Subheads for TOC click-through.** C5 provides specific rewrites for all seven subheads (see §3 of C5 review). The two most important: §3 subhead ("The score said avoid. The stock tripled.") and §4 subhead ("The checklist reads where you are in the cycle, not how good the company is"). These are the two most generic subheads in the current plan.

**Title pick confirmed.** "A famous investing checklist gave me the opposite of the right answer" — 65 characters, fits Medium card view and push notifications without truncation. The other two candidates both truncate on mobile.

---

🔄 §1-§4 done. Drafting §5-§6 priority lists.

---

## §5 — Consolidated action list — prioritized

### P0 — Must fix before drafting

**P0.1 — Add a second cyclical stock to address the sample-size problem**
The N=4 from one stock does not support the directional claim. Add one sentence each for two additional metal/cyclical stocks (JSPL and SAIL are the cleanest candidates) showing the same inversion at the same trough date. You do not need tables — "I checked JSPL at March 2020 and the pattern held" is enough. Optionally add one messy data point (Hindalco, where the inversion was smaller) to build credibility through transparency. This single fix has the highest return-on-effort of any item in this list.
**Critics**: C1 (P0), C3 (implied), C5 (implied)
**Section**: §3

**P0.2 — Reframe central evidence: March 2021 and March 2022 are the clean data points; demote March 2020**
March 2020 is confounded by COVID macro — the +355% can be explained by "everything was cheap, leveraged cyclicals gave 3-4x market return." The cyclical-specific argument cannot be cleanly isolated for that date. Lead the evidence with March 2021 (F=8, +34%) and March 2022 (F=7, ~0%) — those two rows have no COVID explanation. Demote March 2020 to a supporting data point with an explicit caveat: "March 2020 was also a global macro dislocation, which makes the cyclical argument harder to isolate there." Also: drop the March 2024 row from the table entirely; move it to a single prose sentence below the table.
**Critics**: C3 (explicit), C1 (implicit), C2 (March 2024 row)
**Section**: §3

**P0.3 — Rewrite §4 reframe: "Piotroski never said this was for cyclicals" is factually incomplete**
The current framing will be challenged by any technically literate reader: cyclicals at troughs look like high-B/M value stocks — exactly Piotroski's intended universe. The sharper, more defensible argument: "Cyclicals at cycle troughs often look like the distressed value stocks Piotroski was studying — the B/M is high because the price has collapsed. But the F-Score fires at the wrong time for cyclicals because the recovery is cycle mean-reversion, not value realization. The fundamentals look genuinely bad at the trough and they will look genuinely good at the peak — and the stock price has already moved both times." This is a stronger claim that preempts the counter-argument rather than walking into it.
**Critics**: C3 (explicit, §Q5), C1 (implicit)
**Section**: §4

**P0.4 — Replace BOTH "It's not X. It's Y." constructions**
§4: "It's not that Piotroski is wrong. It's that he never said this was for cyclicals." → rewrite per C4 options (see §6 below)
§6: "It's not perfect. But it's better than the textbook version for this class of stock." → rewrite per C4 options (see §6 below)
Both are High severity voice tells. Rewrite before drafting begins — they will not be fixable in a voice pass after the draft is written.
**Critics**: C4 (both High severity), C2 (§4 instance has additional "quietly extended" problem)
**Section**: §4, §6

**P0.5 — Replace Stock X / Stock Y with "the Metals Stock" / "the Consumer Goods Stock"**
Rename at first introduction in §2. Hold consistently. Brief parenthetical acknowledgment of prior convention optional: "I'll call it the Metals Stock throughout this post." Do not alternate between "the Metals Stock" and "Stock X" — pick one and commit.
**Decision point**: If Pranav prefers Blog #1 consistency, use "Company A / Company B" instead. See Q1 in §7.
**Critics**: C2 (recommends descriptive names), C5 (explicit P0-equivalent recommendation)
**Section**: all

**P0.6 — Make §6 actionable for retail investors**
The 5-year-average version requires custom Screener.in formula syntax or Excel export. Most retail investors cannot run it. Add a manual proxy: "If you're looking at a metals or fertiliser stock, scroll back five years on Screener.in and eyeball whether this year's margin is near a five-year high. If it is, be cautious — even if the F-Score looks strong." Frame the 5-year-average as "what I do in my system" and the manual proxy as "what you can approximate without custom formulas." Also: frame the 5-year-average as a hypothesis, not a validated improvement — "I think it might be better, but I haven't backtested that yet."
**Critics**: C1 (P0, 4/10 score), C2 (needs illustrative calculation), C3 (explicit — "a different guess, not a validated fix")
**Section**: §6

**P0.7 — Cut length to 1800 words; trim §1 and the Stock Y section**
The 2000–2500 range is outside Medium's curation sweet spot. Achievable cuts: §1 (F-Score explanation) can be a table + 100 words rather than 250; §5/§5b merge (Agreement 3) removes the seam and saves ~50 words; §6 tightening (-50 words). Target: 1800 prose words + 3 mermaid diagrams + 1 markdown table.
**Critics**: C5 (explicit, most consequential Medium problem), C1 (lean toward 1500 if Stock Y uses illustrative numbers)
**Section**: all

**P0.8 — Move disclosure to §2, before the data**
The plan notes disclosure can go in §1 or §3. On Medium, §3 is too late — readers form impressions during the hook and §1. Placement: first paragraph of §2, before any data is presented. Suggested language: "Before the numbers: this is from my own testing on one stock at four dates. It's not peer-reviewed research, and I might be wrong. I'm sharing it because the pattern surprised me — and because I want to know if others have seen the same thing on other stocks."
**Critics**: C5 (explicit), C1 (early placement, §1 or before §3)
**Section**: §2

---

### P1 — Should fix

**P1.1 — Rewrite the hook: cut sentence 1 and the "first few tests went fine" clause**
Sentence 1 ("If you read Indian investing books…you've probably heard") is reader-flattery with epistemic hedging. C2 recommends starting with the rule ("The Piotroski F-Score is a 9-point checklist"). C4 recommends starting in the action ("I was six months into building my investing system when…"). Cut "The first few tests went fine" entirely — it defers the surprise. Hook should be 5 sentences, not 6.
**Critics**: C2 (explicit Rewrite 1 + Rewrite 2), C4 (Hook §Q1 — Medium severity)
**Section**: Hook

**P1.2 — Replace "quietly extended" with charitable framing**
The word "quietly" implies the Indian investing community knew the F-Score was not designed for cyclicals and did it anyway. That is uncharitable and probably wrong. Replace with: "Indian investing books picked it up — reasonably — and applied it across all types of stocks. Cyclicals were never part of the original test. That's the gap." The word "reasonably" does the tonal work.
**Critics**: C2 (explicit Rewrite 3), C4 (same sentence as the "It's not X" construction)
**Section**: §4

**P1.3 — Add TA corroboration sentence**
One sentence in §4 noting that technical momentum signals showed the same inversion on the same stock would strengthen the N=4 evidence as cross-validation. It does not make the post about TA; it shows the inversion is a property of any backward-looking indicator applied to mean-reverting assets, not something specific to the F-Score. C3 is the only critic who flagged this, but the impact is high given how much the post currently rests on N=4 from one framework.
**Critics**: C3 (explicit §Q7)
**Section**: §4

**P1.4 — Add data-source statement for the +355% number**
One line: what price date, BSE/NSE adjusted closing, and whether dividends are included. Steel companies pay variable dividends at cycle peaks — if dividends are excluded, the post should say so. A technically literate reader who checks the number and finds a different figure can undermine the entire post. One parenthetical protects against this.
**Critics**: C3 (explicit, Claim 2)
**Section**: §3 (footnote or parenthetical in the table)

**P1.5 — Rewrite the closing link structure**
Move Blog #1's link to §1 (project context). Move Blog #2's link to §4 or §6 (AI-arguing-with-itself methodology is relevant there). Do not save both links for §7. §7 should end on the learning, not on navigation. Final line of §7 should close the intellectual arc, not send the reader somewhere else.
**Critics**: C2 (explicit), C5 (recommend one link in §7, not two)
**Section**: §7

**P1.6 — Confirm Stock Y uses real data or cut to prose**
Real Asian Paints pre-2021 data exists in the project at `12_cycle_A_test_v0.1.md`. Check whether it tells a clean "F-Score worked" story at four comparable dates. If yes: use it, explicitly stating the dates and the source. If the data is messy: one prose paragraph — "I ran the same check on a large consumer-goods stock and the F-Score tracked the stock direction much more closely" — is better than an illustrative table. Do not use illustrative numbers as a positive control alongside real data in §3.
**Critics**: C1 (explicit — "use real numbers or cut to a paragraph"), C3 (explicit — "illustrative numbers as positive control invalidates the inference")
**Section**: §5

**P1.7 — Rewrite the §5b "NIFTY 100" generalization**
The plan's current §5b language: "For FMCG, IT services, private banks, pharma — most of NIFTY 100 — the F-Score works closer to as intended (based on what I've tested so far)." This is a sector-level claim covering FMCG, IT, banks, pharma based on N=1 non-cyclical tested. Replace with: "For the non-cyclical stock I tested, the F-Score moved in the expected direction." Do not generalize to sectors not tested.
**Critics**: C3 (explicit, Claim 4)
**Section**: §5b / merged §6

---

### P2 — Nice to have

**P2.1 — Add the specific month when Stock X's price started moving vs when the F-Score turned positive**
One sentence: "Stock X's price started recovering around October 2020. The F-Score didn't cross 7 until March 2021 — five months later." This concretises the lag argument more than four rows in a table. If this data is available (it should be from the Tata Steel hand-compute work), add it. High value for one sentence of effort.
**Critics**: C1 (explicit), C2 (implicit — "one illustrative calculation" note in §6)
**Section**: §4

**P2.2 — Rewrite subheads for TOC click-through**
C5 provides specific rewrites for all seven subheads. The two highest-priority: §3 ("The score said avoid. The stock tripled.") and §4 ("The checklist reads where you are in the cycle, not how good the company is"). Current subheads for those sections are generic and lose TOC click-through on Medium.
**Critics**: C5 (explicit, §Q3)
**Section**: All section headings

**P2.3 — Sweep performed-humility phrases**
Phrases to use sparingly or replace with specific uncertainty: "from what I'm seeing" (acceptable once, not as a blanket qualifier), "I might be wrong about this" (replace with "I only tested one stock at four dates"), "the data I have so far suggests" (one instance fine; three is a tic), "would love feedback from anyone who's tested this" (replace with specific ask: "if you've run F-Scores on fertiliser or steel stocks, I'd be curious what you found"). C4's guidance: genuine learning-voice has a specific shape of uncertainty; performed humility hedges everything uniformly.
**Critics**: C4 (explicit, §Q7)
**Section**: §3, §6, §7

**P2.4 — Roughen the "matched the market — boring" landing**
The word "boring" is a placed punchline that reads as AI precision. C4 alternative: "The stock just sat there. Two years, roughly flat, maybe up with the market." The messier landing is more human.
**Critics**: C4 (Low severity)
**Section**: Hook

**P2.5 — Address Mermaid rendering on Medium**
All mermaid diagrams must be exported to PNG or SVG and embedded as images. Medium's native editor does not render mermaid blocks — they appear as code blocks. This is a production step the plan does not address. With three mermaid diagrams remaining (§3 inversion, §4 cycle loop, §5 Stock Y comparison) after Diagram 1 becomes a table, the export step is manageable but should be explicitly planned.
**Critics**: C1 (explicit, Score 6/10), C5 (implicit — "export step" note)
**Section**: Production note

---

### P3 — Defer

**P3.1 — Optional Diagram 5 (§5b "where F-Score works vs where it breaks")**
The lowest-ROI diagram in the plan. C5 recommends replacing it with a bulleted list (the content is already a list in the plan). C4 agrees it will not need voice fixes. Keep the list; retire the diagram concept.

**P3.2 — Backtest of 5-year-average F-Score**
C3 flags that "it's better" is speculation without a backtest. The post should frame it as a hypothesis. The actual backtest — comparing 5-year-average F-Score vs standard F-Score on Tata Steel across multiple cycles — is valuable but out of scope for this blog post. Flag as a future post or a future Cycle A refinement.

**P3.3 — Tag strategy refinement**
C5 provides a 5-tag recommendation (Indian Stock Market, Investing, Personal Finance, Quant Investing, Data Science). Correct and implementable at publish time. Not a pre-draft concern.

---

## §6 — Specific rewrite suggestions for the draft

Each formatted as: Original → Rewrite → Reason

---

**Rewrite 1 — Hook sentence 1 (reader-flattery opener)**

Original:
> "If you read Indian investing books or watch the popular YouTube channels, you've probably heard about the Piotroski F-Score."

Rewrite (Editorial, Option A):
> "The Piotroski F-Score is a 9-point checklist. Score 8 or 9 and the company is a strong buy. Score 3 or below and it's a sell."

Reason: Starts with the rule, not with the reader's assumed media habits. Works for both the reader who knows the F-Score (reminder) and the reader who doesn't (clean intro). Does not presuppose media consumption. C2 provides the full revised 5-sentence hook using this opening.

---

**Rewrite 2 — Hook sentence 3 ("first few tests went fine" throat-clearing)**

Original:
> "A few months ago I built it into my own investing system and tested it on real Indian stocks. The first few tests went fine."

Rewrite:
> "A few months ago I built it into my own investing system and tested it on real Indian stocks."

Reason: Hard stop. The next sentence delivers the contradiction immediately. "The first few tests went fine" signals to the reader that nothing interesting has happened yet. Delete it. (C2, Rewrite 2)

---

**Rewrite 3 — §4 "Piotroski never said this" (both the "quietly extended" problem and the factual gap)**

Original:
> "It's not that Piotroski is wrong. It's that he never said this was for cyclicals. The original paper was about value stocks. The Indian investing community quietly extended it to all stocks. That extension is where the problem lives."

Rewrite (combining C3's factual correction with C4's voice note):
> "Piotroski's original paper was about US value stocks — companies trading at a big discount to their book value. Cyclical stocks at the bottom of their cycle look exactly like that. The price has collapsed; the book value hasn't changed. So these stocks land in Piotroski's universe. But the F-Score still fires at the wrong time — because the fundamentals look bad at the trough and good at the peak, while the stock price has already done the opposite move. The recovery is the cycle turning, not the company's quality improving. Indian investing books picked up the F-Score — reasonably — and applied it to everything. Cyclicals were the gap nobody tested."

Reason: (1) Fixes the factual incompleteness (cyclicals at troughs ARE in Piotroski's universe); (2) Replaces both AI constructions; (3) Replaces "quietly extended" with "reasonably." (C2 Rewrite 3 + C3 §Q5 + C4 §Q3)

---

**Rewrite 4 — §6 "It's not perfect. But it's better."**

Original:
> "It's not perfect. But it's better than the textbook version for this class of stock."

Rewrite (C4 Option A — names the imperfection and explains the specific improvement):
> "The 5-year average version has its own problems — if a company went through a one-time restructuring, the average absorbs it badly. But for a normal cyclical, it stops the signal from screaming BUY at exactly the wrong moment. That's enough for me to use it — though I haven't backtested whether it actually improves the signal across more stocks and more cycles. That's the next step."

Reason: Names the imperfection concretely (as C4 prescribes), frames the improvement as hypothesis not validated fix (as C3 prescribes), and keeps the "still learning" voice credibly. (C3 §Q6 + C4 §Q4)

---

**Rewrite 5 — §4 "smart money has already bid up the stock"**

Original:
> "By the time the F-Score is telling you 'things are improving', the smart money has already bid up the stock."

Rewrite:
> "By the time the F-Score turns positive, the stock price has already moved. In the case I looked at, the price started recovering roughly five months before the F-Score crossed 7."

Reason: C3 flags "smart money" as an unsourced claim about market efficiency and institutional behavior. Hedging to "in the case I looked at" with a specific timing data point (if available) replaces an assertion with evidence. (C3, Claim 1)

---

**Rewrite 6 — §7 closing sentence**

Original:
> "If you want to follow along: [link to blog #1] explains what I'm building and why. [Blog #2 link] is about how I make the AI argue with itself to find these things."

Rewrite (C2 Rewrite 5):
> "I tested this checklist expecting it to work. It didn't — not here, not on this kind of stock. That gap is what I'm building toward closing."

Then: Link to Blog #1 naturally inline earlier in the post (§1, when the project is introduced). One link in §7, not two.

Reason: Ends on the project's emotional logic, not on navigation. Consistent with "still learning" voice. The links move to where they're contextually relevant, not where they're convenient. (C2 Rewrite 5 + C5 §Q7)

---

**Rewrite 7 — "would love feedback from anyone who's tested this on more stocks"**

Original (plan tone guidance):
> "would love feedback from anyone who's tested this on more stocks"

Rewrite (C4 §Q7):
> "I ran this on one stock at four dates. If you've computed F-Scores on fertiliser stocks, steel peers, or oil refiners at cycle troughs, I'm curious whether the inversion pattern holds there too — or whether it's specific to how this stock's cycle works."

Reason: Genuine learning-voice asks a specific question. Community-Building Language ("would love feedback from anyone") is an engagement prompt AI generates, not a real ask. Specific uncertainty is both more honest and more compelling. (C4 §Q7)

---

**Rewrite 8 — "This is what I'm doing for the whole system I'm building."**

Original (plan §7):
> "This is what I'm doing for the whole system I'm building."

Rewrite (C4 §Q6, Option A):
> "That's kind of become the pattern for this whole project — find where the imported math breaks, figure out why, patch it or flag it. Repeat."

Reason: Less thesis-statement smooth. More like someone thinking aloud than summarizing. The roughness is the tell that it's human. (C4 §Q6)

---

## §7 — Open questions for Pranav before drafting

Eight binary decisions. Defaults shown; override where you disagree.

**Q1 — Naming convention**
"the Metals Stock / Consumer Goods Stock" (Medium recommendation; memorability wins on long scroll) vs "Company A / B" (Blog #1 consistency)?
**Default: the Metals Stock / Consumer Goods Stock.** Blog #1's A/B convention can be retired — the series is early enough. If Blog #1 consistency is a priority, use Company A/B.

**Q2 — Add second metal stock?**
Yes — C1 and C3 both say this is the fix with the highest return on effort. Which one: JSPL / SAIL / Hindalco?
**Default: JSPL + SAIL, one sentence each.** SAIL has a cleaner cycle; JSPL gives geographic diversity. Optional: one sentence on Hindalco noting the inversion was smaller there (trust-building transparency).

**Q3 — March 2020 demotion**
Lead with March 2021 + March 2022 as clean cyclical evidence; demote March 2020 to supporting data point with COVID-dislocation caveat?
**Default: yes.** C3's argument is decisive on this. March 2021/2022 are defensible; March 2020 is not, against a technically literate reader.

**Q4 — Stock Y: real data or prose paragraph?**
Does the Asian Paints pre-2021 hand-compute data (in `12_cycle_A_test_v0.1.md`) tell a clean "F-Score worked" story at 4 comparable dates? If yes: use it. If messy: one prose paragraph, no table, no illustrative numbers.
**Default: real data if clean; prose if messy. Under no circumstances use illustrative numbers as the positive control.** (C3's "broken positive control" concern is the most serious logical finding across all five reviews.)

**Q5 — Cut length to 1800 words?**
Current plan estimates 2000–2500. C5 notes the curation sweet spot is 4–7 minutes.
**Default: target 1800 words.** Achievable by tightening §1 (F-Score explanation → table + 100 words), merging §5b into §6, and tightening the Stock Y section.

**Q6 — Include TA corroboration sentence?**
One sentence in §4 noting technical momentum signals showed the same inversion on the same stock. C3 says this materially strengthens the N=4 evidence.
**Default: yes.** If the Cycle B work has a specific finding on this (the CLAUDE.md notes TA inversion as a cross-cycle finding), include one sentence. Does not make the post about TA.

**Q7 — Diagram 1 as table, not mermaid?**
C5 recommends replacing the 9-question mermaid flowchart with a native markdown table. This reduces the mermaid count to 3 (§3 inversion, §4 cycle loop, §5 Stock Y comparison) and removes one export step.
**Default: yes.** The information in Diagram 1 is better served by a table than a flowchart on Medium.

**Q8 — Disclosure placement: §2 (before data) vs §3 (after the surprise)?**
C5 recommends §2. C1 recommends before the table (implicitly §2 or end of §2). The plan originally suggested §1 or §3.
**Default: §2.** First paragraph, before any data. "Before the numbers:" framing resets the reader's posture before they start forming conclusions from the table.

---

## §8 — Revised plan: section-by-section

### Hook (target: 80–100 words, 5 sentences)
**Original intent**: Pull in the retail investor with the +355% surprise. Establish personal-testing framing.
**Revisions**: Drop sentence 1 (reader-flattery). Drop "The first few tests went fine." Start with the rule (F-Score in one sentence), then the contradiction in sentences 2 and 3. Replace the competence-claim close ("Here's why, and here's what I do instead") with a curiosity-gap close ("I think I know why — and I'd like to know if others have seen the same"). Final hook: 5 sentences, clean contradiction, genuine open posture.

### §1 — What the F-Score is (target: 100–150 words + 1 markdown table)
**Original intent**: Explain the 9 questions in plain English, 250 words.
**Revisions**: Cut the plain-English walkthrough by half. Replace Diagram 1 (mermaid flowchart) with a native markdown table (9 rows, 3 grouped sections). Move Blog #1 link here — this is where the project context belongs. Add one paragraph on the origin and scope: "The original paper was on US value stocks in the late 1990s. Most Indian investing books mention the checklist without this context." This primes the reader for §4 without spoiling it.

### §2 — How I tested it (target: 200–250 words, includes disclosure)
**Original intent**: Introduce the Metals Stock, explain the four test dates, note the hand-compute approach.
**Revisions**: First paragraph is the disclosure ("Before the numbers: this is from my own testing on one stock at four dates. Not peer-reviewed. I might be wrong. I'm sharing it because the pattern surprised me."). Then introduce "the Metals Stock" — largest description at first use. "(No shortcuts. Real numbers.)" stays verbatim. Optionally note: "I also ran a quick check on two other metal stocks to see if the pattern held — it did, though one showed a smaller effect."

### §3 — What the numbers showed (target: 350–400 words + 1 mermaid diagram)
**Original intent**: The evidence table showing F-Score vs forward returns at four dates.
**Revisions**: Three-row table (drop March 2024). Lead prose paragraph before the table: 3 sentences maximum, tells the reader what they're about to see. The inversion pattern paragraph after the table stays. Add data-source parenthetical for the +355% figure. Add the specific temporal gap sentence (stock price moved in October 2020; F-Score crossed 7 in March 2021) if data is available. Add one-sentence references to two additional metal stocks. Replace Gantt diagram with a directional flowchart showing the inversion (F-Score direction vs stock price direction, not duration).

### §4 — Why this happens (target: 250–300 words + 1 mermaid diagram)
**Original intent**: The coincident-indicator mechanism. The B/M / value-stock framing for why this happens.
**Revisions**: Major rewrite of the core reframe — the "Piotroski never said this" claim is replaced with the sharper B/M argument (see Rewrite 3 above). The "quietly extended" language is gone. Blog #2 link goes here if included. Optional TA corroboration sentence ("When I tested momentum signals on the same stock, the inversion was there too"). The cycle loop diagram (Diagram 3) stays — it is the most important explanatory diagram in the post.

### §5 — Contrast: the Consumer Goods Stock (target: 250 words + 1 mermaid diagram OR 1 prose paragraph)
**Original intent**: Show the F-Score working on a non-cyclical business. Real or illustrative Asian Paints data.
**Revisions**: Real data only (see Q4 above). If the Asian Paints hand-compute at comparable dates shows the F-Score tracking the stock direction, build the contrast table and the parallel diagram (Diagram 4). If the data is messy, cut to one prose paragraph and one sentence: "For stable businesses, the signal and the stock move in the same direction — and the data I have on a large consumer-goods stock supports that." No illustrative numbers.

### §5b + §6 — Merged: "How to tell and what I do instead" (target: 350–400 words)
**Original intent**: §5b = sector checklist (150 words). §6 = 5-year-average fix (250 words).
**Revisions**: Merge with C2's bridge sentence: "The difference between these two stocks comes down to one question: does the company's business have a cycle?" The sector checklist stays — it is the most immediately actionable part of the post for retail investors. The 5-year-average fix is presented as programmatic ("what I do in my system") with the manual proxy added ("what you can do on Screener.in without custom formulas"). Frame the 5-year version as a hypothesis, not a validated improvement.

### §7 — Closing (target: 100–150 words)
**Original intent**: What this taught about imported math. Navigation links to Blog #1 and Blog #2.
**Revisions**: End on the learning, not on the links. The emotional close is the intellectual arc: "I tested this checklist expecting it to work. It didn't — not here, not on this kind of stock. That gap is what I'm building toward closing." Then one natural link to Blog #1 (the project context). The genuine reader question ("if you've run F-Scores on cyclical stocks at troughs, I'm curious what you found") closes the post with an intellectual invitation, not a CTA.

---

**Total P0 items**: 8
**Total P1 items**: 7
**Total P2 items**: 5
**Total P3 items**: 3

**Estimated draft length after revisions**: 1750–1850 words + 3 mermaid diagrams + 1 markdown table.

---

✅ Synthesis complete. 8 P0 items + 7 P1 items + 5 P2 items surfaced. 8 open questions for Pranav. Primary structural concerns: sample-size (N=4 from one stock), §4 factual gap (cyclicals at troughs ARE in Piotroski's intended universe), March 2020 COVID confound, and Stock Y as broken positive control if illustrative numbers are used.
