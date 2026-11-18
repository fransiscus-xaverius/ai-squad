---
name: Subagent-Driven Development
description: Execute planned work by delegating tasks to focused subagents with fresh context, structured handoffs, and review/verification gates
---

# Subagent-Driven Development

Use when a plan can be executed by delegating independent or well-scoped tasks/phases to specialized subagents (provider support permitting).

## Core principles (Anthropic-aligned)
- **Fresh context per task/role:** subagents start without inherited chat history; give them exactly what they need.
- **Orchestrator retains control:** TL/PM coordinates scope, sequencing, integration, and gates.
- **Structured artifacts as interface:** plans/specs/state/QA/review artifacts are the durable contract between roles.
- **Parallelize only independent work:** avoid shared-state conflicts and tight coupling.

## Process
1. **Prepare:** ensure approved PRD/plan/spec/state and clear task/phase boundaries with acceptance criteria.
2. **Delegate with complete packets:** objective, in/out-of-scope, constraints, artifact paths/excerpts, prior attempts/root-cause context (if retry), success criteria, and required outputs/evidence format.
3. **Execute by role/phase:** engineers implement with local checks; QA validates per phase (QA-first gate); apply matching stack skills and `blast-radius` for risky changes.
4. **Integrate and verify:** collect outputs, reconcile conflicts, run/require fresh verification, and update canonical state/tracking artifacts.
5. **Handle failures:** apply `fix-root-causes`/`attack-the-premise`; enforce retry limit (max 3 failed integration/QA attempts per phase -> escalate).
6. **Review adjudication (when in scope):** run hunter -> skeptic -> referee with evidence-backed outputs.

## Fallbacks
- If subagents/parallelism unavailable, emulate roles sequentially while preserving all gates, handoff packets, and evidence.
- Keep packets concise and high-signal (`core/context-engineering.md`).

## References
- Anthropic, *How we built our multi-agent research system*: https://www.anthropic.com/engineering/built-multi-agent-research-system
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *Effective context engineering for AI agents*: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Superpowers, *Subagent-Driven Development*: https://github.com/obra/superpowers
