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

## Directory layout (restructured 2026-05-31)

```
nefarious/
├── LEARNINGS.md                                   # Top-level meta-learnings
├── RESUME.md                                      # Bootstrap doc for fresh Claude sessions
├── instruction.txt                                # Personal scratch (gitignored, not in repo)
└── market_research/
    ├── CLAUDE.md                                  # This file — project state
    │
    ├── 01_phase1_problem_framing/                 # Phase 1: closed, locked at v0.3
    │   ├── problem_statement.md                   #   v0.1 debate (historical)
    │   ├── 01_research.md                         #   market research (5 buckets)
    │   ├── 02_critique_quant.md
    │   ├── 03_critique_regulatory.md
    │   ├── 04_critique_behavioral.md
    │   ├── 05_critique_product.md
    │   ├── 06_critique_retail.md
    │   ├── 07_synthesis.md                        #   📍 DUMP 1 (synthesis + 12 questions)
    │   ├── 08_decisions_locked.md  🔒             #   v0.3 LOCKED problem statement
    │   └── 09_phase_2_plan.md                     #   the 6-cycle plan
    │
    ├── 02_cycle_A_equity_FA/                      # Cycle A: at A.5 done, A.6 next
    │   ├── 10_cycle_A_research.md                 #   A.1: FA research survey
    │   ├── 11_cycle_A_math_v0.1.md                #   A.3: math spec v0.1
    │   ├── 12_cycle_A_test_v0.1.md                #   A.4-1A: Asian Paints hand-compute
    │   ├── 13_cycle_A_test_v0.1_TataSteel.md      #   A.4-1B: Tata Steel hand-compute
    │   ├── 14_cycle_A_test_synthesis_v0.1.md      #   A.4: 6 weaknesses surfaced
    │   ├── A5_plan.md                             #   A.5 plan
    │   ├── 15a_critic_quant.md                    #   A.5 critic 1 (quant)
    │   ├── 15b_critic_forensic.md                 #   A.5 critic 2 (forensic accountant)
    │   ├── 15c_critic_behavioral.md               #   A.5 critic 3 (behavioral finance)
    │   ├── 15d_critic_retail_nse.md               #   A.5 critic 4 (retail + NSE)
    │   └── 15_cycle_A_critiques_v0.1.md           #   A.5 synthesizer (v0.2 brief)
    │
    ├── 03_meta_synthesis/                         # Cross-phase narrative docs
    │   └── problem_statement_dump_2.md            #   📍 DUMP 2 (post-A.5 synthesis)
    │
    ├── 04_blog_posts/                             # Public-facing writing
    │   └── post_01_visibility/                    #   First Medium post
    │       ├── blog_post_01_plan.md
    │       ├── blog_post_01_draft.md              #   v0.1 (initial)
    │       ├── blog_post_01_draft_v0.2.md
    │       ├── blog_post_01_draft_v0.3.md         #   📍 PUBLISHED
    │       ├── blog_post_01_review_C1..C5.md      #   v0.1 critic round (5 files)
    │       ├── blog_post_01_review_synthesis.md   #   v0.1 critic synthesis
    │       ├── blog_post_01_review_v2_C1..C5.md   #   v0.2 critic round (5 files)
    │       └── blog_post_01_review_v2_synthesis.md  # v0.2 critic synthesis
    │
    └── sessionlogs/
        └── 2026-05-30-session-01.md               # Day 1 → Day 3 chronological log
```

**Conventions**:
- Top-level subfolders prefixed with `NN_` so they sort visually
- Within each subfolder, file numbering preserves chronology (Phase 1 = `01_..09_`; Cycle A = `10_..15_`)
- Cycle B will be `03_cycle_B_equity_TA/` with files `20_..27_`, etc.
- `📍` markers indicate "narrative anchor" docs (Dumps, published posts)

## Current phase

**Phase 1 — Problem framing & market research.** ✅ COMPLETE (2026-05-30 PM)
- [x] Initial problem statement debate (v0.1)
- [x] Market research: 16 Indian products audited, 30+ academic/regulatory sources
- [x] 5-lens critique (quant, regulatory, behavioral, product, retail persona) — parallel agents
- [x] Synthesis with 12 questions for Pranav
- [x] Pranav locked all 12 answers + 3 structural updates → v0.3 LOCKED

**Phase 2 — Research → Math → Test → Critique → Refine.** ⏳ In progress (Cycle A closed; Cycle B next)

Phase 2 is **six sequential cycles**, each running the full research/math/test/critique/refine loop:
- **Cycle A — Equity Fundamental Analysis** ✅ **CLOSED 2026-05-31** at v0.3
- **Cycle B — Equity Technical Analysis** ⏳ **NEXT**
- Cycle C — Mutual Fund analytics (pending)
- Cycle D — Portfolio construction & sizing (pending)
- Cycle E — Exit rules + tax-aware math (pending)
- Cycle F — Signal combination + behavioral metrics (pending)

## Cycle A status (CLOSED)

| Step | Status | Output | Key finding |
|---|---|---|---|
| A.1 Research | ✅ | `10_cycle_A_research.md` | Piotroski best-evidenced on NSE; Magic Formula contradicted post-2012; Buffett moat screen excluded |
| A.2 Pranav picks | ✅ | (recorded in session log) | All defaults chosen |
| A.3 Write math v0.1 | ✅ | `11_cycle_A_math_v0.1.md` | Pipeline: BFSI → Beneish → Altman → Pledge → Piotroski → FCF/NI → ROCE pctile → Action label |
| A.4 Test math v0.1 | ✅ | `12, 13, 14` | **6 structural weaknesses surfaced** (W1–W6) |
| A.5 Multi-agent critique | ✅ | `15, 15a–d, A5_plan` | All 4 critics: REFACTOR-REQUIRED; 9 P0 / 7 P1 items synthesized |
| A.6 Refine to v0.2 + v0.4 PS update | ✅ | `16_cycle_A_math_v0.2.md` + `08_decisions_locked.md` v0.4 | BFSI staging clarification (Q7 = YES) |
| A.7 v0.2 re-test (3 stocks) | ✅ | `17, 17a, 17b, 17c` | v0.2 fixes 4/6 v0.1 weaknesses fully + 2/6 substantially; **7 v0.3 candidates surfaced (N1–N7)** |
| A.8 Refine to v0.3 | ✅ | `18_cycle_A_math_v0.3.md` | All 7 v0.3 candidates addressed |
| A.9 v0.3 re-test (3 stocks) | ✅ | `19, 19a, 19b, 19c` | **5 of 7 v0.3 candidates confirmed FIXED**; N3 threshold cosmetic; N7 cycle-window tradeoff (defer to Cycle F); **10 v0.4 candidates queued** |
| **Cycle A** | ✅ **CLOSED 2026-05-31** | v0.3 final for this iteration | Math validated across 3 stock profiles; ready for Cycle B |

## Locked decisions (post-Phase 1, v0.4 as of 2026-05-31)
- **Asset universe**: NIFTY 500 equity (NIFTY 100 for TA in v1) + all Indian Mutual Funds; BFSI staging explicit (stub in v0.2 → full pipeline scheduled for next Cycle A iteration).
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
