---
name: caveman-commit
description: >
  Generate terse caveman-style commit messages in Conventional Commits format.
  Use when writing or reviewing git commit messages. Subject ≤50 chars,
  imperative mood, lowercase after type. Body only when "why" isn't obvious.
---

Generate a terse commit message for the current staged changes.

## Format

Conventional Commits format:

```
<type>(<scope>): <subject>

[optional body]
```

**Types:** feat, fix, docs, style, refactor, perf, test, chore, ci, build

**Subject rules:**
- ≤50 chars
- Imperative mood ("add" not "added", "fix" not "fixes")
- Lowercase after the type
- No period at end

**Body rules:**
- Only include when the "why" isn't obvious from the subject
- Explain motivation, not the what
- Wrap at 72 chars

## Examples

```
fix(auth): handle token expiry edge case

refactor(db): extract connection pool to module

feat(api): add pagination to /users endpoint
Needed for clients with large user bases hitting timeout limits.
```

## Pattern

Look at staged diff. Identify the single most important change. One subject captures it. Skip praise, skip obvious. If it look good, say why it was done.
