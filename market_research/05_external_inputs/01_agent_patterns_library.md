# External Input — Agent Patterns Library

**Source**: https://agent-patterns.readthedocs.io/en/latest/
**Captured**: 2026-06-06
**Why this matters**: Catalogues 9 production-ready agent patterns. Three of them map directly onto what we've been building organically in Phase 2. Helps name what we already do, plus surfaces gaps.

---

## The 9 patterns covered

| # | Pattern | What it is | Direct relevance to our project |
|---|---|---|---|
| 1 | **ReAct** | Tool-using cycles (reason then act) | We use it implicitly in agent workflows |
| 2 | **Reflection** | Generate → critique → refine | **Direct match**: our cycle research → math → test → critique → refine loop is a coarse-grained Reflection pattern |
| 3 | Plan & Solve | Structured task decomposition | Used in our cycle-level planning |
| 4 | Self-Discovery | Adaptive reasoning strategy | Not used currently |
| 5 | **Reflexion** | Learning from execution failures | **Partial match**: each cycle's v0.4 candidate list IS Reflexion at the cycle level (catalogues what failed for next iteration). We don't yet feed it back into the agent's prompts though. |
| 6 | REWOO | Cost-efficient planner-worker | Not used; might be relevant for B.4-style mass testing |
| 7 | LATS | Tree search over solution paths | Not used; possibly Cycle D/F territory |
| 8 | LLM Compiler | Parallel independent subtasks | **Direct match**: we use this every time we spawn 5 critics in parallel per M6 lesson |
| 9 | **STORM** | Multi-perspective research synthesis | **Direct match**: our 5-critic + synthesizer pattern in A.5 and B.5 IS STORM |

---

## Core thesis of the library

The library is built around the idea that **enterprise-grade prompt engineering** is the differentiator. The 0.2.0 redesign expanded system prompts from ~32 lines to "150-300+ lines" with a "9-section structure" — role, capabilities, process, output format, decision-making, quality standards, edge cases, examples, critical reminders.

**Read our agent prompts against this bar**: our A.5 / B.5 critic prompts are ~50-70 lines each (light protocol). The B.4 test agents were ~70-100 lines (heavy protocol). We're under-prompting per the library's recommendation. The library claims 150-300 lines is needed for "production-grade" agents — though "production" here means commercial product, not personal research.

For our personal-research use case, lighter prompts probably remain appropriate. But for the meta-experiment (validating the technique itself), it's worth testing the heavy-prompt approach for at least one critic.

---

## Specific patterns most directly relevant to the Blog #2 senior comment

The senior commenter critiqued the multi-agent pattern. Two patterns from this library are directly responsive:

### Reflection — the foundational generate/critique/refine loop
- **What it adds**: structures the "agent critiques itself" loop more rigorously
- **Limitation it does NOT solve**: same-model blind spots (the senior comment's central critique)
- **Useful for us**: documenting our existing cycle pattern with a recognized name

### STORM — multi-perspective synthesis
- **What it adds**: framework for combining outputs from multiple distinct perspectives
- **Limitation it does NOT solve**: same-model perspectives are still same-model
- **Useful for us**: the official version of what we built in A.5 / B.5. If we read the STORM paper carefully, we may find prompt-design guidance we haven't applied.

### What the library suggests for hybrid critique workflows
> "Start with a Reflection pattern loop for per-response critique, nest a STORM pattern for multi-model perspective gathering, and apply Reflexion-style failure learning across iterations."

**Reading this against our actual work**: that's a clean description of what we built — Reflection at the cycle level, STORM at the critique step, Reflexion at the v0.X candidate queue. We've been doing it from first principles. The library names it and provides patterns we could borrow for prompt design.

---

## Methodology recommendations from the library

1. **9-section system-prompt structure** for any critique or synthesis agent: Role / Capabilities / Process / Output Format / Decision-Making Guidelines / Quality Standards / Edge Cases / Examples / Critical Reminders
2. **Role-based configuration**: assign different LLMs to different steps. E.g., lightweight critic + heavyweight synthesizer. (This intersects directly with the senior comment's cross-model prescription.)
3. **Iterative prompt tuning**: emphasizes testing custom instructions explicitly
4. **Pattern composition**: hybrid approaches (Reflection + STORM + Reflexion) outperform single patterns for complex critique work

---

## What this changes for us

| Recommendation | Effort | Worth doing? |
|---|---|---|
| Expand B.5-style critic prompts to 9-section / 150-300 line structure | Medium | Maybe for meta-experiment; overkill for routine use |
| Cross-model role configuration (Claude + Gemini + GPT) | High | **YES — directly addresses senior comment's critique** |
| Document our existing patterns using Reflection / STORM / Reflexion names | Low | YES — improves clarity for future blogs/docs |
| Read the STORM original paper for prompt-design specifics | Low-Medium | YES — quick win |
| Apply Reflexion-style explicit failure-feedback loops | Medium | YES for Cycle B.6 — the v0.4 candidates from B.5 are de facto failure signals; can we make the loop tighter? |

---

## Bottom line

This library doesn't invalidate what we built. It validates the architecture — we organically converged on Reflection + STORM + Reflexion patterns. The senior commenter's critique still stands (same-model blind spots), and one of the library's own recommendations (role-based cross-model configuration) is the most direct fix.

**Two concrete actions surfaced**:
1. Read STORM paper for prompt-design specifics → upgrade our critic prompts
2. Adopt cross-model configuration for at least the synthesizer role going forward
