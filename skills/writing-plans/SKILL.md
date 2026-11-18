---
name: Writing Plans
description: Produce clear, verifiable implementation plans with phased tasks, acceptance criteria, dependencies, and evidence expectations
---

# Writing Plans

Use this skill to translate an approved PRD into an executable, reviewable plan (Technical Lead planning phase).

## Inputs
- Confirmed `<session-id>-prd.txt`, repo/branch/environment context, and relevant constraints/prerequisites.
- Existing codebase patterns, impacted areas, and any known risks.

## Plan requirements
- **Scope:** goals, in-scope/out-of-scope, assumptions, dependencies.
- **Phased breakdown:** ordered tasks/phases with owners/stacks, dependencies, and explicit acceptance/success criteria per phase.
- **Verification strategy:** QA-first hooks per phase (tests/cases defined before implementation), required local checks, and evidence expectations.
- **Contracts and design:** likely files/components impacted, interfaces/data/state/API changes, and key decisions (detail in `tech-spec.md`).
- **Risk and impact:** blast-radius concerns for risky/cross-cutting changes, migration/rollback notes, and mitigations.
- **Execution policy:** retry rules (root-cause and premise checks), **max 3 failed integration/QA attempts per phase** before human escalation, and mandatory human gates.
- **Frontend/UI phases:** require stable `data-testid` for QA-critical interactions and note Playwright prerequisites.

## Outputs (TL-owned, `tech-notes/<session-id>/`)
- `implementation-plan.md`
- `state-machine.md`
- `tech-spec.md`
- `implementation-state.md` (initialized)
- `feature-list.json` and `progress.md` for session continuity (per lifecycle)

Use `templates/` and comply with `core/artifacts.md`, `harness/engineering-harness.md`, and `README.md` workflow.

## Quality bar
- A fresh-context engineer/QA agent can execute the next phase without guessing critical decisions.
- Criteria are testable/verifiable and mapped to evidence.
- Plan is minimal and incremental (avoid speculative scope).

## References
- Anthropic, *Building effective agents* (workflows, checkpoints, simplicity): https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Superpowers, *Writing Plans* (task decomposition pattern): https://github.com/obra/superpowers
