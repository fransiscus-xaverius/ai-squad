---
name: Technical Writing
description: Produce clear, structured, evidence-aware technical artifacts and reports for framework workflow (PRD, plans, specs, QA, reviews)
---

# Technical Writing

Use when creating or updating artifacts/reports that humans and agents rely on for decisions and execution.

## Principles
- **Clarity and structure:** one purpose per section; use headings/lists/tables for scanability.
- **Concrete and testable:** express requirements, acceptance criteria, assumptions, and constraints in verifiable terms.
- **Evidence-linked:** cite commands, outputs, logs, screenshots/traces, and artifact/file paths. Distinguish observed facts from hypotheses and unknowns.
- **Decision traceability:** record what changed, why, alternatives/tradeoffs (when material), and approvals/gates.
- **Audience-aware brevity:** provide what the next reader needs to act (fresh-context agent or human reviewer).

## Artifact-specific guidance
- **PRD (`<session-id>-prd.txt`):** problem/goals/non-goals, scope, acceptance criteria, constraints/dependencies, confirmed repo/branch/env/prereqs, assumptions/open questions.
- **Tech notes (`tech-notes/<session-id>/`):** phased verifiable plan, state transitions, technical design/contracts, and live implementation state with attempt/decision trail and evidence links.
- **QA (`qa/<session-id>/`):** prerequisites/env, cases mapped to criteria, steps, expected vs actual, verdict (PASS/FAIL/BLOCKED), product-vs-environment assessment, evidence paths.
- **Reviews (`reviews/<session-id>/`):** finding/claim, location, evidence, impact/risk, validation status, adjudication/action and priority.
- **Handoffs/progress:** objective, scope, constraints, current status, blockers/gaps, and exact next action.

## Quality checks
- Can a fresh-context reader execute the next step without guessing?
- Are claims supported by evidence or explicitly marked unverified/unknown?
- Are gates, blockers, and required decisions explicit?
- Are paths/IDs (`<session-id>`, artifact locations) consistent?

## References
- Anthropic prompt engineering overview (clarity, structure): https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview
- Anthropic, *Writing effective tools for agents* (clear descriptions/contracts): https://www.anthropic.com/engineering/writing-tools-for-agents
- Framework: `core/artifacts.md`, `templates/*`, `README.md`, `harness/engineering-harness.md`
