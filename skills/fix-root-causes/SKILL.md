---
name: Fix Root Causes
description: Debug by tracing symptoms to the first faulty decision/state and fixing the cause, not the surface symptom
---

# Fix Root Causes

## Core rule
**Do not patch symptoms. Identify and fix the first faulty decision, state transition, or contract violation that produces the observed failure.**

## Workflow
1. **Capture evidence:** symptom, exact error/output, reproduction steps, environment, and affected scope.
2. **Trace backward:** follow data/control flow from failure point to origin (inputs, validation, state, boundaries, dependencies).
3. **Isolate cause:** distinguish root cause from contributing factors and downstream effects; validate with targeted checks.
4. **Fix at source:** implement smallest correct fix within scope that prevents recurrence for the same class/cause.
5. **Verify:** re-run reproduction/failing check and relevant regressions with fresh evidence.
6. **Record:** document symptom, evidence, root cause, fix rationale, verification, and residual risks.

## Guardrails
- Avoid "whack-a-mole" fixes that merely suppress visible symptoms.
- If cause spans boundaries/contracts, identify owning boundary and coordinate via TL/spec/artifacts.
- When multiple plausible causes exist, test hypotheses systematically (`systematic-debugging`), not in parallel guesswork.
- If repeated attempts fail the same gate, reassess assumptions/premises (`attack-the-premise`) before retry.

## Framework alignment
- Required mindset for retries in `phase-execution` and for accepted review findings.
- Update `implementation-state.md` (and QA/review artifacts as relevant) with root-cause analysis and evidence.
- Pair with `verification-before-completion`, `test-driven-development`/`targeted-tdd`, and `correct` for durable prevention.

## References
- Superpowers, *Systematic Debugging*: https://github.com/obra/superpowers
- Anthropic, *Effective harnesses for long-running agents* (failure diagnosis/evidence): https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Node.js diagnostics/async behavior (context for backend tracing): https://nodejs.org/en/learn
