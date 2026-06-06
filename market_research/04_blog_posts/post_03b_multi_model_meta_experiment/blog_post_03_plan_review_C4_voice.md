# Review C4 — Voice Authenticity (Human vs AI Tells)
**Post**: Blog #3 (replacement) — Plan v0.3
**Reviewer role**: Meta-detector for AI-written prose
**Date**: 2026-06-06

---

## §1 — Voice Verdict

**NEEDS-VOICE-WORK**

Not AI-dominant. Not a clean human pass. The plan contains pockets of genuine voice — particularly the voice constraints section, the "different slices, same well" analogy, and the blunt "design, not data" framing. These read like the same person who wrote Blogs #1 and #2.

But there are seven specific locations in this plan where the drafted prose slips into AI-generated cadence. The risk pattern is consistent: whenever the post engages with the critic's argument, the sentences become more balanced, more rhythmic, and more emotionally curated than anything in the baseline posts. That is the performed-humility tell showing up exactly where it was predicted to — in the critique-engagement sections.

The plan is recoverable. None of the tells are structural. They are phrase-level, and most can be fixed with one targeted edit each. But they need to be caught before the draft, not after, because once the AI writes 1,500 words in the "engaging with critique" tone, the whole post will have this quality and it will be nearly impossible to sand down.

**Count: 9 distinct AI-tell phrases or constructions flagged.**

---

## §2 — Per-Question Voice Analysis

### Q1 — The lede: "I sat with that" and the 5-sentence hook

The lede reads:

> "I've written two posts about this project so far — one about why I'm building a personal AI to argue with me about my own portfolio, and one about the technique I use to make the AI actually push back. Both posts got real feedback. A thoughtful comment on the second post in particular pointed out something I hadn't quite let myself see: when all five agents I describe run on the same model, they share the same blind spots. The technique might be doing less work than I'd claimed. This post is me sitting with that — and with the other questions both posts left open."

**Rhythm tell: yes, present and significant.**

Sentence lengths in order: long / short / long / short / long. This is an alternating-length pattern — it is one of the clearest mechanical tells of AI-generated prose, where the model varies sentence length to avoid monotony by mechanical alternation. No human writer plans sentence length this way consciously, but it is exactly what LLMs do by default.

**"hadn't quite let myself see"** — this is performed-insight language. The construction admits a blind spot but does it with notable literary grace. Compare to Blog #1 voice: "I tried this. I described my holdings to an AI and asked, point blank, 'what should I do with these?' It told me things that were technically true and useless." That is not graceful. That is blunt. "hadn't quite let myself see" is graceful in a way this author's voice baseline is not.

**"This post is me sitting with that"** — the "sitting with" construction is an AI-era emotional processing idiom. It signals reflection and openness, which are exactly the right emotions to signal in a post about engaging with critique. That is precisely why it is suspicious: it is too on-point emotionally. The real author of Blog #1 does not write emotional processing idioms. He writes "I sell winners too early. I tell myself I'm booking profits. I'm getting nervous." No "sitting with." Just flat description of behavior.

**Verdict**: The lede has two specific tells (alternating rhythm, "sitting with") and one more subtle one ("hadn't quite let myself see"). The emotions are right. The phrasing is too curated.

---

### Q2 — "This is not a small critique. It points at the structural assumption..."

The plan contains this framing in §3:

> "The honest reaction: this is not a small critique. It points at the structural assumption the entire technique rests on."

**AI escalation cadence: confirmed.**

"This is not X. It is Y" is a named pattern. It creates emphasis by negating a smaller frame before asserting a larger one. It sounds like someone thinking clearly about scale. But it is also how AI prose almost always escalates importance — the model has been trained on millions of pieces of writing that use this construction for dramatic clarity.

In Blog #1 and Blog #2, the author does not escalate with negation. When he wants to signal importance in Blog #1, he uses flat listing: "I sell winners too early. I hold losers too long." No "this is not X." When he wants to signal importance in Blog #2, he uses understatement: "That was the moment I realised I'd been using AI wrong." One sentence. No negation frame.

The specific two-sentence construction here ("not a small critique / points at the structural assumption") is also a parallel pair — two balanced sentences where the second lands as a conclusion. This is common AI prose architecture.

**Verdict**: Flag. Rewrite needed.

---

### Q3 — Three-bullet patterns in §4 and §5, and the repeated "Yes —" framing

§4 uses:

> "Yes — same model means same training data, same compression, same blind spots."
> "Yes — the synthesizer running on Claude reading critiques from Claude is closer to 'self-confirmation with extra steps'..."
> "Yes — when an LLM plays an authoritative role, it produces more confident outputs."

**Parallel construction tell: confirmed, and the repetition makes it worse.**

Three "Yes —" openers is a rhetorical list structure. It signals systematic agreement with the critic using a call-and-response format. It reads like an AI performing the act of "agreeing honestly and thoroughly." The voice baseline does not use repetition structures like this. Blog #2's §4 ("Why this works") uses plain declarative sentences with no repeated opener structure. Blog #1's problem list uses short sentences but they are confessional in content, not rhetorical in structure.

Additionally, the sub-bullets inside each "Yes" point use comma-series triads: "same training data, same compression, same blind spots." Three-item comma series are another AI prose tell — the model defaults to three because it feels complete. Human lists in this author's voice run on less tidy patterns.

The §5 three-bullet structure (cross-model / adversarial framing / human-as-arbiter) is less tell-heavy on its own, but when it mirrors the §4 structure precisely (three items, each with the same internal architecture of acknowledgment + complication + "my current take"), it creates an over-engineered symmetry that no human writer would build unconsciously across two adjacent sections.

**Verdict**: The "Yes —" openers in §4 are a direct rewrite target. The §5 three-bullet structure is acceptable if the internal architecture of each bullet varies.

---

### Q4 — "My current take" used three times in §5

The plan uses "My current take:" before each of the three §5 bullets:

> "My current take: **this is the right fix, but it has a cost.**"
> "My current take: **partial fix.**"
> "My current take: **this is non-negotiable.**"

**Writing tic: confirmed.**

The repetition is a structural tell. "My current take" is itself fine — it is hedged, it signals opinion rather than fact, it fits the voice constraints. But using the exact same phrase three times in three consecutive bullets turns a useful hedge into a rhetorical stamp. It signals: "I am now systematically concluding each point." No human writer stamps three consecutive paragraphs with the same opener without noticing. An AI does not notice because it is not keeping track of local repetition in that way — it is applying a template.

There is a secondary issue: "My current take" on its own is a mildly AI-ish phrase even in isolation. Blog #1 and Blog #2 never use it. The author's hedge language in the baselines looks like: "I'm still figuring out where this stops working," "I don't yet have a rule," "Something I've taken from doing this." These are integrated into sentences, not used as standalone headers.

**Verdict**: Vary the three openers. Two of the three need to be dissolved into the paragraph prose instead of standing as a stamp.

---

### Q5 — "I sat with that for a while" and "huge thanks to the commenter"

The lede uses "sitting with that" (analyzed in Q1 above). §8 adds:

> "One last thing: huge thanks to the commenter. This kind of pushback is exactly what makes building in public worth it."

**Emotionally-coded phrases — performed rather than authentic.**

On "sat with that / sitting with that": analyzed under Q1. The construction is too emotionally precise — it names the right internal experience in polished language.

On "huge thanks to the commenter": The plan itself flags this as a risk ("Self-flagellation tone: thanking the commenter once at the end is fine. Multiple times = performative humility"). But "huge thanks" is a warmer, more performative phrase than anything in the voice baseline. Blog #1 thanks no one. Blog #2 ends: "If you've tried multi-agent critique on your own work, I'd be curious what you found." Curious, not grateful. The closing register of this author is curiosity and invitation, not gratitude.

The phrase "huge thanks to the commenter" combined with the closing line (see Q6) creates an emotional crescendo at the end of the post that is well-structured and sincere-sounding. That is precisely the problem: it sounds designed to be sincere. Real sincerity in this author's voice is off-register, not on-register.

**Verdict**: "Huge thanks" needs to be rougher or cut. If the thanks stays, it needs to not be followed immediately by the abstract-noun closing line — the two together are too much performed emotion at once.

---

### Q6 — "This kind of pushback is exactly what makes building in public worth it"

This is the highest-risk line in the plan. It sits at §8 close and reads:

> "This kind of pushback is exactly what makes building in public worth it."

**AI-tell classification: Earnest summary closure with abstract-noun reflection. High confidence.**

This sentence has the structure of an AI-generated lesson-statement. It: (a) uses "this kind of X" to abstract the specific into a category, (b) uses "exactly" to signal precise alignment between cause and outcome, (c) invokes the concept of "building in public" as a named practice with recognized value, and (d) ends with the abstraction "worth it" which gestures at a balance of costs and benefits without specifying any of them.

Compare to Blog #2's closing: "If you've tried multi-agent critique on your own work, I'd be curious what you found. Especially the parts where it stopped helping." That ending is curious, specific, and slightly asymmetric — it asks about failure, not success. It does not conclude with a lesson.

Compare to Blog #1's closing: "The work is mine. The accelerant is the AI." That ending is compressed and slightly strange. "Accelerant" is an odd word choice that does not resolve cleanly. It does not summarize a lesson; it images a relationship. That is what this author sounds like when he is writing, not when he is generating.

**Verdict**: This line should not be in the draft. The suggested rough alternative is below in §3.

---

### Q7 — "I haven't actually run this yet" — disclosure vs rhetorical filler

The plan uses this cue:

- In the voice constraints: "I haven't actually run this yet" listed as a voice cue to scatter throughout
- In §6: "I haven't actually run this yet."
- In §7 item 3: "I haven't done it yet. I will, when I can."
- Implicitly in §8: "I haven't measured the gap."

**When does honest disclosure become rhetorical filler? Somewhere around the third repetition.**

The first use — in §6, where the experiment is designed but not run — is essential. It is the point of the section. The disclosure must be there.

The second use — in §7 for cross-model — is also fair, because it tracks a specific action item not yet taken.

The third use — in §8, "I haven't measured the gap" — starts to feel like a formulaic closing hedge. At this point the reader knows the author hasn't run the experiment. Repeating the disclosure at the close suggests the author is worried about being misread and is adding rhetorical insurance. Real confidence in the honest-limitation framing does not need insurance — it just states limitations where they are relevant.

The deeper problem is that "I haven't actually run this yet" scattered throughout is a voice cue that was designed (probably by the planning AI) to sound appropriately humble. But a cue that is designed to sound humble is not humility. It is the performed-humility tell in its generative form — the plan is building in the appearance of epistemic honesty rather than letting it emerge from what the author actually knows and doesn't.

**Verdict**: Keep the §6 disclosure (it is load-bearing). Keep the §7 item 3 disclosure (short, appropriate). Cut or vary the §8 version. Do not use "I haven't actually run this yet" as a recurring phrase — each instance should name the specific thing not yet done.

---

## §3 — Phrase-by-Phrase Rewrite Suggestions

### Lede: "This post is me sitting with that"

**Current**: "This post is me sitting with that — and with the other questions both posts left open."

**Problem**: "Sitting with that" is an AI emotional-processing idiom. The dash-and-extension construction ("— and with the other questions") is also a common AI prose move to add scope without starting a new sentence.

**Suggested rewrite**: "This post is me actually going through it."

Or more specifically: "This post is the response I owe."

**Why rougher**: The author's closing line in Blog #1 is "The work is mine. The accelerant is the AI." His closing in Blog #2 is "Especially the parts where it stopped helping." Both are slightly abrupt. His real register is compressed, not expansive.

---

### Lede: "hadn't quite let myself see"

**Current**: "...pointed out something I hadn't quite let myself see"

**Problem**: Literary. Too self-aware of the emotional mechanism of denial.

**Suggested rewrite**: "...pointed out something I'd walked past"

Or: "...caught something I'd glossed over"

**Why rougher**: Both alternatives are concrete and visual rather than psychological.

---

### §3: "This is not a small critique. It points at the structural assumption..."

**Current**: "The honest reaction: this is not a small critique. It points at the structural assumption the entire technique rests on."

**Problem**: Classic AI negation-escalation pair. Also "The honest reaction:" is a self-labeling preface — no human writes "The honest reaction:" because they do not preface their own reactions with their type.

**Suggested rewrite**: "The critique goes all the way down. The structural assumption the whole technique rests on is what gets challenged."

Or even blunter: "This isn't a small objection. It's the technique's foundation."

Wait — that second version still uses the "not X / it's Y" structure. Better:

"The critique lands on the one thing the whole technique assumes."

One sentence. No negation frame. No self-labeling preface.

---

### §4: Three "Yes —" openers

**Current**:
- "Yes — same model means same training data..."
- "Yes — the synthesizer running on Claude..."
- "Yes — when an LLM plays an authoritative role..."

**Problem**: Rhetorical list with repeated opener. Performs systematic agreement.

**Suggested rewrite approach**: Start the first bullet plainly ("The training-data point stands up."), drop the "Yes" framing entirely, and use varied openers for each point. The agreement is implicit in the content — it does not need to be announced three times.

Alternative for first bullet: "Same model means same training data. Same compression. I can prompt Claude to be a quant and separately prompt it to be a behavioural critic. They're still drawing from the same well."

This version is choppier, uses the "same well" analogy the plan already has, and does not front-load "Yes."

---

### §5: Three "My current take:" stamps

**Current**: "My current take: **this is the right fix, but it has a cost.**" (× 3 variations)

**Problem**: Same opener three times creates a template feel.

**Suggested variation**:
- First: "My current take: this is the right fix, but it has a cost." (keep this one — it is the most important)
- Second: dissolve into prose — "Adversarial framing is cheaper and worth using, but specifically at the synthesizer step. Not everywhere."
- Third: dissolve into prose — "I was already doing the human-arbiter step. The commenter is right that I'd been treating it as a footnote."

---

### §8: "huge thanks to the commenter"

**Current**: "One last thing: huge thanks to the commenter."

**Problem**: "Huge thanks" is warmer than anything in the voice baseline. "One last thing:" is a filler preface.

**Suggested rewrite**: "The commenter who pushed back on this: I'm glad they did."

Or simply omit the thanks and end with the invitation — the act of publicly designing the experiment and inviting others to run it is itself a form of acknowledgment.

---

### §8: "This kind of pushback is exactly what makes building in public worth it"

**Current**: "This kind of pushback is exactly what makes building in public worth it."

**Problem**: Lesson-statement. Abstract-noun closure. "Exactly" used to signal precision. "Building in public" invoked as a named practice. "Worth it" as a cost-benefit gesture. Every element of this sentence is an AI prose tell.

**Suggested rough alternative**: "I wouldn't have known what I'd missed without putting it out there. That's the only reason I keep posting."

Or even rougher: "Being wrong in public is faster than being wrong in private."

**Why this works better**: It is specific about the mechanism (public = faster error correction), uses "wrong" without softening it, and does not use any abstract nouns. It ends on an asymmetric note — it implies there is a cost to building in public ("being wrong") which the AI-generated version erases entirely.

---

### Lede: Alternating sentence-length rhythm

The five-sentence lede alternates long / short / long / short / long. The easiest fix is to break the alternation pattern at one point. If sentence 3 ("A thoughtful comment on the second post...") is long, sentence 4 should also be allowed to be medium-length rather than forced short. Let the rhythm be uneven in at least one place.

---

## §4 — What Rings Authentically Human

Not everything in this plan is a tell. Several elements are genuinely from the voice baseline:

**"Different slices, same well."** The plan uses this analogy in §4: "A Claude pretending to be a quant and a Claude pretending to be a behavioural critic are pulling from the same underlying source. Different slices, same well." This is the kind of compact analogy that appears in Blog #1 ("The accelerant is the AI.") and Blog #2 ("That's a real catch rate for an hour of work."). Compressed, slightly odd, not over-explained. Keep this exactly.

**"Design, not data."** The plan uses this framing for §6. It is blunt and accurate in the way the author's voice is blunt. Blog #2 uses a similar pattern: "That's the experiment." A short sentence that closes a description. This framing has the same energy.

**The operational honesty in §5 (cross-model cost paragraph).** "But it's expensive operationally — multiple API access, prompt engineering per model family, output-format normalization." This reads like someone who has actually thought about what it would cost to implement a thing, not someone performing awareness of tradeoffs. The specificity (three distinct cost types named) is authentic to the author's pattern of being specific about obstacles.

**"Confirm that they're confirming a real signal vs. agreeing because they share a blind spot."** The synthesizer adversarial prompt in §7 item 1. This is concrete, functional, and does not over-explain itself. It sounds like someone who has written the actual prompt in their head.

**The §8 open questions list.** "I don't know what model-family blind spots look like specifically — Claude is good at X but bad at Y; Gemini is different; I haven't mapped this." The "I haven't mapped this" ending is genuinely humble in the baseline register. It does not perform epistemic uncertainty — it just names a gap. Compare to "I haven't actually run this yet" which performs limitation. "I haven't mapped this" is quieter and more real.

**The "false alarm" moment in Blog #2.** This is worth noting as a baseline reference for the draft writer: "One review I want to mention because it didn't pan out: the behaviour person flagged that my system's alerts were 'too anxious'..." This kind of inclusion — voluntarily noting where the technique failed — is what makes Blog #2 feel honest. Blog #3 should have an equivalent moment: somewhere the author notes a case where his engagement with the critic did not fully satisfy him, or where he changed his mind partway through reasoning. The plan does not have this. Adding it would increase the authenticity signal.

---

## Summary of Flags

| # | Location | Tell type | Severity |
|---|---|---|---|
| 1 | Lede, sentence rhythm | Alternating-length pattern | Medium |
| 2 | Lede, "hadn't quite let myself see" | Performed-insight language | Medium |
| 3 | Lede, "sitting with that" | AI emotional-processing idiom | High |
| 4 | §3, "This is not a small critique. It points at..." | Negation-escalation pair | High |
| 5 | §3, "The honest reaction:" | Self-labeling preface | Medium |
| 6 | §4, three "Yes —" openers | Parallel-construction tell | High |
| 7 | §5, three "My current take:" stamps | Repeated rhetorical stamp | Medium |
| 8 | §8, "huge thanks to the commenter" | Warmer-than-baseline gratitude phrase | Low |
| 9 | §8, "This kind of pushback is exactly what makes building in public worth it" | Earnest lesson-statement closure | High (do not use) |

4 flagged High. 4 flagged Medium. 1 flagged Low. Total: 9 distinct tells across the plan's draft prose.

---

`✅ Voice review complete. 9 AI-tell phrases flagged.`
