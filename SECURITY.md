# Security Posture — CraftAgents Marketing Site

This is a **static frontend** (HTML/CSS/JS) with a **scripted mock chat widget**. There is no
backend, database, auth, or server-side code in this repo. Security controls below are scoped to
that reality. We do not fabricate protections for infrastructure that doesn't exist yet.

## Applied (relevant to a static frontend)

- **No secrets in the frontend or repo.** No API keys, tokens, or credentials anywhere. The
  only externalized value, `BOOKING_URL`, is a non-secret placeholder.
- **`.gitignore`** covers `.env`, `.env.*`, `*.key`, `*.pem`. No secrets have ever been committed
  (repo history contains only the static site).
- **XSS-safe rendering.** The mock widget renders ALL message text (including anything a visitor
  types) via `textContent`, never `innerHTML`. Verified: no `innerHTML`, `document.write`,
  `eval`, or `insertAdjacentHTML` in the codebase.
- **Input validation.** The widget input has `maxlength="200"` plus JS trim, empty-check, and a
  length cap (defense in depth).
- **Security headers.**
  - Via `<meta>`: Content-Security-Policy and Referrer-Policy on both pages.
  - Via `_headers` (Netlify) for the ones `<meta>` can't set: X-Frame-Options, X-Content-Type-Options,
    Referrer-Policy, Permissions-Policy, and a CSP with `frame-ancestors 'none'`.
- **Outbound link safety.** Booking buttons that open a new tab get `rel="noopener"`.
- **No cookies.** The site sets no tracking/advertising cookies, so cookie flags are N/A.
- **No CSRF surface.** No form POSTs to a server. The chat form is `preventDefault`ed and local;
  contact is via `mailto:`.
- **No dependencies.** Pure HTML/CSS/JS, no packages, so no dependency/supply-chain risk to manage.
- **No source maps / no verbose errors.** No build step; nothing leaks.

## Known tradeoff
- CSP currently allows `'unsafe-inline'` for styles and scripts on `index.html` because CSS/JS
  are inline in v1. To tighten: move CSS/JS to external files and drop `'unsafe-inline'` (use a
  nonce/hash if any inline remains). Tracked as a future improvement, not a v1 blocker.

## Parked until a real backend / live agent exists
These are NOT applicable to a static site and are intentionally not implemented here. They become
required when the real RAG agent + lead-routing backend is built:

- SQL / NoSQL injection
- JWT / session management, weak/leaked secrets
- Firebase / Supabase / S3 configuration
- IDOR, auth/authz, multi-user data isolation, tenant isolation
- Admin route protection
- Server-side rate limiting on login / signup / AI endpoints
- SSRF
- Webhook signature verification
- Payment / subscription checks
- Prompt injection in AI features
- AI tool/action data-access permission checks
- Audit logs, monitoring/alerting, backup/restore
- Database user permissions

(The live roofing-rag-agent backend already implements several of these — rate limiting, input
validation, secrets in env. They apply there, not to this static site.)
