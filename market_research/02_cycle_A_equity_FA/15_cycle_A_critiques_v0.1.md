# 15 — Cycle A: A.5 Critique Synthesis v0.1

**Status**: 🔄 §1–§5 complete; drafting §6 (A.6 brief) now
**Date**: 2026-05-30
**Inputs**: 4 critic outputs (15a–15d) + v0.1 math spec + 14_synthesis_v0.1
**Output target**: This document → drives A.6 (refine math to v0.2)
**Last updated**: 2026-05-30 T04 (§1–§5 complete)

---

## 1. Cross-critic verdict on v0.1 (top-line)

| Critic | Verdict | One-line rationale |
|---|---|---|
| C1 Quant | **REFACTOR-REQUIRED** | Pipeline architecture sound; signals inside broken for ~35–40% of NIFTY 500 (metals, energy, cement, infra); two knockout gates are correlated, not independent |
| C2 Forensic | **REFACTOR-REQUIRED** | Ind AS context almost entirely absent; gate structure unreliable; governance signals (restatements, auditor changes, RPTs) are entirely missing |
| C3 Behavioral | **REFACTOR-REQUIRED** | Action labels are miscalibrated behavioral nudges; no hysteresis; weekly cadence on quarterly signals generates harmful false oscillation; REVIEW is non-actionable |
| C4 Retail+NSE | **REFACTOR-REQUIRED** | Silent BFSI skip is a broken product promise for any portfolio with banks; PSU class is unaddressed; data quality gaps silently corrupt mid-cap scores |
| **Synthesized** | **REFACTOR-REQUIRED** | Unanimous. Pipeline structure is the one area of consensus strength. Every substantive component (all four gates, the primary signal, the label set, the cadence) requires targeted modification. v0.1 is usable as a prototype proof-of-architecture; it is not usable as a live signal for any real NIFTY 500 portfolio. |

---

## 2. Per-weakness consensus

### W1 — Beneish false positives during regime shifts

- **C1**: CONFIRM with quant precision. DSRI+AQI co-move defensively during macro liquidity crises (cash parking + debtor-day stretch). Asian Paints Mar-2022 crossed threshold by only 0.083 units — within measurement noise. Fix: two-period consecutive confirmation before HALT fires.
- **C2**: CONFIRM AND EXTEND. Identifies five Indian-specific regime-shift triggers: GST (FY2018), demonetization (FY2017), RERA (FY2017), Ind AS 115/109 (FY2019), energy shocks (FY2022). Fix: regime-shift calendar lookup + two-stage gate: borderline zone [−1.78, −1.50] requires corroborating governance flag before halting; M > −1.50 retains hard halt.
- **C3**: CONFIRM — behavioral cost larger than quant cost. False FLAG fires affect heuristic ("MANIPULATION-RISK" = immediate reputational contamination). Investor who exits on a false FLAG learns the wrong lesson. Fix: downgrade to additive flag; pipeline continues to F-Score.
- **C4**: CONFIRM — specialty chemicals growth-phase capex profiles (rising DEPI + high SGI) would structurally false-positive during peak investment phases. Fix: the only acceptable retail fix is additive flag + plain-language note explaining most likely cause.

**Consensus**: UNANIMOUS. Beneish as a hard knockout gate is broken. All four critics agree on the direction: downgrade toward additive or conditional halt.

**Key divergence**: C1 wants two-period confirmation (softened knockout). C2 proposes two-stage gate (clear breach = hard halt; borderline + governance corroboration = halt; borderline alone = warn). C3 and C4 want full additive downgrade. Synthesized recommendation: adopt C2's two-stage gate — it is the most structurally precise and preserves the hard halt for clear manipulators (M > −1.50 is unambiguous) while eliminating the regime-shift false positives that live in [−1.78, −1.50].

**Floor from 14_synthesis_v0.1**: P0. Confirmed P0. Fix is now more specific.

---

### W2 — Beneish false negatives for commodity firms

- **C1**: CONFIRM with mechanism re-specified. At cycle trough, GMI and TATA are structurally anti-correlated: margin collapse (GMI high) AND large non-cash charges (TATA most negative) occur simultaneously. Sector-conditional TATA coefficient: 4.679 → 2.0 for heavy-asset sectors (fixed-asset intensity > 50% OR D&A/Revenue > 8%).
- **C2**: CONFIRM. Impairment-adjusted TATA: TATA_adjusted = (NI + impairments − OCF_adjusted) / TA for capex-heavy sectors. Supplement with capex/D&A flag. Run Beneish on standalone financials for conglomerates (consolidated TA > 1.5× standalone TA) to prevent subsidiary impairment contamination of TATA term.
- **C3**: CONFIRM — false safety is behaviorally worse than false alarm. Stable M-Scores of −3.1 across 52 weeks train investor to trust a mathematically inert signal. Fix: annotation "M-Score has LOW SIGNAL POWER for this sector class" even when M passes.
- **C4**: CONFIRM — for companies where TATA alone drives M below −3.5, flag as BENEISH-INERT; substitute alternative manipulation screen (RPT volume, auditor tenure, restatements).

**Consensus**: UNANIMOUS. TATA suppression is the mechanism. Sector-conditional treatment required.

**Key divergence**: C1's coefficient adjustment (4.679 → 2.0) is simpler; C2's impairment-adjusted TATA is forensically more correct but requires note-level data. For v0.2: C1's coefficient as primary (implementable from ratios); C2's impairment annotation as secondary quality check; C4's BENEISH-INERT flag for extreme cases (TATA alone pushes M below −3.5).

**Floor from 14_synthesis_v0.1**: P0. Confirmed P0. Mechanism is now more precisely specified.

---

### W3 — Piotroski F-Score anti-correlated with cyclical entry

- **C1**: CONFIRM+QUANTIFY. Spearman = −1.0 on 4-date Tata Steel data. F2, F5, F8, F9 all co-move with commodity price cycle. Only F1, F3, F4, F7 are genuine quality signals for cyclicals. Proposes 5-signal "stable quality" routing for cyclical sectors (F1, F3, F4, F6, F7 — excluding the 4 cycle-driven signals).
- **C2**: CONFIRM+NUANCE. Cyclical inversion is partly out-of-sample application (Piotroski designed for low-P/B value stocks, not above-book cyclicals). Fix: normalize earnings inputs: use 3-year average EBIT for F1/F2/F3, 3-year average margin for F8, 3-year average asset turnover for F9 in commodity-cyclical sectors.
- **C3**: CONFIRM — worst behavioral failure. Bot's WATCH→HOLD transition (trough→peak) directly amplifies disposition effect: validates investor anxiety at the best entry point, validates confidence at the worst. 321 pp excess return destroyed in Tata Steel test alone.
- **C4**: CONFIRM+EXPAND SCOPE. Not limited to "designated cyclical sectors" — any company with construction/housing/auto revenue as primary driver faces this anti-correlation. Crompton and Astral (C4's actual holdings) would show the same pattern during construction downturns.

**Consensus**: UNANIMOUS and strongest agreement across all six weaknesses on severity. This is the most damaging structural failure.

**Key divergence**: C1 proposes 5-signal subset routing; C2 proposes normalized 3-year earnings. These are compatible. C4 expands the scope beyond the 3-4 narrow sector tags. For v0.2: implement C2's normalized inputs for labeled cyclical sectors (broader scope than initially thought) as primary, display C1's 5-signal quality score as secondary context, and document C4's scope concern for the sector-tag definition step.

**Floor from 14_synthesis_v0.1**: P0. Confirmed P0. Fix design is now more specific.

---

### W4 — Ind AS 116 breaks YoY signals

- **C1**: CONFIRM. F5 fail + LVGI inflation quantified. Fix: use financial debt only (exclude lease liabilities) for F5 and LVGI in transition year-pairs.
- **C2**: CONFIRM+EXTEND. Full Indian GAAP regime-shift calendar: Ind AS 116 (FY2020), Ind AS 115 (FY2019), Ind AS 109 (FY2019), GST (FY2018), demonetization (FY2017); upcoming Ind AS 117, revised Ind AS 1. Per-event neutralization rules specified for each. Ind AS 116 also affects Altman X1 (current lease liabilities in current liabilities).
- **C3**: CONFIRM — anchoring damage: a single false REVIEW at the COVID bottom corrupts the investor's reference-point framework for the stock for years post-event.
- **C4**: CONFIRM with scale dimension: NIFTY 500 mid-caps (KEI Industries, Crompton) have meaningful adoption-year balance sheet effects. Five-year-old distortion still in 3-year FCF/NI averaging window for some evaluation dates.

**Consensus**: UNANIMOUS. Regime-shift calendar approach is the right fix (hard-coded lookup table; not runtime estimation). All four critics support per-event signal neutralization rather than blanket suppression.

**Key divergence**: C1 says "zero out" affected signals. C4 says "exclude from score denominator" (proportional). C4's approach is more correct: zeroing a signal forces it to "fail," which penalizes the company; excluding it from the denominator produces a score on the remaining valid signals without penalizing for the accounting artifact. Recommend C4's denominator-adjustment.

**Floor from 14_synthesis_v0.1**: P0. Confirmed P0. Calendar scope expanded from Ind AS 116 only → full Indian GAAP history.

---

### W5 — Altman Z″ dominated by century-accumulated reserves

- **C1**: CONFIRM+QUANTIFY. X2+X4' = 53–67% of variable Z″ for Tata Steel, rising over time. Fix: replace X2 with X2_current = NPAT_TTM/TA. Add Net Debt/EBITDA as supplementary display.
- **C2**: CONFIRM+EXTEND. Second failure: Z″ uses book equity (X4') for NSE-listed companies; market cap is available and more informative — captures P/B collapse (the primary distress signal). Third: consolidated minority interest in book equity does not reflect subsidiary insolvency risk. Fix: replace Z″ with three-metric composite (ND/EBITDA < 5.0, Interest Coverage > 1.5, Current Ratio > 0.9) for companies >30 years old; replace X4' with Market Cap/TL for all listed companies.
- **C3**: CONFIRM — false-safe behavioral damage suppresses independent leverage analysis. Fix: display Net Debt/EBITDA alongside Z″ for every non-BFSI stock (mandatory context).
- **C4**: CONFIRM — PSU variant even more extreme (Coal India Z″ = 9.0+ yet faces structural government-pricing risk). Fix: for listing history >15 years, suppress absolute PASS/FAIL, replace with Z″ trend vs 3-year-ago.

**Consensus**: UNANIMOUS. Z″ is structurally unreliable for old Indian companies (majority of large-cap NIFTY 500 names).

**Key divergence**: C1's X2_current substitution preserves the Altman architecture; C2's composite replacement is a full model substitution for old companies. For v0.2: universal X2_current substitution (C1) + composite replacement gate for companies where accumulated reserves > 200% of EBITDA or listing >30 years (C2) + supplementary Net Debt/EBITDA display for all (C3). 14_synthesis_v0.1 classified this as P1; escalate to P0 because Tata Steel's Z″ was structurally inert across all 4 test dates.

**Floor from 14_synthesis_v0.1**: P1. Recommendation: escalate to P0.

---

### W6 — Sector ROCE percentile fails on small sectors

- **C1**: CONFIRM. Small-sector companies are disproportionately quality compounders; v0.1 rule specifically penalizes them. Fix: two-tier fallback (sub-sector → NSE Super-sector N≥15 → NIFTY 500 ROCE bracket ±5pp).
- **C2**: CONFIRM + ROCE consistency fix. Post-Ind AS 116: use financial debt only in Net Debt component of ROCE denominator for consistency. NSE Industry-level fallback proposed.
- **C3**: CONFIRM — behavioral: N/A ROCE prevents "thesis intact on capital efficiency" confirmation. Fix: for N < 10, show "Rank N of M" with peer values rather than "sector too small."
- **C4**: CONFIRM+STRUCTURAL POINT. v0.1 specifies NSE Sector tier (22 sectors) as the primary grouping — this is the BROADEST level and loses economic comparability within heterogeneous sectors (Chemicals mixes commodity and specialty; Healthcare mixes hospitals, pharma, diagnostics; Consumer Durables mixes electronics and paints). The primary grouping should be NSE Industry tier for heterogeneous sectors, with Sector as fallback.

**Consensus**: UNANIMOUS. C4's structural point is important: the problem is not just N-size but economic comparability. v0.1's choice of the broadest tier (22 sectors) as primary is wrong for heterogeneous sectors.

**Key divergence**: C1 and C2 both propose Industry-level fallback; C4 proposes Industry as PRIMARY for heterogeneous sectors. C4's approach is more correct. For v0.2: use Industry tier as primary for heterogeneous sectors (Chemicals, Healthcare, Consumer Durables); use Sector tier for homogeneous sectors (Metals & Mining, Oil & Gas); apply N-threshold fallback rules within this primary grouping.

**Floor from 14_synthesis_v0.1**: P1. Status unchanged — P1 — but fix is now more specific and primary grouping must change.

---

## 3. NEW concerns surfaced by critics (beyond W1–W6)

### Theme A — Gate correlation / false independence (C1 primary)
The pipeline architecture implies independent protection layers; the math does not deliver this. Beneish and Altman share three structural exposures (common Total Assets denominator; both sensitive to leverage changes; both sensitive to earnings quality). "Passed both gates" is not double-confirmation.
**Severity**: High. **Priority**: P1 (transparency annotation + Governance Screen provides genuine independence).

### Theme B — Governance Quality Screen absent (C2 primary; C4, C3 implicit)
In every major NSE manipulation case (IL&FS, Yes Bank, DHFL, Vakrangee, Manpasand Beverages), one or more of the following was present before blow-up: (1) auditor change from Big4 to smaller firm without reason, (2) restatement of financials in past 3 years, (3) RPT > 15% of revenue, (4) qualified audit opinion / emphasis-of-matter on going concern. None are in v0.1. SEBI EDGAR data is machine-readable. Genuinely independent of the correlated Beneish/Altman failures.
**Severity**: High. C2 rates P0; synthesized as P1 (data sourcing dependency). **Priority**: P1 (Gate 2.5 as additive warn; two simultaneous flags = halt).

### Theme C — Consolidated vs standalone for Beneish (C2 only)
For conglomerates (consolidated TA > 1.5× standalone TA): running Beneish on consolidated contaminates TATA term via subsidiary impairments; acquisition goodwill inflates AQI misleadingly.
**Severity**: Medium (affects large conglomerates primarily). **Priority**: P2.

### Theme D — Pledge gate LTV mechanics missing (C2 primary; C4 implicit)
30% static threshold ignores LTV dynamics. A promoter who pledged 5% six months ago and now has 25% (sudden increase) is more dangerous than a stable 25% pledger.
**Severity**: Medium. **Priority**: P2 for LTV; P1 for velocity (QoQ increase > 10pp).

### Theme E — F-Score action label table empirically uncalibrated (C1 primary; C3 implicit)
Three problems: (a) ≥7 HOLD threshold designed for value-portfolio context (Piotroski's original; not general NIFTY 500); (b) ROCE percentile ignored for F ≥ 7 but used as tiebreaker for F = 5–6 (Tata Steel F=8 HOLD with 21st-percentile ROCE); (c) knife-edge boundary cases at ROCE/FCF thresholds.
**Severity**: Medium-High. **Priority**: P1 (recalibrate routing table, especially ROCE ignored at F ≥ 7).

### Theme F — FCF/NI formula: impairment artifact inflation (C1 primary; C2, C4 secondary)
mean(OCF)/mean(NI) ≠ mean(OCF/NI). Single near-zero NI year produces arbitrarily large ratio. 4.86× and 1.05× labeled identically as "HIGH-QUALITY EARNINGS." No upper bound.
**Severity**: Medium. **Priority**: P1 (cap at 3.0× for routing; annotate above cap as IMPAIRMENT-CHECK; switch to mean(OCF/NI) formulation).

### Theme G — BFSI silent skip is a broken product promise (C4 primary; C2, C3 implicit)
HDFC Bank + ICICI Bank = C4's two largest holdings (~20–30% of portfolio). SKIPPED-BFSI = no output. Financial services = 35–40% of NIFTY 500 by market cap. Weekly planning tool that silently skips the largest sector in the index is structurally incomplete for any real portfolio.
**Severity**: High for real portfolios. **Priority**: P0 for minimal stub (NIM, GNPA, PCR, CAR trend flags).

### Theme H — PSU pipeline gap (C4 primary; C3 implicit)
~40–50 NIFTY 500 companies are government-majority-owned. PSUs break every gate: Beneish fires on BPCL when oil prices change government pricing (not manipulation); Altman Z″ = 9.0+ for Coal India; Piotroski penalizes government-mandated capex; pledge gate is always 0% (government doesn't pledge shares).
**Severity**: High at scale. **Priority**: P0 (simple lookup-table gate; suppresses irrelevant signals; adds PSU-CONTEXT annotation).

### Theme I — Mid-cap data quality corrupts scores silently (C4 primary; C1, C2 secondary)
Key problems: (1) SGAI is DATA-UNAVAILABLE for essentially the entire NIFTY 500 (nature-of-expenses P&L format; SGAI coefficient −0.172 systematically set to 0); (2) consolidation inconsistency for growing mid-caps; (3) data gaps near any threshold make binary PASS/FAIL unreliable for mid-caps.
**Severity**: Medium-High for SGAI (universal systematic bias). **Priority**: P1 (data-quality completeness score per output; SGAI missing = flag prominently in every Beneish result).

### Theme J — Weekly cadence wrong for FA signals (C3 primary; C4 secondary)
FA signals are quarterly by design. Weekly reports produce 12 identical outputs for 12 consecutive weeks. Three behavioral failure modes: habituation (investor stops reading), false expectation of weekly-fresh information, label oscillation amplification. C4: delta-only view needed.
**Severity**: Medium for math; High for product. **Priority**: P1 (cadence redesign + delta-view format; requires P0 hysteresis as prerequisite).

### Theme K — Hysteresis absent from label transitions (C3 primary; C4 implicit)
No hysteresis on HOLD/WATCH/REVIEW transitions means F-Score oscillation at 6–7 threshold generates false label flip every quarter. At weekly cadence, this = 3+ sell impulses per quarter for unchanged fundamentals.
**Severity**: High for behavioral product. **Priority**: P0.

### Theme L — REVIEW label is non-actionable (C3 primary; C4 implicit)
"Re-examine the original thesis" is not an instruction the bot supports with any structured output. For retail investors in losing positions, modal response = hold (loss aversion). REVIEW becomes "keep watching your losing position." C3 proposes structured checklist: which Piotroski groups failed, first vs nth occurrence, specific binary thesis question.
**Severity**: High for behavioral product. **Priority**: P0.

### Theme M — Liquidity floor absent (C4 only)
Some NIFTY 500 names have ADTV < ₹2 Cr. FLAG or REVIEW labels implicitly suggest action, but the investor cannot exit a meaningful position without significant market impact. The bot has no awareness of this.
**Severity**: Low-Medium for math; Medium for retail usability. **Priority**: P2.

---

## 4. Ranked v0.2 priorities — synthesized

### P0 — Unanimous or near-unanimous; cannot ship v0.2 without

**P0.1 — Beneish gate: two-stage conditional halt**
Replace single-threshold knockout with: (a) M > −1.50 → hard halt (MANIPULATION-RISK) regardless of context; (b) M ∈ [−1.78, −1.50] in a regime-shift year per calendar AND at least one governance corroboration flag fires → hard halt; (c) M ∈ [−1.78, −1.50] in a regime-shift year with no governance flag → WARN and continue pipeline; (d) M > −1.78 in a non-regime-shift year for two consecutive annual periods → hard halt; (e) single-year crossing in non-regime-shift year → context note only.
Raised by: C1, C2, C3, C4 (all four). 14_synthesis_v0.1: P0. Confirmed; fix is now specific.

**P0.2 — Regime-shift calendar (Indian GAAP transitions)**
Hard-coded lookup: demonetization (FY2017 year-pairs), GST (FY2018 year-pairs), Ind AS 115/109 (FY2019 year-pairs), Ind AS 116 (FY2020 year-pairs), COVID (FY2021–FY2022 year-pairs). Per-event signal exclusion from F-Score denominator (excluded, not zeroed; reduces denominator proportionally). Ind AS 116 adjusts: F5 uses financial debt only (exclude lease liabilities), Beneish LVGI uses financial debt only, Altman X1 excludes current portion of lease liabilities. GST adjustments: Beneish SGI and Piotroski F9 use 2-year average revenue growth (FY2017→FY2019) rather than single-year SGI.
Raised by: C1 (W4), C2 (W4), C3 (W4), C4 (W4). 14_synthesis_v0.1: P0 for Ind AS 116 only; expanded here to full Indian GAAP history.

**P0.3 — Piotroski: normalized inputs for cyclical sectors**
Tag list (CYCLICAL): Metals & Mining, Oil & Gas, Power, Fertilizers, and any company with > 40% revenue from construction/housing/auto (to capture C4's scope concern for Crompton, Astral class). For CYCLICAL-tagged companies: substitute F1/F2/F3 inputs with 3-year average EBIT/TA; substitute F8 inputs with 3-year average gross margin; substitute F9 inputs with 3-year average asset turnover. Display 9-signal raw score as context alongside the normalized score. Mandatory output caveat: "CYCLICAL-SECTOR: F-Score reflects trailing cycle position. Deteriorating signals at sector trough may precede best entry points."
Raised by: C1 (W3), C2 (W3), C3 (W3), C4 (W3). 14_synthesis_v0.1: P0. Confirmed; fix is now more specific.

**P0.4 — Beneish TATA: sector-conditional coefficient**
Heavy-asset sectors (Metals & Mining, Energy, Oil & Gas, Cement, Infrastructure — identifiable as fixed-asset intensity > 50% of TA OR D&A/Revenue > 8%): TATA coefficient = 2.0 (from 4.679). For companies where TATA alone drives M below −3.5 regardless of other seven indices: flag BENEISH-INERT in output; supplement with governance layer flags as the manipulation signal.
Raised by: C1, C2, C3, C4. 14_synthesis_v0.1: P0. Confirmed.

**P0.5 — Altman Z″: escalated to P0; replace X2 and add composite for old companies**
Universal change: replace X2 (Retained Earnings/TA) with X2_current (NPAT_TTM/TA). Replace X4' (book equity/TL) with Market Cap/TL for NSE-listed companies. For companies where accumulated reserves > 200% of current-year EBITDA OR listing history > 30 years: add composite check alongside Z″ (Net Debt/EBITDA < 5.0, Interest Coverage > 1.5, Current Ratio > 0.9 — all three must fail simultaneously for DISTRESS-RISK flag). Display Net Debt/EBITDA and Interest Coverage as mandatory supplementary fields for every non-BFSI stock regardless of Z″ result.
Raised by: C1 (P1 original), C2 (W5), C3 (W5), C4 (W5). 14_synthesis_v0.1: P1. Escalated to P0.

**P0.6 — Hysteresis on HOLD/WATCH/REVIEW label transitions**
All non-knockout label transitions (HOLD→WATCH, WATCH→REVIEW, and reverse) require 2 consecutive quarterly data releases confirming the same direction before label changes. Exception: knockout gates fire immediately. Output label must indicate stability: "HOLD (stable 3 quarters)" or "WATCH (1st consecutive — 1 more quarter needed to confirm trend)."
Raised by: C3 (NC1, P0), C4 (implicitly). Not in 14_synthesis_v0.1. P0 — without this, weekly cadence generates harmful false oscillation.

**P0.7 — BFSI minimal stub output (replace silent skip)**
Replace SKIPPED-BFSI with structured stub: NIM (current vs prior quarter), GNPA (current vs prior quarter), PCR (latest), CAR (latest), NIM TREND: IMPROVING/STABLE/DETERIORATING (QoQ), GNPA TREND: IMPROVING/STABLE/DETERIORATING. Label as "BFSI-MONITOR: no formal FA score — BFSI pipeline pending." Full BFSI pipeline deferred.
Raised by: C4 (P0), C2 (implicitly), C3 (implicitly). Not in 14_synthesis_v0.1. P0 for real portfolio with BFSI holdings.

**P0.8 — PSU classification gate (Gate 0, before BFSI)**
Before any other gate: check government majority ownership (central/state government holds > 50% of equity). If PSU: suppress pledge gate output (always 0%, non-informative), add PSU-CONTEXT annotation to leverage signals ("leverage may reflect government-mandated capex"), suppress F7 dilution interpretation ("government may conduct FPO for disinvestment targets"). ~40–50 NIFTY 500 names.
Raised by: C4 (NEW-5, P0). Not in 14_synthesis_v0.1. P0 — producing actively misleading outputs for 8–10% of NIFTY 500 by count is a correctness failure.

**P0.9 — REVIEW label: structured checklist output**
REVIEW must display: (a) which Piotroski group(s) failed (Profitability / Leverage / Efficiency); (b) whether it is first occurrence or nth consecutive quarter; (c) specific binary thesis question the investor needs to answer ("Has [the primary quality signal] changed durably?"). With P0.6 hysteresis: REVIEW fires only on confirmed 2-quarter deterioration; first-occurrence = WATCH-DETERIORATION-DETECTED.
Raised by: C3 (NC2, P0), C4 (implicitly). Not in 14_synthesis_v0.1. P0 — non-actionable REVIEW generates anxiety without direction.

---

### P1 — 3 of 4 critics agree; strong P1

**P1.1 — Governance Quality Screen (Gate 2.5, between Beneish and Altman)**
Check four indicators: (1) auditor change from Big4/reputable mid-tier → smaller firm in past 2 years without disclosed mandatory rotation reason; (2) any financial restatement in past 3 years covering revenue/receivables/goodwill/impairments; (3) RPT (purchases + sales to related parties) > 15% of revenue in most recent year; (4) qualified/adverse audit opinion OR emphasis-of-matter on going concern in most recent filed year. One flag = WARN and continue pipeline (append GOVERNANCE-CAUTION to output). Two or more flags firing simultaneously = HALT with FLAG: GOVERNANCE-RISK.
Raised by: C2 (P0), C4 (implicitly), C3 (implicitly). 14_synthesis_v0.1: not present. C2's P0; synthesized as P1 due to data sourcing dependency on SEBI EDGAR API.

**P1.2 — ROCE percentile: NSE Industry tier as primary for heterogeneous sectors**
Primary peer set: NSE Industry tier (tier 3) for Chemicals, Healthcare, Consumer Durables, Financial Services, and any sector where Economic-heterogeneity-within-Sector is documented. NSE Sector tier for homogeneous sectors (Metals & Mining, Oil & Gas). Fallback: if Industry-tier N < 10, fall back to Sector tier with note "broader peer set." If Sector N also < 10, show "Rank N of M: ROCE = X% vs [Company A: Y%, Company B: Z%]." ROCE consistency: use financial debt only (exclude Ind AS 116 lease liabilities) in Net Debt component for all data including FY2020+.
Raised by: C1, C2, C3, C4 (all four). 14_synthesis_v0.1: P1. Confirmed P1 with enhanced specificity.

**P1.3 — FCF/NI: cap at 3.0× and switch to mean(OCF/NI) formulation**
Cap CashConversion at 3.0 for routing purposes; annotate values above 3.0× as "IMPAIRMENT-CHECK: ratio may reflect large non-cash charges rather than earnings quality — investigate impairment schedule." Switch formula to mean(OCF_t/NI_t, OCF_{t-1}/NI_{t-1}, OCF_{t-2}/NI_{t-2}) (averaging ratios) rather than mean(OCF)/mean(NI) (ratio of averages) to prevent single near-zero NI year from dominating. Handle chronic-loss case (NI < 0 for denominator year) by excluding that year-ratio from the mean (reducing the averaging window).
Raised by: C1 (NC3, P1), C2 (P1.4), C4 (P2-B). Three critics. 14_synthesis_v0.1: not present. P1.

**P1.4 — Data-quality completeness score per computation**
Every Beneish output: display "X/8 indices computed." SGAI missing flag: "SGAI = 0 (default) — SG&A not disaggregated in Indian nature-of-expenses P&L format; systematic missing input across NIFTY 500; slight downward bias on M-Score." Every F-Score: "Y/9 signals computed" with reason for any missing signal. Every FCF/NI: window completeness note.
Raised by: C4 (NEW-2, P1), C1 (NC4), C2 (NCA). Three critics. 14_synthesis_v0.1: not present. P1.

**P1.5 — Delta-view weekly report format**
Lead weekly report with "Changes this week" section: only holdings whose label or any primary metric changed since last week. Holdings with no change: single table row "ITC — HOLD — No change (F=7, FCF=HIGH, ROCE=68th pctile — last updated [date])." Full reasoning text only for changed labels. FA module status line in weekly report: "FA: HOLD — last updated [date of last quarterly data incorporation]."
Raised by: C3 (NC4, P1), C4 (NEW-4, P1). Two critics. 14_synthesis_v0.1: not present. P1 (requires P0.6 hysteresis as prerequisite).

**P1.6 — Pledge gate: add velocity dimension**
Two-factor gate: (1) absolute threshold: pledge > 40% of promoter holding → WARN; (2) velocity threshold: pledge increased > 10pp QoQ, or pledge > 20% and increased for two consecutive quarters → WARN; (3) both simultaneously → HALT with FLAG: PLEDGE-RISK. Add PLEDGE-LTV-CAUTION when pledging price context was materially above current price (last filed pledge date stock price > 30% above current). Absolute threshold relaxed from 30% → 40% (30% catches too many stable long-standing pledges; velocity is the more dangerous signal).
Raised by: C2 (NCC, P2 originally), C4 (PSU note implicitly). 14_synthesis_v0.1: not present. Upgraded to P1 given velocity is the forensically more dangerous signal.

**P1.7 — Action label composition table: fix ROCE blind spot at F ≥ 7**
Recalibrate routing table: ROCE percentile should not be ignored for F ≥ 7. Proposed fix: F ≥ 7 + FCF/NI ≥ 1.0 + ROCE ≥ 60 = HOLD; F ≥ 7 + FCF/NI ≥ 0.7 + ROCE ≥ 40 = HOLD; F ≥ 7 + ROCE < 40 = WATCH (regardless of FCF/NI — strong momentum but weak capital efficiency, consistent with cycle-peak reading). This prevents the Tata Steel F=8 HOLD at 21st-percentile ROCE scenario.
Raised by: C1 (NC2, P2), C3 (implicitly). Two critics. 14_synthesis_v0.1: not present. P1.

---

### P2 — 2 of 4 critics or single strong specialist

**P2.1 — Beneish standalone for conglomerates** (C2 only; affects large conglomerates). Run Beneish on standalone financials when consolidated TA > 1.5× standalone TA. Flag BENEISH-STANDALONE. Flag consolidated goodwill + intangibles > 20% of consolidated TA as GOODWILL-CONCENTRATION.

**P2.2 — F4 materiality buffer** (C1 + C2). OCF > 1.03×NI = pass; OCF in [0.97×, 1.03×] = tie-breaker; OCF < 0.97×NI = fail. Extend 1% materiality buffer to F2, F5, F8, F9.

**P2.3 — Gate correlation transparency note** (C1). For any stock passing both Beneish and Altman: add output note that dual-pass is not independent confirmation.

**P2.4 — ADTV liquidity floor as output field** (C4). 30-day ADTV alongside any trim/exit flag. ADTV < ₹2 Cr = LOW-RISK (explicit market-impact caveat). Does not change label logic.

---

### P3 — 1 critic; defer

**P3.1** — Specialty chemicals sub-sector peer mapping lookup (C4): one-time 30-row table; defer to v0.2 iteration.
**P3.2** — Z″ trend vs 3-year-ago for old companies (C4): covered by P0.5 X2_current substitution effect.
**P3.3** — Beneish multi-year display (C1): partially addressed by P0.1 two-period confirmation requirement.

---

## 5. What v0.1 got RIGHT (cross-critic consensus)

1. **Pipeline architecture (gate → primary → overlay → action label) is the correct design pattern.** All four critics praised the sequencing logic. Architecture correctly separates "can we trust the numbers?" from "what do the numbers say?"

2. **Consolidated financials as locked convention** is correct and consequential for conglomerates like Tata Steel (European operations invisible in standalone). C2 qualifies this for Beneish specifically (BENEISH-STANDALONE for large conglomerates), but endorses consolidated for F-Score and ROCE.

3. **FCF/NI 3-year averaging is anti-recency-bias by design.** C1 praises OCF over FCF (avoids CapEx-cycle sensitivity). C2 notes the averaging correctly absorbed Asian Paints FY2022 OCF anomaly. C4 confirms this applies to specialty chemicals with lumpy CapEx.

4. **Promoter pledge gate is the most India-specific addition and earns its place.** No Western FA framework includes this. All four critics preserve it (with refinements). C3 notes it is a well-calibrated use of a hard-stop gate, unlike Beneish where hard-stop is miscalibrated.

5. **The reasoning string design (traceable derivation per output) is correctly specified.** C3 strongly endorses this: "a label with a visible derivation is a tool the investor can interrogate." All four critics assume this transparency structure in their fix proposals.

6. **BFSI exclusion gate: correctly designed and correctly placed.** Applying Piotroski/Beneish/Altman to banks would produce meaningless outputs. SKIPPED-BFSI is honest about scope. The criticism is of the silent skip (no stub output), not of the exclusion logic.

7. **Action label glossary correctly distinguishes state description from instruction.** "HOLD = no action needed" is not "add more." C4 notes this is the correct framing for an advisory-only tool. The label definitions are correct; the thresholds and transitions need work.

8. **ROCE as the primary capital-efficiency metric for NSE quality investing is the right choice.** C1 and C4 both confirm ROCE is the single most-cited capital-efficiency ratio in Indian quality investing (Mukherjea, MOSL, MSCI Quality). The issue is implementation of the peer set, not the metric choice.

---

## 6. Specific math changes for A.6 — the v0.2 refactor brief

A.6 should read this section and produce `16_cycle_A_math_v0.2.md`. Each sub-section is a prescription.

### 6.1 Knockout gates

**BFSI gate**: Keep as silent skip for the FA pipeline. ADD: minimal stub output for BFSI stocks (NIM trend, GNPA trend, PCR, CAR — per P0.7). The exclusion logic is correct; the zero-output behavior is not.

**PSU gate**: ADD Gate 0 (before BFSI): Check government majority ownership. If PSU: (a) suppress pledge gate, (b) add PSU-CONTEXT annotation to all leverage/dilution signals, (c) suppress F7 dilution interpretation. Keep running F-Score and ROCE (with PSU-CONTEXT annotations); do not halt the pipeline for PSUs.

**Beneish gate**: REPLACE current single-threshold knockout with a two-stage conditional structure:
- Stage 1: Compute M-Score using sector-conditional TATA coefficient (see §6.2).
- Stage 2: Apply conditional halt logic:
  - M > −1.50 → hard halt: FLAG: MANIPULATION-RISK (no regime-shift exception; this is clear breach territory)
  - M ∈ [−1.78, −1.50] + year-pair in regime-shift calendar + at least one Governance Quality Screen flag fires → hard halt: FLAG: MANIPULATION-RISK
  - M ∈ [−1.78, −1.50] + year-pair in regime-shift calendar + no governance flag → WARN: BENEISH-CAUTION (pipeline continues; flag added to output)
  - M > −1.78 for two consecutive annual periods + year-pair NOT in regime-shift calendar → hard halt: FLAG: MANIPULATION-RISK
  - M > −1.78 for single year + NOT in regime-shift calendar → context note: "Beneish M-Score elevated — review DSRI and AQI drivers"; pipeline continues
  - BENEISH-INERT flag: when TATA contribution alone would push M below −3.5 regardless of other 7 indices (i.e., for companies where D&A/Revenue > 15% and impairments are material): flag BENEISH-INERT; do NOT report a PASS; instead report "M-Score has low signal power for this sector class — governance layer flags substituted."

**Governance Quality Screen (Gate 2.5)**: ADD new gate between Beneish and Altman:
- Check 4 indicators from SEBI EDGAR / NSE XBRL: auditor change from Big4/reputable mid-tier → smaller firm in past 2 years without disclosed mandatory rotation; restatement of revenue/receivables/goodwill in past 3 years; RPT > 15% of revenue; qualified/adverse audit opinion or emphasis-of-matter on going concern.
- One flag → GOVERNANCE-CAUTION (WARN, pipeline continues, flag in output).
- Two or more flags simultaneously → FLAG: GOVERNANCE-RISK (halt).

**Altman Z″ gate**: MODIFY as follows:
- Universal change: replace X2 (Retained Earnings/TA) with X2_current (NPAT_TTM/TA). Replace X4' (Book Equity/TL) with Market Cap/TL for all NSE-listed companies.
- For companies where accumulated reserves > 200% of current-year EBITDA OR listing history > 30 years: run the three-metric composite alongside (not instead of) modified Z″. Composite thresholds: Net Debt/EBITDA > 5.0 AND Interest Coverage < 1.5 AND Current Ratio < 0.9 (all three) = FLAG: DISTRESS-RISK. Either composite or modified Z″ trigger = halt.
- Supplementary mandatory display for all non-BFSI, non-PSU stocks: Net Debt/EBITDA (label: "Elevated" if > 4.0×, "High" if > 6.0×) and Interest Coverage (EBIT/Interest Expense, label: "Low" if < 2.0).
- For companies in the Z″ grey zone [1.1, 2.6]: retain context note (no halt, but record in output) — no change from v0.1.

**Promoter pledge gate**: REPLACE static threshold with two-factor gate:
- Absolute: pledge > 40% of promoter holding → WARN.
- Velocity: pledge increased > 10pp QoQ, OR pledge > 20% and increased for two consecutive quarters → WARN.
- Both simultaneously → halt: FLAG: PLEDGE-RISK.
- PLEDGE-LTV-CAUTION flag: if last pledge filing price (at filing date) was > 30% above current price → add PLEDGE-LTV-CAUTION (WARN, no halt).
- PSU: pledge gate suppressed (see PSU gate above).

---

### 6.2 Beneish formula

**Sector-conditional TATA coefficient** (P0.4):
```
For non-heavy-asset sectors: coefficient = 4.679 (unchanged)
For heavy-asset sectors (Metals & Mining, Energy, Oil & Gas, Cement, Infrastructure
  — identifiable as fixed-asset intensity > 50% of TA OR D&A/Revenue > 8%):
  coefficient = 2.0
```
All other coefficients unchanged.

**TATA term computation**: Use consolidated financials for standalone-comparable companies. For Beneish specifically: if consolidated TA > 1.5× standalone TA (conglomerate), compute TATA on standalone financials and flag BENEISH-STANDALONE in output. This is P2.1 and can be added after the core coefficient change.

**SGAI default handling**: SGAI is DATA-UNAVAILABLE for virtually all NIFTY 500 companies (nature-of-expenses P&L format). Set SGAI = 0 (current default is unchanged) but explicitly flag in every Beneish output: "SGAI = 0 (default) — SG&A not disaggregated under Indian Companies Act Schedule III format; coefficient −0.172 contribution = 0; slight downward M-Score bias." Do NOT try to impute SGAI from other data — zero with explicit annotation is more honest than an imputed estimate.

**Regime-shift year-pair adjustments within Beneish**:
- FY2019/FY2020 year-pair: compute LVGI using financial debt only (Total Borrowings − Lease Liabilities per Ind AS 116 notes). Separately, compute AQI excluding right-of-use assets added to PPE at transition, if the company reports the transition-year impact separately (as required under Ind AS 116 transition disclosures). If ROU assets cannot be separated: flag LVGI as TRANSITION-YEAR in output.
- FY2017/FY2018 year-pair: use 2-year average revenue growth (FY2017→FY2019) for SGI rather than single-year revenue ratio, to avoid GST-driven SGI distortion.

---

### 6.3 Piotroski for cyclicals

**CYCLICAL sector tag list** (to be maintained as a lookup table, not hardcoded):
Primary: Metals & Mining, Oil & Gas, Power, Fertilizers.
Extended (per C4): any company with > 40% revenue concentration from: construction contracts (EPC, infrastructure, housing), automotive OEM or auto-ancillary, housing/real estate.

**Behavior for CYCLICAL-tagged stocks**:
- Compute the full 9-signal F-Score as before. Display it as "F-Score (cycle-adjusted): X/9."
- For signals F1, F2, F3 (ROA-based): substitute 3-year average EBIT/TA in place of single-year NI/TA for the underlying computation.
- For signal F8 (gross margin change): substitute 3-year average gross margin.
- For signal F9 (asset turnover change): substitute 3-year average asset turnover.
- The 4-signal "stable quality" subset (F1, F3, F4, F7 per C1 — these are the signals that do NOT co-move with commodity prices) should be computed and displayed as secondary context: "Stable-quality signals (non-cycle-sensitive): X/4."
- Mandatory output caveat: "CYCLICAL-SECTOR: F-Score reflects trailing cycle position. Deteriorating F-Score at sector trough may precede best entry points. Compare current ROCE and margins to 10-year median before reducing position."
- Action label routing for cyclical stocks: use the normalized (3-year average input) score for routing, not the raw single-year score.

**Secular sectors**: unchanged from v0.1.

---

### 6.4 Ind AS / accounting transition handling (Regime-Shift Calendar)

Create a permanent data structure (lookup table) used by the pipeline before computing any YoY signal. This table is the "Regime-Shift Calendar."

| Event | Affected year-pairs | Affected signals | Neutralization rule |
|---|---|---|---|
| Demonetization | FY2016/FY2017 | Beneish DSRI, Beneish SGI, Piotroski F9 | Flag DEMONETIZATION-YEAR; exclude from F-Score denominator |
| GST introduction | FY2017/FY2018 | Beneish SGI, Piotroski F9 (asset turnover) | Use 2-yr avg revenue FY2017→FY2019 for SGI and F9; flag GST-TRANSITION |
| Ind AS 115 (revenue recognition) | FY2018/FY2019 (EPC, real estate, telecom, retail primarily) | Beneish SGI, Piotroski F9 | Flag IND-AS-115-TRANSITION; exclude from denominator for affected sectors |
| Ind AS 109 (financial instruments / ECL) | FY2018/FY2019 (companies with large receivables books: capital goods, infra, EPC) | Beneish DSRI, Piotroski F1/F2 (ECL provision hits NI) | Flag IND-AS-109-TRANSITION; exclude F1/F2 from denominator for affected sectors |
| Ind AS 116 (leases) | FY2019/FY2020 (all listed companies with material leases) | Piotroski F5, Beneish LVGI, Altman X1 | F5: use financial debt only (Total Borrowings − Lease Liabilities per Ind AS 116 notes); Beneish LVGI: same; Altman X1: exclude current portion of lease liabilities from current liabilities |
| COVID lockdowns | FY2020/FY2021, FY2021/FY2022 | Beneish DSRI, Beneish AQI | These year-pairs are already registered as regime-shift windows for Beneish two-stage gate (§6.1); signal context note added |

**Application rule**: Before computing each YoY signal pair (t, t-1): check if the pair appears in the Regime-Shift Calendar. If yes and the signal is in the "affected signals" list: apply the neutralization rule. If neutralization = "exclude from denominator," subtract 1 from the F-Score denominator for that evaluation date (maximum F-Score denominator decreases proportionally; percentage score displayed rather than /9 when signals are excluded, e.g., "7/8 signals computed (1 excluded: Ind AS 116 transition)").

---

### 6.5 Altman Z″ for old firms

**Prescription**: (incorporated in §6.1; restated here for A.6 reference)

Universal modifications (all companies):
- X2: Retained Earnings/TA → X2_current: NPAT_TTM/TA (same Altman coefficient 3.26 applied to new variable)
- X4': Book Equity/TL → Market Cap/TL (for NSE-listed companies; same Altman coefficient 1.05 applied)

Additional composite check for old/reserve-dominated companies (condition: accumulated reserves > 200% of EBITDA TTM OR company has been operating > 30 years):
- Run three-metric composite in parallel: Net Debt/EBITDA < 5.0, Interest Coverage > 1.5, Current Ratio > 0.9
- Composite halt condition: ALL THREE fail (not just one or two — this preserves the probabilistic nature)
- Either modified Z″ breach OR composite breach → FLAG: DISTRESS-RISK

Supplementary display (mandatory for all non-BFSI stocks):
- Net Debt/EBITDA TTM, labeled "Elevated (>4×)" or "High (>6×)" when applicable
- Interest Coverage (EBIT/Interest Expense), labeled "Low (<2.0×)" when applicable

---

### 6.6 Sector percentile small-N

**Primary grouping change** (P1.2):

Define a tier-selection lookup table for each NSE sector:
- Heterogeneous sectors (economic sub-categories are not comparable): use NSE Industry tier (tier 3) as primary. Sectors: Chemicals, Healthcare, Consumer Durables, Financial Services, IT, Diversified Industrials.
- Homogeneous sectors: use NSE Sector tier (tier 2) as primary. Sectors: Metals & Mining, Oil Gas & Consumable Fuels, Power, Fertilizers.

**Fallback rules** (applied sequentially):
1. Primary tier (per above): if N ≥ 10 → compute percentile; if N < 10 → go to step 2.
2. One tier up from primary (Industry → Sector → Macro): if N ≥ 10 → compute percentile with note "expanded peer set: [tier name]"; if N < 10 → go to step 3.
3. Explicit peer display: show "Rank N of M within [tier]: ROCE = X% vs [Company A: Y%, Company B: Z%]." This is interpretable even at N = 4. Include all companies in the tier, not just the top-N.

**ROCE consistency across Ind AS 116 transition**:
- For all evaluation dates using balance sheets that include FY2020 or later: compute Net Debt in ROCE denominator using financial debt only (Total Borrowings − Lease Liabilities). Label: "ROCE (financial debt basis, comparable across Ind AS 116 transition)."
- For evaluation dates using FY2019-only balance sheets: compute Net Debt using total borrowings. Label: "ROCE (total borrowings basis, pre-Ind AS 116)."
- Do not mix the two bases within a sector peer set for the same evaluation date — all peers in the same cohort must use the same Net Debt convention for a given date.

---

### 6.7 Action label set

**Label set**: KEEP the four existing non-gate labels (HOLD / WATCH / REVIEW / FLAG) but with the following changes:

1. **Add AFFIRM as a label between HOLD and WATCH**: for stocks at F ≥ 8, FCF/NI ≥ 1.0, ROCE ≥ 75th percentile, no governance flags, no Beneish warnings. This signals "actively high-quality, not just passing" and gives the investor a positive signal distinct from the neutral HOLD. Optional for v0.2 — Pranav's call.

2. **Add hysteresis** (mandatory, P0.6): all transitions between HOLD, WATCH, and REVIEW require 2 consecutive quarterly data releases confirming the direction. First-occurrence deterioration = WATCH-DETERIORATION-DETECTED (not REVIEW). Label output format: "HOLD (stable 3 quarters)" or "WATCH-DETERIORATION-DETECTED (1st consecutive — 1 more quarter needed to confirm WATCH)."

3. **REVIEW label**: must include structured checklist output per P0.9. REVIEW only fires on confirmed 2-quarter deterioration.

4. **WATCH label**: for cyclical-sector stocks, append "CYCLICAL-SECTOR WARNING: deteriorating F-Score at sector trough may indicate entry opportunity, not deterioration" (P1.6 — C3's behavioral fix).

5. **ROCE ignored at F ≥ 7**: fix per P1.7 — ROCE percentile must be factored at all F-Score levels, not just F = 5–6. Recalibrate routing table accordingly.

**Retain HOLD/WATCH/REVIEW/FLAG as the top-level label set.** Do not restructure the entire set. The AFFIRM addition is a P2/optional enhancement.

---

### 6.8 Cadence / refresh

**Prescription** (balancing Q9 locked decision with C3/C4 concerns):

The v0.3 problem statement locks weekly cadence (Q9). This cannot be changed at the math level. However, the FA module's behavior within the weekly report should be:

- FA signals are quarterly-data-event-driven, not weekly-data-driven.
- The FA module outputs a label that ONLY CHANGES when new quarterly results (or a new governance flag from SEBI EDGAR) have been incorporated.
- The weekly report MUST include an FA status line format: "FA: HOLD — last data: Q4 FY2026 (incorporated 2026-05-15). No change this week."
- Weekly report leads with a "Changes this week" section (delta-view per P1.5): only holdings that have changed their FA label since last week get full write-up. Holdings unchanged get a single table row.
- Hysteresis (P0.6) ensures that the FA label only changes when 2 consecutive quarterly data releases confirm the direction — this eliminates the false oscillation at the quarterly boundary.

**Do not propose changing the Q9 weekly cadence to monthly.** The problem statement locks this. The fix is within the FA module's behavior, not the report cadence.

---

### 6.9 New components for v0.2

**Governance Quality Screen** (P1.1 — required in v0.2):
Gate 2.5. Four checks: auditor change, restatement history, RPT concentration, audit opinion. One flag = WARN. Two+ = HALT. Data sources: SEBI EDGAR, NSE XBRL, Screener.in annual report disclosures. If data source unavailable for a specific company: flag DATA-UNAVAILABLE for that check (do not fail it silently).

**BFSI stub output** (P0.7 — required in v0.2):
Format: BFSI-MONITOR section with NIM (QoQ trend), GNPA (QoQ trend), PCR (latest), CAR (latest), per-dimension IMPROVING/STABLE/DETERIORATING classification. No formal FA score. Clear disclaimer: "Full BFSI pipeline pending — these trend indicators do not constitute a formal assessment."

**PSU classification** (P0.8 — required in v0.2):
Gate 0 lookup table: list of NIFTY 500 companies with government majority ownership. Suppresses pledge gate; adds PSU-CONTEXT annotations; does not halt the pipeline.

**Data-quality completeness score** (P1.4 — required in v0.2):
Every output (Beneish, F-Score, FCF/NI): add a completion score (X/N computed). SGAI: always flagged as "0 (default) — systematic across NIFTY 500."

**Liquidity floor ADTV display** (P2.4 — optional in v0.2):
30-day ADTV (₹ Cr) alongside any trim/exit flag. ADTV < ₹2 Cr = explicit market-impact caveat.

---

## 7. Idea-review trigger check

Reviewing each potential v0.4 problem-statement update against the v0.3 locked decisions in `08_decisions_locked.md`:

### Asset universe (NIFTY 500 scope)
**Context**: W6 + specialty chemicals quality-compounder problem. C4 raises scope concerns about NSE classification quality for sub-sectors.
**Finding**: The critics do not recommend trimming the universe from NIFTY 500 to NIFTY 250. Instead, they recommend: (1) better sector tier selection (Industry vs Sector primary), (2) PSU-CONTEXT annotation rather than exclusion, (3) BFSI stub rather than exclusion. The NIFTY 500 scope is retained.
**VERDICT**: No change to problem statement. Math v0.2 accommodates the full NIFTY 500 with appropriate sector tier logic, PSU gate, and BFSI stub.

### Time horizon (B1 primary, B2 for timing)
**Context**: W3 cyclical inversion changes what FA signals mean for cyclical entry timing.
**Finding**: W3's fix (normalized 3-year average earnings for cyclicals) reduces the signal inversion without requiring a change to the B1/B2 time-horizon framing. The problem statement's "B1 primary, B2 only for entry/exit timing" remains correct. The FA layer (Cycle A) is exclusively about the company's fundamental state; the time-horizon framing (when to enter a cyclical) belongs to the eventual combination of FA + TA in Cycle F.
**VERDICT**: No change. Cyclical-sector normalized Piotroski is the v0.2 fix; time-horizon re-specification is not needed.

### TA/FA conflict (Q5 context-sensitive prompt)
**Context**: Critics have not changed the analysis of how TA/FA conflict should be resolved. C1's cyclical-inversion finding is a pure FA calibration problem, not a TA/FA conflict.
**Finding**: No new evidence changes the Q5 decision ("context-sensitive prompt with holding-period framing"). The FA signals themselves need calibration; once calibrated (v0.2), the conflict resolution approach remains appropriate.
**VERDICT**: No change.

### Output cadence (Q9 weekly)
**Context**: C3 and C4 both push back strongly on weekly cadence for FA signals. C3 provides a detailed behavioral argument. C4 describes the practical weekly-spam problem.
**Finding**: The critics have a valid point: FA signals are quarterly-data-event-driven, not weekly. However, the fix does not require a problem-statement change — it requires a behavioral rule within the FA module: delta-view, hysteresis, "last updated" date in weekly report. This is entirely implementable within the v0.3 weekly cadence constraint. The problem statement says "weekly structured report" — it does not say "all components of the report must be recalculated weekly." The FA module can be a sub-component that updates on event triggers while still being surfaced in the weekly report.
**VERDICT**: No change to problem statement. Implement delta-view and event-driven FA update semantics within v0.2 math spec. If the bot eventually builds a distinct cadence per module, that is a v0.2 math decision — not a v0.4 problem-statement change.
**Note**: This is a borderline case. If Pranav feels the weekly-cadence-for-FA issue warrants a problem-statement clarification (e.g., "weekly report, but FA module updates on quarterly event trigger"), a minor v0.4 clarification is reasonable but not required for A.6 to proceed.

### BFSI in scope (Q8)
**Context**: v0.1's silent skip + critics' verdict (C4 P0, C2 and C3 implicitly) on stub output requirement.
**Finding**: The problem statement does not explicitly exclude BFSI from the FA pipeline — it is v0.1's math spec decision (Section 2.1: "v0.2 will implement a parallel BFSI pipeline"). The v0.3 problem statement says "NSE direct equity: NIFTY 500 for fundamentals." BFSI is part of NIFTY 500. The problem statement technically requires coverage of BFSI. v0.2 should fulfill this with the minimal stub output (P0.7). A full BFSI FA pipeline (P/ABV, NIM, GNPA, PCR, CAR) should be explicitly scoped as a v0.2 deliverable or deferred to a named future Cycle A iteration.
**VERDICT**: Suggest update — recommend adding one line to the problem statement (v0.4 update, minor): "Cycle A FA pipeline covers NIFTY 500 including BFSI; v0.2 delivers a BFSI stub (trend indicators only) with a full BFSI pipeline in v0.3." This makes the staging explicit rather than implicit.

---

## 8. Open questions for Pranav (decisions A.6 needs)

**Q1: Beneish gate design — which of the following should A.6 implement?**
(a) C2's two-stage gate: M > −1.50 = hard halt; M ∈ [−1.78, −1.50] + regime-shift + governance flag = halt; otherwise continue [recommended by synthesizer — most precise]
(b) C3/C4's full additive downgrade: Beneish M-Score is never a halt; always adds a downgrade modifier to the label
(c) C1's two-period confirmation: single year M > −1.78 = context note only; two consecutive years = halt

**Default recommendation**: (a). Preserves hard halt for clear manipulators (M > −1.50 is above the zone where regime-shift false positives occur); eliminates the false halt problem in the COVID-era false-positive zone.

---

**Q2: Piotroski cyclical sector tag list — how broad should "cyclical" be?**
(a) Narrow: Metals & Mining, Oil & Gas, Power, Fertilizers [~50–60 NIFTY 500 companies]
(b) Broader (C4 recommendation): add any company with > 40% revenue from construction/housing/auto [adds Crompton, Astral, Kajaria, Voltas class — ~80–100 NIFTY 500 companies]
(c) Even broader: include all companies in sectors with commodity-price-linked revenue (adds chemical intermediates, paints upstream)

**Default recommendation**: (b). The normalized F-Score logic is sound for any business where YoY signals are structurally driven by external cycle position. C4's holding-specific examples (Crompton, Astral) demonstrate the real cost of too-narrow tagging.

---

**Q3: Altman Z″ replacement for old companies — which approach?**
(a) C1's X2_current substitution only: keep the Altman architecture but replace accumulated reserves with current-period earnings [simpler, universal]
(b) C2's composite replacement for old companies (>30 years or reserves > 200% of EBITDA): run three-metric composite (ND/EBITDA, Interest Coverage, Current Ratio) as the actual halt trigger for those companies [more forensically correct; two-model overhead]
(c) Both: X2_current universally + composite for old-company condition as additional check

**Default recommendation**: (c). X2_current is a universal improvement with low risk (replaces a structurally wrong variable with a better one, same coefficient). The composite adds a second line of defense precisely where the modified Z″ is still dominated by historical balance sheet items. The three-metric composite is standard credit analysis and data is available from the same source.

---

**Q4: BFSI stub output — what is the minimum viable version for v0.2?**
(a) Qualitative trend card only: NIM, GNPA, PCR, CAR — IMPROVING/STABLE/DETERIORATING per metric, QoQ comparison [achievable from quarterly earnings call summaries or Screener.in]
(b) Quantitative: actual NIM %, GNPA %, PCR %, CAR % pulled from structured data source
(c) Defer BFSI stub entirely — acknowledge the gap but don't create a placeholder that could be misconstrued as a real score

**Default recommendation**: (b), with a prominent "no formal FA score" disclaimer. Quantitative figures are more useful than qualitative IMPROVING/STABLE/DETERIORATING and are available from Screener.in for listed banks. Without the stub, HDFC Bank and ICICI Bank produce zero output — which C4 correctly identifies as a broken product promise.

---

**Q5: PSU gate — should PSUs be explicitly excluded from the FA pipeline, or included with annotations?**
(a) Explicit exclusion: flag PSU-SKIPPED similar to BFSI-SKIPPED; acknowledge the gap [safest from false-signal perspective]
(b) Included with PSU-CONTEXT annotations: run the pipeline but annotate which signals are unreliable for PSUs and why [gives the user more data; risk of misleading annotations being missed]
(c) PSU sub-pipeline: similar to BFSI stub — suppress unreliable signals, retain valid ones (ROCE, FCF/NI, F1/F3/F4 from Piotroski), annotate clearly

**Default recommendation**: (c). PSU-CONTEXT does not mean ALL signals are invalid — ROCE and FCF/NI are meaningful even for PSUs. F7 (dilution), F5 (leverage), and pledge gate are the specific invalid signals. Running a partial pipeline is better than either full exclusion (leaves ~40 stocks without output) or full inclusion (produces misleading outputs on the invalid signals).

---

**Q6: AFFIRM label — add or keep the 4-label set?**
Add AFFIRM as a fifth label (above HOLD) for stocks at F ≥ 8 + FCF/NI ≥ 1.0 + ROCE ≥ 75th percentile + no flags. This gives a positive signal distinct from neutral HOLD.
(a) Add AFFIRM — richer signal set, distinguishes "passing" from "excellent"
(b) Keep 4-label set — simpler; HOLD covers both "passing" and "excellent"

**Default recommendation**: (b) for v0.2. The label set is already being revised (hysteresis, structured REVIEW checklist, cyclical caveats). Adding a fifth label is scope creep for v0.2. AFFIRM can be added in v0.3 once the core behavioral calibration is stable.

---

## 9. Confidence rating

**Confidence: HIGH** in the synthesis's identification of the P0 items (§4) and the specific math changes in §6. Four independent critics with different domain lenses converged on the same set of structural failures — this cross-critic convergence is a reliable signal.

**Confidence: MEDIUM** in the specific fix prescriptions for:
- The two-stage Beneish gate design (§6.1): the boundary between the hard-halt zone and the governance-corroboration-required zone is a judgment call. −1.50 as the inner threshold is proposed but not validated on NSE data. If the FY2023 GMI=1.96 + AQI=1.41 case for a real manipulating company showed M in [−1.60, −1.50], this threshold may still false-negative.
- The CYCLICAL sector tag list breadth (§6.3): whether to include housing-exposed industrials at > 40% revenue is a judgment call that would benefit from a third test case (C4's Crompton or Astral, as suggested).
- The composite Z″ replacement conditions (§6.5): the "accumulated reserves > 200% of EBITDA" condition is a proposed threshold, not a calibrated one.

**What would raise confidence**:
- A third test stock in the cyclical category that is NOT a metal/commodity (e.g., Crompton Greaves Consumer Electricals or Astral Ltd) showing whether the Piotroski anti-correlation holds for housing-linked industrials as well as for steel/metal
- A manipulation case stock (e.g., Vakrangee or Manpasand Beverages retrospectively) run through the Governance Quality Screen to validate that auditor change + RPT flags would have fired before the blow-up
- NSE-calibrated Beneish threshold research (Shah 2018 BSE 100 paper cited in v0.1 spec — if this paper has empirically re-estimated thresholds for Indian data, that should supersede −1.78 and −1.50 used here)

**Confidence: LOW** in the relative priority of P1 vs P2 items (Themes B through M in §3). The prioritization reflects the synthesizer's cross-critic reading but several items (Governance Screen, consolidated vs standalone) are one-critic findings without corroborating test-data evidence. A fourth test stock (specifically a conglomerate with material foreign operations, or a company with a documented auditor change preceding a negative event) would materially change the confidence level on these items.

---

**Status**: ✅ Synthesis complete.
**Last updated**: 2026-05-31

