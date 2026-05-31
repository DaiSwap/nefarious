# I'm building an AI to argue with me about my own stock portfolio. Here's why.

*Draft v0.1 — for review. ~1,800 words.*

---

## The dance every retail investor knows

If you hold Indian stocks, you've probably done this dance.

You sell something a little too early and watch it triple over the next two years. You hold something a little too long because admitting you were wrong feels worse than losing 40 percent of the money you put in. The screeners are full. The YouTube videos are confident. The WhatsApp tips are loud. And yet, when you actually have to make the call, you're alone with it.

I've been thinking about this gap for months. Not the gap between professional investors and retail ones — that one's well understood. The gap between what AI is genuinely good at today, and what a retail investor actually needs *in the moment of deciding*. That gap is enormous, and almost nobody is building for it.

So I started building it. For myself, first. And the first month has already taught me that even my own assumptions about how to do this were wrong in surprising ways.

## What today's AI is good at — and what it isn't

I want to be clear about this part, because I'm going to spend the rest of this post talking about what AI *isn't* doing, which is unfair if I don't first acknowledge what it does well.

Today's AI — Claude, ChatGPT, Gemini — is a genuinely useful thinking partner. It writes well. It explains things clearly. It can argue both sides of almost any question. For most knowledge work, it's the best tool we've ever had.

But ask it to look at your stock portfolio and tell you what to do, and you'll quickly hit a wall.

I tried this. I described my holdings to an AI and asked, point blank, "what should I do with these?" It told me things that were technically true and operationally useless. "Reliance has been flat this year." Yes, I have eyes. "Maybe consider trimming if you're worried about concentration." Worried about what? Why? Against what benchmark? Based on which rule that *I* set?

The deeper issue isn't that AI is bad at this. It's that AI is being built for general conversation, not for thinking about *your* portfolio according to *your* rules across weeks and months. None of the public roadmaps from the big AI labs are heading toward "personal portfolio advisor that knows your behavioural patterns and pushes back when you're about to break your own rules." They're building general-purpose chatbots. Which is fine — that's where the broad market is.

It just means: that other thing? Nobody is building it. So I am.

## What I'm actually trying to solve

The list of problems I want this to solve is shorter and more personal than what most "AI investing apps" promise:

- I sell winners too early. I tell myself I'm "booking profits." I'm actually getting nervous.
- I hold losers too long. Selling feels like admitting I was wrong.
- I buy a stock based on someone else's thesis, and three months later I can't remember what *my* reason was supposed to be.
- I have a dozen mutual funds I added at various points. I'm not sure which ones are still doing what I bought them to do.
- I have stop-loss rules I wrote down somewhere. Sometimes I follow them. Sometimes I rationalise my way around them.
- The tools I currently use — Kite, screeners, news sites — tell me *what's happening*. They don't tell me what to do about it inside the context of *my* rules.

What I want is simpler than what most fintech promises:

- Something that knows my portfolio and the rules I've set for it.
- Something that reasons in plain English about each holding, not just shows me numbers.
- Something that pushes back when I'm drifting from my own discipline.
- Something that improves the *quality* of my decisions, not the *quantity* of my trades.

I'm not trying to beat the market. I'm trying to stop being my own worst enemy.

## What I'm building, in plain English

I'm calling it **Nefarious**. It's an investment-planning assistant — not a trading bot, not an advisor I'd ever sell. Here's what it actually does:

It looks at the Indian stocks and mutual funds I own. It looks at the rules I've defined for myself — when I'd sell, when I'd add, what I'd hold no matter what. Once a week it produces a short report. For each holding, it tells me:

- Is the original reason I bought this still intact?
- Has anything material changed that I should know about?
- Are any of my behavioural patterns showing up — am I anchoring on my entry price, am I about to sell a winner because I'm anxious?
- If I sold this today, what would the tax implications actually be?

That's the core loop. It's intentionally narrow.

```
        YOU                            NEFARIOUS                         YOU AGAIN
   ┌─────────────┐                ┌──────────────────┐               ┌─────────────┐
   │ Your stocks │  ────────────▶ │  Reads them      │ ────────────▶ │   You act   │
   │ Your MFs    │                │  Reads your rules│               │   (or don't)│
   │ Your rules  │                │  Reasons         │               │             │
   └─────────────┘                │  Pushes back     │               └─────────────┘
                                  │  Writes you a    │
                                  │  short report    │
                                  └──────────────────┘

   The bot doesn't trade. It doesn't predict. It thinks alongside you,
   on a schedule, using rules you helped define.
```

What it explicitly does *not* do:

- It doesn't trade. No auto-execution. No order placement. Ever.
- It doesn't predict the market. If the bot tells you anything confident about next week, throw it out.
- It doesn't replace my judgment. Every decision is still mine. The bot's job is to make sure I'm making that decision with the full picture, against my own pre-stated rules.
- It doesn't sell my data. The whole thing runs locally on my machine.

The hard rules I've locked in are simple:

- Indian markets only. NSE stocks, Indian Mutual Funds. No US stocks, no crypto, no derivatives, no day-trading.
- Long-term focus. The point is to make better long-term decisions, not to catch short-term moves.
- Any number the bot uses must be one I can verify. The AI's job is to think out loud — not to predict.
- It's for me, first. The whole project is built to figure out whether it actually helps me before I ever ask whether it might help anyone else.

## Why this problem statement actually makes sense

Four reasons, in plain English.

**One: most investing apps optimise for activity.** They want you to log in, trade, react, repeat. That's how they earn. But the data is clear that for retail investors, more activity usually means worse outcomes. Almost nobody is building an app that gently *reduces* the number of unnecessary decisions you make. That gap is enormous and uncrowded.

**Two: behavioural mistakes are the expensive ones.** When you look at retail portfolios over a decade, the gap between average and good outcomes is almost never about who picked the best stocks. It's about who avoided the worst behavioural mistakes — panic selling in March 2020, holding through obvious deterioration, getting hyped into a momentum trade right before it broke. A tool that catches *those* mistakes in real time, even if it's only right 60 percent of the time, moves the needle more than picking a marginally better stock would.

**Three: I tested my own assumptions, and many of them were wrong.** This is the most important reason. I started by writing down the "math" I thought a good investment assistant would use — well-established formulas from academic finance, the kind you'll see referenced in every textbook. Then I tested those formulas on real Indian companies, going back five years, by hand. Things I was *certain* would work failed in specific, identifiable ways on Indian data. Things I'd assumed were minor turned out to matter a lot. None of that was learnable by reading about it. The only way to find it was to actually do the work — slowly, with Claude helping me push through the parts I'd otherwise have skimmed past.

**Four: the point isn't to win arguments with the AI. It's to be forced to think clearly about why I disagree.** If I tell the bot "I think Reliance is still cheap," and it lays out three reasons that might not be true, the value isn't whether the bot is right. The value is whether *I* can clearly state why I still believe what I believe. That's a different kind of help than what any tool I've used offers.

## Where I am right now, honestly

One month in, I'm not at a finished product. I'm at "I've learned, through testing, that a lot of standard investing math doesn't transfer cleanly to Indian companies." That's a useful thing to know early.

The next phase is fixing the parts that failed and adding the parts I haven't built yet — like reading price-and-volume signals, not just the underlying business. After that comes mutual fund analysis, then portfolio-level position sizing, then exit rules that factor in Indian tax math.

```
   ❌ DOES NOT trade for you            ✅ DOES read your portfolio
   ❌ DOES NOT predict the market       ✅ DOES check it against your rules
   ❌ DOES NOT replace your judgment    ✅ DOES flag when you're drifting
   ❌ DOES NOT touch your money         ✅ DOES explain, in plain English
   ❌ DOES NOT sell your data           ✅ DOES live entirely on your machine
```

I'm using Claude — Anthropic's AI — as my thinking partner throughout. But this isn't "AI built this for me." This is "I'm building it with AI as the implementer and challenger, while I drive the actual strategy." That distinction matters. The AI doesn't know more than I do about what I want to build. But it can stress-test me much faster than I could stress-test myself.

When I get something wrong — and I have, multiple times — Claude is honest about it. When I'm about to over-engineer, the pushback comes immediately. When I'm thinking lazily, the questions get sharper. The work is unmistakably mine. The accelerant is the AI.

## What's next

If you're a retail investor in Indian markets and any of this resonated, I'd genuinely like to hear: *what's the one decision you keep making that you wish a tool would help you stop making?* That kind of answer is exactly what's going to shape what gets built next.

I'll be writing more as this project progresses. The next post will likely be about what real Indian companies actually taught me when I stress-tested my investing assumptions against five years of historical data — and why the textbooks were wrong about half the things I tried. If that sounds interesting, follow along.

---

*Word count: ~1,800.*
