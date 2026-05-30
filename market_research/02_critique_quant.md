# 02 — Critique: Quant/Algo Trader Lens

**Status**: First draft
**Date**: 2026-05-30
**Author perspective**: Ex-systematic trader, NSE F&O + cash book

---

## TL;DR (5 bullets)

- The research documents *why* retail investors lose money but doesn't ask *whether an LLM-advisory layer can fix that*, which is the only question that matters for product viability.
- "Combining TA and FA" has no credible peer-reviewed evidence of producing alpha net of costs. It's a story investors tell themselves. The research cites none.
- The entire framing assumes signal quality is the bottleneck. It isn't. Position sizing, cost management, and behavioral consistency are. The bot is solving the wrong constraint.
- Indian market microstructure — F&O dominance over 84% of global equity options volume, operator manipulation in mid/small caps, circuit-locked stocks — renders every US/EU-derived academic reference suspect without explicit India-market validation.
- An advisory tool whose success metric is "better returns" but whose output is unverifiable natural-language text is not a quant tool. It is a journaling app with delusions of alpha.

---

## Where the research is right

The SEBI data is solid. 93% of F&O traders losing money is documented fact, not hand-waving. The behavioral finance literature on the disposition effect is real and the finding that Indian retail investors exhibit a *larger* disposition effect than US/Japan/China peers is legitimately interesting. The product audit is thorough — the "action gap" framing (data tools exist, no reasoning-to-decision tool exists) is the one genuine market observation the research makes that holds up under scrutiny. The regulatory safe harbor analysis (E1, advisory-only = no RIA registration) is correct and useful. These deserve credit.

---

## Where the research is wrong / naive

### 1. No evidence that TA + FA combo produces alpha — anywhere

The research confidently claims "the TA+FA integration gap is real" and treats this as a *product* gap. It is not. The academic literature does not support the premise that combining technical and fundamental signals generates exploitable alpha net of transaction costs.

The meta-review by Park and Irwin (ResearchGate) found that while TA rules showed *gross* profitability through the early 1990s, this disappeared in data-snooped, out-of-sample tests once data-mining bias was corrected. In efficient-enough markets — and NSE's NIFTY 500 large-cap universe is reasonably efficient by emerging-market standards — the marginal signal from a 14-period RSI or a 200-day moving average has been arbitraged away by HFT and quant funds who got there years earlier.

The research never asks: *what is the published out-of-sample Sharpe of any TA+FA combined strategy on NSE stocks?* Because the answer, based on available evidence, is: nobody knows, and the prior is negative. Citing that "no Indian tool synthesizes TA and FA at the portfolio level" is not evidence of alpha — it may simply mean nobody built it because it doesn't work.

**Evidence you should have cited**: Fama (1991) "Efficient Capital Markets II", Journal of Finance. Sullivan, Timmermann & White (1999) "Data-Snooping, Technical Trading Rule Performance, and the Bootstrap", Journal of Finance — found that TA profitability vanishes once the multiple-testing correction is applied.

### 2. Backtesting is mentioned nowhere. This is disqualifying.

The research reviews six portfolio optimization frameworks (Markowitz, Black-Litterman, HRP, etc.) and multiple LLM papers. Not one of them is evaluated for *out-of-sample performance on NSE data*. Not one mentions:
- Survivorship bias (the NIFTY 500 today is not the NIFTY 500 five years ago — companies get added after they succeed)
- Look-ahead bias (any signal computed on data that wasn't available at trade time invalidates the backtest)
- Multiple-testing bias (if you test 100 TA+FA combinations and report the best five, you've p-hacked your way to an illusion of alpha)
- Walk-forward validation (minimum viable methodology for any claimed trading edge)

Lopez de Prado (2018, "Advances in Financial Machine Learning") shows empirically that the more backtests a quant runs on a strategy, the larger the discrepancy between in-sample and out-of-sample performance. A 2024 ScienceDirect paper on backtest overfitting in the ML era found over 90% of academically published strategies fail when implemented with real capital. The research doesn't even raise these concerns, let alone address them. This is not a minor omission — it is the central question for any strategy system.

### 3. Indian market microstructure invalidates most cited academic work

Every LLM paper cited — AlphaAgents (BlackRock), "Democratizing Alpha" (ACM), FinGPT, arXiv 2512.12922 — is trained and tested on S&P 500 or NASDAQ data. Every portfolio optimization framework in the research comes from US/European market design. None is validated on NSE.

Why does this matter? NSE's microstructure is categorically different:

- **F&O dominates**: Over 84% of all equity options traded globally in Q1 2024 were on Indian exchanges (FIA, 2024). The cash equity market is a rounding error on most days. In this environment, informed order flow in options reveals itself *before* it shows up in cash prices. A TA-on-cash-prices system is reading the shadow, not the object.
- **Retail is dumb-money signal**: One-third of NSE index options turnover is retail. This is a well-documented contrarian signal — retail option positioning is frequently a fade, not a follow. The "action gap" the research identifies may simply be that retail should be doing *less*, not getting a personalized action plan that lets them trade more with confidence.
- **Mid/small cap operator dynamics**: A significant portion of the NIFTY 500's lower tier features stocks with low float, controlled by market operators who run pump-and-dump cycles. RSI and MACD on these stocks are not measuring momentum — they are measuring the operator's execution schedule. Feeding these signals into an LLM advisory system produces confident-sounding garbage.
- **Circuit breakers create selection bias**: Stocks that hit lower circuits are frozen, creating artificial gaps in price series. Any TA system trained or evaluated on NSE data without accounting for circuit events has look-ahead contamination in its results.

### 4. LLM-as-strategy fails the most basic quant test

The research cites a PM Research 2024 finding that "LLMs tend toward tech stocks and large-caps from training data — raising questions about whether LLMs are genuinely understanding markets or merely memorizing patterns." It cites this as a *minor note*. It should be the central problem.

An LLM cannot price a stock. Full stop. Pricing requires a discount rate, a terminal growth assumption, a probability distribution over scenarios, and a current market-clearing price as the null hypothesis. An LLM produces token sequences that are statistically likely given its training data. These are architecturally different operations. The research paper on LLM stock prediction (SSRN 4947135) found LLMs predicted directional movement correctly 51.6–65.6% of the time on S&P 500 — barely above the coin flip that a random walk null implies.

More specifically: an LLM given RSI=72, P/E=32, ROE=18% and asked "should I trim this position" is not *computing* an answer — it is *retrieving* patterns from training text in which similar numbers appeared alongside trading recommendations. If those recommendations were from FinTwitter and finfluencer blogs (which is almost certainly what's in the pretraining corpus for any general-purpose LLM), then the bot is systematizing the exact finfluencer-dependency SEBI identifies as the core behavioral problem. The proposed solution *is* the diagnosed disease.

Where the LLM-as-strategy argument is *weakest*: as a natural language interface to structured quant signals. If a Python function computes RSI and P/E correctly and the LLM only translates those outputs into plain-text reasoning, the LLM's inability to price stocks is irrelevant. But this is architecturally closer to a reporting layer than a strategy layer, and the research conflates the two.

### 5. "Better returns" is misdirected when the base rate is negative alpha

The research correctly notes (Section 4b of the problem statement) that "better returns" may be a trap. Then it doesn't follow through on the implication. Here it is in full:

Individual retail investors earn negative alpha of 4–4.4% per year *before* costs on NSE/global markets (PMC/NCBI study 2021 on emerging market retail performance). After costs, this figure worsens. William Sharpe's 1991 arithmetic is precise: active management is zero-sum before costs and negative-sum after costs. This means the expected value of the bot's recommendations is *negative* — not zero, negative — unless the bot's signal quality exceeds the costs it induces.

The research does not compute a breakeven signal quality. It should. If a TA-driven strategy on NIFTY 500 stocks requires ~50bps edge per trade (after STT at 0.1%, brokerage, exchange charges, GST, slippage, and capital gains tax) to break even, that number needs to appear in the problem statement as the minimum bar the system must clear before a single line of code is written.

### 6. Position sizing is mentioned once, in passing, in the framework table

The research lists HRP and Markowitz in a table and notes they produce *weights*. It doesn't engage with the fundamental finding of betting theory: sizing dominates signal quality in long-run compound returns.

Two traders with identical signals but different position sizing will have compound wealth trajectories that diverge exponentially. At full Kelly, a 55% win-rate coin-flip doubles capital faster than a 70% win-rate bet sized at 1% of capital. The reverse is also true: a 70% win-rate strategy sized at 2x Kelly goes to zero almost surely due to the geometric mean penalty.

For retail investors with concentrated NSE equity portfolios — frequently 8–12 stocks, often with 20–40% of the book in one or two high-conviction names — the sizing problem is far more consequential than the signal problem. The bot as proposed will give a buy/trim/sell action plan but nothing on how large the position should be relative to conviction, volatility, and portfolio correlation. This is the single most leverage-able improvement the bot could make, and the research barely touches it.

### 7. Transaction cost stack is not modeled

The research does not compute what the cost stack means for strategy viability. Here it is:

For a delivery trade (hold >1 day) on NSE:
- STT: 0.1% on buy + 0.1% on sell = 0.2% round-trip
- Brokerage (Zerodha flat fee ~₹20 per order): ~0.05–0.2% for sub-₹40,000 positions
- NSE exchange charges: ₹3.25/lakh (~0.003%)
- SEBI turnover fee: ₹15/crore
- GST on brokerage + charges: 18%
- Stamp duty: 0.015% on buy
- Slippage on mid/small cap: 0.1–0.5% round-trip depending on float
- STCG tax (if held <12 months): 20% on gains (post-Budget 2024)
- LTCG tax (if held >12 months): 12.5% above ₹1.25 lakh annual exemption

Conservative total round-trip cost for a mid-cap delivery trade: **0.5–1.2%**. For a strategy that generates 8–10 signals per month, this is 50–120% per year in gross return drag before alpha. The research says nothing about this.

---

## What's missing entirely

1. **A null hypothesis for the bot's alpha**: The problem statement proposes to "get better returns." Against what benchmark, at what confidence level, over what time period? Without this, the product cannot be evaluated and cannot fail — which means it also cannot succeed.

2. **The correlation structure of TA signals on NSE**: RSI, MACD, Bollinger Bands, and moving crossovers on the same stock are not four independent signals. They are highly correlated nonlinear transforms of the same price series. Treating them as independent inputs to an LLM produces false confidence in the output. Nobody in the research mentions this.

3. **Regime-dependence**: TA signals that "work" in trending markets fail in mean-reverting markets, and vice versa. The NIFTY 500 has gone through at minimum three structurally distinct regimes in the last decade (2017 bull, 2020 COVID crash, 2021–22 F&O retail frenzy, 2024 smallcap correction). Any strategy evaluation that doesn't partition by regime is averaging over non-stationary data.

4. **The counterfactual**: If the bot's advice is to hold 60% of the time, buy 25%, and sell 15%, does that beat a simple low-churn buy-and-hold of the NIFTY 50 ETF? The research assumes the bot will beat the naive benchmark. This needs to be established, not assumed.

5. **Hallucination risk in high-stakes output**: The research notes LLMs "tend toward large caps from training data" but doesn't model the failure mode. An LLM confidently recommending a trim on HDFC Bank two days before a positive earnings surprise, based on RSI=68 and a "technically extended" read, is not a behavioral bias corrector — it is a liability. The research has no error budget for this.

6. **What "advisory-only" means in practice**: If the bot says "trim 30% of your Adani Ports position" and the user does it and loses money, there is no contractual protection if the tool is positioned as an advisory product. The research mentions SEBI's RIA registration concern but doesn't model the product liability exposure.

---

## Implications for the problem statement

If the user takes this critique seriously, the problem statement must change as follows:

1. **Delete "better returns" as a goal**. Replace with: "reduce behavioral errors (disposition effect, overconcentration, panic selling) documented in the user's own trade history." This is measurable, the causal mechanism is established in the literature, and the bot's success does not depend on alpha generation.

2. **Add a mandatory cost-adjusted breakeven analysis** before any signal evaluation. Every proposed signal must pass a hurdle of >50bps edge per trade *before* it enters the strategy.

3. **Restrict the universe to NIFTY 100 for v1**. Large-cap, liquid stocks only. Mid/small cap NSE is too manipulated and too thinly traded for TA signals to be reliable. Solve for the tractable case first.

4. **Define LLM's role precisely**: Natural language interface to Python-computed quant signals. Not a reasoning engine over raw price and fundamental data. The LLM translates outputs, it doesn't generate them.

5. **Add position sizing as a first-class output**. The bot must output recommended position size as a percentage of portfolio, not just direction. Half-Kelly is the sensible default. Without this, the action plan is incomplete.

6. **Add a backtest validation requirement** to the problem statement. Before the bot makes its first recommendation on live data, at least one strategy variant must pass a walk-forward test on 5 years of NSE data with out-of-sample Sharpe > 0.5 after costs.

---

## Specific questions the user must answer before proceeding

1. **What is your current portfolio's Sharpe ratio vs. NIFTY 50, for the last 3 years, after all costs and taxes?** If you don't know this number, you don't have a baseline, and you can't measure improvement.

2. **How many signals per month do you expect the bot to generate, and have you computed the round-trip cost drag at that signal frequency?** If the answer is "I don't know," the cost question has not been taken seriously.

3. **Can you name one peer-reviewed paper that demonstrates TA + FA combined generates positive alpha on NSE stocks, out-of-sample, after costs?** If no, why is TA+FA the methodology?

4. **What is the plan if the bot gives a confident recommendation and it loses money?** Is this a personal tool with no accountability, or a product? The answer changes the architecture.

5. **Have you defined "behavioral bias correction" as a separately measurable outcome, distinct from return improvement?** If not, you have no way to evaluate the bot's core claimed value (per the academic literature cited in your own research).

6. **What position sizing rule do you currently use?** If the answer is "gut feel" or "equal weight," the bot's highest-leverage intervention is sizing, not signal, and the problem statement should reflect that.

7. **Which NSE stocks in the NIFTY 500 do you consider operator-driven or low-float?** Any answer short of "I have a defined exclusion list" means the bot's signal universe contains stocks where TA is noise by construction.

---

## Sources I'd add to the research

- [Sullivan, Timmermann & White (1999) — Data-Snooping, Technical Trading Rule Performance, Bootstrap](https://onlinelibrary.wiley.com/doi/10.1111/1540-6261.00163) — definitive paper showing TA profitability evaporates under multiple-testing correction.
- [Lopez de Prado (2018) — Advances in Financial Machine Learning (overview)](https://www.wiley.com/en-us/Advances+in+Financial+Machine+Learning-p-9781119482086) — on backtest overfitting, combinatorial purged cross-validation, and why most backtests are false.
- [Bailey, Borwein, Lopez de Prado & Zhu (2014) — The Probability of Backtest Overfitting](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2326400) — quantifies the probability that a strategy's backtest Sharpe is inflated by data mining.
- [Fama (1991) — Efficient Capital Markets II, Journal of Finance](https://onlinelibrary.wiley.com/doi/10.1111/j.1540-6261.1991.tb04636.x) — the canonical statement of weak/semi-strong form efficiency and what it implies for TA and FA.
- [Barber & Odean (2000) — Trading Is Hazardous to Your Wealth](https://faculty.haas.berkeley.edu/odean/papers%20current%20versions/individual_investor_performance_final.pdf) — retail investors who trade more earn less; the activity the bot might encourage is already known to destroy returns.
- [FIA (2024) — Meteoric Rise in India's Equity Derivatives Volume](https://www.fia.org/marketvoice/articles/explainer-meteoric-rise-indias-equity-derivatives-volume) — F&O structural dominance; why cash equity TA is reading the wrong market.
- [SSRN 4947135 — Efficacy of LLMs in Predicting Stock Prices](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4947135) — LLMs predict directional movement 51.6–65.6%, barely above coin flip.
- [arXiv 2505.07078 — Can LLM-based Investing Strategies Outperform in the Long Run?](https://arxiv.org/html/2505.07078v3) — buy-and-hold consistently ranks among top performers vs. LLM strategies over longer horizons; short-period LLM outperformance is unstable.
- [ScienceDirect (2024) — Backtest Overfitting in the ML Era](https://www.sciencedirect.com/science/article/abs/pii/S0950705124011110) — 90%+ of published ML trading strategies fail out-of-sample.
- [Bajaj Finserv — STT Rates India 2026](https://www.bajajfinserv.in/securities-transaction-tax) — current cost stack reference.
