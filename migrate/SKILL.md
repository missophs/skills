---
name: migrate
description: >
  Plan and execute code migrations. Covers library upgrades, API version changes,
  language version upgrades, database schema migrations, and framework switches.
  Use when upgrading dependencies, modernizing code, or moving between platforms.
---

Plan the migration. Execute in safe, reversible steps. Verify at each step.

## Migration planning

Before touching code, produce a migration plan:

1. **Scope** — what's changing? List all affected files/modules.
2. **Risk** — what breaks silently? What has no type-checking coverage?
3. **Order** — which changes must come first (deps before callers)?
4. **Rollback** — how to revert each step if it fails?
5. **Verification** — how to confirm each step succeeded?

## Safe migration steps

### Dependency/library upgrade
1. Read the changelog for breaking changes between current and target version.
2. Update version in lock file. Run tests immediately.
3. Fix one error at a time. Don't batch unrelated fixes.
4. Search for deprecated API usage: `grep` for removed method names.
5. Update all call sites before removing compatibility shims.

### API version migration (v1 → v2)
1. Identify all call sites of the old API.
2. Add v2 alongside v1 (parallel run) — don't delete v1 yet.
3. Migrate call sites one by one. Test after each.
4. Once all call sites migrated, delete v1.
5. Never leave dead code — remove the old version completely.

### Database schema migration
1. Write migration as: additive first (add new column/table), then migrate data, then remove old.
2. New column: nullable or with default — never NOT NULL without default on existing table with rows.
3. Rename: add new column, dual-write, backfill, flip reads, remove old. Never rename directly.
4. Large tables: run migration in batches with `WHERE id > :cursor LIMIT 1000`. Avoid locking.
5. Every migration must be reversible: write both `up` and `down`.

### Language version upgrade (e.g., Python 3.9 → 3.12, Node 18 → 22)
1. Run official migration tool first: `2to3`, `pyupgrade`, `node --check`.
2. Fix type errors surfaced by stricter version.
3. Check deprecated stdlib usage — search for removed modules.
4. Update CI matrix to test on new version before dropping old.

## Output format

```
MIGRATION PLAN: <description>

Step 1: <action> — affects <files> — rollback: <how>
Step 2: <action> — affects <files> — rollback: <how>
...

RISKS:
- <risk> → <mitigation>

VERIFICATION: <how to confirm migration succeeded>
```

Then execute each step, showing before/after for changed code.
