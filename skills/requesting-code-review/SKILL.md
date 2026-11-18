---
name: Requesting Code Review
description: Prepare and request focused, evidence-ready code reviews with clear scope, intent, and verification context
---

# Requesting Code Review

Use when requesting hunter/peer/human review or preparing inputs for adjudication.

## Review request packet (self-contained)
- **Scope:** files/paths, diff/commit range (if applicable), phase/task, and explicit out-of-scope.
- **Intent:** what changed and why; links to PRD/plan/spec/state excerpts and acceptance criteria.
- **Risk areas:** contracts/APIs, data/migrations, concurrency/timing, security/auth, UI flows/selectors, performance-sensitive paths.
- **Blast radius:** safety fact(s), proof level/evidence, cleared checks, and unproven/residual risks for non-trivial changes.
- **Verification performed:** commands/tests/checks run, results, evidence paths (`qa/<session-id>/`, logs, traces), and known gaps/unverified areas.
- **Questions:** specific concerns or areas needing scrutiny.

## Standards
- Do not request approval on unverified claims; provide fresh evidence (`verification-before-completion`).
- Keep scope focused; split unrelated changes when possible.
- Ensure relevant artifacts are up to date (`implementation-state.md`, QA notes/verdicts, specs) so reviewers have context.

## Framework alignment
- Feeds `review-adjudication` (hunter -> skeptic -> referee) and phase gates.
- Accepted blocking findings return to fix + re-verification (QA/evidence as required).

## References
- Superpowers, *Requesting Code Review*: https://github.com/obra/superpowers
- Anthropic, *Building effective agents* (feedback/evaluation loops): https://www.anthropic.com/engineering/building-effective-agents
- Framework: `skills/review-adjudication/SKILL.md`, `core/artifacts.md`
