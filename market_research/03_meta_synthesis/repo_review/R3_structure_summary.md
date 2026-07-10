# R3: Structure/Organization Review

**Reviewer role**: Structure/Organization  
**Date**: 2026-06-06  
**Status**: 🔄 Initialized — inventorying repo.

---

## Inventory

### Root (`nefarious/`)
```
coding_assist/
    claude.md              ← generic LLM coding guidelines, no project-specific content
instruction.txt            ← gitignored (correct)
LEARNINGS.md               ← git-tracked (at root)
LICENSE
market_research/
RESUME.md                  ← git-tracked (at root)
```

### `market_research/`
```
01_phase1_problem_framing/   ← 10 files, numbered 01–09 + problem_statement.md
02_cycle_A_equity_FA/        ← 21 files, numbered 10–19 (+A5_plan.md anomaly)
03_cycle_B_equity_TA/        ← 14 files, numbered 20–24
03_meta_synthesis/           ← problem_statement_dump_2.md + next_steps_post_blog2_feedback.md
                               + next_steps_debate/ (UNTRACKED)
                               + repo_review/       (UNTRACKED — this file)
04_blog_posts/
    post_01_visibility/         ← 16 files (correct naming)
    post_02_multi_agent_critique/ ← 7 files + feedback/ subdir
    post_03_piotroski_cyclicals/  ← 8 files
    post_03b_multi_model_meta_experiment/ ← 7 files (NO DRAFT)
05_external_inputs/          ← 2 files
CLAUDE.md
sessionlogs/
    2026-05-30-session-01.md   ← single session file, no Day 2–3 sessions
```

### `coding_assist/`
```
claude.md    ← generic LLM guidelines (not project-specific)
```

---

## Issues identified

| # | Title | Severity |
|---|-------|----------|
| 1 | `post_03_piotroski_cyclicals` and `post_03b_multi_model_meta_experiment` are ambiguous co-equals for "Blog Post 3" | High |
| 2 | `A5_plan.md` breaks the `NN_` numeric naming convention in `02_cycle_A_equity_FA/` | Medium |
| 3 | `03_meta_synthesis/` prefix collides with `03_cycle_B_equity_TA/` | High |
| 4 | `coding_assist/` is a generic-guidelines artifact with no project-specific content, tracked at root | Medium |
| 5 | `next_steps_debate/` and `repo_review/` subdirs under `03_meta_synthesis/` are untracked (absent from git) | Medium |
| 6 | Session log covers only Day 1 — Days 2–3 sessions are not logged | Medium |
| 7 | CLAUDE.md directory layout is stale: does not reflect `03_cycle_B_equity_TA/`, `post_03b_multi_model_meta_experiment/`, or `03_meta_synthesis/` subdirs | Medium |

---

## GitHub issues filed

(populated after `gh issue create` runs)
