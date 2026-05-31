# 08 — Decisions Locked, v0.4 Problem Statement

**Status**: 🔒 LOCKED at v0.4
**Date (v0.3)**: 2026-05-30
**Date (v0.4 update)**: 2026-05-31
**Authorized by**: Pranav

---

## Changelog (v0.3 → v0.4)

Cycle A.6 idea-review surfaced one borderline clarification from the A.5 critic synthesis (Theme G — BFSI silent-skip product gap; Pranav's Q7 = YES). v0.3 said *"Asset universe: Direct equity NIFTY 500 for fundamentals"*, but v0.1 math silently skipped all BFSI companies (∼35–40% of NIFTY 500 by market cap). The math vs problem-statement were out of sync.

**v0.4 changes** (one paragraph added; everything else unchanged):

- **§8 Asset universe**: added explicit BFSI staging sentence — *"Cycle A FA pipeline covers NIFTY 500 including BFSI; v0.2 delivers a BFSI stub (trend indicators: NIM, GNPA, PCR, CAR) with a full BFSI sub-pipeline scheduled for v0.3."*

No changes to Q1–Q12 locked answers, no changes to Constraints X / Y / Z, no changes to any other section. Q7 (Sharing) note: as of 2026-05-31 the GitHub repo and Medium blog #1 are public, narrowing Q7's "strictly personal" from "no public artifacts" to "no shared output / code / signals / recommendations" — the journey is public; the system is not. This is consistent with the original intent; no formal v0.5 needed.

---

## Critical scope updates (beyond Q1–Q12)

Pranav added three structural constraints not in the original 7 axes. These are project-defining; everything else is downstream.

### Constraint X — No trading, no F&O. Investments only.
- **Allowed**: Direct equity (NSE), Mutual Funds (equity, hybrid, debt).
- **Excluded**: F&O, intraday, margin, leveraged anything.
- **Implication**: Time horizon B is now locked **B1 primary, B2 only for entry/exit timing of long-term positions**, not as a strategy in itself.
- **Implication**: Reframes the bot as an *investor's planning tool*, not a trader's signal engine. Lowers TA prominence; raises FA + portfolio construction prominence.

### Constraint Y — Mutual funds in the asset universe.
- **Was**: NSE direct equity only.
- **Now**: NSE direct equity **+ Indian Mutual Funds**.
- **Implication**: New data source — AMFI NAV history + monthly portfolio disclosures. Different analytics layer: expense ratio (TER) drift, portfolio overlap with direct equity (concentration risk), category-relative return percentile, manager-tenure analysis, direct-vs-regular plan analysis, tax efficiency (equity ≥65% gets equity-LTCG treatment; debt MF taxed at slab post-Budget 2023).
- **Implication**: TA largely doesn't apply to MFs. MF analysis = FA + portfolio theory + cost analysis.

### Constraint Z — Staged rollout: paper → test → live.
- **Stage 1 — Paper money**: Bot recommends, we simulate execution, track simulated outcomes. No real portfolio.
- **Stage 2 — Test portfolio**: 20–25 real NSE holdings + a few MFs as a representative dummy. No live money attached.
- **Stage 3 — Live portfolio**: Bot reads Pranav's actual Kite portfolio. Advisory-only output, manual execution.
- **Implication**: Phase 2 must include a paper-trading simulation engine as a first-class deliverable (not an afterthought). The bot must produce identical output across stages — only the source-of-truth changes.

---

## Locked answers (Q1–Q12)

| # | Question | Answer | Notes / Notable choices |
|---|----------|--------|--------------------------|
| 1 | Phase 1 horizon | **(b)** Pranav-only 3 months → PMF eval with 5–10 users | Milestone gate: **2026-08-30** |
| 2 | Test portfolio | **Staged**: paper → test (20–25 real holdings, no money) → live | See Constraint Z |
| 3 | Exit rules | **(c)** Bot proposes default framework; user modifies | Phase 2 must produce the default framework |
| 4 | Success metric | **(d)** Composite: behavioral flags acted + stop-loss adherence + Sharpe improvement | All three logged from Stage 1 (paper) |
| 5 | TA/FA conflict | **(d)** Context-sensitive prompt with holding-period framing | LLM never silently picks; always surfaces conflict |
| 6 | Position sizing | **(c)** Direction + size + correlation-to-portfolio calculation | Adds covariance matrix requirement |
| 7 | Sharing | **(a)** Never — strictly personal | No screenshots, no GitHub publish in Phase 1 |
| 8 | Data sources | **(d)** Kite + bhavcopy combination | **+ AMFI NAV** (added for Constraint Y) |
| 9 | Output format | **(d)** Structured report primary + chat drill-down | Weekly cadence default |
| 10 | Entry price display | **(c)** Thesis-entry framing, not P&L anchor | "Thesis intact? Y/N" UX |
| 11 | Tax awareness | **(a)** LTCG/STCG calculator in v1 — full feature | **STRICTEST option** — factored into sell recommendations |
| 12 | Backtest gate | **(b)** Walk-forward, 3yr NSE data, Sharpe > 0.3 after costs | **STRICTEST option** — hard gate before any signal enters the system |

### Why Q11 and Q12 matter most
- **Q11** elevates tax-awareness from "nice-to-have v2" to "core v1". A sell recommendation that ignores ₹40k of avoidable LTCG is wrong, regardless of how good the signal is. The tax engine becomes a required part of the recommendation pipeline.
- **Q12** is the strictest possible answer. It means **no signal can enter the live system without empirical NSE-specific validation**. Every TA indicator, every FA threshold, every MF screening rule passes through walk-forward backtesting first. This makes the backtest infrastructure (sub-task 2D in Phase 2) the **critical-path deliverable** that gates Stage 2 and Stage 3.

---

## Problem Statement v0.3 (LOCKED)

For **Pranav**, an Indian retail investor holding a portfolio of **NSE-listed direct equities and Mutual Funds**, build an AI investment planning assistant that:

1. **Ingests** the portfolio at three rollout stages — Stage 1 paper-only, Stage 2 real-holdings-no-money, Stage 3 live via Kite — plus market data (Kite for quotes, NSE bhavcopy for historical OHLCV, AMFI for MF NAVs and disclosures).

2. **Produces a weekly structured investment health report** that identifies, per holding:
   - Action label (REVIEW / WATCH / HOLD) with 2–3 sentence reasoning
   - Stop-loss / exit-rule violations against the user's pre-stated framework (which the bot helps the user define in onboarding)
   - Behavioral bias flags: disposition effect, anchoring, concentration risk, exit-rule violations
   - MF-specific flags: expense ratio drift, portfolio overlap with direct equity, category-underperformance, manager change, tax inefficiency
   - Position sizing recommendation with correlation-to-portfolio impact
   - LTCG/STCG tax implications of any suggested sell
   - Layered chat drill-down for any flagged position

3. **Surfaces TA/FA conflicts explicitly** — when signals disagree on the same holding, the bot does NOT silently pick one. It prompts the user with their holding period as context and asks for a weight decision.

4. **Operates LLM as a reasoning and explanation layer ONLY** — never as a signal generator. All signals computed in Python; LLM articulates them, contextualizes them against the user's stated rules, surfaces conflicts. Output language is "analysis" framing ("Your RSI is 72; historically this has preceded corrections"), never "advice" framing ("Sell 30% of HDFC Bank").

5. **Gates all live use behind walk-forward backtest validation** — no signal enters the recommendation pipeline without out-of-sample Sharpe > 0.3 (after costs: STT, brokerage, slippage, GST, taxes) on 3 years of NSE data.

6. **Operates advisory-only** — no auto-execution, no order placement. Output is informational; Pranav executes manually if he chooses.

7. **Measures itself behaviorally**: stop-loss adherence rate, disposition-effect inventory reduction (count of anchored loss-holders disposed of after flag), recommendation-to-review engagement rate. Sharpe improvement is a secondary metric.

8. **Asset universe**:
   - Direct equity: NIFTY 500 for fundamentals; **NIFTY 100 restricted for TA signals in v1** (expand to NIFTY 500 in v2 after NSE-specific validation)
   - **BFSI staging** (added v0.4): *Cycle A FA pipeline covers NIFTY 500 including BFSI; v0.2 delivers a BFSI stub (trend indicators: NIM, GNPA, PCR, CAR) with a full BFSI sub-pipeline scheduled for v0.3. No silent skips on banking/NBFC/insurance/other-financial-services names in real-portfolio output.*
   - Mutual funds: All Indian MFs (equity, hybrid, debt) — analyzed via FA + portfolio theory + cost analysis (no TA)

9. **Time horizon**: Long-term (B1) primary. Swing (B2) used only for entry/exit timing of long-term positions, not as a strategy. **No trading. No F&O.**

10. **Regulatory posture**: Strictly personal, Pranav-only, no sharing of output, code, or recommendations in Phase 1. Productization gate at 2026-08-30.

Phase 1 deliverable: Pranav's personal investment planning assistant, deployed through Stages 1 → 2 → 3.

---

## What's left to design
Phase 2 plan is in `09_phase_2_plan.md`.
