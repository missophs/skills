---
name: explain
description: >
  Explain code in plain English. Describe what it does, how it works, and why it's written
  that way. Use when you need to understand unfamiliar code, onboard into a codebase,
  or prepare to explain code in a PR review or documentation.
---

Explain this code clearly. Assume the reader is a competent developer who doesn't know this specific codebase.

## Explanation structure

1. **Purpose** — one sentence: what problem does this code solve?
2. **How it works** — step-by-step walkthrough of the logic flow.
3. **Key decisions** — why is it written this way? What tradeoffs were made?
4. **Inputs/outputs** — what goes in, what comes out, what side effects occur.
5. **Gotchas** — non-obvious behavior, edge cases, known limitations.

## Rules

- Use analogies for complex concepts — but only if they aid understanding, not to show off.
- Name the pattern if one applies (e.g. "this is a factory function", "this implements the observer pattern").
- Don't just restate the code in English. Add meaning: why each piece exists.
- If the code does something surprising or fragile, flag it.
- Keep technical terms accurate. Don't oversimplify into incorrectness.
- If the code is bad: say so, and why, separately from the explanation.

## Depth levels

Adapt based on context clues:
- Short function → concise 3-5 sentence explanation
- Complex algorithm → numbered walkthrough with inline examples
- Full module/file → overview + per-section breakdown

## Example output shape

```
PURPOSE: Validates and parses incoming webhook payloads from Stripe.

HOW IT WORKS:
1. Reads raw body from request (before JSON parsing — required by Stripe's signature check)
2. Verifies HMAC-SHA256 signature using STRIPE_WEBHOOK_SECRET
3. Parses JSON only after signature passes
4. Routes to handler based on event.type

KEY DECISION: Raw body required because JSON.parse would reformat whitespace, breaking the HMAC.

GOTCHA: If you add body-parser middleware before this route, signature verification breaks.
```
