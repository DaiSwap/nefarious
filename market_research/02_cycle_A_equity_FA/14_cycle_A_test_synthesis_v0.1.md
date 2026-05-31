# 14 — Cycle A: Test Synthesis v0.1 (across Asian Paints + Tata Steel)

**Status**: Final for v0.1; input to A.5 critique
**Date**: 2026-05-30
**Scope**: Synthesizes findings from `12_cycle_A_test_v0.1.md` (Asian Paints — quality compounder profile) and `13_cycle_A_test_v0.1_TataSteel.md` (Tata Steel — commodity cyclical profile).

---

## TL;DR — v0.1 math is broken in six identifiable ways

| # | Weakness | Surfaced in | Severity |
|---|---|---|---|
| 1 | **Beneish gives false positives during regime shifts** (COVID-era WC swings, investment parking) | Asian Paints Mar-2022 | **Critical** |
| 2 | **Beneish gives false negatives for commodity firms** (large non-cash charges suppress TATA term, M-Score never approaches threshold) | Tata Steel all 4 dates | **Critical** |
| 3 | **Piotroski F-Score is anti-correlated with cyclical entry opportunity** (highest score at peak, lowest at trough) | Tata Steel Mar-2020 vs Mar-2021 | **Critical** |
| 4 | **Ind AS 116 lease accounting (effective FY2020) breaks YoY signals** across the universe — spurious leverage/turnover triggers | Asian Paints Mar-2020 F5 | High |
| 5 | **Altman Z″ is dominated by century-accumulated reserves** for old companies — masks current leverage risk | Tata Steel all 4 dates | High |
| 6 | **Sector ROCE percentile fails on small sectors** (paints N<10) — systematic conservative bias on quality compounders in niche sectors | Asian Paints all 4 dates | Medium |

Plus a meta-finding: **trailing fundamentals are blind to forward disruptions** (competitive entries, demand-cycle inflection, valuation mean-reversion). Asian Paints' Birla Opus entry threat and 90× P/E in 2021 — neither visible to v0.1 math.

---

## Test results in compact form

### Asian Paints (quality compounder, ASIANPAINT)

| Date | F-Score | FCF/NI | Beneish M | Altman Z″ | Pledge | Sector ROCE % | Action | Forward excess (vs NIFTY TRI) | Match? |
|---|---|---|---|---|---|---|---|---|---|
| Mar-2020 | 5/9 | 0.97 | −2.35 ✓ | 8.24 ✓ | 0% ✓ | N/A (N<10) | **REVIEW** | +27.6% (24mo) | ❌ false negative |
| Mar-2021 | 8/9 | 1.08 | −2.56 ✓ | 9.22 ✓ | 0% ✓ | N/A (N<10) | **HOLD** | −22.4% (24mo) | ❌ false positive |
| Mar-2022 | — | — | **−1.697 ✗** | — | — | — | **FLAG: MANIP-RISK** | −31.0% (24mo) | ⚠️ direction right, mechanism wrong |
| Mar-2024 | 7/9 | 0.85 | −2.00 ✓ | 9.68 ✓ | 0% ✓ | N/A (N<10) | **HOLD** | ~−26% (14mo, partial) | ❌ false positive (so far) |

**Asian Paints score**: 1 of 4 directionally correct — and the one "correct" call was for the wrong reason (Beneish fired on COVID-era debtor-day stretch + investment parking, not on actual manipulation; the stock then fell because of Grasim/Birla Opus competitive disruption, which the math could not see).

### Tata Steel (commodity cyclical, TATASTEEL)

| Date | F-Score | FCF/NI | Beneish M | Altman Z″ | Pledge | Sector ROCE % | Action | Forward excess | Match? |
|---|---|---|---|---|---|---|---|---|---|
| Mar-2020 (TROUGH) | 5/9 | high | very low ✓ | 5.5–5.9 ✓ | 0% ✓ | low | **REVIEW** | **+355%** | ❌ catastrophic false negative |
| Mar-2021 (PEAK) | 8/9 | high | very low ✓ | 5.5–5.9 ✓ | 0% ✓ | high | **HOLD** | +34% (market-matching) | ❌ false positive (peak entry signal) |
| Mar-2022 | — | — | very low ✓ | 5.5–5.9 ✓ | 0% ✓ | — | (similar HOLD/WATCH) | ~0% | mixed |
| Mar-2024 | — | — | very low ✓ | 5.5–5.9 ✓ | 0% ✓ | — | (similar) | TBD | TBD |

**Tata Steel score**: math gave the strongest BUY at the WORST entry (peak), weakest signal at the BEST entry (trough). The exact inverse of what a cyclical investor would want. This is the most damaging finding in the entire test.

---

## The six weaknesses — in depth

### Weakness 1 — Beneish false positives during regime shifts

**What happened (Asian Paints Mar-2022 / FY2021 data):**
- DSRI elevated (debtor days stretched 49 → 59 days as customers delayed payments during COVID)
- AQI elevated (investment-grade financial assets ballooned as the company parked cash during uncertainty)
- These two TRADITIONAL manipulation flags fired — but they were caused by COVID, not by accounting manipulation
- M-Score crossed −1.78, triggering `FLAG: MANIPULATION-RISK`
- The stock did fall over the next 24 months, but for unrelated reasons (Grasim entry, demand normalization)

**Why this matters:** Beneish was published in 1999 using US data from 1982–1992 — a "normal" macro environment. It was never validated against pandemic-scale working-capital aberrations. **Any non-routine macro event (pandemic, demonetization, GST transition, war-driven commodity spike) will create false manipulation signals.**

**For v0.2:** Either (a) raise the threshold during identified regime-shift windows, (b) require Beneish trigger to be confirmed by independent manipulation indicators (related-party transactions, auditor changes, restatement frequency), or (c) downgrade Beneish from knockout-gate to additive signal so it doesn't unilaterally halt the pipeline.

### Weakness 2 — Beneish structurally suppressed for commodity firms

**What happened (Tata Steel all 4 dates):**
- OCF >> NI by 3× to 17× across all years (depreciation on massive asset base + Corus impairments + acquisition-related non-cash charges)
- The **TATA term** in Beneish is `(Net Income − Operating CF) / Total Assets`, with a coefficient of **+4.679** (the largest in the formula)
- For Tata Steel, this term is **massively negative**, pulling M-Score deep below −1.78 (the "safe" side) even in years when other variables (GMI, AQI) were elevated
- M-Score never approached the threshold, even when FY2023 had GMI = 1.96 and AQI = 1.41 (both of which would flag a normal company)

**Why this matters:** Beneish silently fails to fire for an entire class of NSE companies (heavy industry, infrastructure, oil & gas, anything with large non-cash charges). The math is structurally blind to manipulation in exactly the sectors where it might be most needed.

**For v0.2:** Either (a) compute Beneish on adjusted figures that remove large non-cash items, (b) make the TATA term coefficient sector-dependent, or (c) add a sector-specific manipulation overlay for heavy industry (e.g., capex-to-D&A ratio drift, intangible/goodwill expansion, segment reporting changes).

### Weakness 3 — Piotroski F-Score is anti-correlated with cyclical entry

**What happened (Tata Steel Mar-2020 vs Mar-2021):**
- **Mar-2020 (steel cycle trough)**: F-Score = 5/9. Why low? ROA fell from previous year, margins compressed, asset turnover dropped (all *because* the cycle was at trough — fundamentals look weak at exactly the moment that's the best buy)
- **Mar-2021 (post-recovery peak)**: F-Score = 8/9. Why high? ROA improved YoY, margins expanded, asset turnover up (all *because* steel prices spiked — the math looks strongest exactly when entering is most dangerous)
- Forward returns: Mar-2020 entry → **+355%**; Mar-2021 entry → +34% (market-matching)

**Why this matters:** Piotroski's nine signals measure **year-over-year change in level**, not **regime position**. For mean-reverting cyclicals, this measures the recent tailwind/headwind, not the directional setup. The signal is structurally short-term while cyclical investing is structurally counter-cyclical.

**For v0.2:** Either (a) add a cyclical-vs-secular sector classification gate so Piotroski only runs on non-cyclicals, (b) supplement with a cycle-position indicator (e.g., capacity utilization, margin-vs-10yr-median, P/B-vs-10yr-median), or (c) invert the F-Score interpretation for known cyclicals (high F-Score = caution, low F-Score = opportunity).

### Weakness 4 — Ind AS 116 (lease accounting) breaks YoY signals

**What happened (Asian Paints Mar-2020 F5):**
- Ind AS 116 became effective April 2019 for Indian listed companies
- It moves operating-lease liabilities ON to the balance sheet (previously off-balance-sheet)
- This **artificially increases reported borrowings** in FY2020 vs FY2019, even when no real change in financial structure occurred
- Asian Paints' "leverage increase" triggered F5 = 0 (fail) in v0.1, contributing to the wrong REVIEW label at Mar-2020

**Why this matters:** Any major accounting-standard change creates a one-time year-over-year discontinuity that propagates through Piotroski (F5, F6, F9), Beneish (LVGI, AQI), and Altman (X4'). The math interprets accounting-rule changes as fundamental deterioration.

Known and upcoming Indian accounting changes that will affect this:
- Ind AS 116 (lease accounting, effective FY2020) — already affected our tests
- Ind AS 109 (financial instruments, effective various dates)
- Anticipated changes to revenue recognition (Ind AS 115 interactions)
- Goods and Services Tax (GST) introduction July 2017 — affected FY2017 → FY2018 transitions

**For v0.2:** Either (a) skip year-pairs across known accounting-rule transitions, (b) apply standard-specific normalization adjustments, or (c) flag YoY signals during transition years as low-confidence and de-weight them.

### Weakness 5 — Altman Z″ dominated by century reserves

**What happened (Tata Steel all 4 dates):**
- Tata Steel has been operating since 1907; accumulated reserves and book equity are enormous
- The X2 (Retained Earnings / TA) and X4' (Book Equity / Total Liabilities) terms dominate Z″
- Result: Z″ stayed in the 5.5–5.9 range across all 4 dates, comfortably above the 2.6 "safe" threshold
- This was true even when Tata Steel was carrying ₹88,000–116,000 Cr of long-term debt, with European operations (Corus) dragging on profitability

**Why this matters:** Z″ was designed using firms with shorter histories. For multi-decade Indian companies (Tata Steel, Reliance, ITC, L&T), the legacy book equity will always overwhelm current-period leverage signals. The model is structurally blind to recent leverage deterioration in old companies.

**For v0.2:** Either (a) substitute current-period metrics (Net Debt/EBITDA, Interest Coverage) for distressed-company detection in century-old firms, (b) use *rolling* Z″ comparisons (today vs 3-yr-ago) instead of absolute thresholds, or (c) replace X2 with a 5-year-rolling reserves change rather than cumulative.

### Weakness 6 — Sector ROCE percentile fails on small sectors

**What happened (Asian Paints all 4 dates):**
- Indian Paints sector has < 10 NSE-listed peers (Asian Paints, Berger, Kansai Nerolac, Indigo Paints, Akzo Nobel India, Shalimar — 6 to 9 depending on year)
- v0.1 spec mandates: "for N < 10, show absolute ratio only; for N 10–14, caveat; for N ≥ 15, show percentile"
- Asian Paints' 33% ROCE (which would be a 95+ percentile in most sectors) is never displayed as a percentile — it shows as "absolute only"
- This systematically hides the company's biggest strength

**Why this matters:** Multiple high-quality Indian sectors are small by listed-count: paints, alcoholic beverages, exchange listings, specialty chemicals sub-sectors, defense electronics. The v0.1 rule penalizes quality compounders in niche sectors.

**For v0.2:** Either (a) use a broader sector grouping (e.g., "Consumer — Discretionary") as fallback when sub-sector N is too small, (b) compute percentile against a "comparable size + ROCE bracket" cohort rather than strict sector, or (c) display "rank N of M, ROCE = X%" as a substitute that's interpretable even at N=4.

---

## What v0.1 math DID get right (be fair)

- **Action labels for healthy compounders are stable when fundamentals don't shift dramatically.** Asian Paints Mar-2024 HOLD is reasonable on the math — it's the forward outcome (competitive disruption) that the math can't see.
- **The pipeline structure (gates → primary → overlays → action label) is logically sound** — the issue is which signals are in each box, not how they're composed.
- **The transparency is real.** Every output is traceable to a primary computation. A user can argue with the label because they can see what produced it.

---

## What v0.1 math fundamentally cannot see (acknowledged)

These are not weaknesses to "fix" in v0.2 — they're inherent limitations of pure FA-based math. Other cycles will need to address them:

| Blindspot | Should be handled in |
|---|---|
| Forward competitive disruption (e.g., new entrant) | Cycle B (TA — price action often telegraphs this); also qualitative overlays in Cycle F |
| Valuation mean-reversion (e.g., 90× P/E → P/E compression even if fundamentals improve) | Add P/E percentile to Cycle A v0.2; or handle in Cycle F (signal combination) |
| Cycle position for cyclicals (where in the cycle are we?) | Sector-cycle indicator, Cycle A v0.2 if we want it in FA; or Cycle B if we put it in TA |
| Regulatory shocks | Out of scope for systematic math; qualitative overlay or stop-loss math in Cycle E |
| Sentiment / liquidity / flows | Cycle B (TA) handles this domain |

---

## Implications for A.5 (multi-agent critique)

The critique should ideally include lenses for:
1. **Quant** — focus on Weakness 2 (Beneish coefficient sensitivity), Weakness 3 (cyclical inversion), Weakness 5 (Z″ for old firms). The math is empirically wrong in identifiable ways.
2. **Accountant / Forensic** — focus on Weakness 1 (regime-shift false positives), Weakness 4 (Ind AS 116 break). The math doesn't engage with how Indian accounting standards evolve.
3. **Behavioral** — focus on the labels themselves. WATCH and REVIEW invite action; if the math is wrong, the invitation to act amplifies the cost.
4. **Retail user** — focus on usability. Action labels with no actionable explanation (e.g., FLAG: MANIPULATION-RISK without saying "but this might be COVID, not manipulation") are misleading.
5. **NSE / India-specific** — focus on Weakness 6 (small sectors), and whether the bot's silent BFSI skip is acceptable for a portfolio that contains banks.

---

## Implications for v0.2 math (Cycle A A.6 refinement)

Concrete proposed changes for v0.2 (prioritized):

**P0 — Cannot ship v0.2 without:**
1. Beneish modification — either downgrade from knockout to additive, or add regime-shift detection (volatility-based), or both
2. Piotroski cycle-awareness — at minimum, flag cyclical sectors and present F-Score with cycle-context warning
3. Ind AS 116 / accounting transition handling — skip or normalize year-pairs that span standard changes

**P1 — Strong desirables:**
4. Altman Z″ for old companies — supplement with current-period leverage metric
5. Sector ROCE percentile — broader fallback grouping for small sectors

**P2 — Nice-to-haves:**
6. Add a few more FA ratios (P/E percentile, FCF Yield percentile) that v0.1 deferred
7. Coffee-Can long-run criterion as an OPTIONAL framework (not the only one)

**Open question for Pranav:** before A.6, does he want to commit P0 only (minimum fix) or P0+P1 (substantial fix) for v0.2?

---

## File map of Cycle A artifacts so far

| File | Purpose | Status |
|---|---|---|
| `10_cycle_A_research.md` | A.1 research (FA math survey) | Locked |
| `11_cycle_A_math_v0.1.md` | A.3 math spec v0.1 | Locked (historical) |
| `12_cycle_A_test_v0.1.md` | A.4 test on Asian Paints | Locked |
| `13_cycle_A_test_v0.1_TataSteel.md` | A.4 test on Tata Steel | Locked |
| **`14_cycle_A_test_synthesis_v0.1.md`** | This file — test synthesis | Final for v0.1 |
| Next: `15_cycle_A_critiques_v0.1.md` | A.5 critique pack (TBD) | Pending |
| Next: `16_cycle_A_math_v0.2.md` | A.6 refined math | Pending |
