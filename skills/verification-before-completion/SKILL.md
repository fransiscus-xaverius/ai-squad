---
name: Verification Before Completion
description: Require fresh, command-backed evidence before claiming any task, phase, fix, or review outcome is complete or passing
---

# Verification Before Completion

## Iron law
**No completion, pass, or fix claim without fresh verification evidence collected now.**

Evidence before assertions applies to engineers, QA, reviewers, and orchestrators.

## Gate function (before any status claim)
1. **Identify the claim:** what exactly is asserted (tests pass, bug fixed, build clean, acceptance criterion met, UI flow works, finding resolved).
2. **Identify proof:** command(s), test(s), artifact(s), or observation(s) that can prove it.
3. **Run/collect now:** execute in current state/workspace (not memory, not prior run).
4. **Read and report:** command(s), relevant output/result, exit/suite status, scope/environment covered, and evidence paths.
5. **State outcome accurately:** **PASSED / FAILED / BLOCKED / PARTIALLY VERIFIED** with evidence. If blocked/partial, specify what was not verified and why.

## Evidence standards
- Tie evidence to scoped acceptance criteria and artifact paths (`tech-notes/<session-id>/`, `qa/<session-id>/`, `reviews/<session-id>/`).
- Prefer targeted checks first, then broader/regression checks as warranted; do not imply broader coverage than executed.
- Bug fixes: include failure/reproduction evidence (or failing check) and post-fix verification when feasible.
- UI/browser claims require Playwright/app prerequisites satisfied; if unavailable, report **BLOCKED/UNVERIFIED**, not passed.
- Do not substitute lint/typecheck/build for required tests (or vice versa); report each result separately.

## Invalid claim patterns
- "Should pass", "looks good", "implemented", "done" without fresh evidence.
- Relying on previous runs, partial checks, or unverified subagent reports.
- Treating environment/tool failures as product passes.

## Handoff and recording
- Include verification evidence in engineer/QA/review reports.
- Update `implementation-state.md`, `feature-list.json`, `progress.md`, and QA/review artifacts when status depends on verification.
- Apply before phase handoffs, verdicts, commits/PR claims, and closeout.

## References
- Superpowers, *Verification Before Completion* (pattern inspiration): https://github.com/obra/superpowers
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Playwright Best Practices (traces/evidence): https://playwright.dev/docs/best-practices
