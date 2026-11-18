---
name: Writing Skills
description: Create or revise canonical framework skills with clear trigger descriptions, testable guidance, and alignment to framework workflows and artifacts
---

# Writing Skills

Use when adding or revising skills in `skills/<skill-id>/SKILL.md` (canonical).

## Authoring rules
1. **Canonical location and format:** `skills/<skill-id>/SKILL.md` with YAML frontmatter (`name`, `description`). Adapters (e.g. `.opencode/skills`) should mirror/symlink canonical skills.
2. **Description defines trigger:** state when to use the skill clearly and specifically (conditions/scope), not the full procedure.
3. **Aligned and composable:** reference canonical workflow (`README.md`), `harness/engineering-harness.md`, `core/artifacts.md`, relevant roles/gates, and artifact paths; avoid duplicating other skills except minimal cross-references.
4. **Actionable and evidence-oriented:** provide concrete steps, inputs/outputs, verification/evidence expectations, and escalation/gate handling where relevant.
5. **Portable and safe:** keep guidance provider-agnostic; label prerequisites (e.g. Playwright for UI QA) and avoid unsafe/destructive defaults.
6. **Source-grounded when expanding:** cite reputable sources (official docs, Anthropic engineering posts, recognized references) in a References section for substantive domain guidance.

## Quality checklist
- Triggering is accurate (applies when it should, not overly broad/narrow)
- No contradiction with canonical workflow, harness, artifacts, or other skills
- Evidence, gates, and reporting expectations are explicit where applicable
- Examples/commands are practical and prerequisite-aware
- README inventory and relevant agent/bootstrap/docs references updated for canonical skills

## Validation mindset
- Test against representative scenarios: should trigger, should not trigger, and edge/pressure cases.
- Prefer clarity over verbosity; refine wording where misapplied.

## References
- Skills ecosystem/docs (packaging/discovery): https://skills.sh/docs
- Anthropic, *Writing effective tools for agents* (clear specs/descriptions): https://www.anthropic.com/engineering/writing-tools-for-agents
- Anthropic prompt engineering overview (clarity): https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview
- Superpowers, *Writing Skills*: https://github.com/obra/superpowers
