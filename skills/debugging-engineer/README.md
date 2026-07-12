# debugging-engineer

A skill that turns your AI coding agent into a senior production debugging engineer.

When you invoke `/debugging-engineer`, the agent stops guessing and starts investigating — tracing real execution paths, identifying root causes, surfacing edge cases you haven't thought of yet, and delivering fixes that hold under production load.

---

## What it does

Given any piece of code or bug report, the agent produces five structured sections:

1. **Code Functionality Breakdown** — what the code actually does (not what it was meant to do)
2. **Root Cause Analysis** — the precise failure mechanism and why it's reachable in production
3. **Failure Explanation** — a plain-language account of the bug that any developer can follow
4. **Edge Case Analysis** — every failure mode the code is exposed to, ranked by severity
5. **Fixed Production-Ready Code** — a complete, runnable fix (not a diff, not pseudocode)

---

## When to use it

- You have a production bug and need to know *why*, not just what line to change
- A piece of code is behaving unexpectedly and you can't figure out why
- You're reviewing code and want a senior engineer's eye on failure modes
- You need a fix that won't just paper over the symptom

---

## How to activate

**Slash command:**
```
/debugging-engineer
```
Then paste the code and describe the failure.

**Natural language:**
> "Debug this as a senior debugging engineer" / "root cause analysis" / "production issue investigation"

---

## Example

**Input:**
```python
def get_user_discount(user_id):
    user = db.query(f"SELECT * FROM users WHERE id = {user_id}")
    if user['premium']:
        return 0.20
    return 0.0
```
*"This is returning wrong discounts in production intermittently."*

**Output includes:**
- Breakdown: SQL injection via f-string, no null check on query result, dict access on potentially None
- Root cause: `db.query()` returns `None` when no row found; `None['premium']` raises `TypeError`
- Why intermittent: only triggers for user IDs that don't exist in DB (deleted accounts, invalid input)
- Edge cases: SQL injection, concurrent deletes between query and access, missing `premium` column in older rows
- Fix: parameterized query, null guard, `.get()` with default, proper error handling

---

## Install

```bash
npx skills add missophs/skills --skill debugging-engineer
```

Or add to your agent's skill directory manually.
