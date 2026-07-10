# R4 Process/Methodology — Repo Review Issues

## Issue 1
**Title**: [process] Same-model blind-spot not addressed in Phase 2 critique step
**Labels**: process, methodology, critique-pattern
**Body**:
**Problem**: `09_phase_2_plan.md` §"The cycle" describes step 5 as "multi-agent critics attack math + test results" with no qualification about model diversity. The plan was last edited at v0.2 (2026-05-30) — before the Blog #2 senior comment (captured 2026-06-06) identified the structural flaw that all critics sharing the same training distribution produce "self-confirmation with extra steps."

`LEARNINGS.md` Part 11.10 acknowledges cross-model is "on the roadmap" but marks it as a note, not a protocol change. `01_agent_patterns_library.md` explicitly recommends "role-based cross-model configuration" as a concrete fix. Neither of these back-propagates into `09_phase_2_plan.md` step 5 or into any cycle-level checklist.

**Why it matters**: Cycle C.5, D.5, E.5, F.5 will all run under the same flawed single-model critique assumption unless the plan document is updated. A future contributor or a fresh Claude session reading `09_phase_2_plan.md` as the authoritative process document will spawn five same-model critics with no flag that this is a known architectural limitation.

**Suggested fix**: Add a note to `09_phase_2_plan.md` §"The cycle" step 5 — something like: "NOTE (added after Cycle B): all critics run on the same model. This is a known limitation (shared training distribution → shared blind spots). Mitigation: (a) adversarial framing in prompts ('you must find at least 3 faults; agreement is not a verdict'), (b) Pranav-as-final-arbiter is non-negotiable, (c) cross-model critic is the roadmap upgrade." A one-paragraph addition prevents silent repetition of a documented flaw.

---

## Issue 2
**Title**: [process] "When to close a cycle" has no numeric criterion — loop is open-ended
**Labels**: process, methodology, cycle-management
**Body**:
**Problem**: `09_phase_2_plan.md` §"The cycle" says "LOOP 4–6 until math is stable" with no definition of "stable." The "What happens at end of Cycle A" section says "Math is locked at some v0.x" — equally vague. `LEARNINGS.md` Part 7 explicitly flags this as an open question ("When does Phase 2 close? Need a definition of 'math stable' that ends the cycle loop") but marks it unresolved.

`LEARNINGS.md` Part 10.3 contains the empirical answer learned from closing Cycle A: "Diminishing returns become visible after 3 iterations. v0.4 work would be cosmetic refinement on 2 already-OK fixes, not material change in direction. Closing Cycle A at v0.3 is correct." Part 11.1 gives B.4's 53% hit rate vs 60% target as a concrete threshold. This criterion exists in the record but is never codified as a decision rule in the plan document.

**Why it matters**: Without a documented criterion, each cycle close is an implicit judgment call. A future contributor (or Claude) has no basis to propose or challenge closure — they can only observe that Pranav decided. If Pranav is unavailable for a session, no proxy decision can be made. The loop can run indefinitely.

**Suggested fix**: Add a "Cycle close criteria" section to `09_phase_2_plan.md` capturing the two signals that worked in Cycle A: (a) hit rate on multi-stock test meets target (60% baseline; adjust per cycle), (b) new iteration produces only cosmetic fixes (≤2 material new weaknesses, both already-queued-for-Cycle-F). Link to `LEARNINGS.md` §10.3 where the empirical basis lives.

---

## Issue 3
**Title**: [process] Heavy vs light checkpoint protocol undocumented in plan — agent spawning is inconsistent
**Labels**: process, methodology, agent-protocol
**Body**:
**Problem**: `09_phase_2_plan.md` contains no mention of checkpoint protocol for agent runs. The distinction between the heavy protocol (≥25 writes, for math-test agents >5 min) and the light protocol (≥4 writes, for review-style agents) exists only in `LEARNINGS.md` — Part 2.2 for heavy, Part 9.3 for light, Part 10.4 as a cycle-close lesson. These are lessons from past incidents, not instructions for future runs.

A future contributor (or a fresh Claude session that reads `09_phase_2_plan.md` but skips LEARNINGS) will spawn test agents (A.4-style, B.4-style) with no checkpoint protocol, reproducing mistake M2 (55-min foreground agent, all work lost on interrupt). The plan document does not reference LEARNINGS.md at all, let alone its §2.2 checkpoint rule.

**Why it matters**: The checkpoint protocol was the fix for the single most costly mistake in the project (M2: 55-min lost agent run). It's in LEARNINGS but not in the place a contributor reads before spawning an agent for a new cycle. The knowledge is siloed.

**Suggested fix**: Add a "Agent spawning rules" section to `09_phase_2_plan.md` (3–5 bullet points): always run background mode for >5 min, heavy checkpoint (≥25 writes) for math-test agents, light checkpoint (≥4 writes) for review agents, always confirm prompts before spawning, and a pointer to `LEARNINGS.md` §2.2 for full rationale.

---

## Issue 4
**Title**: [process] Mid-cycle external feedback has no documented integration path
**Labels**: process, methodology, external-input
**Body**:
**Problem**: The Blog #2 senior comment (`04_blog_posts/post_02_multi_agent_critique/feedback/01_comment_senior_critique.md`) arrived mid-project and generated a set of prescriptions that affect the ongoing math critique process. Its prescriptions (cross-model critics, adversarial framing, human-as-arbiter as explicit protocol) are partially absorbed into `LEARNINGS.md` Part 11.3 but are not reflected in any cycle step, process document, or checklist for Cycles C–F.

`09_phase_2_plan.md` has no concept of "external input" at all. There is no documented step for: (a) how an external finding gets assessed against the current cycle plan, (b) whether it triggers a revision of the plan document, (c) who decides if it's incorporated vs deferred vs rejected. The `05_external_inputs/` folder exists as a landing pad for such inputs but has no protocol document.

**Why it matters**: The senior comment is the highest-signal external input the project has received. If the correct response to it is only "note it in LEARNINGS," then Cycles C–F run under the same critique architecture the comment critiqued. If the correct response is "update the plan," that update hasn't happened. Either way, the silence is a process gap: there's no documented decision.

**Suggested fix**: Add a short "Handling external inputs" subsection to `09_phase_2_plan.md` (or a `05_external_inputs/00_integration_protocol.md`). It needs to answer: what triggers a plan-level change vs a LEARNINGS note vs a deferral? Who makes the call? What's the expected latency between receiving feedback and deciding disposition? The senior comment is the first test case; its disposition should be the first example in the protocol.

---

## Issue 5
**Title**: [process] v0.X versioning convention codified in LEARNINGS but not linked from plan
**Labels**: process, documentation, versioning
**Body**:
**Problem**: `09_phase_2_plan.md` §"Versioning rules (locked)" states the v0.X convention concisely. `LEARNINGS.md` Part 2.5 restates it in more detail. However, neither document links to the other, and neither explains the *trigger* for incrementing a version number (v0.1 → v0.2) vs closing a cycle. The plan says math specs go "v0.1 → v0.2 → v0.3 ... per refinement" but "per refinement" is undefined — does a single critic finding justify a new version file? Does the hit-rate threshold matter? Does a Pranav pick trigger one?

In practice, Cycle A created `math_v0.1`, `math_v0.2`, `math_v0.3` — one per critique/refine loop. But this was never written as a rule. A future contributor might create a `math_v0.4` mid-cycle (after a single suggestion) or skip a version entirely.

**Why it matters**: File-numbering ambiguity produces repository state that's harder to read. If a fresh contributor sees `math_v0.2.md` and `math_v0.4.md` with no `v0.3.md`, they can't tell if `v0.3` was deleted, never created, or is in another folder. Version inflation (creating a new file after every small change) bloats the directory and obscures which version marks a cycle milestone.

**Suggested fix**: Add two lines to `09_phase_2_plan.md` §"Versioning rules": "A new version file is created once per critique-and-refine loop iteration (i.e., once per full pass through steps 4–6), not per individual critic finding. Minor edits within a loop stay in the same version file." This aligns with how Cycle A actually ran and prevents version inflation.

---

## Issue 6
**Title**: [process] 9-section prompt recommendation undocumented as deliberate non-adoption
**Labels**: process, methodology, prompt-engineering
**Body**:
**Problem**: `01_agent_patterns_library.md` documents that the agent-patterns library recommends 9-section system prompts (150–300 lines) for "enterprise-grade" critique agents, vs our current ~50–70 line light-protocol prompts. The file notes this gap explicitly: "We're under-prompting per the library's recommendation." It then says "lighter prompts probably remain appropriate" for personal research — but this is a conclusion buried in an external-input capture file, not a documented methodology decision in any process document.

`09_phase_2_plan.md` contains no prompt-design guidance at all. `LEARNINGS.md` mentions prompt compactness only in the context of preventing stalls (Part 9.3). The recommendation to test 9-section prompts "for at least one critic" in a meta-experiment (`01_agent_patterns_library.md` §"What this changes") has no corresponding task, no assigned cycle, and no documented decision about whether to proceed.

**Why it matters**: A future contributor running a Cycle C.5 critique has no guidance on prompt design. They could write a 30-line prompt or a 300-line prompt with equal justification. If the meta-experiment (does heavier prompting improve critique quality?) is never run, we never know whether our 53% hit rate in B.4 was partially a prompt-quality problem. The gap is both a replicability issue and an unresolved methodology question.

**Suggested fix**: Document in `09_phase_2_plan.md` §"The cycle" step 5 (or a new "Prompt design" note): "Our critic prompts run ~50–70 lines (light protocol). The agent-patterns library recommends 150–300 lines for production use. We adopt lighter prompts because (a) our use case is personal research, not production, and (b) longer prompts have stalled agents in our experience (M6). The meta-experiment comparing heavy vs light prompt structure is deferred to a standalone evaluation — not part of the cycle loop." This converts an implicit assumption into a documented choice.

---

✅ 6 issues ready for filing. Output complete.
