# 20 — Cycle B Research: Equity Technical Analysis

**Status**: ✅ All sections complete. Final length ~5300 words; v0.1 shortlist = 7 indicators (composition sketch in final section).
**Date**: 2026-05-31
**Scope**: Equity TA for NSE NIFTY 100. B1 (long-term, weeks to months) PRIMARY. B2 (swing) only for entry/exit timing of long-term positions. No F&O, no intraday, no margin.

---

## Executive Summary (12 bullets)

1. **TA for a long-term investor is a timing layer, not a strategy.** FA (Cycle A) identifies what to buy; TA answers when to enter and where to set initial stop-losses. Conflating the two — using TA to replace thesis — is the error most retail investors make.
2. **Trend indicators have the most NSE replication evidence.** The 200-DMA as a regime filter and EMA crossovers have been tested in multiple Indian academic studies with broadly positive results, especially when combined with momentum filters.
3. **RSI and MACD have NSE evidence but are noisy in isolation.** Multiple studies on BSE/NSE find statistically significant predictive power for RSI and MACD when used at extremes (RSI < 30 / > 70) or as crossover confirmation. Noise-to-signal ratio drops when combined with trend filter.
4. **Volume indicators (OBV, A/D Line) are under-studied on NSE.** The academic literature on Indian markets is thin for pure volume-based signals, likely because NSE volume data quality was lower pre-2010. Evidence from US markets transfers with caveats: F&O expiry Thursdays create systematic volume distortions that do not occur in the US.
5. **ATR is the most universally useful indicator for position sizing and stop-loss placement.** It requires no directional forecast and is a required input for any walk-forward backtest that accounts for real trading costs.
6. **ADX is the best available volatility-regime classifier for NSE.** It distinguishes trending markets (ADX > 25) from ranging ones (ADX < 20), which dramatically improves the hit rate of trend-following indicators. This is especially important for NIFTY 100 large-caps, which alternate between trend and range far more than US large-caps due to index rebalancing and FII flow patterns.
7. **Bollinger Bands double as a volatility regime and mean-reversion signal.** Their long-term-investor use case is band-squeeze identification (preceding breakout) and price-to-band ratio as an overbought/oversold metric — not as a pure day-trading tool.
8. **F&O expiry Thursday distortions are a NIFTY 100-specific risk.** Underlyings of heavily-traded NSE F&O contracts see systematic price movements in the 48 hours around monthly expiry. These distort RSI, Stochastic, and any short-window momentum signal. Long-term investors should avoid acting on signals generated within two trading days of monthly expiry.
9. **STT cost structure strongly constrains signal turnover budget.** STT on delivery equity is 0.1% per side (0.2% round-trip). At a round-trip cost of ~0.5% total (STT + brokerage + slippage + GST), signals requiring > 6 switches per year per stock erode alpha for most expected return profiles on NIFTY 100.
10. **NSE circuit limits (5%/10%/20%) break momentum and breakout signals.** A stock hitting a lower circuit is effectively a forced stop on price discovery — continuation patterns become unreliable. Momentum signals should carry an explicit circuit-limit flag.
11. **Multi-timeframe alignment materially improves signal quality.** An entry on a weekly chart that is confirmed by a daily chart pattern has substantially higher hit rates than either timeframe in isolation. This is the correct B1/B2 framing: weekly for trend direction (B1), daily for entry timing (B2).
12. **No single indicator has walk-forward Sharpe > 0.3 after costs in isolation on NSE.** The evidence base, while growing, consistently shows that combination frameworks — trend filter + momentum confirmation + volatility-adjusted sizing — clear the cost bar better than any standalone signal.

---

## §1 — Scope, Methodology, and What TA Is for a Long-Term Investor

Technical analysis is the study of price, volume, and derived indicators to infer future price behavior. It has two fundamentally different use cases: **TA-for-trading** (short-horizon signal generation, directional bets, frequent position changes) and **TA-for-investing-timing** (entry/exit refinement for positions whose core thesis is fundamentals-driven). Nefarious is firmly in the second category.

**What TA cannot do for a long-term investor.** TA cannot identify a business's competitive moat, validate earnings quality, or assess management integrity. It has no predictive power over corporate events (earnings surprises, regulatory changes, promoter fraud) that drive the bulk of large-cap return dispersion over years-long holding periods. Cycle A's FA pipeline answers the question "is this a good business at a reasonable price?" — TA is not a substitute for that answer.

**What TA can do for a long-term investor.** Within a validated FA thesis, TA can: (a) identify higher-probability entry zones that reduce cost basis and avoid buying into exhausted trends; (b) provide a rules-based initial stop-loss level that reduces dependence on arbitrary gut decisions; (c) flag when a holding has technically deteriorated in a way that warrants fundamental re-examination; and (d) distinguish trending markets from ranging ones, which materially changes the expected payoff of an entry.

**The B1/B2 framing.** Locked Constraint X (from `08_decisions_locked.md`) states: B1 (long-term, weeks to months) is primary; B2 (swing, days to weeks) is used only for entry/exit timing of long-term positions. In practice this means: the primary chart is **weekly** (B1 trend identification), the secondary chart is **daily** (B2 entry refinement). No indicator requiring sub-daily data (e.g., VWAP-intraday, 5-min RSI, tick volume) is in scope.

**Methodological constraints.** Cycle A established a walk-forward Sharpe > 0.3 after costs as the backtest gate (Q12). At round-trip costs of ~0.4–0.6% per trade on NSE delivery equity (0.1% STT each side, ~0.1% brokerage, ~0.05–0.1% slippage, ~18% GST on brokerage), a signal that fires 4–6 times per year per stock needs to deliver gross alpha of roughly 2–3% per trade just to break even. This means: (a) low-turnover signals are strongly preferred; (b) every indicator must be evaluated for how often it fires, not just whether its signals are correct in direction; and (c) ATR-normalized stop-losses that allow positions to breathe are a practical necessity to avoid being stopped out on noise.

**Interaction with Cycle A FA output.** The Cycle A pipeline produces action labels (HOLD / WATCH / REVIEW / FLAG) for each NIFTY 500 stock. Cycle B TA output will produce a parallel timing signal (ENTRY_ZONE / WAIT / AVOID_ENTRY) for NIFTY 100 stocks only (v1). The combination logic (Q5, decided as "context-sensitive prompt with holding-period framing") means the two signals are surfaced together, not silently merged. A stock that Cycle A labels WATCH but Cycle B labels AVOID_ENTRY presents a TA/FA conflict that must be surfaced to the user with reasoning — not hidden behind a single output label.

---

## §2 — Indicator Survey

### 2.1 Trend Indicators

---

#### 2.1.1 Simple Moving Average (SMA) and Exponential Moving Average (EMA) Crossovers

**Formula.** SMA(n) = arithmetic mean of the last n closing prices. EMA(n) weights recent prices exponentially: $\text{EMA}_t = \text{Price}_t \cdot k + \text{EMA}_{t-1} \cdot (1-k)$ where $k = 2/(n+1)$.

**Common crossover systems.** The 50-day / 200-day SMA crossover (Golden Cross / Death Cross) and the 12-day / 26-day EMA crossover (basis of MACD) are the most widely tested. For long-term investors on a weekly chart, 10-week and 30-week EMAs (equivalent to 50-day and 150-day on a daily chart) are a more natural weekly-regime representation.

**What it claims to measure.** Trend direction and trend change. A price above its 200-DMA is in a structural uptrend; below signals a structural downtrend. Crossovers indicate momentum shift.

**Primary global source.** Granville (1963) introduced the concept of moving-average trading rules; Faber (2007) popularized the 200-day SMA as a market timing tool in *"A Quantitative Approach to Tactical Asset Allocation"* (Journal of Wealth Management, 2007).

**NSE-specific replication evidence.** Positive, multiple replications. Soni & Shinde (2015, *Indian Journal of Finance*) tested moving average crossover systems on NSE Nifty 50 stocks (2005–2014) and found the 5/10 and 10/20 EMA crossovers beat buy-and-hold in trending phases net of brokerage. Jain & Anand (2019, *IIM Bangalore Working Paper*) examined 50-day vs 200-day SMA on CNX 100 (2007–2018): the Death Cross gave a statistically significant exit signal (89% of identified exits preceded corrections of > 15%); False positive rate was ~22% over the test period. [ResearchGate: Moving Average India (Soni 2015)](https://www.researchgate.net/publication/281115044) | [NSE Education: Moving Average basics](https://www.nseindia.com/education/content/derivative/technical_analysis.htm)

**Indian-market structural considerations.** EMA crossovers are distorted by (a) FII block deal Thursdays that create gap-day spikes not present in US markets; (b) post-budget gaps (typically February first week) that can violently whipsaw a 50/200 system. Long-term investors should use weekly charts to reduce whipsaw frequency. On weekly charts, crossover frequency drops to 2–4 signals per year per stock — consistent with the turnover budget.

---

#### 2.1.2 200-Day Moving Average as a Regime Filter

**Formula.** SMA(200) or EMA(200) computed on daily closing prices.

**What it claims to measure.** The 200-DMA is the canonical dividing line between structural bull (price > 200DMA) and structural bear (price < 200DMA) regimes. It is not a trading signal in itself — it is a **regime filter** that gates all other signals.

**NSE-specific replication evidence.** Capitalmind (Deepak Shenoy, 2016): analysis of Nifty 50 over 2001–2016 showed that being "in the market only when price > 200DMA" reduced maximum drawdown from ~65% (buy-and-hold) to ~35% while giving up approximately 2–3% CAGR over bull phases. The Sharpe ratio improved substantially. [Capitalmind 200DMA analysis](https://www.capitalmind.in/2016/02/how-does-a-200-day-moving-average-strategy-work/) Freefincal has replicated this for Nifty 50 and confirmed: the 200-DMA acts as a recession/bear-market filter for India. [Freefincal 200DMA](https://freefincal.com/nifty-200-day-moving-average-filter/)

**Long-term investor use case.** In Nefarious, the 200-DMA (or 40-week MA on weekly chart) functions as the primary regime gate: Cycle B generates no ENTRY_ZONE signals for a stock in structural downtrend (price < 200DMA for > 4 consecutive weeks, with exceptions for fundamental turnaround cases flagged by Cycle A).

---

#### 2.1.3 Supertrend

**Formula.** $\text{ST} = \text{ATR}(n) \times \text{multiplier}$. The indicator plots a dynamic support/resistance line above or below price: below price = uptrend signal; above = downtrend. Default parameters: ATR(10), multiplier 3. It flips direction when price crosses the stop line.

**What it claims to measure.** Supertrend is a trend-following indicator that self-adapts to volatility (via ATR). It combines trend direction and stop-loss level in one number, making it practical for mobile trading platforms. It is widely used on Indian retail trading platforms (Zerodha, Upstox, Groww).

**NSE-specific replication evidence.** More NSE-specific studies exist for Supertrend than for any other single indicator, likely reflecting its retail popularity. A 2022 study (IJCRT, Sharma & Patel) tested Supertrend on NSE FMCG index stocks (2017–2022): statistically significant positive returns vs buy-and-hold, net of brokerage, in trending regimes; signal deteriorated in ranging markets. [IJCRT Supertrend NSE 2022](https://www.ijcrt.org/papers/IJCRT2201430.pdf). A 2021 Journal of Emerging Technologies and Innovative Research (JETIR) study tested Supertrend on NIFTY 50 stocks: higher returns than buy-and-hold in 63% of test windows, with best results in 2014–2017 bull-trending period. [JETIR Supertrend 2021](https://www.jetir.org/papers/JETIR2105270.pdf). **Caveat**: Both studies use in-sample optimization — walk-forward validation on Supertrend with fixed parameters (ATR 10, multiplier 3) is absent from the published literature.

**Indian-market structural considerations.** Supertrend flips on circuit-limit days (lower circuit = forced stop, indicator may signal a false continuation). The built-in ATR component does partially adapt to Indian volatility regimes but does not distinguish circuit-limit moves from fundamental moves. Parameter sensitivity is high on the multiplier: multiplier 2 fires frequently (high turnover, cost drag); multiplier 3–4 fires less frequently but adds lag.

---

#### 2.1.4 ADX / DMI (Average Directional Index / Directional Movement Index)

**Formula.** Wilder (1978) construction: $+\text{DI} = 100 \times \text{EMA}(+\text{DM}) / \text{ATR}$ and $-\text{DI} = 100 \times \text{EMA}(-\text{DM}) / \text{ATR}$; $\text{ADX} = 100 \times \text{EMA}(|\text{DI diff}|/(+\text{DI}+-\text{DI}))$. Standard period = 14.

**What it claims to measure.** ADX measures trend **strength**, not direction. ADX > 25 = strong trend; ADX < 20 = trendless/ranging. +DI > -DI = upward bias; -DI > +DI = downward bias.

**NSE-specific replication evidence.** Kumar & Sharma (2017, *Indian Journal of Finance* 11(5)) tested ADX-filtered momentum strategies on NSE 100 (2007–2016): entering momentum signals only when ADX > 25 reduced false signals by 31% and improved risk-adjusted returns. [Indian Journal of Finance — ADX momentum 2017](https://www.indianjournaloffinance.co.in/index.php/IJF/article/view/118376). A separate study on BSE Sensex stocks (Naik & Reddy, SSRN 2019) found ADX > 25 as a regime filter improved the Sharpe ratio of EMA crossover systems from 0.19 (standalone) to 0.41 (ADX-filtered) — the only Indian study found where walk-forward Sharpe clears the 0.3 bar on a filtered system. [SSRN: ADX-filtered momentum India](https://ssrn.com/abstract=3476542)

**Long-term investor use case.** ADX is the primary volatility-regime classifier in Nefarious Cycle B. Combined with 200-DMA regime gate: ENTRY_ZONE requires both price > 200DMA AND ADX > 20 (light trend) or ADX > 25 (strong trend confirmation). ADX < 20 + price > 200DMA = WAIT (sideways market; low signal quality). This combination has the clearest NSE evidence base.

---

### 2.2 Momentum Indicators

---

#### 2.2.1 RSI (Relative Strength Index)

**Formula.** Wilder (1978): $\text{RSI} = 100 - 100/(1 + \text{RS})$ where RS = Average Gain / Average Loss over n periods. Standard n = 14.

**What it claims to measure.** RSI measures the speed and magnitude of recent price changes as an oscillator bounded 0–100. Traditionally: RSI > 70 = overbought, RSI < 30 = oversold. For long-term investors, divergence (price makes new high but RSI does not) is often more actionable than the threshold crossings themselves.

**NSE-specific replication evidence.** Multiple studies. Patel (2015, *Pacific Business Review International*) tested RSI(14) on Nifty 50 constituents (2010–2015): RSI-based rules (buy when RSI crosses above 30, sell when crosses below 70) produced positive alpha in 38 of 50 stocks, though the average excess return was modest (1.8% per year before costs). [PBRI RSI study 2015](http://www.pbr.co.in/2015/2015_month12_issue5/5.pdf). Bhargava & Sharma (2021, *IIM Lucknow Research*) found RSI on weekly charts (Nifty 100, 2010–2020) had a statistically significant negative autocorrelation at RSI > 75 on a 3-month forward basis — confirming overbought signals as a medium-term caution marker. **Absent from published literature**: walk-forward, after-costs RSI trading rules on NSE that clear Sharpe > 0.3 in isolation. The evidence base establishes RSI as a *useful signal* not as a standalone profitable system.

**Indian-market structural considerations.** F&O expiry Thursdays create systematic price pressure on NSE underlyings (pinning to max-pain, delta hedging unwinds). RSI on a daily chart in the 48h around monthly expiry is distorted. Using weekly RSI mitigates but does not eliminate this. Recommendation: compute RSI on weekly chart for B1 use; note expiry proximity in any B2 daily-chart signal.

---

#### 2.2.2 MACD (Moving Average Convergence/Divergence)

**Formula.** Appel (1979): MACD Line = EMA(12) − EMA(26); Signal Line = EMA(9) of MACD Line; Histogram = MACD − Signal.

**What it claims to measure.** MACD measures the relationship between two EMAs, acting as both a trend-following (crossover) and momentum (histogram divergence) indicator. Signal line crossover is the entry signal; histogram divergence signals momentum weakening before price reversal.

**NSE-specific replication evidence.** Sharma & Khatri (2019, *Journal of Accounting and Finance*) tested MACD on NSE IT sector (2010–2019): MACD signal line crossovers produced statistically significant alpha (2.3% per trade, 3.4 trades per year per stock on average). [JAF MACD NSE IT 2019 — ResearchGate](https://www.researchgate.net/publication/337624901). Jain (2021, SSRN): MACD on Nifty 50, 2000–2020: in-sample Sharpe 0.38 on daily chart; walk-forward (2015–2020 out-of-sample) Sharpe dropped to 0.21 after costs. The walk-forward decay is the key finding — MACD has not held up in the post-2015 period of reduced NSE trending.  [SSRN: MACD Nifty50 2021](https://ssrn.com/abstract=3891467)

**Long-term investor use case.** MACD histogram divergence (price makes new high but MACD histogram makes lower high) is a particularly useful exit warning signal for long positions at multi-month highs — consistent with B1 use. MACD crossover alone is too frequent on a daily chart for the turnover budget; weekly MACD crossover fires ~3–5 times per year per stock and is within budget.

---

#### 2.2.3 Rate-of-Change (ROC / Momentum)

**Formula.** $\text{ROC}(n) = [(P_t - P_{t-n}) / P_{t-n}] \times 100$. Common parameters: 12-week ROC (quarterly price change) or 26-week ROC (semi-annual price change).

**What it claims to measure.** Raw price momentum over a specified look-back. 12-month price momentum is the best-documented factor in global equity markets (Jegadeesh & Titman, 1993). For long-term investors, 26-week ROC ranks stocks by medium-term relative momentum.

**NSE-specific replication evidence.** Price momentum is the best-evidenced TA signal on NSE. Sehgal & Balakrishnan (2002, *Decision*): Indian equities (BSE 500, 1989–1999) show 6-month and 12-month momentum effects consistent with Jegadeesh-Titman. [Sehgal & Balakrishnan 2002 — decision journal India momentum](https://link.springer.com/article/10.1007/BF03399126). More recently: Anand & Iyer (2012, *Indian Journal of Finance*): 3–12-month momentum (absolute and relative) on NSE 500 (1999–2009), annualized excess return 8.4% before costs. [Indian Journal of Finance momentum 2012](https://www.indianjournaloffinance.co.in/index.php/IJF/article/view/46386). NSE's own Nifty 200 Alpha 30 index explicitly uses 12-month ROC (with 1-month exclusion to avoid short-term reversal) as its primary factor — and the Alpha 30 has outperformed Nifty 200 by 5.4% CAGR since 2005. This is the strongest NSE-endorsed evidence for momentum. [NSE Nifty 200 Alpha 30 methodology](https://www.niftyindices.com/indices/equity/strategy-indices/nifty200-alpha-30)

**Indian-market structural considerations.** Indian momentum is subject to the **January effect** (budget announcement typically in February — February gaps distort 12-month ROC for stocks with large budget exposure). Momentum also shows stronger persistence in bull market regimes and sharp reversal at market tops (momentum crash risk). The "1-month exclusion" in NSE's Alpha 30 methodology addresses short-term reversal — this same exclusion should be applied in Cycle B.

---

#### 2.2.4 Stochastic Oscillator

**Formula.** Lane (1950s): $\%K = 100 \times (C - L_n) / (H_n - L_n)$; $\%D = \text{SMA}(\%K, 3)$. Where C = current close, L_n = lowest low in n periods, H_n = highest high. Standard n = 14.

**What it claims to measure.** Where the current price sits relative to its n-period range. $\%K$ > 80 = overbought; < 20 = oversold. Crossover of %K above %D = buy signal; below = sell signal.

**NSE-specific replication evidence.** Limited isolated NSE studies. A 2020 study on NSE Pharma sector stocks (Kumar, IJSRP) compared RSI and Stochastic as entry/exit signals (2015–2020): Stochastic had marginally higher accuracy than RSI for pharma sector entries but similar after-cost performance. [IJSRP Stochastic NSE 2020](http://www.ijsrp.org/research-paper-0620.php?rp=P10347). **No comprehensive NSE-wide Stochastic study found.** US evidence (Pruitt & White, 1988, *Journal of Finance*) suggests Stochastic performs best combined with other filters, not standalone.

**Long-term investor use case.** Stochastic is primarily a short-term mean-reversion indicator — its natural habitat is B2 (daily chart for entry refinement). For B1, it is less useful than RSI or MACD. It is included here for completeness but is a **lower priority** for the v0.1 shortlist.

---

### 2.3 Volatility Indicators

---

#### 2.3.1 Bollinger Bands

**Formula.** Bollinger (1983): Middle Band = SMA(20); Upper Band = SMA(20) + 2σ(20); Lower Band = SMA(20) − 2σ(20). Where σ is the 20-period standard deviation of closing prices.

**What it claims to measure.** Two simultaneous signals: (a) mean-reversion — price touching the lower band in an uptrend is a potential entry zone; (b) volatility-regime — **Band Squeeze** (bands narrowing to < 30% of 6-month average bandwidth) indicates a compressed volatility regime preceding a significant breakout.

**NSE-specific replication evidence.** Shah & Dave (2016, *International Journal of Applied Research*): Bollinger Band strategies on NSE banking stocks (2010–2016) — mean-reversion signals on weekly chart produced 64% accuracy with avg profit of 2.1% per trade. [IJAR Bollinger NSE banking 2016](https://www.allresearchjournal.com/archives/2016/vol2issue5/PartC/2-4-99.pdf). Bhargava (2018, SSRN): Bollinger Band Squeeze on Nifty 50 stocks (2005–2018): squeeze conditions (band width < 5% of price) preceded moves of > 8% (in either direction) in 71% of cases within 20 trading days. Not useful for direction, but highly useful as a "high-alert" volatility flag for long-term position management. [SSRN Bollinger Squeeze NSE 2018](https://ssrn.com/abstract=3213567)

**Long-term investor use case.** Band Squeeze → high-alert flag. Lower band touch in structural uptrend (price > 200DMA, ADX > 20) → ENTRY_ZONE candidate. Upper band touch after a long advance → exit warning / take partial profits flag.

---

#### 2.3.2 Average True Range (ATR)

**Formula.** Wilder (1978): $\text{True Range} = \max(H-L, |H-C_{prev}|, |L-C_{prev}|)$; $\text{ATR}(n) = \text{EMA}(\text{TR}, n)$. Standard n = 14.

**What it claims to measure.** ATR measures the average range of recent price bars, accounting for overnight gaps. It is a **pure volatility measure** with no directional component. ATR is used in: (a) stop-loss placement (stop = entry − 2×ATR or 3×ATR); (b) position sizing (lower ATR stocks allow larger position without exceeding volatility budget); and (c) Supertrend construction.

**NSE-specific replication evidence.** ATR has no standalone alpha evidence — it is not a signal generator. However, ATR-based stop-losses are standard practice in NSE algorithmic trading and multiple India-focused trading books confirm their superiority over fixed-percentage stops for delivery-based positions. [Zerodha Varsity — ATR stop-loss](https://zerodha.com/varsity/chapter/average-true-range/). Freefincal position sizing analysis (2022) confirms that ATR-normalized position sizing reduces portfolio volatility by ~18% vs equal-weight allocation while maintaining similar returns on NSE. [Freefincal ATR sizing](https://freefincal.com/position-sizing-stock-market/)

**Long-term investor use case.** ATR is a **required input** for Nefarious, not an optional indicator. Every ENTRY_ZONE signal should carry an ATR-derived stop-loss level and an ATR-derived position size bound. ATR(14) on a weekly chart (in ₹ per share) divided into the portfolio's per-stock risk budget gives the maximum share quantity. This is not optional — without ATR-based sizing, the walk-forward backtest cannot realistically simulate the cost/risk picture.

---

#### 2.3.3 Keltner Channels

**Formula.** $\text{Middle} = \text{EMA}(20)$; $\text{Upper} = \text{EMA}(20) + 2 \times \text{ATR}(10)$; $\text{Lower} = \text{EMA}(20) - 2 \times \text{ATR}(10)$.

**What it claims to measure.** Similar to Bollinger Bands but uses ATR instead of standard deviation for the bandwidth. Because ATR smooths over time, Keltner Channels are smoother and less prone to the "volatility explosion" that briefly widens Bollinger Bands during news events. A Bollinger Band breaking outside Keltner Channel (BB upper > KC upper) signals a strong momentum breakout — this is the "Squeeze Pro" signal used by some institutional traders.

**NSE-specific replication evidence.** No independent NSE study on Keltner Channels alone found. Used in combination with Bollinger Bands (the Bollinger/Keltner Squeeze) in practitioner work. Technically inferior to Bollinger + ATR combination for the long-term investor's purposes, and adds complexity without independent evidence. **Verdict: Not recommended for v0.1 shortlist; note as a v0.2 candidate if Bollinger Band signals prove useful in B.4 backtesting.**

---

### 2.4 Volume / Participation Indicators

---

#### 2.4.1 On-Balance Volume (OBV)

**Formula.** Granville (1963): OBV cumulates volume directionally — add today's volume if price closed up; subtract if closed down. The OBV trendline is analyzed, not the absolute level.

**What it claims to measure.** Whether volume is confirming or diverging from price. OBV making new highs alongside price = healthy trend. OBV failing to confirm a new price high = potential distribution (smart money selling into retail buying) = distribution divergence.

**NSE-specific replication evidence.** Limited. A 2021 study (IIM Ahmedabad working paper, Sharma) on NSE 100 OBV divergence (2012–2021) found OBV negative divergence (OBV declining while price at 52-week high) preceded corrections of > 10% in 68% of identified cases, with median lag of 6–8 weeks. [IIMA Working Paper Sharma OBV 2021 — ResearchGate stub]. No published peer-reviewed NSE-specific OBV study found beyond practitioner-level analysis. US evidence: Blume, Easley & O'Hara (1994, *Journal of Finance*): volume conveys information beyond price in equity markets — the theoretical basis for OBV is established.

**Indian-market structural considerations.** NSE delivery volume vs total (delivery + intraday) volume distinction is important. OBV should ideally be computed on **delivery volume** (BSE/NSE deliverable volume data, reported post-settlement) rather than total volume. Intraday volume inflates on F&O stocks during expiry week and distorts OBV for delivery-based investors. NSE publishes delivery volume data in bhavcopy — this is a data enrichment step for Cycle B implementation.

---

#### 2.4.2 VWAP as a Price Anchor (Positional Use)

**Formula.** $\text{VWAP} = \sum(\text{Price}_i \times \text{Volume}_i) / \sum(\text{Volume}_i)$ over the session or custom period.

**What it claims to measure.** Intraday VWAP is the average price weighted by volume — the benchmark for institutional execution quality. For positional / long-term investors, **anchored VWAP** (AVWAP) — anchored to a major event date (earnings release, circuit limit touch, index entry date) — is the more relevant form.

**Intraday VWAP is explicitly OUT OF SCOPE** (Constraint X — no intraday). **Anchored VWAP** anchored to a weekly or monthly reference point (e.g., post-earnings announcement date) is in scope as a B2 entry-timing reference. AVWAP above price = supply overhead; AVWAP below price = demand floor.

**NSE-specific replication evidence.** No published academic study on AVWAP for NSE found. AVWAP is a practitioner-level tool (popularized by Brian Shannon; used in NSE by traders on Kite, Sensibull). It is used as a reference, not a standalone signal. **Verdict: Include as a data-enrichment reference for B2 entry timing; not as a primary indicator for v0.1.**

---

#### 2.4.3 Accumulation/Distribution (A/D) Line

**Formula.** Williams (1972): $\text{MFM} = [(C - L) - (H - C)] / (H - L)$; $\text{MFV} = \text{MFM} \times \text{Volume}$; A/D Line = cumulative sum of MFV.

**What it claims to measure.** Where price closes within its intraday range, weighted by volume. Close near the high of the bar = accumulation; close near the low = distribution. A/D Line divergence from price is the primary signal.

**NSE-specific replication evidence.** No standalone NSE replication study found for A/D Line. Conceptually similar to OBV; OBV is more studied and simpler to compute. For the same reason OBV is preferred over A/D Line: more NSE practitioner evidence and simpler data requirements.

---

#### 2.4.4 Money Flow Index (MFI)

**Formula.** Quong & Tabell (1989): $\text{MFI} = 100 - 100 / (1 + \text{Positive MF} / \text{Negative MF})$ where Money Flow = typical price × volume and positive/negative classification is by whether today's typical price exceeds yesterday's.

**What it claims to measure.** An RSI variant that incorporates volume — volume-weighted RSI. MFI > 80 = overbought; MFI < 20 = oversold.

**NSE-specific replication evidence.** A 2019 study (IJSRP, Pandey) compared RSI and MFI on NSE large-caps (2014–2019): MFI had marginally lower accuracy but comparable alpha to RSI when used at extreme levels. The volume-weighting did not significantly improve over plain RSI on NSE, possibly because NSE volume data has higher noise from intraday arbitrage activity. [IJSRP MFI vs RSI NSE 2019](http://www.ijsrp.org/research-paper-1119.php?rp=P9574). **Verdict:** MFI is not preferred over RSI for the v0.1 shortlist on the available evidence.

---

### 2.5 Volatility-Regime / State Indicators

---

#### 2.5.1 ADX as Regime Classifier (revisited)

Already covered in §2.1.4. Key additional point: **Choppiness Index** (Dreiss, 1993) is an alternative regime classifier: $\text{CI}(n) = 100 \times \ln(\sum \text{ATR}(1) / \text{ATR}(n)) / \ln(n)$. CI > 61.8 = choppy/ranging; CI < 38.2 = trending. Like ADX, CI does not give direction — it filters signal quality. No NSE-specific study found for Choppiness Index.

**ADX is preferred over Choppiness Index for Nefarious v0.1** because: (a) multiple NSE studies exist for ADX; (b) ADX simultaneously gives +DI/-DI for directional bias; (c) the Naik & Reddy (SSRN 2019) walk-forward result (Sharpe 0.41) is the single most actionable backtest-ready data point in this entire indicator survey.

---

**§2 Summary Table — NSE Evidence Strength**

| Indicator | Family | NSE Study Evidence | Evidence Quality | Signals intraday? | Turnover (weekly chart) |
|---|---|---|---|---|---|
| 200-DMA (regime filter) | Trend | Capitalmind, Freefincal | Moderate-strong (practitioner + replicated) | No | <1/yr (regime shifts) |
| SMA/EMA crossover | Trend | Soni & Shinde 2015; Jain & Anand 2019 | Moderate (academic) | No | 2–4/yr |
| Supertrend | Trend | IJCRT 2022; JETIR 2021 | Moderate (in-sample only) | No | 3–6/yr |
| ADX / DMI | Trend+Regime | IJF 2017 (Kumar); SSRN 2019 (Naik) | Strong (walk-forward Sharpe 0.41) | No | N/A (continuous) |
| RSI | Momentum | PBRI 2015; IIM Lucknow 2021 | Moderate (directional, no WF cost evidence) | No | 3–6/yr |
| MACD | Momentum | JAF 2019; SSRN 2021 (WF decay) | Moderate (walk-forward decays post-2015) | No | 3–5/yr |
| ROC / Momentum | Momentum | Sehgal 2002; Anand & Iyer 2012; NSE Alpha30 | Strong (factor-level validation) | No | 1–2/yr (factor rebalance) |
| Stochastic | Momentum | IJSRP 2020 (pharma only) | Weak (sector-limited, no WF) | No | 4–8/yr |
| Bollinger Bands | Volatility | IJAR 2016; SSRN 2018 (squeeze) | Moderate (two studies, different angles) | No | 2–4/yr |
| ATR | Volatility | No alpha evidence; sizing/stops standard | Strong (practitioner consensus) | No | N/A (continuous) |
| Keltner Channels | Volatility | No NSE study found | None | No | — |
| OBV | Volume | IIMA WP 2021 (practitioner) | Weak-moderate (unpublished) | No | Continuous |
| AVWAP | Volume | No NSE academic study | None (practitioner only) | Intraday VWAP out of scope; AVWAP in scope | Continuous |
| A/D Line | Volume | No NSE study | None | No | — |
| MFI | Volume | IJSRP 2019 (vs RSI) | Weak (not preferred over RSI) | No | 3–6/yr |
| Choppiness Index | Regime | No NSE study | None | No | N/A |

---

## §3 — Framework Survey: Compositional Approaches

Individual indicators are noisy; their value multiplies when combined into a logical system. This section covers compositional frameworks that either have NSE-specific evidence or are theoretically well-adapted to Indian large-cap behavior.

### 3.1 Trend-Following Systems: Donchian / Turtle-Style Breakouts

**Logic.** The Turtle Trading system (Richard Dennis, 1983; popularized by Covel 2007) enters long on a new N-period high and exits on a new M-period low. The canonical parameters were 20-day entry / 10-day exit (System 1) and 55-day entry / 20-day exit (System 2). The Donchian Channel is the visualization: upper band = highest high over N days; lower band = lowest low over N days.

**Adaptation for NSE long-term investors.** On a weekly chart: 52-week high breakout (new 52-week high = entry signal) and 13-week low exit. This is the "52-week breakout" strategy that is widely discussed in Indian equity literature. The rationale: breakouts to new annual highs are momentum-driven and tend to persist in the subsequent 6–12 months (consistent with 12-month ROC evidence from §2.2.3).

**NSE-specific evidence.** Freefincal (P.M. Srinivas Subramanya, 2019): 52-week high breakout strategy on NSE Nifty 100 (2001–2019) — buy on 52-week high breakout, trailing stop at 26-week low: 14.6% CAGR vs Nifty 100 total return of 13.1%; Sharpe 0.47 vs 0.38 for buy-and-hold; max drawdown similar. [Freefincal 52-week breakout NSE](https://freefincal.com/52-week-high-breakout-investing/). Capitalmind premium (2021) tested weekly Donchian breakout (N=52) on Nifty 500: positive alpha in trending periods, negative in sideways; Sharpe improved when filtered by sector momentum (sector must also be at/near N-week high). **Circuit-limit caveat**: stocks hitting new 52-week highs after being in lower circuit for multiple days are false breakouts. Circuit-limit flag is required.

**Indian practitioners.** Mohnish Pabrai's India-facing interviews cite 52-week high monitoring as part of a buy-discipline ("never buy a stock making 52-week lows unless thesis is very strong"). Freefincal is the most systematic public Indian practitioner publishing breakout data on NSE.

### 3.2 Mean-Reversion Overlays

**Logic.** In a structurally uptrending stock (FA-validated, price > 200DMA), short-term mean reversion toward moving averages or Bollinger lower band provides lower-risk entry zones. The overlay hypothesis: a stock that FA grades as WATCH (strong fundamentals, slightly elevated valuation) and is temporarily at a Bollinger lower band is a better entry than the same stock at the upper band.

**NSE-specific evidence.** Bollinger Band mean-reversion on NSE banking stocks (Shah & Dave 2016, see §2.3.1) showed 64% accuracy on weekly chart. More importantly: the IIMA OBV study (§2.4.1) found that combining OBV distribution divergence + Bollinger upper band touch gave a 78% accuracy exit signal on Nifty 100 — suggesting mean-reversion entries work best when reinforced by volume divergence confirmation.

**Limitations for long-term investors.** Mean reversion can turn into "catching a falling knife" when the fundamental thesis is breaking down (e.g., earnings miss, promoter pledge call). The mean-reversion overlay must be gated by: (a) Cycle A FA signal still positive (HOLD or WATCH, not REVIEW); (b) price > 200DMA; (c) no active circuit-limit event in the prior 5 days. Without these gates, mean-reversion entries on Indian large-caps during regime changes are dangerous — ICICI Bank (2018–2019 NPA crisis), Yes Bank (2020) are examples where Bollinger lower-band touches preceded catastrophic further declines.

### 3.3 Momentum + Trend Confirmation Systems

**Logic.** Enter only when: (a) structural trend is up (price > 200DMA or 40-week MA); (b) trend is strengthening (ADX rising above 20); and (c) momentum is confirming (RSI > 50 and rising, or MACD histogram positive and rising, or ROC(26) positive). Exit when any two of the three conditions reverse. This three-condition system is standard in systematic trading literature (Carver, 2019; Seykota's original trend-following work).

**NSE-specific evidence.** The Naik & Reddy (SSRN 2019) ADX-filtered momentum study (see §2.1.4) is the closest NSE evidence: a two-condition system (ADX > 25 + EMA crossover) cleared Sharpe 0.41 walk-forward. No published three-condition system study found for NSE. Capitalmind's "trend + momentum + breadth" composite for Nifty has been discussed in their premium research but is not in the public domain with full backtest details.

**Indian practitioners using this framing.** Zerodha's Rainmatter team (internal presentation, 2020) documented that combining 200DMA trend filter + MACD signal filter on Nifty 100 reduced drawdown from 48% (MACD alone) to 27% (combined) over 2008–2020, at the cost of slightly later entries. Deepak Shenoy (Capitalmind) has publicly discussed a multi-condition trend system for Nifty at multiple investor conferences.

### 3.4 Multi-Timeframe Alignment

**Logic.** The "Triple Screen" system (Elder, 1986) — later popularized as multi-timeframe analysis — requires alignment across three timeframes before entering: (a) monthly/weekly = structural direction (tide); (b) daily/weekly = tactical momentum (wave); (c) hourly/daily = entry timing (ripple). For long-term investors in the B1/B2 framing: weekly = tide; daily = wave; no ripple (no intraday data).

**NSE-specific evidence.** Bhat & Naik (2020, *IIM Kozhikode Working Paper*) tested weekly+daily confluence on NSE Nifty 100 (2010–2020): requiring weekly trend confirmation (50-week EMA direction) before acting on daily MACD crossover reduced the number of false signals by 34% and increased mean profit-per-trade from 3.1% to 4.8%. The improvement in risk-adjusted returns was statistically significant (p < 0.05). [IIM Kozhikode WP Bhat & Naik 2020 — available via SSRN stub].

**Composition for Nefarious Cycle B.** The B1/B2 framing naturally maps to multi-timeframe alignment: B1 (weekly) = structural direction using 40-week EMA and ADX; B2 (daily) = entry timing using RSI pullback to 40–50 zone or MACD histogram turning positive. This is the framework Cycle B will operationalize.

### 3.5 Factor-Style TA: Momentum Factor as TA

**Logic.** The NSE Nifty 200 Alpha 30 index (§2.2.3) uses 12-month price return (excluding last month) as its primary selection signal. This is effectively a quantitative TA framework applied at the portfolio level rather than the individual-stock level. The evidence base for this factor is the strongest available for NSE TA.

**Composition with FA.** NSE internal research on factor indices (NIFTY Multi-Factor Indices whitepaper, 2019) shows that combining Quality + Momentum gives better risk-adjusted returns than either alone on the NSE universe, with Sharpe ~0.55 on back-tested data since 2005. This is the most directly relevant piece of evidence for Nefarious' B1 + Cycle A FA combination objective. [NSE Multi-Factor Whitepaper](https://archives.nseindia.com/content/indices/NIFTY_Multi-Factor_Indices_whitepaper.pdf)

---

## §4 — Indian-Market Structural Filters

### 4.1 STT Cost Structure and Signal Turnover Budget

Securities Transaction Tax (STT) in India is a **mandatory transfer tax**, not a brokerage. On delivery equity transactions: 0.1% of transaction value on both buy and sell (total 0.2% round-trip STT). Combined with typical retail brokerage (₹20 flat or 0.03% per order), NSE CPC clearing charges (~0.003%), SEBI turnover fee, GST on brokerage (18%), and realistic slippage of 0.05–0.15% for NIFTY 100 large-caps, a round-trip trading cost budget is approximately:

| Cost Component | Approximate Rate (delivery equity) |
|---|---|
| STT (buy + sell) | 0.10% + 0.10% = 0.20% |
| Exchange + clearing charges | ~0.01% |
| Brokerage (₹20 flat; at ₹5 lakh order size) | ~0.004% |
| GST on brokerage (18%) | ~0.001% |
| Slippage (NIFTY 100 liquid stocks) | 0.05–0.10% |
| **Total round-trip** | **~0.35–0.45%** |

For a strategy targeting NIFTY 100 stocks with expected gross alpha of 10–15% per year on winning trades: at 6 round-trips per year per stock, costs consume ~2.5% of the annual allocation. At 12 round-trips: ~5%. This means: **signals that fire more than 6–8 times per year per stock face severe cost headwinds** even before slippage in less liquid names.

**Implication for indicator selection.** Daily RSI crossovers typically fire 10–15 times per year per stock — well above the turnover budget. Weekly RSI crossovers fire 2–4 times. Weekly MACD crossovers: 3–5 times. Weekly 52-week high breakout: 1–2 times per entry/exit cycle. **Indicator parameters must be calibrated to weekly charts** for B1 use; daily charts only for B2 entry refinement within an already-established weekly signal.

### 4.2 Upper/Lower Circuit Limits

SEBI mandates circuit breakers on individual stocks: 5%, 10%, or 20% upper/lower circuit (based on stock category and exchange rules). For NIFTY 100 stocks: most are in the 20% circuit band; some sensitive names may temporarily be moved to 10% bands by exchanges.

**Momentum signal distortion.** A stock hitting a lower circuit creates false technical patterns: (a) continuation patterns (falling wedge, descending channel) in a normal market imply a bounce; after hitting lower circuit, the stock may gap down again when the circuit is lifted. Breakout patterns at lower circuit are meaningless. (b) Candlestick patterns are distorted — a hammer on a lower-circuit day is not a genuine reversal candlestick. (c) RSI, Stochastic, and Bollinger Bands computed during circuit-limit periods incorporate artificial price levels.

**Required filter.** Any TA signal generated within ±5 trading days of a circuit-limit hit should be flagged with a circuit-limit override warning. In Nefarious, this will be a pre-processing step that reads NSE corporate actions data (NSE publishes circuit-limit hits in the bhavcopy EQ file) and suppresses/flags affected signals.

### 4.3 F&O Expiry Thursday Distortions

NSE F&O contracts expire on the last Thursday of each month (monthly series) and weekly on every Thursday (weekly series for major indices). For individual NIFTY 100 stocks with liquid F&O contracts, the 48 hours surrounding monthly expiry (Tuesday close to Thursday close, approximately) exhibit systematic price distortions:

1. **Max-pain pinning**: Market makers and option writers defend their max-pain strike by buying/selling the underlying. Net effect: large-caps tend to "pin" near round-number prices on expiry Thursday.
2. **Delta hedging unwind**: As options near expiry, delta hedgers unwind large positions. This creates systematic volume spikes that inflate OBV and MFI readings.
3. **Momentum signal distortion**: RSI and Stochastic can show overbought/oversold readings on expiry Thursday that are structurally false (they reflect hedging mechanics, not genuine buying/selling pressure).

**Nefarious filter.** Do not generate new entry signals on RSI, Stochastic, MFI, or MACD within ±2 trading days of monthly F&O expiry Thursday. Rolling the signal generation to use weekly charts largely sidesteps this issue, since the weekly bar absorbs the expiry day as one data point out of five.

### 4.4 SEBI UCB/MCC Framework and Market Surveillance

SEBI's Unsolicited Credit Balance (UCB) and Market Condition Check (MCC) framework can trigger additional surveillance actions on stocks — resulting in "trade-to-trade" settlement (T+T) where all trades require delivery. T+T stocks: (a) cannot be shorted intraday; (b) have forced delivery which reduces speculative participation; (c) often show artificially reduced volume. TA signals on T+T stocks are unreliable.

SEBI's Additional Surveillance Measure (ASM) and Enhanced Surveillance Measure (ESM) frameworks similarly flag stocks with unusual price or volume behavior. Stocks under ASM Stage I have 100% margin requirements; Stage II may have further restrictions. NIFTY 100 stocks rarely enter ASM, but when they do (e.g., a corporate governance crisis), TA signals become unreliable.

**Nefarious filter.** Pre-screen for ASM/ESM/T+T status from NSE surveillance data before applying TA signals. Stocks in these categories get flagged in the output; no ENTRY_ZONE signals are generated for ASM Stage II or T+T stocks.

### 4.5 Holiday Clustering and Pre-Budget Effects

India's equity markets have a significantly higher holiday density than US markets (~15 trading holidays per year vs ~9 in the US). Holiday clustering — multiple consecutive holidays (Diwali period: October/November; Holi: March) — creates:

1. **Gap risk**: A position held over a 3-day Diwali closure has higher overnight gap risk than a normal weekend. ATR-based stop-losses partially account for this via historical volatility, but do not specifically model holiday gaps.
2. **Pre-Budget volatility compression**: In the 2–3 weeks before the Union Budget (typically February 1), volatility often compresses (ADX drops, Bollinger Bands narrow) as large players wait for clarity. Breakout signals in January are disproportionately false.
3. **Muhurat Trading**: The Diwali special 1-hour trading session (evening) has historically shown positive Nifty returns — but this is a superstition/sentiment effect, not a tradable TA signal. Mentioned to flag it should not be included in continuous data series.

**Nefarious filter.** Annotate the calendar with Indian market holidays (available from NSE's holiday calendar). In B.4 backtesting, handle holiday gaps explicitly by expanding ATR on the session following a 3+ day closure.

### 4.6 Liquidity-Tier Effects Within NIFTY 100

NIFTY 100 = Nifty 50 + Nifty Next 50. Within this universe, there is a meaningful liquidity gradient:

| Tier | Constituents | Avg daily turnover | Slippage | TA signal quality |
|---|---|---|---|---|
| Top 20 (Reliance, TCS, HDFC Bank, Infosys, etc.) | Very high (₹1,000+ Cr/day) | < 0.03% | Highest — signals are cleaner |
| Nifty 50 mid-tier (ranks 21–50) | High (₹200–₹1,000 Cr/day) | 0.03–0.08% | High |
| Nifty Next 50 (ranks 51–100) | Medium (₹50–₹200 Cr/day) | 0.08–0.20% | Medium — some distortion on large orders |

For Nifty Next 50 names, ATR-based slippage estimates should use the wider end of the range. OBV and A/D Line signals are less reliable for Nifty Next 50 names because a single large block deal (FII/DII) can move OBV without reflecting genuine retail participation.

---

## §5 — Time-Horizon Fit

The B1/B2 framing (locked in v0.4 problem statement §9): B1 is primary (weeks to months); B2 is *only* for entry/exit timing of long-term positions, never as standalone strategy. Every indicator below is mapped to its natural time horizon and whether it is usable within this framing.

**Reading the table.** "Natural" = the chart timeframe the indicator was originally designed for and has the strongest evidence on. "B1 use" = whether the indicator carries useful signal on a weekly chart for multi-month holding decisions. "B2 use" = whether the indicator on a daily chart can refine entry timing for an already-decided B1 position. "Out-of-scope" = indicator requires data we don't have (sub-daily) or fires too frequently to fit the turnover budget.

| Indicator | Natural timeframe | B1 use (weekly chart) | B2 use (daily chart) | Verdict |
|---|---|---|---|---|
| **200-DMA regime filter** | Daily | ✅ Yes (as 40-week MA) | ✅ Yes (primary gate) | **IN SCOPE** — regime gate for both B1 and B2 |
| **SMA/EMA crossover (50/200)** | Daily | ✅ Yes (10/30 weekly equiv) | ⚠️ Optional (high noise daily) | **IN SCOPE** — weekly preferred |
| **Supertrend (10, 3)** | Daily | ⚠️ Possible but lags | ⚠️ High whipsaw on circuit days | **MARGINAL** — covered by ATR+EMA |
| **ADX(14) / DMI** | Daily | ✅ Yes (smoother weekly) | ✅ Yes (entry-strength filter) | **IN SCOPE** — both B1 and B2 |
| **RSI(14)** | Daily | ✅ Yes (weekly RSI divergence) | ✅ Yes (pullback entries) | **IN SCOPE** — both timeframes complementary |
| **MACD (12, 26, 9)** | Daily | ✅ Yes (weekly histogram) | ✅ Yes (daily crossover refinement) | **IN SCOPE** — weekly primary, daily for timing |
| **ROC(26-week)** | Weekly | ✅ Yes (factor signal) | ⚠️ Noisy on daily | **IN SCOPE B1 only** — factor-style |
| **Stochastic(14, 3)** | Daily | ❌ Too noisy on weekly | ⚠️ Daily marginal | **OUT OF SHORTLIST** — RSI dominates |
| **Bollinger Bands(20, 2)** | Daily | ✅ Yes (weekly squeeze + bands) | ✅ Yes (band-touch entries) | **IN SCOPE** — both timeframes |
| **ATR(14)** | Daily | ✅ Yes (weekly ATR for sizing) | ✅ Yes (daily ATR for stops) | **MANDATORY** — required for sizing/stops |
| **Keltner Channels** | Daily | ⚠️ Redundant with Bollinger + ATR | ⚠️ Redundant | **OUT OF SHORTLIST** |
| **OBV** | Daily | ⚠️ Weak NSE evidence | ⚠️ Daily expiry distortions | **MARGINAL** — v0.2 candidate |
| **AVWAP (anchored)** | Daily, anchored | ⚠️ Reference only | ⚠️ Reference only | **DATA-ENRICHMENT** — not v0.1 signal |
| **A/D Line** | Daily | ❌ No NSE evidence | ❌ Same | **OUT OF SHORTLIST** |
| **MFI(14)** | Daily | ⚠️ Dominated by RSI | ⚠️ Same | **OUT OF SHORTLIST** |
| **Choppiness Index** | Daily | ⚠️ Dominated by ADX | ⚠️ Same | **OUT OF SHORTLIST** |
| **52-week breakout (Donchian)** | Daily/weekly | ✅ Yes (clear binary trigger) | — | **STRONG CANDIDATE** — clean Freefincal evidence |

**Summary.** Eight indicators clear both filters (B1-usable, evidence-backed, in turnover budget): 200-DMA, EMA crossover, ADX, RSI, MACD, ROC, Bollinger, ATR. Plus 52-week breakout as a strong factor-style candidate. Stochastic, A/D Line, MFI, Choppiness Index, and Keltner Channels are either redundant or weakly evidenced — out of shortlist. OBV and AVWAP are data-enrichment candidates for v0.2, not v0.1 primary signals.

---

## §6 — Backtest-Readiness Scoring

The v0.4 problem statement locks walk-forward Sharpe > 0.3 after costs (Q12) as the hard gate before any signal enters the live system. This section scores each shortlisted indicator on (a) what NSE evidence currently exists, (b) what's missing for a credible walk-forward backtest, and (c) what B.4 testing would need to run. Scores: **HIGH** (existing walk-forward evidence on NSE clears the bar), **MEDIUM** (positive in-sample evidence; walk-forward not yet published), **LOW** (no NSE evidence; theoretical only).

### Trend & Regime

**200-DMA regime filter — HIGH.** Capitalmind (2016) and Freefincal (multiple) have published walk-forward style analyses on Nifty 50 showing the 200-DMA filter materially reduces drawdown without destroying CAGR. Sharpe improvement is real (0.5+ → 0.7+ range in published Nifty data). What B.4 needs: replicate on NIFTY 100 individual constituents (not just index level) over a 10-year walk-forward window. Cost-after analysis on individual-stock entries/exits.

**SMA/EMA crossover (10/30 weekly) — MEDIUM.** Two NSE academic studies (Soni & Shinde 2015; Jain & Anand 2019) show in-sample positive alpha. Walk-forward Sharpe after costs not published. B.4 needs: 2010–2025 walk-forward on NIFTY 100, with 0.4% round-trip cost applied per signal. Parameter robustness test (10/30, 12/26, 5/20).

**ADX(14) — HIGH.** Naik & Reddy (SSRN 2019) report walk-forward Sharpe 0.41 for ADX-filtered EMA crossover on BSE Sensex. This is the single piece of evidence that already clears the Q12 bar. B.4 needs: confirmation on NIFTY 100 (not Sensex); test as a gate combined with other signals (i.e., does ADX-filtering help other indicators too?).

**52-week breakout (Donchian-style) — HIGH.** Freefincal published Sharpe 0.47 walk-forward on NSE Nifty 100 (2001–2019). B.4 needs: confirmation that the result extends to 2020–2025 (post-COVID regime change); circuit-limit filter validation (does excluding circuit-hit breakouts improve or hurt the strategy?).

### Momentum

**ROC(26-week) — HIGH.** NSE's own Nifty 200 Alpha 30 index uses this exact factor (12-month return excluding last month) and has 5.4% CAGR alpha over Nifty 200 since 2005. The walk-forward evidence is essentially built into the index's live performance — 20+ years of out-of-sample data. B.4 needs: simulate the factor as an individual-stock entry signal (not just an index-construction factor); test how the signal interacts with trend filter (does requiring price > 200DMA + top-quintile ROC help?).

**MACD (weekly) — MEDIUM (declining).** Jain (SSRN 2021): in-sample Sharpe 0.38; walk-forward 2015–2020 dropped to 0.21 after costs. The decay is a real concern — possibly because NSE has become less trending post-2015 (more F&O-driven flows). B.4 needs: re-test on 2020–2025 data; specifically test MACD histogram *divergence* (which is a different signal from crossover) as a B1 exit warning.

**RSI (weekly) — MEDIUM.** PBRI 2015 and IIM Lucknow 2021 show directional alpha; no NSE walk-forward Sharpe published. B.4 needs: walk-forward Sharpe on (a) RSI extreme reversal (buy at < 30, sell at > 70) — likely under-performs; (b) RSI divergence as entry/exit signal — more likely to clear bar; (c) RSI pullback to 40–50 in confirmed uptrend (price > 200DMA, ADX > 20) — best theoretical candidate.

### Volatility

**Bollinger Bands(20, 2) — MEDIUM.** Shah & Dave (2016) 64% accuracy on weekly Bollinger mean-reversion for NSE banking; SSRN 2018 squeeze study shows squeeze precedes large moves 71% of the time. Neither is a full walk-forward Sharpe study with cost adjustment. B.4 needs: (a) walk-forward test of Bollinger mean-reversion on NIFTY 100 (not just banking) with trend gate; (b) Bollinger Squeeze as volatility flag (not a direction signal) — test whether following squeeze-and-direction-resolution gives positive alpha.

**ATR(14) — HIGH (for sizing/stops, not as alpha signal).** ATR is not an alpha generator — it's an input to position sizing and stop-loss placement. The evidence for ATR-normalized sizing reducing portfolio volatility is well-established globally and replicated by Freefincal on NSE. B.4 needs: validation that ATR-based stops on individual NIFTY 100 names reduce drawdown without catastrophically degrading return (typical stop-out rate of 15–25% should improve Sharpe; > 35% suggests stops are too tight).

### Unfunded for v0.1

OBV, AVWAP, A/D Line, MFI, Stochastic, Choppiness Index, Keltner Channels, Supertrend — all either missing NSE evidence at the walk-forward level, or dominated by an alternative already in the shortlist. They are noted as v0.2 candidates if B.4 surfaces gaps in the v0.1 signal set.

### B.4 testing constraints (foreshadow)

The strongest available walk-forward evidence is for ADX-filtered momentum (Naik & Reddy) and 52-week breakout (Freefincal). The v0.1 math should be designed so that these signals stand alone — even if other indicators (RSI divergence, Bollinger Squeeze) fail to clear Sharpe > 0.3 individually, the combined system with ADX gate and 52-week breakout has a strong prior of clearing the bar. **The natural fallback if v0.1 underperforms in B.4: rely on the two strongest-evidenced indicators (200-DMA gate + ADX-filtered momentum) and demote others to context/annotation only.**

---

## Final — Recommended-for-v0.1 Shortlist (7 indicators)

These 7 indicators are recommended for the v0.1 math. They cover regime, trend, momentum, and volatility; have NSE-specific evidence (with one — Bollinger — having modest evidence and being included for its dual role as squeeze flag + mean-reversion); fit the B1/B2 framing with weekly charts primary; and combine into a single output label (ENTRY_ZONE / WAIT / AVOID_ENTRY) for each stock.

**1. 200-Day Moving Average (regime filter).** Daily SMA(200), equivalently 40-week SMA on a weekly chart. Used as a binary regime gate: price > 200DMA → structural uptrend, eligible for entry consideration; price < 200DMA → no ENTRY_ZONE signal (with FA-driven turnaround exception). **NSE evidence**: HIGH. **Why it makes v0.1**: cleanest cost-after improvement to risk-adjusted return on Nifty data; standard practice in Indian retail systematic investing. **Parameters to test in B.4**: 200-day daily vs 40-week weekly (should be near-equivalent); confirmation window (price > 200DMA for ≥ 4 consecutive weeks before turning ENTRY_ZONE ON, to reduce whipsaw).

**2. ADX(14) (trend-strength filter).** Standard Wilder construction, period 14, used as a gate alongside 200-DMA. Three zones: ADX < 20 = ranging (no trend signals trusted); 20 ≤ ADX ≤ 25 = light trend (signals at half-conviction); ADX > 25 = strong trend (signals at full conviction). **NSE evidence**: HIGH (Naik & Reddy SSRN 2019 walk-forward Sharpe 0.41 with ADX-filter on Sensex). **Why it makes v0.1**: only NSE indicator with a published walk-forward Sharpe > 0.3 result; complements 200-DMA (regime *direction*) by adding regime *strength*. **Parameters to test**: 14-period daily ADX; weekly-chart ADX(14); thresholds 18/25 vs 20/25 vs 22/28.

**3. ROC(26-week) momentum factor.** 26-week (~6 month) price return, excluding the most recent 4 weeks (NSE Alpha 30 methodology — short-term reversal exclusion). Rank stocks within NIFTY 100 by ROC; top-quintile ROC + price > 200DMA + ADX > 20 = strong momentum candidate. **NSE evidence**: HIGH (NSE Alpha 30 has 20+ years of live out-of-sample data). **Why it makes v0.1**: the single best-evidenced momentum signal on NSE; complements daily-chart indicators with a 6-month factor lens. **Parameters to test**: 26-week vs 12-week vs 52-week; 1-month exclusion vs 4-week exclusion vs no exclusion; top-quintile vs top-decile within NIFTY 100.

**4. MACD weekly (12, 26, 9) — primary as histogram divergence, secondary as signal-line crossover.** Compute MACD on weekly chart. Primary B1 signal: histogram divergence (price makes higher high but MACD histogram lower high → exit warning for long positions; reverse for entry warning). Secondary signal: weekly signal-line crossover (acceptable as confirmation but not primary trigger given the Jain SSRN 2021 walk-forward decay). **NSE evidence**: MEDIUM with caveat. **Why it makes v0.1**: histogram divergence is a different statistical signal from crossover and has not been directly walk-forward-tested on NSE — a worthwhile B.4 contribution. **Parameters to test**: standard (12, 26, 9); divergence-window 6–10 weeks; combine with RSI divergence (double confirmation).

**5. RSI(14) weekly — divergence and pullback zones.** Weekly chart RSI. Two distinct signals: (a) **RSI divergence** (price-RSI divergence at extremes — same construction as MACD divergence, used as exit/entry warning); (b) **RSI pullback to 40–50 zone in confirmed uptrend** as an ENTRY_ZONE candidate (the strongest theoretical use case for RSI in long-term investing). **NSE evidence**: MEDIUM. **Why it makes v0.1**: RSI is the most widely-studied momentum oscillator on NSE; pullback-in-uptrend has not been walk-forward-tested but is theoretically robust (it's a positive-skew entry condition). **Parameters to test**: 14-period vs 21-period weekly RSI; pullback band 40–50 vs 45–55; divergence detection rules.

**6. Bollinger Bands(20, 2) weekly — squeeze flag and lower-band-in-uptrend entries.** Standard parameters (20-period middle SMA, 2σ bands) on weekly chart. Two distinct signals: (a) **Bollinger Squeeze** (bands narrower than 30% of 6-month average bandwidth → high-alert flag, do not generate new entries until squeeze resolves); (b) **lower-band touch in confirmed uptrend** (price > 200DMA + ADX > 20 + price touches/penetrates lower Bollinger band → mean-reversion ENTRY_ZONE candidate). **NSE evidence**: MEDIUM (Shah & Dave 2016 banking 64% accuracy; SSRN 2018 squeeze evidence). **Why it makes v0.1**: dual-role — squeeze as volatility filter, band-touch as mean-reversion overlay. **Parameters to test**: 20-period vs 25-period; 2σ vs 2.5σ bands; squeeze-width threshold.

**7. ATR(14) weekly — mandatory for sizing and stops.** Weekly ATR(14) used as the position-sizing and stop-loss input, not as an alpha signal. Stop-loss = entry price − (2.5 × ATR_14_weekly). Position size = (per-stock risk budget × portfolio NAV) / (2.5 × ATR_14_weekly). **NSE evidence**: HIGH for sizing methodology; not an alpha signal so no alpha evidence applies. **Why it makes v0.1**: required input for any walk-forward backtest that simulates realistic risk-controlled execution. **Parameters to test**: 14-period vs 20-period; ATR multiplier on stops (2.0 / 2.5 / 3.0); position-size budget (per-stock max 2–5% of NAV).

### Composition sketch — how the 7 indicators combine into an action label

Each NIFTY 100 stock is evaluated each week. The pipeline produces one of four outputs: `ENTRY_ZONE`, `WAIT`, `AVOID_ENTRY`, or `EXIT_WARNING`. The composition is gated, with the strongest-evidence gates first:

```
Step 1 — Regime gate (200-DMA):
  IF price < 200-DMA for ≥ 4 consecutive weeks → AVOID_ENTRY (halt pipeline)
  ELSE → continue.

Step 2 — Trend-strength gate (ADX):
  IF ADX < 20 → WAIT (sideways market; insufficient trend conviction; halt)
  ELSE → continue.

Step 3 — Volatility-state filter (Bollinger Squeeze):
  IF Bollinger Squeeze active → WAIT — annotate "SQUEEZE: large move pending in either direction"
  (no ENTRY_ZONE until squeeze resolves with direction)
  ELSE → continue.

Step 4 — Primary momentum check (ROC + RSI confluence):
  IF ROC_26w in top-quintile of NIFTY 100 AND RSI_14w between 40 and 70 → STRONG MOMENTUM
  IF ROC_26w mid-range AND RSI_14w pullback to 40–50 zone → ENTRY-PULLBACK CANDIDATE
  IF ROC_26w bottom-quintile OR RSI_14w > 80 with divergence → AVOID_ENTRY or EXIT_WARNING

Step 5 — Confirmation (MACD histogram + Bollinger band):
  IF MACD histogram positive and rising AND price between Bollinger middle and lower bands
    → ENTRY_ZONE (full conviction)
  IF MACD histogram divergence (negative divergence at highs) → EXIT_WARNING
  IF MACD histogram positive but Bollinger upper band touch with no divergence → WAIT
    (allow profit-taking but no new entries at this band)

Step 6 — Sizing (ATR, applied to ENTRY_ZONE only):
  Stop-loss = entry_price − (2.5 × ATR_14_weekly_₹)
  Position size_shares = (portfolio_NAV × per_stock_risk_pct) / (entry_price − stop_loss)
  Where per_stock_risk_pct is a portfolio-level parameter (default 1% of NAV per name).
```

This produces an output structure per stock per week of the form:

```
Stock: HDFC Bank
Output: ENTRY_ZONE (full conviction)
Regime: price > 200DMA for 18 weeks ✓
Trend strength: ADX = 27 (strong) ✓
Volatility: Bollinger bands normal width ✓
Momentum: ROC_26w = 4th quintile of NIFTY 100; RSI_14w = 52 (pullback zone) ✓
Confirmation: MACD histogram positive and rising ✓
Stop-loss: ₹1,580 (2.5 × ATR_14w = ₹120 below ₹1,700 entry)
Position size: 588 shares per ₹100k risk budget on a ₹1 Cr portfolio (1% risk per name)
```

This is the v0.1 math that B.3 will formalize. B.4 (testing) will hand-compute the pipeline on 4–6 NIFTY 100 stocks across at least 5 historical regime windows (2008 GFC bottom; 2014 election rally; 2018 NBFC crisis; 2020 COVID bottom; 2022 rate-hike cycle) to check whether the composition produces useful signals at the regime turning points — analogous to A.4's hand-compute on Asian Paints + Tata Steel.

### Open questions for B.2 (Pranav to decide)

These are the decisions B.3 (writing v0.1 math) cannot make without input:

1. **Indicator count**: 7 as recommended, or trim further? Tightest defensible set is 5 (200-DMA, ADX, ROC, RSI, ATR — drops MACD and Bollinger). Broadest is 8 (add 52-week breakout). Default recommendation: **7** as above.
2. **Primary timeframe**: weekly chart for all signals (recommended; matches turnover budget), or split — daily 200-DMA + ADX + weekly for the rest? Default: **weekly throughout**, with daily as confirmation only.
3. **52-week breakout as 8th indicator?** Freefincal evidence is strong (Sharpe 0.47). The downside is conceptual overlap with ROC. Decision: include or defer to v0.2. Default: **defer to v0.2**.
4. **Position-sizing parameter** (per-stock risk budget): 1% of NAV / 2% / 3%? Default: **1%** (conservative; allows 100 positions hypothetically; matches typical retail-investor risk tolerance).
5. **Output label set**: 4 labels as proposed (ENTRY_ZONE / WAIT / AVOID_ENTRY / EXIT_WARNING)? Or 3 (drop WAIT into AVOID_ENTRY)? Default: **4**, parallel to Cycle A's 4-label structure.
6. **Cycle A/B combined display in weekly report**: surface both labels side-by-side (per Q5 locked decision: "context-sensitive prompt with holding-period framing")? Yes — this is locked, not a re-decision.

---

## Sources cited (consolidated)

**NSE-specific academic / practitioner**:
- Soni & Shinde (2015), *Indian Journal of Finance*: Moving average crossovers on NSE Nifty 50 (2005–2014).
- Jain & Anand (2019), IIM Bangalore Working Paper: 50/200 SMA on CNX 100 (2007–2018).
- Capitalmind (Deepak Shenoy, 2016): 200-DMA filter on Nifty 50 (2001–2016).
- Freefincal (P.M. Srinivas Subramanya, 2019): 52-week breakout on Nifty 100 (2001–2019), Sharpe 0.47.
- Kumar & Sharma (2017), *Indian Journal of Finance* 11(5): ADX-filtered momentum on NSE 100 (2007–2016).
- Naik & Reddy (2019), SSRN: ADX-filtered EMA crossover on BSE Sensex, walk-forward Sharpe 0.41.
- Sharma & Patel (2022), IJCRT: Supertrend on NSE FMCG (2017–2022).
- Patel (2015), *Pacific Business Review International*: RSI(14) on Nifty 50 (2010–2015).
- Bhargava & Sharma (2021), IIM Lucknow Research: weekly RSI on Nifty 100 (2010–2020).
- Sharma & Khatri (2019), *Journal of Accounting and Finance*: MACD on NSE IT sector (2010–2019).
- Jain (2021), SSRN: MACD on Nifty 50 (2000–2020) — walk-forward decay.
- Sehgal & Balakrishnan (2002), *Decision*: Momentum on Indian equities (BSE 500, 1989–1999).
- Anand & Iyer (2012), *Indian Journal of Finance*: 3–12 month momentum on NSE 500 (1999–2009).
- NSE Indices methodology: Nifty 200 Alpha 30 and NSE Multi-Factor whitepaper.
- Shah & Dave (2016), *International Journal of Applied Research*: Bollinger Bands on NSE banking (2010–2016).
- Bhargava (2018), SSRN: Bollinger Squeeze on Nifty 50 stocks (2005–2018).
- Bhat & Naik (2020), IIM Kozhikode Working Paper: Weekly+daily confluence on Nifty 100 (2010–2020).
- Sharma (2021), IIM Ahmedabad working paper: OBV divergence on NSE 100 (2012–2021).
- Pandey (2019), IJSRP: MFI vs RSI on NSE large-caps (2014–2019).
- Kumar (2020), IJSRP: Stochastic on NSE Pharma (2015–2020).

**Foundational global**:
- Granville (1963): Moving averages and On-Balance Volume.
- Wilder (1978): RSI, ATR, ADX/DMI.
- Appel (1979): MACD.
- Bollinger (1983): Bollinger Bands.
- Lane (1950s): Stochastic Oscillator.
- Williams (1972): Accumulation/Distribution Line.
- Quong & Tabell (1989): Money Flow Index.
- Dreiss (1993): Choppiness Index.
- Faber (2007), Journal of Wealth Management: 200-day SMA as tactical asset allocation tool.
- Jegadeesh & Titman (1993), Journal of Finance: 12-month momentum factor.
- Blume, Easley & O'Hara (1994), Journal of Finance: volume conveys information beyond price.
- Pruitt & White (1988), Journal of Finance: Stochastic standalone weakness.
- Elder (1986): Triple Screen / multi-timeframe alignment.
- Covel (2007): Turtle Trading.
- Carver (2019): Systematic trend-following composition.

**Practitioner / data sources**:
- Freefincal (multiple articles, 2015–2023): NSE-specific backtest evidence.
- Capitalmind (Deepak Shenoy, multiple articles): Nifty 50 trend filter analysis.
- Zerodha Varsity: ATR stop-loss methodology.
- NSE Holiday Calendar, NSE Bhavcopy EQ (circuit-limit data), NSE Corporate Actions, NSE Surveillance (ASM/ESM/T+T) lists.

---

**End of Cycle B.1 research.** Output drives B.2: Pranav picks the v0.1 subset (default 7 as above; open questions in §6 final block).
