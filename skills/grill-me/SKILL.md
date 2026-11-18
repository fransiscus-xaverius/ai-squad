---
name: Grill Me
description: Clarify vague software requests by interrogating goals, scope, constraints, environment, and acceptance criteria before planning or implementation
---

# Grill Me (Requirements Clarification)

Use this skill when a request is ambiguous, underspecified, or risky to implement without clarification.

## Objective
Convert a vague request into a testable, scoped brief/PRD input with explicit assumptions and confirmed constraints.

## What to clarify (ask focused questions, one at a time when interactive)
- **Goal and outcome:** problem to solve, user/value impact, success definition.
- **Scope:** in-scope vs out-of-scope, priority must-haves vs nice-to-haves.
- **Acceptance criteria:** observable/testable conditions for done.
- **Constraints:** tech stack, compatibility, performance/security/compliance, timeline/risk tolerance.
- **Context:** repo/directory, existing behavior, dependencies/integrations, data/migrations.
- **Execution context (mandatory before PRD handoff):** base branch, working branch/worktree, environment/prerequisites, and Playwright readiness for UI QA flows.
- **Open choices:** options/tradeoffs requiring user decision (do not guess material decisions).

## Operating rules
- Prefer the minimum questions needed to remove blocking ambiguity; avoid unnecessary interrogation.
- State assumptions explicitly when proceeding on reversible details (`autonomy-with-gates`).
- Do not start implementation/planning changes before required intake confirmations are captured.
- Record clarified requirements, assumptions, and open questions in `<session-id>-prd.txt`.

## Output
A clear, handoff-ready summary: problem/goals, scope/non-goals, acceptance criteria, constraints/dependencies, confirmed repo/branch/env context, assumptions, and unresolved decisions.

## References
- Anthropic prompt engineering overview (clarity/success criteria): https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview
- Anthropic, *Building effective agents* (clear tasks and checkpoints): https://www.anthropic.com/engineering/building-effective-agents
- Framework: `agents/orchestrator-pm.md`, `core/artifacts.md`
