---
name: refactor
description: >
  Safe, incremental code refactoring. Improves structure, readability, and maintainability
  without changing behavior. Use when code is hard to understand, duplicated, or needs
  restructuring before adding features.
---

Refactor for clarity and maintainability. Behavior must not change. No feature additions.

## Principles

- **Behavior-preserving first.** Every refactor step must leave tests passing (or be clearly marked as requiring test updates).
- **One change at a time.** Rename → extract → move → simplify. Not all at once.
- **Smallest safe unit.** Prefer many small commits over one large rewrite.
- **Don't fix what isn't broken.** Only touch code in scope. Note other issues separately.

## Common refactoring moves

### Extract function/method
When: logic is repeated, or a block is too long to scan.
How: identify inputs/outputs → name the function by its purpose (verb + noun) → replace original with call.

### Rename for clarity
When: name doesn't match what the thing does.
Rule: names describe intent, not implementation. `process()` → `validateAndEnqueueOrder()`.

### Remove duplication (DRY)
When: same logic in 3+ places.
How: extract to shared helper. Don't abstract 2 similar things — wait for the third.

### Flatten nesting
When: more than 3 levels of indent.
How: early returns (guard clauses), extract inner blocks to functions.

### Split large file/class
When: a module does two unrelated things.
How: identify seam → move one concern to new file → update imports.

### Simplify conditionals
When: boolean logic is hard to parse.
How: extract named predicates, use guard clauses, eliminate double negatives.

## Output format

For each change:
```
MOVE: <what> → <where/why>
BEFORE: <original snippet>
AFTER: <refactored snippet>
```

End with: "Tests affected: none / <list files that need updating>"
