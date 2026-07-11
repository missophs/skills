---
name: fix-ticket-skill
description: >
  Fix a specific ticket, bug, or issue end-to-end. Use when user says "fix this ticket",
  "resolve this issue", "work this bug", or pastes a ticket/issue description and wants
  it fully addressed — diagnosed, implemented, and verified.
---

# Fix Ticket

Work a ticket from description to done. No half-measures.

## Process

1. **Understand the ticket** — restate what it's asking in one sentence. If ambiguous, ask one clarifying question before starting.

2. **Reproduce / locate** — find where in the code the problem lives. Read before writing.

3. **Root cause** — what's actually wrong, not just what's symptomatic.

4. **Fix** — smallest change that fully resolves the issue. Don't refactor adjacent code unless it's the cause.

5. **Verify** — confirm the fix works. Check for regressions in related paths.

6. **Done criteria** — the ticket is done when: the bug is gone, no new bugs introduced, and a reviewer could understand the change from the diff alone.

## Rules

- Don't expand scope. Fix what the ticket says.
- If the fix requires changes in 3+ unrelated areas, flag it — this may be a design issue, not a bug.
- Write the commit message to explain why, not what.
