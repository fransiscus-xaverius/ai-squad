---
name: WebSocket Security
description: Harden and verify WebSocket (wss) endpoints for transport, handshake, origin, session, per-message authorization, input validation, and resource-control requirements
---

# WebSocket Security

Use for real-time endpoints (WebSocket upgrade handling, subscription channels, streaming messages) in backend implementation, QA, and review work. Pair with `secure-backend-engineering` and `auth-authorization`; `input-validation-sanitization` for payload handling rules.

## Framework alignment
- Follow `harness/engineering-harness.md`, `core/artifacts.md`, and `blast-radius` (a handshake/authorization gap affects every connected client).
- Real-time channels usually lack the request/response HTTP gates, so treat each control below as a required implementation item and as a QA case with evidence.
- Record connection/auth/message policy decisions in the tech spec and handoff; note client impacts (reconnection, auth refresh, error codes).

## Transport and protocol
- **Always use `wss://`** in production; never ship plain `ws://` for non-local traffic.
- **Support only RFC 6455**; do not retain legacy handshake/version fallbacks.
- **Disable `permessage-deflate`** unless there is a measured need and the risk of compression-based information leakage has been reviewed.
- Ensure proxies/load balancers/CDNs pass the HTTP upgrade correctly, allow long-lived connections, and set read/idle timeouts.

## Handshake: origin, authentication, session
- **Validate the `Origin` header on every handshake against an explicit allowlist** (allowlist, not denylist; avoid wildcards or substring matching). Browsers send `Origin` and page scripts cannot override it.
  - Node.js (`ws`): perform the check in the HTTP server's `upgrade` event before calling `handleUpgrade` (the library discourages `verifyClient`).
  - Go (`gorilla/websocket`): implement the check in `CheckOrigin` rather than always returning true.
- **WebSockets have no built-in authentication:** the handshake must establish identity explicitly.
  - Cookie-based sessions: set `SameSite` attributes (`Lax`/`Strict`) to reduce cross-site transmission; include the project's CSRF token in the handshake when the app already uses CSRF protection.
  - Token-based clients: prefer sending the token in the **first message** over `wss://` rather than in the URL query string (URLs leak into access logs/proxies).
- Until authentication succeeds, accept only the authentication message and send no protected data; close on failure/timeout and cap the number of unauthenticated connections.
- **Session lifecycle:** re-validate long-lived sessions periodically; close connections when the session expires; on logout, close that user's connections immediately via a session-to-connection mapping.

## Message-level authorization and validation
- **Authorize every action, not just the connection:** a valid connection does not imply permission for every message type or resource. Check role/ownership/tenant per message.
- **Treat all messages as untrusted:** validate structure and content against a schema with allow-listed fields/types; reject unknown message types.
- **Size limits:** set an explicit maximum message size (64 KB or less is a common starting point) and close/reject oversized messages.
- **Binary payloads:** determine file type from magic bytes/content inspection rather than declared content type; use safe deserialization for binary protocols.
- **Replay protection:** include a timestamp or nonce and reject duplicates/stale messages where the flow is sensitive.
- **Parsing:** use a safe structured parser (`JSON.parse` and equivalents), never evaluate message content as code.

## Resource controls (DoS resistance)
- **Connection limits:** cap total connections and apply per-user limits (preferred) or per-IP limits when identity is not yet established.
- **Message rate limits:** cap message rate per connection (e.g. ~100 messages/minute as a starting point) and return a clear error/close code when exceeded.
- **Idle/dead connections:** implement idle timeouts and heartbeat (ping/pong) to detect and clean up dead connections.
- **Backpressure:** many implementations lack flow control; ensure slow consumers cannot grow server memory unbounded (bounded queues, drop/disconnect policy).

## Observability
- Log connection establishment/termination (identity, IP, origin), authentication and authorization events during handshake and message handling, policy triggers (rate limit, validation failure), and abnormal disconnects/protocol errors.
- Do not log full message bodies, tokens, session identifiers, or personal data.

## Verification and evidence
- Test cases should cover: handshake without credentials, with invalid/expired credentials, from a disallowed origin, oversized message, unknown message type, action exceeding the caller's permissions, message flood, and session expiry/logout closing the connection.
- Use a local WebSocket client or the project's test client against a local server; capture command output/server logs as evidence.
- Report which controls are implemented, which are unverified (with the exact check needed), and any client-visible behavior changes.

## References
- OWASP WebSocket Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/WebSocket_Security_Cheat_Sheet.html
- RFC 6455, *The WebSocket Protocol*: https://www.rfc-editor.org/rfc/rfc6455
- OWASP Session Management Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
- OWASP Cross-Site Request Forgery Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html
- `ws` (Node.js) documentation: https://github.com/websockets/ws
- `gorilla/websocket` documentation: https://pkg.go.dev/github.com/gorilla/websocket
- Community pattern source (structure adapted for defensive use; Apache-2.0, community project not affiliated with Anthropic PBC): https://github.com/mukul975/anthropic-cybersecurity-skills (upstream skill `testing-websocket-api-security`)
