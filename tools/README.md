# Tools and Integrations (Conventions)

Expected tool usage conventions for this framework. Tools are not bundled unless explicitly added; availability depends on provider/environment. Design and use tools so agents can act reliably with clear, evidence-producing outputs.

## Tool categories

| Category | Purpose | Typical usage |
|---|---|---|
| **File read/write/edit/search** | Inspect code, update artifacts, implement targeted changes | All roles; TL maintains canonical artifacts/state |
| **Shell / CLI** | Build, test, lint, run services, inspect repo/env | Engineer local verification; QA checks; TL env validation |
| **Browser automation (Playwright)** | UI/e2e validation and evidence capture | QA for frontend flows; prefer stable selectors and traces on failure |
| **Git / VCS** | Branch/worktree state, diffs, history, checkpoints | Intake/TL context; review scope; resumable progress (when used) |
| **Subagent/task delegation** | Specialized/fresh-context role execution, parallel work | TL/PM orchestration (provider-dependent); fallback to sequential with same gates |
| **Web fetch/search (when available)** | Retrieve external docs/references | Research with reputable sources; record citations/URLs in artifacts when decisions depend on them |

## Design and usage principles (tooling)

- **Right tool for the job:** prefer dedicated tools over ad-hoc shell parsing when available; use shell for project commands (build/test/run).
- **Clear contracts:** commands/inputs should be unambiguous; capture outputs, exit status, and scope tested as evidence.
- **Poka-yoke (error-resistant):** use absolute/explicit paths, targeted commands, and reproducible steps; avoid destructive operations without confirmation.
- **Token/context efficiency:** return concise, relevant results; link large logs/artifacts instead of flooding context.
- **Idempotence and safety:** avoid irreversible actions unless explicitly approved; document side effects (migrations, installs, generated files).

## Prerequisites

### Playwright (UI/browser QA flows)
Required for UI automation claims:
- Node.js + package manager
- Playwright installed (`npx playwright --version` or project dependency)
- Browsers installed (`npx playwright install`; Linux/CI may need `npx playwright install --with-deps`)
- Target app runnable locally (URL/dev server/build)

If unavailable, report prerequisite gap and mark UI automation **blocked/unverified** (not passed).

## Evidence and reproducibility
- Record commands run, key outputs/results, environment assumptions, and artifact/evidence paths.
- For UI QA: capture screenshots/traces/videos/logs as applicable; prefer Playwright trace viewer artifacts for CI/failure diagnosis.
- Frontend QA-critical elements should have stable `data-testid` selectors (engineer responsibility).

## Provider limitations and fallbacks
- If a tool/capability is missing (subagents, browser, network, vision), preserve workflow gates and document fallback verification and limitations in `implementation-state.md` and QA/review artifacts.
- User/provider selects models; prefer models with reliable tool use and sufficient context for the task.

## Extensions
- Add project-specific wrappers/scripts in `tools/` for standardized build/test/run commands.
- Add provider/MCP configuration docs in `adapters/` or `integrations/`.
- Add environment bootstrap scripts when appropriate (documented and safe).

## References
- Anthropic, *Writing effective tools for agents*: https://www.anthropic.com/engineering/writing-tools-for-agents
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
- Playwright Best Practices: https://playwright.dev/docs/best-practices
- Playwright CI: https://playwright.dev/docs/ci
- Skills ecosystem (discovery/packaging reference): https://skills.sh/docs
