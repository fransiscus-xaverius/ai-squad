---
name: Systematic Debugging
description: Investigate bugs and unexpected behavior with evidence-driven root-cause analysis before proposing or applying fixes
---

# Systematic Debugging

## Iron law
**No fixes without root-cause investigation first.**

Symptom-only patches and guess-and-check loops are failure modes, especially under pressure.

## Use for
- Test failures, regressions, unexpected behavior, build/integration issues, performance problems.
- Repeated failed attempts or unclear failures across boundaries/components.

## Four phases

### 1) Root-cause investigation
- Read errors, logs, stack traces, and failing outputs carefully.
- Reproduce reliably with exact steps/inputs/environment.
- Check recent changes (diffs/commits/config/deps/env) and isolate where behavior diverges.
- In multi-component systems, gather evidence at each boundary (input/output/state) before proposing fixes.
- Trace data/control flow backward from symptom to first faulty decision/state.

### 2) Pattern analysis
- Compare with working examples/paths in the codebase or known-good behavior.
- Identify relevant differences (contracts, state, timing, config, data shape, dependencies).
- Understand assumptions and invariants before changing code.

### 3) Hypothesis and testing
- Form one specific, testable hypothesis.
- Test with the smallest change or observation that can confirm/refute it.
- If disproven, derive a new hypothesis from new evidence (do not stack random fixes).

### 4) Implementation and verification
- Capture intended behavior with a failing test/check when practical (`test-driven-development`/`targeted-tdd`).
- Implement a single fix addressing the root cause within scope.
- Verify fix and relevant regressions with fresh evidence (`verification-before-completion`).
- If fix fails, return to investigation; do not iterate blindly.

## Framework alignment
- Record symptom, reproduction, evidence, root cause, fix rationale, verification, and residual risks in artifacts (`implementation-state.md`, QA/review notes as relevant).
- Before retrying a failed phase, explain why the prior attempt failed and why this attempt differs.
- If repeated fixes fail the same gate or share an assumption, apply `attack-the-premise` before another attempt.
- **Max 3 failed integration/QA attempts per phase => escalate** with evidence, hypotheses tested, and options.

## References
- Superpowers, *Systematic Debugging*: https://github.com/obra/superpowers
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Playwright Trace Viewer (failure diagnosis): https://playwright.dev/docs/trace-viewer-intro
