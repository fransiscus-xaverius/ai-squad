---
name: Backend Node Stack
description: Node.js/TypeScript backend implementation skill for APIs, services, workers, and data access with framework-aligned verification, evidence, and QA handoff
---

# Backend Node Stack

Use for `backend-node` implementation and review tasks (Node.js/TypeScript or JavaScript APIs, services, workers, CLIs, integrations, data access).

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and relevant core skills (`phase-execution`, `blast-radius`, `systematic-debugging`, `fix-root-causes`, `attack-the-premise`, `verification-before-completion`, `artifact-state`).
- Work only in assigned phase scope; escalate material ambiguity/scope/risk decisions.
- Apply `typescript-best-practices` and `boundary-discipline` for TypeScript code.

## Runtime and async/concurrency (Node.js)
- Node.js executes JavaScript on the event loop with non-blocking I/O; avoid blocking the event loop in request/worker paths.
- Prefer async/non-blocking APIs; do not mix blocking sync I/O with hot async paths.
- Offload CPU-intensive work appropriately (worker threads/jobs/queues) when in scope and consistent with project design.
- Handle async errors explicitly (await/promises/callback contracts per codebase); avoid unhandled rejections and swallowed failures.
- Be mindful of concurrency/race conditions in shared state, caches, and multi-step workflows.

## Architecture and boundaries
- Follow existing framework and project conventions (Express/Fastify/Nest/Hono/custom), module boundaries, and layering (transport -> application/service -> data/integration) where present.
- Keep business/domain logic separate from transport/framework/IO concerns; reuse existing middleware, error types, config, and observability patterns (`ponytail`).
- Parse/validate inputs and normalize to trusted types at boundaries (HTTP params/query/body/headers, webhooks, queue/job payloads, files, env/config).

## API contracts and compatibility
- Preserve contracts, status/error semantics, auth behavior, and data shapes unless approved spec requires change.
- Return consistent, safe error responses; do not leak secrets, stack traces, or internal details in production-facing paths.
- Consider pagination/filtering/sorting, idempotency, backward compatibility, and migration impacts when relevant.

## Security and data handling (OWASP-aligned)
- Treat all external input as untrusted; validate types/ranges/formats and enforce size/rate limits as applicable.
- Enforce authentication/authorization at correct boundaries; never trust client-controlled identity/roles/IDs without verification.
- Use parameterized/safe data-access patterns; prevent injection and unsafe deserialization.
- Protect secrets/credentials/tokens; never log sensitive data/PII beyond policy.
- Use secure defaults for cookies/headers/CORS/CSRF as appropriate to app architecture and existing patterns.
- Apply `secure-backend-engineering` (endpoint hardening, status codes, headers/CORS), `api-security-review` (OWASP API Top 10 verification pass), `auth-authorization` (identity/permission decisions), `input-validation-sanitization` (boundary validation), and `websocket-security` (real-time channels) when those surfaces are in scope.

## Reliability, resources, and operations
- Use timeouts/cancellation/abort signals for outbound calls where supported; apply bounded retries/backoff only per existing patterns.
- Manage resources safely (DB connections/transactions, streams, queues, caches, file handles); ensure cleanup on success/failure.
- Keep transactions scoped and explicit; handle partial failure and rollback semantics per design.
- Use structured logging and correlation/request IDs consistent with project observability; include actionable context.
- For data-access or hot-path work, apply `backend-performance` (N+1 avoidance, indexes, pagination caps, pooling, event-loop safety) and report measured before/after evidence.

## Configuration and dependencies
- Validate required configuration/env at startup or boundary per project pattern; fail fast with clear errors when safe.
- Follow existing dependency and lockfile practices; avoid unnecessary additions.
- Document runtime prerequisites, env vars, migrations, and operational notes in handoff/state when relevant.

## Testing and verification
- Run smallest relevant checks first, then broader as warranted: typecheck, lint, unit/integration tests, build/start smoke checks (per repo tooling).
- Add/update tests for changed behavior, edge cases, and error paths as appropriate.
- For retries, report failing evidence, root cause, fix rationale, and rerun evidence.
- If checks cannot run (services/deps/env), do not claim pass; report blocker, commands attempted, and impact.

## Debugging and handoff
- Reproduce minimally; trace boundary -> service -> data/external dependency.
- Distinguish product defects from environment/config/test-harness issues.
- Handoff should include: files changed, contract/behavior impact, commands/checks with results, endpoints/jobs/config/env/migrations touched, local run/verify steps, QA notes, and known limitations.

## References
- Node.js Learn, *Overview of Blocking vs Non-Blocking*: https://nodejs.org/en/learn/asynchronous-work/overview-of-blocking-vs-non-blocking
- Node.js Learn (async/event loop/diagnostics): https://nodejs.org/en/learn
- OWASP Node.js Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html
- Express Production Best Practices (Security/Performance): https://expressjs.com/en/advanced/best-practice-security.html
- Node.js Best Practices (community reference): https://github.com/goldbergyoni/nodebestpractices
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/
