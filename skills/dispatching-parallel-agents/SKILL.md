---
name: Dispatching Parallel Agents
description: Decompose independent work into parallel subagent tasks with clear scope, constraints, and integration checks when safe
---

# Dispatching Parallel Agents

Use when multiple tasks are independent and can proceed concurrently without unsafe shared-state coupling.

## When to parallelize
- Different files/modules/problems with minimal overlap, independent investigations, or separate review/prep tasks.
- **Do not parallelize** when tasks share mutable state/files likely to conflict, require strict ordering, or depend on each other's outputs.

## Dispatch pattern
1. **Partition by independence:** define non-overlapping scopes, ownership, and interfaces/dependencies.
2. **Create focused handoff packets (per agent):**
   - Objective and acceptance/success criteria
   - In/out-of-scope boundaries
   - Relevant artifact paths/excerpts and code locations
   - Constraints (gates, stack conventions, tools/prereqs)
   - Required output format and verification/evidence
3. **Dispatch concurrently** (if provider supports); each agent operates with fresh, self-contained context.
4. **Integrate results:** merge outputs, resolve conflicts, assess blast radius/integration risk, run required verification, and update `implementation-state.md`/trackers.

## Framework alignment
- Orchestrator (typically TL) remains accountable for sequencing, gates, and final integration.
- Preserve QA-first, evidence, and escalation rules; parallel work does not bypass phase gates.
- If parallel execution unsupported, run sequentially with same packet quality.

## References
- Anthropic, *How we built our multi-agent research system*: https://www.anthropic.com/engineering/built-multi-agent-research-system
- Anthropic, *Building effective agents* (parallelization/workflows): https://www.anthropic.com/engineering/building-effective-agents
- Superpowers, *Dispatching Parallel Agents*: https://github.com/obra/superpowers
