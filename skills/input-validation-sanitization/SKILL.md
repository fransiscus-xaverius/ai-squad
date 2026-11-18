---
name: Input Validation and Sanitization
description: Validate and normalize untrusted input at system boundaries with allowlists, schema validation, size limits, safe parsing, encoding, and injection-resistant data access
---

# Input Validation and Sanitization

Use when handling untrusted input — HTTP params/query/body/headers, WebSocket messages, file uploads, webhooks, queue/job payloads, env/config, CLI args — in implementation, QA, and review work.

## Framework alignment
- Follow `harness/engineering-harness.md`, `core/artifacts.md`, `boundary-discipline`, and `typescript-best-practices` (typed boundaries).
- Validation belongs at the boundary, before business logic; internal code can then be trusted as typed.

## Core rules
- **Define what is accepted; reject everything else.** Prefer allowlists over denylists. Do not attempt to recognize every bad string (blocking characters breaks legitimate data and does not make a query safe).
- **Validate syntax, then semantics.** Syntax: type, format, length/range, character class. Semantics: is this value consistent with the business rule (state exists, quantity within limits, ownership valid)?
- **Parse safely first, then validate.** Parse into a typed structure with a safe parser (no entity expansion, no external entity resolution, no code evaluation) and reject malformed input instead of partially interpreting it.
- **Prefer strong types.** Use framework/typed parameters where available so invalid shapes fail at the edge; constrain strings with anchored patterns that must match the entire value.
- **Normalize consistently.** Agree on encoding across components, reject malformed input, and apply one Unicode normalization policy before validation, storage, and comparison where comparison semantics require it (document the policy).
- **Bound the work.** Set explicit limits for request/body size, string length, collection counts, nesting depth, numeric ranges, and processing time; reject oversized input (HTTP **413**) instead of truncating silently.
- **Bound pattern matching:** anchored, simple patterns for structured fields; avoid unbounded backtracking; cap input length before matching and prefer linear-time matching where input size is attacker-influenced.

## Injection-resistant data access
- Use **parameterized queries / prepared statements** for all data access; pass values separately from query text.
- Allowlist identifiers (column/table/sort direction) when they must be dynamic and map them through a fixed mapping rather than passing raw strings into query construction.
- Never build query strings by concatenating untrusted input, and never rely on manual escaping as the primary defense.
- Use safe serialization/deserialization for structured formats; avoid unsafe deserialization of untrusted payloads (type confusion/polymorphic gadget risks).

## Output and storage safety
- Encode for the **sink context** (HTML body/attribute/JS/URL), not generically. Prefer context-aware escaping helpers from the framework/library.
- For user-authored rich text, sanitize with an allowlist-based HTML sanitizer and keep the allowed tags/attributes narrow.
- Store and compare secrets with constant-time comparison; hash passwords with a dedicated password hashing function.
- Ensure redirects, file paths, and template names are validated against allowlists to prevent open redirect / path traversal.

## Files and uploads
- Enforce size and count limits before reading the whole payload; stream to storage with limits where possible.
- Determine type from **content inspection (magic bytes)** and validate against an allowlist; the client-declared content type and filename extension are untrusted.
- Store outside the web-served directory or serve through a handler that sets safe headers; never trust the supplied filename as a path.
- Scan for malware where policy requires; document the scanning boundary and failure handling.

## Headers, proxies, and logs
- **Host/forwarding headers:** do not build absolute URLs or trust client-supplied host/protocol from `Host`, `X-Forwarded-Host`, or `X-Forwarded-Proto` unless the deployment is explicitly configured with trusted proxies; derive URLs from configuration.
- **Log injection:** encode/escape untrusted values before writing them into logs; log the failure and relevant metadata, not full request bodies or secrets.
- Treat webhook/callback payload fields as untrusted input; validate structure, signature, and replay window before use.

## Verification and evidence
- Add tests for: invalid type, out-of-range value, over-length string, unknown/extra fields, missing required fields, malformed encoding, oversized payload, and disallowed values.
- Verify rejection happens **before** business logic side effects (no partial writes on validation failure).
- Record which validation rules exist per boundary and the evidence (test output/command) in handoff and QA artifacts.

## References
- OWASP Input Validation Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html
- OWASP SQL Injection Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
- OWASP Cross Site Scripting Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
- OWASP File Upload Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
- OWASP Deserialization Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html
- OWASP Logging Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
- Unicode Standard Annex #15 (Normalization Forms): https://www.unicode.org/reports/tr15/
- OWASP XXE Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html
