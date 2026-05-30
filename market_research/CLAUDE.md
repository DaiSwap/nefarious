# Project: Nefarious — Investment Planning Bot

## One-liner
An AI-powered investment planning bot for Indian NSE equities + Indian Mutual Funds that combines fundamental analysis (Cycle A), technical analysis (Cycle B), and portfolio-construction math (Cycles C–F) to give Pranav a personalized, reasoned action plan to improve his portfolio. **Math correctness is the v0.X priority; implementation comes later.**

## User
- **Owner**: Pranav Venkatesh (pranav.venkatesh@skit.ai)
- **Role in project**: Drives the math/strategy/methodology. The bot is *guided by* the user's domain knowledge — not making strategy up on its own.
- **Initial portfolio**: Indian NSE equities + Mutual Funds. Portfolio file deferred — math validation comes first.

## Working principles
1. **User drives strategy, Claude drives structure.** Pranav specifies what math to use and when. Claude implements the structure, documents, and challenges.
2. **Research → write math → test → multi-agent critique → refine.** No code. No data pipelines. No architecture. The cycle is inside the math.
3. **Document the journey, not just the destination.** All decisions, debates, mistakes, and pivots get written to `sessionlogs/` and the relevant artifact doc.
4. **Everything stays in v0.X.** Nothing escalates to v1.0 during this entire phase of work.
5. **NSE + Indian MFs only.** US equities, crypto, F&O all out of scope.

## Directory layout
```
nefarious/
├── LEARNINGS.md                              # Top-level meta-learnings (mistakes, patterns, lessons)
├── instruction.txt                           # Original prompt from Pranav
└── market_research/
    ├── CLAUDE.md                             # This file — project understanding
    ├── problem_statement.md                  # v0.1 debate (historical)
    ├── 01_research.md                        # Phase 1: market research (5 buckets)
    ├── 02_critique_quant.md                  # Phase 1: quant lens critique
    ├── 03_critique_regulatory.md             # Phase 1: SEBI / regulatory lens
    ├── 04_critique_behavioral.md             # Phase 1: behavioral finance lens
    ├── 05_critique_product.md                # Phase 1: product/PMF lens
    ├── 06_critique_retail.md                 # Phase 1: retail user persona
    ├── 07_synthesis.md                       # Phase 1: synthesis + 12 questions
    ├── 08_decisions_locked.md  🔒            # v0.3 LOCKED problem statement + Pranav's answers
    ├── 09_phase_2_plan.md                    # Phase 2 cycle plan (rewritten after pivot)
    ├── 10_cycle_A_research.md                # Cycle A A.1: FA math survey (4200 words, 50+ citations)
    ├── 11_cycle_A_math_v0.1.md               # Cycle A A.3: math spec v0.1
    ├── 12_cycle_A_test_v0.1.md               # Cycle A A.4 Phase 1A: Asian Paints test
    ├── 13_cycle_A_test_v0.1_TataSteel.md     # Cycle A A.4 Phase 1B: Tata Steel test
    ├── 14_cycle_A_test_synthesis_v0.1.md     # Cycle A: test synthesis across both stocks
    └── sessionlogs/
        └── 2026-05-30-session-01.md          # Comprehensive chronological log
```

## Current phase

**Phase 1 — Problem framing & market research.** ✅ COMPLETE (2026-05-30 PM)
- [x] Initial problem statement debate (v0.1)
- [x] Market research: 16 Indian products audited, 30+ academic/regulatory sources
- [x] 5-lens critique (quant, regulatory, behavioral, product, retail persona) — parallel agents
- [x] Synthesis with 12 questions for Pranav
- [x] Pranav locked all 12 answers + 3 structural updates → v0.3 LOCKED

**Phase 2 — Research → Math → Test → Critique → Refine.** ⏳ In progress (Cycle A active)

Phase 2 is **six sequential cycles**, each running the full research/math/test/critique/refine loop:
- **Cycle A — Equity Fundamental Analysis** ⏳ At A.4 complete, A.5 next
- Cycle B — Equity Technical Analysis (pending)
- Cycle C — Mutual Fund analytics (pending)
- Cycle D — Portfolio construction & sizing (pending)
- Cycle E — Exit rules + tax-aware math (pending)
- Cycle F — Signal combination + behavioral metrics (pending)

## Cycle A status (current)

| Step | Status | Output | Key finding |
|---|---|---|---|
| A.1 Research | ✅ | `10_cycle_A_research.md` | Piotroski best-evidenced on NSE; Magic Formula contradicted post-2012; Buffett moat screen excluded (no NSE evidence) |
| A.2 Pranav picks | ✅ | (recorded in session log) | All defaults chosen — Piotroski-only v0.1 + Beneish/Altman as knockout gates + FCF/NI overlay + sector ROCE percentile |
| A.3 Write math v0.1 | ✅ | `11_cycle_A_math_v0.1.md` | Pipeline: BFSI → Beneish → Altman → Pledge → Piotroski → FCF/NI → ROCE pctile → Action label |
| A.4 Test math v0.1 | ✅ | `12_..._AsianPaints.md`, `13_..._TataSteel.md`, `14_..._synthesis_v0.1.md` | **6 structural weaknesses surfaced** — see synthesis doc |
| A.5 Multi-agent critique | ⏳ Next | Pending | Will attack the 6 weaknesses + propose v0.2 fixes |
| A.6 Refine to v0.2 + idea review | Pending | Pending | Math fixes + check if v0.3 → v0.4 |

## Locked decisions (post-Phase 1, v0.3)
- **Asset universe**: NIFTY 500 equity (NIFTY 100 for TA in v1) + all Indian Mutual Funds.
- **Scope**: Investments only. No F&O, no intraday, no trading.
- **Rollout staging**: Paper → test-portfolio → live advisory (Stages 1/2/3).
- **Automation**: Advisory only (E1, hard-locked).
- **Sharing**: None in Phase 1. Strictly personal use until 2026-08-30 PMF gate.
- **LLM role**: Reasoning/explanation layer over Python-computed signals — **NOT** a signal source.
- **Backtest gate**: Walk-forward, 3yr NSE data, Sharpe > 0.3 after costs, before any signal goes live (will be applied during Phase 3+).
- **Tax**: LTCG/STCG calculator in v1, factored into sell recommendations.
- **Primary success metric**: Behavioral (stop-loss adherence + disposition-effect reduction + engagement rate) + Sharpe improvement as secondary.
- **Milestone gate**: 2026-08-30 for PMF re-evaluation (personal-tool vs productize decision).

## Key learnings so far

See `/Users/pranavvenkatesh/analytics/nefarious/LEARNINGS.md` for the full curated meta-record.

Short version (Cycle A A.4 findings):
- **v0.1 FA math is broken in 6 identifiable structural ways.** Imported US signals (Beneish, Altman, Piotroski) have NSE-specific failure modes that only surface with hand-computation on real data.
- **Piotroski F-Score is anti-correlated with cyclical entry opportunity.** Tata Steel Mar-2020 F=5 (best buy of decade, +355% forward) vs Mar-2021 F=8 (peak, market-matching).
- **Beneish gives false positives during regime shifts** (COVID-era working capital aberrations) and **false negatives for commodity firms** (large non-cash charges suppress TATA term).
- **Trailing fundamentals cannot see forward disruptions** (competitive entries, demand-cycle inflection, valuation mean-reversion). FA alone is insufficient — Cycles B/F will need to address.
- **Process lessons**: agents > 5 min need incremental checkpoint writes + background mode. The Phase 2 "implementation pivot" mistake (deleting tasks 10–14) cost ~30 min but corrected the trajectory.

## Phase log (high-level)

- **2026-05-30 AM**: Project kicked off. Workspace created. Problem statement debate started (v0.1).
- **2026-05-30 16:00–18:00**: Market research + 5-lens parallel critique + synthesis → Pranav locked v0.3.
- **2026-05-30 18:00–20:00**: Phase 2 plan written → then rewritten after "no implementation" pivot (mistake M1). Cycle structure adopted (A → F sequential).
- **2026-05-30 20:00–20:45**: Cycle A A.1 (research agent → 60 KB FA survey) + A.2 (defaults picked) + A.3 (v0.1 math spec written).
- **2026-05-30 20:45–22:00**: A.4 attempt #1: 55-min foreground agent without checkpoint protocol → lost on interrupt (mistake M2 + M3). Recovery: invented checkpoint protocol + background-mode pattern.
- **2026-05-30 22:00–22:30**: A.4 Phase 1A — Asian Paints test (17 min, 25+ checkpoint writes, complete output).
- **2026-05-30 22:30–22:50**: A.4 Phase 1B — Tata Steel test (15 min, same protocol, complete output).
- **2026-05-30 22:50**: A.4 closed. 6 structural weaknesses documented in `14_cycle_A_test_synthesis_v0.1.md`. A.5 critique next.

## What's next

- **Cycle A.5 — Multi-agent critique** of the v0.1 math + Asian Paints + Tata Steel test results. Will attack the 6 structural weaknesses from distinct lenses (quant, forensic accountant, behavioral, retail user, NSE-specific). Output: `15_cycle_A_critiques_v0.1.md`.
- **Cycle A.6 — Refine to v0.2** + check whether anything in A.5 / A.4 demands a problem-statement update (v0.3 → v0.4). Output: `16_cycle_A_math_v0.2.md`.
- Then close Cycle A; begin Cycle B (Equity TA).

## GitHub repo

- **Remote**: https://github.com/DaiSwap/nefarious
- **Default branch**: `main` (contains only LICENSE)
- **Working branch**: `research` (Day 1 work, tracks `origin/research`)
- **Day 1 PR**: https://github.com/DaiSwap/nefarious/pull/1 (open)
- **Credential setup**: repo-local helper using `gh` (logged in as DaiSwap). Global git config + macOS Keychain (`peeveeee` setup) untouched. See `LEARNINGS.md` Part 8 for details.
- **Daily push workflow**: see `LEARNINGS.md` §8.3. Standard `git add <files> / commit / push` from this folder works because the repo-local credential helper resolves to DaiSwap automatically.

## Resume protocol

If context is cleared mid-project, paste this prompt into a fresh Claude:

```
Read /Users/pranavvenkatesh/analytics/nefarious/RESUME.md fully, then follow its §8 instructions. Do not skip steps. Reply only after reading all files in §2.
```

`RESUME.md` lists the 8 files to read in priority order, current task state, immediate next step, working principles, the checkpoint protocol, and 5 named mistakes to avoid.
