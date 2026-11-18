---
name: Receiving Code Review
description: Handle review feedback with technical verification and evidence before implementing changes, especially when feedback is unclear or questionable
---

# Receiving Code Review

## Core rule
**Verify before implementing. Ask before assuming. Technical correctness and evidence over performative agreement.**

## Workflow
1. **Read and inventory:** capture all feedback items, scope, and referenced evidence (`reviews/<session-id>/...`, code locations).
2. **Understand:** restate each actionable item; flag unclear items.
3. **Verify against reality:** inspect code/tests/specs/behavior and approved artifacts for each item.
4. **Evaluate:** determine correctness, relevance to scope/acceptance criteria, risks, and conflicts with approved decisions.
5. **Respond technically:** report confirmed issues, incorrect items (with evidence), and questions/unknowns.
6. **Implement deliberately:** address blocking/correctness issues first; apply fixes in small verifiable steps and verify each.

## Handling unclear or questionable feedback
- If any item is unclear or materially ambiguous, request clarification before implementing that item (do not guess).
- Push back with evidence when feedback is incorrect, out of scope, conflicts with approved spec/decisions, or would introduce regressions.
- Propose alternatives when appropriate, with tradeoffs and verification plan.

## Framework alignment
- Integrates with `review-adjudication` (hunter/skeptic/referee), `fix-root-causes`, and `verification-before-completion`.
- Record significant decisions, accepted/rejected feedback, and unresolved items in `implementation-state.md` and relevant artifacts.
- Respect retry/escalation rules; on repeated failures, include root-cause/premise analysis.

## References
- Superpowers, *Receiving Code Review*: https://github.com/obra/superpowers
- Anthropic, *Building effective agents* (grounded evaluation): https://www.anthropic.com/engineering/building-effective-agents
- Framework: `harness/engineering-harness.md`
