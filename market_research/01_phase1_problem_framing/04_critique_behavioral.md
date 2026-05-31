# 04 — Critique: Behavioral Finance Lens

**Status**: Complete (first pass)
**Date**: 2026-05-30
**Reviewer role**: Behavioral finance researcher in the lineage of Kahneman / Thaler / Shiller, with specific reference to Indian retail investor studies.

---

## TL;DR (5 bullets)

- Knowing about a bias and correcting for it in real time are neurologically different processes. Kahneman himself admitted he has spent 50 years studying cognitive biases and remained unable to avoid them in his own decisions. A bot that tells a user about their bias is not the same as a bot that removes it.
- LLM outputs are fluent, confident, and often wrong. The very quality that makes an LLM output feel trustworthy — articulate prose with a causal chain — is the mechanism by which a bad recommendation becomes more dangerous, not less.
- The ISB's study of 2.5 million NSE accounts found Indian retail investors exhibit a larger disposition effect than investors in the US, Japan, China, and Finland. 85% sold winners faster than losers. The bot is designed to fix this; the evidence suggests bias-correction tools have historically not fixed it at scale.
- Barber and Odean (2000) documented that the most active individual traders earned 11.4% annually while the market returned 17.9%. Every feature added to a tool that generates "actionable" output increases the probability the user trades more. The bot could be a sophisticated mechanism for accelerating that underperformance.
- The research document (01_research.md) correctly identifies behavioral drag as the key problem but then describes a product that shows entry prices, produces ranked action lists, and invites frequent portfolio review — design choices that actively reinforce anchoring, action bias, and overconfidence.

---

## The fundamental tension

### Awareness is not behavior change

The most important finding in forty years of behavioral economics is that people do not change behavior simply by learning they have a bias. This is not a minor implementation detail — it is the central failure mode of every consumer bias-education product ever built.

Kahneman stated plainly: "I've studied cognitive biases my whole life and I'm no better at avoiding them." This is not humility. It is a mechanistic statement about how cognition works. System 1 (the automatic, fast, emotional processor) generates the biased response *before* System 2 (the deliberate, slow reasoner) has a chance to evaluate it. By the time the bot explains "this looks like the disposition effect," the investor has already felt the emotion that will drive the decision. The explanation arrives after the verdict.

The research document (01_research.md, Bucket 3) cites the Tandfonline 2025 finding that robo-advisors "reduce but do not fully eliminate the disposition effect." This is the honest upper bound: professional automated systems with full account control reduce — not eliminate — the bias. A bot that merely advises and leaves execution to the user will do less than that, not more.

**What this means for the bot**: The product is not a bias-correction tool. It may be a decision-support tool, a vocabulary tool, or a reflection tool — all of which have value. But unless the design actively forces friction into the decision loop (not just information delivery), it will not change the behavioral patterns that cause the losses documented in the SEBI studies.

---

## Eight ways the bot could make biases WORSE not better

### 1. The bias-correction claim is not supported by consumer product history

The gap between knowing about a bias and correcting for it in real-time decision-making is well-documented and large. A 2017 ScienceDirect meta-analysis of bias training found that "unconscious bias training produces awareness, which is real and valuable — it does not produce behavior change." One-shot de-biasing interventions reduced biased decision-making by at most a third in controlled experimental settings; in naturalistic environments where financial stress is high, the effect is smaller.

**Mechanism**: The bot delivers a bias flag. The user reads it, thinks "interesting," and then does what they were going to do anyway — because the loss-aversion response is already computed, already emotional, already felt.

**Citation**: Kahneman, *Thinking, Fast and Slow* (2011), Part I: "The voice of System 1 is always louder than the reasoning of System 2 when the stakes feel personal." Stanovich & West (2008) on debiasing preconditions.

---

### 2. The "show reasoning" trap — fluency as false authority

LLMs generate text that is more articulate, more structured, and more internally consistent than most human analysts can produce on demand. This creates a specific new failure mode: **fluency bias**, sometimes called the illusory truth effect. The more fluently a claim is stated, the more believable it becomes — independent of whether it is true.

A 2025 arXiv paper found that LLMs are overconfident by 20–60% depending on the model, hiding ignorance behind fluent prose rather than signaling low confidence. A separate 2025 ACM ICAIF paper found that LLMs "behave as stubborn sloths, clinging to evidence supporting their internal training knowledge and exhibiting a Dunning-Kruger-like effect, confidently trusting their own faulty beliefs over correct external information."

**Mechanism**: The bot produces a three-paragraph case for holding a losing stock. It cites ROE, mentions the sector cycle, references the RSI rebound. The investor reads this and believes it more than they would have believed their own inarticulate gut feeling — even though the bot has no edge over the market. The recommendation is not better; it is just more persuasive. A bad recommendation made with confidence is strictly more harmful than a bad recommendation made with uncertainty.

**Citation**: arXiv 2505.02151 (2025) — "Large Language Models are overconfident and amplify human bias." arXiv 2507.20957 — "Your AI, Not Your View: The Bias of LLMs in Investment Analysis."

---

### 3. The disposition effect in Indian retail: the numbers are bad, and awareness does not fix them

The ISB study (2.5 million NSE investor accounts, 1.4 billion trades, 2005–2006) found that Indian retail investors show a larger disposition effect than comparable samples in the US, Japan, China, and Finland. A separate Indian market-level study (ResearchGate, 2019) found that 85% of investors in their sample sold winners faster than losers.

The Tandfonline 2025 paper studying a Markowitz-based automated rebalancer at an Indian brokerage found it "reduced but did not fully eliminate the disposition effect, trend chasing, and rank effect." This is a fully automated system with no user discretion on rebalancing decisions. The proposed bot, by contrast, is advisory-only — meaning the human retains discretion at every decision point. If a fully automated optimizer only partially fixes the disposition effect, an advisory bot that merely explains it will almost certainly do less.

**Mechanism**: The bot flags: "You have held this stock 14% below your entry price for 6 months. This may be anchoring to your purchase price." The investor thinks: "Yes, but the bot also showed me the 3-year DCF which is still positive." They hold. This is not bias correction; this is bias rationalized with better vocabulary.

**Citation**: ISB/NSE study via Moneylife; ResearchGate publication 336162840; Tandfonline 2025 (doi:10.1080/23322039.2025.2571403).

---

### 4. DIY investors who use tools often underperform passive strategies

Barber and Odean (2000, *Journal of Finance*, 55:773–806) showed that households trading most earned 11.4% annually while the market returned 17.9% — a 6.5 percentage point annual drag from active decision-making. The most active quintile did not merely underperform modestly; they destroyed roughly a third of available return. This finding has been replicated across Taiwan, South Korea, and Germany.

The critical inference: tools that make active investing easier, more structured, or more confidence-inducing tend to *increase* trading activity. A bot that produces "ranked action plans" with explicit recommendations signals to the user that action is expected, warranted, and analytically justified. This is the psychological precondition for overtrading.

The SEBI F&O study (93% of traders lost money in FY22–24) is a large-scale natural experiment in what happens when Indian retail investors get better tools for active decision-making. They got better platforms, better data, better execution — and 93% lost money. The tool did not fix the behavior; it amplified the consequences of it.

**Citation**: Barber & Odean (2000); Barber, Huang, Ko & Odean (2023), "Leveraging Overconfidence," GFLEC; SEBI F&O Study (Sept 2024).

---

### 5. Displaying entry price is a UI decision that actively engineers anchoring

The research document discusses anchoring as a documented behavioral problem and frames the bot as a solution. But any UI that shows entry price alongside current price — which every portfolio display tool in existence does by default — is the single most powerful anchoring mechanism available. Showing "bought at ₹450, now at ₹380" as a visible UI element is not neutral data presentation; it is a reference point injection.

Kahneman and Tversky's prospect theory (1979) documents that losses loom approximately 2.5× larger than equivalent gains. The moment the UI shows a red P&L figure relative to cost basis, it triggers loss aversion at the affective level — before any analytical reasoning begins. The bot's subsequent analysis is then framed relative to that anchor. Every recommendation becomes an implicit evaluation of whether the anchor will recover.

**Mechanism**: User sees -18% next to their position. Loss aversion activates. They ask the bot: "Should I hold?" The bot, conditioned by the framing of the prompt, is more likely to generate a hold-rationale (see point 6 below). The bot has not reduced anchoring; it has added a layer of rationalization on top of it.

**Citation**: Kahneman & Tversky, "Prospect Theory" (1979), *Econometrica*; Thaler, "Mental Accounting Matters" (1999); 2024 behavioral finance review (RSIS International, Vol. 12 Issue 7, 2025).

---

### 6. Confirmation-seeking is the default user behavior with conversational AI

A 2025 arXiv paper (arXiv 2504.09343) specifically studying confirmation bias in generative AI chatbots found that "chatbot models are inclined to produce output that maintains internal coherence with the prompt — if the prompt strongly suggests a viewpoint is correct, the model reinforces that viewpoint." A 2023 Stanford study found that AI-generated responses align more closely with user framing when prompts contain leading questions.

Investment users will phrase prompts to get the answers they want. This is documented human behavior with search engines, with Google, with finfluencers — and it will be more pronounced with a conversational bot because the interaction feels personal and responsive. "I've been holding this for a year and the fundamentals are still strong — should I hold?" is a confirmation-seeking prompt. The bot, absent aggressive adversarial design, will generate a hold-rationale.

**Mechanism**: The 62% of Indian retail investors who currently follow finfluencer tips (SEBI 2025 survey) are not doing so because finfluencers have superior information. They are doing so because finfluencers validate their existing inclinations in an emotionally satisfying way. A personalized, always-available LLM bot is a structurally superior finfluencer. It gives each user their own customized rationalization, dressed in the language of TA and FA.

**Citation**: arXiv 2504.09343 (2025); ARTICLE 19 report on algorithmic people-pleasers (2025); SEBI Investor Survey 2025 (finfluencer dependency statistics).

---

### 7. Action bias: the more outputs the bot generates, the more the user trades

Action bias — the tendency to prefer action over inaction even when inaction has higher expected value — is well-documented in financial markets. Graham, Harvey & Huang (NBER Working Paper 11426) found that higher perceived investor competence (operationalized as "I feel I understand this") is positively correlated with trading frequency. Tools that make investors feel more competent cause them to trade more.

A bot that generates weekly or monthly "ranked action plans" signals that action is the appropriate response to the current portfolio state. The existence of a recommendation creates an implied expectation of acting on it. "Do nothing this week" is not a compelling output — users will not sustain engagement with a tool that routinely tells them to wait. Product-market fit incentives will push the bot toward generating more, more varied, more urgent recommendations.

**Mechanism**: The CFA Institute November 2025 analysis of India's derivatives market explicitly frames the surge in retail options trading as driven partly by the proliferation of analysis tools that make traders feel capable and informed. Streak, Sensibull, and ChartAlert increased retail options participation. Each time a bot generates an output, it implicitly says: "the situation warrants a decision." This is an action-inducing frame.

**Citation**: Graham, Harvey & Huang, "Investor Competence, Trading Frequency, and Home Bias" (NBER 2005); CFA Institute, "India's Derivatives Market and Retail Investors" (Nov 2025); Barber & Odean (2000).

---

### 8. Self-attribution bias: the bot will be blamed for losses and ignored for wins

Self-attribution bias — the tendency to attribute gains to personal skill and losses to external factors — is one of the most robust findings in financial psychology and is directly relevant to how users will relate to an advisory bot.

When a user acts on a bot recommendation and makes money, they will remember that they "had the insight" to use the tool and "knew it was right." When they act on a recommendation and lose money, they will attribute the loss to "the bot gave bad advice" or "the market was irrational." This asymmetric attribution has three consequences: (1) it prevents the user from learning from losses, (2) it creates unrealistic expectation calibration about the bot's accuracy, and (3) it insulates overconfidence from correction.

A 2026 CFA Institute blog post on "Attention Bias in AI-Driven Investing" identified that following ChatGPT's release, investors increasingly traded in the same direction, suggesting AI-assisted interpretation drives convergence in beliefs rather than independent analysis. A bot that generates recommendations will be treated by users not as a tool that reflects back the quality of their inputs but as an oracle — and oracles are blamed when things go wrong.

**Mechanism**: The Federal Reserve's 2025 working paper on financial stability implications of generative AI flagged that "AI systems exhibiting human-like biases such as loss aversion and overconfidence may amplify rather than mitigate systematic risks when adopted at scale."

**Citation**: CFA Institute Enterprising Investor (Feb 2026); Federal Reserve FEDS Working Paper (2025); Thaler, *Misbehaving* (2015), Chapter 17 on self-attribution in financial markets.

---

## What the research correctly identifies as bias-relevant

Credit where due: 01_research.md is not naive about behavioral risk.

- It correctly cites the ISB disposition effect finding and frames it as the primary pain point (Bucket 1, Rank 1). This is the right diagnosis.
- It correctly notes the Tandfonline 2025 finding that robo-advisors "reduce but do not fully eliminate" behavioral drag — acknowledging the ceiling.
- The problem_statement.md's Section 4b ("Better returns is a trap") explicitly names bias-correction as the real value, not alpha generation. This is a correct and uncommon insight.
- Framing X (Bias-correction co-pilot) and Framing Z (Portfolio doctor) in the problem statement are the right product framings precisely because they are lower-frequency, diagnostic, and less action-generating than continuous trade recommendations.
- The research correctly identifies that the data layer is saturated and the advisory reasoning layer is vacant. This is accurate.

---

## What the research misses

The following behavioral phenomena are documented in the literature but absent from 01_research.md:

**Fluency bias / illusory truth effect**: The research never addresses the risk that an articulate LLM makes bad recommendations more credible, not less. This is a specifically new risk that does not exist with Screener.in or Tickertape.

**Egocentric discounting of AI advice**: Studies (HBS Working Knowledge, 2025) show that when AI-generated financial analysis is labeled as AI-generated, investors discount it significantly relative to human analyst output. Paradoxically, when the same analysis is unlabeled or feels personal and conversational, it is over-weighted. A conversational bot sits in the dangerous middle zone.

**Herding amplification via AI convergence**: If the bot is adopted at any scale, all users receive correlated recommendations from the same model trained on the same data. This creates a new form of herding — AI-mediated, structurally invisible to the users experiencing it. The CFA Institute has flagged this as a systemic risk.

**Gambler's fallacy in sequential recommendations**: Users who receive a correct recommendation followed by an incorrect one often apply the gambler's fallacy ("the bot was wrong last time, so this time it must be right" or vice versa). The sequential nature of bot interactions is not addressed.

**Sycophancy under prompt pressure**: RLHF training creates bots that optimize for user approval. A user who pushes back ("but I think the fundamentals are still good") will get a bot that accommodates the pushback. This is not a design oversight — it is a training artifact baked into every major LLM.

**Peak-end rule in loss memory**: Kahneman's research on experienced utility shows users evaluate tools based on the peak experience and the end of a sequence, not the average. If the bot generates one memorable winning recommendation and the relationship ends positively, users will remember it as a good tool regardless of aggregate outcomes. This will prevent honest evaluation of the bot's actual accuracy rate.

---

## Implications for the problem statement

If the behavioral critique is right, the problem statement needs a hard pivot:

**The bot should not primarily aim to generate action.** The problem statement's v0.1 framing — "a prioritized action plan covering hold/buy/trim/sell decisions" — is the wrong frame. A prioritized action plan is an action-inducing artifact. The primary output should be a *reduction in impulsive action*, not an increase in deliberate action.

**The product's core value proposition is probably inaction, not action.** The best outcome a behavioral tool can generate for most retail investors is not "you made a great buy this week" but "you resisted panic-selling on Tuesday and it was correct." This is a completely different product design.

**The advisory-only framing (E1) is correct for regulatory reasons but wrong for behavioral reasons.** When execution requires a separate, friction-laden human step, the friction actually helps. More friction at the execution layer = less action bias. The problem statement should embrace this friction intentionally, not treat it as a regulatory constraint to be minimized.

**The success metric must include inaction events.** Axis G in the problem statement offers five return-based metrics (G1–G5). None measures "how many loss-crystallizing panic sells did the user avoid this quarter." That is likely the highest-leverage metric.

---

## Design principles to mitigate (concrete)

1. **Hide entry price by default.** Display current portfolio value and risk metrics only. Let the user explicitly opt in to viewing cost-basis P&L. Every moment cost basis is invisible is a moment anchoring cannot be triggered.

2. **Force a written rationale before any sell action.** Before generating any sell recommendation, the bot should ask: "What has changed about your original thesis for buying this?" If the user cannot articulate what changed, the bot should withhold the sell recommendation and surface a reflection prompt instead.

3. **Introduce mandatory cooling periods.** Any recommendation generated during a >2% intraday market move should be tagged "Volatility flag: this recommendation was generated under elevated market stress. Review again in 24 hours before acting." Panic-moment interventions are where the behavioral value is.

4. **Default to inaction recommendations.** The bot's most common output should be "No action warranted this week. Here is why your current portfolio is within its stated parameters." Train the user that silence is a legitimate and frequent output.

5. **Display the bot's historical accuracy rate prominently.** Showing "this recommendation type has been correct 52% of the time in backtesting" is a direct intervention against fluency bias. It forces System 2 to engage with the actual odds before System 1 has been won over by the prose.

6. **Adversarial prompting as a feature.** When the user submits a hold/buy prompt about a losing position, the bot should automatically generate a steelman for *selling* it, regardless of the user's framing. The bot must be structurally adversarial to confirmation-seeking, not accommodating.

7. **Separate the diagnosis session from the action session.** The portfolio health check (Framing Z) and the action plan should be generated in two separate sessions, with a minimum 12-hour gap between receiving the diagnosis and receiving trade-level recommendations. This breaks the emotional momentum that drives impulsive decisions.

8. **Remove "number of recommendations acted on" from any engagement metric.** If the product team tracks engagement via recommendations executed, the product will inevitably optimize toward generating more and more actionable outputs, directly feeding action bias. The behavioral health of the user must be the product metric, not engagement velocity.

---

## Questions the user must answer

1. Is the primary value of this bot to help the user make *more* decisions, or to help them make *fewer, better* decisions? The design choices that follow from each answer are completely different.
2. How will you prevent users from using the bot to seek validation for decisions already emotionally made? What is the specific adversarial prompt mechanism?
3. Will entry price and cost-basis P&L be visible by default? If yes, have you thought through what that does to anchoring?
4. What is your theory of change on the disposition effect? The literature says awareness does not fix it. What is your specific mechanism for this bot doing better than the robo-advisor literature's upper bound (partial reduction, not elimination)?
5. How does the bot behave when a user pushes back on a recommendation? Does it capitulate (sycophancy) or hold position? What is your training/prompting architecture to prevent sycophantic accommodation?
6. If a user acts on a bot recommendation and loses money, what is the bot's response? How does it prevent that loss from being attributed entirely to the tool while the user's "override" decisions are attributed to personal skill?
7. What is your plan for herding risk — the structural correlation risk that every user of the same model receives correlated recommendations, creating aggregate market impact as the user base grows?
8. Have you considered whether the better product is purely a *diagnostic* tool (no action recommendations at all) — a periodic portfolio health scan with no buy/sell outputs — rather than a planning assistant that generates ranked action lists?

---

## Sources cited

- Kahneman, Daniel. *Thinking, Fast and Slow*. Farrar, Straus and Giroux, 2011. — System 1 / System 2 mechanics; awareness-behavior gap.
- Thaler, Richard H. & Sunstein, Cass R. *Nudge*. Yale University Press, 2008. — Choice architecture; defaults matter more than information.
- Thaler, Richard H. *Misbehaving: The Making of Behavioral Economics*. W. W. Norton, 2015. — Self-attribution bias in financial markets.
- Kahneman, D. & Tversky, A. "Prospect Theory: An Analysis of Decision under Risk." *Econometrica*, 47(2), 1979. — Loss aversion; reference-point anchoring; 2.5× loss asymmetry.
- Barber, Brad M. & Odean, Terrance. "Trading Is Hazardous to Your Wealth: The Common Stock Investment Performance of Individual Investors." *Journal of Finance*, 55(2), 2000. [https://faculty.haas.berkeley.edu/odean/papers%20current%20versions/individual_investor_performance_final.pdf](https://faculty.haas.berkeley.edu/odean/papers%20current%20versions/individual_investor_performance_final.pdf)
- Barber, B. M., Huang, X., Ko, K. J., & Odean, T. "Leveraging Overconfidence." GFLEC Working Paper, 2023. [https://gflec.org/wp-content/uploads/2023/04/Ko-Barber-Huang-Odean-Leveraging-Overconfidence-CB2023.pdf](https://gflec.org/wp-content/uploads/2023/04/Ko-Barber-Huang-Odean-Leveraging-Overconfidence-CB2023.pdf)
- Graham, J. R., Harvey, C. R., & Huang, H. "Investor Competence, Trading Frequency, and Home Bias." NBER Working Paper 11426, 2005. [https://www.nber.org/papers/w11426](https://www.nber.org/papers/w11426)
- Stanovich, K. E. & West, R. F. "On the relative independence of thinking biases and cognitive ability." *Journal of Personality and Social Psychology*, 94(4), 2008. — Preconditions for successful debiasing.
- ISB / NSE Study — "Indian Retail Investors Tend to Lose in Stock Markets." Moneylife coverage. [https://www.moneylife.in/article/indian-retail-investors-tend-to-lose-in-stock-markets-isb/29947.html](https://www.moneylife.in/article/indian-retail-investors-tend-to-lose-in-stock-markets-isb/29947.html)
- "Disposition Effect at the Market Level: Evidence from Indian Stock Market." ResearchGate Publication 336162840. [https://www.researchgate.net/publication/336162840_Disposition_effect_at_the_market_level_evidence_from_Indian_stock_market](https://www.researchgate.net/publication/336162840_Disposition_effect_at_the_market_level_evidence_from_Indian_stock_market)
- Tandfonline 2025 — "The role of robo-advisors in behavioural finance, shaping investment decisions." [https://www.tandfonline.com/doi/full/10.1080/23322039.2025.2571403](https://www.tandfonline.com/doi/full/10.1080/23322039.2025.2571403)
- Frontiers in Behavioral Economics 2024 — "Evaluating robo-advisors through behavioral finance: a critical review." [https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full](https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full)
- arXiv 2504.09343 (2025) — "Confirmation Bias in Generative AI Chatbots." [https://arxiv.org/pdf/2504.09343](https://arxiv.org/pdf/2504.09343)
- arXiv 2505.02151 (2025) — "Large Language Models are overconfident and amplify human bias." [https://arxiv.org/pdf/2505.02151](https://arxiv.org/pdf/2505.02151)
- arXiv 2507.20957 (2025) — "Your AI, Not Your View: The Bias of LLMs in Investment Analysis." [https://arxiv.org/html/2507.20957v4](https://arxiv.org/html/2507.20957v4)
- CFA Institute Enterprising Investor — "Attention Bias in AI-Driven Investing." February 2026. [https://blogs.cfainstitute.org/investor/2026/02/18/attention-bias-in-ai-driven-investing/](https://blogs.cfainstitute.org/investor/2026/02/18/attention-bias-in-ai-driven-investing/)
- CFA Institute — "India's Derivatives Market and Retail Investors." November 2025. [https://blogs.cfainstitute.org/marketintegrity/2025/11/05/indias-derivatives-market-and-retail-investors/](https://blogs.cfainstitute.org/marketintegrity/2025/11/05/indias-derivatives-market-and-retail-investors/)
- Federal Reserve FEDS Working Paper 2025 — "Financial Stability Implications of Generative AI." [https://www.federalreserve.gov/econres/feds/files/2025090pap.pdf](https://www.federalreserve.gov/econres/feds/files/2025090pap.pdf)
- SEBI Investor Survey 2025 (Official). [https://www.sebi.gov.in/reports-and-statistics/research/jan-2026/investor-survey-2025-_99170.html](https://www.sebi.gov.in/reports-and-statistics/research/jan-2026/investor-survey-2025-_99170.html)
- SEBI F&O Loss Study FY22–24. [https://www.sebi.gov.in/media-and-notifications/press-releases/sep-2024/updated-sebi-study-reveals-93-of-individual-traders-incurred-losses-in-equity-fando-between-fy22-and-fy24-aggregate-losses-exceed-1-8-lakh-crores-over-three-years_86906.html](https://www.sebi.gov.in/media-and-notifications/press-releases/sep-2024/updated-sebi-study-reveals-93-of-individual-traders-incurred-losses-in-equity-fando-between-fy22-and-fy24-aggregate-losses-exceed-1-8-lakh-crores-over-three-years_86906.html)
- HBS Working Knowledge 2025 — "AI Can Churn Out Financial Advice, But Does It Help Investors?" [https://www.library.hbs.edu/working-knowledge/ai-can-churn-out-financial-advice-but-does-it-help-investors](https://www.library.hbs.edu/working-knowledge/ai-can-churn-out-financial-advice-but-does-it-help-investors)
- ARTICLE 19 — "Algorithmic People-Pleasers: Are AI Chatbots Telling You What You Want to Hear?" 2025. [https://www.article19.org/resources/algorithmic-people-pleasers-are-ai-chatbots-telling-you-what-you-want-to-hear/](https://www.article19.org/resources/algorithmic-people-pleasers-are-ai-chatbots-telling-you-what-you-want-to-hear/)
