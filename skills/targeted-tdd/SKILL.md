---
name: Targeted TDD
description: For bug fixes or behavior changes, capture intended behavior with a failing check first when practical, then fix and verify; use closest executable evidence when tests are impractical
---

# Targeted TDD (Bug Fix / Regression)

Focused TDD workflow for defects and regressions where a narrow, practical executable check is feasible.

## Workflow
1. **Understand the bug**
   - Identify intended vs actual behavior, affected path, scope/impact, and smallest reliable reproduction.
   - Gather evidence (error, logs, failing case, user-visible symptom).
2. **Choose narrowest executable check**
   - Prefer the closest existing automated test (unit/integration/component/e2e) for the affected path.
   - If no practical automated test path exists, select the closest executable regression check instead of forcing low-value test scaffolding.
3. **Write/check fails first (when practical)**
   - Encode intended behavior or reproduce the defect.
   - Run now and confirm failure for the expected reason; capture evidence.
4. **Fix minimally**
   - Apply the smallest root-cause fix within scope; avoid unrelated changes.
5. **Verify**
   - Re-run the failing check (now passing) and relevant regressions for touched scope.
   - Capture fresh evidence (`verification-before-completion`).

## When automated tests are impractical
- State why (harness cost, nondeterminism, external dependency, environment constraint, unavailable prerequisite).
- Provide strongest alternative executable evidence: scripted repro, manual steps with outputs/screenshots/traces/logs, or targeted runtime assertions.
- Do not claim automated coverage that was not executed; record residual risk.

## Guardrails
- Do not weaken or change tests to fit broken behavior unless requirements/spec changed (record approval/decision).
- Keep checks deterministic and behavior-focused.
- Pair with `systematic-debugging`, `fix-root-causes`, and `attack-the-premise` (on repeated same-gate failures).

## References
- Superpowers, *Systematic Debugging* / *Test-Driven Development* (workflow patterns): https://github.com/obra/superpowers
- Playwright Best Practices (reliable checks/evidence): https://playwright.dev/docs/best-practices
- Testing Library Guiding Principles: https://testing-library.com/docs/queries/about/
