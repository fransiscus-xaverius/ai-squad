---
name: Brainstorming
description: Clarify intent and design options before planning or implementation for creative, ambiguous, or high-impact work
---

# Brainstorming (Intent & Design Clarification)

Use before planning/implementation when the request is open-ended, creative, or involves meaningful design/approach choices.

## Process
1. **Understand context:** review request, relevant codebase/artifacts, constraints, and prior decisions.
2. **Clarify intent:** goal/why, users and outcomes, scope/non-goals, constraints, and success/acceptance signals.
3. **Explore options:** propose a small set of viable approaches with tradeoffs (complexity, risk, blast radius, testability, time) and a recommended default when appropriate.
4. **Confirm direction:** capture chosen approach, assumptions, and open questions.
5. **Handoff:** produce PRD-quality requirements summary and proceed to TL planning artifacts and required approval gates.

## Guidelines
- Keep exploration grounded in repository/framework constraints and acceptance criteria.
- Ask focused questions for material unknowns; proceed autonomously only on reversible details with recorded assumptions (`autonomy-with-gates`).
- Do not replace mandatory intake confirmations (repo/directory, base/working branch, environment/prerequisites).

## Output
- Agreed direction and rationale
- Key tradeoffs and rejected alternatives (briefly, when relevant)
- Assumptions/open questions and next gated step

## References
- Anthropic prompt engineering overview: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
- Superpowers, *Brainstorming* (intent/design clarification pattern): https://github.com/obra/superpowers
