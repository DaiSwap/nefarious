# Blog Post 01 — Plan (for review)

**Status**: Plan awaiting Pranav's review. Draft to follow after approval.
**Target**: Medium, first public-facing post for the project.
**Date**: 2026-05-31

---

## 1. Decisions already locked (from chat)

| | |
|---|---|
| **Audience (primary)** | Indian retail investors holding NSE stocks + Mutual Funds |
| **Length target** | ~1500–2000 words (7–9 min read) |
| **Project name** | Use "Nefarious" |
| **GitHub link** | No — keep the repo out of this post |
| **Voice** | First-person, human-written feel (you wrote it, not Claude) |
| **Tone** | Story / journey style. "I asked AI to help me with X, here's what happened" |
| **Jargon ban** | No `v0.X`, no "Cycle A", no "Phase 2", no Piotroski/Beneish/Altman, no any project-internal term |
| **Diagrams** | Simple visual aids only. No math. No flowcharts with 12 boxes. |

---

## 2. The core idea I want the reader to walk away with

> *"There's a real gap between what AI is good at today and what a retail investor actually needs when deciding what to do with their portfolio. I'm building something to fill that gap — and the first month of work has already shown me my own assumptions were wrong in surprising ways."*

That's the spine. Everything else supports this.

---

## 3. Title candidates (pick one)

| # | Title | Why it works |
|---|---|---|
| **T1** | **I'm building an AI to argue with me about my own stock portfolio. Here's why.** | Hook + first-person + curiosity gap. Suggests a personal AI, not a generic one. |
| T2 | The problem with every stock-advice tool I've tried — and what I'm building instead | Pain-point first. Slightly defensive ("I tried them, they didn't work"). |
| T3 | I asked AI to help me invest better. Here's what surprised me. | Soft hook. Less specific. |
| T4 | Why I stopped trusting stock screeners and built my own AI investment partner | Polarizing — "stopped trusting" may turn off some readers. |
| T5 | One month into building an AI investment planner. Here's what I've learned. | Honest. Maybe too plain. |

**My recommendation**: **T1** ("I'm building an AI to argue with me..."). It promises a personal angle and signals the bot isn't another "buy / sell" recommender — it's a thinking partner.

---

## 4. The outline (section by section)

Total length target: **1500–2000 words**. Word budgets are rough — adjust during drafting.

### §0 — Opening hook (~200 words)

Open with a specific, personal moment that any Indian retail investor recognizes. Not generic. Something like:

> "Last year I sold a stock for a small profit — and watched it triple in the next 18 months. The same year I held onto another stock that lost 40% of its value because I kept telling myself, *the fundamentals are fine, I'll just wait.* Neither decision felt wrong while I was making it. That's the problem I've been thinking about."

This sets up: bad decisions in real time, not bad decisions in hindsight. Every retail investor has lived this.

### §1 — What today's AI is actually good at (and what it isn't) (~300 words)

This is the "what today's LLMs are NOT solving" section, but framed positively first.

**What AI is good at** (one short paragraph): writing emails, answering questions, explaining concepts, even writing code. It's a genuinely useful thinking partner.

**What it isn't good at** (the meat of the section): when I asked AI to look at my portfolio, it cheerfully told me things that were *technically true but useless*. "Reliance has had a flat year." Yes, I can see the chart. "Maybe consider trimming if you're worried." Worried about what? Why?

The gap: today's AI can talk *about* investing. It cannot reason about *your portfolio* with discipline, context, or memory. It doesn't know your rules. It doesn't track whether you've changed your mind. It doesn't push back when you're about to sell a winner because you're anxious. And — based on what's been announced publicly — none of the big AI companies seem to be heading there. They're building general-purpose chatbots. Not personal financial advisors that watch you for behavioural drift.

Close this section with: *"That's not a flaw in AI. That's just what AI hasn't been built for yet."*

### §2 — What I'm actually trying to solve (~300 words)

This is the "what are we trying to solve here" section.

Frame it as a list of things the reader has probably felt:
- I sold too soon (and the stock kept going up).
- I held too long (because selling means admitting I was wrong).
- I bought a hyped stock and now I don't know if my thesis was real or borrowed.
- I have 14 mutual funds and I'm not sure which ones are still working for me.
- My stop-loss rules exist on a sticky note. Sometimes I follow them, sometimes I don't.
- The tools I have (Kite, Zerodha, screeners) tell me *what's happening*. They don't tell me *what to do about it* — and certainly not in the context of *my* rules.

The thing I want is simpler than what most "AI investing apps" promise:
- An assistant that knows my portfolio and the rules I set for it.
- One that reasons in plain English about each holding — not just numbers.
- One that pushes back when I'm about to break my own rules.
- One that improves the *quality of my decisions*, not the *quantity* of my trades.

I'm not trying to beat the market. I'm trying to stop being my own worst enemy.

### §3 — What the bot is (in plain English) (~400 words)

This is the "neat explanation of the problem statement" section.

Write in three short sub-blocks:

**What it does**: it looks at the Indian stocks and mutual funds I own, plus the rules I've defined for myself (when to sell, when to add, when to hold). Once a week it produces a short report — for each holding it tells me: is the original reason I bought this still intact? Has anything changed that I should be paying attention to? Are any of my behavioural patterns kicking in (am I anchoring on the entry price, am I about to sell a winner)?

**What it doesn't do**: it doesn't trade for me. It doesn't tell me "buy 30 shares of HDFC Bank." It doesn't pretend to know things it can't know (like whether the market will go up next week). And it doesn't replace me — the final decision is always mine.

**Rules I've locked in**:
- Indian markets only. NSE stocks + Indian Mutual Funds. No US stocks, no crypto, no derivatives, no day-trading.
- Long-term focus. The point is to make better long-term decisions, not catch short-term moves.
- The AI's job is to *think out loud*, not to predict. Any number the bot uses must be something I can verify.
- It works for me. I'm not selling this. Not yet. The first version is built for one user — me — and the project's whole goal is to figure out if it actually helps before showing it to anyone else.

This is where I include **Diagram 1** (see §6 below).

### §4 — Why this problem statement actually makes sense (~300 words)

This is the "why the problem statement makes sense" section.

Argument structure:

**Most investing apps optimize for activity.** They want you to log in, trade, react. That's how they make money. But for a retail investor, *more activity usually means worse outcomes*. So an app that *reduces* unnecessary decisions is genuinely valuable — and almost no one is building that.

**The behavioural mistakes are the expensive ones, not the analytical ones.** Looking at a P&L, you might assume the people who beat the market are the people who picked the best stocks. Mostly, they're the people who avoided the worst mistakes. They didn't sell in March 2020. They didn't load up on the hyped IT stocks in early 2022. A tool that catches those mistakes in real time — even if it's only right 60% of the time — moves the needle more than picking a slightly better stock.

**One-person testing is how I avoid pretending I know things I don't.** I tried to write the rules the bot would use. Then I tested those rules on real Indian companies, going back five years. Things I was *certain* would work — well-established formulas from academic finance — failed in obvious, specific ways on Indian data. Things I assumed were minor turned out to matter a lot. That's only learnable by actually doing the work. Not by reading about it.

**The point isn't to win arguments with the AI. It's to be forced to think clearly about why I disagree.** That's a different kind of help than what most tools offer.

### §5 — Where I am right now, honestly (~200 words)

A short, honest status update. No jargon.

> One month in, I'm not at a finished product. I'm at "I've learned, through testing, that a lot of standard investing math doesn't transfer cleanly to Indian companies." That's a useful thing to know early. The next phase is fixing the parts that failed and adding the parts I haven't yet built — like understanding price-and-volume signals, not just the underlying business.
>
> I'm using Claude (Anthropic's AI) as my thinking partner throughout. The work isn't "AI built this for me." It's "I'm building this *with* AI as the implementer and challenger, while I drive the actual strategy." That's an important distinction. The AI doesn't know more than I do about what I want to build. But it can stress-test me much faster than I could stress-test myself.

### §6 — Closing / what's next (~150 words)

End simply. Acknowledge that this is the start, not the end.

> If you're a retail investor and any of this resonated, I'd genuinely like to hear: what's the one decision you keep making that you wish a tool would help you stop making? That's the kind of feedback that's going to shape what gets built next.
>
> I'll be writing more as this project progresses. The next post will likely be about *why my own assumptions about investing math were so wrong* — and what real Indian companies taught me when I actually tested those assumptions. If that sounds interesting, follow along.

---

## 5. Voice samples (so we agree on tone)

A few example paragraphs in the voice I'd write — Pranav reviews these before I draft.

**Voice sample A** (opening): *"Last year I sold a stock for a small profit and watched it triple over the next 18 months. The same year I held onto another stock that lost 40 percent of its value because I kept telling myself, the fundamentals are fine, I'll just wait. Neither decision felt wrong while I was making it. That's the problem I've been thinking about."*

**Voice sample B** (educational, no jargon): *"Today's AI can write you an essay about Reliance. It cannot watch your portfolio and notice that you're about to break your own rule — the one where you said you wouldn't sell on a 12 percent dip. That second thing is what I actually need, and it doesn't exist yet."*

**Voice sample C** (honest about limits): *"This isn't a finished product. It's me, an Indian retail investor, building a thinking partner for myself, in the open. Whether it ends up being something useful to others depends entirely on whether it ends up being useful to me first. That's not a marketing line. That's literally where I am."*

---

## 6. Diagrams (simple, 2 max)

Diagrams render on Medium as embedded images. I'll provide simple ASCII or text-based layouts you can either screenshot from the file or have someone redraw in a cleaner tool (Excalidraw / Figma / Canva).

### Diagram 1 — What the bot is, in one picture

```
        YOU                              THE BOT                       YOU AGAIN
   ┌─────────────┐                   ┌──────────────┐               ┌─────────────┐
   │ Your stocks │  ──────────────▶  │  Reads them  │  ──────────▶  │   Acts (or  │
   │ Your MFs    │                   │  Reads your  │               │   doesn't)  │
   │ Your rules  │                   │  rules       │               │             │
   └─────────────┘                   │  Reasons     │               └─────────────┘
                                     │  Pushes back │
                                     │  Writes you  │
                                     │  a report    │
                                     └──────────────┘

   The bot doesn't trade. It doesn't predict. It thinks alongside you,
   on a schedule, using rules you helped define.
```

Placement: end of §3.

### Diagram 2 — What it specifically does NOT do

```
   ❌ DOES NOT trade for you            ✅ DOES read your portfolio
   ❌ DOES NOT predict the market       ✅ DOES check it against your rules
   ❌ DOES NOT replace your judgment    ✅ DOES flag when you're drifting
   ❌ DOES NOT touch your money         ✅ DOES explain, in plain English
   ❌ DOES NOT sell your data           ✅ DOES live entirely on your machine
```

Placement: end of §3 or §4.

(Two diagrams feels right. More than that and the post gets visually cluttered.)

---

## 7. Things I'm intentionally NOT covering in this post

| Topic | Why I'm leaving it out |
|---|---|
| Specific stocks tested (Asian Paints, Tata Steel) | These are debugging subjects, not the message |
| The actual math (Piotroski, Beneish, Altman Z″) | Jargon. Lose 80% of readers in one sentence. |
| The 6 structural weaknesses found | Too deep for a first post. Save for a follow-up. |
| Multi-agent critique / cycle structure | Project-internal. Reader doesn't care how the sausage is made. |
| Implementation tech / Python / data sources | Wrong audience. Save for a technical follow-up. |
| Claude as a brand | Mentioned once as "Anthropic's AI" — not the focus |
| GitHub repo link | You've chosen not to share it yet |

---

## 8. Closing / CTA strategy

The CTA at the end should:
- Invite a specific, easy response ("what's the one decision you keep making...")
- Not ask for follow / clap / share directly (those feel cheap on Medium)
- Promise a next post topic that's actually interesting (the next post is "what real Indian companies taught me when I tested my own investing assumptions")

This sets up a series. Blog #2 can go deeper. Blog #1 establishes the why.

---

## 9. Open decisions for you to make

Before I write the draft, can you confirm or correct:

1. **Pick a title from §3** — T1 is my recommendation, but happy to swap if T2 (pain-point first) feels more like you.
2. **Voice samples in §5** — do they sound like *you* would write? If not, give me a 2–3 sentence example of a different tone and I'll match it.
3. **The opening anecdote** — the "sold a stock that tripled / held one that fell 40%" line in §0. Is that *true* for you (real experience), *roughly true* (illustrative but not literal), or do you want to use a different specific moment from your own investing history?
4. **Diagrams** — are the two in §6 simple enough? Or do you want fewer? Or hand-drawn instead?
5. **Closing CTA** — happy with the "what's the one decision you keep making..." prompt, or want a different one?
6. **Personal disclosure level** — how much of "this is for me first, others maybe later" do you want to lean into? Too much sounds like indie-hacker; too little sounds like a startup launch.

---

## 10. After plan is approved

Once you confirm the above, I'll write the draft in one go to `market_research/blog_post_01_draft.md`. Then you read, redline, I revise. Expect 1–2 review rounds before it's ready to paste into Medium.

**Estimated time to first draft after plan approval**: 30–45 min of focused writing.

---

**End of plan. Awaiting Pranav's review.**
