---
name: Autonomy with Gates
description: Proceed on reversible in-scope decisions without unnecessary blocking, while honoring mandatory human gates and approvals
---

# Autonomy with Gates

Use this skill to balance execution speed with required control points.

## Default behavior
- **Proceed without blocking** on reversible, in-scope decisions needed to make progress (local implementation details, sequencing, diagnostics, low-risk refactors within approved scope).
- **Record** assumptions, decisions, and rationale in artifacts when they affect behavior, verification, or future work.

## Mandatory gates (must pause for human input/approval)
- Intake context confirmation: repo/directory, base branch, working branch/worktree, and relevant environment/prerequisites.
- Plan/spec approval before implementation begins (as defined by workflow).
- Phase retry-limit escalation: **max 3 failed integration/QA attempts per phase**.
- Irreversible, destructive, security-sensitive, or materially out-of-scope decisions (including major architecture/scope changes, data-destructive actions, production-impacting operations).

## Escalate when
- Requirements or acceptance criteria are contradictory/unclear in a material way.
- Multiple viable options have significantly different risk/cost/scope implications.
- Evidence shows repeated failures tied to a questionable premise or missing prerequisite.
- Required tools/access/prerequisites are unavailable and block valid verification.

## Reporting
- State what was decided autonomously, why it is reversible/in-scope, and what evidence supports it.
- When blocked/escalating: provide concise status, evidence, options, and recommended next step.

## References
- Anthropic, *Building effective agents* (autonomy with checkpoints/human feedback): https://www.anthropic.com/engineering/building-effective-agents
- pstack autonomy/gating principles (adapted): https://github.com/cursor/plugins
- Framework: `harness/engineering-harness.md`, `README.md`
