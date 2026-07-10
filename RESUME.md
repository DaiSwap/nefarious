# RESUME — Read this first when context is cleared

**You are picking up an in-progress project. Stop. Read this entire file before doing anything.**

This document is the bootstrap for a fresh Claude conversation. It exists because context was cleared mid-project. Your job is to resume work without breaking continuity, without repeating known mistakes, and without jumping ahead.

---

## 🟢 CURRENT STATE — last updated 2026-06-10 (READ THIS FIRST)

This is the freshest state info. Trust this over any older claims in this doc if they conflict.

### Git / GitHub state
- **PRs #1–#6 and #31 all MERGED** to `main` (squash). Branch convention: single rolling `research` branch, PRs from `research`, squash-merge.
- **Post-merge routine (MANDATORY after every merged PR)**: `git fetch origin && git rebase origin/main && git push --force-with-lease origin research`. If rebase fails to auto-skip squashed commits: `git rebase --abort && git reset --hard origin/main`, then force-push. Stash uncommitted work first.
- **⚠️ TWO gh ACCOUNTS on this machine**: `DaiSwap` (this project) and `peeveeee` (personal). gh's *active* account flips between sessions. **Before ANY push or `gh pr`/`gh issue` command, run `gh auth status` and if needed `gh auth switch --user DaiSwap`.** A 403 on push means the active account is peeveeee.
- **Open GitHub issues #7–#30**: 24 backlog items filed by repo-review agents (math/spec #7–#13, docs #14–#19, structure #20–#24, process #25–#30). Docs issues #14–#19 addressed by the 2026-06-10 doc refresh.
- **🔒 DO NOT COMMIT** `market_research/03_meta_synthesis/repo_review/R5_public_facing_issues.md` — intentionally local-only (sensitive audit detail). Never `git add` the `repo_review/` folder blindly; add its files by name.

### Blogs — 3 published on Medium (@DaiSwap)
1. [I'm building an AI to argue with me about my own stock portfolio](https://medium.com/@DaiSwap/im-building-an-ai-to-argue-with-me-about-my-own-stock-portfolio-e613a279e628)
2. [One AI agent agrees with you. Five agents catch your mistakes.](https://medium.com/@DaiSwap/one-ai-agent-agrees-with-you-five-agents-catch-your-mistakes-255e3ce606b9) — received a high-signal reader critique (same-model blind spots); stored + analysed at `04_blog_posts/post_02_multi_agent_critique/feedback/`
3. [Everyone can use AI. Almost nobody knows when not to.](https://medium.com/@DaiSwap/everyone-can-use-ai-almost-nobody-knows-when-not-to-4b000183b334) — published 2026-06-10; Pranav's own thesis; source at `04_blog_posts/post_03_keep_the_thinking/`

Two earlier Blog-#3 concepts exist and are NOT published: `post_03_piotroski_cyclicals/` (shelved) and `post_03b_multi_model_meta_experiment/` (deferred; candidate future post).

### Phase 2 progress
- **Cycle A — Equity FA** ✅ CLOSED at v0.3 (2026-05-31). Final math: `02_cycle_A_equity_FA/18_cycle_A_math_v0.3.md`. 10 v0.4 candidates queued in `19_cycle_A_A9_synthesis.md` §6.
- **Cycle B — Equity TA** ⏳ at **B.5 done, B.6 pending**. v0.1 math: `03_cycle_B_equity_TA/21_cycle_B_math_v0.1.md`. B.4 test: 6 stocks × 6 dates, 53% hit rate (below 60% target). B.5 critique: unanimous REFACTOR-REQUIRED; 11 P0 + 13 P1 items + **7 binary decisions for Pranav** in `24_cycle_B_critiques_v0.1.md` §8.
- Cycles C/D/E/F pending.

### Open decision — what runs next (Pranav's call, not yours)
Five advocate agents argued competing priorities in `03_meta_synthesis/next_steps_debate/` (Operator: B.6 now / Skeptic: validate methodology first / Storyteller: publish momentum / Engineer: BFSI structural debt first / Investor: close cycles rough, build the tool). **No synthesis has been run and no verdict picked.** Ask Pranav before starting any of: B.6, Path B (BFSI mini-iteration), Path C (cross-model experiment).

### Known-open items (not blocking, do not silently drop)
- **Privacy findings (R5, local-only file)**: real name + work email + both GitHub accounts are in this repo's tracked files; published Blogs #1–#2 contain real company names that break the anonymization rule. Pranav has NOT yet decided on scrubbing. Raise it if public-facing work comes up; do not unilaterally scrub.
- Cycle A v0.4 BFSI mini-iteration (Path B) — spec'd, not started (task #41).
- Cross-model meta-experiment (Path C) — designed, needs non-Claude model access (task #42).
- 2 tweet sources Pranav referenced remain unfetchable (Twitter/X 402) — pending his paste (`05_external_inputs/02_pending_tweet_sources.md`).

### What NOT to do
- Don't re-open Cycle A (v0.4 candidates are queued, not blocking).
- Don't escalate any version to v1.X. Stay v0.X.
- Don't touch implementation (no code, no architecture, no UX specs).
- Don't start B.6 / Path B / Path C without Pranav picking from the debate.
- Don't commit R5 or `instruction.txt` / `idea_blog3.txt` (personal scratch).

---

## 1. The 60-second orientation

- **Project**: "Nefarious" — a personal AI investment-planning bot for Indian NSE equities + Mutual Funds. Phase 2 = pure math research through repeating cycles (research → math → hand-computed test → multi-agent critique → refine). No implementation until Phase 3. PMF gate: 2026-08-30.
- **Where we are**: Cycle A closed, Cycle B one step from closing, 3 blogs live, a strategy decision pending with Pranav.
- **Versioning rule**: everything stays v0.X for all of Phase 2.

## 2. Read these files in this exact order before doing anything

| # | File | Why |
|---|---|---|
| 1 | `/Users/pranavvenkatesh/analytics/nefarious/LEARNINGS.md` | Meta-learnings; **7 named mistakes (M1–M7) — do NOT repeat**; Parts 8–11 cover git routine, blog process, Cycle A close, Cycle B + external feedback |
| 2 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/CLAUDE.md` | Project state, locked decisions, full file map |
| 3 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/01_phase1_problem_framing/08_decisions_locked.md` | v0.4 LOCKED problem statement |
| 4 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/03_cycle_B_equity_TA/24_cycle_B_critiques_v0.1.md` | B.5 synthesis — the v0.2 brief + 7 pending decisions |
| 5 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/03_meta_synthesis/next_steps_post_blog2_feedback.md` | The 5-path plan (A–E) post-senior-comment |
| 6 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/04_blog_posts/post_02_multi_agent_critique/feedback/01_comment_senior_critique.md` | The highest-signal external input so far |
| 7 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/sessionlogs/2026-06-10-session-02.md` | Catch-up chronological log (2026-05-31 → 2026-06-10) |

Deeper reading as needed: Cycle A files (`02_cycle_A_equity_FA/`), Cycle B files (`03_cycle_B_equity_TA/`), debate cases (`03_meta_synthesis/next_steps_debate/`), published blog sources (`04_blog_posts/post_01_visibility/`, `post_02_multi_agent_critique/`, `post_03_keep_the_thinking/`).

## 3. Current task state (verify against TaskList — trust TaskList over this table)

| Area | Status |
|---|---|
| Cycle A (#15–#21, #28–#30) | ✅ completed, closed at v0.3 |
| Cycle B (#22, #31–#35) | B.1–B.5 ✅; **B.6 (#36) pending** |
| Blogs #1–#3 (#27, #37, #40) | ✅ published |
| External feedback integration (#39) | partially done (stored + analysed; process codification pending — GitHub issues #25–#30) |
| Path B BFSI mini-iteration (#41) | pending |
| Path C cross-model experiment (#42) | pending (blocked on non-Claude access) |
| Cycles C/D/E/F (#23–#26) | pending |

## 4. The immediate next step

**Get Pranav's verdict on the next-steps debate** (`03_meta_synthesis/next_steps_debate/` — five advocate cases; optionally run a synthesis agent over them first). The contenders: B.6 v0.2 math, Path B (BFSI), Path C (cross-model), or the Investor's close-rough-and-build path. Then execute his pick.

## 5. Working principles — non-negotiable

1. **User drives strategy, Claude drives structure.**
2. **No implementation in Phase 2.** If you're drafting architecture, stop (mistake M1).
3. **Everything in v0.X.**
4. **Document the journey** — session logs + LEARNINGS at milestones.
5. **Confirm before non-trivial agent spawns or destructive actions.**
6. **Hand-computation > literature confidence** — test math on real NSE data.

## 6. The checkpoint protocol — MANDATORY for any long agent

For any agent expected to run > 5 minutes: background mode + incremental file writes with a status line at top. **Heavy protocol** (≥15–25 writes) for compute/test agents; **light protocol** (≥4 writes) for review/critique agents. Spawn parallel agents in ONE message (mistake M6). Full rationale: LEARNINGS §2.2, §9.3.

## 7. Seven mistakes already made — do NOT repeat

| ID | Mistake | Avoid by... |
|---|---|---|
| M1 | Jumped to implementation-direction specs | Stay in math/test/critique |
| M2 | 55-min foreground agent, no checkpoints, work lost | Checkpoint protocol (§6) |
| M3 | Claimed "agent didn't run" without checking filesystem | Verify before confident claims |
| M4 | Spawned agents without showing prompts | Show/confirm first |
| M5 | Marked multi-step task complete after one step | All steps done = done |
| M6 | Spawned parallel agents in sequential batches → stalls | All parallel agents in ONE message |
| M7 | Draft uniformly capitulated to external critique | Selective defense + clean concession; uniform agreement is its own AI tell |

## 8. What to do at the start of every resume

1. Read this file fully.
2. Read the files in §2, in order.
3. Run `TaskList`; trust it over §3 if they conflict.
4. Greet Pranav with a short summary **built from the CURRENT STATE block above** (never hardcode a state here — this step has gone stale before; see GitHub issue #15).
5. **Do nothing else until Pranav responds.** No agent spawning, no file writes.

## 9. Things Pranav will say (preempt them)

- "Don't jump to implementation." / "Document everything." / "Show me the prompt first." / "Check progress." (read the checkpoint file, report status line + size)
- Commit convention: **no "Day N" in titles, no Co-Authored-By line; end commit/PR bodies with "Written with help of Claude."**

## 10. Resume prompt Pranav can paste

```
Read /Users/pranavvenkatesh/analytics/nefarious/RESUME.md fully, then follow its
§8 instructions. Do not skip steps. Reply only after reading all files in §2.
```

---

**Last updated**: 2026-06-10 (post PR #31 merge; Blog #3 published; docs refreshed)
**Next update**: when the next-steps verdict lands, Cycle B closes, or any major state change.

---

## Appendix — Git / GitHub operational notes

- **Remote**: `https://github.com/DaiSwap/nefarious` · default branch `main` · working branch `research` (rolling, squash-merged PRs)
- **Credential setup (don't touch)**: repo-local helper in `.git/config` → `credential.helper = !gh auth git-credential`. Global git config and macOS Keychain are NOT modified. Never run `gh auth setup-git`.
- **Multi-account rule**: gh holds two accounts. Active account decides push identity. `gh auth switch --user DaiSwap` before any push/PR/issue command in this repo. 403 on push = wrong active account.
- **Staging rule**: add files by name/folder deliberately; never `git add .` (protects R5, scratch files, `.claude/`).
- If gh token expired entirely: `gh auth login --hostname github.com --git-protocol https --web` in background, surface the one-time code to Pranav.
