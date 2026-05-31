# 16 — Cycle A: Equity FA Math Specification, v0.2

**Status**: Draft — A.6 output (post A.5 multi-agent critique)
**Date**: 2026-05-31
**Version**: v0.2 (replaces v0.1 in `11_cycle_A_math_v0.1.md`)
**Scope**: Indian NSE direct equity, NIFTY 500 universe. FA only (TA → Cycle B; MF → Cycle C).
**Sources**: v0.1 spec + A.5 synthesizer brief (`15_cycle_A_critiques_v0.1.md` §6) + Pranav's confirmed defaults for Q1–Q8.

---

## 0. Changelog (what changed v0.1 → v0.2)

The pipeline architecture stays the same (all 4 A.5 critics confirmed this is the one thing v0.1 got right). Every gate has been modified, two new gates added, and the F-Score logic significantly extended.

| Component | v0.1 | v0.2 | Driver |
|---|---|---|---|
| **PSU classification** | None | **NEW Gate 0** — partial pipeline + PSU-CONTEXT annotations | C4 (∼40–50 NIFTY 500 names broke every gate); Pranav Q5 |
| **BFSI gate** | Silent SKIPPED | Stub output (NIM, GNPA, PCR, CAR with %) | C4 (broken product promise); Pranav Q4 |
| **Beneish** | Single-threshold knockout (M > −1.78) | **Two-stage conditional halt** + sector-conditional TATA coefficient (4.679 → 2.0 for heavy-asset) + BENEISH-INERT flag | All 4 critics; Pranav Q1 |
| **Governance Quality Screen** | None | **NEW Gate 2.5** — auditor changes + restatements + RPT + audit opinion | C2 (most reliable forensic indicators absent) |
| **Altman Z″** | Original X2 + X4' | X2_current (NPAT_TTM/TA) + Market Cap/TL + three-metric composite for old firms | All 4 critics; W5 escalated P1 → P0; Pranav Q3 |
| **Pledge** | Static > 30% | Two-factor (absolute > 40% + velocity > 10pp QoQ) + PLEDGE-LTV-CAUTION | C2 (LTV mechanics) |
| **Piotroski for cyclicals** | Same 9-signal for all | Normalized 3-yr-avg inputs for CYCLICAL-tagged sectors; broader cyclical scope | All 4 critics; W3 most damaging; Pranav Q2 |
| **Regime-Shift Calendar** | None | **NEW** hard-coded lookup table (FY2017–FY2020 transitions: demonetization / GST / Ind AS 115 / 109 / 116) | All 4 critics; W4 extended |
| **FCF/NI overlay** | mean(OCF)/mean(NI), uncapped | Cap at 3.0× + switch to mean(OCF/NI) + IMPAIRMENT-CHECK annotation | C1, C2, C4 |
| **Sector ROCE percentile** | NSE Sector tier (22 sectors); N≥15 floor | NSE Industry tier primary for heterogeneous sectors + 2-tier fallback + explicit peer display at N<10 | All 4 critics; W6 root cause extended |
| **Action labels** | HOLD / WATCH / REVIEW / FLAG; no hysteresis | Same 4 labels + 2-quarter hysteresis + structured REVIEW checklist + cyclical caveats; ROCE-blind-at-F≥7 fixed | C3, C4; Pranav Q6 (keep 4 labels for v0.2) |
| **Data-quality completeness** | Silent zeros (e.g. SGAI) | **NEW** — every output shows X/N computed + reason for any missing | C1, C2, C4 |

---

## 1. v0.2 picks (Pranav's confirmed defaults on Q1–Q8)

| Q | Decision | Pick |
|---|---|---|
| Q1 | Beneish gate design | **Two-stage conditional halt** |
| Q2 | Cyclical tag list breadth | **Broader** — metals/energy/power/fertilizers + companies with > 40% revenue from construction/housing/auto |
| Q3 | Altman Z″ replacement | **Both** — X2_current universal substitution + composite check for old firms |
| Q4 | BFSI stub format | **Quantitative** — actual NIM %, GNPA %, PCR %, CAR % with "no formal FA score" disclaimer |
| Q5 | PSU gate treatment | **Partial sub-pipeline** with PSU-CONTEXT annotations |
| Q6 | AFFIRM label? | **No, keep 4 labels** for v0.2 |
| Q7 (v0.4) | BFSI staging clarification in problem statement | **YES** — one-sentence addition (handled in v0.4 doc) |
| Q8 (v0.4) | Cadence clarification | **NO** — handled at math layer via delta-view + hysteresis |

---

## 2. The pipeline (v0.2)

For every NIFTY 500 stock at every evaluation date, the math runs in this exact order:

```
[0]  PSU classification check   → If PSU: flag PSU-CONTEXT, suppress invalid signals, continue
[1]  BFSI classification check  → If BFSI: produce BFSI-MONITOR stub (no FA score), halt FA branch
[2]  Beneish two-stage gate     → MANIPULATION-RISK halt OR BENEISH-CAUTION warn OR continue
[2.5] Governance Quality Screen → GOVERNANCE-RISK halt OR GOVERNANCE-CAUTION warn OR continue
[3]  Altman Z″ (modified) + composite for old firms → DISTRESS-RISK halt OR continue
[4]  Pledge two-factor gate     → PLEDGE-RISK halt OR PLEDGE-LTV-CAUTION OR continue
[5]  Compute Piotroski F-Score (regular for non-cyclicals; normalized for cyclicals)
[6]  Compute FCF / Net Income (3-yr, capped at 3.0×, IMPAIRMENT-CHECK annotation when applicable)
[7]  Compute Sector ROCE percentile (Industry tier primary; fallback rules)
[8]  Compose action label with hysteresis (2-quarter confirmation for non-knockout transitions)
[9]  Append data-quality completeness score + Regime-Shift Calendar context notes
```

Halts at gates [1]–[4] produce a label (FLAG or BFSI-MONITOR or PSU-suppressed-signals) plus the reason. No further math runs for halted stocks.

---

## 3. Gate 0 — PSU classification (NEW)

**Rule**: At evaluation date, check whether central or state government holds > 50% of equity (direct or via government-owned holding companies).

**Data source**: NSE shareholding-pattern filings (quarterly). Maintain a lookup table of NIFTY 500 PSUs (∼40–50 names: Coal India, ONGC, BPCL, IOC, HPCL, NTPC, Power Grid, SBI, Indian Bank, Bank of Baroda, GAIL, SAIL, etc.) for fast classification.

**If PSU**:

- **Suppress** the pledge gate (PSUs don't pledge promoter shares — government doesn't borrow against shares).
- **Tag** all leverage signals (F5, Beneish LVGI, Altman X4') with PSU-CONTEXT annotation: *"Leverage may reflect government-mandated capex; interpret cautiously."*
- **Tag** F7 (no-dilution) with PSU-CONTEXT: *"Government may conduct FPO for disinvestment targets; F7 fail may not signal weakness."*
- **Run** Beneish, Altman, Piotroski normally (with annotations). ROCE and FCF/NI are still valid for PSUs.
- **Continue** to next gate (don't halt).

**Output**: PSU-CONTEXT flag appears alongside whatever label the rest of the pipeline produces.

**Rationale (per A.5 §3 Theme H)**: PSUs break specific signals (pledge, dilution interpretation) but not all signals. Partial pipeline + annotation > full skip > full pass.

---

## 4. Gate 1 — BFSI classification + minimal stub output (MODIFIED)

**Rule**: If NSE industry classification belongs to `Banking`, `NBFC`, `Insurance`, or `Other Financial Services`, the FA pipeline does NOT run. Instead, produce a **BFSI-MONITOR stub** with the following:

| Field | Source | Display |
|---|---|---|
| NIM (current quarter) | Quarterly results | Show actual % |
| NIM (prior quarter) | Quarterly results | Show actual % |
| NIM trend | QoQ delta | IMPROVING / STABLE / DETERIORATING |
| GNPA (latest) | Asset Quality disclosure | Show actual % |
| GNPA (prior quarter) | Asset Quality disclosure | Show actual % |
| GNPA trend | QoQ delta | IMPROVING / STABLE / DETERIORATING |
| PCR (latest) | Provisioning disclosure | Show actual % |
| CAR (latest) | Capital Adequacy disclosure | Show actual % |

**Label**: `BFSI-MONITOR` (not FLAG, not HOLD).

**Disclaimer (mandatory, displayed with every BFSI-MONITOR output)**:
> *"No formal FA score: BFSI requires P/ABV, NIM stress-testing, GNPA-cycle, and CAR analysis that v0.2 does not implement. These trend indicators flag direction only. Full BFSI pipeline scheduled for v0.3."*

**Halt**: yes — the rest of the FA pipeline does not run for BFSI stocks.

**Rationale (per A.5 §3 Theme G, Pranav Q4)**: v0.1's silent skip produced zero output for ∼35–40% of NIFTY 500 by market cap. A real portfolio with HDFC Bank + ICICI Bank cannot have a planning tool that says nothing about its largest holdings. The stub doesn't claim to be a formal score; it gives direction.

---

## 5. Gate 2 — Beneish M-Score (two-stage conditional halt) (MODIFIED)

### 5.1 Formula

The 8-variable Beneish formula stays, with **one coefficient changed**:

```
M = -4.84
    + 0.920 · DSRI    + 0.528 · GMI
    + 0.404 · AQI     + 0.892 · SGI
    + 0.115 · DEPI    - 0.172 · SGAI
    + α(sector) · TATA - 0.327 · LVGI
```

Where:

```
α(sector) = 4.679   for non-heavy-asset sectors (default)
α(sector) = 2.0     for heavy-asset sectors:
                      Metals & Mining, Energy, Oil & Gas, Cement, Infrastructure
                    Identifiable as:
                      fixed-asset intensity > 50% of TA  OR
                      D&A / Revenue > 8%
```

The 8 indices (DSRI, GMI, AQI, SGI, DEPI, SGAI, TATA, LVGI) are computed exactly as in v0.1 §2.2. **One modification to LVGI**: for year-pairs spanning the Ind AS 116 transition (FY2019/FY2020), use **financial debt only** (Total Borrowings − Lease Liabilities per Ind AS 116 notes). All other coefficients unchanged.

**SGAI handling (data quality)**: SGAI is unavailable for the vast majority of NIFTY 500 companies (nature-of-expenses P&L format under Indian Companies Act Schedule III). Set SGAI = 0 and **explicitly flag in every Beneish output**:
> *"SGAI = 0 (default) — SG&A not disaggregated under Indian P&L format; coefficient contribution = 0; slight downward M-Score bias."*

### 5.2 Two-stage conditional halt logic

For computed M-Score with classification (year-pair in Regime-Shift Calendar per §10 or not):

| M-Score | Year-pair in regime-shift calendar? | Governance Quality Screen result | Verdict |
|---|---|---|---|
| M > −1.50 | (any) | (any) | **HALT** with `FLAG: MANIPULATION-RISK`. Clear breach territory — no regime-shift exception. |
| M ∈ [−1.78, −1.50] | YES | ≥ 1 flag fires | **HALT** with `FLAG: MANIPULATION-RISK`. Borderline + corroborating governance signal = real risk. |
| M ∈ [−1.78, −1.50] | YES | No flags | **WARN** with `BENEISH-CAUTION`. Pipeline continues to gate 2.5. Output note: *"Borderline M-Score in regime-shift window without governance corroboration. Likely a macro artifact."* |
| M > −1.78 | NO (for 2 consecutive years) | (any) | **HALT** with `FLAG: MANIPULATION-RISK`. Two-year persistence outside regime windows is a real signal. |
| M > −1.78 | NO (single year only) | (any) | Context note in output: *"Beneish M-Score elevated in single year — review DSRI and AQI drivers."* Pipeline continues. |

**BENEISH-INERT flag**: when the TATA term alone would push M below −3.5 regardless of the other 7 indices (i.e., when D&A / Revenue > 15% AND impairment-driven OCF >> NI), do NOT report a PASS. Instead, output:
> *"BENEISH-INERT: M-Score has low signal power for this sector class (commodity heavy industry). Manipulation risk assessed via Governance Quality Screen instead."*

When BENEISH-INERT fires, gate 2.5 (Governance Quality Screen) becomes the primary manipulation signal.

### 5.3 Rationale

A.5 critics unanimous: v0.1's single-threshold knockout was the most damaging gate design. Asian Paints Mar-2022 crossed by 0.083 units (knife-edge) in a regime-shift year (COVID-era). C2's two-stage gate (recommended by synthesizer §6.1) preserves hard halt for clear manipulators while eliminating the regime-shift false positive in the [−1.78, −1.50] zone. Combined with sector-conditional TATA per C1 (Tata Steel FY2023 GMI = 1.961 was suppressed by TATA in v0.1 — now visible).

---

## 6. Gate 2.5 — Governance Quality Screen (NEW)

Check four indicators in the most recent annual report year:

| # | Check | Source | Threshold |
|---|---|---|---|
| 1 | **Auditor change** from Big4 / reputable mid-tier → smaller firm in past 2 years | NSE / SEBI auditor filing | Flag fires unless change reason is "mandatory rotation" or "Big4 to Big4" |
| 2 | **Financial restatement** in past 3 years covering revenue / receivables / goodwill / impairments | SEBI EDGAR | Flag fires on any |
| 3 | **RPT concentration** — related-party purchases + sales as % of revenue | Annual report note (mandatory disclosure under Companies Act §188) | Flag fires if > 15% in most recent year |
| 4 | **Audit opinion** — qualified / adverse / emphasis-of-matter on going concern | Annual report Auditor's Report | Flag fires on any |

**Result mapping**:

| Flags firing | Verdict |
|---|---|
| 0 | Pass silently. Pipeline continues. |
| 1 | **WARN** with `GOVERNANCE-CAUTION: [specific flag]`. Pipeline continues. Output annotation visible. |
| ≥ 2 (any combination) | **HALT** with `FLAG: GOVERNANCE-RISK`. Two or more independent governance signals firing is the most reliable forensic indicator pattern (per C2's IL&FS / Yes Bank / Vakrangee / Manpasand history). |

**Data unavailability handling**: if any one of the four checks cannot be performed (data missing), flag with `DATA-UNAVAILABLE: [check name]` in the output. Do not silently fail it as "no flag". Pranav can interpret missing data as he sees fit.

**Rationale (per A.5 §3 Theme B, C2)**: In every major NSE blow-up case in the past decade (IL&FS, Yes Bank, DHFL, Vakrangee, Manpasand), at least one of these four indicators fired before the price collapse. Beneish + Altman are correlated (share Total Assets denominator); this gate provides genuinely independent confirmation.

---

## 7. Gate 3 — Altman Z″ (modified, with composite for old firms) (MODIFIED)

### 7.1 Universal modifications

Replace v0.1's Altman variables as follows:

| Term | v0.1 | v0.2 | Coefficient |
|---|---|---|---|
| X2 | Retained Earnings / Total Assets | **X2_current = NPAT_TTM / Total Assets** | 3.26 (unchanged) |
| X4' | Book Equity / Total Liabilities | **Market Cap / Total Liabilities** (NSE-listed companies always have market cap) | 1.05 (unchanged) |

X1 (Working Capital / TA) and X3 (EBIT / TA) unchanged.

**Modified Z″ formula**:
```
Z″_v0.2 = 6.56·X1 + 3.26·X2_current + 6.72·X3 + 1.05·(MktCap/TL) + 3.25
```

**X1 adjustment for Ind AS 116 transition**: for FY2019/FY2020 year-pairs, exclude the current portion of lease liabilities from current liabilities when computing X1. This prevents the artificial dip from Ind AS 116 adoption.

### 7.2 Composite check for old / reserve-heavy firms

For companies meeting **either** of these conditions:

- Accumulated reserves > 200% of EBITDA (TTM), OR
- Listing history > 30 years

Run a **three-metric composite check** in parallel with the modified Z″:

| Metric | Distressed threshold |
|---|---|
| Net Debt / EBITDA | > 5.0× |
| Interest Coverage (EBIT / Interest Expense) | < 1.5× |
| Current Ratio | < 0.9 |

**Composite halt condition**: ALL THREE thresholds breach simultaneously. (This preserves the probabilistic nature — one or two breaches alone may be cyclical noise.)

**Halt trigger**: either modified Z″ < 1.1 OR composite (all three) breaches → `FLAG: DISTRESS-RISK`. Grey zone for modified Z″ ∈ [1.1, 2.6] → context note, no halt.

### 7.3 Mandatory supplementary display

For every non-BFSI, non-PSU stock (regardless of Z″ verdict), display:

| Field | Threshold for label | Label |
|---|---|---|
| Net Debt / EBITDA (TTM) | > 4.0× | "Elevated" |
| Net Debt / EBITDA (TTM) | > 6.0× | "High" |
| Interest Coverage (TTM) | < 2.0× | "Low" |

**Rationale**: even when Z″ passes (which it almost always does for old Indian firms — Tata Steel Z″ was 5.5–5.9 across all 4 test dates despite ₹88–116k Cr long-term debt), supplementary leverage metrics give the investor the actual debt picture.

---

## 8. Gate 4 — Promoter Pledge (two-factor) (MODIFIED)

### 8.1 The two factors

| Factor | Threshold | Result |
|---|---|---|
| **Absolute** | Pledge > 40% of promoter holding | WARN |
| **Velocity** | Pledge increased > 10pp QoQ, OR pledge > 20% AND increased for two consecutive quarters | WARN |
| **Both simultaneously** | (Absolute > 40% AND velocity > 10pp QoQ) | **HALT** with `FLAG: PLEDGE-RISK` |

### 8.2 PLEDGE-LTV-CAUTION

If the last pledge filing's reference stock price was > 30% above the current price, append `PLEDGE-LTV-CAUTION` annotation. (When pledged shares' LTV is upside-down, forced-sale risk rises sharply — this is the actual SEBI margin-call trigger, not the absolute pledge %.)

### 8.3 PSU suppression

Per Gate 0: PSUs always have 0% pledge (government doesn't borrow against shares). Skip this gate entirely for PSUs.

### 8.4 Data source

NSE pledged-data filings (quarterly). Compute velocity from current vs prior-quarter filing.

**Rationale (per A.5 §3 Theme D)**: 30% absolute threshold in v0.1 caught too many stable long-standing pledges (Adani group e.g. held > 30% for years without issue). The real danger signal is *velocity* (sudden increase) and *LTV* (pledge value relative to current stock price), not the absolute static %.

---

## 9. Piotroski F-Score (with cyclical normalization) (MODIFIED)

### 9.1 Cyclical sector tag list

Define `CYCLICAL = True` for any company meeting **either** condition:

- **Sector match** (primary list): Metals & Mining, Oil & Gas, Power, Fertilizers
- **Revenue concentration**: > 40% revenue from any of:
  - Construction (EPC, infrastructure, real estate, housing)
  - Automotive (OEM, auto-ancillary)
  - Industrial commodities (commodity chemicals, paper, basic materials)

(This is the **broader** scope per Pranav's Q2. C4's housing/auto example — Crompton, Astral, Kajaria, Voltas — is captured.)

### 9.2 Behavior for non-cyclical stocks

Compute the original 9-signal Piotroski F-Score exactly as v0.1 §3.

### 9.3 Behavior for CYCLICAL stocks

Compute the full 9-signal F-Score with **normalized inputs**:

| Signal | v0.1 input | v0.2 input (CYCLICAL only) |
|---|---|---|
| F1 (ROA > 0) | NetIncome_t / Avg(TA) | 3-yr-avg EBIT / Avg(TA) > 0 |
| F2 (ΔROA > 0) | ROA_t − ROA_{t−1} | 3-yr-avg EBIT/TA_t − 3-yr-avg EBIT/TA_{t−1} > 0 |
| F3 (CFO > 0) | OCF_t / TA_{t−1} | 3-yr-avg OCF / Avg(TA) > 0 |
| F4 (CFO > NI) | OCF_t > NI_t | unchanged (still single-year) |
| F5 (ΔLev < 0) | (LTD/Avg.TA)_t < (LTD/Avg.TA)_{t−1} | unchanged (with regime-shift handling per §10) |
| F6 (ΔLiq > 0) | CR_t > CR_{t−1} | unchanged |
| F7 (no dilution) | Shares_t ≤ Shares_{t−1} | unchanged |
| F8 (ΔGM > 0) | GM_t > GM_{t−1} | 3-yr-avg GM_t > 3-yr-avg GM_{t−1} |
| F9 (ΔTurnover > 0) | (Rev/Avg.TA)_t > (Rev/Avg.TA)_{t−1} | 3-yr-avg (Rev/Avg.TA)_t > 3-yr-avg (Rev/Avg.TA)_{t−1} |

### 9.4 Display

For CYCLICAL-tagged stocks, output two scores:

1. **F-Score (cycle-adjusted)** — using normalized inputs above. This is the routing score.
2. **Raw F-Score** — using single-year inputs (v0.1 method) — displayed as context only.

Mandatory caveat in output for cyclical stocks:
> *"CYCLICAL-SECTOR: F-Score reflects trailing cycle position. Deteriorating signals at sector trough may precede the best entry points. Compare current ROCE and margins to 10-year median before reducing position."*

### 9.5 "Stable-quality" subset (secondary context)

Also display the **4-signal stable-quality score** for cyclicals (F1, F3, F4, F7 — the signals that do NOT co-move with commodity prices). Label: *"Stable-quality signals (non-cycle-sensitive): X/4."*

**Rationale**: A.5 W3 — Piotroski cyclical inversion is the most damaging structural failure. Tata Steel Mar-2020 had F=5/9 (trough; +355% forward) vs Mar-2021 F=8/9 (peak; +34% forward). Spearman = −1.0 across 4 dates. Per C1, 4 of 9 signals (F2, F5, F8, F9) measure cycle position, not firm quality. Normalizing via 3-yr averages dampens this; the 4-signal subset is the pure-quality view.

---

## 10. Regime-Shift Calendar (NEW)

Hard-coded lookup table consulted before computing **any** YoY signal:

| Event | Affected year-pairs | Affected signals | Neutralization rule |
|---|---|---|---|
| Demonetization | FY2016/FY2017 | Beneish DSRI, Beneish SGI, Piotroski F9 | Tag DEMONETIZATION-YEAR; exclude affected signals from F-Score denominator (max F-Score reduces from 9 to 7 for this year-pair) |
| GST introduction | FY2017/FY2018 | Beneish SGI, Piotroski F9 (asset turnover) | Use 2-yr avg revenue growth (FY2017 → FY2019) for SGI and F9; tag GST-TRANSITION |
| Ind AS 115 (revenue recognition) | FY2018/FY2019 | Beneish SGI, Piotroski F9 (for EPC, real estate, telecom, retail) | Exclude affected signals from F-Score denominator for those sectors; tag IND-AS-115-TRANSITION |
| Ind AS 109 (financial instruments / ECL) | FY2018/FY2019 | Beneish DSRI, Piotroski F1/F2 (for capital goods, infra, EPC — ECL provision hits NI) | Exclude F1/F2 from denominator for those sectors; tag IND-AS-109-TRANSITION |
| Ind AS 116 (leases) | FY2019/FY2020 | Piotroski F5, Beneish LVGI, Altman X1 | F5 + LVGI: use **financial debt only** (Total Borrowings − Lease Liabilities per Ind AS 116 notes). Altman X1: exclude current portion of lease liabilities. Tag IND-AS-116-TRANSITION |
| COVID lockdowns | FY2020/FY2021, FY2021/FY2022 | Beneish DSRI, Beneish AQI | These year-pairs are also registered as Beneish two-stage regime-shift windows per §5.2. Add COVID-WINDOW context note. |

### 10.1 Application

Before computing each YoY signal pair (t, t−1):

1. Check whether the pair appears in the Regime-Shift Calendar.
2. If yes and the signal is in the "affected signals" list: apply the neutralization rule.
3. If neutralization = "exclude from F-Score denominator," subtract 1 from the denominator. F-Score is then reported as `X/N` where N < 9, plus a note: *"N/9 signals computed (M excluded: [reason])."*
4. If neutralization = "use 2-yr avg," compute the signal across t−2 to t instead of t−1 to t.

### 10.2 Display

Every Beneish, F-Score, FCF/NI output for an affected year-pair carries a context note: *"Year-pair spans [event name]. [Rule applied.]"*

**Rationale (per A.5 §3 Theme A and C2)**: v0.1 was blind to the fact that Indian accounting / regulatory standards have shifted 5+ times in the past decade. Each shift creates a structural YoY discontinuity that doesn't reflect firm quality. Hard-coded calendar > runtime detection — the events are known dates.

---

## 11. FCF / Net Income overlay (modified) (MODIFIED)

### 11.1 Formula

**Switch to mean-of-ratios** (averages the ratio, not the raw cash flows):

```
CashConversion = mean(OCF_t / NI_t, OCF_{t-1} / NI_{t-1}, OCF_{t-2} / NI_{t-2})
```

(v0.1 was mean(OCF) / mean(NI) — which gave arbitrarily large ratios when a single near-zero NI year dominated. C1 explicitly flagged this.)

**Chronic loss handling**: if NI < 0 for any year in the 3-yr window, exclude that year-ratio from the mean. Reduce the averaging window to 2 (or 1) years and note in output: *"FCF/NI averaged over N years (M excluded for loss)."*

### 11.2 Cap and IMPAIRMENT-CHECK annotation

Cap the CashConversion ratio at **3.0×** for routing purposes (i.e., for the action label composition table — see §15).

If raw computed CashConversion > 3.0×, display the capped value AND append annotation:
> *"IMPAIRMENT-CHECK: Cash conversion exceeds 3.0×, which usually indicates large non-cash charges (impairments, write-downs, depreciation > revenue growth) rather than earnings quality. Investigate impairment schedule before treating as quality signal."*

### 11.3 Label thresholds (unchanged from v0.1)

| Capped CashConversion | Label |
|---|---|
| ≥ 1.0 | HIGH-QUALITY EARNINGS |
| 0.7 – 1.0 | ACCEPTABLE |
| < 0.7 | EARNINGS-QUALITY-RISK (additive flag, not a halt) |

---

## 12. Sector ROCE percentile (with tier fallback) (MODIFIED)

### 12.1 Tier selection

For each NSE sector, determine the **primary peer-set tier** using this lookup:

| Sector type | Primary tier |
|---|---|
| **Heterogeneous sectors** (sub-categories not comparable): Chemicals, Healthcare, Consumer Durables, Financial Services, IT, Diversified Industrials | **NSE Industry tier** (Tier 3) |
| **Homogeneous sectors**: Metals & Mining, Oil Gas & Consumable Fuels, Power, Fertilizers | NSE Sector tier (Tier 2 — 22 sectors) |

### 12.2 Fallback rules

Applied sequentially:

| Step | Condition | Action |
|---|---|---|
| 1 | Primary tier N ≥ 10 | Compute percentile. Display: *"ROCE percentile = X within [tier name]"* |
| 2 | Primary tier N < 10 | Fall back to one tier up (Industry → Sector → Macro). If new tier N ≥ 10, compute percentile with note: *"Expanded peer set: [tier name]"* |
| 3 | Even broader tier N < 10 | Show explicit peer comparison: *"Rank N of M within [tier]: ROCE = X% vs [Peer A: Y%, Peer B: Z%, ...]"* (include all M peers). Interpretable at N = 4. |

### 12.3 ROCE definition (with Ind AS 116 consistency)

```
ROCE = EBIT_TTM / (Current Equity + Net Debt + Minority Interest)
```

Where **Net Debt** is computed as:

- For evaluation dates using balance sheets that include FY2020 or later: `Total Borrowings − Lease Liabilities (per Ind AS 116 notes)`. Label: *"ROCE (financial debt basis, comparable across Ind AS 116 transition)."*
- For evaluation dates using pre-FY2020 balance sheets: `Total Borrowings`. Label: *"ROCE (total borrowings basis, pre-Ind AS 116)."*

**Within a sector peer set for a given evaluation date, all peers must use the same Net Debt basis** — do not mix.

### 12.4 Winsorization (unchanged)

Cap ROCE at 3× IQR above the 75th percentile of the sector before ranking.

---

## 13. Action labels (with hysteresis) (MODIFIED)

### 13.1 Label set

Same four labels as v0.1: **HOLD / WATCH / REVIEW / FLAG**. AFFIRM deferred per Pranav Q6.

### 13.2 Hysteresis (mandatory for v0.2)

All non-knockout transitions between HOLD, WATCH, REVIEW require **2 consecutive quarterly data releases confirming the same direction** before the label changes.

**Exception**: knockout-gate labels (FLAG: MANIPULATION-RISK / GOVERNANCE-RISK / DISTRESS-RISK / PLEDGE-RISK) fire immediately on the gate triggering. No hysteresis.

**First-occurrence deterioration**: instead of moving from HOLD straight to WATCH, the label `WATCH-DETERIORATION-DETECTED` is used for the first quarter. If next quarter confirms the same direction, the label moves to WATCH proper. If next quarter reverts, label moves back to HOLD with no churn.

**Output format**:
- *"HOLD (stable 3 quarters)"* — label confirmed; how many quarters stable
- *"WATCH-DETERIORATION-DETECTED (1st consecutive — 1 more quarter needed to confirm WATCH)"* — first-occurrence deterioration
- *"WATCH (2nd consecutive — confirmed)"* — confirmed transition

### 13.3 REVIEW structured checklist

When the math reports `REVIEW`, the output must include a structured breakdown:

```
REVIEW — Specific failure groups:
  - Profitability (F1-F4): X/4 signals failing — [list which]
  - Leverage/Liquidity (F5-F7): Y/3 signals failing — [list which]
  - Operating Efficiency (F8-F9): Z/2 signals failing — [list which]
  - FCF/NI quality: [PASS / EARNINGS-QUALITY-RISK]
  - ROCE percentile: P (within [tier])
  - Consecutive quarters of deterioration: N
  
Specific binary thesis question:
  "Has the original reason you bought this been damaged? Specifically:
   - [If F1-F4 failing] Is the company's profitability durable?
   - [If F5-F7 failing] Is the company over-extending on debt or diluting equity?
   - [If F8-F9 failing] Is the company's competitive edge eroding (margins, asset productivity)?"
```

### 13.4 WATCH for cyclicals

If a cyclical-tagged stock receives WATCH, append:
> *"CYCLICAL-SECTOR WARNING: deteriorating F-Score at sector trough may indicate entry opportunity, not deterioration. Compare current ROCE and margins to 10-year median before reducing position."*

### 13.5 ROCE-blind-at-F≥7 fixed

v0.1's action label composition table ignored ROCE percentile for F ≥ 7. This produced Tata Steel F=8 HOLD at 21st-percentile ROCE (peak entry signal). Fixed: ROCE percentile is now factored at ALL F-Score levels per the updated composition table in §15.

**Rationale (per A.5 §3 Themes E + K + L)**: hysteresis fixes churn (W3 + weekly cadence interaction); structured REVIEW fixes non-actionability (REVIEW = "re-examine" without scaffold was anxiety, not insight); ROCE-blind fix prevents the peak-entry-signal failure mode.

---

## 14. Data-quality completeness score (NEW)

Every output displays a completeness score for the underlying math:

| Output | Completeness display | Reason for missing (when applicable) |
|---|---|---|
| Beneish | "X / 8 indices computed" | SGAI = 0 (default), data missing for prior year, etc. |
| Piotroski F-Score | "Y / N signals computed" (where N = 9 or N reduced via Regime-Shift Calendar) | Regime-shift signal exclusion, missing data, etc. |
| FCF / NI | "Window: M years" (where M = 3 or reduced for loss years) | Excluded year(s) for NI < 0 |
| Governance Quality Screen | "X / 4 checks completed" | DATA-UNAVAILABLE per check |

This makes the output's epistemic state visible. A reader can distinguish "passed" from "data missing → defaulted to pass" — these were silently identical in v0.1.

---

## 15. Action label composition (v0.2 routing table) (MODIFIED)

For non-halted, non-BFSI, non-PSU stocks (after gates [0]–[4] all clear, with PSU and CYCLICAL annotations attached as relevant):

| F-Score (cycle-adjusted if cyclical) | FCF/NI (capped) | ROCE percentile | Action label |
|---|---|---|---|
| ≥ 7 | ≥ 1.0 | ≥ 60 | **HOLD** (healthy across all dimensions) |
| ≥ 7 | ≥ 0.7 | ≥ 40 | **HOLD** (strong momentum; acceptable cash + capital efficiency) |
| ≥ 7 | < 0.7 | (any) | **WATCH** (signals improving but cash quality lagging — investigate) |
| ≥ 7 | (any) | < 40 | **WATCH** (strong momentum but weak capital efficiency — possible cycle peak) |
| 5–6 | ≥ 1.0 | ≥ 50 | **WATCH** (mixed F-Score but cash quality + capital efficiency intact) |
| 5–6 | ≥ 0.7 | < 50 | **REVIEW** (fundamentals mixed and capital efficiency below sector median) |
| 5–6 | < 0.7 | (any) | **REVIEW** (mixed signals + cash-quality risk) |
| ≤ 4 | (any) | (any) | **REVIEW** (fundamentals deteriorating; deep review needed) |

Apply **hysteresis** per §13.2 to every transition between non-FLAG labels.

If a label is **WATCH** and the company is **CYCLICAL-tagged**, append the cyclical caveat per §13.4.

### Glossary (carried from v0.1)

- **HOLD** — fundamentals healthy across all dimensions; no action needed beyond periodic reaffirmation.
- **WATCH** — minor deterioration or mixed signals; monitor next-quarter results before acting.
- **REVIEW** — material concerns; user should re-examine the original thesis using the structured checklist (per §13.3).
- **FLAG** — knockout gate failed; consider exit candidate.

---

## 16. Worked example (illustrative — re-using v0.1's XYZ Ltd)

Re-running v0.1's hypothetical mid-cap manufacturing example `XYZ Ltd` through v0.2:

**Step 0 — PSU check**: Not PSU. Continue.

**Step 1 — BFSI check**: NSE sector = "Industrial Manufacturing". Not BFSI. Continue.

**Step 2 — Beneish**:
- Industrial Manufacturing is **not** heavy-asset → α = 4.679.
- Compute M = −2.41. Year-pair: FY2023/FY2024 (not in Regime-Shift Calendar).
- M < −1.78 + single year + not in regime window. → Context note only. Pipeline continues.
- SGAI = 0 (annotated).

**Step 2.5 — Governance Quality Screen**:
- Auditor: stable Big4 → no flag.
- Restatements (past 3 years): none → no flag.
- RPT: 4% of revenue → no flag (< 15%).
- Audit opinion: clean → no flag.
- Result: 0 flags. Pass silently.

**Step 3 — Altman Z″ modified**:
- X1 = 0.18, X2_current = 0.08, X3 = 0.12, MktCap/TL = 4.5.
- Z″ = 6.56·0.18 + 3.26·0.08 + 6.72·0.12 + 1.05·4.5 + 3.25 = 9.74. Far above 1.1.
- Not old/reserve-heavy → composite skipped.
- Supplementary display: Net Debt / EBITDA = 1.2× (no label); Interest Coverage = 8× (no label). Pipeline continues.

**Step 4 — Pledge**:
- 8% of promoter holding, stable over 4 quarters. No velocity issue.
- LTV: filing-date stock price = current → no LTV-CAUTION.
- Pass silently.

**Step 5 — Piotroski**:
- Not cyclical. Compute v0.1-style 9-signal F-Score.
- Result: F = 7.
- All signals computed (9/9). No regime-shift exclusions.

**Step 6 — FCF / NI**:
- mean(OCF/NI) over 3 yrs = 1.11. Below cap of 3.0×, no IMPAIRMENT-CHECK. Label: HIGH-QUALITY EARNINGS.

**Step 7 — Sector ROCE percentile**:
- Industrial Manufacturing is heterogeneous. Use NSE Industry tier (Tier 3). N = 28.
- XYZ ROCE = 22%, rank 5 of 28. Percentile = (28 − 5) × 100 / (28 − 1) = 85.2 ≈ 85.
- Display: *"ROCE percentile = 85 within Heavy Electrical Equipment (NSE Industry tier)."*

**Step 8 — Action label**:
- F = 7 + FCF/NI ≥ 1.0 + ROCE percentile ≥ 60 → **HOLD**.
- Hysteresis: was HOLD last 2 quarters → "HOLD (stable 3 quarters)."

**Step 9 — Data-quality completeness**:
- Beneish: 7/8 (SGAI default). F-Score: 9/9. FCF/NI: 3-yr window full.

**Reasoning string (sample output)**:

> **XYZ Ltd — HOLD (stable 3 quarters)**
>
> F-Score = 7/9. Cash conversion 1.11× (3-yr avg, capped) — earnings backed by cash. ROCE = 22% (85th percentile within Heavy Electrical Equipment, Tier 3, N=28) — strong capital efficiency.
>
> No manipulation risk (Beneish M = −2.41 with 7/8 indices computed; SGAI default per Indian P&L format).
> No governance flags (auditor stable, no restatements, RPT 4% of revenue, clean audit opinion).
> No distress risk (Altman Z″ = 9.74; Net Debt/EBITDA = 1.2×; Interest Coverage = 8×).
> No pledge risk (promoter pledge 8%, stable across 4 quarters).
>
> Fundamental thesis intact. No action needed beyond periodic reaffirmation.

---

## 17. What v0.2 STILL doesn't do (deferred to later)

| Deferred to | Item |
|---|---|
| v0.3 | Full BFSI FA pipeline (P/ABV, NIM stress-testing, GNPA cycle, CAR analysis) |
| v0.3 | AFFIRM label (5th label for F ≥ 8 + FCF ≥ 1.0 + ROCE ≥ 75th percentile + zero flags) |
| v0.3 | Specialty chemicals sub-sector peer-mapping lookup (one-time table) |
| v0.3 | Beneish on standalone financials for conglomerates (consolidated TA > 1.5× standalone TA) |
| v0.3 | ADTV liquidity floor as output field |
| Cycle B | All TA signals (RSI, MACD, 200DMA, Bollinger, OBV, ATR, Supertrend, ADX) |
| Cycle C | Mutual-fund-specific signals (TER drift, MF-equity overlap, manager tenure, category percentile, direct-vs-regular plan, tax-bucket math) |
| Cycle D | Position sizing, correlation-to-portfolio impact |
| Cycle E | Exit rules, stop-losses, tax-aware sell sequencing (LTCG/STCG calculator) |
| Cycle F | TA/FA conflict resolution math, behavioural-metric formulas, signal combination |

---

## 18. Open questions for A.7 (re-testing v0.2 — optional)

The A.5 synthesizer recommended optionally re-testing v0.2 on Asian Paints + Tata Steel before closing Cycle A. If we do this:

1. **Re-run Asian Paints Mar-2020 / 2021 / 2022 / 2024** through v0.2. Expected:
   - Mar-2022 should no longer FLAG (regime-shift calendar + two-stage Beneish should keep M ∈ [−1.78, −1.50] as WARN, not HALT).
   - Mar-2020 F-Score should improve (Ind AS 116 transition handling restores F5).
   - Sector ROCE percentile should now be computable (Industry-tier fallback for small paints sector).

2. **Re-run Tata Steel Mar-2020 / 2021 / 2022 / 2024** through v0.2. Expected:
   - Mar-2020 should now show "F-Score (cycle-adjusted) = X/9" via normalized 3-yr inputs. May correctly identify trough entry opportunity.
   - Mar-2021 should now show WATCH (cyclical peak warning), not HOLD.
   - Altman Z″ → modified Z″ + composite (>30 years old → composite check). Net Debt/EBITDA 6.7× will be visible.
   - Beneish TATA coefficient drops from 4.679 → 2.0 (heavy-asset sector). M-Score may approach threshold in years with high GMI/AQI (verify FY2023).

3. **Add a third test stock** (per A.5 confidence notes) — ideally a non-metal cyclical (e.g., Crompton Greaves Consumer Electricals or Astral Ltd) to validate that the broader CYCLICAL tag works as expected for housing/auto-revenue-driven companies.

4. **Optionally**: a known-historical manipulation case (e.g., Vakrangee or Manpasand Beverages, run retrospectively pre-blow-up) to validate the Governance Quality Screen catches it.

**Decision deferred to Pranav**: do A.7 re-test now, or close Cycle A and revisit during Cycle F (signal combination)?

---

## 19. Confidence in v0.2

| Component | Confidence | Why |
|---|---|---|
| Pipeline architecture (gates → primary → overlay → label) | HIGH | All 4 critics + v0.1 testing confirmed sound |
| Beneish two-stage halt + sector-conditional TATA | MEDIUM-HIGH | Specific thresholds (−1.50, α = 2.0) are proposed, not NSE-calibrated. A.7 re-test would help |
| Governance Quality Screen | MEDIUM | The four checks are well-established in SEBI enforcement history but un-validated against false-positive rate on healthy NIFTY 500 names |
| Altman X2_current + composite | HIGH | Universal X2 substitution is a clean theoretical improvement; composite metrics are standard credit analysis |
| Piotroski cyclical normalization | MEDIUM-HIGH | 3-yr-avg approach is sound; CYCLICAL tag list breadth (esp. housing/auto extension per Pranav Q2) is judgment, would benefit from a third test stock |
| Regime-Shift Calendar | HIGH | Events and year-pairs are known historical dates; neutralization rules are conservative (exclude from denominator vs zero out) |
| Action label routing table | MEDIUM | The new ROCE-at-F≥7 logic is a clear fix, but threshold values (60, 40, 50) are inherited from v0.1 and would benefit from NSE-data calibration |
| Hysteresis design | HIGH | Standard pattern for advisory tools; 2-quarter confirmation is conservative |

---

## 20. Sources (additions for v0.2)

All v0.1 sources carry forward. Additional sources informing v0.2:

- A.5 multi-agent critique synthesis (`15_cycle_A_critiques_v0.1.md`) — primary driver
- SEBI EDGAR data (governance signals — auditor changes, restatements)
- Indian Companies Act 2013 §188 (related-party transaction disclosure framework)
- Ind AS 116 transition notes (for lease-liability separation)
- NSE Industry classification (Tier 3) (sector peer-set primary grouping)

---

**End of v0.2 spec.** Awaiting Pranav's review. Next steps depend on his call:

- **Option 1**: Close Cycle A now. Cycle B (Equity TA) begins.
- **Option 2**: Run A.7 — re-test v0.2 on Asian Paints + Tata Steel (and optionally a third stock) before closing.
