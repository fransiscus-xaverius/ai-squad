---
name: TypeScript Best Practices
description: TypeScript correctness and modeling best practices for .ts/.tsx work in this framework (type discipline, boundary validation, narrowing, safe refactors, and testable changes)
---

# TypeScript Best Practices

Use for TypeScript/TSX in `backend-node` or `frontend-node` work. Apply within assigned phase scope and repository conventions.

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and `ponytail` (smallest complete, verifiable change).
- **Engineers:** keep types/contracts consistent with spec, run relevant local checks (typecheck/lint/tests/build), and report evidence plus type-related risks/assumptions.
- **Reviewers:** treat unsafe casts, incomplete guards, unvalidated boundaries, and unhandled variants as potential defect sources; require evidence for tradeoffs.
- Record non-trivial type/contract decisions and deviations in `implementation-state.md` as needed (`artifact-state`).

## Type modeling and correctness
- **Make illegal states unrepresentable (where practical):** prefer discriminated unions and precise domain types over loosely-typed bags of optionals.
- **Use `unknown` at trust boundaries:** parse/narrow external/untyped data before use; avoid `any` except narrowly-scoped, justified interop boundaries.
- **Narrow safely:** prefer control-flow narrowing, discriminants, `in` checks, `typeof`/`instanceof`, and well-tested type guards/predicates. Ensure user-defined guards are truthful and complete.
- **Exhaustiveness:** handle unions exhaustively (e.g. `never` checks/switch exhaustiveness) so new variants surface at compile time.
- **Avoid unchecked assertions:** `as` casts should follow validation/narrowing or be isolated with justification; never use casts to silence real uncertainty at boundaries.
- **Preserve useful inference:** prefer `satisfies` (when available/appropriate) to validate shapes without widening; leverage inference and avoid redundant annotations that hide mismatches.
- **Reuse types/schemas:** derive types from source-of-truth schemas and utility types (`Pick`, `Omit`, `Partial`, `ReturnType`, `Parameters`, `Awaited`, `typeof`, generics) before duplicating models.

## Boundaries and runtime validation
- Validate/parse at system boundaries (HTTP/API payloads, env/config, CLI args, file/queue/external data, UI input as applicable) and convert to trusted domain types.
- Prefer project-standard schema/validation libraries/patterns when present; keep runtime validation aligned with compile-time types.
- Do not let unvalidated external shapes propagate into core/domain logic.

## APIs, modules, and maintainability
- Keep public interfaces explicit and stable within scope; avoid breaking exported contracts unless approved.
- Prefer clear, composable functions/types over overly complex generic abstractions.
- Keep error/result handling explicit and consistent with project patterns.
- Follow existing module/import conventions and tsconfig/project constraints.

## Testing and verification
- Test behavior and contracts (including edge/error cases) rather than implementation details.
- Keep tests deterministic; add/update tests for changed behavior where practical.
- Run relevant checks with evidence (typecheck, lint, tests, build) and report results/scope.
- For fixes, pair with `test-driven-development`/`targeted-tdd` and `verification-before-completion` as applicable.

## Common pitfalls to avoid
- Widening to `any`/overly-broad types to "make it compile"
- Non-exhaustive unions/switches
- Lying type guards or assertions without runtime validation
- Duplicated, drifting type definitions across layers

## References
- TypeScript Handbook, *Everyday Types*: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
- TypeScript Handbook, *Narrowing*: https://www.typescriptlang.org/docs/handbook/2/narrowing.html
- TypeScript Handbook, *Generics / Type Manipulation / Modules*: https://www.typescriptlang.org/docs/handbook/
- OWASP Node.js Security Cheat Sheet (boundary/validation context): https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html
- Framework: `boundary-discipline`, `backend-node`, `frontend-node`
