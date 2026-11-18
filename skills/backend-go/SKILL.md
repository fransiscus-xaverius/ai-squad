---
name: Backend Go Stack
description: Go backend implementation skill for services, APIs, CLIs, and workers with idiomatic design, reliability, testing, and framework-aligned verification/evidence
---

# Backend Go Stack

Use for `backend-go` implementation and review tasks (Go modules/services/APIs/CLIs/workers/packages).

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and relevant core skills (`phase-execution`, `blast-radius`, `systematic-debugging`, `fix-root-causes`, `attack-the-premise`, `verification-before-completion`, `artifact-state`).
- Work only in assigned phase scope; escalate material ambiguity/scope/risk decisions.

## Project structure and idioms
- Follow existing module/package layout and conventions (`cmd/`, `internal/`, package boundaries, generated code patterns). Keep package APIs cohesive.
- Use `gofmt`/`goimports`-consistent formatting and idiomatic naming (MixedCaps, clear package names, doc comments for exported identifiers where appropriate).
- Prefer small interfaces at boundaries; accept interfaces where used and return concrete types when practical. Avoid unnecessary abstraction.
- Keep zero values useful where feasible; initialize explicitly when required.

## Errors and API behavior
- Handle errors explicitly; return errors as normal values with useful context.
- Wrap errors when adding context while preserving causes (`%w`) when callers may inspect; use sentinel/typed errors consistently with repo style.
- Do not use panic for expected/control-flow errors. Keep error strings clear and non-leaky at external boundaries.
- Preserve contracts (HTTP/gRPC/CLI behavior, status/codes, wire formats, persistence semantics) unless approved spec requires change.

## Context, cancellation, and concurrency
- Pass `context.Context` through request/operation paths per conventions; respect cancellation, deadlines, and timeouts.
- Do not start goroutines without clear ownership/lifecycle and stop conditions; avoid leaks, data races, and unbounded concurrency.
- Choose appropriate synchronization (channels, mutexes, atomics) for the problem; keep critical sections small.
- Use timeouts/retries/backoff/idempotency for outbound operations when in scope and consistent with existing patterns.
- Preserve graceful shutdown and resource cleanup behavior.

## Data, config, and security
- Follow existing DB/transaction/migration/query patterns; keep transactions scoped and explicit.
- Validate/configure required runtime dependencies and inputs at boundaries/startup as appropriate.
- Enforce authn/authz and input safety at correct boundaries; protect secrets and avoid sensitive logging.
- Apply `secure-backend-engineering` (endpoint hardening, status codes, headers/CORS), `api-security-review` (OWASP API Top 10 verification pass), `auth-authorization` (identity/permission decisions), `input-validation-sanitization` (boundary validation), and `websocket-security` (real-time channels) when those surfaces are in scope.
- For data-access or hot-path work, apply `backend-performance` (N+1 avoidance, indexes, pagination caps, pool sizing, goroutine bounds) and report measured before/after evidence.

## Observability and diagnostics
- Use structured logging and correlation/trace/request identifiers consistent with project conventions.
- Follow existing metrics/tracing/health/readiness patterns when modifying instrumented paths.
- Keep diagnostics actionable and low-noise.

## Testing and verification
- Run relevant checks: `go test` (targeted packages or `./...` as appropriate), `go build`, `go vet`, static analysis/lint/codegen checks per repo tooling.
- Prefer table-driven tests for logic/edge cases; add/update tests for changed behavior and regressions. Use fakes/stubs at boundaries consistent with repo practice.
- For concurrency-sensitive changes, run race-sensitive checks when feasible (`go test -race` for relevant packages) and report coverage/limitations.
- If checks cannot run (tooling/deps/env), do not claim pass; report commands attempted, blocker, and impact.

## Debugging and handoff
- Reproduce minimally; isolate handler/service/repository/integration boundary. Inspect errors, context cancellation, data/state transitions, and concurrency ordering.
- Handoff should include: files/packages changed, contract impact, commands/checks with results, endpoints/CLI/config/env/migrations touched, local run/verify steps, QA notes, and known limitations.

## References
- Effective Go: https://go.dev/doc/effective_go
- How to Write Go Code / Modules: https://go.dev/doc/code
- Go Code Review Comments: https://go.dev/wiki/CodeReviewComments
- Go Concurrency Patterns: Context (blog): https://go.dev/blog/context
- Error handling and Go / error wrapping: https://go.dev/blog/error-handling-and-go
- Table-driven tests: https://go.dev/wiki/TableDrivenTests
- Data Race Detector: https://go.dev/doc/articles/race_detector
- testing package: https://pkg.go.dev/testing
