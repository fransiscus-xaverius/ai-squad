---
name: Benchmark Checklist
description: Validate performance measurements before reporting or acting on them; explain limiter, correctness, and reproducibility with evidence
---

# Benchmark Checklist

Use when producing or evaluating a performance claim (speedup/regression, latency/throughput, resource use). Unvalidated numbers are not evidence.

## Before running
- State the claim precisely: metric, scenario/workload, dataset, environment/config, and expected effect threshold.
- Understand what the benchmark/script measures, excludes, and how it warms/caches/retries.

## Validate with evidence
1. **Limiter identified:** determine what bounds result (CPU, memory/GC, I/O, network, lock/contention, DB, external dependency). Do not guess.
2. **Comparable runs:** same build/config/versions/data/state and fair ordering across variants (or document differences).
3. **Correctness/work actually happened:** outputs correct; requests/operations completed (not timed out/no-op/lazy-skipped). Count errors/timeouts/retries.
4. **Plausibility:** improvement cannot exceed time/resources spent in changed path; sanity-check against profiles/limits.
5. **Repeatability/noise:** run enough iterations with stable conditions; report median and spread/variance. If noise >= effect, report **no measurable difference**.
6. **End-to-end relevance:** relate micro-benchmark to user-visible/system path when making product claims.

## Verdicts
Lead with one of: **faster / slower / no measurable difference / inconclusive**.
- **Inconclusive** when limiter unknown, runs not comparable, correctness/work unverified, or noise dominates; state the specific gap.

## Reporting
Include claim, environment/config, method, run count/order, median + spread/range, limiter evidence, correctness/error notes, conclusion, and links to raw outputs/artifacts. Apply `verification-before-completion`.

## References
- pstack, *benchmark-checklist* (adapted): https://github.com/cursor/plugins
- Go diagnostics/profiling and race tooling context: https://go.dev/doc/diagnostics
- Node.js performance/diagnostics learning resources: https://nodejs.org/en/learn
- Framework: `verification-before-completion`, `artifact-state`
