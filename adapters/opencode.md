# OpenCode Adapter

This repository includes an OpenCode-ready adapter while keeping canonical framework content provider-agnostic.

## Discovery and config

- **Canonical sources:** `agents/` and `skills/`
- **OpenCode discovery paths:** `.opencode/agents` and `.opencode/skills` (symlinks to canonical directories)
- **Project config:** `opencode.jsonc` (agent registry/behavior defaults as configured)

## Usage

1. Open this repository in OpenCode (or copy framework into target workspace preserving structure/symlinks).
2. Paste bootstrap prompt from `BOOTSTRAP.md` (or ensure agent loads canonical context).
3. Start with `orchestrator-pm` intake; follow canonical workflow in `README.md` and `harness/engineering-harness.md`.
4. Use TL to create `tech-notes/<session-id>/` artifacts and orchestrate phased QA-first execution/review with evidence.

## Notes

- Keep agent/skill definitions canonical in `agents/` and `skills/`; adapter paths should reference or mirror them.
- Verify symlinks and config resolve in the target environment; if symlinks are unsupported, copy canonical dirs into `.opencode/` equivalents.
- Model selection is user/provider-defined (no hardcoded IDs in canonical docs). Choose models appropriate for reasoning/tool use; vision-capable models help for UI QA.
- If subagents or specific tools are unavailable, run roles sequentially and preserve all artifacts, gates, and evidence requirements.

## References
- Skills ecosystem/docs: https://skills.sh/docs
- OpenCode adapter context: repository-local `opencode.jsonc`, `.opencode/agents`, `.opencode/skills`
