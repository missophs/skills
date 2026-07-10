---
name: security
description: >
  Security audit for code and infrastructure. Identifies vulnerabilities including OWASP Top 10,
  injection, auth flaws, insecure config, and secrets exposure. Use when reviewing code
  before shipping, doing a pre-deployment audit, or investigating a security incident.
---

Audit for security vulnerabilities. Flag each finding with severity and exact fix.

## Severity levels

- **CRITICAL** — exploitable now with no auth: RCE, SQLi, SSRF, hardcoded secrets
- **HIGH** — exploitable with minimal effort: auth bypass, privilege escalation, mass assignment
- **MEDIUM** — requires specific conditions: stored XSS, IDOR, insecure direct object reference
- **LOW** — defense in depth gap: missing security header, verbose errors, no rate limiting

## OWASP Top 10 checklist

### A01 Broken Access Control
- Every endpoint enforces auth. No auth checks skipped on "internal" routes.
- Object-level permissions: user can only access their own resources.
- No IDOR: IDs in URLs/params validated against session user.

### A02 Cryptographic Failures
- No plaintext secrets in code, logs, or HTTP responses.
- Passwords hashed with bcrypt/argon2/scrypt — not MD5/SHA1.
- TLS enforced everywhere. HTTPS-only cookies.
- Symmetric keys ≥128-bit, asymmetric ≥2048-bit RSA / ≥256-bit EC.

### A03 Injection
- All SQL uses parameterized queries or ORM — no string interpolation.
- Shell commands: no user input passed to exec/spawn without allowlist.
- Template engines: user content escaped before render.
- XML: disable external entity processing (XXE).

### A04 Insecure Design
- Sensitive operations require confirmation (re-auth, CAPTCHA, 2FA).
- Rate limiting on auth endpoints.
- Business logic: can user skip steps, replay actions, purchase at $0?

### A05 Security Misconfiguration
- Debug mode off in production.
- Default credentials changed.
- Stack traces not exposed to users.
- CORS: not `*` for credentialed requests.
- Security headers present: CSP, X-Frame-Options, HSTS, X-Content-Type-Options.

### A06 Vulnerable Components
- Dependencies pinned to versions with no known CVEs (`npm audit`, `pip-audit`, `trivy`).
- No abandoned packages.

### A07 Auth Failures
- Session tokens: random, ≥128-bit, rotated on privilege change.
- JWT: `alg` validated server-side (reject `none`). Secret not in repo.
- Password reset links: single-use, short expiry.
- Brute force protection on login.

### A08 Integrity Failures
- CI/CD pipeline: no untrusted code executed in privileged context.
- Deserialization of untrusted data: type-checked, no auto-execute.

### A09 Logging Failures
- Auth successes and failures logged with user/IP.
- No PII or secrets in logs.
- Logs tamper-evident (append-only store or SIEM).

### A10 SSRF
- Outbound HTTP from server: domain allowlist enforced.
- Internal metadata endpoints blocked (169.254.169.254, fd00::/8).

## Output format

```
[SEVERITY] <vulnerability type>
Location: file:line
Issue: <what's wrong>
Fix: <exact code or config change>
```
