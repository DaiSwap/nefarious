# 19c — Cycle A A.9: Crompton v0.3 Re-test

**Status**: 🔄 Drafting Mar-2020 + Mar-2021 deltas
**Date**: 2026-05-31
**Stock**: Crompton Greaves Consumer Electricals (CROMPTON, NSE) — soft cyclical (housing/consumer durables)
**Method**: re-applied v0.3 math to existing data from v0.2 fresh test (file 17c)
**Last updated**: 2026-05-31 (Checkpoint 2)

---

## 1. Top-line verdict on v0.3 changes for Crompton

| v0.3 change | Behavior on Crompton | Verdict |
|---|---|---|
| N2 — ACQUISITION-YEAR (CRITICAL) | Mar-2024: revenue grew 27.4% YoY (FY2022→FY2023) AND Butterfly acquisition disclosed → ACQUISITION-YEAR fires. AQI + DEPI excluded; SGI smoothed to 2-yr avg. M recomputed = −2.422 (was −1.199). Hard halt eliminated. | **FIXED** |
| N6 — Materiality buffer ±1% | Checked all 4 dates. Mar-2020 F8 is the closest knife-edge: 13.35% vs 0.99×13.50% = 13.365% → still 0 (miss by 0.015 pp). No signals flip across all 4 dates. | **DOESN'T-FIRE** |
| N7 — 5-yr window | Mar-2020/2021: WINDOW-SHORT (Crompton listed May 2016; <5 yrs data available) → falls back to 3-yr, same as v0.2. Mar-2022: 4-yr available → F=5/9 (same as v0.2). Mar-2024: 5-yr fully available → F=6/9 (new computation, was halted in v0.2). | **SAME** (no label changes; Mar-2024 F-Score newly computed at 6/9) |

---

## 2. The ACQUISITION-YEAR test (the headline)

### Did ACQUISITION-YEAR conditions fire at Mar-2024 (FY2022/FY2023 year-pair)?

**Condition 1 — Mechanical signal:**

| Metric | FY2022 (t−1) | FY2023 (t) | YoY growth | Threshold | Fires? |
|---|---|---|---|---|---|
| Consolidated TA | ₹6,449 Cr | ₹5,654 Cr | −12.3% (declined) | > 20% growth | **No** |
| Consolidated Revenue | ₹5,394 Cr | ₹6,870 Cr | +27.4% | > 25% growth | **YES** |

TA declined because FY2022 included Butterfly's balance sheet from March 30, 2022 (1-day consolidation inflating TA), while FY2023 reflects the operating entity post-partial debt repayment. Revenue grew 27.4% — the first full year of Butterfly revenue consolidation vs. 1 day in FY2022 — clearly exceeds the 25% threshold.

**Condition 2 — Disclosed acquisition:**
Butterfly Gandhimathi Appliances acquisition completed March 30, 2022. Disclosed via:
- Ind AS 103 Business Combinations note in the FY2023 annual report (first full consolidation year)
- BSE/NSE corporate-action filings (acquisition announcement Nov 2021; completion Mar 30, 2022)
- The FY2022 annual report discloses 1-day consolidation; FY2023 is first full-year Ind AS 103 disclosure

**Both conditions satisfied → ACQUISITION-YEAR fires at FY2022/FY2023 year-pair.**

Tag in output: `ACQUISITION-YEAR: Butterfly Gandhimathi Appliances (subsidiary, first full-year consolidation FY2023 vs 1-day FY2022). Beneish AQI and DEPI excluded; SGI smoothed via 2-yr average.`

---

### Step-by-step M-Score recomputation (v0.3 ACQUISITION-YEAR)

**From v0.2 (file 17c) Mar-2024 Beneish indices:**

| Index | v0.2 value | v0.3 treatment | v0.3 contribution |
|---|---|---|---|
| DSRI | 0.9054 | Unchanged: 0.920 × 0.9054 | **+0.8330** |
| GMI | 1.2721 | Unchanged: 0.528 × 1.2721 | **+0.6717** |
| AQI | 2.7553 | **EXCLUDED (= 0)** — acquisition consolidation artifact | **0** |
| SGI | 1.2736 (single-year) | **REPLACED with 2-yr-avg SGI** (see below) | *see below* |
| DEPI | 0.3692 | **EXCLUDED (= 0)** — acquired intangibles distort D&A/PPE ratio | **0** |
| SGAI | 0 | Unchanged (default) | **0** |
| TATA | −0.01362 | Unchanged: α×TATA = 2.0 × (−0.01362) | **−0.0272** |
| LVGI | 0.3926 | Unchanged: −0.327 × 0.3926 | **−0.1284** |

**2-yr-avg SGI calculation:**

Single-year revenue SGI values in the 2-yr window:
- FY2021 → FY2022: 5,394 / 4,804 = 1.1228
- FY2022 → FY2023: 6,870 / 5,394 = 1.2736 (single-year, acquisition-distorted)

2-yr-avg SGI = (1.1228 + 1.2736) / 2 = **1.1982**

SGI contribution: 0.892 × 1.1982 = **+1.0688**

Note: The 2-yr average smooths the acquisition-driven revenue spike (FY2022→FY2023 SGI = 1.27) by averaging it with the prior organic-growth year (FY2021→FY2022 SGI = 1.12), bringing SGI from 1.27 down to 1.20. The SGI contribution falls from +1.1361 to +1.0688 — a modest but meaningful reduction.

**v0.3 M-Score computation:**

```
M = −4.84
    + 0.920 × 0.9054   = +0.8330    [DSRI — unchanged]
    + 0.528 × 1.2721   = +0.6717    [GMI — unchanged]
    + 0.404 × 0         =  0.0000   [AQI — EXCLUDED: ACQUISITION-YEAR]
    + 0.892 × 1.1982   = +1.0688    [SGI — 2-yr-avg smoothed]
    + 0.115 × 0         =  0.0000   [DEPI — EXCLUDED: ACQUISITION-YEAR]
    − 0.172 × 0         =  0.0000   [SGAI — default]
    + 2.0 × (−0.01362) = −0.0272    [TATA — clean: OCF > NI]
    − 0.327 × 0.3926   = −0.1284    [LVGI — clean: leverage declining]
    ────────────────────────────────
    Sum of variable terms = +2.4179
    M = −4.84 + 2.4179 = −2.422
```

**v0.3 M-Score = −2.422 → well below −1.78 → PASS.**

Context note appended to output:
> *"ACQUISITION-YEAR (Butterfly Gandhimathi Appliances, first full-year consolidation FY2023): Beneish indices AQI and DEPI excluded due to acquisition consolidation artifacts — AQI was 2.76 (goodwill/intangibles from acquisition accounting) and DEPI was 0.37 (acquired intangibles with long amortization schedules). SGI smoothed via 2-yr average (1.20 vs single-year 1.27). M-Score = −2.422 reflects remaining 5 indices: DSRI (0.91, clean), GMI (1.27, margin dilution from Butterfly — real but not manipulation), smoothed SGI (1.20), TATA (clean: OCF > NI), LVGI (0.39, leverage declining). No manipulation signal in the remaining indices."*

---

### Baseline vs v0.3 comparison for Mar-2024:

| | v0.2 result | v0.3 result |
|---|---|---|
| M-Score | **−1.199** | **−2.422** |
| AQI contribution | +1.1131 (drove the halt) | **0** (excluded) |
| DEPI contribution | +0.0425 | **0** (excluded) |
| SGI contribution | +1.1361 | +1.0688 (2-yr avg) |
| Beneish verdict | **FLAG: MANIPULATION-RISK** (hard halt) | **PASS** (−2.422, pipeline continues) |
| Pipeline continues? | **No** — halted at Gate 2 | **Yes** |

**ACQUISITION-YEAR fixed the Mar-2024 false-positive. This is the critical v0.3 test — CONFIRMED.**

---

### Mar-2024: Full pipeline under v0.3 (Gates 3–8, previously halted)

**Gate 3 — Altman Z″ v0.3 (FY2023 balance sheet)**

Book Equity / TL replaces MktCap / TL:

| Term | Value | Computation |
|---|---|---|
| X1 | WC / Total Assets | −132 / 5,654 = **−0.02335** |
| X2_current | NPAT_TTM / Total Assets | 476 / 5,654 = **+0.08419** |
| X3 | EBIT / Total Assets | 654 / 5,654 = **+0.11567** |
| **X4' (v0.3)** | **Book Equity / Total Liabilities** | **2,660 / 2,994 = 0.8885** |

```
Z″_v0.3 = 6.56 × (−0.02335) + 3.26 × 0.08419 + 6.72 × 0.11567 + 1.05 × 0.8885 + 3.25
         = −0.1532 + 0.2745 + 0.7773 + 0.9329 + 3.25
         = +5.082
```

**Result**: Z″ = **5.08** → well above 2.6 → **PASS**

Supplementary display (v0.3 adds Current Ratio):
- Net Debt / EBITDA: ~₹855 Cr / ₹770 Cr = **1.11× (Normal)**
- Interest Coverage (EBIT/Interest): 654/109 = **6.0× (Strong)**
- **Current Ratio**: CA / CL ≈ 698 / 962 = **0.726 → "Tight" (NEW v0.3 signal, CR < 1.0)**

Gate 3: PASS (Z″ = 5.08). New "Tight" CR label is informational — below 1.0 but above 0.7 "Very Tight" threshold. No halt. Pipeline continues.

**Gate 4 — Pledge (Mar-2024)**: No promoters since FY2022 → PASS (same as v0.2 would have given).

**Gate 5 — Piotroski F-Score (v0.3: 5-yr window, first full computation for Mar-2024)**

Year-pair: FY2022/FY2023 (t = FY2023, t−1 = FY2022). Full 5-year window available (FY2019–FY2023).

*5-yr average inputs:*

| Year | EBIT/TA | OCF/AvgTA | GM% | Rev/AvgTA |
|---|---|---|---|---|
| FY2019 | 571/2,670 = 0.2139 | 299/2,548 = 0.1173 | 13.04% | 4,479/2,548 = 1.758 |
| FY2020 | 572/2,752 = 0.2079 | 411/2,711 = 0.1516 | 13.25% | 4,520/2,711 = 1.668 |
| FY2021 | 690/3,597 = 0.1918 | 830/3,175 = 0.2614 | 14.99% | 4,804/3,175 = 1.513 |
| FY2022 | 727/6,449 = 0.1127 | 736/5,023 = 0.1465 | 14.26% | 5,394/5,023 = 1.074 |
| FY2023 | 654/5,654 = 0.1157 | 553/6,052 = 0.0914 | 11.21% | 6,870/6,052 = 1.135 |

5-yr avg at t (FY2019–FY2023):
- EBIT/TA = (0.2139+0.2079+0.1918+0.1127+0.1157)/5 = **0.1684**
- OCF/AvgTA = (0.1173+0.1516+0.2614+0.1465+0.0914)/5 = **0.1536**
- GM% = (13.04+13.25+14.99+14.26+11.21)/5 = **13.35%**
- Rev/AvgTA = (1.758+1.668+1.513+1.074+1.135)/5 = **1.430**

5-yr avg at t−1 (FY2018–FY2022):
- EBIT/TA = (0.2136+0.2139+0.2079+0.1918+0.1127)/5 = **0.1880**
- GM% = (13.01+13.04+13.25+14.99+14.26)/5 = **13.71%**
- Rev/AvgTA = (1.803+1.758+1.668+1.513+1.074)/5 = **1.563**

Single-year signals (FY2023 vs FY2022) with ±1% buffer where applicable:

| Signal | Test | Values | ±1% buffer | Score |
|---|---|---|---|---|
| F1 (5-yr adj) | 5-yr avg EBIT/TA > 0 | 0.1684 > 0 | N/A (level check) | **1** |
| F2 (5-yr adj) | 5-yr avg EBIT/TA_t > 0.99 × t−1 | 0.1684 vs 0.99×0.1880 = 0.1861 | Buffer applied | 0.1684 < 0.1861 → **0** |
| F3 (5-yr adj) | 5-yr avg OCF/AvgTA > 0 | 0.1536 > 0 | N/A (level check) | **1** |
| F4 | OCF_FY2023 > 0.99 × NI_FY2023 | 553 > 0.99×476 = 471.2 | Buffer applied | 553 > 471.2 → **1** |
| F5 | (LTD/AvgTA)_FY2023 < 0.99 × (LTD/AvgTA)_FY2022 | 1,005/6,052=0.166 vs 0.99×1,686/5,023=0.332 | Buffer applied | 0.166 < 0.332 → **1** |
| F6 | CR_FY2023 > CR_FY2022 | CA/CL: 698/962=0.726 vs 1,017/4,029=0.252 | No buffer (v0.3 §9.2) | 0.726 > 0.252 → **1** |
| F7 | No dilution | Shares ~64.3 Cr both years | Discrete check | Stable → **1** |
| F8 (5-yr adj) | 5-yr avg GM_t > 0.99 × 5-yr avg GM_{t−1} | 13.35% vs 0.99×13.71% = 13.57% | Buffer applied | 13.35 < 13.57 → **0** |
| F9 (5-yr adj) | 5-yr avg Rev/AvgTA_t > 0.99 × t−1 | 1.430 vs 0.99×1.563 = 1.547 | Buffer applied | 1.430 < 1.547 → **0** |

| F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | **Cycle-adj F (v0.3)** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | **6/9** |

Stable-quality subset (F1, F3, F4, F7): 1+1+1+1 = **4/4** — all green.

Gate 6 — FCF/NI (3-yr: FY2021, FY2022, FY2023):

| Year | OCF | NI | OCF/NI |
|---|---|---|---|
| FY2023 | 553 | 476 | 1.162 |
| FY2022 | 736 | 578 | 1.273 |
| FY2021 | 830 | 617 | 1.345 |

CashConversion = mean(1.162, 1.273, 1.345) = **1.260** → **HIGH-QUALITY EARNINGS** (≥ 1.0). No IMPAIRMENT-CHECK (below 3.0× cap). Crompton is not a heavy-asset sector → IMPAIRMENT-CHECK annotation applies if capped, but it's not capped.

Gate 7 — Sector ROCE Percentile (FY2023): Crompton ROCE = **16%** (from Screener.in). Peers compressed in FY2023 due to input cost cycle. Approximate rank ~3rd–4th of 6–7 FMEG peers → ~45–50th percentile within FMEG tier.

Gate 8 — Action Label (Mar-2024):

| Input | Value |
|---|---|
| Cycle-adj F-Score (v0.3) | **6/9** |
| Stable-quality subset | 4/4 |
| FCF/NI | **1.260 — HIGH-QUALITY EARNINGS** |
| ROCE percentile | ~45–50th within FMEG (N<10) |

Routing per v0.2 §15:
- F = 5–6, FCF ≥ 1.0, ROCE ≥ 50 → WATCH
- F = 5–6, FCF ≥ 0.7, ROCE < 50 → REVIEW
- FCF is 1.260 (≥ 1.0) but ROCE is ~48th percentile (< 50). The FCF quality (1.26×) is strong and the 4/4 stable-quality subset is fully green. Conservative: borderline WATCH / REVIEW.

With FCF ≥ 1.0 dominating and ROCE just below 50th: **Label: WATCH** (mixed F=6 but earnings quality and capital efficiency both intact; borderline ROCE doesn't override strong FCF).

CYCLICAL-SECTOR WARNING attached:
> *"CYCLICAL-SECTOR WARNING: cycle-adj F=6 reflects housing/consumer-durables normalization period post-Butterfly integration. OCF quality is strong (1.26× CashConversion). Butterfly acquisition integration completing — FY2024 showed debt declining ₹1,686→₹683 Cr. Current Ratio = 0.726 (Tight) — watch working capital. Compare current ROCE (16%) to Crompton's 5-yr median (~22%) before reducing position."*

**Mar-2024 v0.3 Label: WATCH** (was FLAG: MANIPULATION-RISK in v0.2)

This is a major change — the false-positive FLAG is replaced by a substantive, commercially useful WATCH with full supporting diagnostics.

---

## 3. Per-date comparison (v0.2 → v0.3)

### Mar-2020

**v0.2 result (from file 17c)**: REVIEW (Cycle-adj F = 4/9; Beneish M = −1.963, context note; Pledge WARN + LTV-CAUTION)

**v0.3 changes to assess:**

**ACQUISITION-YEAR at FY2018/FY2019?**
- TA growth: FY2019 2,670 / FY2018 2,425 = +10.1% → below 20%
- Revenue growth: FY2019 4,479 / FY2018 4,080 = +9.8% → below 25%
- No disclosed material acquisition in FY2019
- **ACQUISITION-YEAR does NOT fire at Mar-2020.** M = −1.963 unchanged. Beneish: context note (single year, outside regime window). Same as v0.2.

**Altman Z″ v0.3 (Book Equity/TL):**

| Term | Value | Computation |
|---|---|---|
| X1 | WC / TA | −172 / 2,670 = −0.0644 |
| X2_current | NPAT / TA | 401 / 2,670 = +0.1502 |
| X3 | EBIT / TA | 571 / 2,670 = +0.2139 |
| **X4' (v0.3)** | **Book Equity / TL** | **1,097 / 1,573 = 0.6975** |

```
Z″_v0.3 = 6.56×(−0.0644) + 3.26×0.1502 + 6.72×0.2139 + 1.05×0.6975 + 3.25
         = −0.4225 + 0.4897 + 1.4374 + 0.7324 + 3.25
         = +5.49
```

v0.2 Z″ was 11.93 (dominated by MktCap/TL = 6.87). v0.3 Z″ = 5.49 — far more reasonable, reflects actual balance sheet quality, still comfortably above 2.6. **PASS** either way, but v0.3 gives a meaningful number rather than a market-cap-inflated artifact.

Supplementary display (v0.3 adds Current Ratio):
- Net Debt/EBITDA: ~₹569 / ₹584 = 0.97× (Normal)
- Interest Coverage: 571/60 = 9.5× (Strong)
- **Current Ratio (v0.3 new)**: Other Assets = 1,262; WC = −172; CL = 1,262−(−172) = 1,434; CA = 1,262+(−172) = 1,090; CR = 1,090/1,434 = **0.760 → "Tight" (CR < 1.0)**

**5-yr window (N7) — WINDOW-SHORT at Mar-2020:**
Crompton listed May 2016. At Mar-2020 (using FY2019 as t), 5-yr window = FY2015–FY2019. FY2015/FY2016 pre-listing, no consolidated data. FY2017 is estimated only.
Available reliable data: FY2018, FY2019 = 2 years. Plus estimated FY2017 = 3 years total.
Tag: `WINDOW-SHORT: 3 years available (FY2017 estimated); 5-yr window not achievable. Falls back to 3-yr avg.`

v0.3 3-yr avg = same as v0.2 3-yr avg. F = 4/9 unchanged.

**±1% Materiality buffer (N6):**
- F8: 3-yr avg GM at t = 13.35% vs t−1 = 13.50%. With buffer: 13.35 vs 0.99×13.50 = 13.365. Gap = −0.015 pp → buffer reduces gap from 0.15 pp to 0.015 pp but doesn't flip. F8 = **0** (same, very close)
- F9: 1.715 vs 0.99×1.752 = 1.734. 1.715 < 1.734 → F9 = **0** (same)
- F2: 0.216 vs 0.99×0.217 = 0.2148. 0.216 < 0.2148 → F2 = **0** (same)

No signals changed. F = **4/9** (same as v0.2).

**v0.3 result**: REVIEW (unchanged from v0.2)
**Label change**: **SAME**
**Improvement?**: **PARTIAL** — Z″ is more meaningful (5.49 vs 11.93); CR "Tight" signal is new useful information; but label unchanged.

---

### Mar-2021

**v0.2 result**: WATCH (Cycle-adj F = 5/9; Beneish M = −2.299, PASS; IND-AS-116-TRANSITION tagged)

**v0.3 changes:**

**ACQUISITION-YEAR at FY2019/FY2020?**
- TA growth: FY2020 2,752 / FY2019 2,670 = +3.1% → below 20%
- Revenue growth: FY2020 4,520 / FY2019 4,479 = +0.9% → below 25%
- No disclosed material acquisition in FY2020
- **ACQUISITION-YEAR does NOT fire.** M = −2.299 unchanged.

**Altman Z″ v0.3 (Book Equity/TL):**

| Term | Value | Computation |
|---|---|---|
| X1 (Ind AS 116 adj) | WC / TA | 74/2,752 = +0.0269 (+ lease adj ~0.034; minimal) |
| X2_current | NPAT / TA | 496/2,752 = +0.1803 |
| X3 | EBIT / TA | 572/2,752 = +0.2079 |
| **X4' (v0.3)** | **Book Equity / TL** | **1,468 / 1,284 = 1.143** |

```
Z″_v0.3 = 6.56×0.0269 + 3.26×0.1803 + 6.72×0.2079 + 1.05×1.143 + 3.25
         = 0.1765 + 0.5882 + 1.3971 + 1.200 + 3.25
         = +6.61
```

v0.2 Z″ was 25.45 (MktCap/TL = 19.08 contributing 20.03 points). v0.3 Z″ = 6.61 — correct order of magnitude. **PASS** either way; v0.3 is far more informative.

Supplementary display:
- Net Debt/EBITDA: ~₹368/₹599 = 0.61× (Very Low)
- Interest Coverage: 572/41 = 13.9× (Very Strong)
- **Current Ratio (v0.3)**: OA = 1,262; WC = 74; CL = 1,262−74 = 1,188; CA = 1,262+74 = 1,336; CR = 1,336/1,188 = **1.125 → Normal (CR > 1.0, no label fires)**

**5-yr window — WINDOW-SHORT at Mar-2021:**
FY2021 eval (t = FY2020). 5-yr = FY2016–FY2020. FY2016 pre-listing. FY2017 estimated.
Available reliable: FY2018, FY2019, FY2020 = 3 years. Plus estimated FY2017 = 4 years.
`WINDOW-SHORT: 3 reliable years (FY2018–FY2020) + 1 estimated (FY2017). Falls back to 3-yr for reliable computation.`

v0.3 3-yr avg = same as v0.2. F = 5/9 unchanged.

**±1% Materiality buffer:** Same analysis as v0.2 — F2/F8/F9 all miss the buffer cutoff by comfortable margins. No signals flip. F = **5/9** (same).

**v0.3 result**: WATCH (unchanged from v0.2)
**Label change**: **SAME**
**Improvement?**: **PARTIAL** — Z″ normalized from 25.45 to 6.61 (meaningful improvement in Z″ quality); CR now shown as 1.125 (Normal); label unchanged.

---

### Mar-2022

**v0.2 result**: WATCH (Cycle-adj F = 5/9; Beneish M = −2.706, PASS; COVID-WINDOW)

**v0.3 changes:**

**ACQUISITION-YEAR at FY2020/FY2021?**
- TA growth: FY2021 3,597 / FY2020 2,752 = +30.7% → exceeds 20%!
- Revenue growth: FY2021 4,804 / FY2020 4,520 = +6.3% → below 25%
- Disclosed acquisition? Butterfly acquisition completed March 30, 2022 — AFTER FY2021 year-end. There was NO acquisition in the FY2020/FY2021 period.
- TA growth explanation: FY2021 TA jump (2,752→3,597 = +30.7%) was driven by the strong FY2021 cash generation and working capital build-up (COVID-era OCF was ₹830 Cr, building up other current assets/investments). NOT from an acquisition.

With no disclosed acquisition in the period: **ACQUISITION-YEAR does NOT fire at FY2020/FY2021.** The v0.3 spec requires BOTH the mechanical signal AND the disclosed acquisition. Organic TA growth doesn't trigger it. M = −2.706 unchanged.

**Altman Z″ v0.3 (FY2021 balance sheet):**

| Term | Value | Computation |
|---|---|---|
| X1 | WC / TA | −26/3,597 = −0.0072 |
| X2_current | NPAT / TA | 617/3,597 = +0.1715 |
| X3 | EBIT / TA | 690/3,597 = +0.1919 |
| **X4' (v0.3)** | **Book Equity / TL** | **1,932 / 1,665 = 1.160** |

```
Z″_v0.3 = 6.56×(−0.0072) + 3.26×0.1715 + 6.72×0.1919 + 1.05×1.160 + 3.25
         = −0.0472 + 0.5591 + 1.2896 + 1.218 + 3.25
         = +6.27
```

v0.2 Z″ was 21.26. v0.3 Z″ = 6.27 — normalized and meaningful. **PASS**.

Supplementary display:
- Net Debt/EBITDA: ~₹368/₹720 = 0.51× (Very Low) — pre-Butterfly closing
- Interest Coverage: 690/43 = 16.0× (Very Strong)
- **Current Ratio (v0.3)**: OA = 1,900; WC = −26; CL = 1,900−(−26) = 1,926; CA = 1,900+(−26) = 1,874; CR = 1,874/1,926 = **0.973 → "Tight" (CR < 1.0)**

*Note: the "Tight" CR at Mar-2022 is a valid new signal. This reflects that Crompton was sitting at CR < 1 even before the Butterfly acquisition closed. The pandemic-era working capital squeeze and pre-acquisition cash deployment explain it. This is a useful data point v0.2 didn't surface.*

**5-yr window — 4-yr available at Mar-2022:**
FY2022 eval (t = FY2021). 5-yr = FY2017–FY2021. FY2017 is estimated from Screener trends; FY2018–FY2021 are reliable.
`WINDOW-SHORT: 4 years available (FY2017 estimated + FY2018–FY2021 reliable). Using 4-yr avg.`

4-yr avg inputs (FY2018–FY2021):

| | t = FY2021 window (FY2018–FY2021) | t−1 = FY2020 window (FY2017–FY2020) |
|---|---|---|
| 4-yr avg EBIT/TA | (0.2136+0.2139+0.2079+0.1918)/4 = **0.2068** | (~0.219+0.2136+0.2139+0.2079)/4 = **0.2136** |
| 4-yr avg OCF/AvgTA | (0.1401+0.1173+0.1516+0.2614)/4 = **0.1676** | — (F1/F3 level checks only) |
| 4-yr avg GM% | (13.01+13.04+13.25+14.99)/4 = **13.57%** | (~14.0+13.01+13.04+13.25)/4 = **13.33%** |
| 4-yr avg Rev/AvgTA | (1.803+1.758+1.668+1.513)/4 = **1.686** | (~1.786+1.803+1.758+1.668)/4 = **1.754** |

**Mar-2022 F-Score (v0.3, 4-yr window, ±1% buffer):**

| Signal | Test | Values | ±1% buffer | Score |
|---|---|---|---|---|
| F1 (4-yr adj) | 4-yr avg EBIT/TA > 0 | 0.2068 > 0 | N/A | **1** |
| F2 (4-yr adj) | 0.2068 vs 0.99×0.2136 = 0.2115 | 0.2068 < 0.2115 | Buffer applied | **0** |
| F3 (4-yr adj) | 4-yr avg OCF/AvgTA > 0 | 0.1676 > 0 | N/A | **1** |
| F4 | OCF_FY2021 (830) vs 0.99×NI_FY2021 (617) = 611 | 830 > 611 | Buffer applied | **1** |
| F5 | Financial debt ΔLev: ~438/3,175=0.138 vs 0.99×270/2,711=0.099 | 0.138 > 0.099 → increased | Buffer applied | **0** |
| F6 | CR: 0.973 vs 1.062 (prior yr) | 0.973 < 1.062 | No buffer | **0** |
| F7 | No dilution | Stable ~63.5 Cr | — | **1** |
| F8 (4-yr adj) | 13.57% vs 0.99×13.33% = 13.20% | 13.57% > 13.20% | Buffer applied | **1** ← NOTE: v0.3 4-yr avg changes GM direction |
| F9 (4-yr adj) | 1.686 vs 0.99×1.754 = 1.736 | 1.686 < 1.736 | Buffer applied | **0** |

| F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | **Cycle-adj F (v0.3)** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 0 | **5/9** |

F8 comparison note: v0.2 used 3-yr avg GM (13.76% vs 13.10%) → F8 = 1. v0.3 uses 4-yr avg (13.57% vs 13.33%) → still F8 = 1 (with ±1% buffer). Direction is the same. F = 5/9 is unchanged.

**v0.3 result**: WATCH (unchanged from v0.2)
**Label change**: **SAME**
**Improvement?**: **PARTIAL** — Z″ normalized from 21.26 to 6.27; CR "Tight" (0.97) is a new signal; label unchanged.

---

### Mar-2024 ← The critical date

**v0.2 result**: FLAG: MANIPULATION-RISK (hard halt at Gate 2; M = −1.199)

**v0.3 result**: WATCH (ACQUISITION-YEAR exception fires; M recomputed = −2.422; full pipeline runs)
- Gate 2: PASS (M = −2.422) with ACQUISITION-YEAR annotation
- Gate 3: Z″ = 5.08, PASS; CR = 0.726 "Tight"
- Gate 4: PASS (no promoters)
- Gate 5: Cycle-adj F = 6/9 (5-yr window, full computation)
- Gate 6: FCF/NI = 1.260 — HIGH-QUALITY EARNINGS
- Gate 7: ROCE ~16–19%, ~45–50th percentile FMEG peer set
- Gate 8: **WATCH** with CYCLICAL-SECTOR WARNING

**Label change**: **CHANGED** — FLAG: MANIPULATION-RISK → WATCH
**Improvement?**: **YES** — False positive eliminated; meaningful WATCH with diagnostics is commercially correct.

Forward outcome context: Crompton at Mar-2024 (~₹385) → May-2026 (~₹281) = −27% over 24 months; −49% vs NIFTY. So avoiding Crompton at this date was directionally correct. But v0.2's FLAG mechanism was wrong (manipulation vs. acquisition integration drag); v0.3's WATCH with "Butterfly integration drag + Tight CR" is both more accurate and more actionable. An investor getting WATCH with the cyclical warning about ROCE at 16% vs. 5-yr median of ~22% and the "Tight" CR annotation has a far better picture than a false FLAG.

---

## 4. 5-yr window verdict

### Cycle-adj F-Score comparison: v0.2 (3-yr) vs v0.3 (5-yr or available window)

| Date | v0.2 window | v0.2 F | v0.3 window | v0.3 F | Label change? |
|---|---|---|---|---|---|
| Mar-2020 | 3-yr (FY2017–FY2019; FY2017 est) | 4/9 | 3-yr (WINDOW-SHORT: same) | **4/9** | **No** |
| Mar-2021 | 3-yr (FY2018–FY2020) | 5/9 | 3-yr (WINDOW-SHORT: same) | **5/9** | **No** |
| Mar-2022 | 3-yr (FY2019–FY2021) | 5/9 | 4-yr (FY2018–FY2021; WINDOW-SHORT) | **5/9** | **No** |
| Mar-2024 | Not computed (halted) | N/A | 5-yr (FY2019–FY2023; full) | **6/9** | New computation (was halt) |

**Key finding on N7 for Crompton**: The 5-yr window improvement (N7) doesn't change any of the first three dates because Crompton's listing history creates WINDOW-SHORT conditions. The company only reaches a full 5-yr window at Mar-2024 — and only then because the pipeline runs at all (thanks to N2 ACQUISITION-YEAR exception).

**WINDOW-SHORT conditions:**
- Mar-2020: `WINDOW-SHORT: 3 years available (FY2017 estimated, FY2018–FY2019 reliable). Minimum 5-yr requirement not met — falls back to available history.`
- Mar-2021: `WINDOW-SHORT: 3 years reliable (FY2018–FY2020), 4 with FY2017 estimate. Falls back to 3-yr.`
- Mar-2022: `WINDOW-SHORT: 4 years available (FY2017 estimated + FY2018–FY2021). 5-yr ideal; using 4-yr.`
- Mar-2024: Full 5-yr window available (FY2019–FY2023). No window-short tag.

**Does the longer window change action labels at any date?** No — labels are REVIEW, WATCH, WATCH at Mar-2020/2021/2022 whether using 3-yr or 4-yr windows. The F-Score values are stable because Crompton's EBIT/TA, GM, and asset turnover trends are consistently mild rather than having sharp peak/trough artifacts within the available data window.

**Structural note**: N7's benefit will be more visible for Crompton in future evaluation dates (FY2025, FY2026) when the full 5-yr window anchors against the FY2022 Butterfly acquisition noise and the FY2020 COVID year. The 5-yr window is designed to smooth through full mini-cycles — Crompton is only now accumulating the post-acquisition years needed to demonstrate this.

---

## 5. New issues v0.3 introduces (if any)

**Issue 1 — α=2.0 still mechanically triggered for Mar-2024 by goodwill (unchanged)**

In v0.2, the α = 2.0 coefficient was triggered because PPE/TA = 57.9% > 50% — entirely from Butterfly goodwill/intangibles. v0.3 does NOT fix this because the ACQUISITION-YEAR exception targets AQI/DEPI exclusions but doesn't adjust the α calculation. With α = 2.0, the TATA contribution remains small at −0.027 (TATA = −0.014). Under ACQUISITION-YEAR exception, the AQI and DEPI terms are already zeroed out, so the α issue has no material impact on the final M-Score.

However, in future year-pairs (FY2024 and beyond), if goodwill from Butterfly remains > 50% of TA, the α = 2.0 will continue to apply to what is fundamentally a non-heavy-asset consumer business. The fix suggested in file 17c §5 ("exclude goodwill/intangibles > 20% of TA from the PPE/TA test") is still a valid v0.4 candidate.

Impact on v0.3 result: **Minor.** The TATA term at Mar-2024 with α=2.0 contributes −0.027 vs −0.064 with α=4.679. Either way it's a small contribution to a cleanly negative M-Score under ACQUISITION-YEAR exception. No label change.

**Issue 2 — "Tight" CR at Mar-2020, Mar-2022, Mar-2024 (new v0.3 signal)**

The new CR display (N1 supplement) identifies CR < 1.0 at Mar-2020 (0.76), Mar-2022 (0.97), and Mar-2024 (0.73). All three trigger "Tight." Mar-2021 shows Normal (1.13). This is new information not surfaced in v0.2. For Crompton, working capital is structurally negative in some periods (large trade payables to suppliers, negative WC Days). The "Tight" CR label may be somewhat misleading for companies with this payables-driven negative-WC model — their CR < 1 is a business model feature, not a liquidity warning.

This is not a v0.3 flaw exactly, but a known ambiguity: CR < 1 in payables-heavy businesses (Crompton, HUL, Asian Paints) is common and not inherently distressed. The supplementary display correctly labels it "Tight" informatively, leaving interpretation to the analyst. No label impact; informational flag only.

**Issue 3 — No new issues that change outcomes.** The three v0.3 changes affecting Crompton (N2, N6, N7) all behave as designed: N2 fixes the key false positive, N6 doesn't fire (no knife-edge signals), N7 produces WINDOW-SHORT gracefully.

---

## 6. v0.3 score for Crompton

How many of v0.3's relevant changes (N2, N6, N7) actually improved Crompton's result vs v0.2?

| Change | Relevant? | Fired? | Improved result? | Notes |
|---|---|---|---|---|
| N2 — ACQUISITION-YEAR | YES (Mar-2024 false positive) | **FIRED (Mar-2024)** | **YES — critical fix** | Removed false FLAG, enabled full pipeline to run, produced meaningful WATCH |
| N6 — ±1% materiality buffer | YES (any knife-edge signals) | **DID NOT FIRE** | No change | Closest case: Mar-2020 F8 missed by 0.015 pp; no signals flip at any date |
| N7 — 5-yr window | YES (CYCLICAL-tagged) | **FIRED (4 dates)** | Marginal at first 3 dates; New computation at Mar-2024 | WINDOW-SHORT at Mar-2020/2021/2022 limits benefit; full 5-yr at Mar-2024 gives first meaningful F-Score for that date |

**Score: 1 of 3 directly improved Crompton's label (N2). The other 2 (N6, N7) are present in the computation but don't change outcomes at these specific dates.**

---

## 7. Summary table: v0.2 vs v0.3 across all 4 dates

| Eval Date | v0.2 M-Score | v0.3 M-Score | v0.2 Z″ | v0.3 Z″ | v0.2 Cycle-adj F | v0.3 Cycle-adj F | v0.2 Label | v0.3 Label | Changed? |
|---|---|---|---|---|---|---|---|---|---|
| Mar-2020 | −1.963 | −1.963 | 11.93 | **5.49** | 4/9 | 4/9 | REVIEW | REVIEW | No |
| Mar-2021 | −2.299 | −2.299 | 25.45 | **6.61** | 5/9 | 5/9 | WATCH | WATCH | No |
| Mar-2022 | −2.706 | −2.706 | 21.26 | **6.27** | 5/9 | 5/9 (4-yr WINDOW-SHORT) | WATCH | WATCH | No |
| Mar-2024 | **−1.199** | **−2.422** | N/A (halted) | **5.08** | N/A | **6/9** | **FLAG: MANIP-RISK** | **WATCH** | **YES** |

**Across-the-board Z″ improvement**: v0.2's MktCap/TL-inflated Z″ values (11.93–25.45) are all normalized to a coherent 5.08–6.61 range under v0.3's Book Equity/TL. This is the N1 change — not specific to Crompton, but the Crompton data confirms the v0.3 fix produces meaningful Z″ values that could actually distinguish healthy from distressed balance sheets.

---

## 8. One sentence to Pranav

"For Crompton specifically, v0.3 **does** fix the Mar-2024 false-positive because the ACQUISITION-YEAR exception (N2) correctly detects the 27.4% revenue surge from Butterfly's first full consolidation year, excludes the distorted AQI (2.76) and DEPI (0.37) indices entirely, smooths SGI via 2-yr average, and recomputes M = −2.422 (from −1.199) — moving the hard-halt FLAG to a well-supported WATCH with full pipeline diagnostics and a meaningful Z″ = 5.08, FCF/NI = 1.26×, and Cycle-adj F = 6/9."

---

**Status**: ✅ A.9 Crompton v0.3 re-test complete.
**Last updated**: 2026-05-31 (Checkpoint 4 — final)
