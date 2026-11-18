---
name: Artifact and State Discipline
description: Maintain PRD, technical artifacts, QA/review records, and implementation state with traceable, evidence-linked updates
---

# Artifact and State Discipline

Use this skill to keep work auditable, resumable, and consistent with canonical framework contracts.

## Canonical sources and ownership
- **Canonical docs/contracts:** `README.md` (workflow), `core/artifacts.md`, `core/structure.md`, `harness/engineering-harness.md`.
- **Templates:** `templates/*` (use as starting structure).
- **Ownership:** PM owns PRD handoff; TL owns canonical technical artifacts and implementation-state decisions/summaries; QA/reviewers own their reports/evidence with TL-integrated status.

## Practices
- **Single session identity:** use stable `<session-id>` across all artifacts.
- **Correct locations:** write artifacts to canonical paths under `tech-notes/<session-id>/`, `qa/<session-id>/`, `reviews/<session-id>/` (see `core/artifacts.md`).
- **Append, don't rewrite history:** record attempts, outcomes, decisions, pivots, and reversions chronologically; append superseding entries with rationale/evidence.
- **Evidence-linked updates:** every status change/claim references commands, results, or artifact paths (QA verdicts, logs, traces/screenshots).
- **Decision trail:** capture what changed, why, alternatives considered (when material), and result/impact.
- **Scope control:** note deviations/assumptions; material changes require TL note and appropriate approval.
- **Resumability:** keep `implementation-state.md`, `feature-list.json`, and `progress.md` current so a fresh context can resume safely.

## Minimum contents to maintain
- Current phase/task and overall status
- Attempt log (who/when, actions, checks, outcome, next step)
- Failures/root-cause and premise analyses for retries
- Links to QA and review evidence
- Open risks, blockers, prerequisites gaps, and exact next action

## Quality checks
- Can a new agent/session understand current state and continue without guessing?
- Are claims backed by evidence and clearly scoped (PASS/FAIL/BLOCKED/PARTIAL)?
- Are human gates/approvals and escalations recorded?

## References
- Anthropic, *Effective context engineering for AI agents*: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Framework: `core/artifacts.md`, `harness/session-lifecycle.md`
