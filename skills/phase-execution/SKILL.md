---
name: Phase Execution Harness
description: Run phased implementation with test-first QA gates, engineer execution, evidence-based verdicts, retries, and escalation
---

# Phase Execution Harness

Use this skill to execute implementation in controlled, verifiable phases (QA-first, evidence-gated, resumable).

## Pre-conditions
- Approved PRD and TL artifacts exist in `tech-notes/<session-id>/` (plan, state machine, tech spec, implementation state; plus `feature-list.json`/`progress.md` for resumability).
- Current phase scope and acceptance criteria are clear.
- Environment/prerequisites confirmed for scope (including Playwright for UI QA flows).

## Per-phase loop
1. **QA test design/review (before implementation)**
   - QA produces/revises test plan/cases mapped to acceptance criteria.
   - TL reviews adequacy (coverage, preconditions, expected results, evidence method). Do not start implementation until adequate.
2. **Engineer implementation**
   - Engineer implements only assigned scope using relevant stack/core skills.
   - Frontend work includes/maintains stable `data-testid` for QA-critical interactions.
   - Engineer runs relevant local checks and reports fresh evidence.
3. **QA validation**
   - QA executes planned checks (Playwright/UI where applicable and prerequisites met), captures evidence, and issues verdict: **PASS / FAIL / BLOCKED**.
4. **State update**
   - TL updates `implementation-state.md`, `feature-list.json`, and `progress.md` with attempt, actions, checks, verdict, evidence links, decisions, and next step.

## Failure handling and retries
- On **FAIL/BLOCKED**, analyze root cause before retry (`systematic-debugging`, `fix-root-causes`); distinguish product vs environment/test-harness issues.
- Record why prior attempt failed and why next attempt differs (new evidence/approach).
- If repeated failures share the same gate/assumption, apply `attack-the-premise` before retry.
- **Max 3 failed integration/QA attempts per phase:** mandatory human escalation/pause with summary, evidence, hypotheses/premises tested, and options.
- Do not claim pass on partial/blocked verification.

## Human gates and autonomy
- Mandatory gates: intake context confirmation, plan approval, retry-limit escalation (and material/irreversible decisions).
- Proceed autonomously on reversible in-scope work between gates; record decisions and assumptions.

## Definition of done (phase)
- Scoped acceptance criteria satisfied with local verification evidence.
- QA verdict **PASS** with required evidence (or explicitly approved documented exception).
- Accepted blocking review findings (if in scope) resolved or explicitly deferred.
- Canonical state/tracking artifacts updated.

## References
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Anthropic, *Building effective agents* (workflows/evaluators): https://www.anthropic.com/engineering/building-effective-agents
- Framework: `harness/engineering-harness.md`, `harness/session-lifecycle.md`, `core/artifacts.md`
