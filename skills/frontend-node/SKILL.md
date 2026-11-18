---
name: Frontend Node Stack
description: Frontend (Node.js tooling, React/Next/Vue/etc., TypeScript/JS) implementation skill with accessibility, stable test selectors, Playwright-friendly QA support, and evidence-based verification
---

# Frontend Node Stack

Use for `frontend-node` implementation and review tasks (UI components/pages/routes/state/forms, Node-tooling frontends such as React/Next/Vue/Svelte as present).

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and relevant core skills (`phase-execution`, `qa-playwright`, `blast-radius`, `systematic-debugging`, `fix-root-causes`, `attack-the-premise`, `verification-before-completion`, `artifact-state`).
- Implement only assigned scope; support phase acceptance criteria and QA traceability.
- Apply `typescript-best-practices` and `boundary-discipline` for TS/TSX work.

## Implementation and architecture
- Follow existing framework, routing, styling, component, and state-management conventions; do not introduce new libraries/patterns without spec/approval.
- Build from user-visible behavior and accessibility requirements; keep components focused and reusable where natural.
- Handle required states explicitly: loading, empty, error, success, disabled, and permission/unauthorized states.
- Use appropriate state boundaries (local/UI state, server/cache state, URL state, shared/global state) per existing app patterns.
- Keep client/server boundaries clear in SSR/framework contexts; avoid leaking secrets to client.

## Accessibility (a11y) and semantics
- Prefer semantic HTML elements and native behaviors before custom ARIA.
- Ensure forms have accessible names/labels, instructions, and validation feedback; associate errors with controls.
- Support keyboard navigation, logical focus order, and visible focus; manage focus on dialogs/navigation/state changes when applicable.
- Provide text alternatives for meaningful non-text content; ensure interactive controls have accessible names.
- Use ARIA only when necessary and correctly; verify roles/states/properties reflect actual behavior.
- Consider color/contrast, motion/reduced-motion, and responsive behavior consistent with project standards and scope.

## Testability and selectors (critical for QA/Playwright)
- **Add/maintain stable `data-testid` attributes for QA-critical elements and interactions** (primary actions, forms/inputs, key navigation targets, stateful regions, error/success surfaces).
- Prefer user-facing locators in tests (role/label/text) where stable; use `data-testid` when semantics/text are ambiguous, dynamic, or insufficiently stable.
- Do not remove/rename existing `data-testid` selectors without updating affected tests/notes and reporting impact.
- Document key flows, selectors added/changed, routes/URLs, feature flags, and required test data in handoff for QA.

## Data fetching, errors, and performance basics
- Follow existing data-fetching/caching/mutation patterns; handle race/stale/loading/error states.
- Avoid unnecessary renders and heavy client work in hot paths when easy wins align with scope.
- Preserve existing API contracts and auth/session handling; surface user-safe errors.
- Treat client input as untrusted (`input-validation-sanitization`) and never rely on client-side checks as the enforcement point for authorization (`auth-authorization`).
- When a published design doc exists (`tech-notes/<session-id>/<title>-<date>-design.md`), build from its tokens, states, and mobile-first behavior (`design-principles`) and port the intent into the project framework rather than pasting prototype code.

## Testing and verification
- Run relevant checks: typecheck, lint, unit/component tests, build, and targeted dev/runtime smoke checks as applicable.
- Prefer behavior-focused tests (user-observable outcomes) over implementation details.
- Verify key states/flows locally when feasible and report what was and was not exercised.
- **Playwright/UI QA prerequisite:** automation requires Playwright + browsers + runnable app; if unavailable, do not claim UI automation pass.

## Debugging and handoff
- Reproduce in smallest route/component/state; inspect render/props/state/network/console and boundary with backend/data/env issues.
- Handoff should include: files/components/routes changed, behavior impact, `data-testid` changes, commands/checks with results, local run instructions/URL/env notes, accessibility/error/loading/edge states handled, QA notes, and known limitations.

## References
- React Learn: https://react.dev/learn
- MDN Web Accessibility: https://developer.mozilla.org/en-US/docs/Web/Accessibility
- W3C WCAG 2.2 Quick Reference: https://www.w3.org/WAI/WCAG22/quickref/
- web.dev Learn Accessibility: https://web.dev/learn/accessibility
- Testing Library Guiding Principles & Query Priority: https://testing-library.com/docs/queries/about/
- Playwright Best Practices: https://playwright.dev/docs/best-practices
- Playwright Locators: https://playwright.dev/docs/locators
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/
