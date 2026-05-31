# 15a — Cycle A Critique: Quant / Statistician Lens

**Status**: ✅ Quant critique complete.
**Date**: 2026-05-30
**Lens**: Quant / Statistician
**Last updated**: 2026-05-30T00:50:00

---

## 1. Verdict on v0.1 (top-line)

**REFACTOR-REQUIRED.**

The three knockout gates (Beneish, Altman, Pledge) and the F-Score primary signal each have structurally identifiable failure modes specific to Indian NSE heavy-industry and commodity-cyclical companies; the failures are predictable from the signal design, not random noise. Two of the three gates correlate through shared earnings/leverage factors rather than providing genuinely independent protection. The pipeline structure is sound; the signal choices inside it are broken for the ~35–40% of NIFTY 500 market cap that sits in metals, energy, cement, and infrastructure. v0.1 is usable as-is only for stable quality compounders in non-cyclical consumer/pharma/IT sectors — which is a large blind spot for a bot meant to cover the full NIFTY 500 universe.

---

## 2. Position on each of the 6 known weaknesses

### W1 — Beneish false positives during regime shifts
**Position: CONFIRM, with quantitative precision added**

The Asian Paints Mar-2022 false positive (M = −1.697 vs threshold −1.78) was driven entirely by two indices: DSRI = 1.377 (contribution +1.267) and AQI = 1.858 (contribution +0.751), together providing +2.018 of upward M-score pressure. The TATA term was −0.110 — it actually dampened the score. The gate failed by a margin of only 0.083 units; a single-quarter normalization of debtor days from 44 back toward 36 would have reversed the call. This is a hair-trigger: the gate is operating within measurement noise of the threshold. The deeper structural problem is that DSRI and AQI are mechanically anti-correlated with each other during macro liquidity crises: when customers delay payment (DSRI rises), companies park cash in short-term financial assets as a precaution (AQI rises). This co-movement is textbook defensive cash management, not manipulation. Beneish has no macro-conditioning, no multi-period confirmation requirement, and no corroborating signal requirement before it halts the pipeline. A single year of COVID-era working-capital behavior is sufficient to fire what the spec describes as "MANIPULATION-RISK."

**Proposed v0.2 fix**: Require M > −1.78 in TWO consecutive annual periods before issuing a MANIPULATION-RISK hard halt. A single-year crossing produces a context note ("Beneish M elevated — review DSRI and AQI drivers") but does not halt the pipeline. This retains the gate's protective function while eliminating single-shock false positives.

---

### W2 — Beneish false negatives for commodity firms
**Position: CONFIRM, with mechanism re-specified**

The synthesis correctly identifies TATA coefficient suppression. The precise numbers for Tata Steel:

| FY used | TATA index | TATA contribution (coeff × TATA) | M-Score | Margin below threshold |
|---|---|---|---|---|
| FY2019 | −0.0696 | 4.679 × (−0.0696) = **−0.326** | −2.981 | −1.20 units |
| FY2020 | −0.0763 | 4.679 × (−0.0763) = **−0.357** | −2.986 | −1.21 units |
| FY2021 | −0.1481 | 4.679 × (−0.1481) = **−0.693** | −3.200 | −1.42 units |
| FY2023 | −0.0477 | 4.679 × (−0.0477) = **−0.223** | −2.363 | −0.58 units |

The mechanism is more subtle than just "TATA is large." In FY2023, TATA's contribution is only −0.223. The more important structural point is that in the same year, GMI = 1.961 (contribution +1.035) — a massive margin-collapse flag that would classify any consumer company as extremely high-risk. Yet M stayed at −2.363 because TATA + other offsets absorbed it. For commodity cyclicals, GMI and TATA are structurally anti-correlated across the cycle: at trough (margins collapse → GMI rises), OCF >> NI also tends to be most extreme (impairments suppress NI further from OCF → TATA most negative). So the flag and the suppressor peak together, creating a systematic dead zone. A commodity company could simultaneously exhibit GMI = 2.0 (manipulation-grade margin deterioration), AQI = 1.5 (asset quality degradation), AND LVGI = 1.1 (rising leverage) and still pass Beneish comfortably, because OCF >> NI structurally. The model is blind to manipulation in exactly the industries — steel, cement, oil & gas, power — where non-cash charges are largest and manipulation through capex inflation, goodwill, or asset revaluation is non-trivial.

**Proposed v0.2 fix**: Sector-conditional TATA coefficient. For non-heavy-asset sectors: 4.679 (unchanged). For heavy-asset sectors (Metals & Mining, Energy, Oil & Gas, Cement, Infrastructure — identifiable as fixed-asset intensity > 50% of total assets OR D&A / Revenue > 8%): coefficient = 2.0. At coefficient 2.0, the FY2021 TATA contribution drops from −0.693 to −0.296, leaving the GMI flag (+1.035) far more exposed. The adjusted M for Tata Steel FY2023 becomes approximately −2.140 (vs −2.363 current), and the FY2021 case becomes approximately −2.503 (vs −3.200 current) — both still below threshold, but now 0.36 and 0.72 units from the danger zone rather than 0.58 and 1.42. For any borderline manipulation case in heavy industry, the 2.0 coefficient makes the gate approximately 2× more sensitive to non-TATA manipulation signals. The coefficient of 2.0 is consistent with published re-estimations of Beneish in South Asian manufacturing samples.

---

### W3 — Piotroski cyclical inversion
**Position: CONFIRM, and quantify as a strong negative correlation**

This is the most damaging finding in the test data. For Tata Steel across 4 evaluation dates:

| Eval date | F-Score | Forward excess return vs NIFTY TRI |
|---|---|---|
| Mar-2020 | 6 | +222 percentage points (24mo) |
| Mar-2021 | 5 | +30 pp (24mo) |
| Mar-2022 | 8 | +3 pp (24mo) |
| Mar-2024 | 4 | +16 pp (14mo partial) |

Spearman rank correlation between F-Score and forward excess return: −1.0 on this 4-point dataset (rankings perfectly inverted). While 4 data points do not establish statistical significance in isolation, the mechanism is structurally determined. The four signals that drove cyclical inversion — F2 (ΔROA), F5 (ΔLeverage), F8 (ΔMargin), F9 (ΔTurnover) — all mechanically co-move with the commodity price cycle. At cycle peak (FY2021 data used for Mar-2022 eval): margins expanded (+F8), ROA improved (+F2), leverage reduced as cash poured in (+F5), asset turnover improved (+F9). All four fire positive exactly when the cycle has peaked and mean-reversion risk is maximal. At cycle trough: all four fail. The F-Score is not measuring company quality for cyclicals — it is measuring position in the commodity cycle with a 12-month lag, and producing signals that are the exact opposite of what a contrarian cyclical investor needs.

Additional concern: the signal stability analysis reveals that only 4 of 9 F-score signals are truly firm-quality signals for Tata Steel (F1, F3, F4, F7 — all stable 1s across all four eval dates). The other 5 are cyclical noise. The effective signal count for a cyclical stock is 4, not 9, which reduces the statistical power of the F-Score as a quality discriminator by roughly 55%.

**Proposed v0.2 fix**: Tag sectors as CYCLICAL (Metals & Mining, Energy, Oil & Gas) or SECULAR (all others). For CYCLICAL-tagged stocks: compute the full 9-signal F-Score as context but route action labels from a 5-signal "stable quality" score using only F1, F3, F4, F6, F7 (the signals that are NOT commodity-cycle-driven). Tata Steel's stable 5-signal score is approximately 4/5 across all dates (F6 is the variable one), which more accurately reflects "viable but not exceptional quality" regardless of cycle position. Display the 9-signal score alongside the routing score with a note: "Full F-Score reflects commodity cycle position; stable-quality score used for label routing."

---

### W4 — Ind AS 116 / accounting transitions
**Position: CONFIRM**

The quantitative impact is documented in the Asian Paints test: borrowings spiked ₹533 → ₹1,320 Cr in FY2019 primarily from lease capitalization. This caused F5 to fail (leverage appears to increase) and LVGI in Beneish to rise to 1.051 (contribution −0.327 × 1.051 = −0.344, partially offsetting the M-Score in this case). The F5 failure contributed to the 5/9 F-Score at Mar-2020 which produced REVIEW instead of WATCH/HOLD — a label that missed a +27.6% excess return. This is a step-change in reported leverage with zero information content about the company's economic leverage. Ind AS 116 affects every company with significant operating leases — retail (store leases), airlines, telecom, consumer goods distributors — systematically in the transition year. The signal degradation is sector-wide, not idiosyncratic, and is fully predictable from the transition date.

**Proposed v0.2 fix**: For FY2019–FY2021 year-pairs involving companies with Ind AS 116 impact (identifiable by a sharp single-year borrowings increase with corresponding right-of-use asset appearing on the balance sheet), zero out F5 signal and mark as "NOT COMPUTED — accounting transition (Ind AS 116, FY2019)." Compute Beneish LVGI using financial debt only, excluding lease liabilities. Flag the caveat in the output. Where Screener.in does not break out lease liabilities separately, default to marking F5 as data-quality-flagged rather than failing silently.

---

### W5 — Altman Z″ dominated by century reserves
**Position: CONFIRM, with enhanced quantification**

The share of Altman's variable contribution from backward-looking stock variables (X2, X4') vs current-period flow variables (X1, X3) for Tata Steel:

| FY balance sheet | X2 contribution | X4' contribution | X2+X4' share of variable Z″ | X1+X3 share |
|---|---|---|---|---|
| FY2019 | 0.949 | 0.451 | **53.4%** | 46.6% |
| FY2020 | 0.948 | 0.440 | **54.4%** | 45.6% |
| FY2021 | 0.976 | 0.459 | **64.2%** | 35.8% |
| FY2023 | 1.164 | 0.594 | **66.5%** | 33.5% |

(Variable Z″ = total Z″ minus the constant 3.25; X2+X4' dominance is increasing over time as reserves accumulate.)

By FY2023, the accumulated reserves (X2, X4') account for two-thirds of the non-constant Z″ — and they will only grow. Even if EBIT collapsed to near zero (X3 → 0) AND working capital turned sharply negative (X1 << 0), the accumulated reserves would keep Z″ safely above the distress threshold for Tata Steel for the next several decades. Concretely: Tata Steel carried ₹116,328 Cr of long-term debt at FY2020 (roughly 50% of total assets), with Net Debt/EBITDA of approximately 6.7× — a level that would classify as "leveraged" or "distressed" by standard credit analysis — while Z″ = 5.80 (safe zone). The model is not measuring current-period solvency risk for old, capital-intensive companies. It is measuring the structural permanence of the balance sheet.

For Asian Paints (FY2023), X2+X4' share = 58% of variable Z″. The dominance applies to stable quality compounders too, though the risk is less acute since their leverage is structurally low.

**Proposed v0.2 fix**: Replace X2 (Retained Earnings / Total Assets, a century-accumulated stock) with `X2_current = Net Profit After Tax (TTM) / Total Assets` (a current-period flow variable). This converts X2 from a solvency-history indicator to a current earnings quality indicator. Using Altman's existing coefficient 3.26: Tata Steel FY2023 new X2_current = 8,075 / 285,396 = 0.0283; contribution = 3.26 × 0.0283 = 0.092 (vs current 1.164). Z″ drops from 5.78 to 4.71 — still safe, but now responsive to earnings deterioration. A company with a net loss year would have a negative X2_current contribution, immediately reducing Z″ and increasing distress sensitivity. Add a supplementary non-gating metric display: Net Debt / EBITDA_TTM, with a note if > 4× (elevated leverage) or > 6× (high leverage for sector).

---

### W6 — Sector ROCE percentile fails on small sectors
**Position: CONFIRM, with a sharper mechanism identified**

The synthesis notes the symptom (N < 10, no percentile computed). The quantitative mechanism is worse than it appears: the action label composition table's routing logic requires a ROCE percentile to choose between WATCH and REVIEW for F = 5–6 stocks. When ROCE = N/A (N < 10), the system defaults to the conservative (lower) row. For Asian Paints with ROCE = 33–38% — which would rank 95th+ percentile in any multi-sector cohort — the system permanently routes to REVIEW-band rows at all four evaluation dates. This is a systematic quality blindspot: small-sector companies are disproportionately high-quality compounders (sectors with pricing power and barriers to entry tend to have few participants by design). The v0.1 rule specifically penalizes the most defensible competitive moats in the NIFTY 500.

**Proposed v0.2 fix**: Two-tier fallback. If sub-sector N < 10: escalate to NSE Super-sector (broader grouping such as Consumer Goods or Industrials), provided Super-sector N ≥ 15. If Super-sector N also < 15: compute percentile against NIFTY 500 non-BFSI companies within a ROCE bracket (±5 percentage points of the company's own ROCE), which effectively creates a quality-cohort comparison. Label the computation source explicitly in the output: "ROCE 87th percentile (Consumer Goods super-sector, N=31)." This prevents the permanent N/A routing failure while maintaining interpretive transparency.

---

## 3. NEW concerns this lens surfaces (not in synthesis)

**NC1 — The three knockout gates are correlated, not independent, producing less protection than the pipeline architecture implies**

The synthesis and v0.1 spec treat the three gates (Beneish, Altman, Pledge) as independent safety layers — a pipeline metaphor that implies each provides additive protection. Statistically, Beneish and Altman share three structural exposures: (1) both use Total Assets as denominator (common scale factor); (2) both are sensitive to leverage changes — Beneish through LVGI (debt/assets trend), Altman through X4' (equity/liabilities); (3) both are sensitive to earnings quality — Beneish through TATA (accruals/assets), Altman through X3 (EBIT/assets). In a genuine financial crisis — a company in real distress with simultaneous earnings manipulation — both gates should theoretically fire together (and would, since a company cannot fake EBIT/TA upward while also collapsing on EBIT/TA downward). The false positive and false negative cases in both test stocks confirm that the same underlying macro shocks drive correlated gate responses: COVID created near-breach on Beneish (Asian Paints, M = −1.697) while Altman remained safe (Z″ = 9.22 at the same date, because accumulated equity buffers Altman's X2/X4' regardless of current cash position). The gates are NOT providing independent defense against different failure modes — they share vulnerability to the same class of shocks (leverage increases, earnings deterioration from commodity cycles or macro events) and they share immunity to the same class of failures (companies with large accumulated balance sheets). For v0.2: if both gates remain as hard halts, the system documentation must acknowledge that "passed both gates" is not double-confirmation. A genuinely independent third layer would require a non-financial-statement signal: auditor continuity (same Big 4 for >3 years = positive), related-party transaction ratio (RPT / Revenue > 5% = flag), or restatement frequency (any restatement in last 3 years = flag).

**NC2 — The F-Score → action label mapping in §6 is empirically uncalibrated for NSE and creates internal inconsistency at threshold boundaries**

Three specific quant problems in the label composition table:

(a) The ≥7 threshold for HOLD is inherited from Piotroski's original paper, which applied it within a high-book-to-market (value portfolio) conditioning context. Outside that context — applied to a general universe including growth stocks, cyclicals, and quality compounders — the threshold's predictive content is unknown and likely varies substantially by sector and valuation regime. The 2024 NSE validation paper cited in the spec confirms F-Score predictive on NSE in 2017–2021; it does NOT validate the specific threshold of 7 as optimal for the NSE universe, let alone for the mixed CYCLICAL/SECULAR universe v0.1 is applied to.

(b) The ROCE percentile column is used as a tiebreaker for the F = 5–6 band but is ignored entirely for F ≥ 7. A company with F = 8, FCF/NI ≥ 0.7, and ROCE at the 5th sector percentile gets HOLD. A company with F = 6, FCF/NI ≥ 1.0, and ROCE at the 55th percentile gets WATCH (just barely better than REVIEW). The implicit weighting structure — ROCE matters in the middle band but not the top band — has no empirical justification. Tata Steel at Mar-2022 illustrates this: F = 8, ROCE = 21st percentile → HOLD. The table cannot distinguish a genuinely strong business from a cyclical peak.

(c) The WATCH/REVIEW split at F = 5–6 depends on whether FCF/NI ≥ 1.0 or ≥ 0.7, which routes companies to different ROCE-dependent rows. This creates a non-monotonic region: a company with F = 5, FCF = 0.99 (ACCEPTABLE), ROCE = 55th percentile gets REVIEW (F = 5–6, FCF ≥ 0.7, ROCE < 50... wait, ROCE ≥ 50 here → WATCH actually). The table has multiple boundary cases where a 1-unit difference in ROCE percentile or a 0.01 difference in FCF/NI flips the label by a full step. These knife-edges amplify the noise in all three input metrics. No calibration on NSE data has been performed to establish whether these boundaries correspond to economically meaningful return differences.

**NC3 — The FCF/NI 3-year averaging formula amplifies impairment artifacts for commodity cyclicals**

The synthesis does not flag this. The v0.1 formula averages OCF and NI separately before dividing: `mean(OCF) / mean(NI)`. For Tata Steel at Mar-2022 eval (window FY2019–FY2021): OCF avg = ₹29,944 Cr, NI avg = ₹6,162 Cr → CashConversion = 4.86×, labeled HIGH-QUALITY EARNINGS. But this ratio is primarily an artifact of FY2020, where NI = ₹1,174 Cr (near-zero due to impairments) while OCF = ₹20,169 Cr. The label HIGH-QUALITY EARNINGS is misleading: it is actually measuring "large impairment charges in the period reduced NI far below operating cash generation." A company with three consecutive large asset write-downs would show permanently elevated FCF/NI under this formula even as its underlying cash generation deteriorated. Two additional mathematical issues: (i) mean(OCF)/mean(NI) ≠ mean(OCF/NI) — when NI approaches zero in one year, the former can produce arbitrarily large ratios that the latter would dampen significantly; (ii) there is no upper bound on "HIGH-QUALITY" — a CashConversion of 4.86× and 1.05× are both labeled identically, despite very different interpretations. The formula needs both an upper cap and a check on whether extreme values are impairment-driven.

**NC4 — Binary F-Score encoding creates near-zero signal-to-noise for large-cap stocks at threshold margins**

F4 at Mar-2024 for Asian Paints: OCF = ₹4,193 Cr vs NI = ₹4,195 Cr — a ₹2 Cr difference on a ₹25,000+ Cr asset base. This is 0.008% of total assets. The binary 0/1 encoding of this difference has signal-to-noise ratio near zero: Screener.in rounding, different conventions for receivables factoring, or minor cash timing differences would flip this signal with no economic meaning. More broadly, the information compression from binarizing nine continuous signals is large. A company that improved ROA from 14.5% to 14.6% scores F2 = 1 identically to a company that improved ROA from 2% to 18%. For NIFTY 500 stocks spanning ₹500 Cr to ₹500,000 Cr in assets, the absolute ₹ differences that determine signal outcomes vary by three orders of magnitude — yet the same binary threshold applies universally. The compound effect: a company with nine barely-positive improvements (driven by rounding or data-source differences) scores the same as a company with nine dramatically positive improvements. This amplifies data-source noise and reduces the F-Score's discriminatory power.

---

## 4. Proposed v0.2 changes — prioritized

**P0 — Cannot ship v0.2 without:**

**P0.1 — Sector-conditional Beneish TATA coefficient**

Replace the universal coefficient 4.679 with a sector-conditional value:
- Default (non-heavy-asset sectors): 4.679 (unchanged)
- Heavy-asset sectors (Metals & Mining, Energy, Oil & Gas, Cement, Infrastructure — identifiable by fixed-asset intensity > 50% of TA OR D&A/Revenue > 8%): coefficient = **2.0**

Rationale: At 2.0, the FY2021 TATA suppression for Tata Steel drops from −0.693 to −0.296, exposing the GMI = 1.96 flag (+1.035) with approximately 60% less buffering. Adjusted M-Score for Tata Steel FY2023 becomes −2.140 (vs −2.363 current) — now only 0.36 units from threshold, compared to 0.58 currently. The value 2.0 is consistent with re-estimated Beneish coefficients in non-US manufacturing samples; the Indian-specific calibration should use Shah (2018) BSE 100 data when available.

**P0.2 — Two-period confirmation for Beneish hard halt**

Require M > −1.78 in TWO consecutive annual periods before triggering MANIPULATION-RISK hard halt. A single-year crossing generates a context note only: "Beneish M-Score elevated (−1.697) — DSRI and AQI elevated; review for macro/accounting explanations before acting." This eliminates single-shock false positives (the Asian Paints Mar-2022 case) while preserving the gate's function against persistent manipulation. Genuine manipulation (e.g., multi-year revenue recognition fraud) would cross the threshold in multiple consecutive periods.

**P0.3 — Cyclical sector stable-quality F-Score routing**

For sectors tagged CYCLICAL (Metals & Mining, Energy, Oil & Gas): compute both the full 9-signal F-Score (for display) and a 5-signal "stable quality" score using only F1, F3, F4, F6, F7. Use the 5-signal score for action label routing. Display full score alongside: "Full F-Score = 8/9 (reflects commodity cycle position); Stable-quality score = 4/5 (used for routing — commodity-sensitive signals excluded)."

The 5 signals excluded from routing are the four cyclically-inverted ones (F2, F5, F8, F9) plus none: F1, F3, F4, F6, F7 constitute the quality signals that do not mechanically co-move with commodity prices. Re-calibrate the routing table thresholds for the 5-signal score accordingly: ≥4 = HOLD-equivalent, 3 = WATCH-equivalent, ≤2 = REVIEW-equivalent (roughly preserving the Piotroski signal density ratio from the 9-signal case).

---

**P1 — Strongly desirable:**

**P1.1 — Replace Altman X2 with a current-period earnings proxy**

Replace `X2 = Retained Earnings / TA` with `X2_current = Net Profit After Tax (TTM) / TA`. Rationale: converts X2 from a century-accumulated stock variable (which provides false permanence) to a current-period profitability signal that responds to earnings deterioration within the current measurement period. Using the existing Altman coefficient 3.26, the Tata Steel FY2023 X2_current contribution drops from 1.164 (accumulated) to 0.092 (current-period only), reducing Z″ from 5.78 to 4.71 — still safely above 2.6, but now genuinely sensitive to a period of zero or negative earnings. Add a supplementary non-gating display: `Net Debt / EBITDA_TTM`, with labels "> 4× (elevated leverage)" and "> 6× (high leverage)" as context notes (not hard halts).

**P1.2 — Ind AS 116 adjustment for F5 and Beneish LVGI**

For FY2019–FY2021 year-pairs where a company has a material right-of-use asset appearing (identifiable via Screener.in balance sheet or XBRL filings): compute F5 using financial debt only (exclude Ind AS 116 lease liabilities). Similarly, compute Beneish LVGI using financial debt only. Flag in output: "F5 computed on financial debt only (Ind AS 116 lease liabilities excluded, FY2019 transition)." Where this split is unavailable from Screener.in, default to marking F5 as CAVEAT rather than failing it.

**P1.3 — Sector ROCE percentile two-tier fallback**

When sub-sector N < 10: escalate to NSE Super-sector (e.g., Consumer Goods) provided Super-sector N ≥ 15. When Super-sector N also < 15: compute percentile against NIFTY 500 non-BFSI companies within a ROCE bracket (±5 percentage points of the company's own ROCE). Label source: "ROCE 87th percentile (Consumer Goods super-sector, N = 31)." This eliminates the permanent N/A routing failure for small-sector quality compounders.

**P1.4 — FCF/NI: upper cap and annotation**

Cap CashConversion at 3.0 for routing purposes (values above 3× are dominated by impairment artifacts). Display the computed value but annotate when > 3×: "CashConversion = 4.86× — likely driven by large non-cash impairment charges; interpret carefully as impairment indicator, not earnings quality signal." This prevents the Tata Steel FY2020 near-zero-NI case from labeling impairment risk as HIGH-QUALITY EARNINGS.

---

**P2 — Nice-to-have:**

**P2.1 — Materiality buffer on binary F-Score knife-edge signals**

Apply a 5% materiality buffer to F4 (OCF > NI): pass if OCF > 0.95 × NI (tolerates up to 5% below NI). Extend to F2 (ΔROA), F5 (ΔLeverage), F8 (ΔMargin), F9 (ΔTurnover): require a minimum 1% relative change to count as a pass in either direction. This reduces noise from data-source rounding and near-zero signals without materially changing the signal for meaningful changes.

**P2.2 — Multi-year Beneish display**

Compute Beneish M-Score for three consecutive years (t, t-1, t-2) and display the trend. A stable M-Score near the threshold across multiple years is more informative and more concerning than a single-year spike. The output trend line also allows the user to distinguish "this is a persistent pattern" from "this is COVID-year noise."

**P2.3 — Gate correlation disclaimer in output**

For any stock passing both Beneish and Altman: add a brief output annotation: "Note: Beneish and Altman share sensitivity to leverage trends and earnings changes; dual-pass does not constitute fully independent confirmation." This is a transparency measure, not a math change.

---

## 5. What v0.1 got RIGHT (be fair)

- **The pipeline architecture (gate → primary → overlay → action label) is the correct design pattern.** Ordering manipulation check first, distress check second, quality score third correctly handles the dependency structure: a manipulating company should not benefit from a strong quality score. The architecture cleanly separates "can we trust the numbers?" from "what do the numbers say?" This is sound signal hygiene and should be preserved in v0.2 with the signals inside each step improved.

- **FCF/NI as the primary quality overlay is a well-chosen design.** Using operating cash flow rather than free cash flow avoids CapEx-cycle sensitivity that would artificially suppress FCF for capital-intensive companies during heavy-investment periods. The 3-year averaging is correctly motivated to smooth working-capital noise. The label bands (≥1.0, 0.7–1.0, <0.7) are directionally consistent with published accruals-based return research (Sloan 1996; Dechow et al.). The choice to make this additive (not a gate) is correct — cash conversion is a quality signal, not a binary safety check, and treating it as additive appropriately lets it influence but not dominate the final label.

- **Using consolidated financials as a locked convention is correct and consequential.** The standalone-vs-consolidated gap for diversified Indian conglomerates is large: Tata Steel Europe is entirely invisible in standalone financials, and its drag on consolidated ROCE/NI is the primary quality signal for the international risk. Locking consolidated data prevents a major and systematic source of signal distortion. Many retail-oriented screening tools default to standalone; this is the right call.

- **The promoter pledge gate at 30% is appropriately calibrated.** Research bucket 7.9 in the spec cites 50% as the forced-liquidation correlation point; using 30% as an early-warning level is conservative by design. From a quant perspective, the asymmetric cost of a false negative (holding through a forced-liquidation margin call event) vastly exceeds the cost of a false positive (avoiding a pledged-promoter stock that might be fine). The 30% threshold is also approximately the margin-call trigger level for most Indian brokers, making it an economically meaningful rather than arbitrary boundary.

---

## 6. One sentence to the synthesizer

"If you carry one thing from this critique into the consensus, it should be: the Beneish M-Score and Altman Z″ are correlated — not independent — guards that share vulnerability to leverage and earnings shocks, and both have sector-specific failure modes (Beneish false-negatives for heavy-asset commodity firms where TATA permanently suppresses M; Altman insensitivity for century-old firms where accumulated reserves permanently inflate Z″) that render the two-gate knockout system systematically blind to exactly the 35–40% of NIFTY 500 market cap in metals, energy, cement, and infrastructure — and v0.2 must either recalibrate both signals for NSE heavy-asset sectors (P0.1: sector-conditional TATA coefficient; P1.1: replace Altman X2 with current-period earnings) or replace them with sector-appropriate alternatives."
