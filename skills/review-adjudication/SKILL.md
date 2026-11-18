---
name: Review Adjudication
description: Run hunter-skeptic-referee code review workflow with evidence-backed findings and final adjudication
---

# Review Adjudication

Use this skill for structured code review when independent finding, challenge, and adjudication improve quality/risk control.

## Roles and outputs
- **Hunter (`hunter-specialist-<stack>`):** identify likely defects, regressions, edge/security/contract issues.
  - Output per finding: id/title, severity/impact, affected location(s), evidence (repro, code-path reasoning, command/test output), suggested direction.
- **Skeptic (`skeptic-specialist-<stack>`):** independently validate each hunter finding.
  - Output per finding: confirmed / refuted / inconclusive, rationale, supporting/counter evidence, premise checks or targeted verification performed.
- **Referee (`referee-specialist-<stack>`):** final adjudication and actionability.
  - Output: accepted findings (with severity/priority/required action), rejected findings (rationale), needs-more-evidence items, overall risk summary.

## Process
1. **Scope the review:** define files/changes/phase, intent, acceptance criteria, and relevant artifacts/evidence.
2. **Hunter pass:** produce evidence-backed findings (avoid style-only noise unless risk-bearing).
3. **Skeptic pass:** challenge assumptions/premises and verify claims where feasible.
4. **Referee pass:** adjudicate based on evidence and impact; prioritize confirmed root causes.
5. **Record artifacts:** save under `reviews/<session-id>/` using templates; update `implementation-state.md` with accepted actions/outcomes.

## Standards
- **Evidence over opinion:** every material claim/finding needs concrete support (locations, repro steps, traces/outputs, or traced reasoning).
- **Actionable outcomes:** specify what must change, where, and why; distinguish blocking vs non-blocking.
- **Blast-radius aware:** consider indirect/regression impact beyond the diff for accepted risks.
- **No silent dismissal:** rejected/inconclusive items include rationale and, if needed, what evidence would resolve them.

## Loop and gates
- Accepted blocking findings return to implementation and QA verification (with root-cause fix and fresh evidence).
- Integrate with phase/retry rules and escalation policy in `harness/engineering-harness.md`.
- Apply `verification-before-completion` before claiming findings resolved.

## References
- Anthropic, *Building effective agents* (evaluator/feedback loops): https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *How we built our multi-agent research system* (role separation/challenge): https://www.anthropic.com/engineering/built-multi-agent-research-system
- Framework: `harness/engineering-harness.md`, `core/artifacts.md`
