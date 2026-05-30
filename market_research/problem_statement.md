# Problem Statement — Debate & Evolution

**Status**: 🟡 In debate (not locked)
**Started**: 2026-05-30

---

## 0. The raw prompt (what Pranav said)
> "I need to create an investment planning bot, which gathers technical analysis data and fundamental analysis data and then look at my portfolio and help me fix it, make it better so that I get better returns out of my shares."
> + NSE only, portfolio later, research first.

This is a **direction**, not yet a **problem statement**. Three words need surgical definition: *fix*, *better*, *returns*.

---

## 1. Why this isn't yet a problem statement
A good problem statement has 5 ingredients:
1. **Who** has the problem (user/persona)
2. **What** specific pain they have today
3. **Why** existing solutions don't solve it (the gap)
4. **What** "solved" looks like (the outcome)
5. **Constraints** (scope, budget, time, regulation)

The raw prompt gives us roughly #1 (Pranav) and #4 (better returns), but #2, #3, and #5 are wide open. Below are the axes we need to nail down.

---

## 2. The seven axes of the problem

### Axis A — User scope
| Option | Description | Implication |
|---|---|---|
| **A1** | Just Pranav, his portfolio | Personal tool; no UI polish; tuned to one person's style. |
| **A2** | Pranav + small circle (friends/family) | Light multi-user; still personal-grade. |
| **A3** | Generic Indian retail investor | Productizable; needs onboarding, account model, regulatory care. |

> *Pranav explicitly mentioned wanting to check **product-market fit**, which leans toward A2 or A3. But the immediate utility ("fix MY portfolio") leans toward A1. Possible path: build A1 first, then generalize.*

### Axis B — Time horizon
| Option | Style | Math/Tools used |
|---|---|---|
| **B1** | Long-term investing (months–years) | Heavy fundamentals; valuation models (DCF, P/E, P/B); macro. |
| **B2** | Swing trading (days–weeks) | Mixed TA + FA; trend-following, breakout, momentum. |
| **B3** | Intraday (minutes–hours) | Pure TA; needs real-time data + low-latency infra. |
| **B4** | Multi-horizon | Bot serves different lenses for different sleeves of portfolio. |

> *Indian retail equity holdings are typically swing-to-long-term. Intraday usually needs broker-level latency. Likely B1 or B1+B2.*

### Axis C — Asset universe
| Option | Set | Count |
|---|---|---|
| **C1** | NIFTY 50 | 50 |
| **C2** | NIFTY 500 | 500 |
| **C3** | All NSE equities | ~2000 |
| **C4** | C1/C2/C3 + ETFs/MFs | + ~150 |
| **C5** | Above + derivatives (F&O) | Adds complexity, leverage, expiry math |

> *NIFTY 500 is a sweet spot — covers ~95% of market cap, liquid, large enough to find ideas, small enough to compute on.*

### Axis D — Decision scope (what the bot actually outputs)
| Option | Output type |
|---|---|
| **D1** | Hold/buy-more/trim/sell calls on **existing** positions |
| **D2** | + New entry ideas (idea generation from universe) |
| **D3** | + Portfolio rebalancing (allocations across positions) |
| **D4** | + Risk management (stop-loss, position sizing, hedging) |
| **D5** | + Tax-aware (LTCG/STCG, harvest opportunities) |

> *Pranav's wording "fix my portfolio" most directly maps to D1+D3+D4. D2 (idea generation) is the natural extension. D5 (tax) is a separate axis but huge for Indian investors.*

### Axis E — Automation level
| Option | Description |
|---|---|
| **E1** | Advisory only — bot recommends, Pranav decides & executes manually |
| **E2** | Semi-auto — bot generates orders, Pranav approves one-click |
| **E3** | Fully auto — bot executes via broker API (Kite/Upstox/etc.) |

> *SEBI regulation: only SEBI-registered RIAs / RAs can give personalized advice for compensation. E3 ("algo") requires NSE-approved strategies for retail. **E1 is by far the safest starting point** — for self-use, no regulatory exposure.*

### Axis F — Math & methodology surface
What the user can plug into the bot:
- **F1** Technical indicators: SMA/EMA, RSI, MACD, Bollinger, ATR, Ichimoku, VWAP, OBV
- **F2** Fundamental ratios: P/E, P/B, ROE, ROCE, D/E, Interest coverage, FCF yield
- **F3** Valuation models: DCF, Graham number, PEG, residual income
- **F4** Portfolio theory: MPT (Markowitz), Black-Litterman, Risk parity, HRP
- **F5** Factor models: Fama-French (value, size, momentum, quality, low-vol)
- **F6** Statistical: cointegration, mean reversion, Z-scores, GARCH
- **F7** ML/AI: tree models, LSTM (cautioned), LLM-reasoning-over-signals

> *Pranav has said he'll guide which subset of F1–F7 to use. The bot's job is to **expose these as tools** the user can compose, not to silently pick a strategy.*

### Axis G — Success metric (how we judge "better returns")
| Option | Metric |
|---|---|
| **G1** | Absolute return (₹) |
| **G2** | CAGR vs NIFTY 50 (alpha) |
| **G3** | Sharpe / Sortino (risk-adjusted) |
| **G4** | Max drawdown (downside protection) |
| **G5** | Composite scorecard (G2 + G3 + G4) |

> *"Better returns" naively means G1, but no serious investor uses absolute return alone — a 30% gain in a year the index made 40% is **underperformance**. G5 is the honest answer.*

---

## 3. Claude's proposed working statement (v0.1)

> **For an Indian retail investor (initially Pranav himself) holding a portfolio of NSE-listed equities, build an AI-powered planning assistant that ingests the portfolio plus market data (technical + fundamental) and produces a prioritized, reasoned action plan — covering hold/buy/trim/sell decisions on existing positions, rebalancing suggestions, and risk controls — optimized for benchmark-beating, risk-adjusted returns. The user supplies methodology preferences (which indicators, which valuation models, which weights); the bot composes them into a workflow, computes the signals, explains its reasoning, and outputs an action plan that the user reviews and executes manually. NIFTY 500 universe. Long-term + swing horizon. Advisory only — no auto-execution. Phase-1 deliverable is the planner for Pranav's own portfolio; productization decided after PMF analysis.**

This pins:
- A1 → A3 path (start with A1)
- B1 + B2
- C2 (NIFTY 500)
- D1 + D3 + D4 (skip D2/D5 in v1, revisit)
- E1 (advisory only)
- F1–F5 exposed; F6/F7 optional
- G5 (composite metric)

---

## 4. Where I'd push back if I were the user

### 4a. "Advisory only" might be too weak
If the bot just produces a 20-page reasoning report and Pranav ignores half of it, it adds no value over Screener.in. A **forcing function** is needed — e.g., the bot ranks actions by expected utility and Pranav must dispose of each (do / skip / snooze).

### 4b. "Better returns" is a trap
Most retail investors who say "better returns" actually want **fewer mistakes**: avoiding panic sells, avoiding holding losers too long, avoiding concentration risk, avoiding chasing tips. The bot's primary value may be **bias-correction**, not alpha. Worth a separate problem statement option.

### 4c. The TA+FA combo is harder than it sounds
TA and FA give signals on different time scales and often contradict. A clean fundamental buy can be in a clean technical downtrend. The bot needs a **conflict-resolution rule** — that's a strategy choice Pranav must make explicit.

### 4d. PMF question is premature for v1
You can't really assess PMF for a single-user tool. PMF research is useful as **future-proofing** (so we don't build something unscalable), but the v1 problem statement should be ruthlessly Pranav-focused.

---

## 5. Alternative framings worth considering

### Framing X — "Bias-correction co-pilot"
> Build a bot that watches Pranav's portfolio and flags **behavioral and statistical anomalies** (over-concentration, anchored losers, momentum-decayed holds, sector drift, position-sizing violations). Less "tell me what to buy", more "tell me what I'm doing wrong".

### Framing Y — "Strategy composer"
> Build a bot that lets Pranav **express investment strategies as code/config** (e.g., "buy when RSI<30 AND P/E<sector_median AND ROE>15%") and then continuously evaluates his portfolio + universe against the active strategies, surfacing matches and violations.

### Framing Z — "Portfolio doctor"
> Periodic (weekly/monthly) **health check**: scores the portfolio on diversification, valuation, momentum, quality, and risk; produces a diagnosis + prescription. Reactive on user demand, not continuous.

> *Framing X + Z combined might be the highest-leverage starting product, because it's deeply useful even with simple math, and it generalizes well to other users.*

---

## 6. Open for Pranav
Pranav needs to weigh in on:
1. Which **axis options** (A–G above) feel right?
2. Which **framing** (Claude's v0.1, or X / Y / Z, or hybrid)?
3. Anything I haven't considered (e.g., specific personal pain points with current investing process)?

---

## 7. Evolution log (will be appended as we debate)
- **v0.1 (2026-05-30)** — Initial Claude draft above. Awaiting Pranav's pushback.
