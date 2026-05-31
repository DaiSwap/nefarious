# A.5 Plan — Multi-Agent Critique of v0.1 FA Math + Test Results

**Status**: Plan ready for Pranav's quick confirmation. Execution follows immediately unless Pranav pushes back.
**Date**: 2026-05-30
**Cycle**: A (Equity FA), step A.5
**Inputs under critique**:
- `11_cycle_A_math_v0.1.md` (v0.1 math spec)
- `12_cycle_A_test_v0.1.md` (Asian Paints — quality compounder)
- `13_cycle_A_test_v0.1_TataSteel.md` (Tata Steel — commodity cyclical)
- `14_cycle_A_test_synthesis_v0.1.md` (6 weaknesses synthesis)
**Final output**: `15_cycle_A_critiques_v0.1.md` (synthesizer-produced consensus)

---

## 1. Goal

Attack v0.1 math from four independent lenses, produce a ranked priority list of v0.2 fixes, surface concerns not yet captured in `14_..._synthesis_v0.1.md`. **Decision target for A.6**: which P0/P1 weaknesses absolutely must be fixed in v0.2 vs which can stay open.

Specifically, we want each lens to:
1. **Independently confirm or reject** each of the 6 weaknesses already documented (with reasoning, not vibes).
2. **Surface new concerns** the synthesis missed.
3. **Propose specific v0.2 fixes** — formulas, thresholds, gates, fallback logic.
4. **Issue a verdict** on v0.1 itself: SHIP-AS-IS / REFACTOR / SCRAP-AND-REPLACE.

## 2. Lens design

Four critic lenses + one synthesizer. Lenses are chosen to be **non-overlapping in failure modes** they're best positioned to attack.

| ID | Lens | Primary focus areas (weaknesses #) |
|---|---|---|
| **C1** | **Quant / Statistician** | Empirical math: W2 (Beneish coefficient suppression), W3 (Piotroski cyclical inversion), W5 (Z″ for old firms). Threshold-setting rigor, signal-noise, multicollinearity between gates. |
| **C2** | **Forensic Accountant / Indian GAAP specialist** | Accounting-rule transitions: W1 (regime-shift false positives), W4 (Ind AS 116 break). Restatement handling, consolidated-vs-standalone, related-party flags, segment reporting. |
| **C3** | **Behavioral Finance** | Action-label design: do WATCH/REVIEW/FLAG labels invite harmful action? Disposition effect, action bias, signal hysteresis, churn risk in a quarterly-cadence advisory product. |
| **C4** | **Indian Retail Investor + NSE Specialist** (merged lens) | Usability + market structure: W6 (small sectors / paints sector), BFSI silent skip (does that fail a real portfolio that holds banks?), small/mid-cap coverage, what the labels mean to someone deciding "should I trim?". |
| **S** | **Synthesizer** | Cross-references all 4 critics; identifies unanimous concerns, divergent positions, ranks v0.2 priorities. Produces final `15_cycle_A_critiques_v0.1.md`. |

**Rationale for merging "NSE-specific" into the retail-user lens** (vs. having 5 critics):
- NSE-specific concerns (small sectors, BFSI structure, PSU dominance) are most actionable when filtered through a retail-investor lens: "I hold HDFC Bank — your math silently skips it. That's the question."
- Keeps the critic pool at 4 (matches RESUME directive). Synthesizer makes 5.
- If C4 turns out too broad, A.6 can split it for a later critique cycle.

## 3. Output structure each critic must follow

Every critic agent writes to its own file using the checkpoint protocol (§5). The file must follow this template:

```
# 15X — Cycle A Critique: <Lens Name>

**Status**: 🔄 Initialized — about to begin <lens> critique
**Date**: 2026-05-30
**Lens**: <name>
**Last updated**: <timestamp>

## 1. Verdict on v0.1 (top-line)
One of: SHIP-AS-IS / REFACTOR-REQUIRED / SCRAP-AND-REPLACE
1–2 sentences of reasoning.

## 2. Position on each of the 6 known weaknesses
(One subsection per weakness 1–6. For each: CONFIRM / PARTIAL / REJECT, with reasoning,
and one paragraph on the proposed fix from this lens's perspective.)

### W1 — Beneish false positives during regime shifts
- Position: CONFIRM / PARTIAL / REJECT
- Reasoning (2–4 sentences):
- Proposed v0.2 fix:

### W2 — Beneish false negatives for commodity firms
...

(W3, W4, W5, W6 — same template)

## 3. NEW concerns this lens surfaces (not in synthesis)
(Bulleted list. Each concern: one paragraph. Required: at least 2 new concerns;
the synthesis is empirically incomplete — make me prove it.)

## 4. Proposed v0.2 changes — prioritized
P0 (cannot ship v0.2 without): ...
P1 (strongly desirable): ...
P2 (nice-to-have): ...

## 5. What v0.1 got RIGHT (be fair)
(2–4 bullets. The synthesis already lists what worked; this lens should
either reaffirm or push back on those.)

## 6. One sentence to the synthesizer
"If you carry one thing from this critique into the consensus, it should be: <X>."
```

## 4. Agent prompts (for Pranav's review before spawn)

Each prompt is what gets sent to the agent verbatim. All four critics share an identical preamble; only the lens-specific sections differ.

### Shared preamble (all 4 critics)

```
You are a critic agent for the "Nefarious" project — an AI investment-planning
bot for Indian NSE equities + Mutual Funds. Your job is to critique v0.1 of the
fundamental-analysis (FA) math from a specific lens. Be tough, specific,
and constructive.

# Required reading (in this order)

1. /Users/pranavvenkatesh/analytics/nefarious/market_research/11_cycle_A_math_v0.1.md
   — the math spec being critiqued
2. /Users/pranavvenkatesh/analytics/nefarious/market_research/14_cycle_A_test_synthesis_v0.1.md
   — six structural weaknesses already documented (your floor — don't repeat,
   confirm/reject/extend)
3. /Users/pranavvenkatesh/analytics/nefarious/market_research/12_cycle_A_test_v0.1.md
   — Asian Paints test results (quality compounder profile)
4. /Users/pranavvenkatesh/analytics/nefarious/market_research/13_cycle_A_test_v0.1_TataSteel.md
   — Tata Steel test results (commodity cyclical profile)

OPTIONAL: /Users/pranavvenkatesh/analytics/nefarious/market_research/10_cycle_A_research.md
(the underlying research, only if you need to argue against a research finding)

# Output file (you must create and maintain this)

<<<LENS_OUTPUT_PATH>>>

# Checkpoint protocol (MANDATORY — non-negotiable)

Before reading the input files: use the Write tool to create the output file
with the template structure (see below) and the status line at top:
`🔄 Initialized — about to begin <lens> critique`

After every logical step (reading each input, drafting each section, etc.),
use the Write tool to OVERWRITE the output file with everything accumulated
so far PLUS an updated status line at top. Expected cadence: 15–25 writes
during the run.

When finished, status line at top should read:
`✅ <Lens> critique complete.`

Update the "Last updated" timestamp on every write.

# Output template

<<<TEMPLATE — copy from A5_plan.md §3>>>

# Hard requirements

- Confirm/reject EACH of the 6 documented weaknesses with explicit reasoning.
- Surface at LEAST 2 new concerns the synthesis doesn't already cover.
- Propose specific v0.2 fixes — formulas, thresholds, gate changes. Not "consider
  improving X" but "replace coefficient 4.679 with sector-conditional value: 4.679
  for non-heavy, 2.0 for heavy-industry; rationale: ..."
- Be brutal on issues. Be fair on what works.

# Don't do

- Don't summarize the synthesis. The reader already has it.
- Don't propose implementation (code, data pipelines, architectures). Math + critique only.
- Don't recommend v1.X. Everything stays v0.X.
- Don't suggest going broader than Cycle A — TA, MFs, portfolio sizing are other cycles.

# Constraints

- No version escalation: math stays v0.X.
- Indian NSE context throughout (Indian sector composition, Ind AS, SEBI, AMFI).
- No US-comparison unless directly relevant.
- Hand-written precision — not LLM-fluffy.

# When done
Final write sets status to `✅` and you stop. I will read your output file.
```

### Lens-specific section per critic

**C1 — Quant / Statistician**:
```
# Your lens

You are a quantitative researcher with a stats / signal-processing background.
You think in terms of coefficient sensitivity, multicollinearity, signal-to-noise,
out-of-sample robustness, and how thresholds were chosen.

Your priority focus:
- W2 — Beneish coefficient suppression for commodity firms (TATA term 4.679)
- W3 — Piotroski F-Score anti-correlated with cyclical entry
- W5 — Altman Z″ dominated by century reserves

You should also probe:
- Are the 3 knockout gates (Beneish, Altman, Pledge) statistically independent,
  or do they correlate, multiplying false-positive rates?
- Is the F-Score → action-label mapping in §6 of v0.1 thresholded arbitrarily,
  or does it have empirical justification on NSE data?
- Should knockout gates be additive (sum of penalties) rather than hard halts?
```

**C2 — Forensic Accountant / Indian GAAP specialist**:
```
# Your lens

You are a forensic accountant who has read every Ind AS pronouncement,
been deposed about restatements, and audited NSE-listed conglomerates.
You think in terms of accounting-standard transitions, consolidated-vs-standalone
elections, restatement frequency, and what auditor changes signal.

Your priority focus:
- W1 — Beneish false positives during regime shifts (COVID, demonetization, GST)
- W4 — Ind AS 116 / accounting-standard transitions breaking YoY signals

You should also probe:
- The v0.1 spec uses "consolidated financials throughout" — is that right for
  conglomerates with subsidiary impairments (Tata Steel + Corus)?
- Should restatement frequency or auditor-change frequency be its own knockout?
- Related-party transactions as a share of revenue/cost — should that be a
  manipulation flag in addition to Beneish?
- Pledge data: the v0.1 spec uses ">30% of promoter holding" — is the actual
  forced-liquidation threshold under SEBI rules different?
```

**C3 — Behavioral Finance**:
```
# Your lens

You are a behavioral finance researcher who studies disposition effect, action
bias, and how investor decisions degrade when interfaces invite reaction.
You read action labels as nudges, not just outputs.

Your priority focus:
- The four action labels (HOLD / WATCH / REVIEW / FLAG) and what they nudge.
- Hysteresis: a stock that wobbles between WATCH and HOLD across quarters —
  does that produce a "do nothing" response or a "trim then re-buy" cycle?
- Churn: a weekly report (per Q9) showing a HOLD → WATCH transition with
  no other context — what % of retail investors trim on that signal?
- The asymmetry of the math being wrong: a false FLAG (Asian Paints Mar-2022)
  causes a needless sale; a false HOLD (Tata Steel Mar-2021) causes a peak
  entry. Which is worse, given the disposition effect?

You should also probe:
- Should the labels include hysteresis (don't flip a label until the change
  has held for N consecutive quarters)?
- Is REVIEW even useful? "Material concerns; user should re-examine" —
  re-examine what? Without an actionable next step, REVIEW = noise.
- Should there be a "do nothing" affirmative label distinct from HOLD?
```

**C4 — Indian Retail Investor + NSE Specialist**:
```
# Your lens

You are a 35-year-old Indian retail investor with a 12-stock NSE portfolio
that includes 2 banks (HDFC Bank, ICICI Bank), 3 NIFTY 50 names, 4 mid-caps,
and 3 specialty-chemicals companies. You read the math, then ask: "What does
this tell me about my actual holdings?"

Your priority focus:
- W6 — Sector ROCE percentile fails on small sectors. You hold specialty
  chemicals — are those bucketed correctly?
- BFSI silent skip — your two largest holdings are banks. The bot saying
  "SKIPPED-BFSI" for them is useless. Is that acceptable for v0.1, or
  is it a critical gap?
- The labels (HOLD/WATCH/REVIEW/FLAG) — do they answer "should I trim?"
  Do they tell you anything about sizing or about which thesis is at risk?
- The math runs trailing-only — but you bought ITC at ₹220 in 2019 because
  you thought FMCG would mean-revert. Trailing-only would tell you nothing
  about that thesis being intact / broken.

You should also probe:
- The output report is weekly (per Q9). Will you actually read 12 reports
  per week? Or does a 12-stock portfolio need a "delta-only" view?
- The "thesis-entry framing" (Q10) — does v0.1 math actually let you
  decide "thesis intact Y/N", or is it just labels?
- PSU stocks (Coal India was deferred). Do the same gates work? Or do
  state-owned enterprises need their own pipeline?
- Mid-cap and small-cap — do all NIFTY 500 names have data quality
  sufficient for Beneish (which needs 2 years of consolidated)? If not,
  what fraction of NIFTY 500 silently INSUFFICIENT-DATA?
```

### Synthesizer prompt (separate, runs after critics finish)

```
You are the synthesizer agent for the A.5 multi-agent critique of v0.1 FA math.
Your job is to read all 4 critic outputs, identify cross-critic consensus,
surface divergence, and produce the final consensus document.

# Required reading

1. /Users/pranavvenkatesh/analytics/nefarious/market_research/11_cycle_A_math_v0.1.md
   — the math being critiqued
2. /Users/pranavvenkatesh/analytics/nefarious/market_research/14_cycle_A_test_synthesis_v0.1.md
   — the existing 6-weakness synthesis (the floor)
3. /Users/pranavvenkatesh/analytics/nefarious/market_research/15a_critic_quant.md
4. /Users/pranavvenkatesh/analytics/nefarious/market_research/15b_critic_forensic.md
5. /Users/pranavvenkatesh/analytics/nefarious/market_research/15c_critic_behavioral.md
6. /Users/pranavvenkatesh/analytics/nefarious/market_research/15d_critic_retail_nse.md

# Output file

/Users/pranavvenkatesh/analytics/nefarious/market_research/15_cycle_A_critiques_v0.1.md

# Checkpoint protocol — MANDATORY (same as critics)

Initialize, then overwrite after each section. Final status `✅ Synthesis complete.`

# Output structure

## 1. Cross-critic verdict on v0.1 (top-line)
Each critic's verdict in one row, then your synthesized verdict.

## 2. Per-weakness consensus
For each of W1–W6: how did all 4 critics position (CONFIRM/PARTIAL/REJECT)?
Where they agree, lock as consensus. Where they diverge, document the divergence.

## 3. NEW concerns surfaced by critics (additional to W1–W6)
Aggregate all "new concerns" sections. De-duplicate, group thematically.

## 4. Ranked v0.2 priorities — synthesized
P0 (unanimous, cannot ship without):
P1 (3 of 4 critics agree):
P2 (2 of 4 or recommended by single specialist lens):
P3 (1 critic; document for later cycles):

## 5. What v0.1 got RIGHT (consensus)
Across all 4 critics, what did they agree was working?

## 6. Specific math changes for A.6 (the v0.2 refactor brief)
Concrete prescriptions:
- Knockout gates: [keep / downgrade / replace]
- Beneish formula: [change / accept-with-overlay]
- Piotroski for cyclicals: [exclude / invert / supplement]
- Ind AS 116 transition handling: [skip-year-pair / normalize]
- Z″ for old firms: [replace / supplement]
- Sector percentile small-N: [fallback / alternative metric]
- Action label set: [keep / hysteresis-add / restructure]
- BFSI carve-out: [v0.1 silent skip acceptable / must be in v0.2]

## 7. Idea-review trigger check
Does anything in the critique require updating the v0.3 problem statement
to v0.4? Specifically:
- Asset universe (W6 implies small-sector quality compounders may be hidden)
- Time horizon (W3 implies cyclicals need cycle-position awareness — does
  the Q9 weekly cadence still make sense?)
- TA/FA conflict (Q5) — has anything in the critique changed how this
  should be resolved?

# Hard requirements

- Read all 4 critic files cover-to-cover. Don't skim.
- Where critics disagree, surface the disagreement. Don't paper over it.
- Be specific in §6. v0.2 will be written from this; vague prescriptions
  produce vague code.

# Constraints

- Stay v0.X.
- Indian NSE context.
- No implementation. Math + critique only.
```

## 5. Checkpoint protocol (recap)

Per `LEARNINGS.md` §2.2 and `RESUME.md` §6:

- All 5 agents run with `run_in_background: true`.
- Each agent initializes its output file before reading anything.
- Each agent overwrites its file after every logical step (15–25 writes per run).
- Pranav (or I) can `Read` any agent's file mid-run to see live progress.
- Final status line: `✅ <X> complete.`

## 6. Execution sequence

```
Step 1: Spawn C1, C2, C3, C4 in parallel (4 background agents)
        — same message, 4 Agent tool calls
        — wait for all 4 to complete (Claude is notified on completion)

Step 2: Read all 4 critic files; verify they completed without errors

Step 3: Spawn synthesizer S in background
        — reads all 4 critic files
        — produces 15_cycle_A_critiques_v0.1.md

Step 4: Read final synthesizer output. Confirm task #20 complete.

Step 5: Bundle commit:
        - 4 staged Day-1-close docs (LEARNINGS, RESUME, CLAUDE, session log)
        - A5_plan.md (this file)
        - 15a_critic_quant.md, 15b_critic_forensic.md, 15c_critic_behavioral.md, 15d_critic_retail_nse.md
        - 15_cycle_A_critiques_v0.1.md
        - (updated session log with A.5 entry — added at commit time)

Step 6: Push, open PR #2.
```

## 7. Time estimate

| Phase | Wall-clock |
|---|---|
| 4 critics in parallel | 15–25 min (each runs ~15–20 min independently) |
| Synthesizer | 8–15 min |
| Total wall-clock for A.5 | ~25–40 min |

Compared to A.4 (32 min for 2 stocks sequentially), this should be similar wall-clock — gains from parallelism, losses from a higher number of agents and a serial synthesizer.

## 8. Output files (after A.5 completes)

| File | Author | Purpose |
|---|---|---|
| `A5_plan.md` | this doc | Plan + agent prompts (this file) |
| `15a_critic_quant.md` | C1 | Quant lens critique |
| `15b_critic_forensic.md` | C2 | Forensic accountant lens critique |
| `15c_critic_behavioral.md` | C3 | Behavioral finance lens critique |
| `15d_critic_retail_nse.md` | C4 | Indian retail investor + NSE lens critique |
| **`15_cycle_A_critiques_v0.1.md`** | S | Synthesized consensus + v0.2 brief |

## 9. After A.5 closes (preview of A.6)

The synthesizer's §6 ("Specific math changes for A.6") becomes the **A.6 brief**.
That brief drives `16_cycle_A_math_v0.2.md`.

If A.5 surfaces an idea-review trigger (§7 of synthesizer output), we draft `v0.4` of
the problem statement before A.6 — but only if it's clearly necessary. Otherwise v0.3
stays locked.

---

## 10. Open before spawning agents

Pranav should confirm:
- 4 critic lenses are the right cut (vs 3 or 5)?
- Output filenames OK?
- Should the synthesizer ALSO have an "idea-review" recommendation, or is that
  Pranav's call alone?

**If Pranav doesn't push back on any of the above within his next message, proceed to spawn.**

---

**End of A.5 plan. Ready for execution.**
