# Artifact Contracts (Canonical)

Canonical artifact naming, locations, ownership, and required contents. Artifacts are the durable memory and evidence trail for phased, multi-agent, resumable execution.

**See also:** `README.md` (Main workflow), `harness/engineering-harness.md`, `harness/session-lifecycle.md`, `core/context-engineering.md`, and `templates/`.

## Naming and locations

Use a stable `<session-id>` for all artifacts in a run.

| Artifact | Path | Primary owner |
|---|---|---|
| PRD | `<session-id>-prd.txt` (root or agreed location) | PM (handoff to TL) |
| Implementation plan | `tech-notes/<session-id>/implementation-plan.md` | TL |
| State machine | `tech-notes/<session-id>/state-machine.md` | TL |
| Tech spec | `tech-notes/<session-id>/tech-spec.md` | TL |
| Implementation state (canonical) | `tech-notes/<session-id>/implementation-state.md` | TL |
| Feature tracker | `tech-notes/<session-id>/feature-list.json` | TL (updated with evidence) |
| Progress log | `tech-notes/<session-id>/progress.md` | TL/active role (append-only checkpoints) |
| QA plan/cases | `qa/<session-id>/test-plan.md`, `qa/<session-id>/test-cases.md` | QA |
| QA results/evidence | `qa/<session-id>/results/<phase-or-task>.md`, `qa/<session-id>/evidence/*` | QA |
| Review outputs | `reviews/<session-id>/hunter-<stack>-<scope>.md`, `skeptic-...`, `referee-...` | Review roles |

## Required contents

### PRD (`<session-id>-prd.txt`)
- Problem statement, goals, non-goals/out of scope
- Functional requirements and acceptance criteria (testable where possible)
- Constraints, dependencies, assumptions, open questions/resolved decisions
- Confirmed context: repo/directory, base branch, working branch, environment/prerequisites (note Playwright for UI QA)

### Implementation plan (`implementation-plan.md`)
- Phased/task breakdown with ordering, dependencies, and owners/stack roles
- Acceptance/success criteria and verification method per phase
- QA-first hooks and frontend `data-testid` expectations for critical flows
- Risks, blast-radius concerns (for risky changes), rollback/mitigation notes
- Retry/escalation policy (root-cause/premise checks; max 3 failed integration/QA attempts per phase)

### State machine (`state-machine.md`)
- States, transitions, guards, failure paths
- Mapping to phases/tasks and responsible roles
- Escalation transitions (e.g. 3rd failed attempt -> human decision)

### Tech spec (`tech-spec.md`)
- Architecture/design decisions and impacted components/interfaces
- Contracts, data models, API/schema changes, migration notes (if any)
- Test/observability/deployment-runtime notes relevant to implementation
- Key design rationale and tradeoffs (esp. for non-trivial choices)

### Implementation state (`implementation-state.md`, TL-owned canonical)
- Current phase/task and overall status
- Chronological attempt log (timestamp/context, agent(s), actions, checks/commands, outcome, evidence links)
- Failures/challenges, root-cause and premise analysis for retries
- Decisions, deviations, assumptions, and human approvals (append superseding entries)
- Links to QA/review evidence and next step

### Feature tracker (`feature-list.json`)
- Machine-readable list of features/phases/slices with IDs, acceptance steps, status, evidence links, owner/notes.
- **Rule:** do not mark `passing` without fresh verification evidence; keep acceptance definitions stable (record approved scope changes explicitly).

### Progress log (`progress.md`)
- Append-only session checkpoints: actions, checks/evidence, decisions, blockers/gaps (incl. prerequisites), and exact next action.

### QA outputs
- **Test plan/cases:** scope, environment/prerequisites, setup/data, cases mapped to acceptance criteria, expected results.
- **Security/performance coverage (when the phase touches an API, auth surface, untrusted input, a real-time channel, or hot-path data access):** applicable skills, expected status codes/limits/behavior, and an explicit list of controls that could not be exercised (these stay **BLOCKED/unverified**, never passed).
- **Results/verdict:** executed steps, expected vs actual, PASS/FAIL/BLOCKED, defects, evidence paths (screenshots/traces/videos/logs), and product-vs-environment distinction when inferable.

### Review outputs
- **Hunter:** findings with severity/impact, affected locations, evidence/repro/reasoning, suggested direction.
- **Skeptic:** per-finding status (confirmed/refuted/inconclusive) with rationale/evidence.
- **Referee:** accepted/rejected/needs-more-evidence decisions with priority and required actions.
- **Security findings:** state the control expected, the enforcement point, and the regression test required; severity reflects exploitable impact.

## Evidence and traceability rules
- Link evidence to claims (commands, outputs, test runs, artifact paths); prefer reproducible steps.
- Record environment/tool/prerequisite gaps explicitly (e.g. Playwright unavailable => UI automation blocked/unverified).
- Record security controls that could not be exercised as unverified gaps, not as satisfied requirements.
- Maintain decision trail and attempt history; never silently rewrite history or acceptance criteria.

## References
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Anthropic, *Effective context engineering for AI agents*: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
