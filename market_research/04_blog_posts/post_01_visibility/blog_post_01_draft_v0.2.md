# I'm building an AI to argue with me about my own stock portfolio.

*Draft v0.2 — incorporates feedback from all 5 reviewers (retail reader, editorial, skeptic, voice authenticity, Medium platform). ~1,800 words.*

**Subtitle (for Medium)**: *There's a real gap between what AI is good at today and what an investor actually needs in the moment of deciding. Here's how I'm trying to fill it.*

**Tags (for Medium)**: Investing · Artificial Intelligence · Personal Finance · Behavioral Finance · India

**Target publication submission**: DataDrivenInvestor

---

## The dance every investor knows

Every investor has done this dance. You sell something a little too early and watch it triple over the next two years. You hold something a little too long because admitting you were wrong feels worse than losing forty percent. The gap between what AI is good at today and what you actually need in the moment of deciding is enormous, and almost nobody talks about it.

For Indian retail investors like me, the gap is wider. The screeners are full. The YouTube videos are confident. The WhatsApp tips are loud. And when the moment of deciding shows up, you're alone with it.

I've been thinking about this for months. I'm building something to fix it. For myself first. And the first month has already taught me that even my own assumptions about how to do this were wrong in surprising ways.

---

## What today's AI is good at, and what it isn't

Let me be clear about this part, because I'm going to spend the rest of this post talking about what AI *isn't* doing. That would be unfair if I didn't first acknowledge what it does well.

Claude, ChatGPT, Gemini — they're genuinely useful thinking partners. They write well. They explain things clearly. They argue both sides of almost any question. For most knowledge work, they're the best tools we've ever had.

But ask one of them to look at your stock portfolio and tell you what to do, and you'll quickly hit a wall.

I tried this. I described my holdings to an AI and asked, point blank, "what should I do with these?" It told me things that were technically true and operationally useless. "Reliance has been flat this year." Yes, I have eyes. "Maybe consider trimming if you're worried about concentration." Worried about what? Why? Against what benchmark? Based on which rule that *I* set?

The deeper issue isn't that AI is bad at this. It's that the roadmaps from Anthropic, OpenAI, Google, at least the ones they've made public, are headed toward general-purpose chatbots. Not toward "personal portfolio advisor that knows your behavioural patterns and pushes back when you're about to break your own rules." Which is fine. That's where the market is.

It just means: the thing that would actually help me in the moment of deciding? I haven't seen anyone building it. So I am.

---

## What I'm actually trying to solve

The list of problems I want this to solve is shorter and more personal than what most fintech promises.

I sell winners too early. I tell myself I'm "booking profits." I'm getting nervous.

I hold losers too long. Selling feels like admitting I was wrong.

I buy a stock based on someone else's thesis, and three months later I can't remember what *my* reason was supposed to be.

I have a dozen mutual funds I added at various points. I'm not sure which ones are still doing what I bought them to do, which ones have quietly drifted, which ones I'm paying too much for.

My stop-loss rules exist on a sticky note. Sometimes I follow them. Sometimes I rationalise my way around them.

The tools I have, Kite and screeners and news sites, tell me *what's happening*. They don't tell me what to do about it inside the context of *my* rules.

What I want is simpler than what most apps promise. Something that knows my portfolio and the rules I've set for it. Something that reasons in plain English about each holding, not just shows me numbers. Something that pushes back when I'm drifting from my own discipline. Something that improves the *quality* of my decisions, not the *quantity* of my trades.

Beating the market isn't the goal. Not getting in my own way is.

---

## What I'm building, in plain English

I'm calling it **Nefarious**. The name is a joke about how a bot watching your portfolio sounds. The bot is the opposite of that. It's an investment-planning assistant, not a trading bot, and not an advisor I'd ever sell.

Here's what it does.

It looks at the Indian stocks and mutual funds I own. It looks at the rules I've defined for myself: when I'd sell, when I'd add, what I'd hold no matter what. Once a week it produces a short report. For each holding it tells me:

- Is the original reason I bought this still intact?
- Has anything material changed that I should know about?
- Am I anchoring on my entry price? Am I about to sell a winner because I'm anxious?
- For the mutual funds: are they still doing what I bought them to do? Has the manager left? Has the expense ratio crept up? Has the portfolio drifted into stocks I already hold directly?
- If I sold something today, what would the tax actually cost me?

That's the core loop. It's intentionally narrow.

```
        ME                             NEFARIOUS                         ME AGAIN
   ┌─────────────┐                ┌──────────────────┐               ┌─────────────┐
   │ My stocks   │  ────────────▶ │  Reads them      │ ────────────▶ │   I act     │
   │ My MFs      │                │  Reads my rules  │               │   (or don't)│
   │ My rules    │                │  Reasons         │               │             │
   └─────────────┘                │  Pushes back     │               └─────────────┘
                                  │  Writes a short  │
                                  │  weekly report   │
                                  └──────────────────┘

   It doesn't trade. It doesn't predict. It thinks alongside me,
   on a schedule, using rules I helped define.
```

What it explicitly does *not* do. No trading. No auto-execution. No order placement. Ever. It doesn't predict the market. If the bot ever tells me anything confident about next week, I throw it out. It doesn't replace my judgment. Every decision is still mine. The bot just makes sure I'm making that decision against my own pre-stated rules, with full context. It doesn't sell my data either. The whole thing runs locally on my machine.

The hard rules I've locked in are simple. Indian markets only: NSE stocks and Indian mutual funds. No US stocks, no crypto, no derivatives, no day-trading. Long-term focus only. Any number the bot uses must be one I can verify. And it's for me first. The whole project is built to figure out whether it actually helps me before I ever ask whether it might help anyone else.

---

## Why this problem statement makes sense

A few reasons, in plain English.

Most investing apps optimise for activity. They want you to log in, trade, react, repeat. That is how they earn. But the data on retail investors is pretty unambiguous: more activity usually means worse outcomes. So an app that gently *reduces* the number of unnecessary decisions you make is genuinely valuable. Almost nobody is building that.

The behavioural mistakes are the expensive ones. When you look at retail portfolios over a decade, the gap between average and good outcomes is almost never about who picked the best stocks. It is about who avoided the worst behavioural mistakes. Panic selling in March 2020. Holding through obvious deterioration. Getting hyped into a momentum trade right before it broke. A tool that catches *those* mistakes, even imperfectly, moves the needle more than picking a marginally better stock would.

I tested my own assumptions, and many of them were wrong. This is the most important reason, so let me show you what I actually did.

I started by writing down the "math" I thought a good investment assistant would use. Well-established formulas from academic finance, the kind referenced in every textbook. Then I tested them by hand on two real Indian companies, chosen because they sit at very different ends of the spectrum. Asian Paints, the quality-compounder archetype. And Tata Steel, the commodity cyclical. Four historical points each: March 2020, 2021, 2022, and 2024. I worked through the formulas the way a textbook says you should.

The textbook worked for the stable quality compounder under normal conditions. For Tata Steel, the standard "is this company financially healthy" signal was *perfectly inverted*. It looked strongest at the steel-cycle peak in March 2021, exactly when buying steel was most dangerous. It looked weakest at the trough in March 2020, exactly the moment that turned out to be the best entry of the decade. If I had built the bot trusting the textbook, it would have told me to enter Tata Steel at the worst possible moments and stay away at the best ones. None of that was learnable by reading about it. The only way to find it was to actually run the math on real Indian data, slowly, with the patience to work through every line.

The point isn't to win arguments with the AI. It is to be forced to think clearly about why I disagree. If I tell the bot "I think Reliance is still cheap," and it lays out three reasons that might not be true, the value isn't whether the bot is right. The value is whether *I* can clearly state why I still believe what I believe. That is a different kind of help than what any tool I've used offers.

---

## Where I am right now, honestly

A month in, I'm not at a finished product. I'm at "I have learned, through testing, that a lot of standard investing math does not transfer cleanly to Indian companies." That is a useful thing to know early.

The next phase is fixing the parts that failed and adding the parts I have not built yet. Reading price-and-volume signals, not just the underlying business. Mutual-fund-specific analysis. Portfolio-level position sizing. Exit rules that factor in Indian tax math. There is a long road.

I am using Claude, Anthropic's AI, as my thinking partner throughout. The work is unmistakably mine. The accelerant is the AI.

---

## What's next

If you're a retail investor in Indian markets and any of this resonated, I'd like to hear one specific thing: what's the one decision you keep making that you wish a tool would help you stop making? That kind of answer is exactly what is going to shape what gets built next.

---

*Word count: ~1,810.*
