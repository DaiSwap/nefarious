# 19b — Cycle A A.9: Tata Steel v0.3 Re-test

**Status**: ✅ A.9 Tata Steel v0.3 re-test complete.
**Date**: 2026-05-31
**Stock**: Tata Steel — commodity cyclical (Metals & Mining)
**Method**: re-applied v0.3 math to existing data from v0.2 re-test (file 17b)
**Last updated**: 2026-05-31T01:00:00

---

## Pre-computation notes

All raw financial data taken verbatim from file 17b (v0.2 re-test). No new data fetched. Derived series used for N7 5-yr window:

**Reconstructed from file 17b (back-calculated from 3-yr moving-average disclosures):**

| FY | EBIT (Cr) | OCF (Cr) | NI (Cr) | TA (Cr) | GM% | Rev/TA |
|---|---|---|---|---|---|---|
| FY2018 | 15,691 | 8,023 | 17,743 | 208,723 | 17.4% | 0.591 |
| FY2019 | 21,977 | 25,336 | 9,122 | 232,773 | 18.6% | 0.713 |
| FY2020 | 9,021 | 20,169 | 1,174 | 249,149 | 12.48% | 0.580 |
| FY2021 | 21,271 | 44,327 | 8,190 | 243,910 | 19.5% | 0.636 |
| FY2022 | 54,408 | 44,381 | 41,749 | 282,422 | 26.01% | 0.926 |
| FY2023 | 22,946 | 21,683 | 8,075 | 285,396 | 13.26% | 0.856 |

*Sources: EBIT from IC ratios + 3-yr-avg consistency checks in file 17b. TA from balance sheets. GM% back-calculated from 3-yr-avg GM disclosed at each evaluation date. Rev/TA back-calculated from 3-yr-avg disclosures.*

---

## 2. Per-date comparison (v0.2 → v0.3)

### Mar-2020 (TROUGH)

**v0.2 result (from file 17b)**:
- Beneish M = −2.794; BENEISH-INERT: NOT fired (D&A/Revenue = 4.65%, v0.2 trigger was D&A/Rev > 15%)
- Z″_v0.2 = 6.553 (MktCap/TL = 1.860); v0.2 X4' = MktCap/TL
- FCF/NI = 1.615 — no IMPAIRMENT-CHECK (below 3.0×)
- F-Score (cycle-adj 3-yr) = 7/9
- Action label: **HOLD**

**v0.3 recomputation:**

**N1 — Z″ X4' revert (Book Equity / TL):**

| Term | v0.1 / v0.3 value | v0.2 value | Change |
|---|---|---|---|
| X4' numerator | Book Equity = 69,925 Cr | MktCap = 302,940 Cr | — |
| X4' = BkEq or MktCap / TL | 69,925 / 162,848 = **0.4294** | 302,940 / 162,848 = **1.860** | Large drop |
| 1.05 × X4' contribution | 0.4509 | 1.9530 | −1.502 |
| Z″_v0.3 | 0.5877 + 0.1278 + 0.6343 + **0.4509** + 3.25 = **5.051** | 6.553 | −1.502 |

Z″ drops from 6.55 to 5.05 — still in PASS territory (> 2.6). The composite check (old firm) at this date had 0/3 breaches in v0.2; with v0.3 Z″ = 5.05, still well above the grey-zone floor of 2.6. **No halt. Same verdict — PASS.**

Supplementary display (v0.3 adds Current Ratio threshold):
- Net Debt / EBITDA ≈ 3.9× (below 4.0× — no "Elevated" label)
- Interest Coverage = 2.87× (above 2.0× — no "Low" label)
- Current Ratio = 1.33 (above 1.0 — no "Tight" label)

Result: Z″ = 5.05. Clean. Pipeline continues.

**N3 — BENEISH-INERT redesign:**

TATA = (NI − OCF) / TA = (9,122 − 25,336) / 232,773 = −16,214 / 232,773 = **−0.06967**

α · TATA = 2.0 × (−0.06967) = **−0.13934**

|α · TATA| = **0.139**

Threshold: > 1.0? **NO — BENEISH-INERT does NOT fire.**

The TATA term shifts M-Score by only 0.14 units in absolute terms. Well below the 1.0 threshold. Beneish continues to run normally. M = −2.794 (unchanged from v0.2; α = 2.0 was already applied in v0.2).

**N5 — FCF/NI annotation:**

FCF/NI mean-of-ratios = 1.615 (below 3.0× cap). No annotation fires — neither IMPAIRMENT-CHECK (v0.2) nor ROUTINE-CHARGES (v0.3). No change.

**N7 — 5-yr cyclical window:**

Mar-2020 evaluation uses FY2019 data as "t". The 5-yr t-window would span FY2015–FY2019; t-1 window would span FY2014–FY2018. Data for FY2015–FY2017 is not in the dataset.

**→ WINDOW-SHORT flag fires.** Only 2 years of data available (FY2018–FY2019) for the t-window baseline. v0.3 §9.3: "fall back to the longest available window and tag WINDOW-SHORT: only N years available."

v0.3 falls back to 2-yr window (same as what v0.2 used, which already noted "FY2017 data not in dataset"). The F-Score is unchanged from v0.2: **7/9** with WINDOW-SHORT tag.

**v0.3 F-Score (Mar-2020) = 7/9 (same as v0.2, WINDOW-SHORT flagged)**

**Label change**: HOLD → HOLD. **SAME.**

**Summary table (Mar-2020):**

| Mechanism | v0.2 | v0.3 | Changed? |
|---|---|---|---|
| Z″ | 6.553 (MktCap/TL) | **5.051** (BkEq/TL) | YES — drops 1.5 pts; still PASS |
| BENEISH-INERT | Not fired (D&A proxy) | Not fired (|α·TATA| = 0.139 < 1.0) | NO |
| FCF/NI annotation | No annotation | No annotation | NO |
| F-Score | 7/9 (3-yr, WINDOW-SHORT) | 7/9 (WINDOW-SHORT same) | NO |
| Action label | HOLD | **HOLD** | NO |

**Improvement? PARTIAL** — Z″ drops toward a more realistic value (5.05 vs inflated v0.2 6.55 from market-cap term at depressed stock price). Verdict unchanged. Z″ = 5.05 at trough is actually slightly more informative than 6.55 — it correctly reflects the leveraged balance sheet without being propped up by market cap.

---

### Mar-2021 (COVID trough / FY2020 data)

**v0.2 result (from file 17b)**:
- Beneish M = −2.782; BENEISH-INERT: NOT fired (D&A/Revenue = 6.0%)
- Z″_v0.2 = 9.826 (MktCap/TL = 4.952 — stock had already rallied from COVID lows)
- FCF/NI raw = 6.803 → capped 3.0× → **IMPAIRMENT-CHECK fires**
- Supplementary: Net Debt/EBITDA = 7.4× (High); IC = 1.20× (Low)
- F-Score (cycle-adj 3-yr) = 5/9
- Action label: **REVIEW** (with cyclical caveat + distress-proximity note)

**v0.3 recomputation:**

**N1 — Z″ X4' revert:**

| Term | v0.1 / v0.3 value | v0.2 value | Change |
|---|---|---|---|
| X4' = BkEq or MktCap / TL | 73,576 / 175,573 = **0.4190** | 869,550 / 175,573 = **4.952** | Large drop |
| 1.05 × X4' contribution | 0.4400 | 5.1996 | −4.760 |
| Z″_v0.3 | 0.9177 + 0.01536 + 0.2432 + **0.4400** + 3.25 = **4.876** | 9.826 | −4.950 |

Z″ collapses from 9.83 to 4.88. Still in PASS territory (> 2.6), but much lower. More importantly: **Z″ = 4.88 combined with the supplementary display (ND/EBITDA=7.4× High; IC=1.20× Low; CR=1.589 no flag) now gives a picture of meaningful financial stress that is NOT masked by market-cap inflation.**

This is the best N1 outcome: at Mar-2021, v0.2's MktCap/TL (stock had already rallied) produced Z″ = 9.83, which was actively misleading — it made the balance sheet look stronger precisely because the stock price had recovered, even though leverage had peaked. v0.3's Z″ = 4.88 is lower and more honest. The supplementary display that surfaced ND/EBITDA=7.4× and IC=1.20× remains in v0.3 (it's unchanged), but now Z″ itself no longer contradicts the story.

Composite check (old firm, >30 years): same as v0.2 — 2/3 thresholds breach (ND/EBITDA=7.4× and IC=1.20×; CR=1.589 safe). No halt (all three required). Supplementary display unchanged.

Current Ratio = 1.589 → above 1.0 and 0.7 → no "Tight" or "Very Tight" label (v0.3 new CR addition to supplementary display).

**N3 — BENEISH-INERT redesign:**

TATA = (NI − OCF) / TA = (1,174 − 20,169) / 249,149 = −18,995 / 249,149 = **−0.07625**

α · TATA = 2.0 × (−0.07625) = **−0.15250**

|α · TATA| = **0.153**

Threshold: > 1.0? **NO — BENEISH-INERT does NOT fire.**

Despite this being the COVID trough year with near-zero NI and OCF >> NI by a large margin, the TATA contribution to M-Score magnitude is only 0.15 units — well below 1.0. Reason: even though OCF >> NI in ratio terms (ratio = 17.2×), the difference in absolute terms is ₹18,995 Cr vs TA of ₹249,149 Cr — only 7.6% of assets.

**N5 — FCF/NI annotation (ROUTINE-CHARGES fires):**

Raw FCF/NI = 6.803 → capped at 3.0×. CashConversion > 3.0×.

v0.2 → v0.3 annotation change:
- v0.2: *"IMPAIRMENT-CHECK: Cash conversion exceeds 3.0× ... investigate impairment schedule..."*
- v0.3: *"ROUTINE-CHARGES: CashConversion = 6.80× (capped at 3.0×) — large non-cash charges (depreciation on heavy assets, periodic impairments) are routine for this sector. Treat as context, not signal."*

**ROUTINE-CHARGES fires instead of IMPAIRMENT-CHECK. Annotation tone changes from investigative to contextual.**

Label stays: HIGH-QUALITY EARNINGS (≥ 1.0 after cap). Same routing verdict.

**N7 — 5-yr window:**

Mar-2021 evaluation: "t" = FY2020. 5-yr t-window = FY2016–FY2020; t-1 window = FY2015–FY2019. FY2015–FY2017 data not available.

**→ WINDOW-SHORT flag fires.** Fall back to longest available: 3-yr (FY2018–FY2020), same as v0.2.

F-Score unchanged: **5/9** with WINDOW-SHORT tag.

**Label change**: REVIEW → REVIEW. **SAME.**

**Summary table (Mar-2021):**

| Mechanism | v0.2 | v0.3 | Changed? |
|---|---|---|---|
| Z″ | 9.826 (MktCap/TL = 4.95×) | **4.876** (BkEq/TL = 0.419) | YES — drops 4.95 pts; still PASS but now honest |
| BENEISH-INERT | Not fired (D&A proxy) | Not fired (|α·TATA| = 0.153 < 1.0) | NO |
| FCF/NI annotation | IMPAIRMENT-CHECK | **ROUTINE-CHARGES** | YES — tone change |
| F-Score | 5/9 (WINDOW-SHORT) | 5/9 (WINDOW-SHORT same) | NO |
| Action label | REVIEW + caveats | **REVIEW** + caveats | NO |

**Improvement? PARTIAL** — Z″ is now 4.88 (not inflated by post-COVID rally in stock price). The picture is more internally consistent: Z″ at moderate-pass levels, supplementary display showing High leverage and Low coverage. v0.2's Z″=9.83 was actively misleading (implying "very safe" when leverage was at peak stress). ROUTINE-CHARGES is a tone improvement — less alarmist for a routine heavy-industry situation.

---

### Mar-2022 (CYCLE PEAK / FY2021 data)

**v0.2 result (from file 17b)**:
- Beneish M = −2.803; BENEISH-INERT: NOT fired (D&A/Revenue = 5.9%)
- Z″_v0.2 = 13.377 (MktCap/TL = 8.788 — super-cycle stock price at peak)
- FCF/NI raw = 8.457 → capped 3.0× → **IMPAIRMENT-CHECK fires**
- Supplementary: ND/EBITDA ≈ 3.3×, IC = 2.80× — clean (no "Elevated" or "Low" labels)
- F-Score (cycle-adj 3-yr) = 8/9
- Action label: **WATCH** (F=8 but ROCE=21st percentile < 40 → WATCH routing)

**v0.3 recomputation:**

**N1 — Z″ X4' revert:**

| Term | v0.1 / v0.3 value | v0.2 value | Change |
|---|---|---|---|
| X4' = BkEq or MktCap / TL | 74,231 / 169,670 = **0.4375** | 1,490,840 / 169,670 = **8.788** | Massive drop |
| 1.05 × X4' contribution | 0.4594 | 9.2274 | −8.768 |
| Z″_v0.3 | 0.2139 + 0.1094 + 0.5860 + **0.4594** + 3.25 = **4.619** | 13.377 | −8.758 |

Z″ collapses from 13.38 to 4.62 — the most dramatic N1 delta of all 4 dates. This is because Mar-2022 was the cycle peak when Tata Steel's market cap was ~₹1.49 lakh Cr (stock near all-time highs). In v0.2, the super-cycle market cap dominated X4' and inflated Z″ to 13.38. In v0.3, the book equity tells a far more conservative story. Z″ = 4.62 is still a PASS (> 2.6), but it no longer gives the false impression of an extremely sound balance sheet.

This is the most analytically important N1 result. At a commodity cycle peak, v0.2's MktCap-based Z″ was highest (13.38) — precisely the wrong time to signal strength. v0.3 reverts to 4.62, which correctly shows "acceptable but not exceptional."

Composite check (old firm): ND/EBITDA = 3.3×, IC = 2.80×, CR = 1.098 — 0/3 breaches. No halt.

Current Ratio = 1.098 → above 1.0 → no "Tight" label (v0.3 new addition). Clean supplementary display.

**N3 — BENEISH-INERT redesign:**

TATA = (NI − OCF) / TA = (8,190 − 44,327) / 243,909 = −36,137 / 243,909 = **−0.14814**

α · TATA = 2.0 × (−0.14814) = **−0.29628**

|α · TATA| = **0.296**

Threshold: > 1.0? **NO — BENEISH-INERT does NOT fire.**

This is the highest |α·TATA| value across all 4 dates (0.296), yet it still falls well short of the 1.0 threshold. At Mar-2022, OCF was ₹44,327 Cr vs NI ₹8,190 Cr — a ratio of 5.4× — because the massive FY2021 recovery generated huge operating cash flows while NI was still catching up. Despite this, |α·TATA| = 0.296 shows the TATA contribution only shifts M by ~0.3 units — not the 1.0+ needed to dominate.

**N5 — FCF/NI annotation (ROUTINE-CHARGES fires):**

Raw FCF/NI = 8.457 → capped at 3.0×. CashConversion > 3.0×.

- v0.2 annotation: IMPAIRMENT-CHECK
- v0.3 annotation: *"ROUTINE-CHARGES: CashConversion = 8.46× (capped at 3.0×) — large non-cash charges (depreciation on heavy assets, periodic impairments) are routine for this sector. Treat as context, not signal."*

**ROUTINE-CHARGES fires. Tone change from investigative to contextual.**

Label: HIGH-QUALITY EARNINGS. Same.

**N7 — 5-yr window:**

Mar-2022 evaluation: "t" = FY2021. 5-yr t-window = FY2017–FY2021; t-1 window = FY2016–FY2020. FY2016–FY2017 data not available.

**→ WINDOW-SHORT flag fires.** Fall back to 3-yr (FY2019–FY2021), same as v0.2.

However, for the t-window if we use FY2018–FY2021 (4 years available):
- avg EBIT/TA: (15,691+21,977+9,021+21,271)/4 / avg TA = not a clean comparison
- For consistency, v0.3 falls back to 3-yr (uses FY2019–FY2021 as the 3-yr available approximating the ideal 5-yr). Same as v0.2.

F-Score: **8/9 (WINDOW-SHORT, same as v0.2)**. All 9 signals unchanged.

Action label: F=8, FCF/NI=3.0× (capped, ≥1.0), ROCE=21st (<40) → WATCH (same routing as v0.2).

**Label change**: WATCH → WATCH. **SAME.**

**Summary table (Mar-2022):**

| Mechanism | v0.2 | v0.3 | Changed? |
|---|---|---|---|
| Z″ | 13.377 (MktCap/TL = 8.79×) | **4.619** (BkEq/TL = 0.438) | YES — drops 8.76 pts; most dramatic N1 delta; still PASS |
| BENEISH-INERT | Not fired (D&A proxy) | Not fired (|α·TATA| = 0.296 < 1.0) | NO |
| FCF/NI annotation | IMPAIRMENT-CHECK | **ROUTINE-CHARGES** | YES — tone change |
| F-Score | 8/9 (WINDOW-SHORT) | 8/9 (WINDOW-SHORT same) | NO |
| Action label | WATCH | **WATCH** | NO |

**Improvement? YES (for Z″ specifically)** — Z″ at cycle peak drops from 13.38 (inflated by super-cycle market cap) to 4.62 (honest book-equity picture). This is the most analytically correct N1 result: the model no longer looks most "safe" at the cycle peak, which was a structural failure of v0.2's MktCap/TL. Z″ pattern across 4 dates in v0.3 is now [5.05, 4.88, 4.62, 4.72] — relatively stable and interpretable, rather than v0.2's [6.55, 9.83, 13.38, 15.83] which co-moved perfectly with the stock price cycle.

---

### Mar-2024 (POST-SUPER-CYCLE / FY2023 data)

**v0.2 result (from file 17b)**:
- Beneish M = −2.235 (closest to threshold of all 4 dates); BENEISH-INERT: NOT fired (D&A/Rev = 3.8%)
- Z″_v0.2 = 15.833 (MktCap/TL = 11.160 — large-cap post-super-cycle stock price)
- FCF/NI raw = 3.054 → capped 3.0× (borderline) → **IMPAIRMENT-CHECK fires**
- Supplementary: ND/EBITDA = 2.9×, IC = 3.65× — clean
- F-Score (cycle-adj 3-yr) = 7/9 (F2, F8, F9 flipped 0→1 via 3-yr window including FY2022 peak)
- Action label: **WATCH** (F=7 but ROCE=36th <40 → WATCH routing)

**v0.3 recomputation:**

**N1 — Z″ X4' revert:**

| Term | v0.1 / v0.3 value | v0.2 value | Change |
|---|---|---|---|
| X4' = BkEq or MktCap / TL | 103,036 / 182,314 = **0.5654** | 2,034,892 / 182,314 = **11.160** | Massive drop |
| 1.05 × X4' contribution | 0.5937 | 11.718 | −11.124 |
| Z″_v0.3 | 0.2329 + 0.09222 + 0.5403 + **0.5937** + 3.25 = **4.719** | 15.833 | −11.114 |

Z″ drops from 15.83 to 4.72. The v0.2 value of 15.83 was almost entirely driven by market cap (₹2.03 lakh Cr at Mar-2024 prices for a heavily owned large-cap). With book equity/TL, the picture is Z″ = 4.72 — a moderate pass, consistent with a company that has improved its balance sheet (BkEq/TL = 0.565, higher than earlier years) but is not distress-free.

Composite check: ND/EBITDA = 2.9×, IC = 3.65×, CR = 1.104 — 0/3 breaches. Supplementary clean.

Current Ratio = 1.104 → above 1.0 → no "Tight" label. Clean.

**N3 — BENEISH-INERT redesign:**

TATA = (NI − OCF) / TA = (8,075 − 21,683) / 285,396 = −13,608 / 285,396 = **−0.04769**

α · TATA = 2.0 × (−0.04769) = **−0.09538**

|α · TATA| = **0.095**

Threshold: > 1.0? **NO — BENEISH-INERT does NOT fire.**

This is the smallest |α·TATA| value of all 4 dates. Post-super-cycle normalization means both NI and OCF are more normalized (FY2023 NI = 8,075, OCF = 21,683 — a 2.68× ratio vs 17× in FY2020). TATA contribution is minimal. Beneish continues to run; M = −2.235 (unchanged from v0.2) with the context note that GMI=1.961 and AQI=1.411 are analytically dominant.

**N5 — FCF/NI annotation (ROUTINE-CHARGES fires, borderline):**

Raw FCF/NI = 3.054 → capped at 3.0×. CashConversion barely above 3.0× (0.054 above threshold).

- v0.2: IMPAIRMENT-CHECK (borderline note)
- v0.3: *"ROUTINE-CHARGES: CashConversion = 3.05× (capped at 3.0×) — large non-cash charges are routine for this sector. Note: borderline case, primarily driven by FY2021 near-zero NI pulling up the 3-yr average ratio."*

**ROUTINE-CHARGES fires (borderline). Label unchanged: HIGH-QUALITY EARNINGS.**

**N7 — 5-yr cyclical window (the critical test):**

For Mar-2024, "t" = FY2023. Full 5-yr data IS available: FY2019–FY2023 (data from file 17b).

5-yr t-window: FY2019, FY2020, FY2021, FY2022, FY2023
5-yr t-1 window: FY2018, FY2019, FY2020, FY2021, FY2022

**F1 (5-yr avg EBIT/TA_t > 0):**
avg EBIT(FY2019-23) = (21,977 + 9,021 + 21,271 + 54,408 + 22,946)/5 = 129,623/5 = 25,924.6 Cr
avg TA(FY2019-23) = (232,773 + 249,149 + 243,910 + 282,422 + 285,396)/5 = 1,293,650/5 = 258,730 Cr
5-yr avg EBIT/TA_t = 25,924.6 / 258,730 = **0.1002** > 0 → **F1 = 1**

**F2 (5-yr avg EBIT/TA_t vs _t-1):**
avg EBIT(FY2018-22) = (15,691 + 21,977 + 9,021 + 21,271 + 54,408)/5 = 122,368/5 = 24,473.6 Cr
avg TA(FY2018-22) = (208,723 + 232,773 + 249,149 + 243,910 + 282,422)/5 = 1,216,977/5 = 243,395.4 Cr
5-yr avg EBIT/TA_{t-1} = 24,473.6 / 243,395.4 = **0.1006**

Comparison: 0.1002 vs 0.1006 → declined by 0.0004 (0.04%).
With ±1% materiality buffer: threshold = 0.99 × 0.1006 = 0.09959. Is 0.1002 > 0.09959? **YES (barely — 0.1002 > 0.09959).**
**F2 = 1** (passes only because of the ±1% buffer; without buffer, F2 = 0)

The 3-yr v0.2 F2 was 1 (0.121 > 0.109). In v0.3 with 5-yr, F2 is nominally 0 but rescued by the ±1% buffer. The 5-yr window nearly eliminates the mechanical advantage that the 3-yr window gave — the FY2022 super-cycle peak has proportionally similar weight in both t and t-1 windows over 5 years.

**F3 (5-yr avg OCF/TA > 0):**
avg OCF(FY2019-23) = (25,336 + 20,169 + 44,327 + 44,381 + 21,683)/5 = 155,896/5 = 31,179.2 Cr
5-yr avg OCF/TA = 31,179.2 / 258,730 = **0.1205** > 0 → **F3 = 1**

**F4, F5, F6, F7 (unchanged — single-year or non-normalized):**
F4 = 1 (OCF 21,683 > NI 8,075), F5 = 0 (leverage rose), F6 = 0 (CR fell), F7 = 1 (shares flat)

**F8 (5-yr avg GM):**
5-yr avg GM t-window (FY2019-23) = (18.6 + 12.48 + 19.5 + 26.01 + 13.26)/5 = 89.85/5 = **17.97%**
5-yr avg GM t-1-window (FY2018-22) = (17.4 + 18.6 + 12.48 + 19.5 + 26.01)/5 = 93.99/5 = **18.80%**

Comparison: 17.97% vs 18.80% → declined by 0.83%.
With ±1% buffer: threshold = 0.99 × 18.80 = 18.612%. Is 17.97 > 18.612? **NO.**
**F8 = 0** — GM declined on 5-yr avg basis. This is a genuine improvement vs v0.2.

In v0.2's 3-yr window: t-window (FY2021-23) avg GM = 19.59% vs t-1 (FY2020-22) = 19.33% → F8 = 1 (trivial +0.26% lift, window mechanics). In v0.3's 5-yr window: t drops to 17.97% because FY2023's terrible 13.26% drags down the average while t-1's FY2018 (17.4%) exits. This correctly shows that over the full 5-yr period, Tata Steel's gross margin profile has deteriorated relative to the prior 5-yr period. F8 flip from 1 (v0.2) to 0 (v0.3) is the 5-yr window working as designed — eliminating the window-mechanics artifact.

**F9 (5-yr avg Asset Turnover):**
5-yr avg Rev/TA t-window (FY2019-23) = (0.713 + 0.580 + 0.636 + 0.926 + 0.856)/5 = 3.711/5 = **0.7422**
5-yr avg Rev/TA t-1-window (FY2018-22) = (0.591 + 0.713 + 0.580 + 0.636 + 0.926)/5 = 3.446/5 = **0.6892**

Comparison: 0.7422 vs 0.6892 → improved. With ±1% buffer: 0.7422 > 0.99×0.6892 = 0.6823 → **F9 = 1**.

F9 remains 1 in v0.3 because asset turnover genuinely improved over the 5-yr period — the t-1 window (FY2018-22) includes FY2018 (0.591, low Rev/TA) which was much lower than FY2023 (0.856). The improvement is real: Tata Steel is generating more revenue per unit of assets in the recent 5-yr span.

**v0.3 5-yr F-Score (Mar-2024) = F1+F2+F3+F4+F5+F6+F7+F8+F9 = 1+1+1+1+0+0+1+0+1 = 6/9**

(v0.2 3-yr F-Score was 7/9 — F2, F8, F9 all = 1; v0.3 5-yr: F2 barely survives via buffer, F8 drops to 0, F9 = 1)

**The mechanical artifact is smoothed**: v0.2's F=7 had a known artifact where F8 was +1 due to a trivial 3-yr window shift. v0.3's F=6 eliminates that artifact. F8 now correctly reflects that gross margins have declined over the 5-yr period ending FY2023.

**Action label (Mar-2024):**

v0.3 inputs: F=6 (cycle-adj 5-yr), FCF/NI=3.0× (capped, ≥1.0), ROCE=36th (<50)

Routing table check:
- F=6 (falls in "5–6" row), FCF ≥ 0.7 (yes, ≥ 1.0), ROCE < 50 (yes, 36th)
- Row "5–6, ≥ 0.7, < 50" → **REVIEW**

**v0.3 Label: REVIEW** (v0.2 was WATCH — label **CHANGES, REGRESSES**)

CYCLICAL caveat still applies: *"CYCLICAL-SECTOR WARNING: deteriorating F-Score at sector trough may indicate entry opportunity, not deterioration."*

**Label change**: WATCH → REVIEW. **CHANGED — REGRESSION.**

**Summary table (Mar-2024):**

| Mechanism | v0.2 | v0.3 | Changed? |
|---|---|---|---|
| Z″ | 15.833 (MktCap/TL = 11.16×) | **4.719** (BkEq/TL = 0.565) | YES — drops 11.1 pts; still PASS; more honest |
| BENEISH-INERT | Not fired (D&A proxy) | Not fired (|α·TATA| = 0.095 < 1.0) | NO |
| FCF/NI annotation | IMPAIRMENT-CHECK | **ROUTINE-CHARGES** (borderline) | YES — tone change |
| F8 signal | 1 (3-yr window artifact: +0.26%) | **0** (5-yr: genuine decline −0.83%) | YES — F8 flips 1→0 |
| F-Score (cycle-adj) | **7/9** (3-yr) | **6/9** (5-yr) | YES — drops 1 point |
| Action label | **WATCH** | **REVIEW** | YES — **REGRESSES** |

**Improvement? MIXED** — Z″ is now more honest. F8 artifact correctly eliminated. But the label regression (WATCH → REVIEW) at a post-trough date (+28% vs NIFTY +12% forward) is a step backward in signal quality. The 5-yr window fixes the mechanical artifact but overshoots by demoting the date one label level. This is N7's trade-off: longer window is analytically more correct but does not produce better forward-return alignment for this specific date.

---

## 1. Top-line verdict on v0.3 changes for Tata Steel

| v0.3 change | Behavior on Tata Steel | Verdict |
|---|---|---|
| N1 — Z″ X4' revert | Z″ pattern changes from [6.55, 9.83, 13.38, 15.83] (co-moves with stock price) to [5.05, 4.88, 4.62, 4.72] (stable, book-based). Mar-2021 drops most critically: 9.83→4.88, removing false "very safe" signal at peak leverage. Mar-2022 most dramatic absolute drop: 13.38→4.62. No halt verdicts change. | **FIXED — analytically** |
| N3 — BENEISH-INERT redesign | |α·TATA| values: 0.139 (Mar-2020), 0.153 (Mar-2021), 0.296 (Mar-2022), 0.095 (Mar-2024). All < 1.0. BENEISH-INERT does NOT fire at any of the 4 dates. The new trigger is better-designed (direct impact vs proxy) but has no effect on Tata Steel. | **DOESN'T-FIRE** |
| N5 — ROUTINE-CHARGES annotation | Replaces IMPAIRMENT-CHECK at 3 of 4 dates (Mar-2021, Mar-2022, Mar-2024 — all where FCF/NI cap triggered). Mar-2020 had no cap so no annotation either way. Tone changes from investigative ("investigate impairment schedule") to contextual ("routine for sector"). | **FIXED — tone** |
| N7 — 5-yr window | For Mar-2020, Mar-2021, Mar-2022: WINDOW-SHORT fires (data only goes back to FY2018). Same F-Scores as v0.2. For Mar-2024: 5-yr data available. F-Score drops from 7→6 (F8 loses its window-mechanics boost). Label regresses WATCH→REVIEW. The 3-yr mechanical artifact IS eliminated but the label outcome is worse. | **FIXED analytically, WORSE for label** |

---

## 3. BENEISH-INERT verdict (the most important v0.3 test for Tata Steel)

**At 0 of 4 dates does |α · TATA| > 1.0.**

Full table of TATA term magnitudes:

| Date (data year) | NI (Cr) | OCF (Cr) | TA (Cr) | TATA = (NI−OCF)/TA | α·TATA (α=2.0) | |α·TATA| | Fires? |
|---|---|---|---|---|---|---|---|
| Mar-2020 (FY2019) | 9,122 | 25,336 | 232,773 | −0.06967 | −0.13934 | 0.139 | NO |
| Mar-2021 (FY2020) | 1,174 | 20,169 | 249,149 | −0.07625 | −0.15250 | 0.153 | NO |
| Mar-2022 (FY2021) | 8,190 | 44,327 | 243,909 | −0.14814 | −0.29628 | 0.296 | NO |
| Mar-2024 (FY2023) | 8,075 | 21,683 | 285,396 | −0.04769 | −0.09538 | 0.095 | NO |

**Why BENEISH-INERT does NOT fire for Tata Steel even under v0.3:**

The v0.3 trigger (|α·TATA| > 1.0) requires the TATA term to shift M-Score by more than 1 absolute unit. For Tata Steel with α=2.0, this means TATA itself must exceed 0.5 in magnitude — i.e., |(NI−OCF)/TA| > 0.50. This would require OCF to exceed NI by more than 50% of total assets in a single year.

For that to happen at Tata Steel's scale (TA ≈ ₹250,000–285,000 Cr), (OCF−NI) would need to exceed ~₹125,000–142,500 Cr. The maximum in this dataset was ₹36,137 Cr (Mar-2022). Even in the most extreme year, the TATA contribution is ₹36,137/₹243,909 = 14.8% of TA — only 0.296 units of M-Score impact.

**The v0.3 trigger threshold of 1.0 (implying TATA > 0.5 in TA-normalized terms) appears too strict for steel even at commodity cycle extremes.** Tata Steel's heaviest asset base absorbs the OCF-NI gap, keeping the ratio well below the trigger.

**What BENEISH-INERT firing would mean:** if it fired, the M-Score would be replaced by the Governance Quality Screen as the primary manipulation signal. Since GQS passes cleanly (0/4 flags all dates), the practical effect would be: pipeline continues with GQS note, no change in halt/pass verdict. So even if INERT had fired, the downstream outcome for Tata Steel would have been the same.

**M-Score context at each date (v0.2/v0.3 Beneish output unchanged):**
- Mar-2020: M = −2.794 (GMI = 0.935 — margin slightly improved; AQI = 0.631 — asset intensity fell)
- Mar-2021: M = −2.782 (GMI = 1.488 — significant margin collapse visible; TATA suppression = only −0.153)
- Mar-2022: M = −2.803 (GMI = 0.641 — recovery; large TATA of −0.296 still well below noise floor)
- Mar-2024: M = −2.235 (GMI = 1.961 and AQI = 1.411 dominant; TATA = only −0.095, barely present)

**Conclusion**: BENEISH-INERT's redesign (v0.3 N3) is logically superior to the old D&A/Revenue proxy, but for Tata Steel specifically it doesn't fire at any date. The v0.2 observation in file 17b (§W2 verdict: "incomplete fix — the INERT flag doesn't formally fire") remains true under v0.3's new trigger. The fix works better conceptually but has no operational impact on this stock.

---

## 4. 5-yr window verdict (N7)

**Mar-2024 cycle-adjusted F-Score: v0.2 (3-yr) = 7/9 → v0.3 (5-yr) = 6/9.**

| Signal | v0.2 3-yr result | v0.3 5-yr result | Change | Reason |
|---|---|---|---|---|
| F1 | 1 | 1 | NO | 5-yr avg EBIT/TA_t = 0.1002 > 0 |
| F2 | 1 (0.121 vs 0.109) | 1 (0.1002 vs 0.1006, via ±1% buffer) | NO (buffer saves it) | Marginal: 5-yr averages nearly identical; buffer = the deciding vote |
| F3 | 1 | 1 | NO | 5-yr avg OCF/TA = 0.1205 > 0 |
| F4 | 1 | 1 | NO | Single-year, unchanged |
| F5 | 0 | 0 | NO | Single-year leverage, unchanged |
| F6 | 0 | 0 | NO | Single-year CR, unchanged |
| F7 | 1 | 1 | NO | Discrete share count, unchanged |
| **F8** | **1** (19.59% vs 19.33%, +0.26% window artifact) | **0** (17.97% vs 18.80%, −0.83% genuine decline) | **YES — drops 1→0** | 5-yr window correctly incorporates FY2023's low GM (13.26%) into t-window while FY2018's moderate GM (17.4%) enters t-1 as base; artifact eliminated |
| F9 | 1 | 1 | NO | 5-yr asset turnover: 0.742 vs 0.689, genuine improvement |

**Does the 5-yr window need more historical data than available for Mar-2024?**

No — Mar-2024 evaluation uses FY2023 as "t." The 5-yr t-window (FY2019–FY2023) and t-1 window (FY2018–FY2022) both lie within the available dataset (FY2018–FY2023). Full data is available. **WINDOW-SHORT flag does NOT fire for Mar-2024.**

**Does the artifact smooth out?** YES — F8's +0.26% 3-yr artifact is eliminated. In v0.2, F8=1 because the 3-yr average GM calculation had a trivial improvement as FY2020 (trough year, 12.48%) exited the t-1 window. In v0.3, over 5 years, the FY2022 super-cycle peak (26.01%) is equally present in both t and t-1 windows, and FY2023's post-cycle collapse (13.26%) enters the t-window — correctly showing a 5-yr margin decline.

**Does the score change materially?** F-Score drops by 1 (7→6). Materially, yes — it crosses the F=6/7 boundary that determines WATCH vs REVIEW routing. This is the most consequential N7 effect.

**For Mar-2020, Mar-2021, Mar-2022**: WINDOW-SHORT fires (insufficient historical data for 5-yr). v0.3 falls back to the available window. No F-Score change at these 3 dates.

**The label regression at Mar-2024** (WATCH→REVIEW) is the critical N7 finding: the 5-yr window correctly removes a window artifact but, in doing so, demotes the label at a post-trough entry point that subsequently delivered +28% vs NIFTY +12%. The Spearman correlation between cycle-adjusted F-Score and forward excess return worsens slightly:
- v0.2 F-Scores: [7, 5, 8, 7] — WATCH/REVIEW correctly less negative correlation
- v0.3 F-Scores: [7, 5, 8, 6] — Mar-2024 drops to 6; mild regression

---

## 5. New issues v0.3 introduces for Tata Steel

**5.1 N7 label regression at Mar-2024.** The 5-yr window correctly eliminates the F8 window artifact, but the label regresses from WATCH to REVIEW at a post-trough date. This is the same trade-off noted in the v0.3 spec's confidence table ("5-yr smooths better; trade-off is data requirement") — but the data-availability trade-off here is not the issue; the signal trade-off is. The 5-yr average penalizes Tata Steel for FY2023's post-super-cycle margin collapse more heavily than the 3-yr window did. Whether this is correct depends on whether you think the Mar-2024 evaluation is truly a "trough entry" or a "continued deterioration after a very unusual super-cycle."

**5.2 BENEISH-INERT threshold appears too strict for Metals & Mining even at commodity cycle extremes.** The v0.3 trigger (|α·TATA| > 1.0 with α=2.0) requires OCF-NI to exceed 50% of total assets in a single year — a threshold that Tata Steel never approaches even in the most extreme year (FY2021: 14.8% of TA). The v0.2 D&A/Revenue proxy was wrong (4-6% < 15% trigger); the v0.3 direct-impact trigger is logically cleaner but the threshold may be calibrated for more extreme sectors (power utilities, large-D&A infrastructure) rather than steel. For Tata Steel, the INERT trigger remains non-operational through both v0.2 and v0.3.

**5.3 Z″ stability is now potentially too stable.** v0.3's Z″ pattern [5.05, 4.88, 4.62, 4.72] is remarkably flat across a +355% stock price swing and a full commodity super-cycle. This is correct in that book equity doesn't swing with commodity prices — but it also means Z″ is now completely cycle-unaware. The v0.2 MktCap/TL gave Z″ some cycle-sensitivity (though it moved in the wrong direction — highest at peak). v0.3 reverts to a signal that neither helps nor hurts at cycle turning points. The supplementary leverage display carries all the meaningful information; Z″ is now background noise for Tata Steel.

---

## 6. v0.3 score for Tata Steel

**Label comparison (v0.1 → v0.2 → v0.3):**

| Date | v0.1 Label | v0.2 Label | v0.3 Label | Forward excess | v0.3 better than v0.2? |
|---|---|---|---|---|---|
| Mar-2020 TROUGH | WATCH | HOLD | **HOLD** | +222pp | SAME (no regression) |
| Mar-2021 COVID trough | REVIEW | REVIEW + caveats | **REVIEW** + caveats | +30pp | SAME |
| Mar-2022 PEAK | HOLD | WATCH | **WATCH** | +3pp | SAME (no regression) |
| Mar-2024 post-trough | REVIEW | WATCH | **REVIEW** | +16pp | **WORSE — label regresses** |

**Z″ comparison (v0.1 → v0.2 → v0.3):**

| Date | v0.1 Z″ | v0.2 Z″ | v0.3 Z″ | v0.3 more honest? |
|---|---|---|---|---|
| Mar-2020 | 5.872 | 6.553 | **5.051** | YES — modest drop, closer to v0.1 |
| Mar-2021 | 5.799 | 9.826 | **4.876** | YES — removes market-rally inflation; 4.88 is more honest at peak leverage |
| Mar-2022 | 5.485 | 13.377 | **4.619** | YES — removes super-cycle price inflation; 4.62 is most honest |
| Mar-2024 | 5.780 | 15.833 | **4.719** | YES — removes large-cap inflation; 4.72 is honest |

**Overall v0.3 assessment:**

- N1 (Z″ revert): FIXED analytically. Z″ is now a stable, interpretable, book-based figure. The market-cap dependency introduced in v0.2 is cleanly removed. Critical improvement at Mar-2021 (Z″=9.83→4.88 removes false "very safe" signal at peak leverage) and Mar-2022 (13.38→4.62 removes peak-cycle inflation).
- N3 (BENEISH-INERT): NO-CHANGE in operational terms. Better trigger design; doesn't fire for Tata Steel at any date. The trigger threshold (|α·TATA| > 1.0) is too strict for steel even at extremes.
- N5 (ROUTINE-CHARGES): FIXED in tone. Fires at 3 of 4 dates (same as IMPAIRMENT-CHECK in v0.2). Annotation is more appropriate for a Metals & Mining heavy-asset company.
- N7 (5-yr window): FIXED analytically (F8 artifact eliminated) but WORSE for label quality at Mar-2024. WATCH→REVIEW at the post-trough date (+16pp forward excess) is the only label regression across all 4 dates and both version steps.

**Spearman correlation F-Score vs forward excess:**
- v0.2 F-Scores [7,5,8,7], forward excess [222,30,3,16]: Spearman ≈ −0.20
- v0.3 F-Scores [7,5,8,6], forward excess [222,30,3,16]: Spearman ≈ −0.40

The correlation worsens slightly with v0.3 because Mar-2024's drop from 7→6 makes the F-Score pattern [7,5,8,6] somewhat more correlated with the "wrong" order (highest F at the worst entry, lowest F at a decent entry). The v0.2 pattern [7,5,8,7] was better balanced.

---

## 7. One sentence to Pranav

"v0.3 improves Tata Steel's analytical picture on Z″ (now book-based and honest across the full cycle rather than market-cap-inflated, most critically at Mar-2021 where Z″ drops from a misleading 9.83 to 4.88 at peak leverage) and FCF/NI annotation (ROUTINE-CHARGES is the right label for a sector where heavy non-cash charges are structural), but N3 (BENEISH-INERT redesign) still does not fire for Tata Steel at any date because even at commodity cycle extremes the TATA contribution only reaches 0.296 M-Score units — far below the 1.0 trigger — and N7's 5-yr window, while analytically correct in eliminating the F8 window artifact, causes the only label regression in the entire re-test: Mar-2024 drops from WATCH (v0.2) to REVIEW (v0.3) at a date that subsequently returned +28% vs NIFTY +12%, suggesting the 5-yr window may be too harsh on post-super-cycle cyclicals where the most recent year's margin collapse dominates the average."

---

**Status**: ✅ A.9 Tata Steel v0.3 re-test complete.
**Last updated**: 2026-05-31


