---
name: Test-Driven Development
description: Implement features and behavior changes with strict red-green-refactor discipline and evidence that tests failed before passing
---

# Test-Driven Development (TDD)

## Iron law
**No production behavior change without a failing test/check first, unless an explicit exception is approved and recorded.**

If you did not observe the test fail for the expected reason, you do not know it validates the intended behavior.

## When to use
- New features, bug fixes, refactoring with behavior risk, and behavior changes.
- Apply within assigned phase scope, acceptance criteria, and project testing conventions.

## Red-Green-Refactor cycle
1. **RED — define behavior**
   - Write the smallest automated test/check that expresses required behavior or reproduces the bug.
   - Align with PRD/plan/spec acceptance criteria.
2. **Verify RED — watch it fail**
   - Run targeted test/check now and confirm it fails for the expected reason (not typo/env/setup noise).
   - Capture failing evidence (command, key output, status).
3. **GREEN — minimal implementation**
   - Implement only what is needed to satisfy the test and in-scope criteria.
   - Avoid speculative work/refactors (`ponytail`).
4. **Verify GREEN — watch it pass**
   - Re-run targeted test/check and relevant local/regression checks for touched scope.
   - Capture passing evidence.
5. **REFACTOR — improve safely**
   - Refactor with checks green; preserve behavior unless in scope and specified.
   - Re-run relevant checks after refactor.

## Framework alignment
- Engineers report RED/GREEN (and refactor verification) evidence in handoffs.
- Frontend changes must add/maintain stable `data-testid` for QA-critical interactions.
- If required checks cannot run (including Playwright/UI prerequisites), do not claim pass; record blocker/gap and verified alternatives in artifacts.
- On retries, combine with `systematic-debugging`/`fix-root-causes`; if same gate/pattern repeats, apply `attack-the-premise` before another attempt.
- Apply `verification-before-completion` before claiming done.

## Exceptions (rare, explicit)
Allowed only with approval recorded in artifacts (e.g. exploratory spike, generated/vendor-only edits, or no practical automated check). In that case:
- State why TDD is impractical for this change.
- Provide strongest feasible alternative verification (scripted repro, manual steps with outputs, targeted runtime checks).
- Document residual risk and follow-up test work if needed.

## References
- Superpowers, *Test-Driven Development*: https://github.com/obra/superpowers
- Kent Beck, *Test Driven Development: By Example* (canonical TDD practice)
- Martin Fowler, *Refactoring* / testing discipline (general practice)
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
