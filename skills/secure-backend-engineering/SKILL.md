---
name: Secure Backend Engineering
description: Apply defensive REST/API and service hardening practices (transport, access control, request handling, error/logging hygiene, and security headers) during backend implementation and verification
---

# Secure Backend Engineering

Use for backend/API/service implementation and review work where HTTP endpoints, workflows, or service-to-service interfaces are in scope. Apply alongside stack skills (`backend-node`, `backend-go`) and `auth-authorization`, `input-validation-sanitization`, and `backend-performance` as relevant.

## Framework alignment
- Follow `README.md` workflow, `harness/engineering-harness.md`, `core/artifacts.md`, and relevant core skills (`phase-execution`, `blast-radius`, `boundary-discipline`, `verification-before-completion`, `artifact-state`).
- Implement only assigned scope; record security-relevant decisions, assumptions, and residual risks with evidence in handoff/state artifacts.
- Prefer existing project security middleware/patterns; do not invent parallel controls (`ponytail`).

## Transport and endpoint exposure
- **HTTPS only:** expose secure endpoints; protect credentials/tokens in transit and enforce HSTS per deployment context. For highly sensitive paths, consider mTLS where architecture requires.
- **Management/internal endpoints:** avoid public exposure. If externally reachable, require strong authentication (prefer MFA where applicable), separate ports/hosts/subnets where possible, and restrict with firewall/ACL controls.
- **Do not leak secrets in URLs:** keep passwords, tokens, API keys, and sensitive identifiers out of query/path strings; use headers or request bodies per protocol conventions.

## Request handling and contracts
- **HTTP methods:** define and enforce an allowlist per endpoint; reject disallowed methods with **405 Method Not Allowed**.
- **Content negotiation and types:** for requests with bodies, require a supported `Content-Type` per endpoint contract and reject unsupported types with **415 Unsupported Media Type**. Return **406 Not Acceptable** only when response representation cannot satisfy `Accept` preferences (and no default applies).
- **Size limits:** define and enforce request/body/upload limits; reject oversized requests with **413 Payload Too Large**.
- **Input validation:** validate type/range/format/structure at boundaries before business logic; reject unexpected content. Pair with `input-validation-sanitization` for parsing/encoding/file/log-injection controls.
- **Workflow/state validation:** enforce server-side state transitions for multi-step flows; do not trust client sequencing. Bind operations/tokens to intended workflow state and reject invalid/out-of-order transitions explicitly.

## Authentication, authorization, and abuse controls
- **Access control per endpoint/object/action:** authenticate and authorize every request locally according to design (centralized IdP/tokens acceptable). Deny by default and apply least privilege. Pair with `auth-authorization`.
- **API keys (if used):** treat as sensitive credentials; require per request to protected endpoints, apply rate/usage controls, revoke on abuse/compromise, and do not rely on API keys alone for sensitive/high-value resources.
- **Rate limiting/throttling:** return **429 Too Many Requests** when limits are exceeded; protect login, OTP, expensive, and enumeration-prone operations.

## Responses, errors, and status codes
- Use semantically correct HTTP status codes (e.g. **200/201/202**, **400**, **401** for missing/invalid authentication, **403** for authenticated but unauthorized, **404**, **405**, **406**, **413**, **415**, **429**, **500/503**).
- **Generic error responses:** do not expose stack traces, SQL/errors, internal paths, or sensitive implementation details to clients.
- Keep response bodies and schemas consistent with contracts; avoid accidental data overexposure.

## Security headers and CORS (browser-exposed APIs)
- Apply appropriate response headers per context: `Cache-Control: no-store` for sensitive responses, `Content-Type` accuracy + `X-Content-Type-Options: nosniff`, transport security headers (HSTS), framing protections (`Content-Security-Policy: frame-ancestors 'none'` and legacy `X-Frame-Options: DENY` where needed), and restrictive `Referrer-Policy`/`Permissions-Policy` as applicable.
- **CORS:** disable when cross-origin access is not required; otherwise use explicit origin allowlists (no wildcard/reflective origins for credentialed or sensitive flows) and minimal allowed methods/headers.

## Logging, audit, and operations
- Write audit logs for security-relevant events (authn/authz decisions/failures, privilege changes, sensitive data access/workflow steps) with sufficient context but without secrets/PII beyond policy.
- Sanitize/encode untrusted data before logging to prevent log injection; use structured logging and correlation IDs consistent with project patterns.

## Verification and evidence
- Add/update tests for authz failures, invalid methods/types/sizes, workflow/state violations, and security headers/CORS behavior where feasible.
- Run relevant checks (typecheck/lint/tests/build/smoke) and report commands/results. For UI/browser-facing flows, ensure prerequisites before claiming automated pass (`qa-playwright`).
- Handoff should include endpoints/flows changed, controls enforced, status/error behavior, config/env prerequisites, checks run, and known gaps/risks.

## References
- OWASP REST Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html
- OWASP HTTP Headers Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html
- OWASP Error Handling Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html
- OWASP Logging Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
- OWASP CORS Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/CORS_Security_Cheat_Sheet.html
- OWASP API Security Project (Top 10 2023): https://owasp.org/API-Security/editions/2023/en/0x11-t10/
- Community pattern source (structure adapted for defensive use; Apache-2.0, community project not affiliated with Anthropic PBC): https://github.com/mukul975/anthropic-cybersecurity-skills (upstream skill `testing-api-security-with-owasp-top-10`)
