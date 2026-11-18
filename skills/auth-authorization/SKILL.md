---
name: Auth and Authorization
description: Design and verify authentication (identity proofing, tokens, sessions) and authorization (least privilege, deny-by-default, per-request/per-object checks) for services and APIs
---

# Auth and Authorization

Use when designing, implementing, or reviewing identity, sessions, tokens, roles/permissions, or per-object access control. Applies to HTTP APIs, service-to-service calls, and real-time channels (`websocket-security`).

## Framework alignment
- Follow `harness/engineering-harness.md`, `core/artifacts.md`, and `blast-radius` (authz regressions are cross-cutting).
- Decisions belong in the tech spec (`implementation-state.md` records deviations and human approvals); identity/permission model changes usually require TL sign-off.
- Pair with `api-security-review` (verification pass) and `secure-backend-engineering` (transport, headers, rate limits).

## Authentication (proving identity)
- **Centralize identity issuance** where architecture allows (identity provider issuing tokens) and keep access decisions local to the endpoint/service.
- **Credential handling:** store passwords with salted adaptive hashing (Argon2id/bcrypt/scrypt/PBKDF2 per platform guidance); never log or store plaintext; support credential paste; avoid composition rules that reduce entropy; support long passphrases.
- **MFA:** offer/step up to MFA wherever feasible, especially for administrative and sensitive operations; risk-based triggers (new device, recovery, unusual context) are acceptable.
- **Login throttling:** limit repeated attempts per account and per source; enforce lockout/backoff carefully to avoid denial-of-service on legitimate users.
- **Generic failure responses:** respond identically for unknown user, wrong password, or disabled account so the endpoint cannot be used to enumerate accounts (same for registration and recovery flows).
- **Re-authentication for sensitive actions:** require step-up/re-authentication before high-risk operations (password change, key/secret rotation, payouts, permission changes), and invalidate/rotate sessions and tokens after re-authentication.
- **Session/token hygiene:** bind tokens to session state where possible; enforce server-side expiry and idle timeout; invalidate sessions on logout, password change, and privilege changes; support revocation (short-lived access tokens + refresh-token rotation, or server-side denylist keyed by token identifier).

### Token (JWT) validation rules
- Tokens must be **integrity protected** (signature or MAC); reject unsecured tokens (`{"alg":"none"}`).
- The verifier must choose the verification algorithm from **its own configuration** — never from the token header.
- Prefer asymmetric signatures over shared MACs when multiple services validate the same tokens; if MACs are used, scope keys per service and rotate them.
- **Validate required claims by default:** `iss` (trusted issuer), `aud` (this service is the intended audience), `exp` (not expired), and `nbf` when the token profile requires it. Validate any additional mandatory claims for the profile.
- Keep token lifetimes short; use refresh flows for long sessions; keep sensitive personal data out of token payloads (they are readable by holders).
- Accept credentials from headers/bodies per protocol; **never from URLs** (logs/proxies leak them).

## Authorization (deciding what identity may do)
- **Deny by default** and **validate permissions on every request** — no reliance on UI-hidden controls or earlier middleware assumptions.
- **Least privilege:** grant only what is needed; plan scope early so permissions are not broadly granted and later revoked.
- **Model choice:** RBAC is common, but **ABAC (attributes) and ReBAC (relationships)** usually fit application needs better (e.g. "the user who created this record may edit it"). Choose and record the model early.
- **Per-object checks:** every request that references an entity needs a decision for that entity (ownership, tenant, relationship). Enforce it in the data-access layer (query constraint) so the check cannot be skipped by a different route.
- **Server-side only:** client-supplied identity, role, tenant, or ownership fields are inputs to be validated, never authorization facts.
- **Fail securely:** on policy error or missing context, deny and return a generic error; do not leak whether the resource exists.
- **Errors:** **401** when authentication is missing/invalid; **403** when authenticated but not permitted. Keep the distinction consistent with client behavior.

## Testing expectations
- Maintain an authorization matrix per resource/action/role (including cross-tenant and unauthenticated cases) and keep it as executable tests.
- Include negative tests: another user's object, another role's action, missing/expired token, disabled account, revoked session.
- Include regression tests whenever the permission model changes (see the OWASP authorization regression testing guidance in References, and apply `blast-radius` to scope the impact).

## Output and evidence
- Report the identity/permission model in use, where each decision is enforced (`file:line`), the test matrix status, and any endpoint still relying on role-only checks.
- Flag unverifiable controls (missing environment, dependent service unavailable) with the exact check needed — not as passes.

## References
- OWASP Authentication Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html
- OWASP Authorization Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- OWASP JSON Web Token Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_Cheat_Sheet.html
- OWASP Session Management Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
- OWASP Multifactor Authentication Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html
- OWASP Password Storage Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
- OWASP Authorization Regression Testing Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Regression_Testing_Cheat_Sheet.html
- NIST SP 800-162, *Guide to Attribute Based Access Control*: https://csrc.nist.gov/publications/detail/sp/800-162/final
- Community pattern source (structure adapted for defensive use; Apache-2.0, community project not affiliated with Anthropic PBC): https://github.com/mukul975/anthropic-cybersecurity-skills (upstream skills `testing-jwt-token-security` and `testing-api-for-broken-object-level-authorization`)
