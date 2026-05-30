# 11 — Cycle A: Equity FA Math Specification, v0.1

**Status**: Draft — A.3 output
**Date**: 2026-05-30
**Version**: v0.1 (first iteration; will be refined to v0.2 after critique/test)
**Scope**: Indian NSE direct equity, NIFTY 500 universe. No mutual funds (Cycle C). No TA (Cycle B). No position sizing (Cycle D). No exit math (Cycle E). FA only.
**Source**: Distilled from `10_cycle_A_research.md` + Pranav's A.2 picks (all defaults).

---

## 0. v0.1 picks (recap from A.2)

| Q | Pick |
|---|---|
| Framework | **Piotroski F-Score only** (best NSE evidence) |
| Trailing vs forward | **Trailing only** |
| Bank carve-out | **BFSI flagged & skipped in v0.1** |
| Sector percentile floor | **Show absolute + note if N < 15** |
| Coffee-Can | Deferred (Piotroski-only) |
| Manipulation/distress | **Knockout gates** (Beneish + Altman Z″) |
| Earnings quality | **FCF/Net Income in v0.1**; Sloan Accruals deferred |
| Promoter pledge | **>30% pledged = red flag (knockout)** |

---

## 1. The pipeline

For every NIFTY 500 stock the bot evaluates, the math runs in this exact order:

```
[1] Sector classification check     → BFSI?           → If yes: flag SKIPPED-BFSI, halt.
[2] Knockout gate: Beneish M-Score  → M > -1.78?      → If yes: flag MANIPULATION-RISK, halt.
[3] Knockout gate: Altman Z″        → Z″ < 1.1?       → If yes: flag DISTRESS-RISK, halt.
[4] Knockout gate: Promoter pledge  → Pledge > 30%?   → If yes: flag PLEDGE-RISK, halt.
[5] Compute Piotroski F-Score (0–9)
[6] Compute FCF / Net Income ratio (3-yr average)
[7] Compute sector percentile of ROCE (with N<15 caveat)
[8] Compose action label: HEALTHY / WATCH / REVIEW / FLAG
```

Halts above all produce a `FLAG` action label with the specific reason. No score computed for halted stocks.

---

## 2. Knockout gates (exact math)

### 2.1 BFSI exclusion gate
**Rule**: If stock's NSE industry classification belongs to `Banking`, `NBFC`, `Insurance`, or `Other Financial Services`, set `action = SKIPPED-BFSI` and halt pipeline. No score is meaningful for BFSI in v0.1.

**Rationale**: P/B is replaced by P/ABV for banks; ROCE replaced by ROE; specialized ratios (NIM, GNPA, PCR, CAR) needed. v0.2 will implement a parallel BFSI pipeline. For v0.1, banks are silent.

### 2.2 Beneish M-Score (manipulation detection)
**Formula** (Beneish 1999):

```
M = -4.84
    + 0.920 · DSRI    + 0.528 · GMI
    + 0.404 · AQI     + 0.892 · SGI
    + 0.115 · DEPI    - 0.172 · SGAI
    + 4.679 · TATA    - 0.327 · LVGI
```

Where the 8 indices are computed year-on-year (t vs t-1):

| Index | Definition |
|---|---|
| DSRI | (Receivables_t / Revenue_t) / (Receivables_{t-1} / Revenue_{t-1}) |
| GMI  | Gross Margin_{t-1} / Gross Margin_t  (note the inversion) |
| AQI  | (1 − (CurrentAssets + PPE) / TotalAssets)_t / same_{t-1} |
| SGI  | Revenue_t / Revenue_{t-1} |
| DEPI | (Depreciation / (Depreciation + PPE))_{t-1} / same_t |
| SGAI | (SG&A / Revenue)_t / (SG&A / Revenue)_{t-1} |
| TATA | (NetIncome − OperatingCF) / TotalAssets_t |
| LVGI | ((LTD + CurrentLiab) / TotalAssets)_t / same_{t-1} |

**Knockout threshold**: M > −1.78 → halt with `FLAG: MANIPULATION-RISK`.

**Notes**:
- Requires 2 consecutive years of comparable financials. Companies with <2 years of NSE history → mark `INSUFFICIENT-DATA`.
- Use consolidated financials throughout (locked convention).
- Restatements: use the most recent restated figures available.

### 2.3 Altman Z″ EM variant (distress detection)
**Formula** (Altman EM variant, India-correct form):

```
Z″ = 6.56·X1 + 3.26·X2 + 6.72·X3 + 1.05·X4' + 3.25
```

Where:
| Term | Definition |
|---|---|
| X1 | Working Capital / Total Assets |
| X2 | Retained Earnings / Total Assets |
| X3 | EBIT / Total Assets |
| X4' | **Book** Value of Equity / Total Liabilities  *(Z″ uses book, not market)* |

**Knockout threshold**: Z″ < 1.1 → halt with `FLAG: DISTRESS-RISK`.
Grey zone Z″ ∈ [1.1, 2.6] → no halt, but recorded as a context note in the output.

### 2.4 Promoter pledge gate
**Rule**: If promoter-pledged-shares % of total promoter holding > 30%, set `action = FLAG: PLEDGE-RISK` and halt.

**Data source**: NSE pledged-data filings (quarterly). Use most-recent filing.

**Notes**:
- Threshold = 30% is intentionally aggressive (research bucket 7.9 suggests 50% as the forced-liquidation correlation point, but 30% is the early-warning level).
- If pledge data is missing for the stock (rare), mark `INSUFFICIENT-DATA`, do not halt.

---

## 3. Piotroski F-Score (primary signal)

**Construction** (Piotroski 2000): sum of 9 binary tests, each scored 1 or 0. Range 0–9.

### Group A — Profitability (4 signals)

| ID | Test | Pass condition (= 1) |
|---|---|---|
| F1 | ROA positive | NetIncome_t / Avg(TotalAssets_{t-1}, TotalAssets_t) > 0 |
| F2 | ΔROA improving | ROA_t > ROA_{t-1} |
| F3 | CFO positive | OperatingCashFlow_t / TotalAssets_{t-1} > 0 |
| F4 | Accruals (cash > earnings) | OperatingCashFlow_t > NetIncome_t |

### Group B — Leverage / Liquidity / Funding (3 signals)

| ID | Test | Pass condition (= 1) |
|---|---|---|
| F5 | ΔLeverage decreasing | (LongTermDebt / Avg.TotalAssets)_t < same_{t-1} |
| F6 | ΔLiquidity improving | CurrentRatio_t > CurrentRatio_{t-1} |
| F7 | No share dilution | SharesOutstanding_t ≤ SharesOutstanding_{t-1} |

### Group C — Operating Efficiency (2 signals)

| ID | Test | Pass condition (= 1) |
|---|---|---|
| F8 | ΔGross margin improving | GrossMargin_t > GrossMargin_{t-1} |
| F9 | ΔAsset turnover improving | (Revenue / Avg.TotalAssets)_t > same_{t-1} |

### F-Score interpretation (v0.1)
| F-Score | Label | Meaning |
|---|---|---|
| 8–9 | **STRONG** | Strong fundamental momentum |
| 6–7 | **HEALTHY** | Acceptable; majority of signals positive |
| 4–5 | **WATCH** | Mixed — neither clearly improving nor deteriorating |
| 0–3 | **WEAK** | Majority of signals negative — review for deteriorating fundamentals |

> The label thresholds are deliberately conservative. Piotroski's original paper used ≥7 as the "value winner" gate within value portfolios; here we use a graded label set for richer reporting.

---

## 4. FCF / Net Income quality overlay (additive)

**Formula** (3-year average):
```
CashConversion = mean(OCF_t, OCF_{t-1}, OCF_{t-2}) / mean(NI_t, NI_{t-1}, NI_{t-2})
```

Where OCF = Operating Cash Flow, NI = Net Income.

**Interpretation**:
| CashConversion | Label |
|---|---|
| ≥ 1.0 | **HIGH-QUALITY EARNINGS** |
| 0.7 – 1.0 | **ACCEPTABLE** |
| < 0.7 | **EARNINGS-QUALITY-RISK** (additive flag, not a halt) |

**3-year averaging rationale**: smooths single-year working-capital swings and lumpy CapEx (esp. pharma R&D, infrastructure).

**Edge case**: If 3-year Net Income < 0 (chronic loser), mark `LOSS-MAKING` and apply F-Score independently. CashConversion is meaningless when the denominator is non-positive.

---

## 5. Sector-relative percentile (ROCE for v0.1)

**Why ROCE specifically in v0.1**: ROCE is the single most-cited capital-efficiency ratio in Indian quality investing (Mukherjea, MOSL, MSCI Quality). Other ratios (P/E, FCF Yield) will be added in v0.2 once we know the v0.1 output looks right.

**Formula**:
```
PercentileRank(stock_i) = (rank_i − 1) / (N_sector − 1) × 100
```
where `rank_i` is the ascending rank of `ROCE_i` within its NSE-sector peer set of size `N_sector`. Ties get average rank.

**Sector classification**: NSE 4-tier system, "Sector" level (22 sectors). Source: NSE Indices classification (July 2023).

**Small-sample handling**:
| N_sector | Display |
|---|---|
| ≥ 15 | "ROCE percentile = X within `<sector>`" |
| 10–14 | "ROCE percentile = X (note: sector has only N companies — interpret cautiously)" |
| < 10 | "ROCE = Y% (sector too small for percentile)" |

**ROCE definition** (locked):
```
ROCE = EBIT_{TTM} / (CurrentEquity + Net Debt + Minority Interest)
```
Use trailing-twelve-months EBIT. Use latest balance sheet for denominator components.

**Winsorization**: cap ROCE at 3× IQR above 75th percentile of the sector before ranking, to prevent extreme outliers (post-loss-reversal anomalies) from compressing the rest.

---

## 6. Final action label composition

For non-halted stocks (BFSI / manipulation / distress / pledge gates all passed):

| Piotroski F | FCF/NI | ROCE percentile | Action label |
|---|---|---|---|
| ≥ 7 | ≥ 1.0 | ≥ 60 | **HOLD** (healthy on all fronts) |
| ≥ 7 | ≥ 0.7 | any | **HOLD** (strong fundamental momentum; acceptable cash quality) |
| ≥ 7 | < 0.7 | any | **WATCH** (signals improving but cash quality lagging) |
| 5–6 | ≥ 1.0 | ≥ 50 | **WATCH** (mixed F-Score but cash quality + capital efficiency intact) |
| 5–6 | ≥ 0.7 | < 50 | **REVIEW** (fundamentals mixed and capital efficiency below sector median) |
| 5–6 | < 0.7 | any | **REVIEW** (mixed signals + cash-quality risk) |
| ≤ 4 | any | any | **REVIEW** (fundamentals deteriorating; deep review needed) |

**Action label glossary** (per Q9):
- **HOLD** — fundamentals healthy; no action needed beyond periodic reaffirmation.
- **WATCH** — minor deterioration; monitor next-quarter results before acting.
- **REVIEW** — material concerns; user should re-examine the original thesis explicitly.
- **FLAG** — knockout gate failed; consider exit candidate.

> These labels are **descriptive of the company's fundamental state**, not direct buy/sell instructions. The eventual recommendation per Q5 will combine this with TA, holding-period context, and tax math — all in later cycles.

---

## 7. Worked example (illustrative — Pranav will pick real names in A.4)

Let's walk a hypothetical mid-cap manufacturing company `XYZ Ltd` through v0.1:

**Step 1 — BFSI check**: NSE sector = "Industrial Manufacturing". ❌ Not BFSI. → continue.

**Step 2 — Beneish M-Score**: Suppose M = −2.41. ❌ Not > −1.78. → continue.

**Step 3 — Altman Z″**: Suppose Z″ = 3.2. ❌ Not < 1.1. → continue.

**Step 4 — Promoter pledge**: Suppose pledged = 8% of promoter holding. ❌ Not > 30%. → continue.

**Step 5 — Piotroski F-Score**:
- F1 (ROA>0) = 1
- F2 (ΔROA>0) = 1
- F3 (CFO>0) = 1
- F4 (CFO>NI) = 1
- F5 (ΔLev<0) = 0  (took on debt this year)
- F6 (ΔLiq>0) = 1
- F7 (no dilution) = 1
- F8 (ΔMargin>0) = 1
- F9 (ΔTurnover>0) = 0  (revenue grew slower than assets)
**F-Score = 7. Label: HEALTHY.**

**Step 6 — Cash Conversion (3-yr)**:
- OCF avg = ₹420 Cr, NI avg = ₹380 Cr → CashConversion = 1.11 → **HIGH-QUALITY**.

**Step 7 — Sector ROCE percentile**:
- XYZ ROCE = 22%, sector has 24 companies, XYZ ranks 5th highest.
- Percentile = (24 − 5) × 100 / (24 − 1) = 82.6.
- Display: "ROCE percentile = 83 within Industrial Manufacturing."

**Step 8 — Action label**:
- F-Score 7 + FCF/NI ≥ 1.0 + ROCE percentile ≥ 60 → **HOLD**.

Reasoning string (sample):
> "XYZ Ltd: HEALTHY (F-Score = 7/9). Cash conversion is high (1.11x, 3-yr avg) — earnings backed by cash. ROCE at 83rd percentile of its sector — strong capital efficiency. No manipulation, distress, or pledge risks. Fundamental thesis intact."

---

## 8. What v0.1 explicitly does NOT do (deferred to later versions / cycles)

| Deferred to | Item |
|---|---|
| Cycle A v0.2 | Coffee-Can 10-yr filter (depends on whether v0.1 misses obvious compounders) |
| Cycle A v0.2 | MSCI Quality composite (ROE + D/E + EVAR Z-score) |
| Cycle A v0.2 | Sloan Accruals ratio |
| Cycle A v0.2 | Additional sector percentiles (P/E, FCF Yield, D/E) |
| Cycle A v0.2 | Forward estimates for NIFTY 100 |
| Cycle A v0.2 | BFSI carve-out (P/ABV, NIM, GNPA, PCR, CAR ratio set) |
| Cycle B | All TA signals (RSI, MACD, 200DMA, etc.) |
| Cycle C | Mutual-fund-specific signals |
| Cycle D | Position sizing, correlation-to-portfolio |
| Cycle E | Exit rules, stop-losses, tax-aware sell sequencing |
| Cycle F | TA/FA conflict resolution math, behavioral-metric formulas |

---

## 9. Open questions for A.4 (testing)

To run A.4 (test on 10–20 historical NSE examples), I need Pranav's input on:

1. **Test universe**: Which stocks to test? Options:
   - (a) A mix of well-known names across sectors (e.g., HDFC AMC, Bajaj Finance, Page Industries, Asian Paints, Coal India, ITC, Tata Steel, Sun Pharma, L&T, M&M)
   - (b) Pranav suggests 10–20 specific stocks he's interested in (would prefer this — makes the test directly informative)
   - (c) Random sample from NIFTY 500

2. **Test time-points**: Apply v0.1 math at which historical dates and check what happened in the subsequent 12–24 months?
   - Default: 4 historical dates per stock — Mar-2020 (COVID bottom), Mar-2021 (early bull), Mar-2022 (sideways), Mar-2024 (broad bull)
   - Acceptable, or do you want different time-points?

3. **Pass/fail criteria for the test**: How do we decide if v0.1 math is "working"?
   - Proposed: stocks labeled `HOLD` should not have underperformed NIFTY 50 by >15% over the 12-month forward window; stocks labeled `REVIEW` or `FLAG` should have either underperformed or had a known deterioration event; HEALTHY/STRONG buckets should show consistent quality over forward periods.
   - This is a *qualitative* sanity check, not a backtest (per "test math, not engine").

4. **Manual computation or library-assisted?**
   - Option A: hand-compute each ratio from annual reports (slow, high-fidelity, ~3-4 stocks per hour)
   - Option B: pull data from Screener.in / Tickertape and compute in a quick pandas notebook (fast, fidelity depends on data source)
   - Default: B — but use 2 stocks of A as ground-truth to validate B's data accuracy.

---

## 10. What we expect critics to attack in A.5

Pre-empting the multi-agent critique step:

- **Quant lens** likely to challenge: "Where's the cost-adjusted Sharpe evidence for *this exact composition*? Piotroski alone has evidence; this is Piotroski + FCF + ROCE + 3 knockouts — not the same thing." (Valid; will need test data.)
- **Behavioral lens** likely to challenge: "Action labels invite trading. WATCH and REVIEW will be acted on. How often will a quarterly F-Score wobble produce a needless action?" (Valid; consider hysteresis in v0.2.)
- **Retail-user lens** likely to challenge: "How do I act on REVIEW? It's not clear." (Valid; the action labels need an associated 'what to do' decision tree — but that's the bot's UX layer, not the math.)

---

## 11. Sources used (v0.1 specific)

All citations are inherited from `10_cycle_A_research.md`. Key ones for v0.1:
- Piotroski (2000) — primary source
- Beneish (1999) — primary source
- Altman (1968, 1995 EM variant)
- Communications on Applied Nonlinear Analysis (2024) — NSE F-Score validation
- Indian Journal of Finance (Shah 2018) — BSE 100 M-Score validation
- DOAJ + Indian Journal of Capital Markets — Z-Score on NSE
- NSE Indices Industry Classification (2023)

---

**End of v0.1 spec.** Awaiting Pranav's approval to mark A.3 complete and begin A.4 (testing on real NSE examples).
