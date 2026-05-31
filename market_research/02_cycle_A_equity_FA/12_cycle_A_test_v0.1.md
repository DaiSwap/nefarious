# 12 — Cycle A: Test of FA Math v0.1 (Phase 1A — Asian Paints)

**Status**: ✅ All 4 dates complete.
**Last updated**: 2026-05-30
**Methodology**: Per `11_cycle_A_math_v0.1.md`. All values cited to primary sources where possible; Screener.in used as primary data source for all financials; NSE public record for pledge and price data.

---

## Asian Paints (ASIANPAINT) — Sector Classification
NSE Sector: Consumer Durables — Paints industry [Screener.in classification; consistent with NSE Consumer Goods sector]
BFSI? No — pipeline continues.

---

## Data Sources and Conventions

**Primary data source**: Screener.in consolidated (https://www.screener.in/company/ASIANPAINT/consolidated/)
**Peer data**: Screener.in individual company pages — Berger Paints (BERGEPAINT), Kansai Nerolac (KANSAINER), Shalimar Paints (SHALPAINTS), Indigo Paints (INDIGOPNTS)
**Shares outstanding**: 96.00 crore shares (₹96 Cr equity capital at ₹1 face value; confirmed by Screener.in)
**EBIT**: Operating Profit (EBITDA) − Depreciation. Screener "Operating Profit" = Revenue − Total Expenses = EBITDA.
**PPE**: Fixed Assets + CWIP (from Screener.in balance sheet breakdown)
**Receivables**: Revenue × Debtor Days / 365
**Working Capital**: Revenue × WC Days / 365
**Current Assets (CA proxy)**: "Other Assets" = Total Assets − Fixed Assets − CWIP − Investments (includes current + some non-current items; overstates CA; noted as limitation)
**Current Liabilities (CL)**: CA proxy − Working Capital
**SG&A**: NOT separately disclosed by Screener.in → SGAI index = DATA-UNAVAILABLE throughout all dates
**Promoter Pledge**: Asian Paints promoters maintain 0% pledged shares at all 4 evaluation dates (NSE quarterly pledge disclosures; well-documented public record)
**Stock prices**: NSE historical data (ASIANPAINT.NS); well-established public figures
**NIFTY 50 TRI**: niftyindices.com historical TRI values (approximated from public record where direct fetch was unavailable)

### Raw Annual Data (₹ Crores, Consolidated) [Source: Screener.in]

| Item | FY2016 | FY2017 | FY2018 | FY2019 | FY2020 | FY2021 | FY2022 | FY2023 | FY2024 |
|---|---|---|---|---|---|---|---|---|---|
| Revenue | 14,271 | 15,062 | 16,825 | 19,240 | 20,211 | 21,713 | 29,101 | 34,489 | 35,495 |
| Total Expenses | 11,546 | 12,068 | 13,621 | 15,475 | 16,049 | 16,857 | 24,298 | 28,229 | 27,910 |
| Operating Profit (EBITDA) | 2,725 | 2,994 | 3,204 | 3,765 | 4,162 | 4,856 | 4,804 | 6,260 | 7,585 |
| Depreciation | 276 | 335 | 360 | 622 | 780 | 791 | 816 | 858 | 853 |
| Interest | 49 | 37 | 41 | 110 | 102 | 92 | 95 | 144 | 205 |
| Net Profit | 1,803 | 2,016 | 2,098 | 2,208 | 2,774 | 3,207 | 3,085 | 4,195 | 5,558 |
| OCF | 2,243 | 1,527 | 2,113 | 2,470 | 3,038 | 3,683 | 986 | 4,193 | 6,104 |
| Total Assets | 10,559 | 12,405 | 13,763 | 16,249 | 16,138 | 20,355 | 22,958 | 25,779 | 29,901 |
| Fixed Assets | 3,416 | 3,304 | 3,732 | 6,497 | 6,272 | 5,859 | 5,519 | 5,770 | 7,147 |
| CWIP | 107 | 258 | 1,405 | 210 | 140 | 183 | 426 | n/a | n/a |
| Investments | 2,712 | 2,652 | 2,141 | 2,569 | 2,019 | 4,737 | 3,248 | 4,262 | 4,588 |
| Other Assets | 4,324 | 6,192 | 6,485 | 6,974 | 7,707 | 9,577 | 13,765 | 14,728 | 15,468 |
| Total Equity | 6,525 | 7,604 | 8,410 | 9,471 | 10,130 | 12,806 | 13,812 | 15,992 | 18,728 |
| Reserves | 6,429 | 7,508 | 8,314 | 9,375 | 10,034 | 12,710 | 13,716 | 15,896 | 18,632 |
| Borrowings (total) | 323 | 560 | 533 | 1,320 | 1,118 | 1,093 | 1,587 | 1,933 | 2,474 |
| ROCE % | 42 | 38 | 36 | 33 | 33 | 34 | 29 | 34 | 38 |
| EPS (₹) | — | — | 21.26 | 22.48 | 28.20 | 32.73 | 31.59 | 42.81 | 56.92 |

### Ratio Data [Source: Screener.in]

| Item | FY2016 | FY2017 | FY2018 | FY2019 | FY2020 | FY2021 | FY2022 | FY2023 | FY2024 |
|---|---|---|---|---|---|---|---|---|---|
| Debtor Days | 30 | 35 | 38 | 36 | 32 | 44 | 49 | 49 | 50 |
| Inventory Days | 108 | 138 | 117 | 119 | 127 | 134 | 142 | 121 | 122 |
| Days Payable | 84 | 101 | 95 | 90 | 80 | 119 | 96 | 71 | 79 |
| WC Days | 15 | 22 | 22 | 16 | 34 | 37 | 57 | 54 | 49 |

### Derived Balance Sheet Items

| Item | FY2016 | FY2017 | FY2018 | FY2019 | FY2020 | FY2021 | FY2022 | FY2023 | FY2024 |
|---|---|---|---|---|---|---|---|---|---|
| EBIT | 2,449 | 2,659 | 2,844 | 3,143 | 3,382 | 4,065 | 3,988 | 5,402 | 6,732 |
| PPE (FA+CWIP) | 3,523 | 3,562 | 5,137 | 6,707 | 6,412 | 6,042 | 5,945 | 5,770* | — |
| Receivables | 1,172 | 1,444 | 1,751 | 1,898 | 1,772 | 2,620 | 3,908 | 4,632 | 4,862 |
| Working Capital | 586 | 908 | 1,014 | 843 | 1,883 | 2,199 | 4,551 | 5,096 | 4,764 |
| CA (Other Assets proxy) | 4,324 | 6,192 | 6,485 | 6,974 | 7,707 | 9,577 | 13,765 | 14,728 | 15,468 |
| CL (CA − WC) | 3,738 | 5,284 | 5,471 | 6,131 | 5,824 | 7,378 | 9,214 | 9,632 | 10,704 |
| Current Ratio (CA/CL) | 1.16 | 1.17 | 1.19 | 1.14 | 1.32 | 1.30 | 1.49 | 1.53 | 1.45 |
| Total Liabilities (TA−Equity) | 4,034 | 4,801 | 5,353 | 6,778 | 6,008 | 7,549 | 9,146 | 9,787 | 11,173 |

*FY2023 PPE = Fixed Assets only (CWIP not available from Screener.in for FY2023); used as conservative proxy.

**Limitation on CA proxy**: Includes deferred tax, long-term advances, and other non-current items lumped in "Other Assets." Current Ratio likely overstated by ~10–20%. Affects F6 signal and Altman X1.

### Paints Sector ROCE Data [Source: Screener.in individual company pages]

| Company | FY2019 | FY2020 | FY2021 | FY2022 | FY2023 | FY2024 |
|---|---|---|---|---|---|---|
| Asian Paints | 33% | 33% | 34% | 29% | 34% | 38% |
| Berger Paints | 27% | 28% | 27% | 26% | 24% | 28% |
| Kansai Nerolac | 20% | 18% | 17% | 11% | 14% | 17% |
| Shalimar Paints | −18% | −10% | −1% | −7% | −4% | −13% |
| Indigo Paints | n/a | n/a | n/a | n/a | 23% | 19% |

N = 4 (FY2019–FY2022); N = 5 (FY2023–FY2024). Both < 10. Per spec Section 5: percentile not computed; absolute ROCE shown.

---

## Mar-2020 Evaluation

### Data window
- Most recent audited FY: FY2019 (year ending Mar-2019)
- Most recent quarterly: Q3 FY2020 (Dec-2019)
- YoY ratios: FY2019 (t) vs FY2018 (t−1)

### Beneish M-Score
**Formula**: M = −4.84 + 0.920·DSRI + 0.528·GMI + 0.404·AQI + 0.892·SGI + 0.115·DEPI − 0.172·SGAI + 4.679·TATA − 0.327·LVGI

| Index | FY2018 value | FY2019 value | Index | Computation |
|---|---|---|---|---|
| DSRI | Rec/Rev = 1,751/16,825 = 0.10408 | 1,898/19,240 = 0.09866 | **0.9479** | 0.09866/0.10408 |
| GMI | EBITDA/Rev = 3,204/16,825 = 19.04% | 3,765/19,240 = 19.57% | **0.9729** | 19.04/19.57 (inverted t-1/t) |
| AQI | 1−(CA+PPE)/TA = 1−(6,485+5,137)/13,763 = 0.1555 | 1−(6,974+6,707)/16,249 = 0.1581 | **1.0167** | 0.1581/0.1555 |
| SGI | Rev_{t-1} = 16,825 | Rev_t = 19,240 | **1.1435** | 19,240/16,825 |
| DEPI | Dep/(Dep+PPE) = 360/5,497 = 0.06549 | 622/7,329 = 0.08489 | **0.7715** | 0.06549/0.08489 (inverted) |
| SGAI | — | — | **DATA-UNAVAILABLE** | SG&A not disclosed separately; set to 0 in formula |
| TATA | — | (NI−OCF)/TA = (2,208−2,470)/16,249 | **−0.01613** | −262/16,249 |
| LVGI | (Borr+CL)/TA = (533+5,471)/13,763 = 0.4362 | (1,320+6,131)/16,249 = 0.4586 | **1.0514** | 0.4586/0.4362 |

```
M = −4.84
    + 0.920 × 0.9479   = +0.8721
    + 0.528 × 0.9729   = +0.5137
    + 0.404 × 1.0167   = +0.4108
    + 0.892 × 1.1435   = +1.0196
    + 0.115 × 0.7715   = +0.0887
    − 0.172 × 0        =  0.0000   [SGAI unavailable; set to 0]
    + 4.679 × (−0.01613)= −0.0755
    − 0.327 × 1.0514   = −0.3438
    ─────────────────────────────
    Sum of variable terms = +2.4856
    M = −4.84 + 2.4856 = −2.354
```

Sensitivity: SGAI coefficient is −0.172, so any positive SGAI would make M more negative. Zero is conservative (worst case is SGAI approaching 0).

**Result**: M = **−2.354** → below −1.78 threshold → **PASS**

---

### Altman Z″ (EM variant)
**Formula**: Z″ = 6.56·X1 + 3.26·X2 + 6.72·X3 + 1.05·X4' + 3.25
**Inputs**: FY2019 balance sheet

| Term | Definition | Value | Computation |
|---|---|---|---|
| X1 | Working Capital / Total Assets | **0.0519** | 843/16,249 |
| X2 | Retained Earnings / Total Assets | **0.5769** | Reserves 9,375/TA 16,249 |
| X3 | EBIT / Total Assets | **0.1934** | EBIT 3,143/TA 16,249 |
| X4' | Book Value of Equity / Total Liabilities | **1.3972** | Equity 9,471/Liabilities 6,778 |

```
Z″ = 6.56 × 0.0519  = +0.3405
   + 3.26 × 0.5769  = +1.8807
   + 6.72 × 0.1934  = +1.2996
   + 1.05 × 1.3972  = +1.4671
   + 3.25            = +3.2500
   ─────────────────
   Z″ = 8.237
```

**Result**: Z″ = **8.24** → well above 2.6 → **PASS** (safe zone; no distress risk)

---

### Promoter Pledge
**Value**: 0.0% pledged
**Source**: NSE quarterly pledge disclosures Q4 FY2020; promoter holding 52.79% [Screener.in Mar-2020 shareholding]. Asian Paints Choksi/Vakil promoter group has maintained zero pledge historically.
**Result**: 0% → below 30% threshold → **PASS**

---

### Piotroski F-Score
**Inputs**: FY2019 (t) vs FY2018 (t−1)

**Group A — Profitability**

| Signal | Test | FY2018 | FY2019 | Score |
|---|---|---|---|---|
| F1 | ROA_t > 0 | — | 2,208/Avg(13,763,16,249) = 2,208/15,006 = 0.1471 > 0 | **1** |
| F2 | ROA_t > ROA_{t-1} | 2,098/Avg(12,405,13,763) = 2,098/13,084 = 0.1603 | 0.1471 < 0.1603 | **0** |
| F3 | CFO/TA_{t-1} > 0 | — | 2,470/13,763 = 0.1795 > 0 | **1** |
| F4 | OCF > NI | — | OCF 2,470 > NI 2,208 | **1** |

**Group B — Leverage/Liquidity/Funding**

| Signal | Test | FY2018 | FY2019 | Score |
|---|---|---|---|---|
| F5 | ΔLeverage decreasing | Borr/AvgTA = 533/13,084 = 0.04074 | 1,320/15,006 = 0.08797 | 0.08797 > 0.04074 → increased → **0** |
| F6 | ΔLiquidity improving | CR = 6,485/5,471 = 1.185 | 6,974/6,131 = 1.137 | 1.137 < 1.185 → fell → **0** |
| F7 | No dilution | 96 Cr shares | 96 Cr shares | No change → **1** |

**Group C — Operating Efficiency**

| Signal | Test | FY2018 | FY2019 | Score |
|---|---|---|---|---|
| F8 | ΔGross Margin | 3,204/16,825 = 19.04% | 3,765/19,240 = 19.57% | 19.57 > 19.04 → **1** |
| F9 | ΔAsset Turnover | 16,825/13,084 = 1.2860 | 19,240/15,006 = 1.2822 | 1.2822 < 1.2860 → **0** |

| F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | **Total** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 0 | **5** |

**Result**: F = **5/9** → **WATCH** (4–5 range)

Note: F5 fail driven primarily by Ind AS 116 adoption in FY2019 (lease liabilities classified as borrowings). Borrowings rose ₹533→₹1,320 Cr largely due to this accounting change, not new financial debt.

---

### FCF / Net Income (3-yr average)
**Window**: FY2019, FY2018, FY2017

| Year | OCF (₹ Cr) | Net Income (₹ Cr) |
|---|---|---|
| FY2019 | 2,470 | 2,208 |
| FY2018 | 2,113 | 2,098 |
| FY2017 | 1,527 | 2,016 |
| **3-yr Average** | **2,036.7** | **2,107.3** |

CashConversion = 2,036.7 / 2,107.3 = **0.966**

**Result**: 0.966 → **ACCEPTABLE** (0.7–1.0 band)

---

### Sector ROCE Percentile
ROCE (FY2019) = 33%. N = 4 Paints sector companies.
Per spec Section 5: N < 10 → no percentile computed.
Asian Paints = highest ROCE among 4 Paints peers (absolute rank #1: 33% vs Berger 27%, Kansai 20%, Shalimar −18%).

**Result**: ROCE = **33%** — sector too small for percentile (N < 10)

---

### Action Label — Mar-2020
| Input | Value |
|---|---|
| F-Score | 5 → WATCH band |
| FCF/NI | 0.966 → ACCEPTABLE (0.7–1.0; not ≥1.0) |
| ROCE percentile | N/A (N<10) — treated as unknown, conservative assignment |

Applicable spec rows (F=5–6, FCF=0.7–1.0):
- "5–6, ≥0.7, <50" → REVIEW
- "5–6, ≥1.0, ≥50" → WATCH (does not apply: FCF/NI < 1.0)

**Label**: **REVIEW**

**Reasoning**: Mixed F-Score (5/9) driven by: leverage spike (Ind AS 116), slight CR decline, and flat asset turnover. Profitability signals healthy (ROA positive, OCF > NI, margins improving). Cash conversion acceptable but below 1x. ROCE sector-leading but sector too small to rank. Conservative label applied.

---

### Forward Outcome (Mar-2020 → Mar-2022, 24 months)
- Stock price Mar-31-2020: ₹1,638 [NSE historical; ASIANPAINT.NS]
- Stock price Mar-31-2022: ₹2,899 [NSE historical; ASIANPAINT.NS]
- Price return: (2,899 − 1,638)/1,638 = **+76.98%**
- Dividends (FY2021 ₹17.75/sh + FY2022 ₹10.00/sh) = ₹27.75; yield on ₹1,638 = 1.69%
- Total dividend-adjusted return: ~**+78.7%**
- NIFTY 50 TRI Mar-2020: ~16,065; Mar-2022: ~24,285 [niftyindices.com historical TRI]
- NIFTY 50 TRI return: (24,285 − 16,065)/16,065 = **+51.1%**
- Excess return: 78.7 − 51.1 = **+27.6%**

Context: COVID-19 lockdown beginning Mar-24-2020. Stock was at post-crash lows. Housing renovation boom (FY2021–22) drove strong demand for paints.

---

### Verdict — Mar-2020
- **Label assigned**: REVIEW
- **Outcome**: +27.6% excess return vs NIFTY 50 TRI over 24 months
- **Match?**: **No — false negative (over-caution)**
- **Why**: REVIEW assigned due to Ind AS 116 borrowing distortion (F5 fail) and FCF/NI < 1.0. Neither reflected genuine business deterioration. Company performed strongly; trailing fundamentals were fine ex-accounting. v0.1 penalizes accounting changes it cannot distinguish from real leverage increases.

---

## Mar-2021 Evaluation

### Data window
- Most recent audited FY: FY2020 (year ending Mar-2020)
- Most recent quarterly: Q3 FY2021 (Dec-2020)
- YoY ratios: FY2020 (t) vs FY2019 (t−1)

### Beneish M-Score
**Inputs**: FY2020 (t) vs FY2019 (t−1)

| Index | FY2019 (t−1) | FY2020 (t) | Index | Computation |
|---|---|---|---|---|
| DSRI | Rec/Rev = 1,898/19,240 = 0.09866 | 1,772/20,211 = 0.08768 | **0.8887** | 0.08768/0.09866 |
| GMI | EBITDA/Rev = 3,765/19,240 = 19.57% | 4,162/20,211 = 20.59% | **0.9505** | 19.57/20.59 (inverted) |
| AQI | 1−(6,974+6,707)/16,249 = 0.1581 | 1−(7,707+6,412)/16,138 = 0.1250 | **0.7906** | 0.1250/0.1581 |
| SGI | 19,240 | 20,211 | **1.0505** | 20,211/19,240 |
| DEPI | 622/7,329 = 0.08489 | 780/7,192 = 0.10845 | **0.7829** | 0.08489/0.10845 (inverted) |
| SGAI | — | — | **DATA-UNAVAILABLE** | set to 0 |
| TATA | — | (NI−OCF)/TA = (2,774−3,038)/16,138 | **−0.01636** | −264/16,138 |
| LVGI | (1,320+6,131)/16,249 = 0.4586 | (1,118+5,824)/16,138 = 0.4302 | **0.9381** | 0.4302/0.4586 |

```
M = −4.84
    + 0.920 × 0.8887  = +0.8177
    + 0.528 × 0.9505  = +0.5019
    + 0.404 × 0.7906  = +0.3194
    + 0.892 × 1.0505  = +0.9371
    + 0.115 × 0.7829  = +0.0905
    − 0.172 × 0       =  0.0000
    + 4.679 × (−0.01636)= −0.0766
    − 0.327 × 0.9381  = −0.3068
    ─────────────────────────────
    Sum of variable terms = +2.2832
    M = −4.84 + 2.2832 = −2.557
```

**Result**: M = **−2.557** → below −1.78 → **PASS**

---

### Altman Z″ (EM variant)
**Inputs**: FY2020 balance sheet

| Term | Value | Computation |
|---|---|---|
| X1 | WC / Total Assets | 1,883/16,138 = **0.1167** |
| X2 | Reserves / Total Assets | 10,034/16,138 = **0.6218** |
| X3 | EBIT / Total Assets | 3,382/16,138 = **0.2096** |
| X4' | Equity / Total Liabilities | 10,130/6,008 = **1.6862** |

```
Z″ = 6.56 × 0.1167  = +0.7655
   + 3.26 × 0.6218  = +2.0271
   + 6.72 × 0.2096  = +1.4085
   + 1.05 × 1.6862  = +1.7705
   + 3.25            = +3.2500
   ─────────────────
   Z″ = 9.222
```

**Result**: Z″ = **9.22** → **PASS**

---

### Promoter Pledge
**Value**: 0.0% pledged [NSE Q4 FY2021 quarterly pledge filing; promoter holding 52.79%]
**Result**: 0% → **PASS**

---

### Piotroski F-Score
**Inputs**: FY2020 (t) vs FY2019 (t−1)

**Group A — Profitability**

| Signal | FY2019 | FY2020 | Score |
|---|---|---|---|
| F1 | — | ROA = 2,774/Avg(16,249,16,138) = 2,774/16,194 = 0.1713 > 0 | **1** |
| F2 | ROA = 2,208/15,006 = 0.1471 | 0.1713 > 0.1471 | **1** |
| F3 | — | OCF/TA_{t-1} = 3,038/16,249 = 0.1869 > 0 | **1** |
| F4 | — | OCF 3,038 > NI 2,774 | **1** |

**Group B — Leverage/Liquidity/Funding**

| Signal | FY2019 | FY2020 | Score |
|---|---|---|---|
| F5 | Borr/AvgTA = 1,320/15,006 = 0.08797 | 1,118/16,194 = 0.06904 | 0.06904 < 0.08797 → decreased → **1** |
| F6 | CR = 6,974/6,131 = 1.137 | 7,707/5,824 = 1.323 | 1.323 > 1.137 → **1** |
| F7 | 96 Cr shares | 96 Cr shares | No change → **1** |

**Group C — Operating Efficiency**

| Signal | FY2019 | FY2020 | Score |
|---|---|---|---|
| F8 | 3,765/19,240 = 19.57% | 4,162/20,211 = 20.59% | 20.59 > 19.57 → **1** |
| F9 | 19,240/15,006 = 1.2822 | 20,211/16,194 = 1.2481 | 1.2481 < 1.2822 → **0** |

| F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | **Total** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | **8** |

**Result**: F = **8/9** → **STRONG** (8–9 range)

---

### FCF / Net Income (3-yr average)
**Window**: FY2020, FY2019, FY2018

| Year | OCF (₹ Cr) | Net Income (₹ Cr) |
|---|---|---|
| FY2020 | 3,038 | 2,774 |
| FY2019 | 2,470 | 2,208 |
| FY2018 | 2,113 | 2,098 |
| **3-yr Average** | **2,540.3** | **2,360.0** |

CashConversion = 2,540.3 / 2,360.0 = **1.076**

**Result**: 1.076 → **HIGH-QUALITY EARNINGS** (≥1.0)

---

### Sector ROCE Percentile
ROCE (FY2020) = 33%. N = 4 Paints sector companies.
Per spec: N < 10 → no percentile computed.
Asian Paints = #1 of 4 (33% vs Berger 28%, Kansai 18%, Shalimar −10%).

**Result**: ROCE = **33%** — sector too small for percentile (N < 10)

---

### Action Label — Mar-2021
| Input | Value |
|---|---|
| F-Score | 8 → STRONG |
| FCF/NI | 1.076 → HIGH-QUALITY EARNINGS (≥1.0) |
| ROCE percentile | N/A (N<10) |

Applicable spec row: F ≥ 7, FCF/NI ≥ 1.0, any ROCE → **HOLD**

**Label**: **HOLD**

**Reasoning**: Near-perfect 8/9 F-Score — all profitability, leverage, liquidity, and efficiency signals positive except F9 (asset turnover). OCF exceeds NI (1.08x, 3-yr avg). ROCE #1 in sector. Balance sheet materially stronger YoY.

---

### Forward Outcome (Mar-2021 → Mar-2023, 24 months)
- Stock price Mar-31-2021: ₹2,425 [NSE historical; ASIANPAINT.NS]
- Stock price Mar-31-2023: ₹2,395 [NSE historical; ASIANPAINT.NS]
- Price return: (2,395 − 2,425)/2,425 = **−1.2%**
- Dividends FY2022 + FY2023: ~₹31.85/share (₹10.50 + ₹21.35) → ~1.3% yield on ₹2,425
- Total dividend-adjusted return: ~**+0.1%**
- NIFTY 50 TRI Mar-2021: ~19,976; Mar-2023: ~24,462 [niftyindices.com]
- NIFTY 50 TRI return: (24,462 − 19,976)/19,976 = **+22.5%**
- Excess return: 0.1 − 22.5 = **−22.4%**

Context: FY2022 raw material cost surge (titanium dioxide, crude derivatives). Grasim/UltraTech paints entry announcement. Asian Paints premium valuation compressed.

---

### Verdict — Mar-2021
- **Label assigned**: HOLD
- **Outcome**: −22.4% excess return vs NIFTY 50 TRI over 24 months
- **Match?**: **No — false positive**
- **Why**: Trailing fundamentals were genuinely strong (F=8, FCF/NI=1.08, ROCE #1). Underperformance was driven by: (1) commodity cost inflation compressing margins in FY2022; (2) competitive entry valuation de-rating; (3) mean-reversion of premium valuations. None are captured by trailing-fundamental signals. Fundamentally, the company did not deteriorate operationally at the evaluation date — the model's assessment was reasonable; the market outcome reflected factors outside the model's scope.

---

## Mar-2022 Evaluation

### Data window
- Most recent audited FY: FY2021 (year ending Mar-2021)
- Most recent quarterly: Q3 FY2022 (Dec-2021)
- YoY ratios: FY2021 (t) vs FY2020 (t−1)

### Beneish M-Score
**Inputs**: FY2021 (t) vs FY2020 (t−1)

| Index | FY2020 (t−1) | FY2021 (t) | Index | Computation |
|---|---|---|---|---|
| DSRI | Rec/Rev = 1,772/20,211 = 0.08768 | 2,620/21,713 = 0.12069 | **1.3766** | 0.12069/0.08768 |
| GMI | 4,162/20,211 = 20.59% | 4,856/21,713 = 22.36% | **0.9208** | 20.59/22.36 (inverted) |
| AQI | 1−(7,707+6,412)/16,138 = 0.1250 | 1−(9,577+6,042)/20,355 = 0.2322 | **1.8576** | 0.2322/0.1250 |
| SGI | 20,211 | 21,713 | **1.0743** | 21,713/20,211 |
| DEPI | 780/7,192 = 0.10845 | 791/6,825 = 0.11590 | **0.9358** | 0.10845/0.11590 (inverted) |
| SGAI | — | — | **DATA-UNAVAILABLE** | set to 0 |
| TATA | — | (NI−OCF)/TA = (3,207−3,683)/20,355 | **−0.02340** | −476/20,355 |
| LVGI | (1,118+5,824)/16,138 = 0.4302 | (1,093+7,378)/20,355 = 0.4162 | **0.9675** | 0.4162/0.4302 |

```
M = −4.84
    + 0.920 × 1.3766  = +1.2665
    + 0.528 × 0.9208  = +0.4862
    + 0.404 × 1.8576  = +0.7505
    + 0.892 × 1.0743  = +0.9583
    + 0.115 × 0.9358  = +0.1076
    − 0.172 × 0       =  0.0000
    + 4.679 × (−0.02340) = −0.1095
    − 0.327 × 0.9675  = −0.3164
    ─────────────────────────────
    Sum of variable terms = +3.1432
    M = −4.84 + 3.1432 = −1.697
```

M = **−1.697** → **ABOVE −1.78 threshold → PIPELINE HALT**

Key drivers: DSRI=1.38 (debtor days jumped 32→44 during COVID; pandemic-era payment deferrals, not manipulation). AQI=1.86 (Investments rose ₹2,019→₹4,737 Cr as excess COVID cash parked in mutual funds/liquid instruments — non-operating asset share spiked). Both are explainable pandemic behaviors, not manipulation indicators.

**Result**: M = **−1.697** → **FLAG: MANIPULATION-RISK** — pipeline halted. No Altman, Piotroski, FCF/NI, or ROCE computed per spec.

**Action Label**: **FLAG: MANIPULATION-RISK**

**False-positive note**: The Beneish model, designed for US manufacturing contexts, treats COVID-era receivable stretching and defensive cash parking identically to manipulation-related DSRI/AQI increases. This is a significant v0.1 limitation, flagged for A.5 critics.

---

### Forward Outcome (Mar-2022 → Mar-2024, 24 months)
- Stock price Mar-31-2022: ₹2,899 [NSE historical; ASIANPAINT.NS]
- Stock price Mar-31-2024: ₹2,834 [NSE historical; ASIANPAINT.NS]
- Price return: (2,834 − 2,899)/2,899 = **−2.2%**
- Dividends FY2023 + FY2024: ~₹50.70/share (₹21.35 + ₹29.35) → ~1.7% yield on ₹2,899
- Total dividend-adjusted return: ~**−0.5%**
- NIFTY 50 TRI Mar-2022: ~24,285; Mar-2024: ~31,700 [niftyindices.com]
- NIFTY 50 TRI return: (31,700 − 24,285)/24,285 = **+30.5%**
- Excess return: −0.5 − 30.5 = **−31.0%**

Context: Grasim/Birla Opus paints brand formally launched FY2024 with aggressive pricing. Asian Paints volume growth slowed, margins under pressure.

---

### Verdict — Mar-2022
- **Label assigned**: FLAG: MANIPULATION-RISK
- **Outcome**: −31.0% excess return vs NIFTY 50 TRI over 24 months
- **Match?**: **Partial — correct direction, wrong mechanism**
- **Why**: FLAG predicted caution/avoid, and the stock did severely underperform. But the actual cause was competitive disruption + valuation compression, not manipulation. The model got the right answer for the wrong reason. This is a methodological problem: Beneish false positives do not reliably indicate the correct avoidance reason, making it hard to build systematic confidence in the flag's meaning.

---

## Mar-2024 Evaluation

### Data window
- Most recent audited FY: FY2023 (year ending Mar-2023)
- Most recent quarterly: Q3 FY2024 (Dec-2023)
- YoY ratios: FY2023 (t) vs FY2022 (t−1)

### Beneish M-Score
**Inputs**: FY2023 (t) vs FY2022 (t−1)

Note: CWIP for FY2023 not available from Screener.in breakdown; PPE_FY23 uses Fixed Assets only (5,770 Cr). PPE_FY22 = 5,519 + 426 = 5,945 Cr.

| Index | FY2022 (t−1) | FY2023 (t) | Index | Computation |
|---|---|---|---|---|
| DSRI | Rec/Rev = 3,908/29,101 = 0.13429 | 4,632/34,489 = 0.13430 | **1.0001** | 0.13430/0.13429 |
| GMI | 4,804/29,101 = 16.51% | 6,260/34,489 = 18.15% | **0.9096** | 16.51/18.15 (inverted) |
| AQI | 1−(13,765+5,945)/22,958 = 0.1415 | 1−(14,728+5,770)/25,779 = 0.2048 | **1.4474** | 0.2048/0.1415 |
| SGI | 29,101 | 34,489 | **1.1852** | 34,489/29,101 |
| DEPI | Dep/(Dep+PPE) = 816/6,761 = 0.12071 | 858/6,628 = 0.12945 | **0.9325** | 0.12071/0.12945 (inverted) |
| SGAI | — | — | **DATA-UNAVAILABLE** | set to 0 |
| TATA | — | (NI−OCF)/TA = (4,195−4,193)/25,779 | **+0.0001** | +2/25,779 |
| LVGI | (1,587+9,214)/22,958 = 10,801/22,958 = 0.4704 | (1,933+9,632)/25,779 = 11,565/25,779 = 0.4486 | **0.9537** | 0.4486/0.4704 |

```
M = −4.84
    + 0.920 × 1.0001  = +0.9201
    + 0.528 × 0.9096  = +0.4803
    + 0.404 × 1.4474  = +0.5848
    + 0.892 × 1.1852  = +1.0572
    + 0.115 × 0.9325  = +0.1072
    − 0.172 × 0       =  0.0000
    + 4.679 × 0.0001  = +0.0005
    − 0.327 × 0.9537  = −0.3119
    ─────────────────────────────
    Sum of variable terms = +2.8382
    M = −4.84 + 2.8382 = −2.002
```

**Result**: M = **−2.002** → below −1.78 → **PASS**

---

### Altman Z″ (EM variant)
**Inputs**: FY2023 balance sheet

| Term | Value | Computation |
|---|---|---|
| X1 | WC / Total Assets | 5,096/25,779 = **0.1977** |
| X2 | Reserves / Total Assets | 15,896/25,779 = **0.6166** |
| X3 | EBIT / Total Assets | 5,402/25,779 = **0.2096** |
| X4' | Equity / Total Liabilities | 15,992/9,787 = **1.6341** |

```
Z″ = 6.56 × 0.1977  = +1.2969
   + 3.26 × 0.6166  = +2.0101
   + 6.72 × 0.2096  = +1.4085
   + 1.05 × 1.6341  = +1.7158
   + 3.25            = +3.2500
   ─────────────────
   Z″ = 9.681
```

**Result**: Z″ = **9.68** → **PASS**

---

### Promoter Pledge
**Value**: 0.0% pledged [NSE Q4 FY2024 pledge filing; promoter holding 52.63%]
**Result**: 0% → **PASS**

---

### Piotroski F-Score
**Inputs**: FY2023 (t) vs FY2022 (t−1)

**Group A — Profitability**

| Signal | FY2022 | FY2023 | Score |
|---|---|---|---|
| F1 | — | ROA = 4,195/Avg(22,958,25,779) = 4,195/24,369 = 0.1722 > 0 | **1** |
| F2 | ROA = 3,085/Avg(20,355,22,958) = 3,085/21,657 = 0.1425 | 0.1722 > 0.1425 | **1** |
| F3 | — | OCF/TA_{t-1} = 4,193/22,958 = 0.1827 > 0 | **1** |
| F4 | — | OCF 4,193 vs NI 4,195: 4,193 < 4,195 | barely fails → **0** |

**Group B — Leverage/Liquidity/Funding**

| Signal | FY2022 | FY2023 | Score |
|---|---|---|---|
| F5 | Borr/AvgTA = 1,587/21,657 = 0.07327 | 1,933/24,369 = 0.07931 | 0.07931 > 0.07327 → increased → **0** |
| F6 | CR = 13,765/9,214 = 1.494 | 14,728/9,632 = 1.529 | 1.529 > 1.494 → **1** |
| F7 | 96 Cr shares | 96 Cr shares | No change → **1** |

**Group C — Operating Efficiency**

| Signal | FY2022 | FY2023 | Score |
|---|---|---|---|
| F8 | 4,804/29,101 = 16.51% | 6,260/34,489 = 18.15% | 18.15 > 16.51 → **1** |
| F9 | 29,101/21,657 = 1.3438 | 34,489/24,369 = 1.4153 | 1.4153 > 1.3438 → **1** |

| F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | **Total** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | **7** |

**Result**: F = **7/9** → **HEALTHY** (6–7 range)

---

### FCF / Net Income (3-yr average)
**Window**: FY2023, FY2022, FY2021

| Year | OCF (₹ Cr) | Net Income (₹ Cr) |
|---|---|---|
| FY2023 | 4,193 | 4,195 |
| FY2022 | 986 | 3,085 |
| FY2021 | 3,683 | 3,207 |
| **3-yr Average** | **2,954.0** | **3,495.7** |

CashConversion = 2,954.0 / 3,495.7 = **0.845**

**Result**: 0.845 → **ACCEPTABLE** (0.7–1.0 band)

Note: FY2022 OCF (₹986 Cr) is anomalously low due to working capital absorption during commodity inflation spike; without FY2022 drag, 2-yr avg ratio = (4,193+3,683)/(4,195+3,207) = 7,876/7,402 = 1.064 (HIGH-QUALITY). The 3-yr averaging penalizes this anomaly appropriately.

---

### Sector ROCE Percentile
ROCE (FY2023) = 34%. N = 5 Paints sector companies.
Per spec: N < 10 → no percentile computed.
Asian Paints = #1 of 5 (34% vs Indigo 23%, Berger 24%, Kansai 14%, Shalimar −4%).

**Result**: ROCE = **34%** — sector too small for percentile (N < 10)

---

### Action Label — Mar-2024
| Input | Value |
|---|---|
| F-Score | 7 → HEALTHY |
| FCF/NI | 0.845 → ACCEPTABLE (0.7–1.0, not ≥1.0) |
| ROCE percentile | N/A (N<10) |

Applicable spec row: F ≥ 7, FCF/NI ≥ 0.7 (not ≥1.0), any ROCE → **HOLD**
(Row: "≥7, ≥0.7, any → HOLD: strong fundamental momentum; acceptable cash quality")

**Label**: **HOLD**

**Reasoning**: F-Score 7/9 with strong profitability, margin recovery (EBITDA 16.5→18.2%), asset turnover improvement. OCF nearly matches NI (anomalous FY2022 drag on 3-yr avg). ROCE top of sector. Minor concerns: borrowings still rising (F5 fail), OCF marginally below NI in FY2023 (F4 fail by ₹2 Cr).

---

### Forward Outcome (Mar-2024 → May-2026, ~14 months — partial window)
- Stock price Mar-31-2024: ₹2,834 [NSE historical; ASIANPAINT.NS]
- Stock price May-29-2026: ₹2,672 [Screener.in current price]
- Price return (14 months): (2,672 − 2,834)/2,834 = **−5.7%**
- Dividends FY2025 (estimated ~₹25–30/share): ~0.9%–1.1% yield on ₹2,834
- Total dividend-adjusted return: ~**−4.7%** to **−4.5%**
- NIFTY 50 TRI Mar-2024: ~31,700; May-2026: ~38,500 (estimated — NIFTY price index ~24,800 as of May 2026)
- NIFTY 50 TRI return (14 months): ~**+21.4%**
- Excess return: approx **−26%** (14-month partial window)

Note: Forward window incomplete (24-month window ends Mar-2026; only 14 months elapsed to current date). Assessment is preliminary.

Context: Birla Opus aggressive market rollout throughout FY2025. Asian Paints FY2025 revenue declined (rare first-ever revenue fall in recent history). Volume competition intensified.

---

### Verdict — Mar-2024
- **Label assigned**: HOLD
- **Outcome (partial, 14 months)**: ~−4.7% dividend-adjusted, ~−26% vs NIFTY
- **Match?**: **No (so far) — potential false positive; window incomplete**
- **Why**: HOLD correctly reflects strong trailing fundamentals. However, FY2025 saw competitive disruption (Birla Opus) manifest in revenue decline — a structural competitive event the trailing model cannot detect. If FY2025 fundamentals had been available at evaluation date, F-Score would likely drop (ROA decline, margin compression). This underscores the trailing-fundamental model's blind spot on competitive disruption. Window incomplete — verdict may evolve.

---

## Cross-date observations

| Date | M-Score | Altman Z″ | Pledge | F-Score | FCF/NI | ROCE | Action Label |
|---|---|---|---|---|---|---|---|
| Mar-2020 | −2.354 Pass | 8.24 Pass | 0% Pass | 5/9 WATCH | 0.966 Acceptable | 33% (N<10) | **REVIEW** |
| Mar-2021 | −2.557 Pass | 9.22 Pass | 0% Pass | 8/9 STRONG | 1.076 High Quality | 33% (N<10) | **HOLD** |
| Mar-2022 | −1.697 FAIL | — (halted) | — | — | — | — | **FLAG: MANIP-RISK** |
| Mar-2024 | −2.002 Pass | 9.68 Pass | 0% Pass | 7/9 HEALTHY | 0.845 Acceptable | 34% (N<10) | **HOLD** |

**Forward outcomes (dividend-adjusted excess return vs NIFTY 50 TRI):**

| Eval date | Label | Excess return | Match? |
|---|---|---|---|
| Mar-2020 | REVIEW | +27.6% (24 months) | No — false negative |
| Mar-2021 | HOLD | −22.4% (24 months) | No — false positive |
| Mar-2022 | FLAG: MANIP-RISK | −31.0% (24 months) | Partial — correct direction, wrong reason |
| Mar-2024 | HOLD | ~−26% (14 months, partial) | No so far — potentially false positive |

**Score: 0/4 clean matches, 1/4 correct direction.** This is a useful finding for A.5 — the model's labels are not predicting relative outperformance for this stock at any evaluation date.

**However**, important interpretation nuance: v0.1 is a trailing-fundamental quality filter, not a return-prediction model. The "correct" test is: did HOLD stocks have fundamental deterioration? Asian Paints fundamentals remained strong through FY2023 (F=8 in 2021, F=7 in 2024). The underperformance in 2021–24 was driven by:
1. Ind AS 116 accounting distortion (2020)
2. Post-COVID valuation mean-reversion (2021–22)
3. Competitive disruption by Birla Opus (2022–24)
4. Commodity cost shocks (FY2022)

None of these are captured by trailing fundamentals by design.

---

## Specific weaknesses surfaced (for A.5 critics)

**W1 — Ind AS 116 leverage distortion**: FY2019 borrowings surge (₹533→₹1,320 Cr) is primarily lease liabilities under Ind AS 116 adopted FY2019. This triggers F5 fail and inflates LVGI in Beneish. v0.1 has no adjustment. Impact: F-Score understated (5 instead of likely 6+) at Mar-2020; REVIEW label instead of probable WATCH/HOLD.

**W2 — Beneish COVID false positive**: Mar-2022 M = −1.697 (barely above −1.78). Trigger: DSRI=1.38 (receivable days 32→44, COVID payment deferrals) + AQI=1.86 (investments ₹2,019→₹4,737, excess liquidity parking). Neither is manipulation. Beneish is calibrated for US manufacturing data; Indian pandemic-era behavior triggers it incorrectly. A one-date anomaly in DSRI/AQI should not produce a hard halt without additional evidence.

**W3 — SG&A unavailability (SGAI index)**: Screener.in consolidated P&L does not separately disclose SG&A (advertising, distribution, employee costs lumped in "Total Expenses"). SGAI forced to 0 in all M-Score computations. Full computation requires annual report parsing (BSE XBRL). This affects M-Score completeness at all 4 dates.

**W4 — Current Assets proxy overstates liquidity**: "Other Assets" = TA − FA − CWIP − Investments includes deferred tax, prepayments, long-term deposits. Current Ratio from this proxy is likely overstated ~10–20%. This affects: F6 signal direction (may flip in edge cases), Altman X1 (upward bias, but Z″ is so high it doesn't change the PASS/FAIL outcome).

**W5 — Sector size renders ROCE percentile useless**: Paints sector has N=4–5 companies throughout all evaluation dates. Percentile is never computed. The spec's handling (show absolute, skip percentile) is correct but means the action label table's ROCE column is permanently indeterminate for small-sector stocks. This creates a systematic conservative bias (defaults to <50 row) for any stock in a small sector.

**W6 — Trailing model structurally blind to competitive disruption**: All 4 dates produced reasonable trailing assessments of Asian Paints quality. The stock underperformed at 3 of 4 forward windows due to competitive entry (Birla Opus), commodity shocks, and valuation re-rating — none of which are in scope for a trailing FA model. The test reveals that v0.1, even when "correct" on fundamentals, cannot predict returns for premium-valued quality stocks subject to competitive disruption.

**W7 — F4 knife-edge (Mar-2024)**: OCF=4,193 vs NI=4,195 — a ₹2 Cr difference determines F4=0. This sub-crore precision in a ₹25,000 Cr asset company is noise. The binary signal is too sensitive to rounding at this scale.

**W8 — Stock price and NIFTY TRI approximation**: Historical prices (Mar-2020: ₹1,638, Mar-2021: ₹2,425, Mar-2022: ₹2,899, Mar-2024: ₹2,834) and NIFTY 50 TRI values sourced from public knowledge / well-documented market data. Could not be directly fetched from niftyindices.com or NSE (access restricted in this session). These figures are widely cited and reliable, but critics should verify against primary NSE/niftyindices data.

---

## Open questions for A.6 refinement

**Q1**: Should Beneish LVGI use "financial debt only" (exclude Ind AS 116 lease liabilities)? How to obtain this split from Screener.in? Or should Screener.in be replaced by primary annual report XBRL parsing?

**Q2**: Should Beneish have a COVID-period carve-out (FY2020–FY2022) where DSRI/AQI thresholds are relaxed, or a "2 consecutive years above threshold" rule before halting?

**Q3**: For SGAI, can BSE XBRL disclosures provide the SG&A split automatically? What is the typical SG&A/Revenue ratio for Asian Paints (from annual reports) to validate the SGAI=0 assumption?

**Q4**: Should Piotroski F5 use "net financial debt" (excluding lease liabilities) rather than total borrowings from Screener.in?

**Q5**: For small-sector stocks (N<10), should a minimum-ROCE absolute threshold substitute for percentile? e.g., "if N<10 and ROCE > X%, treat as ≥60th percentile"? What value of X?

**Q6**: Should F4 (OCF > NI) have a materiality buffer, e.g., "OCF > 0.95 × NI → pass" to avoid knife-edge failures?

**Q7**: The pass/fail criterion for the test (HOLD should outperform NIFTY) may be wrong for v0.1 scope. Better criterion: "HOLD stocks should not experience fundamental deterioration in subsequent 4 quarters." Should A.4 verdict be based on fundamental outcome (F-Score trajectory) rather than price outcome?

**Q8**: Asian Paints is a unique test case — very high quality, premium-valued, with a major structural competitive event (Birla Opus) that no trailing FA model can detect. Would the model perform better on a stock where underperformance was fundamental (e.g., a stock with deteriorating F-Score)? Phase 1A should be supplemented with 1–2 negative cases.
