# Framework Structure (Canonical)

Provider-agnostic agentic engineering framework with optional provider adapters. Canonical behavior lives in-repo; integrations map provider-specific wiring to these sources.

## Canonical locations

| Area | Path | Purpose |
|---|---|---|
| **Core contracts/docs** | `core/` | Shared contracts and cross-cutting guidance (`artifacts.md`, `structure.md`, `context-engineering.md`) |
| **Agents** | `agents/` | Canonical agent role prompts/specs (PM, TL, QA, engineer/hunter/skeptic/referee specialists) |
| **Skills** | `skills/` | Canonical reusable skills (`skills/<skill-id>/SKILL.md`) for workflow, quality, stack, and review practices |
| **Workflow (canonical)** | `README.md` | Main end-to-end workflow (Mermaid), inventory, prerequisites, and usage |
| **Harness** | `harness/` | Execution/review/QA rules, gates, retries/escalation, evidence standards, session lifecycle (`engineering-harness.md`, `session-lifecycle.md`) |
| **Templates** | `templates/` | Reusable templates for PRD, plan/spec/state, QA, review, tracking, progress, and handoffs |
| **Tools (conventions)** | `tools/` | Tooling expectations/integration notes (not bundled runtimes) |
| **Adapters / Integrations** | `adapters/`, `integrations/` | Provider-specific bootstrap/install and mapping docs |
| **Bootstrap** | `BOOTSTRAP.md` | Single-prompt, fetch-and-follow bootstrap for providers |
| **OpenCode adapter example** | `opencode.jsonc`, `.opencode/` | Example config and discovery paths (symlinks to canonical `agents/`, `skills/`) |

## Session/runtime outputs (generated per run)

Use a stable `<session-id>` and canonical paths per `core/artifacts.md`:
- `<session-id>-prd.txt`
- `tech-notes/<session-id>/` (plan, state-machine, tech-spec, implementation-state, feature-list, progress)
- `qa/<session-id>/` (plan/cases/results/evidence)
- `reviews/<session-id>/` (hunter/skeptic/referee outputs)

## Design intent
- Keep **behavioral definitions** (agents/skills/workflow/harness/core contracts) canonical and portable.
- Keep **provider wiring** in adapters/integrations and provider-native config locations.
- Keep **project/session outputs** separate from framework definitions.
- Prefer **evidence-backed, resumable, gated execution** with fresh-context handoffs and progressive disclosure.

## References
- Skills ecosystem/docs: https://skills.sh/docs
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
