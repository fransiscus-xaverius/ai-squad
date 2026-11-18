---
name: Backend Performance
description: Diagnose and fix backend performance problems (N+1 queries, missing indexes, unbounded results, blocking work, connection/resource limits) with measured evidence
---

# Backend Performance

Use for backend/API/service performance work: slow endpoints, high query counts, latency or throughput regressions, resource exhaustion, or review of a risky change to hot paths. Pair with `benchmark-checklist` for measurement discipline and `blast-radius` for change impact.

## Framework alignment
- Follow `harness/engineering-harness.md`, `core/artifacts.md`, and `verification-before-completion`.
- Performance work is only valid with **evidence**: before/after measurement under a stated load shape, environment, and method. Without it, report as an unproven hypothesis.
- Keep optimizations inside assigned scope; propose larger changes (schema, architecture, capacity) to the TL with data.

## Diagnose before changing
1. **Establish the load shape:** read/write ratio, request rate, payload sizes, concurrency, dataset size, and which flows matter to the user. Optimizing the wrong flow is wasted work.
2. **Measure the baseline:** record the metric (latency percentiles, query count, throughput, CPU/memory, DB time) with the command/tool and environment.
3. **Find the dominant cost:** query count and time, serialization, lock contention, I/O wait, event-loop blocking, GC pressure, or downstream latency.
4. **Change one factor at a time** and re-measure the same way (`benchmark-checklist`).

## Common defects and fixes

### N+1 and query amplification
- **Symptom:** one request issues a query per item in a list/loop (ORM lazy loading, per-row lookups, per-item permission checks).
- **Fixes:** eager-load/join the needed relations; batch-fetch by key set (`WHERE id IN (...)`) and map results in memory; use a dataloader-style batching layer; project only the columns needed; move per-item checks into a single scoped query.
- **Verify:** compare query counts per request before/after (query log/counter) — the count should be roughly constant, not proportional to result size.
- **Careful:** eager loading everything can overload memory; load exactly what the response needs.

### Indexing and query shape
- Add indexes matching actual filter, join, and sort columns (composite index column order matters: equality filters then range/sort).
- Remove redundant indexes on write-heavy tables; each index costs write throughput and storage.
- Avoid `SELECT *`; select needed columns so indexes and row format are used efficiently.
- Watch for implicit conversions, functions applied to filtered columns, and non-sargable predicates that prevent index usage.
- Verify with the database's query plan/explain output as evidence.

### Unbounded work
- **Pagination with caps:** default and maximum page size; cursor or keyset pagination for deep pages; stable sort keys to avoid duplicates/skips.
- Cap request body size, upload size, batch sizes, expansion/nesting depth, and concurrent work per request.
- Enforce limits server-side even if clients are expected to comply.

### Caching
- Cache only when reads dominate and the value is safe to be stale within the accepted window.
- Define invalidation/TTL explicitly; never cache per-user or permission-sensitive responses under a shared key.
- Avoid caching failures or mutable objects returned by reference.
- Measure hit ratio and end-to-end effect; caching without measurement is a guess.

### Resource management and concurrency
- Size connection pools deliberately (pool size vs database limits vs concurrency) and set acquisition/query timeouts.
- Apply timeouts and cancellation to every outbound call; bound retries with backoff and jitter.
- **Node.js:** never block the event loop in request/worker paths — avoid synchronous file/DB/crypto calls and unbounded CPU work; offload heavy computation to workers/queues.
- **Go:** avoid unbounded goroutine creation; bound concurrency with semaphores; respect `context.Context` deadlines and cancellation.
- Apply backpressure when producers can outrun consumers (queues, sockets, streams) — bounded buffers with an explicit overflow policy.

### Caching headers vs application caches
- If responses are sensitive, set `Cache-Control: no-store` and keep them out of application-managed caches (`secure-backend-engineering`).

## Verification and evidence
- **Evidence to produce:** baseline vs after metrics, environment/load description, commands/tooling used, and the query/plan or profile output that supports the diagnosis.
- Keep measurements comparable (same dataset, same machine class, same concurrency, warm/cold state stated).
- Guard the change with a **regression check** (query-count assertion, latency budget test, or load script) so the improvement does not silently revert (`correct`).
- If the environment cannot support a trustworthy measurement, say so and provide the closest executable evidence (e.g. query counts in tests, EXPLAIN output) instead of claiming a speedup.

## Handoff content
- Problem statement + load shape, baseline metrics, root cause, change made, after metrics, residual risk (e.g. cache staleness, memory growth, index write cost), and follow-ups not done due to scope.

## References
- OWASP REST Security Cheat Sheet (resource limits / status codes): https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html
- OWASP Denial of Service Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Denial_of_Service_Cheat_Sheet.html
- Node.js Learn, *Overview of Blocking vs Non-Blocking*: https://nodejs.org/en/learn/asynchronous-work/overview-of-blocking-vs-non-blocking
- Effective Go (concurrency, performance): https://go.dev/doc/effective_go
- Go blog, *Context* (cancellation/timeout propagation): https://go.dev/blog/context
- PostgreSQL docs, *EXPLAIN*: https://www.postgresql.org/docs/current/sql-explain.html
- Framework skills: `benchmark-checklist`, `blast-radius`, `correct`, `verification-before-completion`
