# Session Lifecycle (Long-Running Harness)

Practices for reliable multi-session/multi-agent runs (initializer, continuity, clean handoff), aligned with Anthropic's long-running agent harness guidance.

## 1) Initializer / first session setup (per `<session-id>`)
- **Context & gates:** confirm repo/directory, base and working branch/worktree, environment/prerequisites (incl. Playwright for UI QA flows), and how to run/build/test/smoke-check.
- **Create session artifacts** from `templates/`:
  - `<session-id>-prd.txt`
  - `tech-notes/<session-id>/implementation-plan.md`
  - `tech-notes/<session-id>/state-machine.md`
  - `tech-notes/<session-id>/tech-spec.md`
  - `tech-notes/<session-id>/implementation-state.md`
  - `tech-notes/<session-id>/feature-list.json` (from `feature-list.template.json`)
  - `tech-notes/<session-id>/progress.md` (from `progress-log-template.md`)
  - `qa/<session-id>/` and `reviews/<session-id>/` as needed
- **Establish baseline health:** run feasible smoke/build/tests and record evidence before feature work. Broken baseline is a blocker to log, not to hide.
- **Tracking rules:** feature list is source for "what remains"; keep acceptance criteria/IDs stable, update status/evidence only with fresh verification.

## 2) Start-of-session routine (every run/resume)
1. Identify `<session-id>`, workspace/branch, and current phase/gate.
2. Read `progress.md`, `feature-list.json`, `implementation-state.md`, PRD/plan/spec excerpts as needed, and recent git history/commits (if available).
3. Re-run baseline smoke/health checks when practical; if failing, investigate/fix or record blocker before new scoped work.
4. Select one highest-priority incomplete feature/phase slice; state acceptance criteria, risks/blast radius (if relevant), and evidence required.

## 3) During session
- Work in **small, verifiable increments**; preserve gates (QA-first per phase, evidence-backed verification, review/adjudication when in scope).
- Update `implementation-state.md` with attempts, actions, checks/commands, outcomes, decisions, and evidence paths.
- Update `feature-list.json` and `progress.md` as status changes (passing only with evidence; no silent scope rewrites).
- For retries: record root cause/premise analysis and what differs; enforce max 3 failed integration/QA attempts per phase before escalation.
- Keep handoffs/checkpoints concise and artifact-linked (`core/context-engineering.md`, `templates/handoff-packet-template.md`).

## 4) End-of-session / clean handoff
- Leave a **clean, resumable state**: no undocumented half-finished changes; clearly mark done/blocked/in-progress with evidence.
- Record: what changed, checks run and results, blockers/gaps (incl. missing prerequisites like Playwright), decisions/risks, and **exact next action**.
- Update `progress.md`, `feature-list.json`, and `implementation-state.md`.
- Prefer descriptive commit/checkpoint boundaries aligned to verified increments when using git (subject to repo/human policy).

## 5) Resumption rule
Trust artifacts and repository state over memory: `progress.md`, `feature-list.json`, `implementation-state.md`, PRD/plan/spec, and git/test evidence are the recovery map. Re-verify assumptions if environment changed.

## References
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Anthropic, *Harness design for long-running application development*: https://www.anthropic.com/engineering/harness-design-long-running-apps
- Anthropic, *Effective context engineering for AI agents*: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
