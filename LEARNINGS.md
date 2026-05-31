# LEARNINGS — Nefarious Investment Planning Bot

**Last updated**: 2026-05-30 (end of Day 1)
**Purpose**: Curated meta-learnings that don't fit anywhere else. Distinct from session logs (chronological) and decision docs (committed positions). This is the "what did we learn that should not be forgotten" doc.

The session logs in `market_research/sessionlogs/` are the chronological record. This doc is the curated extraction — lessons, mistakes, and patterns we want to remember.

---

## Part 1 — Math learnings

Distilled from Cycle A, A.4 test on Asian Paints (quality compounder) and Tata Steel (commodity cyclical). Full detail in `market_research/14_cycle_A_test_synthesis_v0.1.md`.

### 1.1 The six structural weaknesses of FA v0.1

Each surfaced empirically by hand-computing v0.1 math against real Indian companies across 4 historical dates each. None of these were predictable from the literature alone — they only show up when you run the math on actual NSE data.

1. **Beneish M-Score gives false positives during regime shifts.** Pandemic-era working-capital aberrations (debtor-day stretch, investment parking) trigger DSRI/AQI elevation, pushing M-Score above −1.78 in companies that did no manipulation. Asian Paints Mar-2022.

2. **Beneish gives false negatives for commodity firms.** Large non-cash charges (depreciation on heavy assets, impairments) make TATA term (coefficient 4.679) deeply negative, suppressing M-Score below threshold permanently — even when other Beneish variables (GMI, AQI) would flag concerns. Tata Steel all 4 dates.

3. **Piotroski F-Score is anti-correlated with cyclical entry opportunity.** Year-over-year improvements track *coincident* fundamentals; for cyclicals this means strongest signal at the cycle peak (worst entry), weakest signal at the trough (best entry). Tata Steel Mar-2020 (5/9 at trough, +355% forward) vs Mar-2021 (8/9 at peak, +34% forward).

4. **Indian accounting standard transitions break YoY signals.** Ind AS 116 (lease accounting, effective FY2020) artificially inflates leverage, triggering spurious Piotroski F5/F6 fails. GST transition (2017–2018) had similar effects on prior tests.

5. **Altman Z″ is dominated by century-accumulated reserves** for old Indian companies. Tata Steel's Z″ stayed in 5.5–5.9 across all 4 dates despite ₹88–116k Cr of long-term debt, because the X2 (retained earnings) and X4' (book equity) terms overwhelm everything else.

6. **Sector ROCE percentile fails on small sectors.** Paints sector has N<10 across all dates; v0.1's N≥15 floor rule silently hides Asian Paints' 33% ROCE (which would be 95+ percentile in most sectors). Systematic conservative bias on niche-sector compounders.

### 1.2 The meta-finding

**Trailing fundamentals cannot see forward disruptions.** Birla Opus / Grasim entering the paints market was the actual driver of Asian Paints' underperformance — completely invisible to v0.1 math. Same for valuation mean-reversion (Asian Paints' 90× P/E in 2021 was the leading indicator; FA can't see it without explicit valuation ratios). FA alone is insufficient; signal-combination (Cycle F) will need to incorporate price-based and qualitative overlays.

### 1.3 What v0.1 DID get right

- Pipeline structure (gates → primary signal → overlays → action label) is logically sound; the issue is which signals are in each box, not the composition logic.
- For stable quality compounders in normal regimes, the math gives stable HOLD labels — the false positive rate is reasonable.
- Transparency is real: every output is traceable to a primary computation; a user can argue with a label because they can see what produced it.

### 1.4 Lessons about the math itself

- **Imported US-developed signals (Beneish, Altman, Piotroski) need NSE re-validation, not just citation.** Each has structural failure modes specific to Indian sector composition (large public-sector, large heavy-industry, accounting-standard evolution).
- **Year-over-year signals are fragile to discontinuities** of any kind — accounting changes, macro shocks, corporate restructurings, post-merger first years. v0.2 needs explicit "discontinuity-aware" handling.
- **Knockout gates are dangerous when a single signal can halt the pipeline.** Beneish as a knockout gate took out Asian Paints Mar-2022 for wrong reasons. Knockouts should require multiple independent indicators agreeing, or be downgraded to additive.
- **The math is empirically wrong in identifiable ways — test data > literature confidence.** Without A.4, we would have shipped v0.1 confidence that turned out to be misplaced.

---

## Part 2 — Process learnings

### 2.1 The "agent ran silently for 55 minutes" incident

**What happened**: I spawned an agent to test v0.1 on 3 stocks × 4 dates without (a) checkpoint protocol, (b) background mode, (c) any way for the user to inspect progress. The agent ran for 55 minutes in the foreground. Pranav interrupted because he had no visibility into what was happening. All 55 min of work was lost — agent doesn't have a clean "save what you've done" hook on interrupt.

**Compounding mistake**: When the interrupt happened, I received a "tool use was rejected" message. I told Pranav "the agent hasn't started — interrupted before it ran". Pranav (correctly) called this out: "it was running for 55 mins, really?" I had misread the rejection signal. The agent had run; I just didn't realize it.

**Lessons**:
1. **Any agent expected to run > ~5 min must have an incremental checkpoint protocol** — write to disk after every logical step, not just at end.
2. **Long agents should run in background mode** (`run_in_background: true`) so they don't block the chat and the user can `Read` the output file anytime.
3. **When something looks ambiguous (e.g., a "rejected" message after a long-running agent), check the filesystem before making confident claims.** Don't state "X didn't happen" — verify first.
4. **Be honest about mistakes immediately when caught.** The right move when Pranav called out the misread was to verify the filesystem and acknowledge the error.

### 2.2 The checkpoint protocol (post-mortem fix)

After the incident, I revised the agent-spawning approach for any long-running computation:

```
At start: Agent uses Write tool to create skeleton file with status line `🔄 Initialized — about to begin <task>`.

After EACH logical step (per ratio, per date evaluation, etc.):
  Agent re-uses Write tool to overwrite the file with everything accumulated so far PLUS updated status line.
  This means ~25+ writes during a 15-min run.

At end: Status updated to `✅ All <X> complete.`
```

The user can `Read` the file at any time mid-run to see live progress. If the agent dies, work up to the last checkpoint is preserved (atomic overwrites mean we never see a half-written file).

This worked perfectly on Asian Paints (17 min, 25+ writes, complete output) and Tata Steel (15 min, 1224-line file written). **Lesson confirmed: the protocol works.**

### 2.3 The Phase 2 implementation pivot (mistake → correction)

**What happened**: After locking the v0.3 problem statement, I drafted `09_phase_2_plan.md` with 7 implementation-direction sub-tasks (data-source design, backtest infrastructure design, architecture sketch, behavioral UX spec, metrics logging design, plus math/exit-rule specs). I started spawning agents for 5 of them in parallel.

Pranav interrupted: *"what are you doing?"*

He clarified: *"do not jump to any kind of implementation. i just need to build plans, research, test, write the math, test again, review with multiple agents, build plan again."*

**Lesson**: I had over-extended the problem-statement-locking momentum into specification-of-systems. Pranav's cycle is:
```
research → write math → test math → multi-agent review → refine → loop
```
Not:
```
research → specify-architecture → specify-data-layer → specify-UX → ...
```

The cycle is **inside the math**, not around the system. Implementation specs are for after the math stabilizes — possibly far after.

**Correction**: Deleted tasks 10–14 (the implementation-y ones). Rewrote `09_phase_2_plan.md` from scratch with the six-cycle structure (A through F). Stripped all architecture/UX/metrics-logging content from Phase 2.

**Meta-lesson**: When the user says "research first" or "no implementation", be aggressive about what counts as implementation. Even "specifying the architecture" is a form of getting ahead. The math is the only product right now.

### 2.4 The Phase 1 multi-agent critique pattern (what worked)

For the original problem-statement debate, I spawned 5 specialist agents in parallel after the initial research:
- Quant
- SEBI/Regulatory
- Behavioral
- Product/PMF
- Skeptical retail investor

Then one synthesis agent. Total ~6 agent runs, ~15 min wall-clock (parallel saves time).

**Why this worked**:
- Each lens had a distinct, predictable failure mode for the proposed product
- Critique is naturally parallel (no dependencies between perspectives)
- Synthesis on top brings them into one document
- The structured "verdict (ACCEPT/PARTIAL/REJECT) per critique" forced commitment

**Plan**: Replicate this for A.5 (Cycle A critique). The lenses for math critique will differ — likely quant, forensic accountant, behavioral, retail user, NSE/India-specific.

### 2.5 Versioning conventions (locked)

Decided early; restated for clarity:
- **All plans, math specs, problem statements stay in v0.X during this whole phase.** Nothing escalates to v1.X.
- Problem statement: v0.1 (draft) → v0.2 (post-synthesis) → v0.3 (locked, current) → v0.4+ (per-cycle idea review)
- Math specs (per cycle): v0.1 (first draft) → v0.2 (post-critique refinement) → v0.3+ (further iterations)
- File numbering: 10–17 = Cycle A, 20–27 = Cycle B, etc.
- New file per version (e.g., `16_cycle_A_math_v0.2.md`), not overwriting v0.1

### 2.6 File-naming and organization

Decided during execution:
- Per-cycle subdivision via numeric prefix (10–17 for Cycle A, etc.)
- One file per major step in a cycle (research, math-vN, test-vN, critique-vN, etc.)
- Multi-stock tests get one file per stock (`12_..._AsianPaints.md`, `13_..._TataSteel.md`)
- Synthesis files have the suffix `_synthesis` (e.g., `14_cycle_A_test_synthesis_v0.1.md`)
- Meta files at project root (`LEARNINGS.md`, `instruction.txt`)
- Session logs date-stamped (`sessionlogs/2026-05-30-session-01.md`)

---

## Part 3 — Mistakes and corrections (named explicitly)

| # | Mistake | When | Correction |
|---|---|---|---|
| M1 | Jumped to implementation-direction specs (data-source / architecture / UX) after locking v0.3 | After Pranav picked Mode D | Pranav interrupted; I deleted tasks 10–14, rewrote `09_phase_2_plan.md`, pivoted to cycle structure |
| M2 | Spawned 55-min foreground agent without checkpoint protocol or background mode | First A.4 attempt | Pranav interrupted; revised approach to checkpoint-per-step + `run_in_background: true` |
| M3 | Misread "tool use rejected" as "agent didn't start" when it had actually run for 55 min | After M2 interrupt | Pranav called it out; I verified filesystem (no test file existed → confirmed work lost), apologized, reset task state |
| M4 | Spawned 3 infrastructure agents in parallel without showing prompts first | After picking Mode D, before M1 was caught | Pranav stopped me; I now show / confirm before any non-trivial agent spawn |
| M5 | Marked task #19 (A.4) complete after only Phase 1A (Asian Paints) — premature | After Asian Paints finished | Re-opened to in_progress, ran Phase 1B (Tata Steel), then marked complete |

The pattern across M1, M2, M3: **moving too fast, over-committing, then having to revert.** Going slower with explicit confirmation points avoids all of them.

---

## Part 4 — Open risks for future cycles

Cycle B (Equity TA) starts after Cycle A closes. Things to carry forward:

1. **TA signals are even more cycle-sensitive than FA.** If Piotroski inverted on Tata Steel, RSI/MACD on the same stock may invert too — but in the opposite direction (TA is supposed to catch turns). The interaction between Cycle A's FA conclusions and Cycle B's TA conclusions will need to be explicit when we get to Cycle F (signal combination).

2. **The "no NSE-validated US signal" lesson generalizes.** Don't bring in TA indicators on the strength of their US literature alone. Insist on Indian-market replication before locking thresholds.

3. **MF analytics (Cycle C) will face a different math universe entirely.** No TA, no Piotroski, no Beneish. Expense ratio drift, portfolio overlap, category percentile — different math, different failure modes to discover. Don't assume Cycle A's lessons transfer.

4. **Portfolio construction (Cycle D) is where math interactions get complex.** Half-Kelly is a position-sizing math; correlation-to-portfolio is a covariance math; both are sensitive to bad signal quality upstream. If Cycle A signals are weak (which the test suggests), Cycle D needs to compensate — possibly with very low position-size confidence intervals.

5. **Exit rules (Cycle E) include tax math** which is jurisdiction-specific. LTCG/STCG thresholds change in budgets; the math must be parameterizable to the rate, not hardcoded.

6. **Signal combination (Cycle F) is where the explosion happens.** TA + FA + MF + sizing + exit rules + behavioral metrics → exponential complexity. The lesson from Cycle A: test the combined math on real examples before locking it. Critique what surfaces.

---

## Part 5 — What's working well (positive learnings)

Don't just collect mistakes. Things to keep doing:

1. **The cycle structure (research → math → test → critique → refine).** Each step has a clear deliverable and an explicit transition. No ambiguity about what's done.

2. **Per-step task tracking** with `TaskCreate`/`TaskUpdate`. Visibility into project state is high; tasks block each other appropriately.

3. **Hand-computing tests on real NSE data.** The 6 structural weaknesses would not have surfaced from theory alone. Real data > literature confidence.

4. **Checkpoint protocol + background agents.** After the M2 incident, this combination has been working beautifully. ~17-min agent runs with full transparency.

5. **Multi-agent critique with structured lenses.** Worked for Phase 1 problem-statement debate; should work for A.5 math critique. Forces consideration of perspectives I wouldn't generate alone.

6. **Pranav's "no implementation" guardrail.** When I drift, Pranav intervenes. This is healthy; it keeps the work focused on what matters now (math correctness), not infrastructure that depends on math being correct.

7. **Defaults-with-rationale offers.** I propose recommended defaults for every multi-option question, with reasoning. Pranav typically picks defaults but can override. Fast decisions with explicit reasoning preserved in the doc trail.

---

## Part 6 — Documentation conventions (for any future contributors)

If this project ever has other contributors (human or AI), here's what they need to know:

1. **`market_research/CLAUDE.md`** is the project context. Read first.
2. **`market_research/08_decisions_locked.md`** is the source of truth for the problem statement (v0.3). Anything else is research / draft / iteration.
3. **`market_research/sessionlogs/`** is the chronological record. Comprehensive; don't summarize.
4. **`LEARNINGS.md`** (this file) is the curated meta-record. Updated at major milestones.
5. **Cycle files** (10–17 = Cycle A, 20–27 = Cycle B, ...) are the working artifacts of the research → math → test → critique → refine loop.
6. **Nothing escalates to v1.X** in this phase. All versions stay in v0.X.
7. **No implementation work in Phase 2.** No data pipelines, no architecture, no code beyond hand-computation notebooks for math testing.

---

## Part 7 — A short list of things to revisit

Open threads that this doc captures but doesn't resolve:

- [ ] When does Phase 2 close? Need a definition of "math stable" that ends the cycle loop.
- [ ] How do we incorporate qualitative signals (competitive moats, management quality, governance) without losing the math-first discipline?
- [ ] Do we need a Cycle 0 (or Cycle G) for "things the math fundamentally can't see" — explicit qualitative overlays?
- [ ] What's the boundary between Cycle A v0.X iterations and "give up on FA-as-currently-defined and rethink"?
- [ ] When do mutual fund analytics (Cycle C) get their own A.5-style critique?
- [ ] Will the multi-agent critique pattern hold up at scale, or do we need different lens-sets per cycle?

These are not blockers; they're context for future decisions.

---

**End of LEARNINGS.md v1.** Next update: end of Cycle A (after A.5 and A.6 are done).

---

## Part 8 — Git / GitHub setup (added end of Day 1)

After completing the test synthesis and documentation pass, Pranav requested the project be pushed to GitHub at https://github.com/DaiSwap/nefarious.

### 8.1 The two-account problem

Pranav has two GitHub accounts on this Mac:
- **`peeveeee`** — his personal/other identity, credentials cached in macOS Keychain (used by git's default credential helper for github.com)
- **`DaiSwap`** — the account owning `DaiSwap/nefarious` (this project's home)

When `gh auth login` authenticated as DaiSwap, `gh` had the right token, but `git push` still used macOS Keychain (peeveeee) → 403 Permission denied.

### 8.2 The solution: repo-local credential helper

We set up the credential helper **only in this repo's `.git/config`** — global config and Keychain entries untouched:

```bash
git config --local credential.helper ""
git config --local --add credential.helper "!gh auth git-credential"
```

After this:
- `~/.gitconfig` (global) — untouched
- macOS Keychain — untouched
- This repo's `.git/config` — has `credential.helper = !gh auth git-credential`
- Any other repo on this Mac — uses default helper (peeveeee)
- This repo only — uses `gh` (DaiSwap)

**Reversible**: `git config --local --unset-all credential.helper` removes it.

**Caveat**: if a second account is added to `gh` later (`gh auth login` for peeveeee in gh too), `gh auth git-credential` picks by URL match. Should still resolve to DaiSwap for `DaiSwap/nefarious`, but worth watching.

### 8.3 Daily push workflow (committed pattern)

For ongoing daily pushes:

```bash
# Work as normal in /Users/pranavvenkatesh/analytics/nefarious
# At end of day:
git checkout research              # or current working branch
git add market_research/<new-files>  # by name, not `git add .` (safety)
git commit -m "Day N: <summary>"
git push                           # works because of repo-local credential helper
```

Two cadence options:
- **Single rolling `research` branch** — daily commits stack on it; one long-running PR (or merge daily)
- **One branch per day** — `research/day-N`; one PR per day; cleaner history

Decision deferred to Pranav's preference once Day 2 begins.

### 8.4 What's in PR #1 (Day 1)

- PR: **https://github.com/DaiSwap/nefarious/pull/1**
- Branch: `research`
- Base: `main`
- Files: 22 (entire `market_research/` + `LEARNINGS.md` + `RESUME.md` + `instruction.txt` + `.gitignore`)
- Status: open, Pranav to merge

### 8.5 What's in `.gitignore` (initial)

```
.claude/                  # Claude Code internal state
.DS_Store                 # macOS
__pycache__/, *.pyc       # Python (future)
.ipynb_checkpoints/       # Jupyter (future)
.vscode/, .idea/          # editors
```

### 8.6 Lessons codified

- **Two-account GitHub setups need repo-local credential helpers.** Global `gh auth setup-git` would override the other account.
- **`gh auth git-credential` is a clean credential source** when gh is already authenticated. No PAT needed, no Keychain entry, nothing to leak.
- **Always do `git config --local`, not `git config --global`** for repo-specific identity / credential setup.
- **Before pushing, run `gh api repos/<owner>/<repo>` to inspect remote state.** Knowing what's already on the remote (just LICENSE in our case) prevents conflicts.
- **Stage files by name (`git add market_research/`) not `git add .`** — avoids accidentally adding `.claude/` or sensitive files.

---

### 8.7 Post-squash-merge rebase routine — MANDATORY after every merged PR

**The problem (surfaced after PR #2 was opened)**:

After PR #1 was squash-merged into `main`, PR #2 immediately showed conflicts (`mergeable: CONFLICTING`, `mergeStateStatus: DIRTY`) even though Day 2 work was a clean linear extension of Day 1.

Cause: squash-merge creates a brand-new commit on `main` containing all the merged changes, but our local `research` branch still has the **original** pre-squash commit underneath any new work. The two histories share only the initial-commit ancestor; the same files modified on both sides look like a conflict to GitHub.

Visual:

```
                          ┌─ <squash_sha>  PR #N merged into main
e99713f (initial) ───────┤
                          └─ <orig_sha> ──▶ <new_work_sha>  research
                              (PR #N's      (PR #N+1's
                               original)     new commits)
```

**The fix** — rebase `research` onto `origin/main` immediately after each PR is merged:

```bash
# 1. Update origin refs
git fetch origin

# 2. If there's uncommitted work, park it
git stash push -m "<short description>"

# 3. Rebase research onto the new main
git rebase origin/main

# 4. Force-push (use --force-with-lease, not --force)
git push --force-with-lease origin research

# 5. Restore any parked work
git stash pop
```

**Why rebase works cleanly**:
- Git detects that the pre-squash commit on `research` is equivalent to the squash commit on `main` (it auto-detects "previously applied" patches and skips them — you'll see `warning: skipped previously applied commit <sha>`).
- Only the post-squash commits (the new work) get replayed onto `main`.
- Result: linear history where `research = main + new_work`. PR #N+1 diff now shows only the new work.

**Force-push safety**:
- `--force-with-lease` refuses to push if `origin/research` has changed since your last `git fetch`. This protects against overwriting concurrent work (e.g., another collaborator's commit).
- `--force` (no lease) is dangerous. Never use it on `research` unless you have explicit confirmation.
- **NEVER force-push to `main`** under any circumstance. System rule + project rule.

**The routine — committed**:

After EVERY squash-merged PR, before starting new work:
1. `git fetch origin`
2. `git rebase origin/main`
3. `git push --force-with-lease origin research`

This keeps `research` always one PR ahead of `main`, with clean linear history. If we ever forget this routine, the next PR will conflict.

**What NOT to do**:
- ❌ Don't merge `main` into `research` — produces ugly merge commits, defeats the squash-merge purpose.
- ❌ Don't `git reset --hard origin/main` without first verifying you've cherry-picked your post-merge commits — loses work irreversibly.
- ❌ Don't force-push to `main` ever (system rule).
- ❌ Don't skip the rebase — every subsequent PR will conflict and need manual resolution.
- ❌ Don't rebase mid-work if uncommitted edits exist; stash first.

**When NOT to use rebase + force-push**:
- If `research` has collaborators (multiple humans/agents pushing to it). For a solo project this is safe; for a team you'd need coordination.

**Edge case (added after PR #2 merge)**: if rebase fails to auto-skip the "previously applied" commits (e.g., because multiple commits were squashed together and patch-id matching gets confused), abort the rebase and `git reset --hard origin/main` instead. Then force-push. This is equivalent in effect but skips the confusing conflict-resolution dance. Safe because origin/main has all the merged content.

---

### 8.8 — Folder restructure (added 2026-05-31)

After ~40 markdown files accumulated at `market_research/` root, the folder became hard to traverse. Restructured into 4 topical subfolders:

```
market_research/
├── CLAUDE.md
├── 01_phase1_problem_framing/   # Phase 1 close (locked at v0.3)
├── 02_cycle_A_equity_FA/        # Cycle A: research → math → test → critique
├── 03_meta_synthesis/           # Cross-cutting narrative docs (Dump 2 etc.)
├── 04_blog_posts/               # Public-facing writing
│   └── post_01_visibility/
└── sessionlogs/
```

**Move method**: used `git mv` for all tracked files (preserves history; git detects every move as a rename, not as a delete + create). Untracked blog files moved with plain `mv` then `git add`.

**Naming convention**:
- Top-level subfolders prefixed `NN_` for visual sort order
- Within subfolders, original numeric prefixes preserved (Phase 1 files keep `01_..09_`; Cycle A files keep `10_..15_`). New cycles will continue: Cycle B → `20_..27_`, Cycle C → `30_..`, etc.
- `📍` markers in CLAUDE.md's layout for narrative-anchor docs (Dump 1, Dump 2, published posts)

**Lesson codified**: Restructure when traversal pain crosses ~30 files at one level. Use `git mv` so history is preserved. Update CLAUDE.md and RESUME.md path references in the same commit.

### 8.9 — Untracking `instruction.txt` (added 2026-05-31)

`instruction.txt` at project root was Pranav's prompt → Claude communication channel. He'd write his next ask into it, then point me there. The file accumulated personal content over the project.

**Decision**: untrack via `git rm --cached instruction.txt` + leave the `.gitignore` entry he'd added. Effects:
- File stays on Pranav's local disk
- Removed from repo on next push
- Future edits stay local; not in commit history

**Lesson codified**: When the user adds a file to `.gitignore`, check whether it's already tracked. `.gitignore` only affects untracked files. Already-tracked files need `git rm --cached` for the gitignore to bite.

---

## Part 9 — Blog post writing process (added 2026-05-31)

The first public-facing blog post for the project taught a separate set of lessons from the math cycles. Distilled here.

### 9.1 The plan → draft → critic → synthesis → revise loop

Same shape as the math cycle (research → math → test → critique → refine), applied to writing:

```
Pranav's ask → Plan written → Draft v0.1
            → 5 critics in parallel → Synthesizer → Pranav reviews
            → Draft v0.2 → 5 critics again → Synthesizer + Pranav reviews
            → Draft v0.3 → publish
```

Three critic rounds (v0.1, v0.2, sometimes a final consistency pass) was the right cadence. Fewer would have left structural issues. More would have ground down to "no new feedback" noise.

### 9.2 The 5 lenses that work for a blog draft

For a blog post written by AI on behalf of a human, the 5 critic lenses that produced non-overlapping findings:

| ID | Lens | Catches |
|---|---|---|
| C1 | **Target reader** (Indian retail investor here) | Does the hook land? Are the pain points real? Would they share/follow? |
| C2 | **Editorial / writing quality** | Sentence rhythm, repetition, weak verbs, em-dash count, paragraph length |
| C3 | **Skeptic / counter-argument** | Unsupported claims, false modesty, fabricated precision, weasel hedges |
| C4 | **Voice authenticity (human vs AI tells)** | Em-dash overuse, hedge-word repetition, parallel-construction "tells", polished closing lines |
| C5 | **Platform fit** (Medium here) | Title, opening hook for bounce window, subheads, tags, CTA structure |

**C4 was the gating critic** in this project. The post sounded "part-human-part-AI" until C4's specific catches were addressed. The other 4 critics couldn't catch these — they're trained on different signal.

### 9.3 Lighter checkpoint protocol for blog critics

For math-test agents the protocol mandated 15–25 writes during a 15-minute run (Part 2.2). For blog reviewers that was overkill and contributed to the first round's stall.

**Light protocol** that worked second time: ≥4 writes per agent (initialize → mid-read → mid-drafting → final ✅). Each prompt compact (~50–70 lines vs 120 for math critics). This brought reviewers from "watchdog stalled at 600s" to consistent 2–3 min completions.

### 9.4 Mistake M6: batched critic spawns instead of one parallel message

| ID | Mistake | When | Fix |
|---|---|---|---|
| **M6** | Spawned blog critics in two batches (2, then 3) instead of all 5 in one parallel message. The two-batch first round stalled at the watchdog after 600s — both agents wrote only the initial skeleton (~600 bytes) before silence. | First v0.1 critic round | Re-spawned all 5 in a single parallel message with lighter prompts. Worked. |

**Lesson**: when spawning multiple agents for the same task, send them all in **one parallel message** (multiple Agent tool calls per message). Don't batch sequentially.

### 9.5 Critic conflicts and how to resolve them

When critics disagree, the resolution principles that worked:

- **Audience > craft**: When C1 (retail reader) and C2 (editor) disagreed on naming AI labs (C2 said "name them" — Anthropic, OpenAI, Google; C1 said "reads as tech-blog inside-baseball for retail"), audience won.
- **User > critics**: When Pranav's review caught what no critic caught (reframe motivation; use mermaid not ASCII; anonymize real company names), the user's reading is irreplaceable. Critics see the post; the user sees the post AND knows the actual intent.
- **Voice critic always wins on voice issues**: C4 calls *"unmistakably"* defensive; C2 calls the same lines the *"two best sentences"*. Drop *"unmistakably"* (C4); keep the lines + put them last (C2). Both critics satisfied.

### 9.6 Reframe-the-motivation insight

The biggest single improvement v0.2 → v0.3 came from Pranav's correction: stop framing the project as *"nobody is building this, so I am"*. The actual motivation was **personal learning** (investing + AI). This:
- Removed the C3 skeptic vector entirely (no more contested landscape claims)
- Made the post feel more honest, not defensive
- Aligned with the v0.3 problem-statement Q7 ("strictly personal" in Phase 1)

**Lesson**: AI drafts default to *"explaining the gap in the market"* framing. The user's intent is often more personal than that. Ask the user *what they're actually trying to do* before writing in a draft that assumes commercial framing.

### 9.7 Anonymization for public-facing writing

Pranav's instruction to anonymize real company names in the published post (Asian Paints → Company A; Tata Steel → Company B) had three benefits:
1. Aligned with v0.3 "strictly personal" sharing constraint
2. Softened C3's "perfectly inverted" overclaim concern (easier to make a claim about Company B than about Tata Steel specifically)
3. Made the principle more portable (any reader thinks "do I have a Company B in my portfolio?")

**Lesson**: internal docs keep real names (for traceability). Public-facing docs anonymize. The line between *research notes* and *publishable content* is a transformation step, not a re-write.

---

**End of LEARNINGS.md v1.3 (Parts 8.8, 8.9, Part 9 added).** Next update: end of Cycle A.
