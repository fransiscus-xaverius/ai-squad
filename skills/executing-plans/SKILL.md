---
name: Executing Plans
description: Execute an approved implementation plan in-session task by task when subagent-per-task execution is unavailable or not chosen, preserving gates and evidence
---

# Executing Plans

Use when an approved plan exists and execution happens inline in the current session (no per-task implementer/reviewer subagents), while preserving all framework gates.

## Core principles
- **Plan/spec as source of truth:** follow approved artifacts; do not make hidden deviations.
- **Small verifiable steps:** execute task/phase slices with clear acceptance criteria and evidence.
- **Resumable progress:** maintain task tracking and update `implementation-state.md`, `feature-list.json`, and `progress.md`.
- **Evidence before claims:** apply `verification-before-completion` for every completion/fix.

## Process
1. **Setup:** confirm approved PRD/plan/spec/state, session `<session-id>`, workspace/branch, prerequisites, and create a checklist aligned to phases/tasks.
2. **Execute per task/step:**
   - Understand scope/criteria and relevant context (JIT retrieval).
   - Apply `test-driven-development`/`targeted-tdd` as appropriate; implement minimally.
   - Run required local checks and capture fresh evidence.
3. **Handle mismatches:**
   - Code/behavior issue -> debug systematically (`systematic-debugging`, `fix-root-causes`).
   - Plan/spec ambiguity or material conflict -> record and escalate per gates (do not guess material decisions).
4. **Phase gates:** follow QA-first per phase, QA verdicts, and optional review adjudication per workflow.
5. **Record continuously:** after each attempt/task/phase, update artifacts with actions, evidence, results, decisions, blockers, and exact next action.
6. **Closeout:** complete required QA/review gates and finalize artifacts/evidence.

## Guardrails
- Honor `autonomy-with-gates` (pause only for mandatory/material/irreversible decisions).
- Retry discipline: root-cause/premise analysis before retries; **max 3 failed integration/QA attempts per phase -> escalate**.
- Do not skip tests, QA, evidence, or state updates.

## References
- Superpowers, *Executing Plans*: https://github.com/obra/superpowers
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Framework: `README.md`, `harness/engineering-harness.md`, `harness/session-lifecycle.md`
