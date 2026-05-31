# 19a — Cycle A A.9: Asian Paints v0.3 Re-test

**Status**: ✅ A.9 Asian Paints v0.3 re-test complete.
**Date**: 2026-05-31
**Stock**: Asian Paints — quality compounder archetype
**Method**: re-applied v0.3 math from §18 to existing data from v0.2 re-test (file 17a)
**Last updated**: 2026-05-31T00:45Z (all 4 dates complete; verdict written)

---

## 1. Top-line verdict on v0.3 changes for Asian Paints

| v0.3 change | Behavior on Asian Paints | Verdict |
|---|---|---|
| N1 — Z″ X4' revert | Z″ drops from 30–46 range (v0.2) to 6.8–8.2 range (v0.3) across all 4 dates; metric is now discriminative again | FIXED |
| N4 — F5 Ind AS 116 narrowing | No change on any of the 4 test dates: Mar-2021 (the affected date) uses the FY2019/FY2020 year-pair, which v0.3 still excludes; Mar-2022/Mar-2024 had F5 included under v0.2 already | NO-CHANGE |
| N6 — Materiality buffer | Mar-2024 F4 knife-edge resolved: OCF 4,193 > 0.99 × NI 4,153 → F4=1; F-Score 7→8/9; label remains HOLD but F-count improves | FIXED (label same, signal quality improved) |

**Z″ summary across all dates (N1 effect)**:

| Date | v0.2 Z″ (MktCap/TL) | v0.3 Z″ (BookEq/TL) | X4' v0.2 | X4' v0.3 | Drop |
|---|---|---|---|---|---|
| Mar-2020 | 29.70 | **6.80** | 23.20 | 1.397 | −22.90 |
| Mar-2021 | 46.27 | **7.75** | 38.75 | 1.686 | −38.52 |
| Mar-2022 | 44.52 | **7.59** | 36.87 | 1.696 | −36.93 |
| Mar-2024 | 35.65 | **8.20** | 27.80 | 1.634 | −27.45 |

All v0.3 Z″ values: 6.80–8.20 range (safely above 1.1 threshold; safely below the "stuck high" range of v0.2). The X4' term contribution drops from ~24–41 to ~1.5–1.8 — the MktCap premium was dominating the formula.

**Per-date label summary (v0.2 → v0.3)**:

| Date | v0.2 Label | v0.3 Label | Changed? | Primary driver of change |
|---|---|---|---|---|
| Mar-2020 | WATCH | WATCH | NO | Z″ recovers; N4/N6 no effect; routing identical |
| Mar-2021 | HOLD | HOLD | NO | Z″ recovers; N4 no restoration (FY2019/FY2020 still excluded); N6 no knife-edge |
| Mar-2022 | HOLD | HOLD | NO | Z″ recovers; F5 already included; no knife-edge |
| Mar-2024 | HOLD | HOLD | NO (label) | Z″ recovers; F4 knife-edge resolved (F: 7/9→8/9); label stays HOLD same routing band |

---

## 2. Per-date comparison (v0.2 → v0.3)

### Mar-2020

**v0.2 result (from file 17a)**: WATCH. Z″_v0.2 = 29.70. F-Score = 5/8 (F5 excluded; year-pair FY2018/FY2019 — Asian Paints early Ind AS 116 adoption). FCF/NI = 0.961 (ACCEPTABLE). ROCE ≥60th percentile.

**v0.3 result**: WATCH (label unchanged)

**N1 — Z″ recomputation (Book Equity / TL)**:

- FY2019 data: TA = 16,249 Cr; TL = 6,778 Cr → Book Equity = **9,471 Cr**; X4'_v0.3 = 9,471/6,778 = **1.397**
- X1 = 0.0519, X2_current = 0.1359, X3 = 0.1934 (all unchanged from v0.2)

```
Z″_v0.3 = 6.56 × 0.0519  = +0.3405
         + 3.26 × 0.1359  = +0.4430
         + 6.72 × 0.1934  = +1.2996
         + 1.05 × 1.397   = +1.4669    [was +24.36 in v0.2 (MktCap/TL)]
         + 3.25            = +3.2500
         ─────────────────────────────
         Z″_v0.3 = 6.80      (was 29.70 in v0.2)
```

Still above 1.1 → No halt. Composite check clear (net cash, IC=28.6×, CR=1.14). v0.3 supplementary display: net cash, IC=28.6×, CR=1.14 (no threshold labels fire).

**N4**: Mar-2020 uses year-pair FY2018/FY2019. Asian Paints adopted Ind AS 116 early in FY2019, making this the actual company-level transition pair. v0.3 formally specifies FY2019/FY2020 (mandatory adoption), so strictly the FY2018/FY2019 pair falls outside v0.3's exclusion scope. However, since the early-adopter transition data gap (no lease-liability split from Screener.in) exists regardless, F5 remains effectively excluded in both v0.2 and v0.3 due to data unavailability. **F-Score = 5/8 (unchanged).**

**N6**: No knife-edge signals at Mar-2020. F2 showed a clear YoY decline in ROA (not marginal). Buffer irrelevant. F-Score = 5/8.

**Label change**: SAME (WATCH)
**Improvement?**: PARTIAL — Z″ drops from 29.70 → 6.80, restoring interpretive value. Label and all other signals unchanged.

---

### Mar-2021

**v0.2 result (from file 17a)**: HOLD. Z″_v0.2 = 46.27. F-Score = 7/8 (F5 excluded; year-pair FY2019/FY2020; F5 was a passing signal but excluded). FCF/NI = 1.074 (HIGH-QUALITY EARNINGS). ROCE ≥75th percentile.

**v0.3 result**: HOLD (label unchanged)

**N1 — Z″ recomputation**:

- FY2020 data: TA = 16,138 Cr; TL = 6,008 Cr → Book Equity = **10,130 Cr**; X4'_v0.3 = 10,130/6,008 = **1.686**
- X1 = 0.1167, X2_current = 0.1719, X3 = 0.2096

```
Z″_v0.3 = 6.56 × 0.1167  = +0.7655
         + 3.26 × 0.1719  = +0.5604
         + 6.72 × 0.2096  = +1.4085
         + 1.05 × 1.686   = +1.7703    [was +40.69 in v0.2 (MktCap/TL)]
         + 3.25            = +3.2500
         ─────────────────────────────
         Z″_v0.3 = 7.75      (was 46.27 in v0.2)
```

Still above 1.1 → No halt. Composite check clear (net cash −901 Cr, IC=33.2×, CR=1.323). Supplementary display clean.

**N4 — Key finding for this date**:
- Mar-2021 evaluation uses year-pair FY2019/FY2020 (balance sheet at end of FY2020, compared to FY2019).
- Under v0.3: F5 exclusion applies to FY2019/FY2020 ONLY — which is exactly this year-pair. So F5 remains excluded.
- The v0.3 N4 fix was designed to prevent exclusion at FY2020/FY2021 and later. It does NOT restore F5 at Mar-2021 because Mar-2021 IS the FY2019/FY2020 pair.
- F-Score: **7/8 (unchanged from v0.2)**. The passing F5 signal (borrowings fell 1,320→1,118 Cr) is still excluded due to data-source limitation (lease-liability split unavailable from Screener.in).
- Routing: F=7 ≥ 7 threshold → HOLD tier. FCF/NI=1.074 (≥1.0). ROCE≥75. **HOLD confirmed.**

**N6**: No knife-edge at Mar-2021. F4: OCF=3,038 vs NI=2,774 — OCF exceeds NI by ₹264 Cr (clear pass). All YoY signals well away from ±1% threshold. Buffer irrelevant. **F=7/8 (unchanged).**

**Label change**: SAME (HOLD)
**Improvement?**: PARTIAL — Z″ recovers from an uninformative 46.27 to a meaningful 7.75. N4 and N6 have no effect at this date.

---

### Mar-2022

**v0.2 result (from file 17a)**: HOLD (upgraded from v0.1 FLAG). Z″_v0.2 = 44.52. F-Score = 7/9 (no F-Score exclusions; year-pair FY2020/FY2021). FCF/NI = 1.121 (HIGH-QUALITY EARNINGS). ROCE ≥75th percentile. Beneish: BENEISH-CAUTION (COVID-WINDOW + 0 governance flags).

**v0.3 result**: HOLD (label unchanged)

**N1 — Z″ recomputation**:

- FY2021 data: TA = 20,355 Cr; TL = 7,549 Cr; Book Equity = **12,806 Cr** (given directly in file 17a)
- X4'_v0.3 = 12,806 / 7,549 = **1.696**
- X1 = 0.1080, X2_current = 0.1575, X3 = 0.1997

```
Z″_v0.3 = 6.56 × 0.1080  = +0.7085
         + 3.26 × 0.1575  = +0.5135
         + 6.72 × 0.1997  = +1.3420
         + 1.05 × 1.696   = +1.7808    [was +38.71 in v0.2 (MktCap/TL)]
         + 3.25            = +3.2500
         ─────────────────────────────
         Z″_v0.3 = 7.59      (was 44.52 in v0.2)
```

Still above 1.1 → No halt. Composite check: Net Debt = 1,093 − 4,737 = −3,644 Cr (strongly net cash). IC = 44.2×. CR = 1.30. v0.3 supplementary adds CR display: CR=1.30 → no threshold labels (< 1.0 for "Tight"). All clean.

**N4**: Mar-2022 uses year-pair FY2020/FY2021. Under both v0.2 and v0.3, F5 was INCLUDED at this year-pair (FY2020/FY2021 is outside the Ind AS 116 exclusion window). F5=1 (leverage fell; borrowings 1,118→1,093 Cr; LTD/AvgTA 0.0690→0.0599). No change. **F=7/9 (unchanged).**

**N6**: Mar-2022 signals: F2=1 (ROA improved 0.1713→0.1758, clear), F4=1 (OCF 3,683 vs NI 3,207, large margin), F5=1, F8=1 (GM improved 20.59→22.36%), F9=0 (asset turnover fell, clear fail). No knife-edge signals. Buffer irrelevant. **F=7/9 (unchanged).**

Beneish two-stage: BENEISH-CAUTION (same as v0.2 — no changes to Beneish logic affect this date).

**Label change**: SAME (HOLD)
**Improvement?**: PARTIAL — Z″ drops from 44.52 → 7.59. No change to F-Score, FCF/NI, ROCE, or label. Z″ now informative.

---

### Mar-2024

**v0.2 result (from file 17a)**: HOLD. Z″_v0.2 = 35.65. F-Score = 7/9 (F4=0 knife-edge: OCF 4,193 < NI 4,195 by ₹2 Cr). FCF/NI = 0.822 (ACCEPTABLE). ROCE ≥60th percentile.

**v0.3 result**: HOLD (label unchanged; F-count improves)

**N1 — Z″ recomputation**:

- FY2023 data: TA = 25,779 Cr; TL = 9,787 Cr; Book Equity = **15,992 Cr** (given directly in file 17a)
- X4'_v0.3 = 15,992 / 9,787 = **1.634**
- X1 = 0.1977, X2_current = 0.1628, X3 = 0.2096

```
Z″_v0.3 = 6.56 × 0.1977  = +1.2969
         + 3.26 × 0.1628  = +0.5307
         + 6.72 × 0.2096  = +1.4085
         + 1.05 × 1.634   = +1.7157    [was +29.19 in v0.2 (MktCap/TL)]
         + 3.25            = +3.2500
         ─────────────────────────────
         Z″_v0.3 = 8.20      (was 35.65 in v0.2)
```

Still above 1.1 → No halt. Composite check: Net Debt = 1,933 − 4,262 = −2,329 Cr (net cash). IC = 37.5×. CR = 1.53. v0.3 supplementary adds CR: 1.53 → no threshold labels. All clean.

**N4**: Mar-2024 uses year-pair FY2022/FY2023 — well outside the Ind AS 116 exclusion window. F5 was included in v0.2 (F5=0: borrowings rose from FY2022→FY2023, not an exclusion issue). No change under v0.3. **F5=0 (same).**

**N6 — Materiality buffer — the key change at this date**:

- F4 signal: OCF_t = 4,193 Cr vs NI_t = 4,195 Cr. Difference = −₹2 Cr.
- v0.2: F4 = 0 (strict: OCF < NI).
- v0.3: F4 passes if OCF_t > 0.99 × NI_t.
  - Threshold: 0.99 × 4,195 = **4,153.05 Cr**
  - OCF = 4,193 Cr > 4,153.05 Cr → **F4 = 1 under v0.3**
- This eliminates the knife-edge. At a ₹25,000+ Cr asset scale, ₹2 Cr difference is rounding noise (0.05% of NI). The ±1% buffer correctly identifies this as immaterial.
- F4 changes: 0 → **1**

Updated F-Score table:

| F1 | F2 | F3 | **F4** | F5 | F6 | F7 | F8 | F9 | **Total** |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 1 | **1** (was 0) | 0 | 1 | 1 | 1 | 1 | **8/9** (was 7/9) |

- F-Score: **8/9** (up from 7/9 in v0.2).
- Check other YoY buffer signals at Mar-2024: F2 (ΔROA = ROA_FY2023/ROA_FY2022): FY2023 NI = 4,195 Cr, FY2022 NI = 3,085 Cr → ROA clearly improved. Not knife-edge. F8 (ΔGM): file 17a shows F8=1 clearly. F9 (ΔAT): F9=1 clearly. F5 (ΔLev): F5=0 clearly. No other knife-edge signals.

**Action label routing**:
- F = 8 → tier F≥7. FCF/NI = 0.822 (ACCEPTABLE ≥0.7). ROCE ≥60.
- Row "F≥7, FCF≥0.7, ROCE≥40" → **HOLD**. Label unchanged from v0.2.
- However, F=8/9 is stronger than F=7/9. The F-count improvement is real: one knife-edge false-fail eliminated. Under hysteresis logic, the stock is now at "F≥7 stable" more cleanly.

**Label change**: SAME (HOLD)
**Improvement?**: YES (partial) — F4 knife-edge resolved (F-Score improves 7→8/9). Label stays HOLD because the routing band is the same. The improvement is signal-quality: F=8/9 at Mar-2024 is a stronger reading than F=7/9. The ₹2 Cr OCF–NI gap is no longer artificially penalizing what is effectively a perfect earnings quality year by all other metrics.

---

## 3. New issues v0.3 introduces (if any)

**Issue A — Z″ with Book Equity/TL: the v0.1 "stuck high for mature firms" problem partially returns**

v0.3 reverts X4' to Book Equity/TL, citing that MktCap/TL "made Z″ non-discriminative for premium-valued names." The fix works: Z″ drops from 30–46 (v0.2) to 6.8–8.2 (v0.3), which is a meaningful range.

However, Asian Paints' Book Equity / TL ratios range from 1.40–1.70× across the 4 dates. This is moderate — not inflated by accumulated reserves in the way that v0.1 worried about for "mature firms with accumulated reserves > 200% EBITDA." Asian Paints is profitable and growing, so reserves accumulate, but at the pace justified by earnings.

The v0.1 problem (Retained Earnings/TA as X2 being "stuck high" for old firms) is now handled by X2_current = NPAT_TTM/TA — that fix is retained in v0.3. The v0.1 problem with X4' (Book Equity/TL inflated by decades of reserves) manifests more strongly for firms like HDFC (pre-HDFC Bank merger) or old PSU companies. For Asian Paints, Book Equity = 9,471→15,992 Cr against TL = 6,778→9,787 Cr — the ratio stays in a 1.4–1.7× band that is proportionate to a profitable, low-leverage company. Not a problem here.

**Verdict**: the v0.1 "stuck high" concern does NOT materialize for Asian Paints specifically. The supplementary leverage display (ND/EBITDA + IC + Current Ratio) remains the primary distress signal, and Z″ now functions as an appropriate corroborating sanity-check rather than an outlier.

**Issue B — N4 does not benefit Asian Paints despite being designed in response to Asian Paints data**

The v0.3 spec explicitly says N4 addresses "Asian Paints Mar-2021 lost a passing F5." However, the re-test shows that Mar-2021 uses the FY2019/FY2020 year-pair — the exact year-pair v0.3 retains the F5 exclusion for. The v0.3 fix prevents over-exclusion at FY2020/FY2021 and later, but that over-exclusion was never applied in file 17a's v0.2 implementation for Asian Paints (file 17a correctly excluded F5 only at FY2019/FY2020 and included it at FY2020/FY2021+).

This suggests one of two things: (a) the v0.3 spec's N4 motivation was based on an incorrect reading of which year-pair maps to Mar-2021, OR (b) the v0.3 spec intended to restore F5 even at the FY2019/FY2020 pair (once enough time has passed and financial-debt-only figures become available). If interpretation (b) is intended — i.e., that F5 should be COMPUTED (not excluded) at FY2019/FY2020 using financial-debt-only figures — then the fix is correct in design but inoperational until the data source (annual report lease-liability split) is available.

**Practical consequence**: F=7/8 at Mar-2021 under both v0.2 and v0.3 (label = HOLD both). N4 has no observable effect on this test set.

---

## 4. v0.3 score for Asian Paints

| Change | Applied? | Observable effect on Asian Paints | Score |
|---|---|---|---|
| **N1 — Z″ X4' revert** | YES | Z″ drops from 30–46 → 6.8–8.2 range. Metric recovers interpretive value. No halt in either version, but v0.3 Z″ is now a meaningful "no-distress" indicator. | **IMPROVED** |
| **N4 — F5 Ind AS 116 narrowing** | NOMINAL | Mar-2021 uses FY2019/FY2020 pair → F5 still excluded under v0.3 as under v0.2. Mar-2022/Mar-2024 already had F5 included under v0.2. No observable change across 4 dates. | **NO EFFECT** |
| **N6 — Materiality buffer** | YES | Mar-2024 F4 knife-edge resolved: F-Score improves 7/9 → 8/9. Action label stays HOLD (same routing band), but signal quality improves (one artificial fail eliminated). | **IMPROVED** |

**Score: 2 of 3 changes have observable effect on Asian Paints. N1 and N6 improve the output quality; N4 has no measurable impact on this test set.**

---

## 5. One sentence to Pranav

For Asian Paints specifically, v0.3 improves on v0.2 because N1 restores Z″ to a meaningful 6.8–8.2 range (vs the uninformative 30–46 outliers in v0.2) and N6 eliminates the Mar-2024 F4 knife-edge (F-Score improves 7→8/9), while N4 has no observable effect since the Mar-2021 evaluation date uses exactly the FY2019/FY2020 year-pair that v0.3 still excludes — meaning the stated motivation for N4 ("restoring Mar-2021's passing F5") is technically sound in spec but does not materialize in the data because the exclusion correctly applies to that year-pair regardless of version.
