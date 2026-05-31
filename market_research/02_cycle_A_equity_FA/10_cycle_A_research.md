# 10 — Cycle A Research: Equity Fundamental Analysis

**Status**: Draft — A.1 complete  
**Date**: 2026-05-30  
**Scope**: Direct equity (NSE) FA math only. MFs → Cycle C. TA → Cycle B. Sizing → Cycle D. Exit → Cycle E.

---

## Executive Summary (15 bullets)

1. **Classical ratios are well-documented** — P/E, P/B, EV/EBITDA, ROE, ROCE formulas are unambiguous. The debate is in their thresholds, not their construction.
2. **Value premium exists on NSE, but is smaller and noisier than the US.** P/B and E/P signals show positive but modest return differentials in India (see Emerald / Sage 2015–2020 studies). No clean 5-year rolling evidence after 2016.
3. **Piotroski F-Score shows positive NSE evidence** — a 2024 study on Nifty 100 (2007–2024) confirms high-F-score portfolios outperform, particularly in downturns. The most rigorous India replication found.
4. **Magic Formula (Greenblatt) has contradictory NSE evidence.** Pre-2012 backtests look promising; 2012–2020 period shows ~1% CAGR vs Sensex ~100% — a severe underperformance. Likely driven by small-cap liquidity artefacts and exclusion of transactions costs.
5. **Saurabh Mukherjea's Coffee-Can criteria are the most precisely documented Indian framework.** Exact thresholds: revenue growth ≥10% AND ROCE ≥15% each year for 10 consecutive years; min market cap ₹100 Cr. Financial services carve-out: loan growth ≥15% + ROE ≥15% each year for 10 years.
6. **Marcellus Consistent Compounders adds FCF quality** — the twin-filter is similar to Coffee-Can but requires sustained FCF CAGR ~25%; 10–20 stock concentrated portfolio.
7. **MSCI Quality Factor is formally defined** as Z-score composite of three metrics: ROE, D/E (inverted), and earnings variability (inverted). Weights are equal-average of the three Z-scores. NSE's own multi-factor indices use a version of this.
8. **Indian-specific gotchas are material and sector-defined.** Banks require P/ABV (not P/B), NIM, NPA%, PCR. Commodities: EV/EBITDA normalized not P/E. Real estate: NAV discount/premium. PSUs: government ownership distorts capital efficiency. Promoter-pledge: high pledge % is a non-financial red flag that FA alone cannot capture.
9. **NSE classification differs from GICS.** NSE Indices uses a 4-tier system (12 Macro-Economic Sectors → 22 Sectors → 59 Industries → 197 Basic Industries). GICS has 11 sectors, 25 industry groups. Both coexist; screener platforms use their own mappings.
10. **Sector-relative percentile rank math is straightforward** but small-sample sectors require caution (<10 constituents: percentile ranks become unstable). Banking sector P/B comparison is meaningless cross-sector; only within-sector P/ABV percentile is valid.
11. **Beneish M-Score has Indian validation** — Indian Journal of Finance study on BSE 100 confirms it flags manipulation precursors; telecom and construction sectors show highest signals. M-Score > -1.78 is the manipulation flag threshold.
12. **Altman Z-Score EM variant (Z'') is the correct form for Indian companies.** Replaces market equity with book equity in X4; adds +3.25 constant. EM safe zone: Z'' > 2.6; distress: Z'' < 1.1.
13. **No NSE-specific empirical evidence for Buffett-style moat screens.** The moat criteria (brands, network effects, switching costs) are qualitative and no peer-reviewed Indian study validates a quantitative moat proxy as a return predictor on NSE. Excluded from v0.1 per Pranav's direction.
14. **Data availability is asymmetric.** Screener.in has 10+ years of financials for 5,000+ stocks and is the de-facto standard. Consolidated vs. standalone confusion is the single largest data quality issue on Indian platforms.
15. **Open questions for A.2** include: which scoring frameworks to combine, whether to use trailing or forward estimates, and how to handle sector carve-outs for banks and commodities.

---

## Bucket 1 — Classical Valuation Ratios

### 1.1 Price-to-Earnings (P/E)

| Attribute | Detail |
|---|---|
| **Trailing P/E** | $P/E_{TTM} = \text{Price} / \text{EPS}_{TTM}$ where EPS is the sum of the last four quarters |
| **Forward P/E** | $P/E_{fwd} = \text{Price} / \widehat{\text{EPS}}_{t+1}$ where $\widehat{\text{EPS}}$ is analyst consensus or own estimate |
| **What it measures** | How many years of current earnings you're paying per rupee of price |
| **Theoretical basis** | Gordon Growth Model collapses to $P/E = 1/(r - g)$ for a stable growing firm; hence low P/E implies high discount rate or low growth, high P/E the reverse |
| **India ranges** | Nifty 50 long-run median ~22x; below 15x historically signals cheap, above 30x historically elevated. Sector variation is extreme (IT 30–40x; PSU banks 5–10x) |
| **Failure modes** | (1) Cyclical companies: P/E is very high at cycle trough and low at peak — counter-intuitive. (2) Loss-making companies: undefined. (3) One-time items inflate/deflate EPS. (4) Earnings quality (accruals) problem. |
| **NSE evidence** | Saji & Harikumar (2015, *Vision — Sage Journals*) confirm E/P rate is a prime determinant of NSE IT sector returns 2000–2010. Emerald Insight study (2020) finds value premium sector-specific, not uniform. NSE publishes daily sector P/E ratios — [NSE Sector P/E](https://craytheon.com/charts/nse_sector_pe_chart.php) |

### 1.2 PEG Ratio

| Attribute | Detail |
|---|---|
| **Formula** | $\text{PEG} = P/E_{TTM} / g$ where $g$ = expected 3–5 yr EPS growth % (e.g., 15% → use 15, not 0.15) |
| **What it measures** | P/E normalized for growth; a PEG < 1 suggests undervalued relative to growth |
| **Theoretical basis** | Lynch (1989): a "fairly valued" growth company has PEG ≈ 1 |
| **India ranges** | PEG < 1 = potentially undervalued; PEG 1–2 = neutral; PEG > 2 = expensive relative to growth |
| **Failure modes** | Growth estimates are subjective/unreliable; doesn't account for quality of growth or ROCE; works poorly for slow-growth value stocks |
| **NSE notes** | Screener.in supports PEG-based screens. No India-specific empirical studies validating PEG predictive power found. Treat as qualitative aid only. |

### 1.3 Price-to-Book (P/B)

| Attribute | Detail |
|---|---|
| **Formula** | $P/B = \text{Market Cap} / \text{Book Value of Equity}$ |
| **Book value** | Total assets minus total liabilities minus intangibles (or as reported) |
| **What it measures** | Premium/discount to net assets; proxy for market's expectation of future ROE vs. cost of equity |
| **Theory** | Fama-French (1992) value factor; low P/B historically earns a premium. For banks, use **P/ABV** (Price / Adjusted Book Value) where ABV = Book Value − Net NPA |
| **India ranges** | Nifty 50 long-run range: 2.5–5x. P/B < 1.0 for non-banks is a deep-value signal. Banking sector fair value: 1–2.5x P/ABV depending on ROE, NPA cycle |
| **Failure modes** | (1) Asset-heavy vs. asset-light companies not comparable. (2) Banks: gross book includes NPAs — use P/ABV. (3) Tech/services: book value is mostly intangibles or near-zero, so P/B > 10x is normal. (4) Buybacks reduce book value, artificially inflating P/B. |
| **NSE evidence** | Emerald Insight (2020): "Is value premium sector-specific? Evidence from India" — value premium (low P/B) is statistically significant within sectors but not uniformly across sectors. [Link](https://www.emerald.com/insight/content/doi/10.1108/mf-02-2020-0049/full/html) |

### 1.4 Price-to-Sales (P/S)

| Attribute | Detail |
|---|---|
| **Formula** | $P/S = \text{Market Cap} / \text{Revenue}_{TTM}$ |
| **What it measures** | Valuation relative to top-line; useful when earnings are depressed or negative |
| **India ranges** | Consumer/FMCG: 3–8x; IT services: 3–6x; Auto: 0.5–1.5x; Pharma: 2–5x |
| **Failure modes** | Ignores profitability — a high-revenue, low-margin business and a high-margin business at same P/S are very different. High P/S with shrinking margins = red flag. |
| **NSE notes** | Used in Nifty500 Value 50 index composition (Sales to Price is one of four factors) alongside E/P, B/P, and dividend yield. [NSE Value 50 methodology](https://archives.nseindia.com/content/indices/NIFTY_Multi-Factor_Indices_whitepaper.pdf) |

### 1.5 EV/EBITDA and EV/EBIT

| Attribute | Detail |
|---|---|
| **EV formula** | $\text{EV} = \text{Market Cap} + \text{Net Debt} + \text{Minority Interest} + \text{Preferred Stock}$ |
| **EV/EBITDA** | $\text{EV/EBITDA} = \text{EV} / \text{EBITDA}_{TTM}$ |
| **EV/EBIT** | $\text{EV/EBIT} = \text{EV} / \text{EBIT}_{TTM}$ (more conservative — reflects depreciation) |
| **Advantage over P/E** | Capital-structure neutral; comparable across companies with different leverage |
| **India ranges** | 8–12x is "reasonable" for most Indian sectors; below 6x may indicate undervaluation; above 15x reflects growth premium ([Business Standard](https://www.business-standard.com/article/markets/when-should-you-use-ev-ebitda-as-an-alternative-to-p-e-ratio-here-s-a-tip-119031200362_1.html)) |
| **Sector preference** | Cyclicals (metals, cement, chemicals): EV/EBITDA preferred over P/E. Greenblatt's Magic Formula uses a version of Earnings Yield = EBIT/EV. |
| **Failure modes** | (1) Does not account for CapEx intensity — use EV/EBIT or EV/FCF for capex-heavy sectors. (2) Negative EBITDA: undefined. (3) Working-capital swings distort EBITDA for some retailers. |

### 1.6 FCF Yield and FCFE Yield

| Attribute | Detail |
|---|---|
| **FCF Yield** | $\text{FCF Yield} = \text{FCF} / \text{Market Cap}$ where FCF = Operating Cash Flow − CapEx |
| **FCFE** | $\text{FCFE} = \text{Net Income} + \text{D\&A} - \Delta \text{NWC} - \text{CapEx} + \text{Net Borrowing}$ |
| **FCFE Yield** | $\text{FCFE Yield} = \text{FCFE} / \text{Market Cap}$ |
| **What it measures** | True earnings yield stripped of accounting accruals; FCF yield > risk-free rate + spread is a buying signal |
| **India usage** | Marcellus Consistent Compounders filter FCF CAGR ~25% over 5–10 years. Coffee-Can uses FCF/Net Income > 1 as quality signal. [Marcellus FCF article](https://marcellus.in/newsletter/consistent-compounders/the-path-to-consistent-compounding-is-paved-with-free-cashflow/) |
| **Failure modes** | Lumpy CapEx (infrastructure, pharma R&D) distorts single-year FCF. Use 3-year average FCF. |

### 1.7 Dividend Yield and Payout Ratio

| Attribute | Detail |
|---|---|
| **Dividend Yield** | $\text{DY} = \text{DPS} / \text{Price}$ |
| **Payout Ratio** | $\text{Payout} = \text{DPS} / \text{EPS}$ |
| **India context** | Post-2020 Budget, dividends are taxed at investor's slab rate (previously DDT at ~20%). This reduces dividend appeal for high-tax-bracket investors vs. buybacks. |
| **NSE notes** | Dividend yield is one of the four Nifty500 Value 50 composition factors. PSU companies often have mandated high payouts (SEBI's 2021 rules). |

### 1.8 Earnings Yield (Greenblatt variant)

| Attribute | Detail |
|---|---|
| **Formula** | $\text{Earnings Yield} = \text{EBIT} / \text{EV}$ (inverse of EV/EBIT; used in Magic Formula) |
| **Intuition** | Measure how much pre-interest, pre-tax operating profit you're buying per rupee of enterprise value |
| **NSE notes** | Used in Magic Formula backtests (see Bucket 4). Directly comparable across capital structures. |

---

## Bucket 2 — Profitability and Quality Ratios

### 2.1 ROE, ROCE, ROIC — Indian Balance Sheet Nuances

**ROE (Return on Equity)**  
$$\text{ROE} = \text{Net Profit} / \text{Average Shareholders' Equity}$$

**ROCE (Return on Capital Employed)**  
$$\text{ROCE} = \text{EBIT} / \text{Capital Employed}$$  
where Capital Employed = Total Assets − Current Liabilities = Fixed Assets + Net Working Capital.

**ROIC (Return on Invested Capital)**  
$$\text{ROIC} = \text{NOPAT} / \text{Invested Capital}$$  
where NOPAT = EBIT × (1 − tax rate) and Invested Capital = Net Debt + Equity (or Total Assets − Non-interest-bearing current liabilities − Excess cash).

**Key differences on Indian books:**

| Issue | Impact |
|---|---|
| **Consolidated vs. Standalone** | Subsidiaries included in consolidated; parent-only in standalone. ROCE from consolidated is more relevant for conglomerates (e.g., Reliance, Tata group). Screener.in auto-picks the "more representative" set, but this heuristic can mislead. |
| **Excess cash treatment** | Holding companies or profitable companies (e.g., TCS) carry large cash piles. ROIC should subtract excess cash from invested capital; ROCE does not — ROIC is the more precise measure for companies with large cash. |
| **Investments in associates** | Indian holding companies (e.g., Bajaj Holdings, Chola) have large listed equity investments. These inflate equity but generate investment income, not operating income. ROE is thus depressed relative to operating ROCE. |
| **ROCE is pre-tax; ROIC is post-tax** | For cross-sector comparison, ROIC is cleaner. Greenblatt explicitly uses after-tax ROIC (net fixed assets + NWC as denominator). |

**Coffee-Can and Marcellus use ROCE (pre-tax)** as the primary filter — Mukherjea specifies ROCE ≥ 15% explicitly.

### 2.2 Margin Ratios

| Ratio | Formula | Notes |
|---|---|---|
| Gross Margin | (Revenue − COGS) / Revenue | Measures pricing power + input cost management |
| EBITDA Margin | EBITDA / Revenue | Industry comparisons; strips out financing + depreciation |
| Operating Margin | EBIT / Revenue | Most common; affected by depreciation method |
| Net Margin | Net Profit / Revenue | Bottom-line; affected by tax rate, leverage |

Indian FMCG companies (HUL, Dabur, Marico) typically maintain 15–20% EBITDA margins. IT services (TCS, Infosys): 20–25%. Metals and commodities: 5–15% at mid-cycle. Banking sector: margin concept replaced by NIM (Net Interest Margin).

### 2.3 Asset Turnover

$$\text{Asset Turnover} = \text{Revenue} / \text{Average Total Assets}$$

High turnover + low margin = retailer model (D-Mart: AT ~2.5x, net margin ~5%). Low turnover + high margin = capital goods (L&T AT ~0.5x, net margin ~7%).

### 2.4 DuPont — Sustainable Growth Rate

**3-factor DuPont:**  
$$\text{ROE} = \underbrace{\text{Net Margin}}_{\text{Profitability}} \times \underbrace{\text{Asset Turnover}}_{\text{Efficiency}} \times \underbrace{\text{Equity Multiplier}}_{\text{Leverage}}$$

**Sustainable Growth Rate (Higgins, 1977):**  
$$g^* = \text{ROE} \times (1 - \text{Payout Ratio})$$

This is the growth rate a firm can achieve without issuing new equity or changing leverage. NSE application: companies sustaining growth above $g^*$ must either dilute equity, raise debt, or compress margins — all three are warning signals.

### 2.5 FCF / Net Income (Quality of Earnings)

$$\text{Cash Conversion} = \text{Operating Cash Flow} / \text{Net Income}$$

- Ratio > 1.0 = earnings backed by cash (good quality).
- Ratio < 0.5 consistently = earnings heavily accrual-driven (risk flag).
- Marcellus uses this filter in CCP stock selection. Mukherjea (2018, *Coffee Can Investing*, Chapter 4) explicitly discusses FCF quality as a criterion for long-hold candidates.

### 2.6 Accruals Ratio (Sloan 1996)

$$\text{Accruals Ratio} = \frac{\Delta\text{Net Operating Assets}}{\text{Average Total Assets}}$$  
where $\Delta \text{Net Operating Assets} = \Delta\text{Total Assets} - \Delta\text{Cash} - \Delta\text{Total Liabilities} + \Delta\text{Short-term Debt} + \Delta\text{Long-term Debt}$

Or equivalently (balance-sheet version): $(\text{BS accruals}) = \frac{\text{Net Income} - \text{Operating CF}}{\text{Average Total Assets}}$

Sloan (1996) found that high accruals predict negative future returns; this pattern is documented in many markets. Indian evidence: Accruals study on NSE 100 via *Asian Journal of Finance & Accounting* (2019) found that recovering firms showed significant accrual-based earnings management during 2007 and 2012 recessions. [AJFA link](https://ajfa.macrothink.org/index.php/ajfa/article/download/14839/11747)

**Interpretation:** Accruals ratio > 0.08 is elevated; > 0.15 is a strong quality-of-earnings red flag. Combine with Beneish M-Score for earnings manipulation screening.

---

## Bucket 3 — Leverage and Solvency

### 3.1 Key Leverage Ratios

| Ratio | Formula | Healthy Range (India) | Failure Modes |
|---|---|---|---|
| D/E | Total Debt / Equity | < 1.0x for most sectors; NBFCs/banks by nature different | Doesn't account for off-balance-sheet items; lease liabilities post-IndAS 116 |
| Debt/EBITDA | Net Debt / EBITDA | < 3.0x generally; < 2.0x for high-quality | EBITDA overstates cash if working capital is deteriorating |
| Net Debt/EBITDA | (Debt − Cash) / EBITDA | < 2.0x preferred | Cash may be restricted; holding company cash vs operating cash confusion |
| Interest Coverage | EBIT / Interest Expense | ≥ 3.0x preferred; ≥ 1.5x minimum; 5.64x India average in 2023 | One-time EBIT items; lease interest not always in EBIT |
| FCF / Interest | Operating FCF / Interest | > 2.0x for safety | Capex timing distortions |

Indian ICR average rose to 5.64x in 2023, reflecting post-COVID deleveraging among large NSE-listed firms. ([Goodwill's Blog](https://www.gwcindia.in/blog/what-does-the-interest-coverage-ratio-reveal-about-the-financial-stability-of-indian-companies/))

### 3.2 Liquidity Ratios

| Ratio | Formula | Healthy Range |
|---|---|---|
| Current Ratio | Current Assets / Current Liabilities | 1.5–3.0x; Graham minimum: 2.0x |
| Quick Ratio | (Current Assets − Inventory) / Current Liabilities | > 1.0x |

Graham's defensive criterion requires current ratio ≥ 2.0x — this filters out many Indian companies in asset-heavy sectors.

### 3.3 Cash Conversion Cycle (CCC)

$$\text{CCC} = \text{DIO} + \text{DSO} - \text{DPO}$$

where DIO = Days Inventory Outstanding = (Inventory/COGS) × 365; DSO = Days Sales Outstanding = (Receivables/Revenue) × 365; DPO = Days Payable Outstanding = (Payables/COGS) × 365.

**Indian sector norms:**
- FMCG (HUL): CCC can be negative (strong bargaining power with suppliers; fast-moving inventory).
- Manufacturing/Industrials: CCC typically 60–120 days.
- Capital Goods (L&T, BEL): CCC can extend to 150–250 days due to long project cycles.
- IT Services: Very short CCC (receivables are main working capital item); typically 20–45 days.

Deteriorating CCC (increasing over time) + stable margins = potential channel-stuffing or receivables manipulation risk. Cross-check with Beneish DSRI component.

---

## Bucket 4 — Value Investing Frameworks

### 4.1 Graham Defensive Investor — 7 Criteria

Source: Benjamin Graham, *The Intelligent Investor*, Chapter 14 (Harper & Row, 1973 rev. ed.)

| # | Criterion | Exact Rule |
|---|---|---|
| 1 | Adequate size | Exclude companies below Graham's "adequate size" threshold; for Indian context, ≥₹500 Cr market cap is a reasonable adaptation |
| 2 | Financial condition | Current ratio ≥ 2.0x; Long-term debt ≤ Net Working Capital |
| 3 | Earnings stability | Positive EPS for each of the last 10 years (no loss-making year) |
| 4 | Dividend record | Uninterrupted dividend payments for at least 20 years |
| 5 | Earnings growth | EPS 10-yr growth ≥ 33% (using 3-year average at start and end) |
| 6 | Moderate P/E | Current P/E ≤ 15x on 3-year average EPS |
| 7 | Moderate P/B | Current P/B ≤ 1.5x OR P/E × P/B ≤ 22.5 |

**NSE applicability:** Criteria 4 (20-year dividend) eliminates virtually all mid/small-caps and most large-caps on NSE (Indian dividend cultures are inconsistent). Criteria 3 (10-year positive EPS) and criteria 2 (current ratio ≥ 2.0) together create a very small NSE universe. [GrahamValue NSE page](https://www.grahamvalue.com/stock/hdfcbankns) applies these screens to NSE stocks.

### 4.2 Graham Number

$$\text{Graham Number} = \sqrt{22.5 \times \text{EPS} \times \text{Book Value per Share}}$$

This represents the maximum price a defensive investor should pay (derived from P/E ≤ 15 and P/B ≤ 1.5 → product ≤ 22.5). At current India valuations, very few NIFTY 500 stocks trade below their Graham Number.

### 4.3 NCAV (Net-Net Stocks)

$$\text{NCAV} = \text{Current Assets} - \text{Total Liabilities}$$

Graham required buying at ≤ 67% of NCAV. On NSE, NCAV stocks exist primarily among micro-caps and PSUs with large cash/investment holdings relative to liabilities. Applicability is limited for the NIFTY 500 universe. GrahamValue.com confirms IEX.NS passes NCAV criteria; most large-caps do not. **Verdict: too narrow for NIFTY 500 scope; note as a special situations screen only.**

### 4.4 Greenblatt's Magic Formula

Source: Joel Greenblatt, *The Little Book That Beats the Market* (2005)

**Two factors, two ranks, combined:**
- **Factor 1 — Earnings Yield:** $\text{EY} = \text{EBIT} / \text{EV}$ (rank all stocks high → low)
- **Factor 2 — ROIC:** $\text{ROIC} = \text{EBIT} / (\text{Net Fixed Assets} + \text{Net Working Capital})$ (rank all stocks high → low)
- **Combined rank** = sum of EY rank + ROIC rank; buy top 30 stocks annually

**NSE Evidence:**

| Study | Period | Finding |
|---|---|---|
| Simmar Preet et al. (SSRN 3945468) | India, backtested | Magic Formula "pretty astonishing" pre-2012 |
| FinancialTales blog | 2012–2020 | BSE Sensex +99.8%; Magic Formula ~1% CAGR — severe underperformance |
| BacktestIndia.com | 18-yr NSE | Value-Quality (low P/E + high ROE) 11.38% net CAGR; 1.59% excess over index |

**Verdict:** Pre-2012 Indian evidence is positive. Post-2012 evidence suggests the formula may not survive transaction costs, liquidity constraints in small-caps, and changing market structure. [SSRN paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3945468) | [FinancialTales India](https://financialtales.home.blog/2020/05/04/joel-greenblatts-magic-formula-in-the-indian-context-does-it-work/)

### 4.5 Piotroski F-Score — Exact Construction

Source: Piotroski, J.D. (2000). *Value Investing: The Use of Historical Financial Statement Information to Separate Winners from Losers.* Journal of Accounting Research, 38(Suppl.), 1–41.

**Nine binary tests (1 = pass, 0 = fail):**

**Group A — Profitability (4 signals):**
| Signal | Test | Condition |
|---|---|---|
| F_ROA | ROA positive | Net Income / Beginning Total Assets > 0 |
| F_ΔROA | ROA improving | ROA this year > ROA last year |
| F_CFO | Cash flow positive | Operating CF / Beginning Total Assets > 0 |
| F_ACCRUAL | Earnings quality | CFO > ROA (i.e., cash earnings > accrual earnings) |

**Group B — Leverage, Liquidity, Source of Funds (3 signals):**
| Signal | Test | Condition |
|---|---|---|
| F_ΔLEVER | Leverage decreasing | Long-term Debt/Avg. Assets ratio fell YoY |
| F_ΔLIQUID | Liquidity improving | Current ratio improved YoY |
| EQ_OFFER | No dilution | No new shares issued in the past year |

**Group C — Operating Efficiency (2 signals):**
| Signal | Test | Condition |
|---|---|---|
| F_ΔMARGIN | Gross margin improving | Gross margin this year > last year |
| F_ΔTURN | Asset turnover improving | Revenue/Assets this year > last year |

**F-Score = sum of all 9 signals.** Range 0–9. Score ≥ 8 = strong; score ≤ 2 = weak.

**NSE Evidence:**
- [Communications on Applied Nonlinear Analysis (2024)](https://internationalpubls.com/index.php/cana/article/view/6028): Nifty 100, 2007–2024. High-F-score firms delivered stronger returns and provided downside cushion. Most rigorous recent India replication.
- [ResearchGate (IJEF)](https://www.researchgate.net/publication/312397957_Effect_of_F_Score_on_Stock_Performance_Evidence_from_Indian_Equity_Market): NSE top-500 by market cap; F-score shifts stock performance favorably. Finding consistent with US evidence.
- [Cement sector study](https://www.researchgate.net/publication/340455126_IMPACT_OF_PIOTROSKI_SCORE_ON_PE_RATIO_A_STUDY_ON_INDIAN_CEMENT_SECTOR): F-Score negatively correlated with P/E (high F-score → lower P/E = relatively cheap quality stocks).

**Verdict: Best-evidenced single quantitative framework for NSE among all four multi-factor models surveyed.**

### 4.6 Altman Z-Score — Three Variants

**Original (Public Manufacturing, 1968):**
$$Z = 1.2 X_1 + 1.4 X_2 + 3.3 X_3 + 0.6 X_4 + 1.0 X_5$$

where $X_1$ = WC/TA, $X_2$ = RE/TA, $X_3$ = EBIT/TA, $X_4$ = Market Equity/Total Liabilities, $X_5$ = Sales/TA.  
Zones: Safe Z > 2.99; Grey 1.81–2.99; Distress Z < 1.81.

**Z' (Private companies — replaces market equity with book equity in X4):**
$$Z' = 0.717 X_1 + 0.847 X_2 + 3.107 X_3 + 0.420 X_4' + 0.998 X_5$$
Zones: Safe > 2.9; Grey 1.23–2.9; Distress < 1.23.

**Z'' (Emerging Market / Services — correct for India):**
$$Z'' = 6.56 X_1 + 3.26 X_2 + 6.72 X_3 + 1.05 X_4' + 3.25$$
$X_4'$ uses book value of equity. Zones: Safe > 2.6; Grey 1.1–2.6; Distress < 1.1. ([CreditGuru Z'' reference](https://www.creditguru.com/index.php/bankruptcy-and-insolvency/altman-z-score-insolvency-predictor-for-non-manufacturers-emerging-markets))

**NSE Evidence:** DOAJ study on NSE-listed companies confirms moderate-to-strong predictive power; limitations noted for SMEs and family-owned businesses. [DOAJ article](https://doaj.org/article/cb2a512b9ceb4953895eba3099a96f94) | [NSE logistics study](https://indianjournalofcapitalmarkets.com/index.php/ijrcm/article/view/173826)

**Note:** Z'' drops the Sales/TA term (X5) to reduce industry bias; the +3.25 constant aligns scale with US credit ratings.

### 4.7 Beneish M-Score — Earnings Manipulation Detection

Source: Beneish, M.D. (1999). *The Detection of Earnings Manipulation.* Financial Analysts Journal, 55(5), 24–36.

**8-variable model:**
$$M = -4.84 + 0.92 \cdot \text{DSRI} + 0.528 \cdot \text{GMI} + 0.404 \cdot \text{AQI} + 0.892 \cdot \text{SGI} + 0.115 \cdot \text{DEPI} - 0.172 \cdot \text{SGAI} + 4.679 \cdot \text{TATA} - 0.327 \cdot \text{LVGI}$$

| Variable | Description | Formula |
|---|---|---|
| DSRI | Days Sales Receivables Index | (Receivables/Revenue)_t / (Receivables/Revenue)_{t-1} |
| GMI | Gross Margin Index | Gross Margin_{t-1} / Gross Margin_t |
| AQI | Asset Quality Index | (1 − (CA + PPE)/TA)_t / (1 − (CA + PPE)/TA)_{t-1} |
| SGI | Sales Growth Index | Revenue_t / Revenue_{t-1} |
| DEPI | Depreciation Index | (Dep/(Dep+PPE))_{t-1} / (Dep/(Dep+PPE))_t |
| SGAI | SGA Expense Index | (SGA/Revenue)_t / (SGA/Revenue)_{t-1} |
| TATA | Total Accruals to Total Assets | (Net Income − OCF) / Total Assets |
| LVGI | Leverage Index | (LTD+Current Liab)/TA)_t / same_{t-1} |

**Threshold:** M > -1.78 → likely manipulator. M < -2.22 → likely non-manipulator.

**NSE Evidence:** Indian Journal of Finance (Shah, 2018): BSE 100 companies — M-Score effective at flagging irregularities in financial reporting. 9 of 28 sample industries susceptible. Telecom and construction showed highest signals. [Indian Journal of Finance](https://www.indianjournaloffinance.co.in/index.php/IJF/article/view/122796) | Telecom case study: [Ignited Journal](https://ignited.in/index.php/jasrae/article/view/7131/14064)

---

## Bucket 5 — Quality / Compounder Frameworks (India-Relevant)

### 5.1 Saurabh Mukherjea's Coffee-Can Criteria

Source: Mukherjea, S., Ranjan, R., & Uniyal, P. (2018). *Coffee Can Investing: The Low-Risk Road to Stupendous Wealth.* Portfolio Penguin.

**Large-Cap/General Criteria (stated explicitly in Chapter 2 and Chapter 4):**
- Revenue growth ≥ 10% year-on-year **for each of the last 10 consecutive years**
- ROCE (pre-tax) ≥ 15% **for each of the last 10 consecutive years**
- Minimum market cap ≥ ₹100 Crore (for data reliability)
- Hold for minimum 10 years ("invest and forget")

**Financial Services Sector Carve-out (banks, NBFCs):**
- Loan/Asset book growth ≥ 15% per year for each of the last 10 years
- ROE ≥ 15% per year for each of the last 10 years
- (ROCE is replaced by ROE because banks operate with leverage by design)

**Sources:** [Safalinvesting summary](https://safalinvesting.com/coffee-can-investing-saurabh-mukherjea/) | [Screener.in Coffee-Can screen](https://www.screener.in/screens/57601/coffee-can-portfolio/) | [Profile Traders review](https://www.profiletraders.in/post/coffee-can-investing-by-saurabh-mukherjea-book-review-profile-traders) | [Equitymaster small-cap application (2025)](https://www.equitymaster.com/detail.asp?date=03/04/2025&story=2&title=5-Smallcap-Stocks-Matching-Saurabh-Mukherjeas-Coffee-Can-Portfolio-Criteria)

**Mid-cap / Little Champs (Marcellus PMS product):** The Little Champs strategy targets small-caps (market cap < ~₹3,500 Cr / US$500M) and focuses on the same ROCE + revenue growth criteria with corporate governance screening. The specific amended thresholds are not publicly disclosed in the PMS presentation materials — the qualitative governance overlay (clean promoter history, low related-party transactions, DSRA/pledging review) becomes more prominent at smaller caps. [Little Champs PMS](https://marcellus.in/wp-content/uploads/2023/03/Marcellus_Little_Champs_presentation_Regular-.pdf)

**Why it works (Mukherjea's thesis):** Only 25–30 listed Indian companies pass the 10-year dual filter at any given time. This concentration reflects durable moats. 10-year holding amplifies compounding and taxes are deferred. The empirical claim is that this filter has produced ~23% CAGR historically vs Sensex ~12–15%.

### 5.2 Marcellus Consistent Compounders (CCP)

The CCP goes beyond Coffee-Can in two ways:

1. **Investable universe of 25–30 stocks** from Coffee-Can filter, then narrow to 10–20 via bottom-up research on competitive moats.
2. **FCF quality requirement**: Portfolio companies must exhibit FCF CAGR of ~25% sustained over 5–10 years. This adds a cash-flow-quality dimension absent from the basic Coffee-Can screen.

Key philosophy: "Firms with high pricing power sustain a wide gap between ROCE and cost of equity." [Marcellus CCP philosophy](https://marcellus.in/portfolio-management-services/marcellus-consistent-compounder-pms/) | [FCF compounding newsletter](https://marcellus.in/newsletter/consistent-compounders/ccp-25-free-cashflow-cagr-25-share-price-compounding/)

### 5.3 MSCI Quality Factor — Formal Definition

Source: MSCI Quality Indices Methodology (May 2013, updated June 2014). [MSCI methodology PDF](https://www.msci.com/eqb/methodology/meth_docs/MSCI_Quality_Indices_Methodology.pdf)

**Three fundamental variables:**
1. **ROE** (Return on Equity) — high is good; positive Z-score.
2. **D/E** (Debt-to-Equity) — low is good; negative Z-score computed so lower D/E → higher score.
3. **EVAR** (Earnings Variability) — low is good; measured as std dev of 5-year EPS; negative Z-score.

**Calculation:**
- Each variable is winsorized (cap outliers at 3 std devs).
- Compute Z-score: $z_i = (x_i - \mu) / \sigma$
- Composite Quality Z-Score = simple average of the three Z-scores.
- Tilt: stocks with higher composite Z-score get higher index weight.

**NSE multi-factor usage:** NSE Nifty Quality 30, Nifty Midcap 150 Quality 50, Nifty Alpha Quality Low-Volatility 30 all use Quality as a factor. The Alpha-Quality-Low-Volatility 30 index outperformed NIFTY 50 by 5.22% CAGR since April 2005. [NSE strategy index](https://www.niftyindices.com/indices/equity/strategy-indices/nifty-alpha-quality-value-low-volatility-30) | [Capitalmind analysis](https://www.capitalmind.in/blog/nse-strategy-indices-factor-investing-basics)

### 5.4 Indian Fund Manager Criteria

**Raamdeo Agrawal (Motilal Oswal) — QGLP**

Source: *The QGLP Checklist: 25 Questions, 25 Frameworks* (Motilal Oswal 25th Annual Wealth Creation Study, 2021). MOSL has published the Wealth Creation Study annually since 1996. [MOSL Wealth Creation Study](https://www.motilaloswal.com/wealth-creation-study)

- **Q — Quality of Business and Management:** High ROE, pricing power, brand, earnings consistency, honest promoters.
- **G — Growth:** 15–20%+ EPS CAGR expected, industry tailwinds.
- **L — Longevity:** Runway of 10+ years for continued growth; no secular decline risk.
- **P — Price:** Buy at a reasonable P/E relative to growth (PEG discipline); "Price comes last" in the evaluation sequence.

All four factors are multiplicative: any zero nullifies the entire evaluation. [Value Research interview](https://www.valueresearchonline.com/stories/225104/price-comes-last-qglp-raamdeo-agrawal-motilal-oswal-interview/)

**Vijay Kedia — SMiLE Framework**

Source: [Value Research](https://www.valueresearchonline.com/stories/54019/how-to-invest-like-vijay-kedia/)

- **S** — Small in size (targets market cap < ₹1,000 Cr, ignored by institutions)
- **M** — Medium in experience (few years of proven operations; not startup)
- **i** — Large in aspiration (management with an ambitious but credible vision)
- **L** — Extra-Large in market potential (industry must have decade-long runway)

Kedia also applies his own version of QGLP and emphasizes management quality ("bet on the jockey"). His iconic multi-baggers (Atul Auto, Cera Sanitaryware) validated the small-cap + management quality + market potential combination.

**Sanjoy Bhattacharyya (Fortuna Capital)**

Source: [Morningstar India profile](https://www.morningstar.in/posts/60673/6-stock-investing-insights-sanjoy-bhattacharyya.aspx) | [FLAME University presentation (2024)](https://www.flame.edu.in/pdfs/fil/presentations/A-Credo-for-Value-Investing-Sanjoy-Bhattacharyya-FIL-With-The-Masters-June2024.pdf)

Criteria: EPS CAGR > 15% over the last decade; current P/E not exceeding the normalized P/E trading band for the last 5 years. Concentrated portfolio. Former CIO of HDFC AMC. Early investor in Asian Paints, Infosys, HDFC, Kotak.

**Mohnish Pabrai (Dhandho/India exposure)**

Source: Pabrai, M. (2007). *The Dhandho Investor.* Wiley. [Stockinvestoriq profile](https://stockinvestoriq.com/mohnish-pabrai/)

Pabrai's framework is a cloning + value investing hybrid (not NSE-specific). His India holdings are through Indian-listed ADRs or direct NSE stocks, not a systematic India screen. Core principles: margin of safety, circle of competence, distressed businesses in distressed industries. **No published quantitative NSE-specific criteria from Pabrai.** His fund has produced 781% net returns since 2000 vs S&P 378%, but this is primarily US-focused.

**Buffett/Munger criteria on NSE:** No peer-reviewed empirical study demonstrates that a quantitative Buffett-style moat screen (e.g., 10-yr ROE > 15% + D/E < 0.5 + brand value proxy) produces statistically significant alpha on NSE after 2010. Qualitative moat identification is widely discussed in Indian investment writing but lacks the same quantitative replication as Piotroski or Coffee-Can. **Verdict per Pranav's direction: excluded from v0.1 for lack of NSE-validated evidence.**

---

## Bucket 6 — Sector-Relative Computation

### 6.1 NSE vs. GICS Classification

| Dimension | NSE Indices System | GICS (MSCI/S&P) |
|---|---|---|
| Developer | NSE Indices Ltd. (since Nov 2022, both NSE and BSE use this) | MSCI + S&P Global, 1999 |
| Structure | 4 tiers: 12 Macro-Economic Sectors / 22 Sectors / 59 Industries / 197 Basic Industries | 4 tiers: 11 Sectors / 25 Industry Groups / 74 Industries / 163 Sub-Industries |
| Classification basis | Revenue > 50% from primary segment | Revenue + assets + market perception |
| Indian specificity | Higher: includes "Financial Services" macro-sector, "PSU" overlays, sector-specific indices | Lower: designed globally |

[NSE Industry Classification July 2023](https://www.niftyindices.com/docs/default-source/default-document-library/nse-indices_industry-classification-guideline-2023-07.pdf) | [NSE classification guidelines page](https://www.niftyindices.com/resources/industry-classification)

For FA purposes, **NSE's own classification is preferred** for Indian sector percentile calculations because screener platforms (Screener.in, Trendlyne) use it natively.

### 6.2 Percentile Rank Math — Exact Computation

Given a set of $N$ companies in a sector for ratio $r$, the percentile rank of company $i$ is:

$$\text{Percentile Rank}_i = \frac{\text{rank}(r_i) - 1}{N - 1} \times 100$$

where rank() is ascending for metrics where higher is better (ROE, ROCE, FCF yield, etc.) and descending for metrics where lower is better (P/E, P/B, D/E). This is the "exclusive" percentile formula — it produces 0 for the lowest and 100 for the highest.

**Implementation notes:**
1. **Handle ties**: Use average rank (e.g., two companies tied for rank 3 and 4 both get rank 3.5).
2. **Direction**: For valuation ratios where lower = cheaper (P/E, EV/EBITDA), rank = descending so that a cheaper stock gets a higher percentile ("P/E percentile 80 = cheaper than 80% of sector peers"). This is non-obvious and must be convention-locked.
3. **Winsorize outliers**: Companies with extreme ratios (e.g., P/E of 500x post-loss reversal) distort ranks. Cap at 3× IQR above 75th percentile before ranking.

### 6.3 Worked Example: HDFC Bank ROE Percentile in Private Banking Sector

**Setup (illustrative data for methodology, not live numbers):**

Private Banking sector on NSE = {HDFC Bank, ICICI Bank, Kotak Mahindra, Axis Bank, IndusInd Bank, Federal Bank, IDFC First, Bandhan Bank, RBL Bank, Yes Bank} — 10 companies.

ROE values (hypothetical for example): 16%, 15%, 14%, 13%, 12%, 11%, 9%, 8%, 5%, 2%

HDFC Bank ROE = 16% → rank in ascending order = rank 10 (highest).

$$\text{Percentile} = \frac{10 - 1}{10 - 1} \times 100 = 100\text{th percentile}$$

If HDFC Bank ROE = 15% (same as ICICI, tied rank 9.5):

$$\text{Percentile} = \frac{9.5 - 1}{9} \times 100 = 94.4\text{th percentile}$$

**Interpretation:** "HDFC Bank's ROE is at the 94th percentile within the Private Banking sector" means it earns higher returns on equity than approximately 94% of sector peers.

### 6.4 Small-Sample Sector Problem

NSE has several sectors with < 10 listed companies (e.g., specialty chemicals sub-industries, defense, certain infrastructure niches). With N < 10:

- Each additional company changes ranks by >10 percentile points.
- Percentile rank becomes unreliable as a cross-company signal.
- **Recommendation:** For sectors with N < 10, report absolute ratio value and cross-sector absolute rank, not within-sector percentile. Or use a broader grouping (e.g., aggregate multiple sub-industries).

A practical floor: use sector percentile only when N ≥ 15. For N between 10 and 15, caveat prominently.

### 6.5 Sector-Specific Ratio Rules (Gotchas)

| Sector | Issue | Correct Approach |
|---|---|---|
| Banks / NBFCs | P/B inflated by NPAs; D/E meaningless (banking uses leverage by design) | Use P/ABV (Price / [Book − Net NPA]); use NIM, GNPA%, PCR, CAR |
| Commodity Cyclicals (steel, aluminum, cement) | P/E meaningless at cycle trough (near-zero or negative earnings) | Use EV/EBITDA on through-cycle normalized EBITDA; EV/tonne for capacity-based |
| Real Estate / Developers | Earnings lumpy (project completion accounting); book value is land bank | Use P/NAV: Price vs. Net Asset Value of land bank + projects |
| PSUs | Low ROCE due to government mandates (social pricing, dividend caps); P/B < 1 normal | Sector-within-PSU comparison; watch for dividend mandate distortions |
| IT Services | Asset-light; P/B > 10x normal; no debt | P/E, P/FCF, EV/Revenue more relevant; ROE very high due to low equity base |
| Pharma | Capex for R&D often expensed, understating PPE; one-time USFDA hits | Normalize EPS for one-time hits; use EV/EBITDA adjusted for R&D |

---

## Bucket 7 — NSE-Specific Empirical Evidence

### 7.1 Value Premium (P/E, P/B)

| Study | Finding | Notes |
|---|---|---|
| Saji & Harikumar (2015), *Vision (Sage)* | E/P and earnings growth are prime determinants of NSE IT sector returns 2000–2010 | Sector-limited; IT only |
| Emerald Insight (2020) | Value premium exists within sectors; P/B signal is sector-specific | India BSE/NSE combined sample |
| BacktestIndia.com | Low P/E + High ROE strategy: 11.38% net CAGR (18 years, NSE) vs index; excess return only 1.59% with 33% volatility | High vol undermines Sharpe; value-quality not a clean win |
| LSEG/FTSE (global incl. India) | Value factor has underperformed globally since 2007; Indian evidence suggests similar decay post-2016 | No India-specific decay study found with hard numbers |

**Verdict:** P/B and P/E value signals work on NSE but with lower alpha than pre-2010 and require quality filters (ROCE, FCF) to be viable.

### 7.2 Piotroski F-Score

**Strongest positive evidence** on NSE among all frameworks.

- [Communications on Applied Nonlinear Analysis (2024)](https://internationalpubls.com/index.php/cana/article/view/6028): Nifty 100, 2007–2024. High-F-score firms outperformed index and provided crash cushion.
- [IJEF / ResearchGate (2017)](https://www.researchgate.net/publication/312397957_Effect_of_F_Score_on_Stock_Performance_Evidence_from_Indian_Equity_Market): NSE top-500, F-score separates winners from losers consistent with Piotroski's original findings.
- [Freefincal application](https://freefincal.com/piotroski-score-stock-analysis/): Practical implementation notes for Indian investors.

**Verdict: Use on NSE is well-supported. Apply to Nifty 500 universe.**

### 7.3 Magic Formula (Greenblatt)

Mixed; net negative post-2012 on Indian data. See Bucket 4 table above. SSRN 3945468 is the most credible positive India study, but it predates 2012. Likely suffers from small-cap liquidity premium inflation in earlier periods.

**Verdict: Use with caution. Earnings Yield and ROIC as individual signals may be useful; the combined 30-stock portfolio approach lacks post-2015 India validation.**

### 7.4 Quality Factor / Factor Indices

NSE's own Nifty Quality 30 and Alpha-Quality-Low-Vol 30 indices demonstrate measurable outperformance:
- Alpha + Quality + Low-Vol 30: +5.22% CAGR over NIFTY 50 since April 2005.
- Nifty 200 Alpha 30: top-5 performer in 10-year returns across all NSE strategy indices.

[Capitalmind factor analysis](https://www.capitalmind.in/blog/nse-strategy-indices-factor-investing-basics)

**Verdict: Quality and momentum factors have the most consistent Indian index-level evidence. Value alone is noisier.**

### 7.5 Coffee-Can / Compounders

No academic replication study of Mukherjea's exact Coffee-Can screen was found. Marcellus' own CCP PMS has produced positive live returns since 2018 inception but (a) has a short live track record, (b) AUM effects matter, and (c) coincided with a broad India growth bull market. The underlying thesis (long ROCE + revenue consistency → compounding) has theoretical grounding in finance.

**Verdict: Framework is theoretically sound and heuristically validated in practice. No independent academic replication on NSE.**

### 7.6 Banking-Specific Ratios

Core banking valuation ratios (India context):
- **P/ABV** = Price / (Book Value − Net NPA): corrects for stressed assets. HDFC Bank trades ~3–4x P/ABV; PSU banks ~0.5–1.5x P/ABV.
- **NIM** (Net Interest Margin): India bank average ~3%. Private banks: 3.5–4.5%; PSU banks: 2.5–3.2%.
- **GNPA%** (Gross Non-Performing Assets %): < 2% = healthy; 3–5% = watchlist; >5% = stressed.
- **PCR** (Provision Coverage Ratio): > 70% = adequate buffer against NPA losses.
- **CAR** (Capital Adequacy Ratio): Regulatory minimum 9% (RBI); well-capitalized = > 15%.

[Samco banking analysis guide](https://www.samco.in/knowledge-center/articles/analyse-banking-stocks/) | [Winvesta banking guide](https://www.winvesta.in/blog/investors/how-to-analyze-banking-stocks-key-metrics-and-ratios)

### 7.7 Altman Z-Score — NSE Evidence

[DOAJ NSE study](https://doaj.org/article/cb2a512b9ceb4953895eba3099a96f94) and [IJCRT](https://www.ijcrt.org/papers/IJCRT25A5743.pdf) confirm Z'' model has moderate-to-strong predictive power for NSE large-caps. Limitations: under-performs for SMEs, family-owned firms, and sectors with non-standard asset structures (IT, financial services).

### 7.8 Beneish M-Score — NSE Evidence

[Indian Journal of Finance (Shah, 2018)](https://www.indianjournaloffinance.co.in/index.php/IJF/article/view/122796): M-Score applied to BSE 100 + S&P BSE MidSmallCap (2013–2019); effective early-warning tool. 9 of 28 industries susceptible.

### 7.9 Promoter Pledge and Related-Party Risks

Not a "ratio" in the classical sense but a material India-specific risk overlay:
- High promoter pledge % (>50% of holding pledged) correlates with forced liquidation risk.
- NSE publishes quarterly pledged shares data. [NSE pledging data](https://www.nseindia.com/companies-listing/corporate-filings-pledged-data)
- Related-party transaction threshold in India: >10% of net worth or ₹1,000 Cr requires shareholder approval. US threshold is 5%+.
- PSU governance distortions: Government-mandated dividends, cross-subsidized pricing (BPCL, HPCL on petrol/diesel historically), board appointments by Ministry — all distort ROCE and ROE comparability.

---

## Bucket 8 — Data Sources and Quality

| Source | What's Available | Free vs. Paid | Data Quality Issues |
|---|---|---|---|
| **Screener.in** | 10+ yr P&L, Balance Sheet, Cash Flow, 50+ ratios, quarterly results, custom formula screening, 5,000+ stocks | Free (basic); ₹10,000/yr Pro (export, portfolio) | Auto-picks consolidated vs standalone — may mismatch for specific analyses. Restated financials sometimes not backfilled. Screener.in's own note: picks "more representative" set heuristically. |
| **Tickertape** | Stocks + MFs + ETFs, 100+ metrics, Investment Scorecard, screener | Free (3 custom filters); Pro removes limit | Historical depth shallower than Screener.in; data accuracy "under user scrutiny" per comparison reviews. |
| **Trendlyne** | 1,400+ (3,000+ premium) screener parameters, DVM score, backtesting, real-time updates during market hours | Tiered pricing | Most comprehensive screener parameter count; DVM is proprietary. Real-time is a significant advantage for intraday ratio tracking. |
| **Tijori Finance** | 6,000+ operational metrics: market share, revenue mix, store counts, supply chain — extracted from annual reports | Subscription | Best for qualitative-quantitative operational data not available elsewhere. Does NOT replace Screener.in for standard FA ratios. |
| **NSE / BSE XBRL** | All listed company financials in XBRL format; quarterly and annual filings | Free | Requires parsing; raw data quality depends on company compliance. Missing footnotes, restatements not always flagged. |
| **NSE Corporate Filings** | Quarterly results, shareholding patterns, pledging data, investor presentations | Free | HTML/PDF format; not structured for systematic use. |
| **MoneyControl** | News, peer comparison, analyst estimates, broker reports | Free (basic) | Analyst estimates are crowd-sourced from brokers — quality varies. Not suitable as primary data source for systematic screening. |
| **Prowess (CMIE)** | Deep historical financial data, 25+ yr history, economy and industry data | Institutional subscription (~₹50k+ /yr) | Highest quality; used in IIM/academic studies. Out of reach for individual investors. |
| **BSE XBRL Portal** | Machine-readable financials | Free | [BSE XBRL info](https://www.bseindia.com/static/about/xbrl_info.aspx) — standardized since 2011 but field mapping inconsistent across companies. |
| **Kite (Zerodha)** | Quote data, historical OHLCV, portfolio positions | With brokerage account | No FA data natively — requires combination with Screener.in/Trendlyne. |

**Consolidated vs. Standalone — the single largest data quality issue:** For conglomerates (Tata Motors, Reliance, Bajaj group), standalone numbers exclude subsidiary performance. Consolidated numbers include all subsidiaries but may include non-Indian revenue. Screener.in heuristically picks the "more representative" set, but this is not always correct for analysts who specifically want the Indian operating entity.

---

## Synthesis

### Well-evidenced for NSE (include in v0.1 candidate list)

| Signal | Evidence Quality |
|---|---|
| Piotroski F-Score | Strong — two independent India replications, Nifty 100 and Nifty 500, positive and consistent |
| Coffee-Can dual filter (ROCE ≥ 15% + Revenue growth ≥ 10%, 10-year) | Heuristically validated; theoretically sound; no independent academic replication but Marcellus live CCP shows positive returns |
| MSCI Quality composite (ROE + D/E + EVAR) | NSE own quality indices show +5.22% CAGR excess; methodologically rigorous |
| P/B within-sector percentile | Moderate India evidence; Emerald 2020 study confirms sector-specific value premium |
| Beneish M-Score (manipulation screen) | Positive India evidence (BSE 100 study); useful as a quality filter / fraud avoidance |
| Altman Z'' (distress screen) | Moderate India evidence; use as binary solvency gate, not as alpha signal |
| EV/EBITDA for cyclicals | No formal NSE backtest but well-accepted practitioner standard; sector-relative percentile meaningful |
| ROCE / ROE consistency (Coffee-Can) | Core to Mukherjea; MSCI quality; Nifty Quality 30 index — multiple corroborating evidences |

### Unproven or Contradicted on NSE

| Signal | Status |
|---|---|
| Greenblatt Magic Formula (combined 30-stock portfolio) | Contradicted post-2012; recommend against |
| NCAV net-net | Too narrow; NIFTY 500 universe has almost no NCAV stocks |
| Graham defensive 7 criteria (strict) | Too restrictive; eliminates most Indian companies (no 20-yr dividend records) |
| Buffett/Munger moat screen (quantitative) | No India empirical validation; excluded |
| PEG as standalone signal | No India empirical validation found |
| Value premium (P/E alone) | Mixed; decayed post-2016; requires quality overlay |

### Indian-Specific Gotchas Needing Carve-outs

1. **Banks**: Replace P/B with P/ABV; replace ROCE with ROE; add NIM, GNPA%, PCR, CAR.
2. **Commodity cyclicals**: Replace P/E with EV/EBITDA on normalized EBITDA; flag at cycle top and trough.
3. **Real estate**: Use P/NAV where available; note RERA compliance as a qualitative overlay.
4. **PSUs**: Flag government ownership %; treat ROCE with skepticism due to social mandates; watch dividend policy changes.
5. **Promoter-pledged shares**: >50% pledge = non-financial red flag; add to all-stock screener output.
6. **Consolidated vs. standalone**: Lock convention per stock; prefer consolidated for conglomerates.

---

## Open Questions Pranav Must Answer for A.2

1. **Scoring framework combination.** Which of these to use together in v0.1?
   - Option A: Piotroski F-Score as a binary gate (≥ 7 = pass) + MSCI Quality Z-Score ranking.
   - Option B: Coffee-Can dual filter (10-yr ROCE + revenue) as primary; Piotroski as secondary quality check.
   - Option C: Custom composite of ROCE percentile + FCF conversion + Beneish M-Score gate + Altman Z'' gate.
   - Option D: Just Piotroski (most evidence, simplest, NSE-validated) for v0.1; add others in v0.2.

2. **Trailing vs. forward estimates.** All ratios above are computable from trailing data (available). Forward P/E requires analyst estimates (noisy on NSE for mid/small caps). Proposed: trailing only for v0.1; forward added in v0.2 only for NIFTY 100 where analyst coverage is dense.

3. **Sector carve-outs in v0.1.** Banking carve-out (P/ABV, NIM, GNPA% substitution) is material and well-defined. Do we implement it in v0.1 or stub it out?
   - Option A: Full bank carve-out in v0.1 — separate ratio set for BFSI.
   - Option B: Flag BFSI stocks with a "not comparable — use banking-specific ratios" notice in v0.1; implement carve-out in v0.2.

4. **Sector-relative percentile floor.** For small-sample sectors (N < 15), what do we display?
   - Option A: Absolute ratio + note "sector too small for percentile."
   - Option B: Use broader sector grouping (e.g., merge Specialty Chemicals into overall Chemicals).

5. **Time-series window for Coffee-Can.** The strict 10-consecutive-year rule produces a very small universe. For a screening bot, do we want:
   - Option A: Strict 10-year consecutive (authentic Coffee-Can).
   - Option B: "8 of last 10 years" (more practical; less strict but catches most compounders).

6. **Manipulation/distress gates.** Run Beneish M-Score and Altman Z'' as pre-screen knockout gates (stocks failing these are excluded entirely), or as additive signals contributing to a composite score?

7. **Earnings quality inclusion.** Include FCF/Net Income (cash conversion) and Sloan Accruals Ratio in v0.1 as quality signals, or defer to v0.2?

8. **Promoter pledge as a signal.** Include promoter pledge % as a non-financial quality signal? Data is available on NSE; threshold is debatable (>30%? >50%?).

---

## Appendix — All Sources, Grouped by Topic

### Value Ratios and Premium
- [Value effect in Indian stock market: An empirical analysis (ResearchGate)](https://www.researchgate.net/publication/324075362_Value_effect_in_Indian_stock_market_An_empirical_analysis)
- [Earnings Growth and Value Premium: The Indian Experience — Saji & Harikumar (Sage/VISION, 2015)](https://journals.sagepub.com/doi/10.1177/0256090915608542)
- [Is value premium sector-specific? Evidence from India (Emerald, 2020)](https://www.emerald.com/insight/content/doi/10.1108/mf-02-2020-0049/full/html)
- [BacktestIndia.com — Value-Quality 18-yr NSE backtest](https://backtestindia.com/blog/value-quality-investing-india-backtest)
- [NSE Sector P/E Charts (Craytheon)](https://craytheon.com/charts/nse_sector_pe_chart.php)
- [NSE Nifty P/E, P/B & Dividend Yield Charts](https://craytheon.com/charts/nifty_pe_ratio_pb_value_dividend_yield_chart.php)

### Piotroski F-Score
- [Effect of F Score on Stock Performance: Evidence from Indian Equity Market (ResearchGate / IJEF)](https://www.researchgate.net/publication/312397957_Effect_of_F_Score_on_Stock_Performance_Evidence_from_Indian_Equity_Market)
- [Evaluating Piotroski F-Score Effectiveness — Nifty100 2007–2024 (Communications on Applied Nonlinear Analysis, 2024)](https://internationalpubls.com/index.php/cana/article/view/6028)
- [Impact of Piotroski Score on P/E: Indian Cement Sector (ResearchGate)](https://www.researchgate.net/publication/340455126_IMPACT_OF_PIOTROSKI_SCORE_ON_PE_RATIO_A_STUDY_ON_INDIAN_CEMENT_SECTOR)
- [Piotroski F-Score for Indian Private Banks (ResearchGate)](https://www.researchgate.net/publication/349638116_Using_Piotroski_F-Score_for_Assessing_Financial_Health_Evidence_from_Leading_Indian_Private_Banks)
- [Freefincal Piotroski practical application](https://freefincal.com/piotroski-score-stock-analysis/)

### Magic Formula
- [Back Testing Magic Formula on Indian Stock Markets (SSRN 3945468)](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3945468)
- [Magic Formula in the Indian context — FinancialTales (2020)](https://financialtales.home.blog/2020/05/04/joel-greenblatts-magic-formula-in-the-indian-context-does-it-work/)

### Altman Z-Score
- [DOAJ — Altman Z-Score for NSE-listed companies](https://doaj.org/article/cb2a512b9ceb4953895eba3099a96f94)
- [Altman's Z-Score in Indian Context (IJCRT)](https://www.ijcrt.org/papers/IJCRT25A5743.pdf)
- [Predicting Financial Distress: Logistics Companies in India](https://indianjournalofcapitalmarkets.com/index.php/ijrcm/article/view/173826)
- [Altman Z'' Emerging Market variant (CreditGuru)](https://www.creditguru.com/index.php/bankruptcy-and-insolvency/altman-z-score-insolvency-predictor-for-non-manufacturers-emerging-markets)

### Beneish M-Score
- [Predicting Earnings Manipulation Using Beneish M-Score: India (Indian Journal of Finance, Shah, 2018)](https://www.indianjournaloffinance.co.in/index.php/IJF/article/view/122796)
- [Beneish M-Score Telecom India (Ignited Journal)](https://ignited.in/index.php/jasrae/article/view/7131/14064)

### Coffee-Can / Marcellus
- [Coffee Can Investing — Book summary (Safalinvesting)](https://safalinvesting.com/coffee-can-investing-saurabh-mukherjea/)
- [Coffee-Can screen on Screener.in](https://www.screener.in/screens/57601/coffee-can-portfolio/)
- [Marcellus CCP Portfolio page](https://marcellus.in/portfolio-management-services/marcellus-consistent-compounder-pms/)
- [Marcellus FCF compounding newsletter](https://marcellus.in/newsletter/consistent-compounders/ccp-25-free-cashflow-cagr-25-share-price-compounding/)
- [Marcellus Little Champs PMS presentation](https://marcellus.in/wp-content/uploads/2023/03/Marcellus_Little_Champs_presentation_Regular-.pdf)
- [Coffee-Can small-cap application (Equitymaster, 2025)](https://www.equitymaster.com/detail.asp?date=03/04/2025&story=2&title=5-Smallcap-Stocks-Matching-Saurabh-Mukherjeas-Coffee-Can-Portfolio-Criteria)

### Indian Fund Managers
- [Raamdeo Agrawal QGLP — MOSL Wealth Creation Study](https://www.motilaloswal.com/wealth-creation-study)
- [Value Research interview — Price comes last, QGLP](https://www.valueresearchonline.com/stories/225104/price-comes-last-qglp-raamdeo-agrawal-motilal-oswal-interview/)
- [Vijay Kedia SMiLE — Value Research](https://www.valueresearchonline.com/stories/54019/how-to-invest-like-vijay-kedia/)
- [Sanjoy Bhattacharyya — Morningstar India](https://www.morningstar.in/posts/60673/6-stock-investing-insights-sanjoy-bhattacharyya.aspx)
- [Sanjoy Bhattacharyya — FLAME 2024 Presentation](https://www.flame.edu.in/pdfs/fil/presentations/A-Credo-for-Value-Investing-Sanjoy-Bhattacharyya-FIL-With-The-Masters-June2024.pdf)
- [Mohnish Pabrai — Dhandho Investor (Stockinvestoriq)](https://stockinvestoriq.com/mohnish-pabrai/)

### MSCI Quality Factor
- [MSCI Quality Indices Methodology (2013 PDF)](https://www.msci.com/eqb/methodology/meth_docs/MSCI_Quality_Indices_Methodology.pdf)
- [NSE Nifty Alpha Quality Value Low-Volatility 30](https://www.niftyindices.com/indices/equity/strategy-indices/nifty-alpha-quality-value-low-volatility-30)
- [Capitalmind NSE Strategy Indices analysis](https://www.capitalmind.in/blog/nse-strategy-indices-factor-investing-basics)
- [NIFTY Multi-Factor Indices Whitepaper (NSE)](https://archives.nseindia.com/content/indices/NIFTY_Multi-Factor_Indices_whitepaper.pdf)

### NSE Classification
- [NSE Industry Classification Guidelines (July 2023)](https://www.niftyindices.com/docs/default-source/default-document-library/nse-indices_industry-classification-guideline-2023-07.pdf)
- [NSE Industry Classification Structure (July 2023)](https://nsearchives.nseindia.com/web/sites/default/files/inline-files/nse-indices_industry-classification-structure-2023-07.pdf)

### Banking Valuation
- [How to analyse banking stocks — Samco](https://www.samco.in/knowledge-center/articles/analyse-banking-stocks/)
- [Banking stock analysis — Winvesta](https://www.winvesta.in/blog/investors/how-to-analyze-banking-stocks-key-metrics-and-ratios)
- [NIM explained — StableMoney India](https://stablemoney.in/blog/net-interest-margin-nim-explained)

### Data Sources
- [Screener.in features page](https://www.screener.in/features/)
- [Screener.in main site](https://www.screener.in/)
- [Tickertape main site](https://www.tickertape.in/)
- [Trendlyne main site](https://trendlyne.com/)
- [Tijori Finance (via comparison review)](https://ticker.finology.in/discover/solutions/screener-vs-tickertape-vs-trendlyne)
- [NSE Corporate Filings — Financial Results](https://www.nseindia.com/companies-listing/corporate-filings-financial-results)
- [NSE Corporate Filings — Pledged Data](https://www.nseindia.com/companies-listing/corporate-filings-pledged-data)
- [BSE XBRL information](https://www.bseindia.com/static/about/xbrl_info.aspx)
- [Winvesta 2026 fundamental analysis tools guide](https://www.winvesta.in/blog/investors/fundamental-analysis-tools-and-screeners-2026-guide)

### Sector Valuation and Cyclicals
- [EV/EBITDA vs P/E — Business Standard](https://www.business-standard.com/article/markets/when-should-you-use-ev-ebitda-as-an-alternative-to-p-e-ratio-here-s-a-tip-119031200362_1.html)
- [Working capital cycles across Indian industries — Goodwill](https://www.gwcindia.in/blog/how-do-working-capital-cycles-differ-across-indian-industries-and-why-it-matters-for-valuations/)
- [Interest Coverage Ratio — Goodwill India](https://www.gwcindia.in/blog/what-does-the-interest-coverage-ratio-reveal-about-the-financial-stability-of-indian-companies/)

### Graham Criteria
- [Graham defensive investor 7 criteria (Bajaj Finserv)](https://www.bajajfinserv.in/benjamin-grahams-7-stock-criteria)
- [GrahamValue — NSE stocks screened (NATIONALUM example)](https://www.grahamvalue.com/stock/nationalumns)

### Sloan Accruals
- [Sloan Ratio — Investing.com](https://www.investing.com/academy/analysis/sloan-ratio-definition/)
- [AJFA accruals study India (2019)](https://ajfa.macrothink.org/index.php/ajfa/article/download/14839/11747)

### Promoter Pledge / Governance
- [NSE Pledged Shares Data](https://www.nseindia.com/companies-listing/corporate-filings-pledged-data)
- [Promoter pledging impact on stock valuation — Groww](https://groww.in/blog/pledging-of-shares-by-promoters)
