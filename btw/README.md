# /btw — Ask Without Derailing

Ask a quick question mid-task. Get an answer. Task continues. Context untouched.

## The problem

Before `/btw`:

1. Cancel task
2. Ask question
3. Re-prompt original task
4. Lose all context

5 minutes gone. Focus shattered.

## The fix

```
/btw what file has the auth middleware?
```

```
src/middleware/auth.ts — wraps every protected route.

Back to it — finishing the checkout flow refactor now.
```

Answer in 3 seconds. Task continues. Context untouched.

## Usage

```
/btw <your question>
```

That's it. One command. The agent answers inline and resumes without missing a beat.

## Install

```bash
npx skills add missophs/skills -s btw
```
