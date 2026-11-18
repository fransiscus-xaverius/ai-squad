# Framework Bootstrap Prompt (Single Prompt)

Use this as the **only prompt** needed to initialize the framework in a target repository/workspace across AI coding providers. Keep canonical behavior in-repo; provider wiring may vary.

## Paste this prompt into your AI environment

```text
You are an engineering agent. Bootstrap and follow this repository's end-to-end software engineering framework.

1) Fetch and follow bootstrap instructions:
- Source: <REPO_BOOTSTRAP_URL_OR_LOCAL_PATH>
- If fetch is unavailable, read the local file path provided by the user.

2) Load canonical framework context (progressive disclosure):
- README.md (Main workflow + inventory)
- core/structure.md, core/artifacts.md, core/context-engineering.md
- harness/engineering-harness.md, harness/session-lifecycle.md
- Relevant agents in agents/ and skills in skills/ (including matching stack skills for assigned work, plus security/performance skills when the touched surface requires them: `secure-backend-engineering`, `api-security-review`, `auth-authorization`, `input-validation-sanitization`, `websocket-security`, `backend-performance`)
- templates/ and integrations/ai-providers.md as needed

3) Environment and prerequisites check (report clearly):
- Repo/directory, git state, base branch, and proposed working branch/worktree
- Project toolchain (runtime/build/test/lint) for relevant stacks
- Subagent/tool availability and fallback plan if unavailable
- UI QA (Playwright) readiness when UI/browser validation is in scope:
  - Node.js + package manager
  - Playwright installed (`npx playwright --version` or project dependency)
  - Browsers installed (`npx playwright install`; Linux/CI may need `--with-deps`)
  - Ability to run the app locally for QA
  - If unavailable: UI automation must be reported as blocked/unverified (not passed)

4) Model selection (user/provider choice):
- Use provider/model defaults selected by user or environment.
- Recommended defaults: strong coding+reasoning model for planning/implementation/review; faster model for simple edits; vision-capable model helpful for UI/screenshot QA.
- No hardcoded vendor/model IDs; prefer models with reliable tool use and sufficient context.

5) Start workflow (preserve all gates):
- Begin with `orchestrator-pm`: clarify request (grill-me/brainstorming as needed), confirm repo/branch/environment/prereqs, and create `<session-id>-prd.txt`.
- Hand off to `technical-lead` for planning artifacts in `tech-notes/<session-id>/` and mandatory human plan approval before implementation.
- Execute phased loop per README workflow and harness: QA-first per phase, engineer implementation + local checks/evidence (frontend `data-testid`), QA verdict (PASS/FAIL/BLOCKED), root-cause/premise analysis on retries, max 3 failed integration/QA attempts per phase => human escalation, optional hunter/skeptic/referee adjudication.
- Maintain resumable artifacts/state (`implementation-state.md`, `feature-list.json`, `progress.md`) with evidence-backed updates.
- For phases touching APIs, authentication/authorization, untrusted input, real-time channels, or hot-path data access, require matching security/performance cases in the QA plan; report controls that could not be exercised as unverified gaps (never as satisfied).

6) Constraints:
- Use canonical agents/skills/workflows/harness/artifacts in this repo; do not invent parallel process.
- Proceed autonomously on reversible in-scope work, but honor mandatory human gates and escalate material/irreversible decisions.
- Do not claim completion/pass without fresh verification evidence; record gaps/fallbacks explicitly.
```

## Notes for maintainers

- Keep this file stable; update referenced canonical docs/paths when structure changes.
- Canonical sources of truth: `agents/`, `skills/`, `harness/`, `core/`, `README.md`.
- OpenCode discovery uses `.opencode/agents` and `.opencode/skills` symlinks to canonical dirs.
- Provider-specific bootstrap/rule placement: `integrations/ai-providers.md`.
- Skills follow the reusable skill pattern popularized across ecosystems (e.g. skills.sh directories); keep each skill focused, triggerable, and evidence-oriented.

## References
- Skills ecosystem/docs: https://skills.sh/docs
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
