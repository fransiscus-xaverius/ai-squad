---
name: QA Playwright Validation
description: Design and execute QA test cases with evidence capture, including Playwright-based UI validation and verdict reporting
---

# QA Playwright Validation

Use this skill for QA planning and execution in phased workflows. QA is evidence-driven: no pass claim without fresh, reproducible evidence.

## Framework alignment
- Follow canonical workflow in `README.md`, `harness/engineering-harness.md`, `core/artifacts.md`, and `phase-execution`.
- QA test design/review happens before implementation each phase; QA verdict gates phase completion.
- Verdicts: **PASS / FAIL / BLOCKED**. Record scope, env/prereqs, steps, expected vs actual, evidence, defects, and recommendation.
- Distinguish **product defects** from **environment/test-harness issues** with rationale when inferable.

## Prerequisites (UI/browser automation)
UI automation claims require all of the following (or must be marked blocked/unverified):
- Node.js + package manager available
- Playwright installed (`npx playwright --version` or project dependency)
- Browsers installed: `npx playwright install` (Linux/CI may need `npx playwright install --with-deps`)
- Target application runnable locally for testing (URL/dev server/build)

**Rule:** if prerequisites/app/runtime are unavailable, report UI automation as **BLOCKED/UNVERIFIED (never PASS)**, include setup commands attempted and gaps, and record in QA verdict and `implementation-state.md`.

## Test planning
- Translate phase acceptance criteria into concrete cases in `qa/<session-id>/test-plan.md` (and cases/results/evidence as needed).
- For each case: preconditions/setup data, steps, expected result, automation/manual method, and traceability to criteria/phase.
- Cover: happy path, key edge/error/empty/permission/loading states in scope, and regression-sensitive behavior.
- For UI phases, plan selector strategy and critical flows requiring stable `data-testid` hooks.

## Locator and selector strategy (Playwright + Testing Library guidance)
Prefer selectors that reflect user-visible behavior and accessible semantics; keep tests resilient to implementation churn.
1. **User-facing/accessible first:** roles/names/labels/text/alt/title where stable and meaningful (`getByRole`, `getByLabel`, `getByText`, etc.).
2. **`data-testid` for QA-critical hooks:** when role/label/text is ambiguous, dynamic, or unstable, use stable `data-testid` attributes provided/maintained by frontend implementation. Do not rely on brittle CSS/XPath or incidental structure.
3. **Chaining/filtering:** scope locators within regions/containers to disambiguate.
4. **Avoid:** selectors tied to styling classes, deep DOM paths, or copy that changes frequently unless explicitly asserted.

Coordinate selector additions/changes with frontend engineers and document in handoff/artifacts.

## Execution best practices
- **Test isolation:** tests should be independent (fresh state/contexts) and not depend on order; avoid shared mutable state.
- **Web-first assertions and auto-waiting:** prefer Playwright assertions that wait/retry for conditions (visibility, text, state) over manual sleeps or non-waiting checks.
- **Avoid flakiness:** do not use arbitrary timeouts/waits; wait on observable conditions, network/app readiness signals, or deterministic fixtures as appropriate.
- **Network/external dependencies:** control test data/environment where possible; mock/stub only as appropriate and document deviations from real integration.
- **Evidence capture:** collect command outputs, screenshots, traces, videos, and logs (especially on failure). Use trace viewer artifacts when available for actionable debugging.
- **Cross-browser/config (when in scope):** run against configured projects/browsers relevant to acceptance criteria and report coverage.

## Environment and CI considerations
- Run only required browsers/dependencies in constrained environments.
- Prefer reproducible environments (pinned deps/browsers, controlled data, known app URL/build).
- On CI/failures, traces/logs/screenshots are primary debugging evidence; record paths in verdicts.
- Use parallelism/sharding only when tests are isolated and environment supports it.

## Verdict report
Produce a clear report in `qa/<session-id>/results/...` including:
- Scope tested and mapping to acceptance criteria/cases
- Environment and prerequisites status (Playwright/app/runtime)
- Executed cases/steps and results (expected vs actual)
- Evidence paths (commands, screenshots, traces/videos/logs)
- Defects with severity, repro steps, and observed impact
- Product defect vs environment/test-harness issue assessment (with rationale)
- Verdict: **PASS / FAIL / BLOCKED** and recommendation (proceed/fix/retry/escalate)

## References
- Playwright Best Practices: https://playwright.dev/docs/best-practices
- Playwright Locators: https://playwright.dev/docs/locators
- Playwright Assertions: https://playwright.dev/docs/test-assertions
- Playwright Fixtures/Isolation: https://playwright.dev/docs/test-fixtures
- Playwright Trace Viewer: https://playwright.dev/docs/trace-viewer-intro
- Playwright CI: https://playwright.dev/docs/ci
- Testing Library Queries/Priority: https://testing-library.com/docs/queries/about/
