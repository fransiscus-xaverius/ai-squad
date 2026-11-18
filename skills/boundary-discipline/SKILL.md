---
name: Boundary Discipline
description: Validate and parse at system boundaries, trust internal typed code, and keep business logic separate from transport/framework concerns
---

# Boundary Discipline

Use when designing or changing interfaces, adapters, validation, error handling, or module boundaries.

## Principles
- **Validate at boundaries:** treat external inputs as untrusted (CLI, env/config, HTTP/RPC, files, DB/external APIs, queues/jobs, user/UI input). Parse/validate and normalize into trusted domain types at entry points.
- **Trust inside the boundary:** once data is validated/typed, avoid redundant deep re-validation; rely on invariants and types.
- **Keep adapters thin:** separate transport/framework/IO concerns from domain/business logic where practical to improve testability and clarity.
- **Expose domain concepts:** avoid leaking transport/wire/storage/framework-specific shapes across boundaries unless intentionally part of the contract.
- **Clear error mapping:** translate internal failures to safe, actionable boundary responses/errors without leaking secrets or internals.
- **Idempotence/retry awareness (when applicable):** define behavior for duplicates/retries/timeouts/crashes at boundaries.

## Checklist
- Where is the trust boundary and what invariants are enforced there?
- Are internal APIs operating on trusted types?
- Are errors/logs safe, contextual, and non-leaky at boundaries?
- Are contracts/invariants documented when non-obvious (and reflected in tests/spec)?

## Framework alignment
- Supports `architect`, stack skills, `typescript-best-practices`, `blast-radius`, and `fix-root-causes`.
- Record material boundary/contract decisions and compatibility impacts in `tech-spec.md` / `implementation-state.md`.
- Validate behavior with evidence (`verification-before-completion`).

## References
- pstack, *principle-boundary-discipline* (adapted): https://github.com/cursor/plugins
- OWASP Node.js Security Cheat Sheet (input/validation/boundary concerns): https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html
- Go Code Review Comments / Effective Go (API/error boundaries): https://go.dev/wiki/CodeReviewComments
- TypeScript Handbook (narrowing/unknown at boundaries): https://www.typescriptlang.org/docs/handbook/2/narrowing.html
