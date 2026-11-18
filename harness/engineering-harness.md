# Engineering Harness (Canonical)

Provider-agnostic execution, verification, evidence, and escalation rules for all roles. This harness encodes practices from long-running agent and multi-agent engineering guidance (Anthropic) adapted to this framework's artifacts and gates.

**Read with:** `README.md` (Main workflow), `core/structure.md`, `core/artifacts.md`, `core/context-engineering.md`, `harness/session-lifecycle.md`, and relevant skills in `skills/`.

## Core principles

- **Simple, composable patterns:** prefer the simplest workflow that meets requirements; add multi-agent complexity only where it improves outcomes (planning, parallelism, independent review), per "Building effective agents".
- **Source of truth:** PRD and TL-owned technical artifacts (`tech-notes/<session-id>/...`) govern scope and decisions. Do not infer silent scope changes.
- **Small, verifiable increments:** execute in phased, testable units with explicit acceptance criteria and evidence (long-running harness pattern).
- **Evidence over assertion:** no completion/pass/fix claim without fresh verification evidence (commands, tests, traces/screenshots/logs, artifact paths). Apply `verification-before-completion`.
- **QA-first per phase:** define/review tests before implementation for each phase; verdicts gate progress.
- **Fresh-context handoffs:** subagents/roles may start without prior chat context. Every handoff must be a complete packet (objective, scope, constraints, artifact paths, success criteria, prior attempts/root-cause context, required output/evidence).
- **Autonomy with gates:** proceed on reversible in-scope decisions; pause only at mandatory human gates or irreversible/material scope/risk decisions (`autonomy-with-gates`).
- **Root-cause before repeat fixes:** retries must address evidenced causes/premises, not symptoms (`fix-root-causes`, `systematic-debugging`, `attack-the-premise`).
- **No silent scope creep:** deviations require TL note; material deviations require human confirmation/approval.
- **Secure by default, verified by evidence:** new HTTP surfaces, authentication/authorization, untrusted input, and real-time channels require explicit controls (`secure-backend-engineering`, `api-security-review`, `auth-authorization`, `input-validation-sanitization`, `websocket-security`) and matching QA cases. A control that could not be exercised is recorded as **unverified**, never assumed present.
- **Design from the product, not the template:** interface work starts from the real user flow and lands in an approved design handoff before implementation; screens are not built from a default shell, and design states (loading/empty/error/permission) are designed, not improvised in code.

## Prerequisites and environment

- **Toolchain:** project runtimes/build/test/lint tools for target stack(s).
- **Git/workspace:** confirm repo, base branch, working branch/worktree as part of intake/planning gates.
- **Playwright (UI/browser QA):** required for UI automation claims. Prereqs: Node.js + package manager, Playwright installed (`npx playwright --version`), browsers installed (`npx playwright install`; CI/Linux may need `--with-deps`), and runnable target app. **If unavailable, UI automation is blocked/unverified (never PASS)**; record gaps and alternatives in QA verdict/state.
- **Model selection (user/provider choice):** no hardcoded model IDs. Prefer capable coding/reasoning models for planning/implementation/review; faster models for simple edits; vision-capable models helpful for UI/screenshot analysis. Choose models with reliable tool use and sufficient context for multi-file work.
- **Provider/tool limitations:** if subagents, browser automation, network, or other tools are unavailable, preserve all gates/artifacts and document fallback verification and limitations.

## Role harness

### Orchestrator/PM (`orchestrator-pm`)
- Clarify ambiguity and intent before PRD finalization (`grill-me`, `brainstorming` as needed).
- **Mandatory gate:** confirm repo/directory, base branch, working branch, and relevant environment/prerequisites (including Playwright readiness for UI QA flows).
- Produce `<session-id>-prd.txt` (problem/goals/non-goals, acceptance criteria, constraints, context, assumptions/open questions).
- Do not start technical implementation; hand off to `technical-lead` with artifact paths and confirmed context.
- Keep user informed of gates, status, blockers, and required decisions.

### Technical Lead (`technical-lead`)
- Owns canonical artifacts under `tech-notes/<session-id>/`: `implementation-plan.md`, `state-machine.md`, `tech-spec.md`, `implementation-state.md`, and session tracking (`feature-list.json`, `progress.md`) per `session-lifecycle.md`.
- Converts PRD into phased plan with dependencies, acceptance/success criteria, verification method, stack/role assignments, risks, and rollback/mitigation notes (`writing-plans`, `architect` for non-trivial design).
- Requires `blast-radius` analysis for risky/cross-cutting changes (safety fact, proof/evidence or explicit unproven gap).
- Ensures matching stack skills are applied (`backend-node`, `frontend-node`, `backend-go`, `typescript-best-practices` for TS/TSX).
- Reviews QA test plans for adequacy before implementation each phase.
- Orchestrates engineers/QA/reviewers with precise, self-contained handoff packets (`subagent-driven-development`, `dispatching-parallel-agents` when safe; sequential fallback if unsupported).
- **Retry policy:** before retrying failed phase, require recorded root-cause/premise analysis and why next attempt differs. If failures share same gate/pattern, apply `attack-the-premise`. **Max 3 failed integration/QA attempts per phase -> mandatory human escalation** with evidence, hypotheses, and options.
- Maintains decision trail (decisions, assumptions, pivots, retries, reversions) with why/evidence/result; updates canonical state summaries.

### Engineer specialists (`engineer-specialist-<stack>`)
- Implement only assigned phase scope aligned to PRD/plan/spec; follow relevant stack skill and framework skills.
- Run relevant local verification before handoff (typecheck/lint/tests/build/smoke as applicable) and report fresh evidence.
- On failures, debug systematically and fix root causes; record rationale and rerun evidence.
- Frontend engineers must add/maintain stable `data-testid` for QA-critical interactions and document selector/flow notes for QA.
- Apply the security/performance skills for the surface in scope (`secure-backend-engineering`, `api-security-review`, `auth-authorization`, `input-validation-sanitization`, `websocket-security`, `backend-performance`) and report which controls were implemented, verified by evidence, or left unproven.
- Report: files changed, checks/commands/results, behavior/contract impact, risks/limitations, and spec ambiguities.
- Do not declare phase complete without evidence.

### Designer (`designer-ui-ux`)
- Runs **in parallel** with the technical lead and engineers; the design lane never blocks implementation: publish the direction checkpoint first, then rolling prototypes (`tech-notes/<session-id>/prototypes/*.html`), while engineers build from the published design doc.
- Owns the frontend design doc `tech-notes/<session-id>/<title>-<date>-design.md` (`templates/design-doc-template.md`), which lists the direction, tokens, **fonts**, **libraries and custom CSS**, and **every prototype file** — the contract engineers implement and QA verifies.
- Derives interface direction from the product's real flow (states, data, entry/exit points), not from a default template; states the default it avoided and the reason for its own direction (`antialgorithm`).
- Applies the project's rules (`design-principles`, including the mobile-first rule) and the broader design guidance (`ui-ux-pro-max`); records any rule intentionally broken and why.
- Specifies the system (tokens, component states, icon set, motion) plus every state (loading, empty, error, success, disabled, permission) and responsive/mobile-first behavior — not just the happy path.
- Prototypes are reference artifacts (self-contained HTML, no build step), not production code; engineers port the intent into the project's framework and tokens.
- Verifies what can be verified (contrast ratios, focus visibility, reflow, mobile layout at 320/375px, reduced motion, target sizes); unverified items are reported as unverified, never assumed.
- **Change protocol:** a design or prototype change after implementation started is recorded in the design doc change log and raised with the technical lead, who applies `blast-radius` to decide re-work versus an accepted deviation. Direction approval is tracked by the doc status (`draft → in-review → approved`).

### QA agent (`qa-agent`)
- Produces/revises phase test cases before implementation; TL confirms adequacy before build work proceeds.
- Executes validation against target environment (local when applicable) with reproducible steps and evidence.
- Uses Playwright for browser/UI flows when prerequisites are met; prioritizes user-facing locators (role/label/text) and `data-testid` for QA-critical stable hooks; uses web-first assertions/auto-waiting; captures traces/screenshots/videos/logs on failure where possible (Playwright best practices).
- Issues verdict **PASS / FAIL / BLOCKED** with scope, env/prereqs, steps, expected vs actual, evidence paths, defects, and distinction between product vs environment/harness issues when inferable.
- Never reports UI automation PASS when prerequisites/app/runtime unavailable.
- Include security/performance cases for in-scope API, authentication/authorization, input-boundary, and real-time surfaces (`api-security-review`, `auth-authorization`, `input-validation-sanitization`, `websocket-security`, `backend-performance`); a control that could not be exercised is **BLOCKED/unverified**, not a pass.
- For UI phases, verify the approved design doc (`tech-notes/<session-id>/<title>-<date>-design.md`): every designed state exists (loading/empty/error/success/disabled/permission), tokens are used instead of raw values, contrast/focus/target-size/reflow/mobile-first/reduced-motion expectations hold, and the handoff's `data-testid` suggestions are present and stable. Prototypes are the visual reference, not the app: the verdict covers the implementation.

### Review roles (hunter / skeptic / referee, per stack)
- **Hunter:** find likely defects/regressions/edge/security/contract issues with concrete evidence (locations, repro/reasoning, executed checks) and impact.
- **Skeptic:** independently validate each finding as confirmed/refuted/inconclusive with rationale/evidence; challenge weak premises.
- **Referee:** adjudicate to accepted/rejected/needs-more-evidence with severity/priority/actionability; prefer fixes for confirmed root causes.
- All review outputs are evidence-backed and actionable; route blocking accepted findings back to fix/QA loops.
- **Security/performance in review:** hunters assess the controls for the surface in scope; skeptics confirm the control is absent at the actual enforcement point (not merely undocumented); referees require fixes at the enforcement point plus a regression test for accepted security findings.

## State, artifacts, and traceability

- **Ownership:** TL owns canonical implementation-state decisions/summaries; other roles contribute reports/findings/evidence.
- **Chronology:** each phase attempt records timestamp/context, agent(s), actions, checks, outcome, and next step.
- **Decision trail:** append superseding entries (do not rewrite history); capture why, evidence, and result.
- **Evidence paths:** QA under `qa/<session-id>/`, reviews under `reviews/<session-id>/`, technical artifacts under `tech-notes/<session-id>/`.
- **Feature tracking:** maintain `feature-list.json` and `progress.md` for resumability (status changes only with evidence).
- **Mandatory human gates:** intake context confirmation, plan approval before implementation, and escalation at retry limit breach (and material/irreversible decisions as required).

## Definition of done (phase/task)

A phase/task is done only when:
1. Implementation meets scoped acceptance criteria and relevant local checks pass with evidence.
2. QA verdict is **PASS** with required evidence for scope (or explicitly approved, documented exception).
3. Accepted blocking review findings (if in scope) are resolved or explicitly deferred by human decision.
4. `implementation-state.md` (and related artifacts/trackers) updated with outcome, evidence links, and decision/attempt history.

## References
- Anthropic, *Building effective agents*: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, *How we built our multi-agent research system*: https://www.anthropic.com/engineering/built-multi-agent-research-system
- Anthropic, *Effective harnesses for long-running agents*: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Anthropic, *Harness design for long-running application development*: https://www.anthropic.com/engineering/harness-design-long-running-apps
- Anthropic, *Effective context engineering for AI agents*: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Anthropic, *Writing effective tools for agents*: https://www.anthropic.com/engineering/writing-tools-for-agents
- Playwright Best Practices: https://playwright.dev/docs/best-practices
- OWASP Cheat Sheet Series (REST, WebSocket, Authentication, Authorization, Input Validation): https://cheatsheetseries.owasp.org/
