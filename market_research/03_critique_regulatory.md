# 03 — Critique: SEBI / Regulatory Lens

**Status**: Complete (first pass)
**Date**: 2026-05-30
**Reviewer persona**: SEBI compliance lawyer / Indian fintech regulatory expert

---

## TL;DR (5 bullets — the licenses and regulations you must be aware of)

1. **RIA trigger is "consideration," not "clients."** Under Regulation 2(1)(m) of SEBI (Investment Advisers) Regulations 2013, the registration obligation fires the moment you provide investment advice *for consideration*. Free, self-use, single-user = no trigger. Share it with one paying friend = full RIA registration required (net worth ₹5 lakh, NISM-X-A/X-B certification, compliance infrastructure).

2. **Auto-execution is a hard wall.** The SEBI circular dated February 4, 2025 ("Safer participation of retail investors in Algorithmic trading") mandates exchange-level approval for every algorithm above 10 OPS per exchange. Even a self-use algo requires static IP whitelisting, broker empanelment, and exchange registration. Advisory-only (Axis E1) avoids this entirely; E2/E3 does not.

3. **NSE market data is not free for anything that touches a product.** NSE's Data Usage and Sharing Policy prohibits redistribution of market data without a board-approved commercial agreement. yfinance and web scraping are legally ambiguous for personal use and clearly prohibited for any commercial or redistributed application. The "self-use" carve-out in NSE's ToS is real but narrow and untested in litigation.

4. **SEBI's June 2025 AI/ML Consultation Paper is pre-final regulation.** It will impose mandatory model governance, bias audits, explainability disclosures, 5-year documentation, and continuous SEBI reporting on any market participant deploying AI/ML tools that interact with clients. The paper is in its comment-response phase; final circular expected within 12–18 months. If the bot is ever productized before this circular is finalized, the compliance burden is retroactively large.

5. **The DPDP Act 2023 rules (effective ~May 2027) will classify portfolio data as personal data requiring consent, purpose limitation, and security safeguards.** Even self-use storage of another person's portfolio data (Axis A2 — friends/family) trips the Data Fiduciary obligations immediately upon the rules taking effect.

---

## Self-use scenario (Pranav-only, no monetization)

### What's allowed

The IA Regulations 2013 (Regulation 2(1)(m)) define "investment adviser" as a person who provides investment advice *for consideration*. The FAQs published by SEBI confirm that advice given without consideration is outside the registration net. A tool built for Pranav's own portfolio, not marketed to others, not charged to anyone, and not publicized, does not fit the definition. There is no registration requirement under IA Regulations for genuine self-use.

Similarly, SEBI (Research Analysts) Regulations 2014 apply to persons who publish research reports for clients. A private tool that produces analysis consumed only by its builder is outside this definition. No RA registration needed.

For algo execution at low order rates: the SEBI February 2025 circular sets a 10 OPS per-exchange threshold below which no algo registration is required. A swing/long-term bot executing, say, 1–2 trades per week is far below this. If the execution leg is wired up through a broker API (Zerodha Kite, Upstox, AngelOne), the orders travel through a SEBI-registered broker's infrastructure, which provides a compliance buffer.

DPDP Act 2023: as of today (May 2026), the substantive compliance rules are scheduled for effect ~May 2027. Self-use with no third-party data sharing is the lowest-risk data posture possible. There is no "Data Fiduciary" obligation when you are processing only your own data.

### What's risky even for self-use

**The "education vs. advice" line is still at risk if you use live market data.** SEBI's January 2025 finfluencer circular specifically bars use of live stock price data even in "educational" contexts unless you are a registered entity. If the bot pipes live NSE data and outputs actionable buy/sell language, it looks like advice even if no money changes hands. The defense ("it's my own portfolio") works legally but could be scrutinized if you ever share outputs, screenshots, or code.

**yfinance / scraping legal exposure.** NSE's ToS restricts site usage to "personal, non-commercial use only." NSE's Data Usage and Sharing Policy states that "Trading Members and Subscribers shall not be permitted to redistribute any Market Data, except as agreed in the Relevant Agreement." yfinance pulls from Yahoo Finance which in turn aggregates from exchange feeds under its own licensing. Yahoo Finance's ToS prohibits commercial use and automated scraping. For pure personal use with no monetization or redistribution, this is a grey zone — NSE has not initiated any enforcement against individual developers using yfinance for personal Python scripts. But the moment code is published on GitHub, shared with others, or connected to a service, redistribution exposure materializes.

**Auto-execution even for self-use.** If Pranav wires up E3 (full auto via broker API), the bot becomes an algo in the eyes of SEBI's February 2025 circular. If it breaches 10 OPS, it needs exchange registration through the broker. The registration requires static IP whitelisting, broker-level empanelment, and exchange approval — doable but non-trivial even for personal use.

**"Portfolio doctor" framing (Framing Z) creates a paper trail.** If the bot generates periodic written reports with specific buy/sell/trim language, those documents are indistinguishable from investment advice reports as defined in the IA Regulations. If Pranav ever emails one to a friend or posts to a WhatsApp group, the consideration element becomes constructive (reputational benefit, reciprocal favors) and a SEBI inquiry would be very uncomfortable.

### Citations

- SEBI (Investment Advisers) Regulations, 2013, Regulation 2(1)(m) — definition of investment adviser
- SEBI (Investment Advisers) Regulations, 2013, Regulation 2(1)(g) — definition of "consideration" (includes non-cash economic benefit)
- SEBI FAQs on IA Regulations (published 2015): advice given free through "media at large" is exempt, but privately targeted advice is not
- SEBI Circular SEBI/HO/MIRSD/DoP/CIR/2025/XX dated February 4, 2025 — "Safer participation of retail investors in Algorithmic trading" (10 OPS threshold, IP whitelisting, family-use carve-out)
- NSE Data Usage and Sharing Policy (NSE Archives, current version): redistribution prohibited without board-approved agreement
- SEBI (Research Analysts) Regulations, 2014, Regulation 3 — registration requirement only applies to persons who "publish or make available" research to clients

---

## Productization scenario (any sharing or monetization)

### License thresholds

The moment Pranav charges a rupee, shares the bot with a paying subscriber, or runs it as a SaaS service, he is providing investment advice for consideration. This triggers mandatory SEBI RIA registration. The post-2020 amendment thresholds are:

- Individual RIA: minimum net worth ₹5 lakh; NISM-Series-X-A and X-B certification; written client agreement with risk profiling for every client; suitability documentation; compliance auditor; grievance redressal mechanism; SEBI-registered
- Non-individual (firm/LLP): minimum net worth ₹50 lakh; same certification + compliance infrastructure
- Client cap: an individual RIA is capped at 150 clients. Beyond 150, must convert to non-individual entity registration

If the bot produces sector-level or stock-level recommendations that are distributed (even free but to multiple people), the SEBI (Research Analysts) Regulations 2014 apply instead. RA registration requires NISM-Series-XV certification, net worth of ₹1 lakh (individual) or ₹25 lakh (firm), and compliance with conflict-of-interest disclosure rules.

**The "smallcase model" escape hatch.** Smallcase is not registered as an RIA — it distributes SEBI-registered RA or RIA content through a technology platform. This is a specific structural arrangement. Replicating it requires upstream RA/RIA partners, which means finding licensed parties and operating as a technology intermediary, not as the advisory layer itself.

### Compliance burden

If RIA registration is triggered:

1. **KYC and risk profiling** (mandatory per Regulation 16): every client must undergo risk assessment before receiving advice. An automated risk questionnaire is acceptable (this is how Kuvera and INDmoney operate for MFs), but it must meet the suitability standard
2. **Written client agreement** (Regulation 19): formal agreement covering fees, scope, redressal
3. **Suitability documentation**: every recommendation must be linked to the client's documented risk profile
4. **Fee cap structure**: AUA mode (percentage of assets under advice) or fixed fee mode — no commissions from product providers
5. **Separation of advisory and distribution**: an RIA cannot simultaneously earn commissions from distributing MFs, insurance, or any product on which they advise. This makes the typical freemium broker-affiliate model unavailable
6. **Compliance officer**: mandatory for non-individual IAs
7. **SEBI's AI/ML framework (forthcoming)**: once the June 2025 consultation paper converts to a final circular, any productized AI advisory tool will additionally require model governance documentation, explainability disclosures to each client, bias audits, 5-year data retention, and incident reporting to SEBI. These obligations will apply retrospectively to any player in the market at that time

**Data licensing for a product:**
- Live NSE/BSE data: must purchase a commercial data license from NSE (through authorized vendors like Global Datafeeds, Refinitiv, or BSE's data division). These are priced for commercial users and are not cheap — typical small-company fees range from ₹5–50 lakh per year depending on coverage and latency
- yfinance / scraping: explicitly prohibited for commercial or redistribution purposes. Liability is real

**DPDP Act 2023 (rules effective ~May 2027):**
- A productized bot processing user portfolio data becomes a "Data Fiduciary"
- Obligations: notice before collection, consent for each processing purpose, purpose limitation, data minimization, security safeguards, breach notification, user rights (access, correction, erasure)
- Penalty for non-compliance: up to ₹250 crore
- Even a beta with 10 users, if collecting portfolio data, creates DPDP exposure

### Citations

- SEBI (Investment Advisers) Regulations, 2013 (as amended December 16, 2024), Regulations 3, 7, 15, 16, 19
- SEBI Circular dated September 2020 — Guidelines for Investment Advisers (separation of advisory and distribution)
- SEBI (Research Analysts) Regulations, 2014 (as amended December 16, 2024), Regulations 3, 7
- SEBI Circular dated February 4, 2025 — Safer participation of retail investors in Algorithmic trading
- SEBI Consultation Paper dated June 20, 2025 — Guidelines for Responsible Usage of AI/ML in Indian Securities Markets
- Digital Personal Data Protection Act, 2023 (No. 22 of 2023), Sections 4, 5, 6, 8, 17 — DPDP Rules 2025 effective ~May 2027
- NSE Data Usage and Sharing Policy (NSE Archives)

---

## Specific landmines in the current problem-statement drafts

The following exact lines or framings in `problem_statement.md` create regulatory exposure:

**Line: "A2 — Pranav + small circle (friends/family)" (Section 2, Axis A)**
This is the single most dangerous option in the document. The moment the bot serves even one person other than Pranav, the "for consideration" analysis opens. "Consideration" under Regulation 2(1)(g) includes *non-cash economic benefit*. Reciprocal goodwill, reputational gain, a dinner, a thank-you — SEBI enforcement has construed these broadly in finfluencer cases (e.g., Avadhut Sathe, where implicit consideration from follower engagement was treated as sufficient). There is no safe "family carve-out" in the IA Regulations. The algo trading circular has a family carve-out for execution algos; the IA Regulations do not extend this to advisory.

**Line: "E2 — Semi-auto — bot generates orders, Pranav approves one-click" (Axis E)**
E2 is not meaningfully different from E3 in SEBI's eyes if the order-generation is automated. The February 2025 circular defines an algo as any system that automatically generates orders. "One-click approval" is cosmetic from a regulatory standpoint — if the bot generates the order parameters and the human just confirms, it is still an algo. This requires exchange registration for the strategy.

**Line: "E3 — Fully auto — bot executes via broker API" (Axis E)**
Unambiguously algo trading. Requires: (a) broker to be empanelled as algo provider with the exchange, (b) the strategy to be approved by the exchange prior to deployment, (c) static IP whitelisting, (d) OPS compliance. Implementing this before these approvals are in place is a SEBI violation and the broker can terminate API access.

**Line: "D2 — New entry ideas (idea generation from universe)" (Axis D)**
Generating buy recommendations across the NIFTY 500 universe, even for Pranav alone, starts to look like research analyst activity. Publishing these (even in a private Notion or GitHub) is a grey zone. Sharing them with anyone else triggers RA registration.

**Line: "A3 — Generic Indian retail investor" and "PMF analysis" language throughout**
The research document (01_research.md, Bucket 5, Net-New Opportunity Space) explicitly frames the goal as a product for the "Indian retail investor." The problem_statement.md acknowledges "product-market fit" testing. The moment PMF testing involves giving the bot's output to real users (even as a free beta), the IA/RA registration question is live. SEBI does not recognize a "beta testing" exemption from the IA Regulations.

**Line in 01_research.md (Bucket 5): "Sits in the regulatory safe harbor: advisory-only, no compensation, self-use = no SEBI-RIA requirement"**
This claim is correct *but incomplete*. It omits: (a) the data licensing issue with live feeds, (b) the RA regulations which apply to publication of research regardless of compensation in some readings, (c) the DPDP implications for any multi-user scenario, (d) the incoming AI/ML framework. Framing this as a settled "safe harbor" is overconfident and should be flagged prominently.

---

## Implications for the problem statement

**1. Lock Axis A at A1 (Pranav-only) with legal language, not just preference.** The problem statement should explicitly state that the tool is for single-user personal use, never shared, never monetized in Phase 1 — and this should be treated as a hard constraint, not a soft starting point. Every downstream design decision (data sources, output format, sharing features) should be evaluated against this constraint.

**2. Remove E2 and E3 from the framing entirely in Phase 1.** E1 (advisory-only, manual execution) is the only option with clean regulatory footing. E2/E3 should be listed only as potential Phase 3 options, contingent on obtaining broker empanelment and exchange algorithm approval.

**3. Reframe Framing Z ("Portfolio Doctor") output as analysis, not advice.** The output language matters. "Your RSI is 72 and historically that has preceded corrections in this stock" is analysis. "Sell 30% of your HDFC Bank position" is advice. The bot's output template should consistently use the analysis framing. This is not merely semantic — it is the actual legal distinction SEBI draws, and it is the line finfluencer enforcement has been organized around.

**4. The "product-market fit" research frame creates a two-track problem.** PMF research requires testing with users; testing with users requires compliance infrastructure. The research document should separate "Phase 1 PMF research" (desk research, surveys, interviews — no product in users' hands) from "Phase 2 pilot" (product deployment, requires compliance review first). Conflating them creates a window of unintentional regulatory violation.

**5. Data sources must be decided before code is written.** yfinance is fine for prototyping. It is not fine for a product. The problem statement should flag that any productization path requires a commercial NSE/BSE data license — and that cost should appear in any PMF/business model analysis.

---

## Questions the user must answer

1. Is this definitively Phase 1 = Pranav-only, or is the goal to have friends/family test it within 6 months? (Answer determines whether IA Regulations are live now or later.)

2. Will the bot ever execute orders automatically, or will Pranav always click "place order" manually in Zerodha/Upstox? (Answer determines whether algo trading rules apply at all.)

3. Will the bot's output ever be shared — even screenshots, WhatsApp messages, or a private GitHub repo with a colleague? (Answer affects RA and IA exposure.)

4. What data source is planned for live NSE prices? yfinance/scraping for prototype is fine; is there a plan to switch to a licensed vendor before any public release?

5. Is there any monetization path imagined — subscription, API licensing, white-labeling to a broker? If yes, at what user count or revenue milestone does compliance infrastructure need to be in place? (The 150-client cap for individual RIA is the hard ceiling before mandatory entity upgrade.)

6. Will the bot store portfolio data on a server (cloud or otherwise), or run entirely locally on Pranav's machine? (Server-side storage creates DPDP Data Fiduciary exposure even before rules take effect.)

7. Is the "NSE-only, advisory-only, NIFTY 500" scope actually locked, or does the problem statement leave room for F&O instruments? (F&O derivatives are a separate regulatory universe with additional complexity.)

---

## Regulatory sources cited

- [SEBI (Investment Advisers) Regulations, 2013 — Last amended December 16, 2024](https://www.sebi.gov.in/legal/regulations/dec-2024/securities-and-exchange-board-of-india-investment-advisers-regulations-2013-last-amended-on-december-16-2024-_90151.html)
- [SEBI (Investment Advisers) Regulations, 2013 — Last amended August 3, 2021](https://www.sebi.gov.in/legal/regulations/aug-2021/securities-and-exchange-board-of-india-investment-advisers-regulations-2013-last-amended-on-august-03-2021-_48742.html)
- [SEBI Guidelines for Investment Advisers — September 2020 Circular](https://www.sebi.gov.in/legal/circulars/sep-2020/guidelines-for-investment-advisers_47640.html)
- [SEBI Guidelines for Investment Advisers — January 2025 Circular](https://www.sebi.gov.in/legal/circulars/jan-2025/guidelines-for-investment-advisers_90632.html)
- [SEBI FAQs on Investment Advisers Regulations, 2013](https://www.sebi.gov.in/sebi_data/attachdocs/1424862077270.pdf)
- [SEBI FAQs on IA Regulations — September 2024 Update](https://www.sebi.gov.in/sebi_data/faqfiles/sep-2024/1727418139473.pdf)
- [SEBI (Research Analysts) Regulations, 2014 — Last amended December 16, 2024](https://www.sebi.gov.in/legal/regulations/dec-2024/securities-and-exchange-board-of-india-research-analysts-regulations-2014-last-amended-on-december-16-2024-_90153.html)
- [SEBI Circular — Safer participation of retail investors in Algorithmic trading, February 4, 2025](https://www.sebi.gov.in/legal/circulars/feb-2025/safer-participation-of-retail-investors-in-algorithmic-trading_91614.html)
- [SEBI Circular — Extension of timeline for Algo Trading implementation, September 2025](https://www.sebi.gov.in/legal/circulars/sep-2025/extension-of-timeline-for-implementation-of-sebi-circular-dated-february-04-2025-on-safer-participation-of-retail-investors-in-algorithmic-trading-_96979.html)
- [SEBI Consultation Paper — Guidelines for Responsible Usage of AI/ML in Indian Securities Markets, June 20, 2025](https://www.sebi.gov.in/reports-and-statistics/reports/jun-2025/consultation-paper-on-guidelines-for-responsible-usage-of-ai-ml-in-indian-securities-markets_94687.html)
- [NSE Data Usage and Sharing Policy (current)](https://nsearchives.nseindia.com/web/sites/default/files/inline-files/NSE_DataUsageandSharingPolicy.pdf)
- [NSE Data Policy — Market Data page](https://www.nseindia.com/static/market-data/nse-data-policy)
- [Digital Personal Data Protection Act, 2023 (Ministry of Electronics and IT)](https://www.meity.gov.in/static/uploads/2024/06/2bf1f0e9f04e6fb4f8fef35e82c42aa5.pdf)
- **Enforcement action — Avadhut Sathe (SEBI Order, December 2025)**: SEBI impounded ₹546 crore and banned Avadhut Sathe for providing unregistered investment advisory services disguised as "education." This is the clearest recent signal that SEBI treats output framing ("advice" vs. "education") as determinative and will pierce the education label if specific securities are named. [LiveLaw coverage](https://www.livelaw.in/amp/corporate-law/sebi-cracks-down-on-finfluencer-avadhut-sathe-impounds-546-crore-for-providing-unregistered-investment-advice-312335)
- **Enforcement action — Nasir Ansari ("Baap of Charts")**: SEBI initiated ₹18.14 crore recovery for unregistered investment advice. [Moneylife coverage](https://www.moneylife.in/article/sebi-initiates-1814-crore-recovery-from-finfluencer-nasir-ansari-of-baap-of-charts-2-others/79146.html)
- **Enforcement action — PR Sundar**: SEBI fined ₹6 crore for unregistered options advisory. Enforcement shows SEBI will pursue even technically-framed content if specific securities with actionable recommendations are involved.
- [SEBI Finfluencer regulations — Business Standard January 2025](https://www.business-standard.com/markets/news/sebi-finfluencer-circular-live-stock-data-market-education-rules-125013000571_1.html)
- [Robo-Advisors and SEBI Registration requirement — analysis by cskruti.com](https://cskruti.com/robo-advisors-sebi-registration/)
- [SEBI AI/ML Governance Framework analysis — India Corp Law](https://indiacorplaw.in/2025/07/16/from-algorithms-to-accountability-analysing-sebis-ai-ml-governance-framework/)
