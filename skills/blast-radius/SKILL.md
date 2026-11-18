---
name: Blast Radius
description: Identify what a change could break outside the diff and prove the key safety fact with runnable evidence before shipping
---

# Blast Radius

Answer: **"What could this break beyond the diff, and how do we know it's safe?"** Direct callers are only the start; focus on non-obvious breakage.

## When to use
- **TL:** planning/impact for non-trivial phases, contract/API/schema changes, migrations, refactors, dependency/config changes.
- **Engineer:** before risky edits and before handoff/claiming completion.
- **Reviewers (hunter/skeptic/referee):** assessing regression/contract risk or disputed safety claims.
- **QA:** targeting regression checks.

State explicitly when scope is low-risk/local.

## Prove the safety fact (evidence ladder)
Identify the load-bearing fact(s) that make the change safe and get to the strongest feasible proof:
1. **Said** (weak) — claim only
2. **Cited** — concrete `file:line`, spec, or authoritative source behavior
3. **Reasoned** — traced why failure case cannot occur
4. **Run** — executed test/script/command against real code showing expected behavior (preferred when cheap)
5. **Observed in runtime** — verified in running app/environment

If not proven, mark **unproven** and specify the exact check needed.

## Procedure
1. **Understand change:** explicit diff + implicit effects (contracts, data shape/persistence, timing/lifecycle, config/flags, compatibility).
2. **State safety fact(s):** assumptions/invariants required for safety.
3. **Search beyond grep:** indirect consumers, downstream chains, interfaces/wire/serialization, stored data, cross-process/language readers, concurrency/ordering, and dependency/version behavior. If a search finds nothing, report query/scope.
4. **Assess impact:** for each risk — what breaks, where (evidence), likelihood, impact, detection/repro. Separate **confirmed risks**, **cleared checks**, and **unknowns/unproven**.
5. **Run cheapest real check when feasible:** capture command/output/result and residual gaps.
6. **Record:** include in handoff/review/state artifacts and plan targeted QA/regression coverage.

## Output format
- **Change summary** (incl. implicit effects)
- **Safety fact(s):** statement, proof level, evidence
- **Risks:** issue, location/evidence, likelihood, impact, detection
- **Cleared checks:** what was checked and why safe
- **Unproven/next checks:** gaps and required actions

## References
- pstack, *blast-radius* (safety-fact/proof concept, adapted): https://github.com/cursor/plugins
- Anthropic, *Effective harnesses for long-running agents* (verification/evidence): https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Framework: `phase-execution`, `review-adjudication`, `artifact-state`
