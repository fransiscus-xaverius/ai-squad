# Context Engineering (Canonical)

Guidance for keeping agent context high-signal, resumable, and token-efficient across roles, phases, and sessions (aligned with Anthropic context engineering guidance).

## Principles

- **Treat context as finite:** every token competes for attention. Curate the smallest, highest-signal set for the current task/gate.
- **Just-in-time retrieval:** prefer targeted reads/searches and identifiers (file paths, symbols, artifact sections) over preloading large docs/logs/transcripts.
- **Progressive disclosure:** start from stable, high-level context and drill into details as needed.
  1. `README.md` (Main workflow) + `harness/engineering-harness.md` + `core/artifacts.md`
  2. Session PRD and relevant `tech-notes/<session-id>/` artifacts (`implementation-plan`, `state-machine`, `tech-spec`, `implementation-state`, `progress`, `feature-list`)
  3. Relevant role/stack skills and templates for the active task
  4. Targeted source files, test outputs, and `qa/<session-id>/` / `reviews/<session-id>/` evidence
- **Structured, file-based memory:** persist decisions, attempts, evidence, blockers, and next actions in artifacts (not chat memory). Artifacts are the recovery and handoff substrate.
- **Condensed handoffs:** subagent/role handoffs must be self-contained but concise (objective, scope, constraints, artifact paths, success criteria, prior relevant state/evidence, required output). Avoid passing full transcripts.
- **Compaction/checkpoints:** before context pressure, reset, or session end, write a checkpoint: current phase/feature, key decisions/rationale, evidence paths, blockers/gaps, and exact next action. Link raw logs/evidence rather than duplicating them.

## Handoff packet minimum
- Objective and acceptance/success criteria
- In-scope / out-of-scope boundaries
- Artifact paths and relevant excerpts/IDs
- Constraints (gates, tools/prereqs, stack conventions, Playwright/UI notes if applicable)
- Prior attempts, root-cause/premise analysis (if retry), and what differs now
- Required output format and verification/evidence expectations

## Role-specific loading hints
- **PM:** request/context, existing repo docs, PRD template, intake gates.
- **TL:** PRD, tech-notes, harness/workflow, planning/architecture/blast-radius skills, current state/progress.
- **Engineer:** assigned phase spec/plan excerpts, relevant stack skill, touched code/tests, prior failure evidence.
- **QA:** acceptance criteria, test plan/cases, app run/env/prereqs, Playwright guidance, prior verdicts/evidence.
- **Reviewers:** scoped diff/files, spec/intent, prior findings, verification evidence.

## References
- Anthropic, *Effective context engineering for AI agents*: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
