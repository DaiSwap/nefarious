# 06 — Critique: Skeptical Retail Investor Lens

**Written from the perspective of**: A 38-year-old salaried IT professional in Bangalore.
₹15L portfolio, 25 stocks, 8 years investing, Zerodha + Tickertape + Screener + Smallcase user.
Has been burned by tipster Telegram groups. Follows Pranjal Kamra and Akshat Shrivastava on YouTube.

---

## About me (the user persona)

I work at a mid-size product company in Whitefield. SIP in index funds for the past 4 years (Akshat's influence), and direct equity in 25 stocks — mostly Nifty 500, some mid-caps I've been holding since 2019. My portfolio has returned roughly 14–16% CAGR on average, but honestly two or three stocks are doing all the heavy lifting. I have no idea what to do with the rest.

I spent about ₹12,000 on a "stock market masterclass" in 2021 that was basically useless. I've been on three Telegram tip groups — exited all three after losing money on at least one tip each. These days I'm cautious. If something smells like a tip service with a UI, I'm out.

---

## TL;DR — would I use this?

- **Yes, I'd try it once** — if it could actually read my Zerodha portfolio via Kite and tell me something I don't already know, without me having to enter 25 stocks manually.
- **No, I wouldn't pay immediately** — I need to see at least 2–3 months of recommendations and compare them to what actually happened before I trust it with my money decisions.
- **The "AI-powered" label actively hurts credibility with me** — I've seen too many "AI stock screeners" that are just Screener.in with a chatbot wrapper. Show me the reasoning, not the label.
- **The behavioral bias angle is genuinely interesting** — I suspect I'm holding at least 4–5 stocks out of stubbornness, not conviction. If the bot could tell me that without judgment, I'd listen.
- **If it passes my 3-month test, I'd pay ₹300–400/mo** — not ₹500 without an annual discount. There is a real ceiling here.

---

## Reaction to each pain point in 01_research.md

| Pain Point | My Reaction | Honest Take |
|------------|-------------|-------------|
| **Disposition effect** (hold losers, sell winners too early) | YES — this is real | I have three stocks down 40%+ that I haven't sold because "I'll wait for it to recover." Two of them I've been waiting on for three years. This is the most embarrassing truth about my portfolio. |
| **Finfluencer dependency / tip-chasing** | SORT OF — mostly past tense | I used to. Now I watch Pranjal for conceptual understanding, not tips. But I still feel FOMO when a WhatsApp group says something is "moving." I won't admit this to many people. |
| **Overconfidence + overtrading** | NO — exaggerated for me | I don't overtrade. I'm the opposite problem — I under-act. I know something's wrong with a position and I sit on it for months. The overtrading narrative is more for F&O people. |
| **Panic selling in bear markets** | YES — partially | I sold Tata Motors in the COVID crash. Bought back six months later at a higher price. Classic. But I've learned from that — I haven't panic-sold since 2022. |
| **Comprehension gap (data exists, can't act)** | YES — this is the real one | I have Screener.in premium. I have Tickertape. I look at the data and I still don't know what to *do*. "P/E of 28, sector median 32, promoter holding 61%, ROE 18%" — so what? Is this a buy, hold, or trim? The data doesn't tell me. |
| **Concentration risk** | YES — big yes | My top 5 holdings are 58% of my portfolio. I know this is too much. I've known for 18 months. I just don't know what to do about it. |
| **No systematic personal investment process** | YES — very real | My process is: watch a Pranjal video, check Screener.in, read one Tickertape report, then feel vaguely confident and either do nothing or place an order I'm not sure about. That's not a process. |
| **FOMO-driven leverage / F&O overuse** | NO — not my problem | I don't do F&O. I learned that lesson early from colleagues who lost significant money. But I know many people who do. |

---

## My honest take on existing tools

**Screener.in** — I use the free version mostly. It's genuinely good for fundamentals. But it's a database, not an advisor. I can tell you HDFC Bank's P/E history for 10 years; I can't tell you whether I should hold it. No one at Screener.in is judging my specific portfolio.

**Tickertape** — Better UI than Screener. The Mutual Fund section is fantastic. Stock analysis is decent. But again — it tells me about stocks, not about what I personally should do with mine. The "Portfolio Health" feature is superficial — it just tells me I'm overweight in Financial Services. I know that.

**Smallcase** — I have two Smallcases — Windmill Capital's momentum one and one for IT stocks. They've done okay. But I'm a passive passenger. I don't really understand why specific stocks are in or out. When the IT Smallcase dropped 22%, I had no idea whether to add more or exit. The opacity is frustrating.

**Zerodha Console** — Excellent for tax P&L and historical performance. But it's purely backward-looking. "Your Tata Steel position is up 67% since purchase" — great, but should I book profit now or hold? No answer.

**Zerodha Kite** — Good execution platform. I don't use the charts much because I never learned TA properly.

**Varsity** — I respect this. Actually learned how options work here, even though I don't use them. But reading Varsity and knowing what to do with my actual portfolio are two completely different things. Knowledge gap solved; action gap not.

**StockEdge / Trendlyne** — Tried both. Paid for StockEdge for three months. Cancelled. The data is comprehensive, maybe too comprehensive. 40 filters, 15 screeners — I didn't know which one to trust. Felt like I was doing research but had no better decisions at the end.

**INDmoney / Groww** — I use INDmoney to track my net worth. It's fine for MFs. The equity advice is generic garbage — "your portfolio is moderately aggressive, consider adding debt" — the same message it would give any 35-year-old. Not personalized at all.

**MoneyControl** — It's a news site. Good for checking results. Not an investment tool.

---

## What the bot must do to win me (3 tiers)

### Tier 1 — Try once
Show me one thing I did not already know about my own portfolio. Not generic — *mine*.

Specifically: connect to my Zerodha account via Kite API (or let me upload a CSV), load my 25 holdings, and within 5 minutes give me a ranked list like: "Your top 3 positions that have the weakest current case for holding are X, Y, Z. Here's why."

If it can name the actual stocks and give me a non-generic reason — "NMDC: RSI has been below 40 for 6 weeks, ROE has declined from 24% to 17% over 3 years, and you've been holding a 32% unrealized loss for 18 months. This looks like anchoring bias, not conviction" — I will use it again.

If it says "Your portfolio is diversified across 8 sectors. Consider adding defensive stocks" — I will uninstall it.

### Tier 2 — Use weekly
Give me a Monday morning brief. My 25 holdings, ranked by urgency of action. Something like:

- "Review now (3): Infosys broke below 200 DMA on Friday; consider trimming. SAIL: earnings next week, position sizing is 8% — high concentration into a news event. ITC: technical pattern turning positive, if you have been waiting to add, this week might be a reasonable entry."
- "Watch (5): [brief notes]"
- "Hold — no change (17): [names only]"

That's it. 10 minutes on Monday morning. If it does that consistently and is right more often than wrong over 2 months, I start to trust it.

The key word is *consistently*. I don't need it to be right every time. I need it to show up every week with a clear output format so I know what I'm looking at.

### Tier 3 — Pay ₹500/mo
For ₹500/mo, I need three things in addition to Tier 2:

1. **A track record it shows me.** Not backtested — actual recommendations it made, and what happened. If it recommended trimming SAIL three weeks ago and SAIL is down 12% since then, show me that. I want the bot to have skin in the game in the form of transparency. If it hides past recommendations, I'm done.

2. **A "why I was wrong" explanation.** Once a month, if a recommendation was wrong, I want the bot to say "I said hold Reliance Industries; it dropped 9%. Here's what I missed: [reason]." That honesty is more valuable to me than being right. It tells me the bot isn't just rationalizing after the fact.

3. **Tax awareness.** I have significant LTCG positions I haven't thought about properly. If the bot tells me "Selling HDFC Bank now triggers ₹68,000 in LTCG tax. Waiting 3 months after the next results gets you past a favourable holding period. Here are the tax implications of your 4 highest-gain positions" — that is genuinely valuable and I cannot get it anywhere today without paying a CA.

---

## What would make me delete the app immediately

1. **Any recommendation followed by a "Powered by AI" badge but no visible reasoning.** "Based on our AI analysis, we recommend BUY on IRCTC." Why? What signals? If I can't see the logic, it's a tip service. Tip services have cost me money. Deleted.

2. **A "Pro" paywall on the reasoning.** If the free version shows me a signal but locks the explanation behind ₹499/mo, that tells me the product's business model depends on my ignorance. I know this trick — Stock Edge does this too. Deleted.

3. **Return promises or star ratings with no methodology.** "9.2/10 stock quality score" with no explanation of how the score is computed. "Expected return: 18–24%" with no confidence interval or methodology. These are tipster vibes dressed in a UI. Deleted instantly.

Bonus fourth: if there's a referral bonus or affiliate commission built in to the recommendation engine — even if undisclosed — I'll suspect it within weeks. "Recommends only SEBI-registered stocks" is not reassuring if the ranking is opaque.

---

## Trust competitors (who I trust today)

**Pranjal Kamra (Finology / YouTube)** — I trust him because he explains concepts without selling me anything. He tells me to avoid F&O, explains why businesses work, and never guarantees returns. He's consistent. He admits mistakes. He's been saying the same things for 5 years. The consistency is the trust signal.

**Akshat Shrivastava (YouTube)** — I trust him for frameworks — index funds, real estate vs equity tradeoffs, FIRE thinking. He's rich enough that he doesn't need to sell me something, and that shows in his content. He monetizes coaching/courses, but the free content is not a funnel.

**My CA** — For tax. Not for investment decisions, but for what the tax implications of my decisions are. This is actually a big gap — nobody I trust connects the investment decision to the tax outcome.

**Zerodha's brand** — I trust them not to be a scam because they've spent 15 years building trust through Varsity, Console, and transparent pricing. If they endorsed a tool or built it themselves, I'd give it more initial trust than a random startup.

How does the bot compete? It can't compete on brand (it has none). It can't compete on longevity. It competes by being **right about my specific portfolio** in ways that the YouTube people can't be, because the YouTube people don't know what I hold. The bot's only edge is personalization + specificity. If it loses that — if it gives me generic advice — it loses to Pranjal Kamra's free videos every time.

---

## Real problems the research did NOT mention

1. **The "what do I do with this ₹20,000 salary credit today" problem.** Every month I get my salary, I have ₹15,000–25,000 to deploy. The problem isn't what to hold — it's what to *buy next* when I have fresh capital. "I have ₹20K, my portfolio is as above, current market is X — what should I add and in what proportion?" This is a concrete weekly decision that no tool helps me with systematically.

2. **The exit problem is completely unaddressed.** When do I actually sell? Everyone tells me when to buy. Nobody tells me a clean, rule-based when to sell. My portfolio has three stocks with 60–80% gains that I've been "letting run" for 2 years. I have no exit rule. I'm going to give back those gains at some point and not know why I didn't sell. The bot needs a "when to exit" module more than a "when to enter" one.

3. **LTCG management at the retail level.** I don't think about taxes until March. By then it's too late to do proper tax-loss harvesting or LTCG optimization. A bot that reminds me in October "you have ₹1.4L in short-term gains that will be taxed at 20% if you realize them before 12 months; consider waiting X weeks" would save me meaningful money every year. The research mentions tax-awareness (D5) in passing but doesn't treat it as a real pain point. For me, it's a ₹30,000–60,000/year problem.

4. **The "I don't know my actual strategy" problem.** I realize I don't have a coherent investing philosophy. I have a mix of "Pranjal's quality investing" logic for some stocks, "Akshat's macro thesis" for others, and "someone told me this is good" for at least 5 positions. The research documents lack of systematic process but doesn't acknowledge that many investors like me can't even articulate their own strategy — let alone have it enforced. The bot assuming I have a coherent strategy to encode (Framing Y) is too optimistic. I need help discovering what my strategy actually is first.

5. **Illiquid mid/small-cap positions with no volume.** I have two stocks with average daily volumes so low that a 2% position for me is effectively illiquid. If I wanted to sell, I'd move the price. No screener or portfolio tool flags this. The research discusses NIFTY 500 as the universe, but many retail portfolios have names outside that, and the liquidity trap is real.

---

## Implications for the problem statement

The current problem statement is written for someone who already has a coherent investment methodology and wants to automate its application. That's not most retail investors — that's maybe the top 15% who have been investing 10+ years and have done real work.

For me:

- **Framing Z (Portfolio doctor) is the right starting point**, not Framing Y (Strategy composer). I want a diagnosis before I want a prescription. I cannot compose strategies I can't yet articulate.
- **The exit problem should be in v1**, not v2. This is more urgent than entry for many people who've been holding for 2–3 years.
- **Tax-awareness (D5) is not a "nice to have"** — it's a real differentiator that no existing tool does well. Build it early.
- **"Methodology agnostic" onboarding is needed** — let me describe my investing in plain language and let the bot tell me what methodology I'm *actually* using. Then refine from there. Don't make me start with "configure your RSI threshold."
- **Trust-building features need to be designed first**, not retrofitted. The product needs a "bot's past calls" section on day one. If I can't audit what the bot recommended 4 weeks ago, I won't trust what it recommends today.
- **The SEBI advisory-only constraint is fine with me** — I don't want the bot to auto-execute. I want to retain control. I'm worried about a bot doing something irreversible with my money. Advisory-only is actually a feature, not a limitation, for someone like me.

---

## Questions the user must answer

1. What is the minimum viable integration path? If I have to manually enter 25 stocks by hand, I might do it once, not weekly. Is Kite API integration in v1 or v2?

2. What does the bot do when TA and FA disagree on the same stock? Does it tell me there's a conflict? Does it pick one? Does it ask me which lens I want to use? This is not a technical question — it's the product's core design question, and I don't see it answered anywhere.

3. How does the bot handle stocks where it genuinely doesn't have enough data? Some of my mid-caps have limited coverage. Does it say "I don't know"? Or does it hallucinate a recommendation? I'd rather it say nothing than say something wrong with confidence.

4. How will you handle the period where the bot is wrong? It will be wrong. What's the feedback loop? Can I tell it "this recommendation was bad and here's why"? Does that improve future recommendations or just disappear into a void?

5. Who is liable if I follow a recommendation and lose money? Not legally — I understand it's advisory-only. But emotionally and from a product design standpoint: does the bot frame its output as "here is information to help you decide" or as "here is what you should do"? The framing matters for how I hold the bot accountable.
