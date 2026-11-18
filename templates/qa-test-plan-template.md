# QA Test Plan — <SESSION_ID> — <PHASE>

## Scope
- Phase/task:
- PRD/plan/spec references: `tech-notes/<session-id>/...`, `<session-id>-prd.txt`
- Acceptance criteria covered (IDs/links):

## Environment and prerequisites
- Build/URL/services under test:
- App run command(s) / config / branch-worktree:
- Required tooling available (test runner, browsers, Playwright, etc.):
- Playwright status (UI flows): `ready | not installed | browsers missing | app not runnable | n/a`
  - Setup/commands if needed: `npx playwright install` (Linux/CI may need `--with-deps`)
  - If not ready: UI automation = **BLOCKED/UNVERIFIED** (not passed)
- Test data/accounts/fixtures/feature flags:

## Preconditions and assumptions
- Setup steps:
- Dependencies/invariants:
- Known constraints/gaps:

## Test cases
| ID | Title | Type (unit/integration/ui/e2e/manual) | Preconditions | Steps | Expected result | Selector/locator or command (prefer role/label; use `data-testid` for QA-critical hooks) | Evidence to capture | Status |
|---|---|---|---|---|---|---|---|---|
| TC-01 |  |  |  |  |  |  |  | Not run |

## Coverage notes
- In scope:
- Out of scope:
- Risks/gaps not covered and rationale:

## Security / performance coverage (when in scope)
- Surfaces in scope (API endpoints / auth surface / input boundaries / real-time channel / hot-path data access):
- Applicable skills used for case design (`api-security-review`, `auth-authorization`, `input-validation-sanitization`, `websocket-security`, `backend-performance`):
- Expected status codes, limits, and behavior to assert (e.g. 401/403 split, 405/406/413/415, 429, origin allowlist, per-object authorization):
- Controls that cannot be exercised in this environment (must be reported as **BLOCKED/unverified**, never passed):

## TL review
- Adequacy: `Approved | Revisions required`
- Reviewer notes (coverage, selectors, env/prereqs, traceability):
- Date:
