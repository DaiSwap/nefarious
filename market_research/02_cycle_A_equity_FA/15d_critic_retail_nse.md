# 15d — Cycle A Critique: Indian Retail Investor + NSE Specialist Lens

**Status**: ✅ Retail + NSE critique complete.
**Date**: 2026-05-30
**Lens**: Indian Retail Investor + NSE Specialist (merged)
**Last updated**: 2026-05-30T00:15:00

## 1. Verdict on v0.1 (top-line)

**REFACTOR-REQUIRED.**

v0.1 is structurally broken for two of my largest holdings (HDFC Bank, ICICI Bank — silently skipped) and actively misleading for at least one archetype I actually hold (specialty chemicals, small-sector ROCE problem). The pipeline logic is sound and the transparency is real, but a system that produces no output for 2 of my 12 stocks and cannot distinguish "Asian Paints HOLD" from "Asian Paints HOLD at 90x P/E with Birla Opus about to launch" is not yet an investor's planning tool — it is a financial data summary that dresses up as one.

## 2. Position on each of the 6 known weaknesses

### W1 — Beneish false positives during regime shifts
**CONFIRM — and the Indian context makes it worse than the synthesis suggests.**

The synthesis correctly identifies COVID-era working-capital aberrations as the mechanism. But Indian retail investors face at least three additional regime-shift triggers that the synthesis does not name explicitly: GST implementation (July 2017, which distorted debtor days and inventory across the full NIFTY 500 for two fiscal years), demonetization (November 2016, distorted cash/receivables), and Ind AS first-time adoption windows (various dates, FY2017–FY2020). Any of my 12 holdings with a history going back through GST transition will have a permanently contaminated FY2018 M-Score input — the DSRI, LVGI, and SGAI signals all have structural discontinuities from that event that Beneish cannot filter.

Concretely, for my specialty chemicals holdings (SRF, Aarti, PI Industries): these companies were aggressive capex stories post-2019. Rising DEPI (declining depreciation rate on expanded asset base) and high SGI (revenue growth) are structural features of their growth phase, not manipulation signals. The Beneish formula was calibrated on US manufacturing firms that do not have equivalent rapid-capex-plus-revenue-growth profiles. I would expect all three to produce elevated M-Scores during their peak investment phases, creating false positives precisely when the underlying business is most healthy.

**Fix**: The synthesis proposes three options (raise threshold, require confirming signal, downgrade to additive). From a retail perspective, the ONLY acceptable fix is downgrading Beneish from a knockout gate to an additive flag with an attached plain-language note. "Potential manipulation signal — likely caused by working-capital anomaly, verify manually" is useful. "FLAG: MANIPULATION-RISK, pipeline halted" is dangerous. A retail investor who sees the latter will either panic or stop trusting the system.

---

### W2 — Beneish false negatives for commodity firms
**CONFIRM — but I hold no commodity names, so this is a lesser concern for MY portfolio specifically.**

For Tata Steel, the TATA term (4.679 coefficient on the accruals index) overwhelms every other signal across all four test dates. This is not a flaw of Tata Steel's accounting — it is a structural property of any company with large non-cash charges (depreciation, impairments) relative to net income. My Polycab and KEI are capital-intensive but not at the same magnitude as steel. However, if the NIFTY 500 universe includes Coal India, ONGC, or SAIL, the Beneish model structurally cannot detect manipulation in any of them.

More concerning from an NSE-specialist view: this means Beneish creates a two-tier system where it functions as a manipulation screen for asset-light companies (FMCG, IT, chemicals) and is essentially switched off for heavy industry and PSUs. The bot does not communicate this distinction to the user. A retail investor with SAIL in their portfolio sees PASS for Beneish and draws false comfort from a signal that is mathematically inert.

**Fix**: For companies where the TATA term alone would carry M-Score below −3.5 regardless of the other seven indices, flag the score as BENEISH-INERT and substitute an alternative manipulation screen (related-party transaction volume, auditor tenure, restatement history) rather than reporting a PASS that carries no information.

---

### W3 — Piotroski F-Score is anti-correlated with cyclical entry opportunity
**CONFIRM — and this is the most dangerous failure for Indian retail investors specifically.**

Indian retail investors are notoriously late to cyclical entries. The entire behavioral trap is: we wait for "the numbers to confirm" before buying. v0.1 would serve that bias perfectly — it scores highest (F=8, HOLD) at exactly the point when trailing numbers look best, which is the cycle peak. A retail investor using v0.1 would systematically buy cyclicals at peaks and receive REVIEW signals at troughs, reinforcing the classic disposition-effect loop.

This matters not just for steel. My four mid-caps include Crompton and Astral. Crompton is cyclical (exposed to housing/real estate cycle). Astral (pipes) is semi-cyclical, exposed to construction cycles. During a construction downturn, both would generate low F-Scores not because they are poor businesses but because YoY signals — margin change, asset turnover change, ΔROA — all deteriorate in lockstep with sector demand. The system would flag REVIEW/WATCH on businesses that should be ACCUMULATE for a long-term investor.

Additionally, the synthesis frames this as a "cyclicals problem" implying it only affects designated cyclical sectors. This is too narrow. Any company with meaningful revenue concentration in infrastructure, housing, real estate, or auto faces the same Piotroski anti-correlation problem. That includes a large fraction of the NIFTY 500 mid-cap space.

**Fix**: The synthesis proposes a cyclical-sector classification gate. From a retail perspective, this must be explicit in the output — not just a backend filter. When the bot produces a REVIEW label for Crompton, I need to see "Note: This is a cyclical sector. Low F-Score at trough does not have the same meaning as low F-Score for a secular compounder." Without that, I will act incorrectly on the signal.

---

### W4 — Ind AS 116 lease accounting breaks YoY signals
**CONFIRM — with an additional NSE-specific dimension the synthesis underweights.**

The synthesis correctly identifies Ind AS 116 as a one-time transition distortion for FY2020 data. But the FY2020 distortion is now FIVE YEARS behind us. If v0.1 is computing any signal using a YoY pair that spans FY2019 → FY2020, the Ind AS 116 distortion is still in the denominator for any 3-year averaging window (e.g., the FCF/NI ratio uses FY2018–FY2020 for a Mar-2020 evaluation). The practical fix is to hardcode the FY2019/FY2020 year-pair as a flagged transition year and suppress affected signals rather than treat them as informative.

More broadly, Indian accounting history has multiple such transitions: GST (FY2017/FY2018), Ind AS first-time adoption (FY2017 for many listed companies), and Ind AS 116 (FY2020). Any evaluation date that uses data spanning one of these transitions should carry a low-confidence flag across multiple signals.

This is not a theoretical concern for mid-caps. Screener.in shows many NIFTY 500 mid-cap companies with abrupt FY2017 or FY2018 balance sheet jumps that are pure accounting reclassification, not business change. For my KEI Industries and Crompton holdings, both had meaningful adoption-year balance sheet effects that would distort F-Score and Beneish on any evaluation window that crosses those years.

**Fix**: Maintain a lookup table of known Indian accounting transition year-pairs (FY2017→FY2018 for GST; FY2019→FY2020 for Ind AS 116) and suppress affected signals or flag them as TRANSITION-YEAR-DISTORTION rather than as informative positive/negative signals.

---

### W5 — Altman Z″ dominated by century-accumulated reserves
**CONFIRM — and the PSU variant is even more extreme.**

The synthesis correctly notes this for Tata Steel and Reliance. From an NSE-specialist view, the problem is broader: virtually every NSE-listed company that has operated for more than 20 years has a Retained Earnings / Total Assets (X2) term high enough to push Z″ comfortably above 2.6 regardless of current-period leverage. This includes ITC (1910, century of reserves), Reliance (1973, massive reserves), L&T (1938), ONGC (1956 via government oil pools), Coal India (decades of state profits). For all of these, Altman Z″ is structurally inert as a current-period distress screen.

The PSU extension is especially concerning: Coal India, ONGC, BPCL, and SAIL all have enormous retained earnings from decades of state ownership, yet they face structural risks (government-mandated pricing, dividend extraction, capex interference) that Altman's model was never designed to detect. A Coal India with Z″ = 9.0 can still face a cash crunch if the government forces it to underprice coal at below-market rates — and Altman tells you nothing about this.

**Fix**: For companies with listing history >15 years, suppress the absolute Z″ PASS/FAIL interpretation and replace with "Z″ trend vs. 3-year-ago" as a relative distress indicator. A company whose Z″ is declining by >1.0 per year despite high absolute levels deserves a warning regardless of threshold breach.

---

### W6 — Sector ROCE percentile fails on small sectors
**CONFIRM — and this is the failure that directly hits my specialty chemicals holdings hardest.**

The synthesis identifies Indian Paints as the canonical small-sector case (N=4–5). But from my portfolio's vantage point, the MORE IMPORTANT small-sector problem is specialty chemicals. NSE classifies SRF, Aarti Industries, and PI Industries under "Chemicals" sector at the broad level. But:

- At the NSE "Industry" tier, they are split: SRF (Specialty Chemicals / Diversified Chemicals), Aarti Industries (Specialty Chemicals / Benzene Derivatives), PI Industries (Agrochemicals / Crop Protection). If ROCE percentile is computed at the Industry or Basic Industry tier (not the Sector tier), all three are in peer sets of N < 10.

- Even at the Sector tier ("Chemicals"), if we include commodity chemicals (GHCL, Deepak Nitrite, Vinati Organics, Gujarat Fluorochemicals, Navin Fluorine, SRF, Aarti, PI, Atul, Tata Chemicals, NOCIL, Gujarat Alkalis...) the N might reach 20+, but now we're comparing fine-chemistry agrochemical exporters (PI Industries) with commodity soda-ash producers (Tata Chemicals), which produces meaningless ROCE percentiles. PI Industries' 25–30% ROCE is genuinely exceptional relative to fine-chemical peers, but gets compressed to median when measured against the broader Chemicals sector bucket.

The v0.1 spec says "NSE 4-tier system, Sector level (22 sectors)" — this is the broadest possible grouping. At 22-sector level, "Chemicals" as a sector has enough N but loses all sub-sector signal. My specialty chemicals holdings would be told they are at, say, the 70th percentile of a peer set that includes commodity producers — which understates their quality advantage within their specific market. Conversely, a commodity chemicals company could look like it has acceptable ROCE percentile because it is being measured against fine-chemical premiums.

**Fix**: For ROCE percentile, use NSE's "Industry" tier (one level below Sector) as the primary grouping, but apply the N-threshold rules. If N < 10 at Industry tier, fall back to Sector tier with an explicit note: "Peer set expanded to Sector level (N too small at Industry level) — interpret with caution." This preserves the fine-chemicals vs commodity-chemicals distinction for MY holdings while still producing a number when Industry-N is too small.

## 3. NEW concerns (not in synthesis)

### NEW-1 — BFSI silent skip is a critical gap, not an acceptable v0.1 limit

The synthesis mentions the BFSI skip in passing. The math critique documents acknowledge it as a known limitation. But from my perspective as a retail investor, HDFC Bank and ICICI Bank are my TWO LARGEST HOLDINGS. They represent somewhere between 20–30% of my 12-stock portfolio's value. v0.1 produces exactly zero output about them.

This is not a minor limitation. It means:

**The bot's weekly report is structurally incomplete for my actual portfolio.** Every Monday I open the report and the two positions I care most about — because they are the largest, because they are also the two names where a bad quarter (GNPA spike, NIM compression, AUM growth miss) can most move my total portfolio value — are listed as SKIPPED-BFSI with no context whatsoever. No F-Score, no quality flag, no "did anything materially change since last week" signal. Nothing.

The synthesis notes that BFSI needs its own pipeline (P/ABV, NIM, GNPA, PCR, CAR). Absolutely correct. But the v0.1 spec's decision to simply skip BFSI rather than produce even a minimal "we can't score this, here's what to manually check" output is actively harmful for a user like me. SKIPPED-BFSI as a label gives me no information. It does not tell me whether HDFC Bank's GNPA is trending up or down. It does not tell me that ICICI Bank's PCR is 80%+ (genuinely good) vs a peer that might be at 60%. It does not tell me anything.

The cost of this gap: I will continue making holding decisions about HDFC Bank and ICICI Bank on the same gut+Screener.in+YouTube basis I use today, which is the exact behavior the bot is supposed to replace. v0.1 is built for a portfolio that has NO banks. A NIFTY 500 bot that can't cover BFSI — the single largest weight in the NIFTY 500 (financial services is typically 35–40% of the index by market cap) — is a bot that covers the minority of the market by weight.

**Is this acceptable as a v0.1 limit?** Only if the v0.1 report clearly states to the user: "IMPORTANT: This report covers 10 of your 12 holdings. HDFC Bank and ICICI Bank are not covered in v0.1. Manual review required for these positions." Without that explicit disclaimer, the user will draw false comfort from the 10 that ARE covered, while the 2 biggest ones are invisible. The current spec's SKIPPED-BFSI label buried in the report does not meet this standard.

**Fix (P0 for v0.2)**: Even before a full BFSI pipeline is built, produce a minimal BFSI stub output that pulls the most recent quarterly result (NIM, GNPA, PCR from the latest earnings call or annual report) and flags whether it is improving or deteriorating YoY. This is a qualitative data card, not a score — but it is infinitely more useful than a blank label. A user seeing "HDFC Bank: NIM 4.2% (last year: 4.1% — stable), GNPA 1.3% (last year: 1.4% — improving), PCR 74% — no immediate concern, but no formal score available until BFSI pipeline built" can make a reasonable hold/watch decision.

---

### NEW-2 — Mid-cap and small-cap data quality will silently corrupt Beneish at scale

The synthesis does not address data sufficiency for the 400 non-NIFTY 100 stocks in the NIFTY 500. The Beneish model requires 2 consecutive years of comparable consolidated financials. The Piotroski 3-year FCF/NI window requires 3 years. The ROCE sector percentile requires peer data for all companies in the sector.

For the NIFTY 100, data quality from Screener.in and Tickertape is generally acceptable. For the remaining 400 NIFTY 500 companies (the mid-cap, small-cap zone where stocks like Crompton, KEI, and Polycab sit), data quality has several systematic problems:

**Problem 1 — Consolidation inconsistency**: Many NIFTY 500 mid-caps have subsidiaries but report inconsistently between standalone and consolidated across years. Screener.in sometimes shows both and sometimes shows only one. If a company switches from standalone to consolidated reporting mid-history (not uncommon among growing mid-caps), the YoY Beneish comparison will be between two incompatible bases, producing a spurious manipulation flag on the transition year.

**Problem 2 — Missing SG&A data**: The Asian Paints test found that SGAI was DATA-UNAVAILABLE for all four dates because Screener.in does not disaggregate SG&A. This is not just an Asian Paints problem — it is universal across Indian listed companies that use the "nature of expenses" P&L format (raw materials, employee costs, depreciation, other expenses) rather than the "function of expenses" format (cost of goods sold, SG&A, R&D). Per the Companies Act 2013 Schedule III, Indian companies may use either format. The vast majority use nature-format, which means SGAI is DATA-UNAVAILABLE for essentially the entire NIFTY 500. Setting SGAI=0 as the Asian Paints test does is not "conservative" — it is systematically biasing the M-Score by omitting a term with coefficient −0.172. For every company, the SGAI coefficient is set to 0 instead of its actual value, meaning the M-Score has a permanent missing-input bias of unknown magnitude across the entire universe.

**Problem 3 — Beneish 2-year requirement at NIFTY 500 scale**: The spec says companies with <2 years of NSE history get INSUFFICIENT-DATA. But what fraction of the NIFTY 500 actually qualifies? As of 2026, several NIFTY 500 constituents are recent IPOs (post-2022 listings like Zomato, Paytm-era entrants, some defense PSU listings). More importantly, for the Beneish window to be meaningful, the YoY data must be from comparable accounting periods — which rules out transition years. If we exclude FY2018 (GST) and FY2020 (Ind AS 116) from YoY comparisons, we have effectively created data gaps that may render Beneish un-computable for any evaluation date where the denominator year is FY2018 or FY2020 for the entire universe of 500 companies simultaneously.

**My practical concern**: I hold KEI Industries. KEI is a NIFTY 500 mid-cap cables company — not tiny, not illiquid — but its Screener.in data has gaps in CWIP and some quarterly breakdowns. If the bot runs Beneish on KEI and AQI uses a proxy for PPE that is off by 10%, the M-Score result changes. For a company sitting near the −1.78 threshold, a 10% AQI error could flip a PASS to a HALT. The bot should report data confidence alongside the output, not just the final score.

**Fix (P1)**: Add a data-quality confidence score to every pipeline output: "Beneish computed on complete data (8/8 indices)" vs "Beneish computed on partial data (7/8 indices — SGAI missing, set to 0)" vs "Beneish not computed — insufficient history." Do not silently produce a PASS when two of the eight indices were filled with defaults. Report the partial completeness to the user so they can calibrate trust.

---

### NEW-3 — NSE classification tier is unspecified, and the choice materially changes signal quality

The v0.1 spec states: "NSE 4-tier system, Sector level (22 sectors). Source: NSE Indices classification (July 2023)."

This locks the ROCE percentile peer set at the broadest available tier. 22 sectors for ~500 stocks means an average N of approximately 23 per sector — barely above the N≥15 threshold for "full confidence." But the actual distribution is extremely uneven:

- BFSI (Financial Services): ~100+ companies — N so large that percentile is dominated by PSU banks, private banks, NBFCs, insurance, AMCs, brokerages, all in one bucket.
- Metals & Mining: ~20–25 companies (as shown in Tata Steel test)
- Oil, Gas & Consumable Fuels: ~10–15 companies
- Chemicals: ~30–40 companies (mixes commodity and specialty)
- Consumer Durables: ~40–50 companies (mixes electronics, paints, household products)
- Healthcare: ~50 companies (mixes hospitals, pharma, diagnostics)

At the Sector tier, ROCE percentile comparisons mix economically unrelated businesses. A specialty hospital comparing ROCE against a generic drug manufacturer within "Healthcare" is not informative. A specialty chemicals exporter comparing ROCE against a commodity bulk chemical producer within "Chemicals" is not informative.

The spec DOES NOT address this economic heterogeneity within sectors. It treats 22-sector ROCE percentile as a neutral measure, but it is actually a measure whose informativeness varies enormously by sector. For my specialty chemicals holdings (SRF, Aarti, PI Industries), a Sector-level ROCE percentile against all "Chemicals" companies is less informative than an Industry-level comparison against only specialty/fine chemicals peers.

More specifically: PI Industries at Sector level competes for ROCE rank against Tata Chemicals (commodity, low ROCE). At Industry level, PI Industries competes against agrochemical companies only — its 28–30% ROCE places it genuinely at the top of that peer set. The Sector-level measurement systematically undercredits PI Industries' capital efficiency by including a long tail of commodity producers.

**Fix (P1)**: The spec must explicitly state which tier is used for which sector and why. The simplest rule: use Industry tier (tier 3) for heterogeneous sectors (Chemicals, Consumer Durables, Healthcare, Financial Services) and Sector tier for homogeneous ones (Metals & Mining, Oil & Gas). Publish the tier mapping alongside sector N-counts so users can see which peer set their holding was benchmarked against.

---

### NEW-4 — Weekly cadence creates report overload; no delta view means 12 reports, not 1

Per Q9 (locked: weekly structured report, weekly cadence), v0.1 generates a full output for each of my 12 holdings every week. That is 12 independent HOLD/WATCH/REVIEW assessments, each with 2–3 sentences of reasoning.

Here is the practical problem: Piotroski F-Score is computed from annual data. FCF/NI is a 3-year average. ROCE is trailing-twelve-months but changes meaningfully only quarterly. The fundamental picture for a holding almost NEVER changes week-to-week. A HOLD label for ITC this Monday will still be a HOLD label for ITC next Monday, and the Monday after that, and very likely for the next 12 Mondays.

So what am I reading in weeks 2 through 12? The same label with the same reasoning, maybe lightly reworded. This is not a weekly investment planning tool — it is a quarterly review tool with a weekly delivery mechanism. Reading 12 identical reports per week will train me to stop reading them. And the one week that ITC's label changes from HOLD to WATCH, I will miss it because I have stopped paying attention.

The v0.1 spec has no concept of "nothing changed this week." There is no delta view, no "unchanged since last report" suppression, no "only show me what's new" option.

For a retail investor with 12 holdings, the correct weekly output is:
- **Delta-only view first**: "Changed since last week: ITC moved from HOLD to WATCH (F-Score dropped from 7 to 6, leverage up)." That is the only thing I read unless I want to dig deeper.
- **Full view on demand**: Accessible via drill-down, not pushed every week.

Without this, the weekly report will feel like spam after three weeks and the core behavioral value (catching the week something changes) will be lost.

**Fix (P1)**: Add a "delta mode" to the report spec. Each holding tracks its previous-week label and reasoning. The weekly report surface leads with changes only. Holdings with no label change since last week are listed as "No change — [HOLD/WATCH/REVIEW]" with a single line, not a full write-up. Only newly changed labels get the full 2–3 sentence reasoning. This dramatically reduces the cognitive load while preserving signal fidelity.

---

### NEW-5 — PSU pipeline gap is more severe than the synthesis implies for NIFTY 500 scope

The problem statement scopes the universe as NIFTY 500 equity. NIFTY 500 includes the following PSUs (government-majority-owned companies) as significant constituents: Coal India, ONGC, BPCL, IOC, NTPC, Power Grid, NHPC, NMDC, NALCO, SAIL, BHEL, BEL, HAL, IRCTC, Indian Railways Finance Corp, CONCOR, HUDCO, SJVN, and others. This is approximately 40–50 companies, or roughly 8–10% of the NIFTY 500 by count.

PSUs in India have structural behavioral differences from private-sector companies that break every gate in the v0.1 pipeline:

**Beneish on PSUs**: PSUs are required to follow government procurement and pricing directives. BPCL must buy crude at market rate and sell petrol/diesel at government-controlled prices. When oil prices spike, BPCL's receivables from the government for under-recovery compensation create exactly the DSRI and AQI elevation that Beneish flags as manipulation — but this is structured government policy, not earnings management. Beneish will false-positive on fuel PSUs whenever oil price environments change.

**Altman Z″ on PSUs**: Coal India, ONGC, BHEL all have Z″ above 5.0 from accumulated government reserves. This is structurally identical to the Tata Steel problem — except worse, because these companies also benefit from implicit government backstops. A Coal India Z″ of 9.0 means nothing about distress risk because the government will never let Coal India default. Altman's model has even less information content here than for private-sector conglomerates.

**Piotroski on PSUs**: PSU F-Score signals are heavily distorted by government directives. F7 (no dilution) — government does QIP or FPO of PSUs to meet disinvestment targets, creating dilution that is government-directed not management-driven. F5 (leverage decreasing) — NHPC, NTPC, Power Grid take on large amounts of debt for government-mandated capacity expansion, which the F-Score would flag as deterioration even when it is the exact right use of capital for an infrastructure company. F8 (gross margin improving) — BPCL/IOC gross margins fluctuate with oil price (which they cannot control) and under-recovery schedules.

**Promoter pledge on PSUs**: By definition, a PSU's promoter is the Government of India. The government cannot pledge shares. The pledge gate is always 0% for PSUs and provides zero information. The gate is irrelevant for approximately 40–50 NIFTY 500 names.

This is not a niche issue. NIFTY 500 scope means the bot WILL encounter Coal India, ONGC, NTPC, and SAIL. The v0.1 pipeline will produce labels for all of them, and those labels will be actively misleading because none of the four gates and none of the three scoring components have been calibrated for state-owned enterprise behavior.

**Fix (P0 for v0.2 if PSUs are in scope)**: Create a PSU classification gate (step 0, before BFSI) that flags government-majority-owned companies and applies at minimum a PSU-context warning to every output. Ideally, define which signals remain valid for PSUs and which must be suppressed or interpreted differently. At minimum, suppress the pledge gate (always 0%, always passes, never informative) and add a note: "Leverage signals may reflect government-mandated capex, not management financial decisions."

---

### NEW-6 — Liquidity floor is absent; the bot may recommend trimming a position you cannot exit

My holding in specialty chemicals includes some names that are NIFTY 500 constituents but have modest daily traded volumes. Even for NIFTY 500 names, there is a long tail of stocks with ADTV (average daily traded volume) below ₹5 crore. Some NIFTY 500 names have ADTV as low as ₹0.5–2 crore on quiet days.

Here is the practical problem: if v0.1 generates a FLAG label for one of these low-liquidity names, and I decide to act on it by trimming my position, I cannot sell a meaningful quantity without moving the price against myself by 2–3%. For a ₹2 crore ADTV stock where I hold ₹8 lakh of notional value (a 4% position in a ₹20 lakh portfolio), selling 50% of my position = ₹4 lakh sell order = 20% of one day's volume. That is a price-moving trade for a retail investor trying to execute at market.

The bot has no concept of this. It produces a FLAG label with the implicit action "consider exit." But exiting at market impact is a real cost that is invisible to a purely fundamental model.

This is not hypothetical. Phase 1 retail critique (06_critique_retail.md) mentions this same problem: "I have two stocks with average daily volumes so low that a 2% position for me is effectively illiquid. If I wanted to sell, I'd move the price. No screener or portfolio tool flags this." The bot needs to be different from Screener.in precisely on this dimension — and if it does not address it, it commits the same omission every other tool makes.

**Fix (P1)**: Add an ADTV floor check to the pipeline — ideally as a parallel data field in the output, not as a gate. The output for any holding should include: "ADTV = ₹X Cr (last 30-day average). At this volume, a 10% position reduction (~₹Y Cr) represents Z% of ADTV." When Z > 5%, add a LIQUIDITY-CAUTION note. When Z > 20%, add a LIQUIDITY-RISK note. This does not change the fundamental label — it contextualizes the actionability of the recommendation. A FLAG label with a LIQUIDITY-RISK note tells me "the bot thinks this is an exit candidate but you cannot easily exit." That is genuinely useful for a retail investor to know.

## 4. Proposed v0.2 changes — prioritized

### P0 — Cannot ship v0.2 without these

**P0-A: Downgrade Beneish from knockout gate to additive flag with Indian-context note.**
Not "M > -1.78 → halt pipeline." Instead: "M > -1.78 → add BENEISH-CAUTION flag, note most likely cause (regime shift / commodity structure / transition year), continue pipeline." The flag appears in the output alongside the F-Score label so the user can evaluate both. In the action label composition table, Beneish flag adds one level of caution (HOLD → WATCH, WATCH → REVIEW) but does not unilaterally halt and replace the label with FLAG: MANIPULATION-RISK. Mechanism: if Beneish flags AND F-Score is ≤ 4 AND at least one additional independent signal supports concern (pledge > 20%, FCF/NI < 0.7), THEN and only then escalate to FLAG.

**P0-B: PSU classification gate (step 0 before BFSI).**
Before any other gate, check government-majority ownership. If PSU: suppress pledge gate (always 0%, non-informative), add "PSU-CONTEXT: leverage signals may reflect government-mandated capital decisions; BFSI-equivalent stub output for govt-owned financial entities" to output. Do not attempt to score PSU leverage, dilution, or pledge signals as if they represent normal management behavior. This applies to ~40–50 NIFTY 500 names and prevents actively misleading outputs for a material fraction of the universe.

**P0-C: Produce a minimal BFSI stub output instead of a silent skip.**
SKIPPED-BFSI as a label is not acceptable for a user whose two largest holdings are banks. Minimum viable BFSI stub: pull latest quarterly NIM (vs prior quarter), GNPA (vs prior quarter), PCR (latest), CAR (latest). Classify as IMPROVING / STABLE / DETERIORATING on each dimension based on QoQ trend. Output as "BFSI-MONITOR: [bank name]: NIM trend: STABLE (4.2%, was 4.1%), GNPA trend: IMPROVING (1.3%, was 1.4%), PCR: 74% (adequate), CAR: 16% (above RBI minimum). No formal FA score — BFSI pipeline pending." This is achievable before a full BFSI pipeline is built and makes the report immediately more useful for my actual portfolio.

**P0-D: Transition-year suppression for YoY signals.**
Hardcode the following year-pairs as contaminated by Indian accounting transitions: FY2017→FY2018 (GST transition), FY2019→FY2020 (Ind AS 116 adoption). For any YoY signal (F2, F5, F6, F8, F9, DSRI, LVGI, AQI) that uses these contaminated pairs, flag the signal as TRANSITION-YEAR and exclude it from the F-Score count (do not score it 0 — exclude it, reducing the score denominator proportionally). This directly fixes the Asian Paints Mar-2020 false REVIEW caused by Ind AS 116 borrowings distortion in F5.

---

### P1 — Strong desirables for v0.2

**P1-A: NSE sector classification tier clarification — use Industry tier for ROCE percentile in heterogeneous sectors.**
Define a lookup: for Chemicals, Consumer Durables, Healthcare, Financial Services (where applicable) — use NSE Industry tier (tier 3) as the primary ROCE peer set. For homogeneous sectors (Metals & Mining, Oil & Gas) — use Sector tier. Publish the tier used for each holding's ROCE percentile in the output: "ROCE: 28% — 82nd percentile within Specialty Chemicals (Industry tier, N=14)." This directly fixes the specialty chemicals problem in my portfolio and is a 1-time classification table exercise.

**P1-B: Delta-only weekly report format.**
Track label and primary score (F-Score, FCF/NI band, ROCE percentile band) from the prior week's report for each holding. Lead the weekly report with a "Changes this week" section showing only holdings whose label or any primary metric changed. Holdings with no change are listed in a single table row: "ITC — HOLD — No change (F=7, FCF=HIGH, ROCE=68th pctile)." Full reasoning text only for changed labels. This is a report design change with zero math implications and directly prevents the weekly-spam problem.

**P1-C: Altman Z″ trend supplement for long-established companies.**
For companies with listing history > 15 years, add a secondary Z″ metric: current Z″ minus Z″ three years ago. If this delta is negative by more than 0.5 per year, flag as Z-DETERIORATING regardless of absolute threshold. For a company going from Z″=7.0 to Z″=5.5 over three years, the absolute threshold PASS tells the user nothing useful — the trend is the signal. Applies directly to ITC, Reliance, and the PSU names in the NIFTY 500.

**P1-D: ADTV liquidity floor as output field.**
Pull 30-day average daily traded volume (₹ Cr) for every holding. Add to output: "Liquidity: ADTV ₹X Cr — [HIGH/MEDIUM/LOW-CAUTION/LOW-RISK]." Thresholds: > ₹50 Cr = HIGH, ₹10–50 Cr = MEDIUM, ₹2–10 Cr = LOW-CAUTION (add market-impact caveat to any trim/exit recommendation), < ₹2 Cr = LOW-RISK (add explicit "position exit may require multiple days at significant market impact"). Does not change label logic — purely contextualizes it.

**P1-E: Data-quality completeness score per computation.**
For Beneish: report "8/8 indices computed" or "7/8 — SGAI missing (set to 0, systematic underestimate)" or "5/8 — multiple inputs from proxy data." For Piotroski: "9/9 signals computed" vs "8/9 — F7 dilution check inconclusive (share count data gap)." For FCF/NI: "3-year window complete" vs "2-year proxy used — FY201X OCF unavailable." This prevents silent false confidence in incomplete scores and is the single most impactful change for mid-cap data quality.

---

### P2 — Nice-to-have for v0.2

**P2-A: Cyclical sector tagging with F-Score interpretation modifier.**
For sectors tagged as CYCLICAL (Metals & Mining, Oil & Gas, some Consumer — Building Materials), add a label modifier: "F-Score 5/9 [at cyclical trough — sector ROCE at 10-yr low; trailing deterioration signals may not reflect forward trajectory]." For these sectors, do NOT automatically escalate to REVIEW at F ≤ 4 if ROCE percentile is below sector median FOR DOCUMENTED STRUCTURAL REASONS (trough, not deterioration). Still show REVIEW, but add a trough-context note so the user understands the mechanism.

**P2-B: Specialty chemicals sub-sector peer mapping.**
Create a lookup table: agrochemicals (PI Industries, Dhanuka, Sumitomo Chem India, Bayer CropScience, Sharda Cropchem), benzene-derivatives specialty (Aarti Industries, Vinati Organics, Deepak Nitrite), fluorochemicals (SRF, Navin Fluorine, Gujarat Fluorochemicals), diversified specialty (Atul Ltd). Use this sub-sector mapping for ROCE percentile when the parent Industry tier has N < 10. This is a one-time 30-row lookup table, not a complex calculation.

**P2-B: FCF/NI ratio cap at 3× with IMPAIRMENT-ANOMALY note above that.**
A CashConversion of 4.86× (Tata Steel FY2021 window) or 1.91× (Tata Steel 3-yr avg) does not mean "extremely high earnings quality" for a steel company. It means "large non-cash charges suppressed NI while OCF remained normal." Cap the displayed ratio at 3× and for values > 3×, note: "CashConversion > 3× — likely driven by non-cash impairment charges or large depreciation; interpret as earnings quality signal with caution for capital-intensive companies."

## 5. What v0.1 got RIGHT

- **The pipeline ordering is correct and NSE-appropriate.** Running gates before scores is the right architecture. A stock that fails Beneish (even as an additive flag) does not need a full Piotroski computation to be surfaced as a concern. The sequential design also gives a clear audit trail: a retail investor can step through "why did ITC get REVIEW?" and trace it to specific failing signals. This is exactly what distinguishes a reasoning tool from a tip service.

- **The promoter pledge gate is the most India-specific addition and it earns its place.** No Western FA framework includes this gate. Promoter pledge > 30% is a real forced-liquidation risk in Indian mid-caps (as seen in multiple NIFTY 500 companies in 2018 and 2022). The threshold of 30% is arguably conservative (the synthesis notes 50% as the correlation point) but erring early is the right call for a retail investor who cannot monitor margin calls on promoter holdings in real time. This gate has the highest signal-to-false-positive ratio of the four knockout gates.

- **The 3-year FCF/NI averaging is correct for Indian companies.** Single-year OCF can be distorted by lumpy capital cycles, working-capital timing, and quarterly reporting anomalies. For specialty chemicals (SRF, Aarti, PI Industries), where CapEx cycles create OCF swings, a 3-year average correctly smooths single-year anomalies. This is a design choice that shows genuine understanding of how Indian mid-caps behave.

- **The action label glossary distinguishes "what the label means" from "what to do."** The spec explicitly states: labels describe the company's fundamental state, not direct buy/sell instructions. HOLD = "no action needed beyond periodic reaffirmation," not "add more." REVIEW = "re-examine original thesis," not "sell." This is the correct framing for an advisory-only tool and is consistent with Q10 (thesis-entry framing) in the locked problem statement. A retail investor who understands this distinction will use the labels correctly; one who treats REVIEW as "sell signal" will not — but that is a UX communication problem, not a math problem.

## 6. One sentence to the synthesizer

"If you carry one thing forward, it should be: the bot silently skipping BFSI while calling itself a portfolio planning tool for an investor whose two largest holdings are banks is not an acceptable v0.1 limitation — it is a broken product promise that must be resolved with a minimal BFSI stub output before v0.2 ships to any real portfolio."
