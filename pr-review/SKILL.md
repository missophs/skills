---
name: pr-review
description: >
  Thorough pull request code review. Checks correctness, security, performance, test coverage,
  and API design. Use when reviewing a diff or PR before merge. Produces ranked findings
  with severity and suggested fix.
---

Review this diff for correctness bugs, security issues, performance problems, and missing tests. Rank findings by severity.

## Severity levels

- **CRITICAL** — data loss, security vulnerability, broken contract, crash in production path
- **HIGH** — logic bug that will surface under normal use, missing auth check, N+1 query
- **MEDIUM** — edge case unhandled, poor error message, test gap on changed code path
- **LOW** — style, naming, doc gap, minor inefficiency

## Checklist

### Correctness
- [ ] Does the logic match the intent described in PR title/description?
- [ ] Are all code paths (happy + error) handled?
- [ ] Are boundary conditions correct (empty input, null, zero, max value)?
- [ ] Are concurrency/race conditions possible?
- [ ] Are return values and error codes checked?

### Security
- [ ] Any user input used in SQL/shell/eval without sanitization?
- [ ] Auth/authz enforced on new endpoints?
- [ ] Secrets or credentials hardcoded or logged?
- [ ] CORS/CSP headers correct on new routes?
- [ ] Dependency version pinned to known-safe range?

### Performance
- [ ] N+1 queries introduced?
- [ ] Unbounded loops or missing pagination?
- [ ] Large allocations in hot paths?
- [ ] Caching invalidated correctly on writes?

### Tests
- [ ] Are new/changed behaviors covered?
- [ ] Are error paths tested, not just happy path?
- [ ] Are tests deterministic (no sleeps, no random seeds)?

### API / interface design
- [ ] Breaking change in public API? Versioned?
- [ ] Return shape consistent with existing endpoints?
- [ ] Error responses machine-readable (not just string messages)?

## Output format

List findings, most severe first:

```
[SEVERITY] file:line — <what's wrong> → <suggested fix>
```

Then a one-line summary: "Approve" / "Request changes" + reason.
