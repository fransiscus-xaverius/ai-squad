# State Machine — <SESSION_ID>

## Overview
Describe end-to-end flow as states and transitions for intake, planning, phased execution, QA, review, and escalation.

## States
- `INTAKE`
- `PRD_READY`
- `PLANNING`
- `PLAN_REVIEW` (human gate)
- `PHASE_TEST_DESIGN` (QA-first)
- `PHASE_IMPLEMENTATION`
- `PHASE_QA`
- `PHASE_REVIEW` (optional, hunter/skeptic/referee)
- `PHASE_COMPLETE`
- `ESCALATION_HUMAN_DECISION` (mandatory pause)
- `DONE`
- `PAUSED`

## Transitions
| From | Event/Guard | To | Owner | Notes |
|---|---|---|---|---|
| INTAKE | requirements + repo/branch + env/prereqs confirmed | PRD_READY | orchestrator-pm | mandatory gate |
| PRD_READY | technical-lead spawned | PLANNING | orchestrator-pm |  |
| PLANNING | artifacts drafted (plan/spec/state-machine/state/trackers) | PLAN_REVIEW | technical-lead |  |
| PLAN_REVIEW | human approved | PHASE_TEST_DESIGN | technical-lead | mandatory gate |
| PHASE_TEST_DESIGN | QA cases adequate/approved by TL | PHASE_IMPLEMENTATION | qa-agent/technical-lead | test-first |
| PHASE_IMPLEMENTATION | local checks pass with evidence | PHASE_QA | engineer-specialist-* |  |
| PHASE_QA | verdict PASS with evidence | PHASE_COMPLETE | qa-agent/technical-lead |  |
| PHASE_QA | verdict FAIL/BLOCKED and attempts < 3 | PHASE_IMPLEMENTATION | technical-lead | root-cause/premise analysis required before retry |
| PHASE_QA | 3rd failed integration/QA attempt in phase | ESCALATION_HUMAN_DECISION | technical-lead | mandatory escalation/pause |
| PHASE_COMPLETE | review required and blocking findings accepted | PHASE_IMPLEMENTATION | technical-lead/referee | fix + re-verify |
| PHASE_COMPLETE | more phases remain | PHASE_TEST_DESIGN | technical-lead |  |
| PHASE_COMPLETE | all phases complete and gates satisfied | DONE | technical-lead |  |

## Phase/task mapping
- Phase -> states/substates:
- Owners/stack skills:
- Notes (prereqs, UI/data-testid, blast-radius concerns):
