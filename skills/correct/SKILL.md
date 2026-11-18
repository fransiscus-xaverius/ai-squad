---
name: Correct
description: Convert repeated mistakes into durable prevention (design, types, checks, tests) with evidence that the guard catches the original failure
---

# Correct (Durable Prevention)

Use when the same class of mistake recurs (bugs, QA escapes, repeated review findings, flaky assumptions).

## Procedure
1. **Define the mistake class (evidence-based):** collect concrete instances; describe narrowly what went wrong and why it was possible.
2. **Choose highest effective enforcement (prefer in order):**
   - Eliminate by design/single source of truth
   - Make invalid states unrepresentable (types/contracts/schemas/invariants)
   - Automated guard (lint/static/CI/runtime check) with actionable feedback
   - Behavior/regression test
   - Documentation/checklist only for judgment calls that cannot be enforced
3. **Implement smallest durable fix** within approved scope (`ponytail`, `boundary-discipline`, subtract-before-add when safe).
4. **Prove the guard works:** demonstrate it fails/catches the original class (or reproduction) and passes after fix; capture evidence.
5. **Record and propagate:** update `implementation-state.md` and relevant artifacts with cause, guard, evidence, and result; update canonical docs/skills/templates if the lesson should prevent future recurrence.

## Framework alignment
- Complements `fix-root-causes`, `attack-the-premise`, `test-driven-development`/`targeted-tdd`, and `artifact-state`.
- Escalate when prevention requires material architecture/scope change or cross-team decisions.

## References
- Superpowers, *Systematic Debugging* and prevention mindset: https://github.com/obra/superpowers
- pstack, *correct* (adapted): https://github.com/cursor/plugins
- Anthropic, *Effective harnesses for long-running agents* (learning captured in artifacts): https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
