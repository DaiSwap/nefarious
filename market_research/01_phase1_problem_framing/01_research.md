# 01 — Market Research on Problem Statements

**Status**: Complete (first pass)
**Date**: 2026-05-30
**Scope**: Problem-statement framing across pain points, Indian products, academic literature, LLM-finance agents, and synthesized gaps.

---

## Executive Summary (10 bullets)

1. **The loss crisis is documented and severe**: SEBI's 2024 study found 93% of individual F&O traders lost money (FY22–24); losses exceeded ₹1.8 lakh crore over three years. Even in equity cash markets, the ISB's landmark study of 2.5 million NSE investors found Indian retail investors show a *larger* disposition effect than peers in the US, Japan, China, and Finland — booking profits too early and holding losses too long.

2. **The SEBI 2025 survey names the real problem**: Only 9.5% of aware households actually invest. 62% of active retail investors make decisions based on social-media finfluencers. The documented barrier is not data access — it's *comprehension gaps* and *absence of a systematic personal process*.

3. **Every Indian product solves data access or execution, not decision quality**: Screener.in, Tickertape, Tijori, Trendlyne, StockEdge — all give investors better data. Smallcase gives curated baskets. Zerodha Console gives analytics. None produces a *personalized reasoning chain* over a specific user's portfolio that outputs an actionable decision.

4. **The TA+FA integration gap is real**: Investar and ChartAlert offer combined screens, but no Indian tool synthesizes technical signals with fundamental quality scores *at the portfolio level* and explains the conflict or alignment to the user.

5. **Robo-advisors in India are MF-oriented, not equity-stock-oriented**: Kuvera, INDmoney, ETMoney — all route users toward mutual funds and SIPs. None applies personalized portfolio optimization to *direct equity* holdings. INDmoney explicitly is not SEBI-registered, so its suggestions are legally constrained to being generic.

6. **Global LLM tools (BloombergGPT, FinGPT, AlphaAgents, Magnifi) target institutions or US markets**: BloombergGPT is closed, institutional-only. FinGPT is open-source but weak on numerical reasoning. AlphaAgents (BlackRock, 2025) is institutional. No LLM product with an Indian-market-first framing exists at consumer quality.

7. **Academic literature frames the robo-advisor problem as bias-reduction, not alpha-generation**: The consensus finding is that personalization quality is highest for investors with stable risk profiles, and that the key value of advisory systems is *reducing behavioral drag* (disposition effect, panic selling, herding) rather than picking winning stocks.

8. **Portfolio optimization models each solve a narrow sub-problem**: Markowitz solves mean-variance tradeoffs but is numerically unstable with many assets; Black-Litterman incorporates investor views but requires explicit prior beliefs; HRP solves the invertibility problem but ignores return forecasts. None outputs a "what should I do this week" recommendation.

9. **The "action gap" is the clearest white space**: Every tool gives data *about* a portfolio. No Indian tool says "based on your current positions, here is a ranked list of actions you should take and why, weighted by urgency, risk, and your stated strategy." This is the framing our bot should own.

10. **Regulatory constraint is a real scoping lever**: Auto-execution requires SEBI-registered algo approval. Personalized for-compensation advice requires RIA registration. Advisory-only, self-use framing (E1) is the safe and sufficient starting point — and is the framing none of the existing tools fully occupies.

---

## Bucket 1 — Indian Retail Investor Pain Points

### Key Findings

#### 1.1 Documented Loss Scale
- **SEBI FY24 study**: 93% of individual equity F&O traders incurred net losses between FY22–FY24. Aggregate losses: ₹1.8 lakh crore over 3 years. [Source: SEBI Press Release Sept 2024](https://www.sebi.gov.in/media-and-notifications/press-releases/sep-2024/updated-sebi-study-reveals-93-of-individual-traders-incurred-losses-in-equity-fando-between-fy22-and-fy24-aggregate-losses-exceed-1-8-lakh-crores-over-three-years_86906.html)
- **SEBI FY25 update**: Net losses of individual traders surged 41% YoY to ₹1,05,603 crore in FY25. [Source: Moneylife, 2025](https://www.moneylife.in/article/91-percentage-of-retail-traders-lost-money-in-derivatives-losses-in-fo-surged-41-percentage-to-rs105-lakh-crore-in-fy2425-sebi-study/77613.html)
- **ISB study (largest behavioral finance dataset ever, 2.5 million NSE investors, 1.4 billion trades, Jan 2005–Jun 2006)**: Retail investors lost ₹83.76 billion over 18 months (~₹55.84 billion/year). [Source: Business Standard, ISB](https://www.business-standard.com/article/markets/retail-investors-tend-to-lose-in-stock-markets-says-isb-study-112120100043_1.html)

#### 1.2 Behavioral Biases Documented in Indian Context
- **Disposition effect**: Indian retail investors exhibit a *larger* disposition effect than US, Japanese, Chinese, and Finnish investors — holding losers too long, booking winners too fast. [ISB/NSE study via Moneylife](https://www.moneylife.in/article/indian-retail-investors-tend-to-lose-in-stock-markets-isb/29947.html)
- **Research finding**: 85% of investors in one sample sold winners faster than losers. [Disposition Effect paper, ResearchGate](https://www.researchgate.net/publication/336162840_Disposition_effect_at_the_market_level_evidence_from_Indian_stock_market)
- **Herding**: "Herding is a very common form of bias in the Indian stock market" alongside representativeness bias, overconfidence, cognitive dissonance. [Multiple academic sources, ResearchGate 2024](https://www.researchgate.net/publication/397113427_Behavioral_Biases_and_Investment_Choices_Understanding_the_Mediating_Role_of_Risk_Perception_among_Indian_Retail_Investors)
- **Overconfidence + excess trading**: Excessive trading amplifies losses among underperformers while the *same behavior* increases returns for outperformers — meaning overconfidence is doubly dangerous for the loss-prone majority. [JRPS Journal study](https://jrpsjournal.in/index.php/j/article/view/317)
- **Finfluencer dependency**: 62% of active retail investors acknowledge making investment choices influenced by social-media finfluencers; 93% rate them as moderately to highly trustworthy. [SEBI Investor Survey 2025](https://www.sebi.gov.in/reports-and-statistics/research/jan-2026/investor-survey-2025-_99170.html)
- **FOMO and overconfidence as key drivers**: SEBI identifies "cognitive biases like FOMO and overconfidence" as primary catalysts for the surge in retail options trading. [Whalesbook/SEBI analysis, 2025](https://www.whalesbook.com/news/English/sebiexchange/Indias-Retail-Frenzy-Info-Gap-Fuels-Volatility-SEBI-Tackles-Finfluencers/699c8d82d83cd4ce4fe95e37)

#### 1.3 Structural / Process Failures
- **Information comprehension gap, not access gap**: SEBI highlights that "information asymmetry in Indian markets stems from comprehension gaps, not just availability." [Forrester / SEBI analysis 2024](https://www.forrester.com/blogs/thats-what-we-predicted-for-indian-financial-services-in-2024/)
- **Awareness–action gap**: 63% of households are aware of securities products; only 9.5% actually invest. Fear of losses (30–34% of non-investors) and complexity (74% cite it) dominate barriers. [SEBI Investor Survey 2025](https://scanx.trade/stock-market-news/stocks/sebi-investor-survey-2025-63-households-aware-of-market-products-only-9-5-actually-invest/30475080)
- **Risk appetite mismatch**: Nearly 80% of Indian households prefer capital preservation, yet retail F&O participation has surged — suggesting a *stated vs. revealed* preference gap driven by FOMO. [SEBI 2025, finnovate.in](https://www.finnovate.in/learn/blog/sebi-investor-survey-2025-insights)
- **Panic selling / recency bias**: SEBI notes "increased selling during bear markets, driven by fear of losses, and aggressive buying during bull markets, fueled by greed" — a textbook buy-high-sell-low behavioral loop. [SEBI DRG "Elusive Retail Investor" study](https://www.sebi.gov.in/sebi_data/DRG_Study/elusiveretailinvestor.pdf)
- **Institutional technology gap**: Institutional investors have algorithmic systems executing in milliseconds; this technological edge widens as AI evolves, structurally disadvantaging retail participants. [CFA Institute, Nov 2025](https://blogs.cfainstitute.org/marketintegrity/2025/11/05/indias-derivatives-market-and-retail-investors/)

### Sources Cited
- [SEBI FY24 F&O Loss Study — Press Release](https://www.sebi.gov.in/media-and-notifications/press-releases/sep-2024/updated-sebi-study-reveals-93-of-individual-traders-incurred-losses-in-equity-fando-between-fy22-and-fy24-aggregate-losses-exceed-1-8-lakh-crores-over-three-years_86906.html)
- [SEBI Investor Survey 2025 — Main Report](https://www.sebi.gov.in/reports-and-statistics/research/jan-2026/investor-survey-2025-_99170.html)
- [SEBI Investor Survey 2025 — Insights breakdown](https://www.finnovate.in/learn/blog/sebi-investor-survey-2025-insights)
- [ISB Study — Business Standard](https://www.business-standard.com/article/markets/retail-investors-tend-to-lose-in-stock-markets-says-isb-study-112120100043_1.html)
- [ISB Study — Moneylife](https://www.moneylife.in/article/indian-retail-investors-tend-to-lose-in-stock-markets-isb/29947.html)
- [Behavioral Biases & Investment Choices — ResearchGate 2024](https://www.researchgate.net/publication/397113427_Behavioral_Biases_and_Investment_Choices_Understanding_the_Mediating_Role_of_Risk_Perception_among_Indian_Retail_Investors)
- [Disposition Effect at Market Level — Indian Stock Market](https://www.researchgate.net/publication/336162840_Disposition_effect_at_the_market_level_evidence_from_Indian_stock_market)
- [CFA Institute — India Derivatives & Retail Investors](https://blogs.cfainstitute.org/marketintegrity/2025/11/05/indias-derivatives-market-and-retail-investors/)
- [SEBI "Elusive Retail Investor" DRG Study](https://www.sebi.gov.in/sebi_data/DRG_Study/elusiveretailinvestor.pdf)
- [Moneylife — FY25 Loss Surge](https://www.moneylife.in/article/91-percentage-of-retail-traders-lost-money-in-derivatives-losses-in-fo-surged-41-percentage-to-rs105-lakh-crore-in-fy2425-sebi-study/77613.html)

### Pain Points Ranked by Frequency-of-Mention

| Rank | Pain Point | Evidence Strength |
|------|-----------|-------------------|
| 1 | Disposition effect (hold losers, sell winners too early) | ISB 2.5M investor study; multiple academic papers; larger than any comparable nation |
| 2 | Finfluencer dependency / tip-chasing | SEBI 2025 (62% influenced by finfluencers); SEBI crackdown actions |
| 3 | Overconfidence + overtrading | ISB study; multiple behavioral finance papers; SEBI FOMO reference |
| 4 | Panic selling in bear markets / recency bias | SEBI investor surveys (2015, 2025); behavioral pattern documented |
| 5 | Comprehension gap (data exists, can't act) | SEBI explicit finding; Forrester 2024; finnovate breakdown |
| 6 | Concentration risk | ISB study; behavioral finance papers; portfolio diversification gap |
| 7 | No systematic personal investment process | Implied by finfluencer reliance; CFA analysis; robo-advisor adoption gap |
| 8 | FOMO-driven leverage (F&O overuse) | SEBI F&O studies; CFA Institute 2025 |

---

## Bucket 2 — Existing Indian Products and Their Problem Framings

### Per-Product Table

| Product | Stated Problem (Framing) | What They DON'T Solve | Source URL |
|---------|--------------------------|----------------------|------------|
| **Screener.in** | "Stock analysis and screening tool for investors in India" — democratize fundamental data access; investors rely on tips because FA data was inaccessible | No TA signals; no portfolio-level advice; no "what should I do" output; no bias correction | [screener.in](https://www.screener.in/) |
| **Tickertape** | "Financial freedom begins here" — "data, information & content for Indian stocks, mutual funds, ETFs & indices"; the market is a "complex maze" | No personalized action plan; no portfolio-level synthesis; tools for research, not for deciding | [tickertape.in](https://www.tickertape.in/) |
| **Tijori Finance** | "A suite of tools for comprehensive Investment Research & Tracking" — fragmentation of equity research data; investors need one place to "keep an eye on investments and track exposure & risk" | Deep research, not decision; no TA; no action plan output; no bias detection | [tijorifinance.com/features](https://www.tijorifinance.com/features/) |
| **Smallcase** | "Put your money to work. Build long-term wealth with expert-managed portfolios" — investors have an idea but can't find/assemble the right stocks; need curated baskets | Passive basket consumption, not portfolio analysis; no optimization of existing holdings; no TA; not for users who want control | [smallcase.com](https://www.smallcase.com/) |
| **Streak (Zerodha)** | Algorithmic trading "without coding" — retail traders can't implement systematic strategies because they require Python/R expertise; they lose money watching screens manually | Strategy backtester, not portfolio advisor; no fundamental signals; no portfolio-level reasoning; short-term algo focus | [top10stockbroker review](https://top10stockbroker.com/algo-trading-platform/zerodha-streak/) |
| **Tradetron** | "No-code/low-code automated algo trading" — coding barrier to systematic trading; deploy strategies across 50+ brokers | Execution automation, not planning; no FA; no existing-portfolio analysis; institutional complexity | [tradingtuitions.com comparison](https://tradingtuitions.com/tradetron-vs-streak-which-is-a-better-algorithmic-trading-platform/) |
| **Sensibull** | "Less than 1% of options traders make money" — options complexity intimidates retail traders; they treat F&O as lottery | Options-only; no equity portfolio planning; no FA; not for long-term investors | [sensibull.com](https://sensibull.com/) |
| **StockEdge** | Research and screening — "stock screeners, market analysis, technical tools, portfolio insights, institutional data" | Aggregates data; no synthesis; no personalized action; more data layer than advisory layer | [strike.money review](https://www.strike.money/reviews/trendlyne) |
| **Trendlyne** | "The Stock Market Platform to Stay Ahead" — investors need DVM (Durability, Valuation, Momentum) screening to stay competitive | Data + screens, not decisions; no portfolio-level personalized reasoning; no integrated TA+FA action plan | [trendlyne.com](https://trendlyne.com/) |
| **MoneyControl** | News + data aggregation — "comprehensive financial news and data portal" | News, not advice; no portfolio optimization; no action plan | [Google Play listing](https://play.google.com/store/apps/details?id=com.divum.MoneyControl) |
| **ETMoney / INDmoney** | "Simplify the digital finance journey" / holistic financial management — fragmented personal finance | MF/SIP focused; not SEBI-RIA so advice is generic not personalized; no direct equity portfolio optimization | [invsify.com comparison](https://invsify.com/blog/best-portfolio-optimization-software) |
| **Kuvera** | "Simplify your wealth management" — goal-based MF investing | MF-only; no direct equity analysis; no TA/FA for stock holdings | [Wikipedia/Kuvera](https://en.wikipedia.org/wiki/Kuvera.in) |
| **Groww** | Cost barrier + complexity — "simple, flat-fee brokerage for beginners and long-term investors" | Execution platform; no research tools; no portfolio advice | [saras.market review](https://www.saras.market/blogs/top-10-trading-apps-india) |
| **Zerodha Console** | Analytics gap — "multi-dimensional insights on your trades and portfolio"; retail investors couldn't compute accurate P&L, sector exposure, or tax implications | *Backward-looking* (analytics on past trades); no forward recommendations; no TA or FA signals; no action plan | [zerodha.com/products/console](https://zerodha.com/products/console/) |
| **AngelOne SmartAPI** | Institutional-grade API access for retail — programmatic access to trading | Developer tool, not advisory; no reasoning layer; raw data/execution | [angelone.in](https://www.angelone.in) |
| **Zerodha Varsity** | Financial literacy gap — "retail investors were entering markets without understanding what they are buying" | *Education*, not execution; reading-room, not planning tool; knowledge gap addressed but action gap not | [zerodha.com/varsity](https://zerodha.com/varsity/) |

### Patterns Across Products

**Pattern 1 — The data layer is saturated.** Screener.in, Tickertape, Tijori, StockEdge, Trendlyne, MoneyControl all compete on data quality and breadth. The problem "I can't find financial data" is largely solved.

**Pattern 2 — Execution is democratized.** Groww, Zerodha, Upstox, Dhan, AngelOne have made brokerage nearly zero-cost and mobile-native. The problem "investing is too expensive/inaccessible" is largely solved.

**Pattern 3 — The advisory-reasoning layer is vacant for direct equity.** No product asks: "given YOUR holdings, YOUR strategy preferences, and TODAY's data, what should YOU specifically do?" The closest analog is Smallcase (pre-built baskets) and Zerodha Console (portfolio analytics), but neither closes the loop with a reasoned recommendation.

**Pattern 4 — MF robo-advisors exist but don't generalize to stocks.** Kuvera, INDmoney, ETMoney serve the mutual fund investor. The direct equity investor is unserved by the advisory layer.

**Pattern 5 — TA and FA exist in silos.** Screener.in is FA-only. Streak is TA/algo. Trendlyne does both but does not synthesize them into a recommendation. No product has a conflict-resolution layer for when TA and FA disagree on the same stock.

---

## Bucket 3 — Academic & Industry Framings

### Robo-Advisor Literature

The academic framing of the robo-advisor problem has shifted from "portfolio construction automation" (early 2010s) toward "behavioral bias reduction" (2020s).

**Standard framing (2015–2020)**: Robo-advisors gather investor risk-profile data via questionnaire, then recommend ETF portfolios using mean-variance optimization or risk-parity. Problem = automation of client profiling and asset allocation. [Frontiers in Behavioral Economics 2024](https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full)

**Key critique of this framing (2024 Frontiers paper)**: Robo-advisors claim to "de-humanize" investment decisions to eliminate bias, but four failures persist:
1. They lack "affective trust" — the emotional basis of an advisory relationship.
2. Their algorithms inherit the biases in historical training data.
3. They cannot manage systematic market risk (only diversifiable risk).
4. They foster financial dependency rather than financial literacy.

**Indian-context framing (Banerjee 2025, Wiley)**: "What drives retail Indian investors to robo-advisors?" — found that perceived interactivity, personalization, autonomy, and algorithm transparency influence adoption. Indian robo-advisor adoption slower than global peers because of trust gap. [Wiley 2025](https://onlinelibrary.wiley.com/doi/abs/10.1002/isd2.12346)

**Behavioral robo-advisor finding (Tandfonline 2025)**: "Robo-advising reduces — but does not fully eliminate — the disposition effect, trend chasing, and rank effect." An automated portfolio optimizer at an Indian brokerage (using Markowitz MVO) reduced but did not cure behavioral drag. [Tandfonline 2025](https://www.tandfonline.com/doi/full/10.1080/23322039.2025.2571403)

**Personalized robo-advising (Capponi, Olafsson, Zariphopoulou — Management Science 2022)**: Personalization is most beneficial for investors with stable risk profiles. Key finding: "Sharpe ratios are higher if robo-advisors deviate from the client tendency to reduce market exposure during market downturns" — i.e., the bot's biggest value is *counteracting* the human's panic. [Wiley Literature Review](https://onlinelibrary.wiley.com/doi/10.1111/ijcs.70131)

### Portfolio Optimization Literature

Each major framework solves a narrow, formally-specified problem — none outputs a plain-language action plan:

| Framework | Formal Problem It Solves | Key Limitation |
|-----------|--------------------------|----------------|
| **Markowitz MPT (1952)** | Minimize portfolio variance for a given expected return (or maximize return for given variance) | Numerically unstable with many assets; sensitive to input estimation errors; no "buy/sell" output |
| **Black-Litterman (1990)** | Blend market equilibrium priors with investor's subjective views into a stable portfolio | Requires investor to explicitly quantify views and confidence levels; not intuitive for retail |
| **Risk Parity** | Equalize risk contribution across assets (not capital allocation) | Ignores return forecasts; can be suboptimal in trending markets; complex for retail |
| **HRP (Lopez de Prado, 2016)** | Portfolio construction without requiring covariance matrix inversion; works on ill-conditioned matrices | Ignores return forecasts; addresses math problem, not decision problem |
| **Factor Investing (Fama-French+)** | Capture systematic return premia (value, size, momentum, quality, low-vol) | High turnover for momentum; hard to implement at individual stock level; factor data sparse for mid/small-cap India |

**Critical gap**: All of these produce *weights* or *allocations*. None of them tell a human investor "sell 30% of your HDFC Bank position" in natural language with a reason attached.

### Recent Papers (2020–2026)

| Paper | Year | Problem Framing | Gap/Finding |
|-------|------|----------------|-------------|
| [LLM-based Personalized Portfolio Recommender (arXiv 2512.12922)](https://arxiv.org/abs/2512.12922) | 2024 | "Traditional rule-based or static optimization approaches fail to capture nonlinear interactions among investor behavior, market volatility, and evolving financial objectives" | Combines LLM (user preference) + RL (market adaptation); still US-market-centric; no Indian data |
| [Democratizing Alpha: LLM-Driven Portfolio Construction (ACM ICAIF 2024)](https://dl.acm.org/doi/10.1145/3768292.3770376) | 2024 | Institutional-grade portfolio construction is inaccessible to retail; LLMs can extract signals from public financial media | Backtested on S&P500/NASDAQ only; no Indian market; no personalization to existing holdings |
| [Financial News-Driven LLM RL for Portfolio Mgmt (arXiv 2411.11059)](https://arxiv.org/html/2411.11059v1) | 2024 | "Gap in literature: integration of LLM-driven sentiment analysis into RL models for portfolio management" | Sentiment+RL outperforms pure RL; no FA integration; no individual investor layer |
| [AlphaAgents (BlackRock, arXiv 2508.11152)](https://arxiv.org/abs/2508.11152) | 2025 | "Multi-agent LLMs for systematic equity portfolio construction: prior studies emphasize chain-of-thought but neglect structured agent interaction" | Institutional tool; no Indian market; no retail or personalization layer |
| [Robo-advisors: Systematic Literature Review (ScienceDirect 2024)](https://www.sciencedirect.com/science/article/abs/pii/S1544612324001491) | 2024 | "Standardized frameworks fail to adapt to local market structures" and "strategy convergence creates collective vulnerability during crises" | Personalization remains the core unsolved problem; local-market adaptation is a gap |
| [Evaluating Robo-Advisors through Behavioral Finance (Frontiers 2024)](https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full) | 2024 | Robo-advisors cannot eliminate bias because algorithms inherit biases in historical data; financial literacy neglected | Bias-correction as a problem statement is validated; human reasoning layer needed |
| [LLM-Enhanced Black-Litterman (arXiv 2504.14345)](https://arxiv.org/html/2504.14345v2) | 2025 | BL model requires explicit investor views which are hard to elicit; LLMs can generate and quantify these views automatically | Still institutional; no retail interface; no Indian market |

### Sources

- [Frontiers Behavioral Economics — Robo-Advisor Critique 2024](https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full)
- [Wiley — Evolution of Robo-Advisors Literature Review 2025](https://onlinelibrary.wiley.com/doi/10.1111/ijcs.70131)
- [Tandfonline — Robo-advisors in Behavioural Finance 2025](https://www.tandfonline.com/doi/full/10.1080/23322039.2025.2571403)
- [Wiley — Banerjee 2025 Indian Robo-Advisor Adoption](https://onlinelibrary.wiley.com/doi/abs/10.1002/isd2.12346)
- [ScienceDirect — Robo-Advisors Systematic Review 2024](https://www.sciencedirect.com/science/article/abs/pii/S1544612324001491)
- [arXiv 2512.12922 — LLM Portfolio Recommender](https://arxiv.org/abs/2512.12922)
- [ACM ICAIF 2024 — Democratizing Alpha](https://dl.acm.org/doi/10.1145/3768292.3770376)
- [arXiv 2411.11059 — Financial News LLM RL](https://arxiv.org/html/2411.11059v1)
- [arXiv 2508.11152 — AlphaAgents (BlackRock)](https://arxiv.org/abs/2508.11152)
- [arXiv 2504.14345 — LLM-Enhanced Black-Litterman](https://arxiv.org/html/2504.14345v2)
- [Wikipedia — Hierarchical Risk Parity](https://en.wikipedia.org/wiki/Hierarchical_Risk_Parity)

---

## Bucket 4 — LLM-Finance Agent Landscape

### Per-Agent Table

| Product / Paper | Problem Framing | Stated Gap Filled | What Still Remains | Source URL |
|-----------------|-----------------|------------------|--------------------|------------|
| **BloombergGPT** (Bloomberg, 2023) | Finance generates enormous unstructured text (news, filings, reports); general LLMs perform poorly on financial NLP tasks | Proprietary 50B-param model trained on Bloomberg's financial corpus | Closed, institutional-only; requires Bloomberg terminal access; ~$2.67M training cost — zero retail access; no Indian market | [Bloomberg Press Release](https://www.bloomberg.com/company/press/bloomberggpt-50-billion-parameter-llm-tuned-finance/) |
| **FinGPT** (AI4Finance, 2023) | BloombergGPT's data is proprietary; need an *open-source* financial LLM to democratize FinLLM research | Open-source, data-centric pipeline; low-cost fine-tuning via LoRA/RLHF | Weak on complex reasoning, numerical arithmetic, summarization; no Indian market adaptation; not a retail product | [arXiv 2306.06031](https://arxiv.org/abs/2306.06031) |
| **FinRL** (Columbia/AI4Finance, 2021+) | Retail investors and researchers lack accessible RL-based trading frameworks | Open-source deep RL library (DDPG, SAC, PPO) for automated stock trading | Academic/research tool; no natural language interface; no FA signals; no personalization to individual portfolios; US-centric | [FinRL at Columbia](https://openfin.engineering.columbia.edu/research-projects/financial-reinforcement-learning-finrl) |
| **AlphaAgents** (BlackRock, 2025) | "Multi-agent LLMs for systematic equity portfolio construction remain relatively unexplored; prior studies neglect structured agent interaction" | Role-based multi-agent system integrating fundamental, sentiment, and valuation analyses; reduces hallucination via agent debate | Institutional tool; closed-source; no Indian market; no retail personalization layer | [arXiv 2508.11152](https://arxiv.org/abs/2508.11152) |
| **Magnifi** (TIFIN, US, 2023+) | Individual investors struggle to monitor "dozens of variables" across fragmented accounts; traditional advisors have conflicts of interest | AI-powered portfolio health check; buy/sell impact analysis; natural language interface to $2B+ in linked assets | US market only; no Indian NSE coverage; no TA signals; advice is generic not strategy-personalized | [Magnifi / TIFIN](https://tifin.com/news/magnifi-now-providing-ai-powered-investment-intelligence-on-over-2b-of-linked-self-directed-assets/) |
| **Composer** (US, 2025) | "Algorithmic trading historically requires Python/R and brokerage API expertise"; retail investors can't implement systematic strategies | No-code AI trading platform; describe strategy in plain English; AI builds, backtests, and executes | US market only; strategy builder not portfolio advisor; no FA integration; no existing-holdings analysis | [BusinessWire 2025](https://www.businesswire.com/news/home/20251021050436/en/Composer-Supercharges-Investing-Platform-with-New-Trade-With-AI-Tool) |
| **Kavout** | Retail traders and financial advisors need fundamental, pricing, and alternative data ranked into actionable signals | Kai Score (ML equity rating 1–9); InvestGPT for prompt-based analysis; Smart Signals | US-focused; signal provider not portfolio advisor; no personalized existing-holdings reasoning | [Kavout Review 2026](https://www.aitoolcurator.com/ai-tools/finance-investing/kavout/) |
| **Numerai** | Hedge fund needs diverse ML predictions; crowdsourced data scientists outperform internal analysts | Crowdsourced encrypted ML tournament; ensemble Meta Model powers hedge fund | Institutional hedge fund application; encrypted (can't reuse signals); not a retail advisory tool | [Gate Learn — Numerai](https://www.gate.com/learn/articles/what-is-numerai/742) |
| **PortfolioPilot** (US) | Managing investments requires monitoring dozens of variables; traditional advisors have conflicts | AI portfolio analysis, consolidated net worth, personalized recommendations, tax optimization | US-only; no Indian NSE; no TA signals; recommendations general not strategy-specific | [portfoliopilot.com](https://portfoliopilot.com/) |
| **LLM+RL Paper (arXiv 2411.11059)** | Sentiment+RL outperforms pure RL but literature gap exists in integrating LLM-derived signals into RL for portfolio management | Demonstrates sentiment-enhanced RL beats market; higher net worth and cumulative profit | Academic; US/global markets; no FA integration; no retail user interface; no Indian market | [arXiv 2411.11059](https://arxiv.org/html/2411.11059v1) |

### Key Patterns in LLM-Finance Products

1. **US-market-first, universally**: Every commercial LLM-finance product (Magnifi, Composer, Kavout, PortfolioPilot) is built for US equities. NSE/BSE is unserved at this product quality level.
2. **Institutional models dominate the research frontier**: AlphaAgents (BlackRock), BloombergGPT — these are not consumer products. The gap between institutional AI quality and retail AI access is large.
3. **TA+FA integration is unsolved even in LLM tools**: Most LLM-finance tools use sentiment (NLP on news) or fundamentals. Pure TA (RSI, MACD, Bollinger) is almost entirely absent from LLM-reasoning pipelines.
4. **"Existing portfolio" is a blind spot**: All tools either (a) build new portfolios from scratch or (b) analyze holdings at a data level. No tool takes an existing portfolio and produces a reasoned, prioritized "here's what to do next" plan in natural language.
5. **LLMs exhibit pre-trained biases**: LLMs tend toward tech stocks and large-caps from their training data — "raising questions about whether LLMs are genuinely understanding markets or merely memorizing patterns." [PM Research 2024](https://www.pm-research.com/content/iijpormgmt/51/2/211)

---

## Bucket 5 — Synthesized Gap Analysis

### Confirmed Gaps (with Evidence)

**Gap 1: No personalized, reasoned action plan for direct equity portfolios in India**
- Every Indian tool gives data or execution. None says: "For YOUR portfolio, here is what you should do today, ranked by priority, with the reasoning shown." This gap is confirmed by the INDmoney assessment ("stops short of giving personalized, regulation-backed advice"), the Screener/Tickertape product reviews (research tools, not decision tools), and the SEBI 2025 survey (comprehension gap, not data gap).
- *Evidence strength: High — confirmed by product audit across 16 platforms, no counterexample found.*

**Gap 2: TA + FA integrated reasoning is absent at the portfolio level**
- Investar and ChartAlert combine TA+FA screens for *stock discovery*. But no tool applies both lenses *simultaneously to existing holdings* and explains conflicts. The academic literature treats them as separate problems. This gap is particularly relevant for swing-to-long-term Indian retail investors whose decisions span both time horizons.
- *Evidence strength: High — Investar/ChartAlert confirmed as closest; neither offers portfolio-level synthesis or reasoning.*

**Gap 3: Bias correction is not explicitly framed as a product problem by any Indian tool**
- The academic literature (Frontiers 2024, Tandfonline 2025) confirms that behavioral bias reduction is the highest-leverage value of advisory systems. No Indian product explicitly frames their offering as "I will flag when you are exhibiting the disposition effect" or "this holding looks like loss-aversion anchoring."
- *Evidence strength: High — no Indian product found with explicit bias-correction framing. The nearest global product (PortfolioPilot) does partial portfolio-health checks but no behavioral diagnosis.*

**Gap 4: No LLM-native advisory product built specifically for Indian NSE equities**
- Commercial LLM-finance tools (Magnifi, Kavout, Composer, PortfolioPilot) are US-only. Indian tools (Tickertape, Screener.in, etc.) have no LLM reasoning layer for portfolio decisions. Jarvis Invest covers NSE/BSE but focuses on AI-generated stock picks (data layer), not reasoning over a user's existing portfolio.
- *Evidence strength: High — systematic product survey finds no counterexample. Jarvis Invest is the nearest but still operates at stock-recommendation level, not portfolio planning level. [StockGro/Jarvis reference](https://www.stockgro.club/stoxo/resources/top-free-ai-tools-for-the-indian-stock-market/)*

**Gap 5: The "systematic personal investment process" gap**
- SEBI 2025 + multiple academic papers confirm that retail investors lack a systematic personal process — they react to news, tips, and market moves. No Indian tool helps a user *define and then enforce* their own strategy (e.g., "only buy when RSI<35 AND ROE>15%"). Streak does this for algos; no one does it for the long-term investor's decision process.
- *Evidence strength: High — documented in SEBI survey, ISB study, and multiple behavioral papers. Streak covers the trading use case; long-term investor use case unserved.*

### Refuted "Gaps" (Already Solved)

**"Data access is a gap"** — REFUTED. Screener.in, Tickertape, Tijori, Trendlyne, StockEdge collectively give comprehensive fundamental and technical data for free or low cost. The data problem is solved. The *action* problem is not.

**"Algorithmic trading is inaccessible to retail"** — PARTIALLY REFUTED. Streak, Tradetron, AlgoTest give no-code algo tools to retail traders. The gap is for *advisory/planning* for non-algo long-term investors.

**"Portfolio tracking doesn't exist"** — REFUTED. Zerodha Console, INDmoney, MoneyControl, Tickertape all offer portfolio tracking. The gap is in portfolio *reasoning and recommendations*, not tracking.

**"No Indian robo-advisor exists"** — PARTIALLY REFUTED. Kuvera, INDmoney, ETMoney are functional robo-advisors for mutual funds. The gap is for *direct equity* portfolio advisory.

### Net-New Opportunity Space for Our Bot

The clearest unoccupied position, supported by evidence across all five buckets:

> **An AI planning assistant that takes an existing Indian NSE equity portfolio, applies the user's stated methodology (TA indicators + FA ratios + portfolio theory parameters), produces a prioritized action plan in natural language, flags behavioral anomalies in the current holdings, and outputs explicit reasoning for each recommendation — advisory-only, long-term + swing focus, NIFTY 500 universe.**

This framing:
- Does not compete with Screener.in / Tickertape (they give data; we give decisions)
- Does not compete with Streak / Tradetron (they do algo execution; we do planning)
- Does not compete with Kuvera / ETMoney (they do MF; we do direct equity)
- Does not replicate BloombergGPT / AlphaAgents (those are institutional and US-only)
- Is supported by SEBI's documented pain point: the problem is comprehension + action, not data
- Is supported by the academic literature's finding: the biggest value of advisory AI is behavioral-drag reduction
- Sits in the regulatory safe harbor: advisory-only, no compensation, self-use = no SEBI-RIA requirement

**The three product framings from the problem_statement.md that survive this research:**
- **Framing X (Bias-correction co-pilot)**: Strongly validated. No competitor. Highest documented ROI per academic literature.
- **Framing Z (Portfolio doctor)**: Validated. No Indian competitor. Closest global analog (PortfolioPilot) is US-only.
- **Framing Y (Strategy composer)**: Partially validated. Streak covers the algo subset. The long-term investor version is unserved.

*The combined X+Z framing — periodic portfolio health check with explicit behavioral diagnosis and prioritized action plan — represents the most defensible and highest-evidence opportunity.*

---

## Appendix — All Sources (Grouped)

### Pain Points (Bucket 1)
- [SEBI F&O Loss Study FY22–24 (Sept 2024)](https://www.sebi.gov.in/media-and-notifications/press-releases/sep-2024/updated-sebi-study-reveals-93-of-individual-traders-incurred-losses-in-equity-fando-between-fy22-and-fy24-aggregate-losses-exceed-1-8-lakh-crores-over-three-years_86906.html)
- [SEBI Investor Survey 2025 — Official](https://www.sebi.gov.in/reports-and-statistics/research/jan-2026/investor-survey-2025-_99170.html)
- [SEBI Investor Survey 2025 — Finnovate Analysis](https://www.finnovate.in/learn/blog/sebi-investor-survey-2025-insights)
- [SEBI Investor Survey 2025 — Key Takeaways, Lexology](https://www.lexology.com/library/detail.aspx?g=f7681a41-3d97-418e-a4ab-77bcdc93257d)
- [SEBI 2025: 63% Aware, 9.5% Invest (ScanX)](https://scanx.trade/stock-market-news/stocks/sebi-investor-survey-2025-63-households-aware-of-market-products-only-9-5-actually-invest/30475080)
- [SEBI "Elusive Retail Investor" DRG Study](https://www.sebi.gov.in/sebi_data/DRG_Study/elusiveretailinvestor.pdf)
- [ISB Study on Retail Investor Losses — Business Standard](https://www.business-standard.com/article/markets/retail-investors-tend-to-lose-in-stock-markets-says-isb-study-112120100043_1.html)
- [ISB Study — Moneylife coverage](https://www.moneylife.in/article/indian-retail-investors-tend-to-lose-in-stock-markets-isb/29947.html)
- [FY25 F&O Losses +41% — Moneylife](https://www.moneylife.in/article/91-percentage-of-retail-traders-lost-money-in-derivatives-losses-in-fo-surged-41-percentage-to-rs105-lakh-crore-in-fy2425-sebi-study/77613.html)
- [CFA Institute — India Derivatives & Retail Investors (Nov 2025)](https://blogs.cfainstitute.org/marketintegrity/2025/11/05/indias-derivatives-market-and-retail-investors/)
- [Disposition Effect at Market Level — India (ResearchGate)](https://www.researchgate.net/publication/336162840_Disposition_effect_at_the_market_level_evidence_from_Indian_stock_market)
- [Behavioral Biases & Investment Choices India 2024 (ResearchGate)](https://www.researchgate.net/publication/397113427_Behavioral_Biases_and_Investment_Choices_Understanding_the_Mediating_Role_of_Risk_Perception_among_Indian_Retail_Investors)
- [Behavioral Biases — PMC NIH study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12824484/)
- [SEBI Finfluencer / Info Gap Analysis (Whalesbook)](https://www.whalesbook.com/news/English/sebiexchange/Indias-Retail-Frenzy-Info-Gap-Fuels-Volatility-SEBI-Tackles-Finfluencers/699c8d82d83cd4ce4fe95e37)

### Existing Products (Bucket 2)
- [Screener.in](https://www.screener.in/)
- [Tickertape.in](https://www.tickertape.in/)
- [Tijori Finance Features](https://www.tijorifinance.com/features/)
- [Smallcase.com](https://www.smallcase.com/)
- [Zerodha Streak review](https://top10stockbroker.com/algo-trading-platform/zerodha-streak/)
- [Tradetron vs Streak](https://tradingtuitions.com/tradetron-vs-streak-which-is-a-better-algorithmic-trading-platform/)
- [Sensibull.com](https://sensibull.com/)
- [Trendlyne.com](https://trendlyne.com/)
- [Zerodha Console](https://zerodha.com/products/console/)
- [Zerodha Varsity](https://zerodha.com/varsity/)
- [StockEdge review](https://www.strike.money/reviews/trendlyne)
- [INDmoney gap analysis](https://invsify.com/blog/best-portfolio-optimization-software)
- [Kuvera Wikipedia](https://en.wikipedia.org/wiki/Kuvera.in)
- [India fintech overview 2026](https://www.winvesta.in/blog/investors/fundamental-analysis-tools-and-screeners-2026-guide)
- [Investar — TA+FA combined tool](https://investarindia.com/)
- [Jarvis Invest — AI stock picks India](https://www.stockgro.club/stoxo/resources/top-free-ai-tools-for-the-indian-stock-market/)

### Academic (Bucket 3)
- [Frontiers — Robo-Advisors through Behavioral Finance 2024](https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full)
- [Wiley — Evolution of Robo-Advisors 2025](https://onlinelibrary.wiley.com/doi/10.1111/ijcs.70131)
- [Tandfonline — Robo-advisors in Behavioural Finance 2025](https://www.tandfonline.com/doi/full/10.1080/23322039.2025.2571403)
- [ScienceDirect — Robo-Advisors Systematic Review 2024](https://www.sciencedirect.com/science/article/abs/pii/S1544612324001491)
- [Wiley — Indian Robo-Advisor Adoption 2025](https://onlinelibrary.wiley.com/doi/abs/10.1002/isd2.12346)
- [ResearchGate — Robo advisory & behavioral biases India (qualitative)](https://www.researchgate.net/publication/338957812_Robo_advisory_and_its_potential_in_addressing_the_behavioral_biases_of_investors_-_A_qualitative_study_in_Indian_context)
- [Wikipedia — Hierarchical Risk Parity](https://en.wikipedia.org/wiki/Hierarchical_Risk_Parity)
- [Hudson Thames — HRP Introduction](https://hudsonthames.org/an-introduction-to-the-hierarchical-risk-parity-algorithm/)
- [arXiv 2512.12922 — LLM Personalized Portfolio Recommender](https://arxiv.org/abs/2512.12922)
- [ACM ICAIF 2024 — Democratizing Alpha LLM Portfolio](https://dl.acm.org/doi/10.1145/3768292.3770376)
- [PM Research — LLMs for Financial and Investment Management 2024](https://www.pm-research.com/content/iijpormgmt/51/2/211)
- [IIMA — Indian Fama-French Momentum Data Library](https://faculty.iima.ac.in/iffm/Indian-Fama-French-Momentum/)
- [S&P Global — Factor Investing India](https://www.spglobal.com/spdji/en/documents/research/research-an-index-approach-to-factor-investing-in-india.pdf)

### LLM Agents (Bucket 4)
- [Bloomberg — BloombergGPT Press Release](https://www.bloomberg.com/company/press/bloomberggpt-50-billion-parameter-llm-tuned-finance/)
- [arXiv 2306.06031 — FinGPT Open-Source](https://arxiv.org/abs/2306.06031)
- [FinRL — Columbia Open Finance](https://openfin.engineering.columbia.edu/research-projects/financial-reinforcement-learning-finrl)
- [arXiv 2508.11152 — AlphaAgents (BlackRock)](https://arxiv.org/abs/2508.11152)
- [MarkTechPost — AlphaAgents Introduction](https://www.marktechpost.com/2025/08/19/blackrock-introduces-alphaagents-advancing-equity-portfolio-construction-with-multi-agent-llm-collaboration/)
- [Magnifi / TIFIN — $2B Asset Intelligence](https://tifin.com/news/magnifi-now-providing-ai-powered-investment-intelligence-on-over-2b-of-linked-self-directed-assets/)
- [Composer — Trade With AI (BusinessWire 2025)](https://www.businesswire.com/news/home/20251021050436/en/Composer-Supercharges-Investing-Platform-with-New-Trade-With-AI-Tool)
- [Kavout — AI Tool Curator Review 2026](https://www.aitoolcurator.com/ai-tools/finance-investing/kavout/)
- [Numerai — Gate Learn Explainer](https://www.gate.com/learn/articles/what-is-numerai/742)
- [PortfolioPilot.com](https://portfoliopilot.com/)
- [arXiv 2411.11059 — Financial News LLM RL](https://arxiv.org/html/2411.11059v1)
- [arXiv 2504.14345 — LLM-Enhanced Black-Litterman](https://arxiv.org/html/2504.14345v2)
