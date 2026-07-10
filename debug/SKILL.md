---
name: debug
description: >
  Systematic debugging workflow. Given an error, stack trace, or unexpected behavior,
  diagnose root cause and produce a targeted fix. Use when something is broken and you
  need a structured investigation rather than a guess.
---

Diagnose root cause. Produce minimal targeted fix. No speculative changes.

## Process

1. **Reproduce** — confirm the exact failure: error message, stack trace, inputs, environment.
2. **Isolate** — narrow to the smallest failing unit. Identify which call/line/condition triggers it.
3. **Hypothesize** — list 1-3 candidate causes ranked by likelihood. Eliminate with evidence.
4. **Fix** — change only what the root cause requires. No opportunistic cleanup.
5. **Verify** — state what test/run confirms the fix without reintroducing the bug.

## Output format

```
ROOT CAUSE: <one sentence>
FIX: <minimal code change>
VERIFY: <how to confirm it's fixed>
```

## Rules

- Quote the exact error line. Never paraphrase error text.
- If stack trace present, read from bottom up — find caller, not the crash site.
- If multiple hypotheses: state confidence. Prefer simplest explanation (Occam).
- Never add unrelated changes to a bug fix. If you see other issues, mention separately.
- If fix requires data migration or config change, call it out explicitly.
- For flaky/intermittent bugs: identify the race condition or timing dependency first.

## Common patterns

**TypeError/AttributeError** → check None/undefined propagation up the call chain.
**Off-by-one** → look at loop bounds, slice indices, pagination math.
**Auth/403** → check token expiry, scope, middleware order.
**Race condition** → look for shared mutable state across async paths.
**Import/module error** → check install, version pin, circular imports.
**Env-only bug** → diff env vars, secrets, config files between working and broken env.
