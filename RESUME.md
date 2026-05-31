# RESUME — Read this first when context is cleared

**You are picking up an in-progress project. Stop. Read this entire file before doing anything.**

This document is the bootstrap for a fresh Claude conversation. It exists because context was cleared mid-project. Your job is to resume work without breaking continuity, without repeating known mistakes, and without jumping ahead.

---

## 🟢 CURRENT STATE — last updated 2026-05-31 end of Day 2 (READ THIS FIRST)

This is the freshest state info. Trust this over any older claims in this doc if they conflict.

### Git state
- **PR #1 (Day 1) is MERGED** to `main`. Day 1 work landed.
- **PR #2 (Day 2) is OPEN** at https://github.com/DaiSwap/nefarious/pull/2 — Pranav to squash-merge.
- Working tree clean. `research` in sync with `origin/research` at commit `efcb33e`.
- Branch convention: **single rolling `research` branch**. All PRs come from `research`.
- Merge convention: **squash and merge** (not rebase). Each PR = 1 commit on `main`.

### Cycle A progress
- A.1 Research → A.2 Pranav picks → A.3 Math v0.1 → A.4 Test (Asian Paints + Tata Steel) → **A.5 Multi-agent critique**: all ✅ done.
- **A.6 (refine v0.1 → v0.2 math + idea-review check)**: ⏳ NEXT — but BLOCKED on Pranav's answers to 8 open questions (see below).

### IMPORTANT — Don't start A.6 without Pranav's answers

The A.5 synthesizer left 8 open questions in `15_cycle_A_critiques_v0.1.md` §8 (tabulated also in `problem_statement_dump_2.md` §11). Defaults exist; Pranav must confirm:

| Q | Decision | Synthesizer's default |
|---|---|---|
| Q1 | Beneish gate design — two-stage / additive / two-period? | Two-stage conditional halt |
| Q2 | Cyclical tag list breadth — narrow / broader / broadest? | Broader (incl. housing/auto/construction) |
| Q3 | Altman Z″ replacement — X2_current only / composite only / both? | Both |
| Q4 | BFSI stub format — qualitative / quantitative / defer? | Quantitative with disclaimer |
| Q5 | PSU gate — exclude / annotate / partial sub-pipeline? | Partial sub-pipeline |
| Q6 | AFFIRM 5th label — add / keep 4? | Keep 4 for v0.2 |
| Q7 *(v0.4)* | Add BFSI staging sentence to problem statement? | YES |
| Q8 *(v0.4)* | Add cadence clarification to Q9? | NO — math handles it |

### What to do at the start of your next session

1. Read the rest of this file (§1–§10 below) + the 8 files in §2.
2. Run `TaskList` — verify A.5 (#20) is **completed**; A.6 (#21) is **pending**.
3. Check Pranav's most recent message: has he answered Q1–Q8?
   - **If YES**: write `16_cycle_A_math_v0.2.md` directly. No agent needed — prescriptions are already explicit in `15_cycle_A_critiques_v0.1.md` §6. Optional: re-test on Asian Paints + Tata Steel before closing Cycle A.
   - **If NO**: greet Pranav with current state and the Q1–Q8 table. Wait for answers.

### What NOT to do
- Don't write A.6 math without Q1–Q6 answers. (Q7–Q8 are v0.4 problem-statement edits; can be deferred.)
- Don't auto-merge PR #2. Pranav merges manually.
- Don't escalate any version to v1.X. Stay v0.X.
- Don't touch implementation (no code, no architecture, no UX specs).
- Don't make A.6 a multi-agent process — synthesizer already specified prescriptions; A.6 is a single careful write.

### After A.6 closes Cycle A
- If Q7 = YES: draft `v0.4` of the problem statement (add one BFSI-staging-clarification sentence) before starting Cycle B.
- **Cycle B (Equity TA)** is next — same 6-step pattern as Cycle A. Will need fresh A.1-style research first.

### Recovery if anything's broken
- If `16_cycle_A_math_v0.2.md` already exists when you check (partial): read it first; assume a previous Claude crashed mid-write and continue from where it left off rather than starting fresh.
- If git push fails: see `LEARNINGS.md` §8.2 — credential helper troubleshooting.
- If anything else: check `LEARNINGS.md` Part 3 (mistakes M1–M5) for the patterns to avoid.

---

## 1. The 60-second orientation

- **Project**: "Nefarious" — an AI investment-planning bot for Pranav Venkatesh (Indian retail investor, NSE equities + Mutual Funds).
- **Where we are**: **Phase 2, Cycle A, between A.4 and A.5**. The v0.1 FA math has been tested on Asian Paints (Phase 1A) and Tata Steel (Phase 1B). Six structural weaknesses surfaced. Next step is **A.5 — multi-agent critique** of the v0.1 math + test results.
- **Where we are NOT**: Anywhere near implementation. No code. No data pipelines. No architecture. Just research → math → test → critique → refine cycles. Stay in this loop.
- **Versioning rule**: Everything stays in v0.X. Never escalate to v1.0 anywhere in Phase 2.

## 2. Read these files in this exact order before doing anything

**Note**: Folder structure was reorganized 2026-05-31. All Phase 1 files are now under `market_research/01_phase1_problem_framing/`, Cycle A files under `market_research/02_cycle_A_equity_FA/`, narrative synthesis under `market_research/03_meta_synthesis/`, and blog work under `market_research/04_blog_posts/`. See `market_research/CLAUDE.md` for the full layout.

| # | File | Why |
|---|---|---|
| 1 | `/Users/pranavvenkatesh/analytics/nefarious/LEARNINGS.md` | Meta-learnings: math weaknesses, process lessons, **5 named mistakes (M1–M5) — do NOT repeat**, git/restructure notes |
| 2 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/CLAUDE.md` | Project state, locked decisions, current phase, full file map |
| 3 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/01_phase1_problem_framing/08_decisions_locked.md` | v0.3 LOCKED problem statement — Pranav's answers to all 12 questions |
| 4 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/01_phase1_problem_framing/09_phase_2_plan.md` | The cycle structure (A through F) — research → math → test → critique → refine |
| 5 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/02_cycle_A_equity_FA/11_cycle_A_math_v0.1.md` | The math spec being tested |
| 6 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/02_cycle_A_equity_FA/14_cycle_A_test_synthesis_v0.1.md` | **The 6 structural weaknesses surfaced** |
| 7 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/02_cycle_A_equity_FA/15_cycle_A_critiques_v0.1.md` | A.5 multi-agent critique synthesis — drives the v0.2 refactor |
| 8 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/03_meta_synthesis/problem_statement_dump_2.md` | Latest narrative dump — companion to `07_synthesis.md` (Dump 1) |
| 9 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/sessionlogs/2026-05-30-session-01.md` | Full chronological log (Day 1 through Day 3) |

Optional / deeper reading (don't need at start):
- `01_phase1_problem_framing/01_research.md` through `07_synthesis.md` (Phase 1 research & critique)
- `02_cycle_A_equity_FA/10_cycle_A_research.md` (Cycle A FA research)
- `02_cycle_A_equity_FA/12_cycle_A_test_v0.1.md` + `13_cycle_A_test_v0.1_TataSteel.md` (raw test outputs)
- `04_blog_posts/post_01_visibility/blog_post_01_draft_v0.3.md` (published blog post)
- Note: `instruction.txt` (at project root) is now gitignored — Pranav's personal scratch / next-instruction file; **NOT** required for resuming work

## 3. Current task state (verify against TaskList)

| ID | Task | Status |
|---|---|---|
| 15 | Cycle A header | pending (blocked by sub-tasks) |
| 16 | A.1 Research | ✅ completed |
| 17 | A.2 Pranav picks | ✅ completed |
| 18 | A.3 Write FA math v0.1 | ✅ completed |
| 19 | A.4 Test FA math v0.1 | ✅ completed |
| 20 | A.5 Multi-agent critique | ✅ completed |
| **21** | **A.6 Refine to v0.2 + idea review** | ⏳ **NEXT** (Pranav has confirmed defaults for Q1–Q8) |
| 27 | Plan + write first blog post (Medium) | ✅ completed (v0.3 published 2026-05-31) |
| 22 | Cycle B header (Equity TA) | pending |
| 23 | Cycle C header (MF analytics) | pending |
| 24 | Cycle D header (Portfolio construction) | pending |
| 25 | Cycle E header (Exit rules + tax) | pending |
| 26 | Cycle F header (Signal combination) | pending |

**Verify this with `TaskList` after resuming. If reality differs from above, trust `TaskList`, not this doc.**

## 4. The immediate next step

**A.6 — Refine FA math v0.1 → v0.2, plus idea-review check (does v0.3 → v0.4?).**

Inputs:
- `15_cycle_A_critiques_v0.1.md` — A.5 synthesizer output with concrete v0.2 prescriptions in §6
- `11_cycle_A_math_v0.1.md` — the math being refactored

Steps:
1. **Get Pranav's answers to Q1–Q8** (see top "CURRENT STATE" section). Do not start writing without Q1–Q6 at minimum.
2. **Write `16_cycle_A_math_v0.2.md`** directly. No agent. Prescriptions in §6 of the critique synthesis are explicit enough.
3. **Optional**: re-test the v0.2 math on Asian Paints + Tata Steel to verify the fixes don't break what worked. If you do this, use the checkpoint protocol (§6).
4. **If Q7 = YES**: draft `17_decisions_locked_v0.4.md` with the BFSI staging clarification sentence added to v0.3.
5. **Bundle commit + PR #3** after A.6 lands.

Do NOT make A.6 a multi-agent process. The synthesizer already produced specific prescriptions; A.6 is a careful single write that integrates them.

## 5. Working principles — non-negotiable

1. **User drives strategy, Claude drives structure.** Pranav decides what math to use, what to include in v0.X, what to prioritize. Claude implements the structure, documents, challenges.
2. **No implementation in Phase 2.** No code (except hand-computation in notebooks for math testing). No data pipelines. No architecture. No UX specs. The cycle is *inside the math*, not around it. If you find yourself drafting a data-layer spec or talking about Python module structure, **stop** — that's mistake M1 re-emerging.
3. **Everything in v0.X.** No version escalation. Math goes v0.1 → v0.2 → v0.3. Problem statement stays v0.3 unless cycle-end review bumps it to v0.4.
4. **Document the journey.** Every session adds to `sessionlogs/`. Every cycle has its own numbered files. Every major decision goes in the relevant artifact doc. `LEARNINGS.md` is updated at major milestones.
5. **Confirm before acting on non-trivial work.** Before spawning agents, before deleting tasks, before rewriting a doc — show what you'd do and let Pranav approve. Don't go silent and come back with surprises.
6. **Hand-computation > literature confidence.** Test math on real NSE data before trusting it. The 6 structural weaknesses in v0.1 weren't predictable from US literature; they only surfaced when computed on real Indian companies.

## 6. The checkpoint protocol — MANDATORY for any long agent

After mistake M2 (a 55-minute agent ran silently in foreground; user interrupted because no visibility; all work lost), this protocol is non-negotiable:

```
For any agent expected to run > 5 minutes:

1. Use run_in_background: true (so chat isn't blocked, file is observable)
2. Instruct the agent to:
   - Write a skeleton output file at the start with a status line at top:
     `🔄 Initialized — about to begin <task>`
   - After EVERY major computational step, use the Write tool to overwrite the
     file with everything accumulated so far PLUS an updated status line:
     `🔄 <current step in progress>`
   - At end, status: `✅ All <X> complete.`
   - Update "Last updated" timestamp on every write
3. Pranav (or you) can `Read` the file mid-run to see live progress
4. If the agent dies, work up to the last checkpoint is preserved
```

**Estimated cadence**: ~25+ Write operations during a 15-minute run. Far more than feels necessary. That's the point.

## 7. Five mistakes already made — do NOT repeat

(See `LEARNINGS.md` Part 3 for full detail.)

| ID | Mistake | Avoid by... |
|---|---|---|
| **M1** | Jumped to implementation-direction Phase 2 (data-source / architecture / UX specs). | Stay in math/test/critique. If you draft an architecture, stop. |
| **M2** | Spawned 55-min foreground agent with no checkpoints. Work lost on interrupt. | Use checkpoint protocol from §6 above. |
| **M3** | Misread "tool use rejected" as "agent didn't start" when it actually ran 55 min. | When something looks ambiguous, **check the filesystem first.** Don't make confident claims. |
| **M4** | Spawned multiple agents in parallel without showing prompts. | Show the prompt and confirm before spawning, especially for first-of-a-kind agents. |
| **M5** | Marked a multi-step task complete after only one step done. | Tasks scoped to multiple stocks/dates/items aren't done until all are done. |

The pattern across them: **moving too fast, over-committing, then having to revert.** When in doubt, slow down and confirm.

## 8. What to do at the start of every resume

1. Read this file fully (you've done that).
2. Read the 8 files in §2 above, in order.
3. Run `TaskList` and verify task state matches §3.
4. Greet Pranav with a short summary: "Resumed. I've read RESUME.md, LEARNINGS.md, CLAUDE.md, and the locked decisions. We're at Cycle A A.5 (multi-agent critique of v0.1 math + test results). 6 structural weaknesses to attack. Want me to propose the A.5 agent plan?"
5. **Do nothing else until Pranav responds.** No agent spawning. No file writes. No exploration. Just wait.

## 9. Things Pranav definitely will say (preempt them)

- "Don't jump to implementation." (No code in Phase 2.)
- "Document everything in depth." (Update session log + LEARNINGS.md at milestones.)
- "Check progress." (Read the latest checkpoint file; report size, status line, key results.)
- "Show me the prompt first." (Print the agent prompt; wait for approval.)
- "How long?" (Give honest estimate; the answer is usually 15–25 min for a careful agent.)

## 10. Resume prompt Pranav can paste

When clearing context and starting fresh, paste this exactly:

```
Read /Users/pranavvenkatesh/analytics/nefarious/RESUME.md fully, then follow its
§8 instructions. Do not skip steps. Reply only after reading all files in §2.
```

That's it. Don't add anything else. The doc handles the rest.

---

**Last updated**: 2026-05-30 (end of Day 1, post-PR)
**Next update**: When Cycle A closes (after A.5 + A.6), or whenever significant state changes.

---

## Appendix — Git / GitHub state (added end of Day 1)

The project is pushed to GitHub. The post-compression Claude should know this.

- **Remote**: `https://github.com/DaiSwap/nefarious`
- **Default branch**: `main` (contains only LICENSE)
- **Working branch**: `research` (Day 1 work pushed here)
- **Day 1 PR**: https://github.com/DaiSwap/nefarious/pull/1 — open, awaiting Pranav's merge

### Credential setup (don't touch)

A repo-local credential helper is configured in `.git/config`:
```
credential.helper = !gh auth git-credential
```

This routes credentials only for THIS repo through `gh` (logged in as `DaiSwap`). Pranav's other account `peeveeee` (used elsewhere on this Mac via macOS Keychain) is NOT affected.

**Do NOT** run `gh auth setup-git` (it would route ALL github.com through gh globally — disrupts peeveeee).

**Do NOT** add credentials to global git config or modify Keychain.

If a daily push fails with 403 / permission denied:
1. Run `git config --local --get-all credential.helper` — confirm `!gh auth git-credential` is present
2. Run `gh auth status` — confirm `gh` is still logged in as DaiSwap
3. If gh expired, run `gh auth login` interactively (Pranav must do this)

### Daily push workflow

From `/Users/pranavvenkatesh/analytics/nefarious/`:

```bash
git checkout research              # or current branch
git add <specific files>           # by name; avoid `git add .` for safety
git commit -m "Day N: <summary>"
git push                           # works via repo-local helper
```

Two cadence options Pranav hasn't picked yet:
- (a) Single rolling `research` branch — daily commits stack
- (b) Branch per day (`research/day-N`) — one PR per day

If you create a new branch, you don't need to repeat the credential setup — it's on `.git/config` of the repo, applies to all branches.

### Reading the repo on GitHub

If reading the project ON GitHub (not from local filesystem), the file structure is the same as listed in §2 above. All paths are repo-relative (e.g., `LEARNINGS.md`, `market_research/CLAUDE.md`).
