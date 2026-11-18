---
name: API Security Review
description: Review REST/JSON APIs against the OWASP API Security Top 10 as a defensive code-and-test pass, covering authorization, authentication, resource consumption, misconfiguration, and inventory checks
---

# API Security Review

Use when reviewing, hardening, or regression-testing an existing HTTP API (REST/JSON) as part of implementation, QA, or review phases. Complements `secure-backend-engineering` (build-time controls) with a structured verification pass over what was actually built.

## Scope and framing
- This is a **defensive review of code and behavior owned by the project**. It does not include scanning third-party or production systems, exploitation tooling, or credential attacks. Any dynamic probing must run against local/staging environments the team controls, with documented authorization.
- Use for: API endpoint inventories, per-object authorization checks, authentication/token handling review, resource-consumption limits, misconfiguration checks, and security test-case design for QA.
- Pair with `auth-authorization` (identity/permissions), `input-validation-sanitization` (payload handling), and `websocket-security` (real-time channels).

## Framework alignment
- Follow `harness/engineering-harness.md`, `core/artifacts.md`, `review-adjudication`, and `blast-radius` (a missing control often affects many endpoints).
- Record findings with location + evidence in `reviews/<session-id>/` (hunter template) and hand security cases to `qa-agent` for `qa/<session-id>/test-plan.md`.
- Classify each item as **implemented / not implemented / unverifiable** — unverifiable is a gap, not a pass.

## Review passes

### 1. Endpoint inventory and access control
- Enumerate endpoints (routes, methods, auth middleware, object identifiers) from code, route definitions, or the API spec.
- Confirm each endpoint declares expected authentication and authorization behavior; flag endpoints with no auth decision recorded.
- Check that method access is allowlisted per endpoint and that management/admin endpoints are separated and strongly protected.
- Check for legacy/duplicate/shadow endpoints still routable (version drift, deprecated paths).

### 2. Object-level authorization (BOLA/IDOR)
- Confirm per-object checks exist where a request references an entity, not only a role check.
- Verify the ownership/tenant constraint is applied in the data-access layer (query filter) rather than only in the route or client.
- Check nested/batch/list endpoints that accept multiple identifiers or filters, and endpoints where the identifier appears in body/query rather than path.
- Check that responses for out-of-scope objects do not leak existence differences to unauthorized callers.
- Note that identifier unpredictability (UUIDs) is defense in depth, not a substitute for authorization.

### 3. Property-level authorization and mass assignment
- Verify request payloads are mapped through an explicit allowlist of writable fields; privileged fields (roles, flags, balances, ownership, tenant) must not be client-settable.
- Verify responses are projected to intended fields; check for overexposure of internal identifiers, secrets, or sensitive attributes.

### 4. Authentication and token handling
- Confirm token/session validation happens server-side for every request path that needs identity; verify signature/algorithm policy, required claims (`iss`, `aud`, `exp`, `nbf` when required), expiry, and revocation behavior.
- Confirm session expiry, logout invalidation, and idle-timeout behavior are enforced.
- Confirm credentials/tokens are not accepted in URLs and are excluded from logs.

### 5. Resource consumption and abuse controls
- Verify rate limits/quotas exist on authentication, OTP/verification, expensive or bulk operations, and that exceeded limits return **429**.
- Verify pagination/limit caps prevent unbounded result sets, and that batch sizes are bounded.
- Verify request/body/upload size limits exist and reject with **413**.

### 6. Misconfiguration and error handling
- Confirm unsupported methods → **405**, unsupported request media types → **415**, unacceptable response negotiation → **406**.
- Confirm error responses are generic and do not expose stack traces, queries, internal hosts, or framework details.
- Confirm CORS is either disabled or restricted to an explicit origin allowlist, and that credentialed cross-origin requests are not permitted with permissive origins.
- Confirm security headers relevant to browser-consumed responses are present and correct.

### 7. Outbound/integration safety
- Review any server-side URL fetching (webhooks, importers, preview/avatar fetchers) for allowlisted destinations, scheme restrictions, redirect handling, and private-network/loopback blocking.
- Review consumption of third-party API responses: validate structure before use; do not trust third-party fields as authorization inputs.

### 8. Workflow/state integrity
- For multi-step flows (create → submit → approve → finalize), verify server-side state validation and rejection of out-of-order transitions; confirm frontend sequencing is not the only enforcement.

## Output format (per review or QA case)
- **Area**: endpoint/flow
- **Control expected**: one line
- **Status**: `implemented | not implemented | unverifiable`
- **Evidence**: `file:line`, test result, or command output
- **Impact**: what an unauthorized/over-privileged caller could achieve
- **Recommended action**: smallest sufficient fix, with test to add

## Verification expectations
- Prefer executable evidence: a targeted test (authz matrix, status-code contract, limit enforcement) over a code-reading claim.
- Every "implemented" claim needs evidence; every "unverifiable" needs the exact check that would close it.
- Security checks are part of phase acceptance when in scope: add them to the QA test plan and record results in the QA verdict (`templates/qa-verdict-template.md`).

## References
- OWASP API Security Top 10 (2023): https://owasp.org/API-Security/editions/2023/en/0x11-t10/
- OWASP REST Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html
- OWASP Authorization Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- OWASP IDOR Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html
- OWASP Mass Assignment Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html
- OWASP API Security Project: https://owasp.org/API-Security/
- Community pattern source (structure adapted for defensive use; Apache-2.0, community project not affiliated with Anthropic PBC): https://github.com/mukul975/anthropic-cybersecurity-skills (upstream skills `testing-api-security-with-owasp-top-10` and `testing-api-for-broken-object-level-authorization`)
