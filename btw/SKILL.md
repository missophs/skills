---
name: btw
description: "Ask a quick question mid-task without derailing. Say /btw <question> to get an answer inline, then continue exactly where you left off."
---

# BTW — Ask Without Derailing

You just received a `/btw` query. This is a quick inline question, not a new task.

## What to do

1. **Answer the question only.** One short, direct answer. No preamble.
2. **Resume immediately.** After answering, say "Back to it —" and continue the active task from exactly where it was interrupted.
3. **Do not lose context.** The task in progress is unchanged. The `/btw` answer is a parenthetical, not a pivot.

## Format

```
[answer to btw question]

Back to it — [continue task]
```

## Rules

- Answer is ≤3 sentences. If it genuinely needs more, give the short version and offer to elaborate after the task.
- Never ask the user to re-explain the current task. You already know it.
- Never treat `/btw` as permission to stop, summarize, or check in about the task.
- If the question is actually complex enough to require its own session, say so in one sentence and offer to park it for after.

## Example

> /btw what file has the auth middleware?

```
src/middleware/auth.ts — wraps every protected route.

Back to it — finishing the checkout flow refactor now.
```
