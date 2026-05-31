# 09 — Phase 2 Plan: Research, Math, Test, Review, Refine (v0.2)

**Status**: ⏳ Tasks created, awaiting Pranav's go-ahead to start Cycle A
**Date**: 2026-05-30
**Goal**: Refine the **plan, idea, and math** through iterative research/test/review cycles. **No implementation.** No data engineering. No architecture. No UX specs. No code. Math + thinking + plans only.

---

## The cycle (run once per scope area)

```
1. RESEARCH        — what math exists, evidence on NSE, sources
                     ↓
2. PRANAV PICKS    — which subset goes into v0.1 (conversation, recorded in session log)
                     ↓
3. WRITE MATH v0.1 — formulas, thresholds, composition rules
                     ↓
4. TEST MATH v0.1  — worked examples on 10–20 NSE stocks across regimes
                     ↓
5. CRITIQUE v0.1   — multi-agent critics attack math + test results
                     ↓
6. REFINE → v0.2   — incorporate critiques + idea review (does v0.3 problem statement → v0.4?)
                     ↓
   LOOP 4–6 until math is stable
                     ↓
7. CYCLE CLOSES    — math locked at v0.x (still 0.X); next cycle begins
```

## Versioning rules (locked)
- **Everything stays in v0.X.** No v1.X anywhere in Phase 2.
- Problem statement: v0.3 → v0.4 → v0.5 ... per cycle-end idea review.
- Math specs: v0.1 → v0.2 → v0.3 ... per refinement.

## What "test" means (and does NOT mean)
- ✅ Hand-compute or notebook-compute the formulas on real historical examples
- ✅ Use libraries (pandas, ta-lib) only to *compute* the math
- ❌ Build a backtest engine
- ❌ Wire data pipelines
- ❌ Design architecture / schemas / runners
- ❌ Any code that resembles "the bot"

The math is on trial. The system is not.

---

## The 6 cycles (sequential)

| ID | Cycle | Scope |
|---|---|---|
| **A** | Equity Fundamental Analysis | Value/quality ratios (P/E, P/B, ROE, ROCE, D/E, FCF, sector-relative), value/quality frameworks (Graham, Greenblatt Magic Formula, Piotroski F-Score, Altman Z, Buffett/Munger, coffee-can). |
| **B** | Equity Technical Analysis | TA indicators (RSI, MACD, 200DMA, Bollinger, OBV, ATR, Supertrend, ADX), restricted to NIFTY 100. |
| **C** | Mutual Fund Analytics | Expense ratio drift, overlap with direct equity, category-percentile, manager tenure, direct vs regular, tax-bucket math. No TA. |
| **D** | Portfolio Construction & Sizing | Half-Kelly, correlation-to-portfolio impact (Q6), HRP, concentration/sector exposure. Equity + MF unified. |
| **E** | Exit Rules + Tax-Aware Math | Stops (hard, trailing), FA-deterioration triggers, TA exits, time-based, MF-specific exits, LTCG/STCG (Q11) factored. |
| **F** | Signal Combination + Behavioral Metrics | TA/FA conflict resolution math (Q5, holding-period sensitive), aggregation across A–D, behavioral-metric formulas (Q4). |

**Order**: A → B → C → D → E → F. Each gated by the previous one closing.

## File naming convention
Per cycle, files numbered 10–17 (Cycle A), 20–27 (B), 30–37 (C), etc.:
- `N0_cycle_X_research.md`
- `N1_cycle_X_math_v0.1.md`
- `N2_cycle_X_test_v0.1.md`
- `N3_cycle_X_critiques_v0.1.md`
- `N4_cycle_X_math_v0.2.md` (and further iterations)
- ...

## Task structure
- 6 cycle-header tasks (1 per cycle) — for visibility
- 6 step-tasks per cycle (research → refine), created when cycle starts
- Currently created: Cycle A header (#15) + steps A.1–A.6 (#16–#21) + headers for B–F (#22–#26)
- Sub-tasks for B–F will be created at the start of each cycle

---

## What happens at end of Cycle A
1. Math is locked at some v0.x (still 0.X — no v1).
2. **Idea review**: does anything we learned about FA on NSE change the v0.3 problem statement? If yes, draft a v0.4.
3. Cycle B begins (sub-tasks for B get created).

## What happens after Cycle F
- All 6 math specs locked at v0.x.
- Problem statement at some v0.x (possibly v0.4 or v0.5).
- Phase 2 closes. **Phase 3 is still TBD** — likely "test the math holistically against a portfolio-level scenario", but defined when we get there. We're explicitly not planning Phase 3 yet.

---

## Open before starting Cycle A
- Pranav approves this plan.
- Pranav says "go" for A.1 (Research — Equity FA).

**Nothing executes until that go signal.**
