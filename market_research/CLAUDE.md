# Project: Nefarious — Investment Planning Bot

## One-liner
An AI-powered investment planning bot for Indian NSE equities + Indian Mutual Funds that combines fundamental analysis (Cycle A), technical analysis (Cycle B), and portfolio-construction math (Cycles C–F) to give Pranav a personalized, reasoned action plan. **Math correctness is the v0.X priority; implementation comes later (Phase 3).**

## User
- **Owner**: Pranav Venkatesh
- **Role in project**: Drives the math/strategy/methodology. The bot is *guided by* the user's domain knowledge — not making strategy up on its own.
- **Portfolio file**: deferred — math validation comes first.

## Working principles
1. **User drives strategy, Claude drives structure.**
2. **Research → write math → test → multi-agent critique → refine.** No code. No data pipelines. No architecture. The cycle is inside the math.
3. **Document the journey, not just the destination** — session logs + LEARNINGS.md.
4. **Everything stays in v0.X** for all of Phase 2.
5. **NSE + Indian MFs only.** US equities, crypto, F&O all out of scope.

## Directory layout (refreshed 2026-06-10)

```
nefarious/
├── LEARNINGS.md                                   # Meta-learnings (Parts 1–11; mistakes M1–M7)
├── RESUME.md                                      # Bootstrap doc — CURRENT STATE block is authoritative
├── coding_assist/claude.md                        # Generic coding guidelines (Pranav's)
├── instruction.txt / idea_blog3.txt               # Personal scratch (untracked / gitignored)
└── market_research/
    ├── CLAUDE.md                                  # This file
    │
    ├── 01_phase1_problem_framing/                 # Phase 1: closed, LOCKED at v0.4
    │   ├── 01_research.md .. 07_synthesis.md      #   research + 5-lens critique (📍 07 = DUMP 1)
    │   ├── 08_decisions_locked.md  🔒             #   v0.4 LOCKED problem statement
    │   └── 09_phase_2_plan.md                     #   the 6-cycle plan
    │
    ├── 02_cycle_A_equity_FA/                      # Cycle A: ✅ CLOSED at v0.3 (2026-05-31)
    │   ├── 10_cycle_A_research.md                 #   A.1 research
    │   ├── 11_cycle_A_math_v0.1.md → 18_..._v0.3.md  # math iterations (18 = final)
    │   ├── 12/13 test files; 14 test synthesis    #   A.4 (6 weaknesses W1–W6)
    │   ├── 15, 15a–d + A5_plan.md                 #   A.5 critique round
    │   ├── 17, 17a–c                              #   A.7 v0.2 re-test
    │   └── 19, 19a–c                              #   A.9 v0.3 re-test (10 v0.4 candidates queued in 19 §6)
    │
    ├── 03_cycle_B_equity_TA/                      # Cycle B: at B.5 done, B.6 PENDING
    │   ├── 20_cycle_B_research.md                 #   B.1 research (7-indicator shortlist)
    │   ├── 21_cycle_B_math_v0.1.md                #   B.3 v0.1 math
    │   ├── 22_..._<6 stocks>.md                   #   B.4 tests (6 stocks × 6 dates)
    │   ├── 23_cycle_B_test_synthesis_v0.1.md      #   B.4 synthesis (B-W1..B-W7 + B-P1; 53% hit rate)
    │   └── 24, 24a–e                              #   B.5 critique (unanimous REFACTOR-REQUIRED; 11 P0 + 13 P1; 7 decisions pending in 24 §8)
    │
    ├── 03_meta_synthesis/                         # Cross-phase narrative + strategy docs
    │   ├── problem_statement_dump_2.md            #   📍 DUMP 2
    │   ├── next_steps_post_blog2_feedback.md      #   the 5-path plan (A–E)
    │   ├── next_steps_debate/                     #   5 advocate cases (Operator/Skeptic/Storyteller/Engineer/Investor) — verdict PENDING
    │   └── repo_review/                           #   R1/R3/R4 summaries (⚠️ R5 is local-only, NEVER commit)
    │
    ├── 04_blog_posts/
    │   ├── post_01_visibility/                    #   📍 PUBLISHED — Blog #1
    │   ├── post_02_multi_agent_critique/          #   📍 PUBLISHED — Blog #2 (+ feedback/ = senior comment)
    │   ├── post_03_piotroski_cyclicals/           #   shelved, unpublished
    │   ├── post_03b_multi_model_meta_experiment/  #   deferred concept (plan + reviews only)
    │   └── post_03_keep_the_thinking/             #   📍 PUBLISHED — Blog #3 (2026-06-10)
    │
    ├── 05_external_inputs/                        # External sources (agent-patterns library; 2 tweets pending)
    │
    └── sessionlogs/
        ├── 2026-05-30-session-01.md               # Day 1–3 chronological log
        └── 2026-06-10-session-02.md               # Catch-up log: 2026-05-31 → 2026-06-10
```

**Conventions**: `NN_` numeric prefixes for order; per-cycle file numbering (Cycle A = 10–19, B = 20–29, C = 30–39...); new file per math version; synthesis files suffixed `_synthesis`. Known structural debts filed as GitHub issues #20–#24.

## Current phase

**Phase 1** ✅ complete — problem statement LOCKED at v0.4 (`01_phase1_problem_framing/08_decisions_locked.md`).

**Phase 2** ⏳ in progress — six sequential cycles:

| Cycle | Scope | Status |
|---|---|---|
| **A** | Equity Fundamental Analysis | ✅ **CLOSED at v0.3** (2026-05-31); 10 v0.4 candidates queued |
| **B** | Equity Technical Analysis | ⏳ **B.5 done; B.6 pending** (7 decisions await Pranav) |
| C | Mutual Fund analytics | pending |
| D | Portfolio construction & sizing | pending |
| E | Exit rules + tax-aware math | pending |
| F | Signal combination + behavioral metrics | pending |

### Cycle B status detail

| Step | Status | Key finding |
|---|---|---|
| B.1 Research | ✅ | 7-indicator shortlist (200-DMA, ADX, ROC, MACD, RSI, Bollinger, ATR) |
| B.3 Math v0.1 | ✅ | 8-step pipeline; ENTRY_ZONE / WAIT / AVOID_ENTRY / EXIT_WARNING labels |
| B.4 Test | ✅ | 6 stocks × 6 dates; **53% hit rate (below 60% target)**; 7 weaknesses B-W1..B-W7 + positive B-P1 (DI-flip leads) |
| B.5 Critique | ✅ | 5 critics unanimous REFACTOR-REQUIRED; **B-W1 cross-cycle compounding** (FA + TA both trail cyclical troughs); **B-W5 MIN/MAX safety catch**; BFSI = cross-cycle blocker |
| **B.6 Refine to v0.2** | ⏳ pending | Blocked on Pranav's 7 binary decisions (`24_cycle_B_critiques_v0.1.md` §8) + next-steps verdict |

## Public face — blogs (Medium @DaiSwap)

1. [I'm building an AI to argue with me about my own stock portfolio](https://medium.com/@DaiSwap/im-building-an-ai-to-argue-with-me-about-my-own-stock-portfolio-e613a279e628)
2. [One AI agent agrees with you. Five agents catch your mistakes.](https://medium.com/@DaiSwap/one-ai-agent-agrees-with-you-five-agents-catch-your-mistakes-255e3ce606b9)
3. [Everyone can use AI. Almost nobody knows when not to.](https://medium.com/@DaiSwap/everyone-can-use-ai-almost-nobody-knows-when-not-to-4b000183b334)

Blog #2 drew a high-signal reader critique (same-model blind spots) — stored + analysed at `04_blog_posts/post_02_multi_agent_critique/feedback/01_comment_senior_critique.md`; it drives methodology upgrades (adversarial synthesizer framing, cross-model roadmap, human-as-arbiter as explicit protocol).

## Locked decisions (v0.4, 2026-05-31)
- **Asset universe**: NIFTY 500 equity (NIFTY 100 for TA in v1) + all Indian MFs; BFSI staging explicit (stub → full pipeline scheduled).
- **Scope**: investments only — no F&O, no intraday.
- **Rollout**: paper → test-portfolio → live advisory (Stages 1/2/3). Advisory only (E1 hard-locked).
- **Sharing**: journey public (blogs/repo); system/signals/recommendations private. PMF gate 2026-08-30.
- **LLM role**: reasoning/explanation layer — NOT a signal source.
- **Backtest gate**: walk-forward, 3yr NSE, Sharpe > 0.3 after costs (Q12).
- **Tax**: LTCG/STCG calculator in v1.
- **Primary metric**: behavioral (stop-loss adherence, disposition-effect reduction, engagement) + Sharpe secondary.

## Key learnings
See `LEARNINGS.md` (Parts 1–11; mistakes M1–M7). Highlights: trailing signals (FA *and* TA) invert at cyclical troughs — real fix lives in Cycle F; imported US math needs NSE re-validation every time; multi-agent critique catches real bugs (B-W5 MIN/MAX inversion) but same-model critics share blind spots (senior comment) — mitigations: adversarial synthesizer prompts, human-as-arbiter, cross-model roadmap.

## Phase log (high-level)
- **2026-05-30**: Phase 1 closed (v0.3 locked); Cycle A through A.4; checkpoint protocol invented after M2.
- **2026-05-31**: Cycle A closed at v0.3 (A.5–A.9). Blog #1 published. Cycle B B.1–B.5 run. Blogs #2/#3 drafted. Folder restructure. (PRs #3–#5)
- **2026-06-06**: Blog #2 published; senior comment received + integrated; F-Score Blog #3 shelved; replacement planned; 5-path next-steps plan. (PR #6)
- **2026-06-10**: Blog #3 pivoted to Pranav's "keep the thinking" thesis and **published**. 5-advocate next-steps debate written (verdict pending). 5-agent repo review → 24 GitHub issues (#7–#30). LEARNINGS Part 11. Docs refreshed. (PRs #31+)

## What's next
Authoritative next-step lives in **RESUME.md → CURRENT STATE** (single source; this section just points there). As of 2026-06-10: get Pranav's verdict on the next-steps debate, then execute (B.6 v0.2 math / Path B BFSI / Path C cross-model / build-rough per Investor).

## GitHub repo
- **Remote**: https://github.com/DaiSwap/nefarious · `main` (squash-merge target) · `research` (rolling work branch)
- **PRs #1–#6, #31 merged**. Issues **#7–#30 open** (repo-review backlog).
- **Two-account rule**: `gh auth switch --user DaiSwap` before any push/PR/issue command. See RESUME.md appendix.

## Resume protocol
Paste into a fresh Claude:
```
Read /Users/pranavvenkatesh/analytics/nefarious/RESUME.md fully, then follow its §8 instructions. Do not skip steps. Reply only after reading all files in §2.
```
