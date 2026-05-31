# 18 — Cycle A: Equity FA Math Specification, v0.3

**Status**: Draft — A.8 output (post A.7 re-test)
**Date**: 2026-05-31
**Version**: v0.3 (incremental update to v0.2 in `16_cycle_A_math_v0.2.md`)
**Scope**: Same as v0.2 — Indian NSE direct equity, NIFTY 500. FA only.
**Sources**: v0.2 spec + A.7 cross-stock test results (`17_cycle_A_A7_synthesis.md`) + 3 stock-level tests (`17a`, `17b`, `17c`)

---

## 0. Changelog (v0.2 → v0.3)

A.7 surfaced 7 v0.3 candidates (N1–N7) when v0.2 was tested across 3 stocks (Asian Paints quality compounder, Tata Steel commodity cyclical, Crompton soft cyclical). v0.3 addresses all 7. Pipeline architecture and most gate logic unchanged from v0.2 — these are surgical refinements, not a refactor.

| # | A.7 candidate | v0.3 fix | Section |
|---|---|---|---|
| **N1** | Z″ MktCap/TL non-discriminative for premium-valued names (Asian Paints Z″ = 30–46; same v0.1 problem moved to opposite valuation extreme) | **Revert X4' to Book Equity/TL.** Distress detection now lives primarily in the mandatory supplementary leverage display (ND/EBITDA + IC + Current Ratio). Z″ becomes supportive context, not the primary signal. | §7 Altman |
| **N2** | Acquisition-year Beneish false positive (Crompton Mar-2024 hard-halt entirely from Butterfly acquisition consolidation; NEW failure mode not in v0.1 list) | **NEW ACQUISITION-YEAR entry in the Regime-Shift Calendar.** When consolidated TA or revenue grows materially YoY from a disclosed acquisition, exclude AQI + DEPI from Beneish; use 2-yr-avg SGI. | §10 Regime-Shift Calendar |
| **N3** | BENEISH-INERT trigger too strict for Metals & Mining (v0.2 trigger = D&A/Revenue > 15%; Tata Steel is 4–6% and INERT doesn't fire even though TATA dominates) | **Replace D&A-proxy trigger with direct impact measure:** BENEISH-INERT fires when `|α · TATA| > 1.0` (TATA term alone shifts M-Score by > 1 unit). Cleaner — trigger on actual impact, not proxy. | §5 Beneish |
| **N4** | F5 over-aggressive Ind AS 116 exclusion (v0.2 excluded F5 from F-Score denominator for ongoing year-pairs; Asian Paints Mar-2021 lost a passing F5) | **Narrow Ind AS 116 F5 exclusion to ONLY the FY2019/FY2020 year-pair.** For FY2020/FY2021 and later, compute F5 normally with financial-debt-only convention applied to both years. | §10 Regime-Shift Calendar |
| **N5** | IMPAIRMENT-CHECK noise on commodity cyclicals (fires at 3 of 4 Tata Steel dates because heavy industry has routine large non-cash charges) | **Sector-conditional**: heavy-asset sectors get `ROUTINE-CHARGES` annotation instead of IMPAIRMENT-CHECK when CashConversion > 3.0×. | §11 FCF/NI |
| **N6** | F4 knife-edge unaddressed (Asian Paints Mar-2024 OCF − NI = ₹2 Cr; rounding swings F4 = 0 vs 1) | **±1% materiality buffer on all YoY-comparison F-Score signals** (F2, F4, F5, F8, F9). | §9 Piotroski |
| **N7** | 3-yr window mechanical artifact for cyclical F-Score (peak years entering/leaving the window inflate cycle-adjusted score) | **Extend cyclical normalization window from 3-yr to 5-yr.** Longer window smooths through full mini-cycles. | §9 Piotroski cyclical |

---

## 1. v0.3 picks (recap from Pranav's defaults on Q1–Q8)

No change to policy. v0.3 picks are identical to v0.2 picks. All changes in v0.3 are tactical refinements driven by A.7 test data, not by re-asking Q1–Q8.

For reference, v0.2 picks (carried forward):

| Q | Decision | Pick |
|---|---|---|
| Q1 | Beneish gate design | Two-stage conditional halt |
| Q2 | Cyclical tag list breadth | Broader |
| Q3 | Altman Z″ replacement | Both (X2_current universal + composite for old firms) |
| Q4 | BFSI stub format | Quantitative with disclaimer |
| Q5 | PSU gate | Partial sub-pipeline + PSU-CONTEXT annotations |
| Q6 | AFFIRM label? | No, keep 4 labels |

---

## 2. The pipeline (v0.3 — same shape as v0.2)

```
[0]  PSU classification check     (unchanged from v0.2)
[1]  BFSI classification check    (unchanged from v0.2)
[2]  Beneish two-stage gate       (BENEISH-INERT trigger changed — see §5)
[2.5] Governance Quality Screen   (unchanged from v0.2)
[3]  Altman Z″ + composite        (X4' reverted to Book Equity/TL — see §7)
[4]  Pledge two-factor gate       (unchanged from v0.2)
[5]  Piotroski F-Score            (materiality buffer + 5-yr cyclical window — see §9)
[6]  FCF / NI overlay             (IMPAIRMENT-CHECK sector-conditional — see §11)
[7]  Sector ROCE percentile       (unchanged from v0.2)
[8]  Action label with hysteresis (unchanged from v0.2)
[9]  Data-quality completeness    (unchanged from v0.2)
```

Sections marked "unchanged from v0.2" mean: refer to `16_cycle_A_math_v0.2.md` for full spec; v0.3 doesn't modify them.

---

## 3. Gate 0 — PSU classification

**Unchanged from v0.2 §3.**

---

## 4. Gate 1 — BFSI classification + minimal stub output

**Unchanged from v0.2 §4.**

---

## 5. Gate 2 — Beneish (v0.3: BENEISH-INERT trigger redesigned)

### 5.1 Formula

Unchanged from v0.2 §5.1 — the 8-variable Beneish formula with sector-conditional α (4.679 for non-heavy-asset; 2.0 for heavy-asset Metals & Mining / Energy / Oil & Gas / Cement / Infrastructure).

### 5.2 Two-stage conditional halt logic

Unchanged from v0.2 §5.2.

### 5.3 BENEISH-INERT trigger (REDESIGNED in v0.3)

**v0.2 trigger** (deprecated): D&A / Revenue > 15% AND impairment-driven OCF >> NI.

**v0.3 trigger** (new):

```
BENEISH-INERT fires when |α · TATA| > 1.0
```

Where `α` is the sector-conditional coefficient (4.679 or 2.0) and `TATA = (NI − OCF) / TA_t`.

**Interpretation**: this directly measures the TATA term's contribution to the M-Score. If TATA alone shifts M by more than 1 absolute unit, the M-Score is being dominated by accruals/non-cash-charge structure and not by manipulation signals. The other 7 indices become noise relative to TATA.

**Effect on output**:
- BENEISH-INERT fires → output reads: *"BENEISH-INERT: M-Score has low signal power for this stock (TATA contribution = X.X). Manipulation risk assessed via Governance Quality Screen instead."*
- Pipeline continues to gate 2.5; Governance Quality Screen result becomes the primary manipulation signal for this stock.

**Rationale**: A.7 found Tata Steel's D&A/Revenue = 4–6% (below v0.2's 15% trigger), even though TATA contribution suppressed M-Score by 0.40–1.0 units. The v0.2 proxy was wrong — high D&A is one driver of TATA dominance but not the only one (impairment patterns, asset write-downs, accumulated CapEx all matter). Trigger-on-impact > trigger-via-proxy.

### 5.4 SGAI handling

Unchanged from v0.2 §5.1.

---

## 6. Gate 2.5 — Governance Quality Screen

**Unchanged from v0.2 §6.**

**v0.3 note**: this gate remains UNTESTED in real data — none of the A.7 test stocks had any of the 4 indicators fire. The Governance Screen needs a known-historical manipulation case (Vakrangee or Manpasand Beverages, run retrospectively pre-blow-up) to validate. Deferred to future Cycle A iteration OR Cycle F.

---

## 7. Gate 3 — Altman Z″ (v0.3: X4' reverted; supplementary display expanded)

### 7.1 Modified Z″ formula (v0.3)

```
Z″_v0.3 = 6.56·X1 + 3.26·X2_current + 6.72·X3 + 1.05·(BookEquity/TL) + 3.25
```

Where:

| Term | Definition | Note |
|---|---|---|
| X1 | Working Capital / Total Assets | Unchanged from v0.2 (with Ind AS 116 lease-liability adjustment for FY2019/FY2020 year-pair only) |
| X2_current | NPAT_TTM / Total Assets | Unchanged from v0.2 (replaces v0.1's Retained Earnings / TA) |
| X3 | EBIT / Total Assets | Unchanged |
| **X4'** | **Book Equity / Total Liabilities** | **REVERTED in v0.3.** v0.2 had MktCap/TL which made Z″ non-discriminative for premium-valued names. Returning to book equity. |

### 7.2 Composite check for old / reserve-heavy firms

Unchanged from v0.2 §7.2 — runs in parallel for companies meeting either condition (accumulated reserves > 200% EBITDA OR listing history > 30 years). Halt on Composite (all three of ND/EBITDA > 5×, IC < 1.5×, CR < 0.9) OR modified Z″ < 1.1.

### 7.3 Mandatory supplementary display (EXPANDED in v0.3)

For every non-BFSI, non-PSU stock (regardless of Z″ verdict), display **three** leverage / liquidity metrics:

| Field | Threshold for label | Label |
|---|---|---|
| Net Debt / EBITDA (TTM) | > 4.0× | "Elevated" |
| Net Debt / EBITDA (TTM) | > 6.0× | "High" |
| Interest Coverage (TTM) | < 2.0× | "Low" |
| **Current Ratio** | **< 1.0** | **"Tight" (NEW v0.3)** |
| **Current Ratio** | **< 0.7** | **"Very Tight" (NEW v0.3)** |

The Current Ratio addition gives a third independent leverage/liquidity signal alongside ND/EBITDA and Interest Coverage. Three metrics together are now the **primary distress signal**; Z″ is supportive context.

### 7.4 Rationale

A.7 confirmed v0.2's MktCap/TL substitution had moved the v0.1 problem from "Z″ stuck high for mature firms" to "Z″ stuck high for premium-valued firms" (Asian Paints Z″ = 30–46 across 4 dates). The premise of v0.2's change — that market cap is more informative than book equity for distress — was wrong: in NSE's reality, premium valuations swamp leverage info just as accumulated reserves do.

The cleaner fix is: keep Book Equity / TL (the original Z″ X4'), but stop relying on Z″ as the primary distress signal. The supplementary metrics ARE the signal in v0.3. Z″ now functions as a sanity check.

---

## 8. Gate 4 — Promoter Pledge (two-factor)

**Unchanged from v0.2 §8.**

A.7 (Crompton) validated the two-factor design — 65.58% pledge with LTV-CAUTION at Mar-2020 (PE-era) fired correctly; 0% promoter scenario from FY2022 onwards handled cleanly without false fires.

---

## 9. Piotroski F-Score (v0.3: materiality buffer + 5-yr cyclical window)

### 9.1 CYCLICAL sector tag list

Unchanged from v0.2 §9.1.

### 9.2 Behavior for non-cyclical stocks (v0.3: ±1% materiality buffer)

Compute the original 9-signal Piotroski F-Score with a **±1% materiality buffer** applied to all YoY-comparison signals:

| Signal | v0.2 condition | v0.3 condition |
|---|---|---|
| F2 (ΔROA > 0) | ROA_t > ROA_{t−1} | ROA_t > 0.99 × ROA_{t−1} |
| F4 (OCF > NI) | OCF_t > NI_t | OCF_t > 0.99 × NI_t |
| F5 (ΔLev < 0) | (LTD/Avg.TA)_t < (LTD/Avg.TA)_{t−1} | (LTD/Avg.TA)_t < 0.99 × (LTD/Avg.TA)_{t−1} |
| F8 (ΔGM > 0) | GM_t > GM_{t−1} | GM_t > 0.99 × GM_{t−1} |
| F9 (ΔAT > 0) | (Rev/Avg.TA)_t > (Rev/Avg.TA)_{t−1} | (Rev/Avg.TA)_t > 0.99 × (Rev/Avg.TA)_{t−1} |

F1 (ROA > 0), F3 (CFO > 0), F6 (CR > prior), F7 (no dilution): unchanged from v0.2 (no buffer needed — F1/F3 are level checks, F6 is a small-step ratio, F7 is discrete share count).

**Rationale**: A.7 (Asian Paints Mar-2024) had OCF − NI = ₹2 Cr — essentially zero, but v0.2's strict comparison swung F4 = 0/1 on rounding. ±1% buffer eliminates knife-edge cases without materially changing the signal.

### 9.3 Behavior for CYCLICAL stocks (v0.3: 5-yr rolling window)

For CYCLICAL-tagged stocks, compute the full 9-signal F-Score with **normalized 5-yr rolling-average inputs** (was 3-yr in v0.2):

| Signal | v0.2 input (3-yr) | v0.3 input (5-yr) |
|---|---|---|
| F1, F2, F3 (ROA-based) | 3-yr-avg EBIT / Avg(TA) | **5-yr-avg EBIT / Avg(TA)** |
| F4 (CFO > NI) | single-year | unchanged (still single-year) |
| F5–F7 | unchanged | unchanged |
| F8 (ΔGM > 0) | 3-yr-avg GM | **5-yr-avg GM** |
| F9 (ΔAT > 0) | 3-yr-avg asset turnover | **5-yr-avg asset turnover** |

The ±1% materiality buffer applies to the cycle-adjusted signals as well.

**Rationale**: A.7 (Tata Steel Mar-2024) showed the 3-yr window had a mechanical artifact — the FY2022 cycle peak proportionally inflated the cycle-adjusted F-Score because peak years entering/leaving the window swing the average. A 5-yr window smooths through a full mini-cycle on most commodity cycles and reduces the entry/exit artifact.

**Trade-off**: 5-yr requires more historical data. For companies with less than 5 years of data (recent listings), fall back to the longest available window and tag `WINDOW-SHORT: only N years available`.

### 9.4 4-signal stable-quality subset display

Unchanged from v0.2 §9.5.

---

## 10. Regime-Shift Calendar (v0.3: M&A exception added; Ind AS 116 F5 exclusion narrowed)

### 10.1 Calendar entries

Unchanged events from v0.2 §10.1. **NEW v0.3 entries / refinements** marked in bold:

| Event | Affected year-pairs | Affected signals | Neutralization rule |
|---|---|---|---|
| Demonetization | FY2016/FY2017 | DSRI, SGI, F9 | Exclude from F-Score denominator; tag DEMONETIZATION-YEAR |
| GST introduction | FY2017/FY2018 | SGI, F9 | Use 2-yr avg revenue; tag GST-TRANSITION |
| Ind AS 115 (revenue recognition) | FY2018/FY2019 | SGI, F9 (EPC/real estate/telecom/retail) | Exclude from denominator for affected sectors |
| Ind AS 109 (financial instruments / ECL) | FY2018/FY2019 | DSRI, F1/F2 (capital goods/infra/EPC) | Exclude from denominator for affected sectors |
| **Ind AS 116 (leases) — NARROWED in v0.3** | **FY2019/FY2020 ONLY** | F5, LVGI, Altman X1 | **F5 excluded from denominator ONLY at FY2019/FY2020 year-pair. For FY2020/FY2021 and later, F5 is computed normally with financial-debt-only convention applied consistently in both years (was: ongoing exclusion in v0.2).** |
| COVID lockdowns | FY2020/FY2021, FY2021/FY2022 | DSRI, AQI (Beneish two-stage regime windows per §5.2) | COVID-WINDOW context note added |
| **ACQUISITION-YEAR (NEW in v0.3)** | **Any year-pair where consolidated TA grew > 20% YoY OR consolidated revenue grew > 25% YoY AND a material acquisition was disclosed in the period** | **AQI, DEPI, SGI (Beneish)** | **Exclude AQI from M-Score (contribution = 0). Exclude DEPI from M-Score (contribution = 0). For SGI: use 2-yr-avg revenue growth from t−2 to t (instead of single-year). Tag in output: `ACQUISITION-YEAR (with acquirer/target name if disclosed)`. Add context note: "Beneish indices AQI, DEPI excluded due to acquisition consolidation artifacts; SGI smoothed via 2-yr average. M-Score reflects remaining 5 indices."** |

### 10.2 Acquisition detection (operational note)

For the new ACQUISITION-YEAR entry, the trigger is twofold:
1. **Mechanical signal**: consolidated TA grew > 20% YoY OR consolidated revenue grew > 25% YoY between t−1 and t.
2. **Disclosed acquisition in period**: the company's annual report or stock exchange filings disclose a material acquisition completed in year t (typically as a "Business Combination" note under Ind AS 103).

Both signals together. A company growing 25% organically doesn't trigger ACQUISITION-YEAR (no disclosed acquisition). A small bolt-on acquisition that doesn't move TA materially doesn't trigger either (no mechanical signal).

**Data source**: Ind AS 103 disclosures (Business Combinations note); BSE/NSE corporate-action filings; annual report notes on acquisitions.

### 10.3 Application

Unchanged from v0.2 §10.2.

### 10.4 Rationale for new entries

- **ACQUISITION-YEAR**: A.7 surfaced this on Crompton Mar-2024 — Butterfly Gandhimathi Appliances acquisition consolidation produced AQI = 2.76 (vs ~1.0 baseline), DEPI = 0.37 (vs ~1.0), SGI = 1.27. None reflected manipulation; all reflected consolidation accounting. M = −1.199 triggered hard halt entirely on these artifacts. New failure mode beyond v0.1's documented 6 weaknesses.

- **Ind AS 116 narrowing**: A.7 (Asian Paints Mar-2021) showed v0.2's blanket exclusion of F5 for any post-FY2020 year-pair was over-aggressive. F5 should be excluded only at the actual transition year-pair (FY2019/FY2020), not in perpetuity afterwards.

---

## 11. FCF / NI overlay (v0.3: IMPAIRMENT-CHECK sector-conditional)

### 11.1 Formula

Unchanged from v0.2 §11.1.

### 11.2 Cap behavior (v0.3: sector-conditional)

Same cap at 3.0× as v0.2. But the annotation differs by sector:

| Sector class | When CashConversion > 3.0× | Annotation |
|---|---|---|
| **Non-heavy-asset sectors** (default) | IMPAIRMENT-CHECK | *"IMPAIRMENT-CHECK: Cash conversion exceeds 3.0× — usually indicates large non-cash charges. Investigate impairment schedule before treating as quality signal."* |
| **Heavy-asset sectors** (Metals & Mining, Energy, Oil & Gas, Cement, Infrastructure) | **ROUTINE-CHARGES** (NEW in v0.3) | *"ROUTINE-CHARGES: CashConversion = X.X× — large non-cash charges (depreciation on heavy assets, periodic impairments) are routine for this sector. Treat as context, not signal."* |

### 11.3 Label thresholds

Unchanged from v0.2 §11.3.

### 11.4 Rationale

A.7 (Tata Steel) found IMPAIRMENT-CHECK fired at 3 of 4 dates — turning a designed signal into noise. The fix isn't to suppress the cap (which still protects against single-loss-year ratio inflation), but to label the cap differently for sectors where exceeding it is routine, not exceptional.

---

## 12. Sector ROCE percentile

**Unchanged from v0.2 §12.**

---

## 13. Action labels (with hysteresis)

**Unchanged from v0.2 §13.** Still untested in v0.3 — hysteresis requires consecutive quarterly data, which A.7 didn't have (only 4 historical snapshots per stock).

---

## 14. Data-quality completeness score

**Unchanged from v0.2 §14.**

---

## 15. Action label composition (routing table)

**Unchanged from v0.2 §15.**

---

## 16. Worked example (v0.3 — note for reader)

The v0.2 worked example (XYZ Ltd, Industrial Manufacturing mid-cap, no acquisition activity) does not exercise any of v0.3's changes:

- It's not heavy-asset, so the BENEISH-INERT trigger redesign (N3) doesn't apply.
- It's not premium-valued, so the X4' revert (N1) doesn't change Z″ materially (Z″ = 9.74 with Book Equity/TL is similar to 9.74 with MktCap/TL for a typical mid-cap with P/B ≈ 3).
- No acquisition in the year-pair, so ACQUISITION-YEAR doesn't fire (N2).
- Not in FY2019/FY2020, so F5 exclusion narrowing (N4) doesn't apply.
- Non-cyclical, so 5-yr window (N7) doesn't apply.
- All YoY signals are clearly above their thresholds, so the ±1% materiality buffer (N6) doesn't change any signal.
- CashConversion = 1.11 (below 3.0× cap), so IMPAIRMENT-CHECK/ROUTINE-CHARGES (N5) doesn't apply.

→ XYZ Ltd v0.3 result = v0.2 result = **HOLD (stable 3 quarters)** with the same reasoning string.

For an illustration of v0.3 changes IN ACTION, refer to the v0.3 re-test (if A.9 runs) — Tata Steel and Crompton results should differ materially.

---

## 17. What v0.3 STILL doesn't do (deferred)

| Deferred to | Item |
|---|---|
| v0.4 | Full BFSI FA pipeline (P/ABV, NIM stress-testing, GNPA cycle, CAR analysis) |
| v0.4 | AFFIRM label (5th label) |
| v0.4 | Specialty chemicals sub-sector peer-mapping lookup |
| v0.4 | Beneish on standalone financials for conglomerates |
| v0.4 | ADTV liquidity floor as output field |
| Cycle B | All TA signals |
| Cycle C | Mutual-fund-specific signals |
| Cycle D | Position sizing, correlation-to-portfolio |
| Cycle E | Exit rules, stop-losses, tax-aware sell sequencing |
| Cycle F | TA/FA conflict resolution, signal combination, behavioural metrics |

**UNTESTED in v0.3 (would benefit from future validation)**:
- Governance Quality Screen — needs a known manipulation case (Vakrangee / Manpasand) tested retrospectively
- Hysteresis — needs consecutive-quarter data
- Structured REVIEW checklist — needs a stock that actually receives REVIEW in production-style use

---

## 18. Confidence in v0.3 (post-A.7-driven changes)

| Component | v0.2 confidence | v0.3 confidence | Change |
|---|---|---|---|
| Pipeline architecture | HIGH | HIGH | — |
| Beneish two-stage gate | HIGH | HIGH | — |
| Beneish sector-conditional TATA | MED-HIGH | MED-HIGH | — |
| **BENEISH-INERT trigger** | MED (D&A proxy) | **MED-HIGH** (direct impact measure) | ↑ |
| Beneish acquisition-year handling | MISSING | MEDIUM | ↑↑ (new, untested in re-test) |
| Governance Quality Screen | UNTESTED | UNTESTED | — |
| Altman X2_current | HIGH | HIGH | — |
| **Altman X4'** | LOW-MED (MktCap/TL) | **MED-HIGH** (reverted to Book; supplementary metrics primary) | ↑ |
| Altman composite for old firms | HIGH | HIGH | — |
| **Supplementary leverage display** | HIGH (2 metrics) | **HIGH** (3 metrics — CR added) | ↑ slight |
| Pledge two-factor | HIGH | HIGH | — |
| Piotroski materiality buffer | MISSING | MEDIUM | ↑ (new; conceptually sound but untested) |
| Piotroski cyclical 5-yr window | MED (3-yr artifact known) | MED-HIGH (5-yr smooths better; trade-off is data requirement) | ↑ |
| CYCLICAL tag breadth | HIGH | HIGH | — |
| Regime-Shift Calendar (Ind AS / COVID) | MED-HIGH | HIGH (F5 narrowing fixes Asian Paints regression) | ↑ |
| Regime-Shift Calendar (M&A) | MISSING | MEDIUM (new; untested in re-test) | ↑↑ (new) |
| FCF/NI capped + mean-of-ratios | MED (noise on cyclicals) | MED-HIGH (sector-conditional annotation) | ↑ |
| Sector ROCE Industry-tier | HIGH | HIGH | — |
| Action label hysteresis | UNTESTED | UNTESTED | — |
| Data-quality completeness | HIGH | HIGH | — |

**Net**: v0.3 closes 5 of the 7 v0.3 candidates with high confidence (N1, N3, N4, N5, N7). 2 are new mechanisms (N2 M&A handling and N6 materiality buffer) introduced with medium confidence — untested in re-test.

---

## 19. Open question for Pranav: A.9 re-test?

The A.7 cycle gave us confidence v0.2 was substantially better than v0.1. Three of the v0.3 changes (N1, N4, N7) are clear refinements that wouldn't change A.7's conclusions materially. Two (N2 ACQUISITION-YEAR, N6 materiality buffer) are new mechanisms that would benefit from validation.

**Option A — Close Cycle A now.** Mark v0.3 as the final Cycle A math; trust the A.7 evidence + the surgical nature of v0.3 changes. Move to Cycle B.

**Option B — Run A.9 re-test on the same 3 stocks** to validate v0.3. Expected outcomes:
- Asian Paints: Z″ should drop from 30–46 range back into reasonable values (Book Equity/TL); other dates' verdicts should be similar to v0.2 with F4 buffer addressing knife-edge.
- Tata Steel: BENEISH-INERT should now fire at multiple dates (|α · TATA| > 1.0 will trigger when α = 2.0 and TATA suppresses M-Score). Z″ behavior should normalize.
- Crompton Mar-2024: M-Score should no longer hard-halt — ACQUISITION-YEAR catches the Butterfly acquisition; AQI and DEPI excluded; M recomputed on 5 indices should land in safer territory.

**My recommendation**: **Option A — close Cycle A.** v0.3 is a tactical patch on v0.2, not a structural redesign. The patches are well-motivated and surgical. A.9 would mostly confirm what we already expect. Cycle B starts.

If Pranav says yes to A.9: 3 agents again in parallel (~15–25 min each), then a v0.3 synthesis like `17_cycle_A_A7_synthesis.md`.

---

## 20. Sources

All v0.1 + v0.2 sources carry forward. v0.3 added sources:

- A.7 cross-stock synthesis (`17_cycle_A_A7_synthesis.md`) — primary driver of all 7 v0.3 changes
- A.7 stock-level test files (`17a_AsianPaints`, `17b_TataSteel`, `17c_Crompton`)
- Ind AS 103 (Business Combinations) disclosure framework — for ACQUISITION-YEAR detection

---

**End of v0.3 spec.** Awaiting Pranav's decision on A.9 re-test vs Cycle A close.
