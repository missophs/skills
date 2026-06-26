---
name: caveman-review
description: >
  Terse one-line code review comments. Use when reviewing diffs, PRs, or
  code changes. Findings formatted as L<line>: <severity> <problem>. <fix>.
  Skips praise and obvious observations.
---

Review the current code changes. One line per finding.

## Format

```
L<line>: <severity> <problem>. <fix>.
```

**Severity levels:**
- `bug` — incorrect behavior, will break
- `risk` — won't break now but likely to cause problems
- `nit` — style, naming, minor cleanup
- `q` — question, unclear intent

## Rules

- One line per finding — no multi-line explanations
- Skip praise
- Skip obvious (no "add a comment here")
- If code looks good: say `LGTM` and stop
- Quote the specific identifier or value, not a paraphrase

## Examples

```
L14: bug `user.id` can be null here — add null check before comparison.
L27: risk unbounded loop if `items` never empty — add max iterations guard.
L42: nit `getData` → `fetchUserData` — name too generic.
L55: q why reset counter to 0 here instead of -1?
```
