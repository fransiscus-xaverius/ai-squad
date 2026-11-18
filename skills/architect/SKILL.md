---
name: Architect
description: Design types, interfaces, and module boundaries before implementation for non-trivial work; align contract with plan/spec and implement in verifiable increments
---

# Architect

Use for non-trivial work where upfront design reduces rework/risk (cross-cutting changes, new abstractions, domain/state modeling, API/data-contract changes).

## When to use
- **Technical Lead:** phase shaping, interface/data-model decisions, de-risking plan/spec.
- **Engineer:** implementing assigned scope against an agreed contract/shape.
- Pair with `writing-plans`, `blast-radius`, `boundary-discipline`, and `phase-execution`.

## Steps
1. **Ground in existing system**
   - Read PRD/plan/spec/state and inspect real code paths, owners, invariants, and constraints.
   - Identify compatibility requirements and intended change boundaries.
2. **Define the contract first**
   - Specify data shapes/types, interfaces, module boundaries, ownership, state/error behavior, and key invariants.
   - Prefer simple, explicit designs consistent with codebase conventions.
3. **Evaluate options when it matters**
   - For high-impact/novel decisions, compare viable options on correctness, clarity, blast radius/migration cost, testability, operability, and reversibility.
4. **Record and align**
   - Capture chosen design, rationale, tradeoffs, and compatibility/migration notes in `tech-spec.md` and/or `implementation-state.md`.
   - Respect mandatory gates (plan approval/material decisions).
5. **Implement incrementally with verification**
   - Treat design/spec as contract; surface deviations early.
   - Verify each increment with appropriate checks/evidence.
6. **Revisit on structural friction**
   - If workarounds accumulate, re-ground and redesign rather than layering patches; update artifacts.

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, and `artifact-state`.
- Do not bypass QA/review gates or human approvals.

## References
- Anthropic, *Building effective agents* (simplicity, clear interfaces): https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *Writing effective tools for agents* (clear contracts): https://www.anthropic.com/engineering/writing-tools-for-agents
- Go Effective Go / design idioms (stack-specific inspiration): https://go.dev/doc/effective_go
- Superpowers/pstack design practice (adapted): https://github.com/obra/superpowers
