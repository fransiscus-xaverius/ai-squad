---
name: Attack the Premise
description: When repeated fixes sharing the same assumption fail the same gate, test the assumption before attempting another fix
---

# Attack the Premise

## Trigger
Use when **repeated fixes fail the same gate/test/symptom pattern** or multiple attempts rely on the same unverified assumption.

## Premise check (before next retry)
1. **State the shared premise:** what must be true for the attempted fixes to work (e.g. "the bug is in module X", "tests are correct", "environment is valid", "API contract is Y").
2. **List contrary evidence:** failures, logs, inconsistencies, or observations that challenge the premise.
3. **Test the premise directly:** run a targeted experiment/check to confirm or refute it (isolate component, verify contract/input/output, reproduce minimally, validate environment/test harness).
4. **Decide:**
   - **Refuted:** pivot approach; update hypothesis/plan and record why.
   - **Confirmed:** proceed with a materially different fix strategy grounded in new evidence.
   - **Inconclusive:** gather specific missing evidence; do not guess.
5. **Record:** premise, test performed, result, and impact on next attempt.

## Integration with retry policy
- Mandatory consideration before each retry after repeated same-gate failures.
- **Max 3 failed integration/QA attempts per phase => escalate to human** with evidence, premises tested, hypotheses, and options (do not loop indefinitely).
- Update `implementation-state.md` and relevant artifacts with premise analysis.

## Examples of premises to challenge
- "The implementation is wrong" vs test/spec/environment is wrong or outdated
- "Failure is flaky" vs deterministic race/ordering/state leak
- "Fix is correct" vs wrong layer/contract/consumer
- "Tooling/CI issue" vs real product regression (or vice versa)

## References
- Superpowers, *Systematic Debugging* (challenge assumptions, isolate variables): https://github.com/obra/superpowers
- Anthropic, *Building effective agents* (evaluation/checkpoints, clarity): https://www.anthropic.com/engineering/building-effective-agents
- Framework harness: `harness/engineering-harness.md`
