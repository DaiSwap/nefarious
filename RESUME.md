# RESUME — Read this first when context is cleared

**You are picking up an in-progress project. Stop. Read this entire file before doing anything.**

This document is the bootstrap for a fresh Claude conversation. It exists because context was cleared mid-project. Your job is to resume work without breaking continuity, without repeating known mistakes, and without jumping ahead.

---

## 🟢 PRE-COMPACTION STATE — captured 2026-05-30 23:15 (READ THIS FIRST)

This is the freshest state info, captured immediately before Pranav compacted context. Trust this over any older claims in this doc if they conflict.

### Git state
- **PR #1 is MERGED.** Squash-merged to `main`. Day 1 work landed.
- **Local `research` branch has 4 STAGED files** (uncommitted) — these are the post-PR doc updates (LEARNINGS.md Part 8, RESUME.md Appendix, CLAUDE.md GitHub section, session log Day-1 close). Do NOT lose them. Run `git status` to verify they're still staged. If they show as "modified" not "staged", re-stage them.
- Branch convention: **single rolling `research` branch** (no per-day branches). All PRs come from `research`.
- Merge convention: **squash and merge** (not rebase). Each PR = 1 commit on `main`.

### Immediate next task — TAKE THIS ON IMMEDIATELY, do not wait

**Pranav's directive (recorded 2026-05-30): "immediately take on A.5 planning and execution".**

Sequence to run as soon as you've finished reading the resume files:

1. **PLAN A.5 first** — write a detailed plan (lenses, agent prompts, output structure) to `market_research/A5_plan.md`. This is the planning step, not execution.
2. **Show Pranav the plan briefly** (one paragraph + the lens list) — this is a quick confirmation, not an extended back-and-forth. If Pranav doesn't push back within his next message, **proceed to execution**.
3. **Execute A.5** — spawn 4 critic agents in parallel (background mode + checkpoint protocol per §6), then 1 synthesizer after they finish. Output: `market_research/15_cycle_A_critiques_v0.1.md`.
4. **Bundle commit** — after A.5 lands, commit ALL changes together (the 4 already-staged Day-1-close docs + A5_plan.md + 15_cycle_A_critiques_v0.1.md).
5. **Push and open PR #2** for Pranav to merge.

Do not stall at any of these steps. Pranav wants execution, not deliberation. Plan = a written document; execution = agent spawns. Both happen in this session.

### What Pranav explicitly wants from this session
- **"Do this properly"** — plan in writing first, but don't pad the planning step. Tight plan, then go.
- **Immediate execution after planning** — don't ask "shall I proceed?". Just proceed unless Pranav has pushed back.
- **Commit everything together after A.5 is done** — single bundled commit for PR #2.

### Don't do these
- Don't spawn agents during the planning phase. Plan is a written document, not action.
- Don't commit the 4 staged files standalone. Wait until A.5 output is ready, then bundle.
- Don't escalate any version to v1.X. Stay in v0.X.
- Don't touch implementation (no code, no architecture, no UX specs). Just math + critique + refine.

### Lenses I had in mind for A.5 (for reference; Pranav will confirm)
- **Quant** — Beneish coefficient sensitivity, Piotroski cyclical inversion, Z″ for old firms
- **Forensic accountant** — regime-shift false positives, Ind AS 116 transitions, restatement handling
- **Behavioral** — do action labels invite harmful action?
- **Retail user** — are action labels actually actionable?
- Possibly **NSE-specific** as a 5th lens (small sectors, BFSI silent skip)
- Plus **1 synthesizer agent** at the end → `15_cycle_A_critiques_v0.1.md`

These are not locked. Pranav may modify during planning.

### Recovery if anything's broken
- If staged files are gone: check `git stash list`, `git reflog`, and `git status`. The modifications are tracked.
- If git push fails: see `LEARNINGS.md` §8.2 — credential helper troubleshooting.
- If a previous Claude already started A.5: check `market_research/15_cycle_A_critiques_v0.1.md` for partial output before spawning new agents.

---

## 1. The 60-second orientation

- **Project**: "Nefarious" — an AI investment-planning bot for Pranav Venkatesh (Indian retail investor, NSE equities + Mutual Funds).
- **Where we are**: **Phase 2, Cycle A, between A.4 and A.5**. The v0.1 FA math has been tested on Asian Paints (Phase 1A) and Tata Steel (Phase 1B). Six structural weaknesses surfaced. Next step is **A.5 — multi-agent critique** of the v0.1 math + test results.
- **Where we are NOT**: Anywhere near implementation. No code. No data pipelines. No architecture. Just research → math → test → critique → refine cycles. Stay in this loop.
- **Versioning rule**: Everything stays in v0.X. Never escalate to v1.0 anywhere in Phase 2.

## 2. Read these files in this exact order before doing anything

| # | File | Why |
|---|---|---|
| 1 | `/Users/pranavvenkatesh/analytics/nefarious/instruction.txt` | The original prompt Pranav wrote — the WHY of the project |
| 2 | `/Users/pranavvenkatesh/analytics/nefarious/LEARNINGS.md` | Meta-learnings: math weaknesses, process lessons, **5 named mistakes (M1–M5) — do NOT repeat** |
| 3 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/CLAUDE.md` | Project state, locked decisions, current phase, file map |
| 4 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/08_decisions_locked.md` | v0.3 LOCKED problem statement — Pranav's answers to all 12 questions |
| 5 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/09_phase_2_plan.md` | The cycle structure (A through F) — research → math → test → critique → refine |
| 6 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/11_cycle_A_math_v0.1.md` | The math spec being tested |
| 7 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/14_cycle_A_test_synthesis_v0.1.md` | **The 6 structural weaknesses surfaced** — this is what A.5 critics will attack |
| 8 | `/Users/pranavvenkatesh/analytics/nefarious/market_research/sessionlogs/2026-05-30-session-01.md` | Full chronological log of Day 1 |

Optional / deeper reading (don't need at start, useful for specific questions):
- `01_research.md` through `07_synthesis.md` (Phase 1 research & critique)
- `10_cycle_A_research.md` (Cycle A FA research)
- `12_cycle_A_test_v0.1.md` + `13_cycle_A_test_v0.1_TataSteel.md` (raw test outputs)

## 3. Current task state (verify against TaskList)

| ID | Task | Status |
|---|---|---|
| 15 | Cycle A header | pending (blocked by sub-tasks) |
| 16 | A.1 Research | ✅ completed |
| 17 | A.2 Pranav picks | ✅ completed |
| 18 | A.3 Write FA math v0.1 | ✅ completed |
| 19 | A.4 Test FA math v0.1 | ✅ completed |
| **20** | **A.5 Multi-agent critique** | ⏳ **NEXT** |
| 21 | A.6 Refine to v0.2 + idea review | pending |
| 22 | Cycle B header (Equity TA) | pending |
| 23 | Cycle C header (MF analytics) | pending |
| 24 | Cycle D header (Portfolio construction) | pending |
| 25 | Cycle E header (Exit rules + tax) | pending |
| 26 | Cycle F header (Signal combination) | pending |

**Verify this with `TaskList` after resuming. If reality differs from above, trust `TaskList`, not this doc.**

## 4. The immediate next step

**A.5 — Multi-agent critique of v0.1 math + test results.**

Plan:
- Spawn ~4–5 agents in parallel, each from a distinct lens, to attack `11_cycle_A_math_v0.1.md` and the test results in `12_`, `13_`, `14_`.
- Proposed lenses: **quant** (focus on Beneish coefficient sensitivity, Piotroski cyclical inversion, Z″ for old firms) / **forensic accountant** (regime-shift false positives, Ind AS 116 transitions) / **behavioral** (whether the action labels invite harmful action) / **retail user** (whether the labels are actionable) / **NSE-specific** (small sectors, BFSI silent skip).
- One synthesizer agent at the end consolidates into `15_cycle_A_critiques_v0.1.md`.
- **Use the checkpoint protocol** for any agent > 5 min (see §6 below).

Do NOT spawn anything until Pranav says go. Show prompts before spawning if asked.

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
