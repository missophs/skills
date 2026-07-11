---
name: premortem
description: >
  Run a pre-mortem on any plan, project, or decision. Imagine it has already failed
  and work backwards to find why. Use when user says "premortem", "what could go wrong",
  "failure modes", or wants to surface risks before committing.
---

# Pre-Mortem

Assume the plan has already failed. It's 6–12 months from now and things went badly wrong. Work backwards: what happened?

## How to run it

1. **Describe the failure** — paint a specific picture of what "it failed" looks like. Not vague — name the actual bad outcome.

2. **Root causes** — list everything that could have caused this failure. Go wide: people, process, technology, market, timing, dependencies, assumptions that didn't hold.

3. **Rank by likelihood × impact** — which causes are most dangerous?

4. **Preventive actions** — for each top-ranked cause, what specific action taken now would reduce the risk?

5. **Kill criteria** — what single signal, if observed early, should trigger stopping or pivoting?

## Rules

- Think in specifics, not categories. "The team was misaligned" is not a cause. "Engineering and product disagreed on the definition of done for feature X and it shipped broken" is.
- Surface the risks people are too polite to say out loud.
- Don't let optimism bias sneak back in. Stay in the failure mindset.
