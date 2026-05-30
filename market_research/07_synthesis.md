# 07 — Synthesis: Problem Statement, Phase 1 Closeout

**Status**: Final
**Date**: 2026-05-30
**Phase 1 verdict**: Problem statement partially locked — critical-path questions remain. See Section 10.

---

## 1. Executive Summary (read this in 2 minutes)

- **What we did**: One round of market research (5 buckets, 16 products audited, 30+ papers/sources) followed by five parallel critiques across distinct lenses (quant, regulatory, behavioral, product, retail persona), then this synthesis.
- **What we found**: The "action gap" is real and documented — no Indian tool produces a personalized, reasoned action plan for a direct equity portfolio. The primary bottleneck for retail investors is not data, not execution, but comprehension-to-decision. Behavioral bias (especially the disposition effect) is the highest-leverage problem, not alpha generation.
- **What the critiques changed**: v0.1 framed the bot as an alpha-generator with "benchmark-beating returns" as the success metric. That framing is wrong. All five critiques, from different angles, say the same thing: the bot's primary value is behavioral correction and discipline enforcement, not stock-picking intelligence. The success metric should be behavioral, not return-based.
- **Biggest unresolved tension**: Quant says "TA+FA has no peer-reviewed alpha evidence; don't promise it." Retail user says "I just want you to tell me when I'm doing something stupid." These are not contradictory — they resolve to the same product (behavioral accountability), but the quant's additional requirements (backtesting, cost modeling, position sizing) need to be designed into the architecture from day one.
- **Regulatory verdict**: Advisory-only, self-use, no compensation = clean regulatory footing today. The moment you share output with anyone else or charge a rupee, the entire compliance stack activates. This is a hard constraint, not a design preference.
- **What's decided**: Axis E1 (advisory-only) is locked. Start with Axis A1 (Pranav-only). Bias correction + portfolio discipline are the core value proposition. "Benchmark-beating returns" is removed as a primary success metric.
- **What's still open**: The 3 critical-path questions in Section 10 must be answered before Phase 2 begins.

---

## 2. What we did

Phase 1 consisted of one structured research pass and five parallel critique passes. The research document (01_research.md) covered five buckets: Indian retail investor pain points, existing Indian products and their problem framings, academic and industry literature, the LLM-finance agent landscape, and a synthesized gap analysis. Five specialist agents then each critiqued that research document from a different vantage point: (1) a quant/algo trader concerned with signal quality, backtesting, and cost modeling; (2) a SEBI/regulatory expert concerned with registration triggers, data licensing, and the incoming AI/ML framework; (3) a behavioral finance researcher in the Kahneman/Thaler tradition, focused on whether advisory tools actually correct bias or amplify it; (4) a product/PMF analyst focused on market sizing, distribution moats, and competitive dynamics; and (5) a skeptical retail investor persona (38-year-old Bangalore IT professional, ₹15L portfolio, 25 stocks, burned by tip services). This synthesis closes Phase 1.

---

## 3. What the research found (the 5 strongest signals)

1. **The loss crisis is severe and behavioral in origin.** 93% of individual F&O traders lost money (FY22–24), aggregate losses ₹1.8 lakh crore. Indian retail investors exhibit a *larger* disposition effect than US, Japanese, Chinese, and Finnish peers — holding losers too long and booking winners too fast at an 85% rate. [SEBI FY24 Press Release; ISB/NSE study, Moneylife]

2. **The action gap is the genuine white space.** Sixteen Indian products were audited. Every one provides data, execution, or education. None takes a user's existing portfolio and outputs "here is what you should do next, ranked by urgency, with reasoning." [Product audit across Screener.in, Tickertape, Zerodha Console, Smallcase, et al.]

3. **The comprehension gap, not the data gap, is the documented bottleneck.** SEBI explicitly finds that "information asymmetry in Indian markets stems from comprehension gaps, not just availability." 62% of active retail investors follow finfluencers not because they lack data, but because they lack a process for acting on data. [SEBI Investor Survey 2025; Forrester 2024]

4. **Behavioral bias reduction is the highest-leverage value of advisory AI — not alpha generation.** The academic consensus (Frontiers 2024, Tandfonline 2025, Capponi et al. Management Science 2022) is that the biggest value of advisory systems is counteracting panic selling, disposition effect, and herding — not picking winning stocks. Even fully-automated robo-advisors only *reduce, not eliminate* these biases. [Tandfonline 2025; Frontiers 2024]

5. **Every LLM-finance product is US-market-first and institutionally-focused.** BloombergGPT, AlphaAgents (BlackRock), Magnifi, Composer, Kavout — all US-only. No consumer-quality LLM product with Indian NSE equity first-framing exists. This is a gap, but also a window that is closing: Groww MCP and Zerodha MCP integrations already exist as of 2025–26. [Product survey; Groww MCP, Zerodha MCP documentation]

---

## 4. Where the critiques pushed back — the debate

### 4.1 — Quant/Algo Lens

**Strongest point**: TA+FA combination has no peer-reviewed evidence of alpha generation on NSE equities out-of-sample after costs. The gap may exist because it doesn't work, not because nobody built it.

**Counter to research v0.1**: The research frames "no Indian tool synthesizes TA+FA at portfolio level" as a product gap implying alpha opportunity. This conflates market gap with signal quality. The Sullivan-Timmermann-White (1999) finding that TA profitability vanishes under multiple-testing correction, and the SSRN 4947135 finding that LLMs predict directional movement at 51.6–65.6% (barely above coin flip), undercut the premise.

**Implication if true**: The bot cannot be framed as an alpha-generation system. It must either prove signal quality first (walk-forward backtest, cost-adjusted, NSE-specific data), or drop alpha claims entirely and reframe as a behavioral discipline tool. The round-trip transaction cost stack (0.5–1.2% for mid-cap delivery trades) sets a breakeven hurdle that every proposed signal must clear before entering the system.

**Verdict**: **ACCEPT** — The alpha-generation framing in v0.1 is unsupported and should be removed. The quant's requirements (position sizing as a first-class output, explicit cost modeling, LLM as reporting layer over Python-computed signals — not as a strategy engine) are architecturally correct and must be incorporated.

---

### 4.2 — Regulatory Lens

**Strongest point**: "Advisory-only, self-use = regulatory safe harbor" is correct but incomplete. The safe harbor has four invisible edges: (a) data licensing (yfinance is legally ambiguous for products), (b) the RA regulations which apply to publication of research in some readings, (c) the DPDP Act 2023 (rules effective ~May 2027) classifying portfolio data as personal data, and (d) SEBI's forthcoming AI/ML framework (June 2025 consultation paper) imposing model governance, explainability, and 5-year documentation on any AI advisory tool interacting with clients.

**Counter to research v0.1**: The research (01_research.md, Bucket 5) states "sits in the regulatory safe harbor: advisory-only, no compensation, self-use = no SEBI-RIA requirement" as if settled. The regulatory critique shows this is settled only for Axis A1 and only today. A2 (friends/family) immediately reopens the IA Regulations' "consideration" question; E2 (semi-auto orders) is treated as "algo" by SEBI's February 2025 circular; and any productization path requires a commercial NSE data license (₹5–50L/year for commercial vendors).

**Implication if true**: Axis A must be locked at A1 (Pranav only) with explicit legal language. E2 and E3 should be removed from Phase 1 framing entirely. Output language matters legally: "Your RSI is 72 and historically this has preceded corrections" is analysis; "Sell 30% of your HDFC Bank" is advice. The distinction is the Avadhut Sathe enforcement line.

**Verdict**: **ACCEPT** — The regulatory critique adds precision without contradicting the core premise. Its recommendations (A1 lock, E1 only, analysis framing vs. advice framing, yfinance for prototype only) are actionable constraints that must enter the problem statement.

---

### 4.3 — Behavioral Finance Lens

**Strongest point**: Knowing about a bias and correcting for it are neurologically different. Kahneman spent fifty years studying cognitive biases and remained unable to avoid them. A bot that explains the disposition effect is not the same as a bot that removes it. The research correctly identifies bias as the core problem but then proposes a product (ranked action lists, visible entry prices, frequent review cycles) whose design choices actively reinforce anchoring, action bias, and confirmation-seeking.

**Counter to research v0.1**: The v0.1 framing of "prioritized action plan covering hold/buy/trim/sell decisions" is an action-inducing artifact. Barber and Odean (2000) showed that tools which make active investing feel more structured increase trading frequency, which destroys returns for the majority. The research cites the Tandfonline 2025 finding that fully automated robo-advisors only partially reduce the disposition effect — but then proposes an advisory-only tool that by design gives users more discretion. An advisory bot will do less bias correction than a fully automated one, not more.

**Implication if true**: The primary product output should be a *reduction in impulsive action*, not an increase in deliberate action. Concretely: hide entry price by default; force a written rationale before any sell recommendation is generated; introduce mandatory cooling periods during high-volatility sessions; make "no action warranted" the most common output; include adversarial prompting (auto-generate the steelman sell case for any position the user wants to hold, regardless of framing).

**Verdict**: **ACCEPT** — The behavioral critique's design principles are the most actionable inputs to Phase 2 architecture. The success metric must include "avoided impulsive actions" as a primary axis alongside return metrics (Axis G must expand).

---

### 4.4 — Product/PMF Lens

**Strongest point**: This is likely a feature, not a product. Groww MCP and Zerodha MCP already exist. Every major broker can ship "ask your portfolio anything" as a tab in their app in one sprint. The TA+FA synthesis layer is a weekend engineering project for a competent ML team at a broker with live portfolio data, not a defensible moat.

**Counter to research v0.1**: The research correctly identifies the action gap but does not ask whether a standalone product can reach distribution at scale before incumbents close the gap. The real SAM for a paying Indian AI portfolio bot is 5–10 lakh users, not 13.6 crore registered investors. At ₹499/month and 5% monthly churn, this is a ₹37–60 crore ARR ceiling — a lifestyle business or acqui-hire target, not a venture-scale outcome.

**Implication if true**: The "build for myself first, then PMF" path is disciplined only if gated milestones force the transition. The product PM critique's steelman — a behavioral accountability partner distributed B2B2C through SEBI-registered RIAs, not direct to retail — is the version with defensible economics. RIA-as-distribution also resolves the regulatory moat problem (RIAs can legally charge for personalized advice, which a standalone subscription cannot).

**Verdict**: **PARTIAL** — The critique is correct that standalone consumer distribution is fragile and incumbents are closing the gap. However, this matters primarily if Pranav's goal is a scalable product; if the goal is a personal tool first, the moat question is premature. The critique's discipline-tool framing (bot enforces the user's own stated rules rather than generating alpha) is the correct reframing regardless of business model.

---

### 4.5 — Retail Investor Persona

**Strongest point**: The product as proposed is built for someone who already has a coherent investment methodology and wants to automate its application. That is the top 15% of Indian retail investors — not the majority who cannot articulate their strategy. The persona also surfaces three pain points absent from the research: the "deploy fresh monthly salary" problem, the exit-rule problem (everyone teaches entry; nobody teaches exit), and the LTCG tax optimization problem (₹30,000–60,000/year opportunity for a 8-year investor with significant gains).

**Counter to research v0.1**: v0.1's Framing Y (Strategy Composer) assumes the user can encode their strategy in RSI/FA parameters. The retail persona cannot. Framing Z (Portfolio Doctor) is the right entry point — diagnosis before prescription. The persona would not configure the bot; they need the bot to discover their de facto strategy from their portfolio and surfacing violations of it.

**Implication if true**: Onboarding should be methodology-agnostic: "describe your investing in plain language and let the bot tell you what methodology you're actually using." Exit rules and LTCG tax awareness should be in v1, not deferred. Trust-building requires a "past recommendations and outcomes" log from day one — not retrofitted. The Kite API integration (not manual CSV entry) is the minimum viable activation path.

**Verdict**: **ACCEPT** — The three unaddressed pain points (fresh capital deployment, exit rules, tax optimization) are genuine gaps in the v0.1 scope. The persona's trust-building requirements (visible reasoning, track record log, "why I was wrong" explanations) are product design constraints that must enter the architecture.

---

## 5. Points of agreement across all five critiques

These are the highest-confidence findings — all five lenses converge:

1. **Behavioral bias correction, not alpha generation, is the core value proposition.** The quant says "alpha evidence is thin"; the behavioral researcher says "awareness doesn't fix bias"; the PM says "the discipline tool is what's defensible"; the retail persona says "tell me when I'm doing something stupid." All five are saying the same thing from different angles.

2. **Advisory-only (E1) is the correct automation level.** The regulatory critique says it's the only clean legal path. The behavioral critique says friction at execution is *behaviorally beneficial*. The retail persona says they *want* to retain control. All three independently arrive at E1.

3. **The action gap is real and currently unoccupied.** All five critiques accept the product audit finding that no Indian tool produces a personalized, reasoned action plan for a direct equity portfolio. The disagreement is about what kind of plan is valuable — not whether the gap exists.

4. **"Better returns" is the wrong primary success metric.** The quant cites Sharpe arithmetic; the behavioral researcher cites the action-frequency literature; the PM cites unverifiability in any 90-day window; the retail persona says "I don't need the bot to be right every time, I need it to be honest." All five say the metric must be behavioral or process-based, not return-based, at least for v1.

5. **LLM as reporting/reasoning layer over Python-computed signals, not as strategy engine.** The quant makes this the explicit architectural requirement. The behavioral researcher flags the fluency-as-false-authority risk. The PM flags that LLMs alone are not a moat. The retail persona says "show me the reasoning, not the label." All four independently argue for the same architecture: Python computes signals correctly; LLM explains and contextualizes them.

---

## 6. Points of disagreement across critiques

| Disagreement | Quant position | Behavioral position | Retail persona position | Proposed resolution |
|---|---|---|---|---|
| **Should the bot generate action recommendations at all?** | Only if backed by walk-forward backtested signals with positive cost-adjusted Sharpe | No — the primary output should be inaction framing and behavioral flags, not action plans | Yes, but anchored to the user's own stated rules, not the bot's opinion | Resolve toward a hybrid: bot generates a prioritized watchlist of "positions to review," not direct buy/sell orders. Behavioral flags are the primary output; action recommendations are secondary and always tied to the user's pre-stated rules. |
| **TA signals: use or reject?** | Use only after NSE-specific, out-of-sample, cost-adjusted validation; restrict to NIFTY 100 liquid names | Irrelevant to the behavioral case; TA signals may increase action bias regardless of accuracy | Useful for timing the exit/entry on positions I already fundamentally believe in | Resolve by treating TA as one contextual signal among several, never as the primary recommendation driver. Restrict to NIFTY 100 for v1. Add explicit signal confidence levels. |
| **Scope: Pranav-only or retail product?** | Irrelevant to the quant; focus on the math | Retail product distribution = herding risk at scale; be aware | Build for me first; don't make it generic until you know it works | Resolve per the regulatory and product critiques: A1 (Pranav-only) for Phase 1 with explicit 3-month gating milestone before any multi-user path is evaluated. |
| **Tax awareness (D5): v1 or later?** | Not in quant scope | Irrelevant to behavioral argument | High-priority v1 feature; ₹30K–60K/year real money | Resolve toward including a basic LTCG/STCG calculator in v1 given the retail persona's strong signal and the fact it has no behavioral downside risk. |

---

## 7. Refined Problem Statement (v0.2)

For an Indian retail investor (initially Pranav himself) holding a portfolio of NSE-listed equities, build an AI planning assistant that **ingests the portfolio via Kite API or CSV and produces a weekly structured portfolio health report** — identifying positions whose technical, fundamental, and behavioral signals suggest review, flagging likely cognitive biases in the user's current holdings (disposition effect, anchoring, concentration risk, exit-rule violations), and **presenting the reasoning transparently so the user can evaluate and decide**. *The bot's primary output is behavioral accountability and discipline enforcement against the user's own stated rules — not alpha generation.* The user's strategy (which indicators, which fundamental thresholds, which risk parameters) is elicited through plain-language onboarding, not parameter configuration. *The LLM operates as a reasoning and explanation layer over Python-computed signals; it does not generate signals itself.* NIFTY 500 universe (restricting to NIFTY 100 for TA signals in v1). Long-term + swing horizon. Advisory-only, manual execution (E1). *The primary success metric in v1 is behavioral: stop-loss adherence rate, reduction in anchored loss-holders, recommendation-to-review engagement rate — not benchmark-relative return.* Phase 1 deliverable is the planner for Pranav's own portfolio; productization path evaluated at a defined milestone gate, not assumed.

**What changed from v0.1 (marked in italics above):**
- "Benchmark-beating, risk-adjusted returns" removed as primary goal; behavioral metrics substituted
- "User supplies methodology preferences" replaced with plain-language onboarding that infers methodology
- LLM architectural role made explicit: reasoning layer over Python signals, not strategy engine
- NIFTY 100 restriction for TA signals added (v1 only) per quant critique
- Phase 1 = Pranav-only made explicit with a milestone gate before multi-user
- Kite API integration named as activation path
- Tax-awareness scope expanded from "defer to v2" to "basic LTCG/STCG calculation in v1"

---

## 8. The 7 axes — recommendation after critique

| Axis | v0.1 recommendation | v0.2 recommendation after critique | Why changed |
|---|---|---|---|
| **A — User scope** | A1 → A3 path (start A1) | **A1 only, hard-locked for Phase 1.** Explicit milestone gate (3-month, Sean Ellis test) before evaluating A2/A3. | Regulatory: A2 opens IA Regulations' "consideration" question immediately. Product: false PMF risk from solo-user validation. |
| **B — Time horizon** | B1 + B2 (long-term + swing) | **B1 + B2, unchanged.** | All five critiques accept this. No disagreement. |
| **C — Asset universe** | C2 (NIFTY 500) | **C2 for fundamentals; C1 (NIFTY 100) for TA signals in v1.** Expand TA universe to C2 in v2 after NSE-specific validation. | Quant: mid/small cap NSE has operator dynamics that make TA signals unreliable; large-cap is the tractable case. |
| **D — Decision scope** | D1+D3+D4; defer D2 and D5 | **D1+D3+D4 unchanged; D5 (LTCG/STCG basic) added to v1; D2 (new entry ideas) deferred to v2.** | Retail persona: tax-awareness is a ₹30K–60K/year real pain point. Exit rules (D1) are more urgent than entry ideas (D2). |
| **E — Automation** | E1 (advisory only) | **E1 only. E2 and E3 removed from Phase 1 framing.** | Regulatory: E2 is treated as algo by SEBI's Feb 2025 circular. Behavioral: advisory friction is beneficial. All five lenses agree. |
| **F — Math/methodology** | F1–F5 exposed; F6/F7 optional | **F1 (TA) and F2 (FA ratios) are primary. F4 (portfolio theory: HRP for weighting, position sizing via half-Kelly) added as first-class output. F3/F5/F6 deferred to v2. F7 (LLM) scoped as reasoning layer only, not signal source.** | Quant: position sizing is more leverage-able than signal quality; LLM architectural role must be explicit; cost-adjusted breakeven analysis required before any signal enters the system. |
| **G — Success metric** | G5 (composite: alpha + Sharpe + drawdown) | **G5 retained as secondary; primary metric is behavioral: stop-loss adherence rate, disposition-effect inventory reduction, "no action warranted" acceptance rate.** | All five critiques: return metrics are unverifiable in any 90-day window, mis-incentivize the product toward action generation, and obscure the real value of bias correction. |

---

## 9. Questions Pranav must answer (the decision list)

### Scope

**Q1. What is your Phase 1 time horizon — personal use only, for how long?**
- (a) Pranav-only, indefinitely — this is a personal tool, productization is not a current goal
- (b) Pranav-only for 3 months, then evaluate PMF with 5–10 non-Pranav users
- (c) Pranav-only for 3 months, then evaluate whether to pursue SEBI RIA registration for productization
- *Your default if unanswered*: (b) — 3-month gate, then PMF evaluation

**Q2. What stocks and positions will you use for v1 testing?**
- (a) Pranav's actual live portfolio (highest validity, highest stakes)
- (b) A test portfolio with 20–25 real NSE holdings but no live money attached
- (c) A subset of 10 high-conviction holdings only
- *Your default if unanswered*: (a) — live portfolio with advisory-only output (no auto-execution)

**Q3. Exit rules: do you have defined exit rules today, or does the bot need to help you discover them?**
- (a) I have specific rules (e.g., sell if down >15% from entry, sell if RSI > 75 AND P/E > 2× sector median)
- (b) I have rough rules I've never written down — the bot should help me formalize them
- (c) I have no exit rules — the bot should propose a default framework I can accept or modify
- *Your default if unanswered*: (b) — rough rules needing formalization

### Strategy

**Q4. What is the primary success metric you will use to evaluate the bot at 90 days?**
- (a) Change in portfolio performance vs. NIFTY 50 (benchmark alpha)
- (b) Number of behavioral flags acted on (e.g., anchored positions reviewed and disposed of)
- (c) Stop-loss rule adherence rate (% of times the bot flagged a stop-loss violation and I acted)
- (d) Composite: (b) + (c) + Sharpe improvement
- *Your default if unanswered*: (d) — composite with behavioral metrics primary

**Q5. When TA and FA disagree on the same stock — e.g., strong fundamentals but in a confirmed technical downtrend — what should the bot do?**
- (a) Default to FA; flag the TA conflict as context
- (b) Default to TA for entries/exits; flag the FA context
- (c) Show both signals and refuse to recommend until the user selects a resolution rule
- (d) Prompt the user with: "Your holding period for this position is [X]. For a [swing/long-term] investor, [TA/FA] is the more relevant signal here. Current FA says [Y]. Current TA says [Z]. Which do you want to weight?"
- *Your default if unanswered*: (d) — context-sensitive prompt, no silent default

**Q6. Position sizing: do you want the bot to recommend position-size adjustments, or only direction (hold/trim/add)?**
- (a) Direction only — I manage sizing manually
- (b) Direction + position size as % of portfolio (half-Kelly default)
- (c) Direction + position size + explicit correlation-to-portfolio calculation
- *Your default if unanswered*: (b) — direction plus half-Kelly sizing recommendation

### Compliance

**Q7. Will you ever share the bot's output with anyone else?**
- (a) Never — strictly personal tool, no screenshots, no sharing, no GitHub publish
- (b) Possibly screenshots or outputs to a trusted friend/colleague informally
- (c) Possibly a public GitHub repo with the code (not the outputs)
- *Your default if unanswered*: (a) — if (b) or (c), the regulatory constraints change immediately and must be re-evaluated

**Q8. Which data source for v1?**
- (a) yfinance / scraping — prototype grade, no commercial risk at personal-use scale
- (b) Zerodha Kite Connect API — ₹2,000/month developer subscription; live portfolio + price data; first-party data for Pranav's own trades
- (c) NSE bhavcopy (end-of-day bulk download) — free, legal, delayed-data only
- (d) Combination: Kite for portfolio/trade data, bhavcopy for historical price series
- *Your default if unanswered*: (d) — Kite for portfolio, bhavcopy for historical analysis

### Product

**Q9. What is the minimum viable output format you would actually use weekly?**
- (a) A structured text report: [Review now / Watch / Hold] per position with 2–3 sentence reasoning each
- (b) A conversational chat interface — ask the bot specific questions about the portfolio
- (c) A simple dashboard with signal scores per holding (no prose)
- (d) (a) as the primary output, with (b) as a follow-up layer for drilling in
- *Your default if unanswered*: (d) — structured weekly report plus conversational drill-down

**Q10. Should the bot display entry price and cost-basis P&L by default?**
- (a) Yes — I want the full picture including my gains/losses from cost basis
- (b) No — hide entry price by default; show only current value and % of portfolio; let me toggle it on
- (c) Show entry price but frame it as "your thesis entry" not as a P&L anchor (e.g., "you entered at ₹450 thesis: value + momentum; current: ₹380; thesis intact? Y/N")
- *Your default if unanswered*: (c) — thesis framing reduces anchoring vs. raw P&L display

### Tech

**Q11. Should tax-awareness (LTCG/STCG) be in v1 or v2?**
- (a) v1 — basic LTCG/STCG calculator: show tax implications of selling each position today vs. waiting
- (b) v2 — too complex for v1 scope
- (c) v1 but read-only: show the tax cost, but don't factor it into recommendations
- *Your default if unanswered*: (c) — show tax cost in v1, factor into recommendations in v2

**Q12. What is the backtesting requirement before the bot makes its first live recommendation?**
- (a) No formal backtest for v1 — use it on my live portfolio and treat it as an ongoing experiment
- (b) A minimum walk-forward backtest on 3 years of NSE data, with out-of-sample Sharpe > 0.3 after costs, before any signal is trusted
- (c) Informal signal validation only — manually check 20–30 historical examples per signal type
- *Your default if unanswered*: (c) — informal validation for v1, formal walk-forward required before any multi-user or productization path

---

## 10. What I recommend Pranav decides FIRST (the critical-path questions)

These three questions constrain every subsequent design and implementation decision. Answer these first; the others can be deferred.

**CP-1: Q5 — TA vs FA conflict resolution rule.** This is the core design question for the entire system. The bot ingests two signals that frequently disagree. Without an explicit resolution rule, the LLM will make an implicit one — probably one absorbed from finfluencer content in its pretraining corpus. Every prompt template, every output format, every signal weighting depends on the answer to this question. My recommendation: adopt (d) — context-sensitive prompting that surfaces the conflict and asks the user to resolve it against their stated holding period. This is honest, educational, and non-committal in v1 while you gather data on how you actually want to resolve conflicts.

**CP-2: Q4 — Primary success metric at 90 days.** You cannot evaluate a tool that has no evaluation criteria. The choice between return-based and behavioral metrics is not cosmetic — it determines what features you build, what data you log, and whether the bot can fail in a visible, learnable way. My recommendation: (d) composite, with behavioral metrics (stop-loss adherence, disposition-effect flags acted on) as the primary signal in the first 90 days. Return attribution is too noisy in any 90-day window to be meaningful; behavioral metrics are visible within weeks.

**CP-3: Q1 — Phase 1 time horizon and personal-vs-product commitment.** This is the strategic question that all the other critiques circle back to. If this is definitively a personal tool, the architecture can be lean, the data sources can be scrappy, the regulatory posture can be relaxed. If there is any intention to productize — even informally — the architecture must be designed for it from day one, the data licensing must be commercial from day one, and the regulatory obligations must be acknowledged from day one. Mixing the two approaches produces a tool that is neither personal nor productizable. My recommendation: commit fully to (a) — personal tool, strict A1 — for Phase 1, with a calendar date for a PMF pivot evaluation (suggest 2026-09-30). If you are still uncertain, lean (a) and set the date.

---

## 11. What we'll do in Phase 2 once the problem statement is locked

- **Math and strategy survey**: NSE-specific validation of TA signal performance (RSI, MACD, Bollinger, 200DMA) on NIFTY 100 constituents with walk-forward methodology; cost-adjusted Sharpe computation; position sizing framework (half-Kelly implementation); TA/FA conflict-resolution taxonomy.
- **Data source survey**: Formal comparison of Kite Connect, NSE bhavcopy, yfinance, and commercial vendors for data quality, latency, legal footing, and cost; decision on v1 data stack.
- **Architecture sketch**: Python signal computation layer → Claude API reasoning layer → structured output format (JSON + human-readable brief); prompt templates for behavioral flag generation; prompt templates for TA/FA conflict surfacing; caching strategy for repeated portfolio queries.
- **Claude API design**: Prompt caching for portfolio-level context (reduces cost on weekly repeated queries); tool-use architecture for structured signal retrieval; agent design for multi-step portfolio analysis workflows; output schema for the weekly health report.
- **Behavioral design spec**: Specific UX rules per the behavioral critique (entry price display policy, cooling period logic, adversarial sell-case generation, sycophancy mitigation, track record logging from day one).
- **v1 backtest**: Informal signal validation on 20–30 historical examples per signal type (Q12 default), documented and revisable before any multi-user expansion.

---

## Appendix A — All sources (grouped by topic)

### Indian retail behavior and SEBI surveys
- [SEBI F&O Loss Study FY22–24 — Press Release](https://www.sebi.gov.in/media-and-notifications/press-releases/sep-2024/updated-sebi-study-reveals-93-of-individual-traders-incurred-losses-in-equity-fando-between-fy22-and-fy24-aggregate-losses-exceed-1-8-lakh-crores-over-three-years_86906.html)
- [SEBI F&O Losses FY25 +41% — Moneylife](https://www.moneylife.in/article/91-percentage-of-retail-traders-lost-money-in-derivatives-losses-in-fo-surged-41-percentage-to-rs105-lakh-crore-in-fy2425-sebi-study/77613.html)
- [SEBI Investor Survey 2025 — Official](https://www.sebi.gov.in/reports-and-statistics/research/jan-2026/investor-survey-2025-_99170.html)
- [SEBI Investor Survey 2025 — Finnovate Analysis](https://www.finnovate.in/learn/blog/sebi-investor-survey-2025-insights)
- [SEBI Investor Survey 2025 — 63% aware, 9.5% invest (ScanX)](https://scanx.trade/stock-market-news/stocks/sebi-investor-survey-2025-63-households-aware-of-market-products-only-9-5-actually-invest/30475080)
- [SEBI "Elusive Retail Investor" DRG Study](https://www.sebi.gov.in/sebi_data/DRG_Study/elusiveretailinvestor.pdf)
- [ISB Study on Retail Investor Losses — Business Standard](https://www.business-standard.com/article/markets/retail-investors-tend-to-lose-in-stock-markets-says-isb-study-112120100043_1.html)
- [ISB Study — Moneylife](https://www.moneylife.in/article/indian-retail-investors-tend-to-lose-in-stock-markets-isb/29947.html)
- [CFA Institute — India Derivatives and Retail Investors, Nov 2025](https://blogs.cfainstitute.org/marketintegrity/2025/11/05/indias-derivatives-market-and-retail-investors/)
- [Disposition Effect at Market Level — India (ResearchGate)](https://www.researchgate.net/publication/336162840_Disposition_effect_at_the_market_level_evidence_from_Indian_stock_market)
- [Behavioral Biases and Investment Choices India 2024 (ResearchGate)](https://www.researchgate.net/publication/397113427_Behavioral_Biases_and_Investment_Choices_Understanding_the_Mediating_Role_of_Risk_Perception_among_Indian_Retail_Investors)
- [SEBI Finfluencer / Info Gap Analysis (Whalesbook)](https://www.whalesbook.com/news/English/sebiexchange/Indias-Retail-Frenzy-Info-Gap-Fuels-Volatility-SEBI-Tackles-Finfluencers/699c8d82d83cd4ce4fe95e37)
- [FIA — India's Equity Derivatives Volume, 2024](https://www.fia.org/marketvoice/articles/explainer-meteoric-rise-indias-equity-derivatives-volume)
- [Bain — How India Invests 2025](https://www.bain.com/insights/how-india-invests-2025/)

### Existing products (problem framings)
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
- [Investar — TA+FA combined tool](https://investarindia.com/)
- [Jarvis Invest — AI stock picks India](https://www.stockgro.club/stoxo/resources/top-free-ai-tools-for-the-indian-stock-market/)
- [Groww MCP AI Portfolio Chat](https://groww.in/updates/groww-mcp)
- [Zerodha MCP + LLM Portfolio Insights](https://medium.com/google-cloud/unlocking-autonomous-portfolio-insights-with-google-adk-zerodha-mcp-and-llms-7c5f2bf3d4a3)
- [Tickertape Pro Pricing](https://www.tickertape.in/pricing)
- [StockEdge Premium Plans](https://stockedge.com/pricing)

### Academic / portfolio theory
- [Frontiers — Evaluating Robo-Advisors through Behavioral Finance 2024](https://www.frontiersin.org/journals/behavioral-economics/articles/10.3389/frbhe.2024.1489159/full)
- [Wiley — Evolution of Robo-Advisors 2025](https://onlinelibrary.wiley.com/doi/10.1111/ijcs.70131)
- [Tandfonline — Robo-advisors in Behavioural Finance 2025](https://www.tandfonline.com/doi/full/10.1080/23322039.2025.2571403)
- [ScienceDirect — Robo-Advisors Systematic Review 2024](https://www.sciencedirect.com/science/article/abs/pii/S1544612324001491)
- [Wiley — Indian Robo-Advisor Adoption 2025](https://onlinelibrary.wiley.com/doi/abs/10.1002/isd2.12346)
- [Wikipedia — Hierarchical Risk Parity](https://en.wikipedia.org/wiki/Hierarchical_Risk_Parity)
- [IIMA — Indian Fama-French Momentum Data Library](https://faculty.iima.ac.in/iffm/Indian-Fama-French-Momentum/)
- [S&P Global — Factor Investing India](https://www.spglobal.com/spdji/en/documents/research/research-an-index-approach-to-factor-investing-in-india.pdf)
- [Sullivan, Timmermann & White (1999) — Data-Snooping and TA Performance](https://onlinelibrary.wiley.com/doi/10.1111/1540-6261.00163)
- [Lopez de Prado (2018) — Advances in Financial Machine Learning](https://www.wiley.com/en-us/Advances+in+Financial+Machine+Learning-p-9781119482086)
- [Bailey, Borwein, Lopez de Prado & Zhu (2014) — Probability of Backtest Overfitting](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2326400)
- [Barber & Odean (2000) — Trading Is Hazardous to Your Wealth](https://faculty.haas.berkeley.edu/odean/papers%20current%20versions/individual_investor_performance_final.pdf)
- [ScienceDirect (2024) — Backtest Overfitting in the ML Era](https://www.sciencedirect.com/science/article/abs/pii/S0950705124011110)
- [Bajaj Finserv — STT Rates India 2026](https://www.bajajfinserv.in/securities-transaction-tax)

### LLM-finance agents
- [Bloomberg — BloombergGPT Press Release](https://www.bloomberg.com/company/press/bloomberggpt-50-billion-parameter-llm-tuned-finance/)
- [arXiv 2306.06031 — FinGPT Open-Source](https://arxiv.org/abs/2306.06031)
- [FinRL — Columbia Open Finance](https://openfin.engineering.columbia.edu/research-projects/financial-reinforcement-learning-finrl)
- [arXiv 2508.11152 — AlphaAgents (BlackRock)](https://arxiv.org/abs/2508.11152)
- [Magnifi / TIFIN](https://tifin.com/news/magnifi-now-providing-ai-powered-investment-intelligence-on-over-2b-of-linked-self-directed-assets/)
- [Composer — Trade With AI (BusinessWire 2025)](https://www.businesswire.com/news/home/20251021050436/en/Composer-Supercharges-Investing-Platform-with-New-Trade-With-AI-Tool)
- [Kavout — AI Tool Curator 2026](https://www.aitoolcurator.com/ai-tools/finance-investing/kavout/)
- [PortfolioPilot.com](https://portfoliopilot.com/)
- [arXiv 2512.12922 — LLM Personalized Portfolio Recommender](https://arxiv.org/abs/2512.12922)
- [ACM ICAIF 2024 — Democratizing Alpha](https://dl.acm.org/doi/10.1145/3768292.3770376)
- [arXiv 2411.11059 — Financial News LLM RL](https://arxiv.org/html/2411.11059v1)
- [arXiv 2504.14345 — LLM-Enhanced Black-Litterman](https://arxiv.org/html/2504.14345v2)
- [PM Research — LLMs for Financial Management 2024](https://www.pm-research.com/content/iijpormgmt/51/2/211)
- [SSRN 4947135 — Efficacy of LLMs in Predicting Stock Prices](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4947135)
- [arXiv 2505.07078 — Can LLM Investing Strategies Outperform Long-Run?](https://arxiv.org/html/2505.07078v3)
- [arXiv 2505.02151 — LLMs are Overconfident and Amplify Human Bias](https://arxiv.org/pdf/2505.02151)
- [arXiv 2507.20957 — Your AI, Not Your View: LLM Bias in Investment Analysis](https://arxiv.org/html/2507.20957v4)
- [arXiv 2504.09343 — Confirmation Bias in Generative AI Chatbots](https://arxiv.org/pdf/2504.09343)

### Regulatory (SEBI / RBI / DPDP)
- [SEBI (Investment Advisers) Regulations 2013 — amended Dec 2024](https://www.sebi.gov.in/legal/regulations/dec-2024/securities-and-exchange-board-of-india-investment-advisers-regulations-2013-last-amended-on-december-16-2024-_90151.html)
- [SEBI Guidelines for Investment Advisers — Sep 2020 Circular](https://www.sebi.gov.in/legal/circulars/sep-2020/guidelines-for-investment-advisers_47640.html)
- [SEBI Guidelines for Investment Advisers — Jan 2025 Circular](https://www.sebi.gov.in/legal/circulars/jan-2025/guidelines-for-investment-advisers_90632.html)
- [SEBI FAQs on IA Regulations — Sep 2024 Update](https://www.sebi.gov.in/sebi_data/faqfiles/sep-2024/1727418139473.pdf)
- [SEBI (Research Analysts) Regulations 2014 — amended Dec 2024](https://www.sebi.gov.in/legal/regulations/dec-2024/securities-and-exchange-board-of-india-research-analysts-regulations-2014-last-amended-on-december-16-2024-_90153.html)
- [SEBI Circular — Safer Retail Participation in Algo Trading, Feb 2025](https://www.sebi.gov.in/legal/circulars/feb-2025/safer-participation-of-retail-investors-in-algorithmic-trading_91614.html)
- [SEBI Circular — Algo Trading Timeline Extension, Sep 2025](https://www.sebi.gov.in/legal/circulars/sep-2025/extension-of-timeline-for-implementation-of-sebi-circular-dated-february-04-2025-on-safer-participation-of-retail-investors-in-algorithmic-trading-_96979.html)
- [SEBI Consultation Paper — AI/ML Guidelines, Jun 2025](https://www.sebi.gov.in/reports-and-statistics/reports/jun-2025/consultation-paper-on-guidelines-for-responsible-usage-of-ai-ml-in-indian-securities-markets_94687.html)
- [NSE Data Usage and Sharing Policy](https://nsearchives.nseindia.com/web/sites/default/files/inline-files/NSE_DataUsageandSharingPolicy.pdf)
- [Digital Personal Data Protection Act 2023 (MeitY)](https://www.meity.gov.in/static/uploads/2024/06/2bf1f0e9f04e6fb4f8fef35e82c42aa5.pdf)
- [Enforcement — Avadhut Sathe, SEBI, Dec 2025 (LiveLaw)](https://www.livelaw.in/amp/corporate-law/sebi-cracks-down-on-finfluencer-avadhut-sathe-impounds-546-crore-for-providing-unregistered-investment-advice-312335)
- [Enforcement — Nasir Ansari "Baap of Charts" (Moneylife)](https://www.moneylife.in/article/sebi-initiates-1814-crore-recovery-from-finfluencer-nasir-ansari-of-baap-of-charts-2-others/79146.html)
- [SEBI Finfluencer Circular — Business Standard Jan 2025](https://www.business-standard.com/markets/news/sebi-finfluencer-circular-live-stock-data-market-education-rules-125013000571_1.html)
- [SEBI AI/ML Governance Framework — India Corp Law analysis](https://indiacorplaw.in/2025/07/16/from-algorithms-to-accountability-analysing-sebis-ai-ml-governance-framework/)

### Behavioral finance
- Kahneman, D. *Thinking, Fast and Slow*. FSG, 2011.
- Kahneman, D. & Tversky, A. "Prospect Theory." *Econometrica* 47(2), 1979.
- Thaler, R. & Sunstein, C. *Nudge*. Yale UP, 2008.
- Thaler, R. *Misbehaving*. W. W. Norton, 2015.
- [Barber & Odean (2000) — Trading Is Hazardous to Your Wealth](https://faculty.haas.berkeley.edu/odean/papers%20current%20versions/individual_investor_performance_final.pdf)
- [Graham, Harvey & Huang (2005) — Investor Competence and Trading Frequency (NBER)](https://www.nber.org/papers/w11426)
- [Federal Reserve FEDS Working Paper 2025 — Financial Stability Implications of Generative AI](https://www.federalreserve.gov/econres/feds/files/2025090pap.pdf)
- [CFA Institute — Attention Bias in AI-Driven Investing, Feb 2026](https://blogs.cfainstitute.org/investor/2026/02/18/attention-bias-in-ai-driven-investing/)
- [HBS Working Knowledge 2025 — AI Financial Advice and Investor Outcomes](https://www.library.hbs.edu/working-knowledge/ai-can-churn-out-financial-advice-but-does-it-help-investors)
- [ARTICLE 19 — Algorithmic People-Pleasers, 2025](https://www.article19.org/resources/algorithmic-people-pleasers-are-ai-chatbots-telling-you-what-you-want-to-hear/)

### Product / fintech PMF
- [Wealthfront Unit Economics — Sacra](https://sacra.com/c/wealthfront/)
- [Wealthfront at $340M ARR — SaaStr](https://www.saastr.com/5-interesting-learnings-from-wealthfront-at-340000000-in-arr/)
- [Smallcase Revenue $105M — Latka](https://getlatka.com/companies/smallcase.com)
- [SEBI RIA / RA Count 2025 — Outlook Money](https://www.outlookmoney.com/plan/financial-plan/the-future-of-fiduciary-advice-in-india-building-trust-and-not-just-rules)
- [India Fintech Retention Benchmarks — BusinessDojo](https://dojobusiness.com/blogs/news/fintech-ideal-retention-rate)
- [Inc42 — State of Indian Fintech 2025](https://asset.inc42.com/2025/07/State-of-Indian-Fintech_Report.pdf)
- [NSE Registered Investors — NSE India](https://www.nseindia.com/registered-investors)

---

## Appendix B — Glossary

| Term | Definition |
|---|---|
| **TA (Technical Analysis)** | Analysis of price and volume patterns to forecast future price movements. Common tools: RSI, MACD, Bollinger Bands, moving averages, OBV. |
| **FA (Fundamental Analysis)** | Analysis of a company's financial statements, ratios, and business quality to assess intrinsic value. Key ratios: P/E, P/B, ROE, ROCE, D/E, FCF yield. |
| **RIA (Registered Investment Adviser)** | SEBI-registered entity licensed to provide personalized investment advice for compensation. Individual RIA: min ₹5L net worth, NISM-X-A/X-B certified, max 150 clients. |
| **RA (Research Analyst)** | SEBI-registered entity licensed to publish research reports on securities. Requires NISM-XV certification. |
| **MPT (Modern Portfolio Theory)** | Markowitz (1952) framework: construct portfolios that maximize expected return for a given level of risk (variance) using mean-variance optimization. |
| **Sharpe Ratio** | Risk-adjusted return metric: (portfolio return − risk-free rate) / portfolio standard deviation. Higher is better. |
| **Sortino Ratio** | Variant of Sharpe that penalizes only downside volatility (negative returns), not total volatility. More appropriate for asymmetric return distributions. |
| **HRP (Hierarchical Risk Parity)** | Lopez de Prado (2016) portfolio construction method using hierarchical clustering of asset correlations; does not require covariance matrix inversion. |
| **Black-Litterman** | Goldman Sachs (1990) model: blends market equilibrium (CAPM) return estimates with investor's subjective views into a stable portfolio allocation. |
| **Kelly Criterion / Half-Kelly** | Position sizing formula: bet size = edge / odds. Full Kelly maximizes long-run growth but is mathematically aggressive; half-Kelly (bet half the Kelly size) is the practical standard for reducing volatility of outcomes. |
| **DPDP (Digital Personal Data Protection Act 2023)** | Indian law (effective ~May 2027 for substantive rules) governing collection, processing, and storage of personal digital data. Penalties up to ₹250 crore. |
| **MITC (Most Important Terms and Conditions)** | SEBI-mandated summary document that RIAs must provide to clients before onboarding, covering fees, scope, and redressal. |
| **Disposition Effect** | Behavioral bias: tendency to sell winning investments too early and hold losing investments too long. Documented across all markets; strongest in Indian retail investors vs. global peers (ISB study). |
| **LTCG / STCG** | Long-Term Capital Gains / Short-Term Capital Gains. For Indian equities: LTCG tax at 12.5% above ₹1.25L exemption (held >12 months); STCG at 20% (held <12 months). Post-Budget 2024 rates. |
| **RSI (Relative Strength Index)** | TA momentum oscillator (0–100). Conventionally: RSI > 70 = overbought; RSI < 30 = oversold. Computed over a rolling window (typically 14 days). |
| **MACD (Moving Average Convergence Divergence)** | TA trend-following indicator: difference between a fast EMA (12-day) and slow EMA (26-day), with a signal line (9-day EMA of MACD). |
| **OBV (On-Balance Volume)** | TA volume indicator: cumulative volume in the direction of price movement; used to confirm price trends. |
| **Fama-French** | Multi-factor asset pricing models. Three-factor (1993): market, size, value. Five-factor (2015): adds profitability and investment. Used in factor investing. |
| **Walk-Forward Validation** | Backtesting methodology that progressively trains on historical data and tests on out-of-sample periods, mimicking live deployment. Minimum viable standard for any claimed trading edge. |
| **STT (Securities Transaction Tax)** | Indian tax on equity trades. For delivery: 0.1% on buy + 0.1% on sell = 0.2% round-trip. |
| **OPS (Orders Per Second)** | SEBI's February 2025 algo trading circular sets a 10 OPS per-exchange threshold; above this, exchange registration for the algorithm is required. |
| **MCP (Model Context Protocol)** | Anthropic-developed open standard enabling LLMs to connect to external data sources (e.g., Zerodha, Groww portfolio data). Used by Groww MCP and Zerodha MCP integrations (2025–26). |
| **CAGR** | Compound Annual Growth Rate: the annualized rate of return that would take an investment from its beginning value to its ending value over a given period. |
| **DCF (Discounted Cash Flow)** | Valuation model: estimates the present value of a company based on projected future free cash flows discounted at a required rate of return (WACC or cost of equity). |
