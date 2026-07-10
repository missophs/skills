---
name: sql
description: >
  Write, review, and optimize SQL queries. Covers SELECT, INSERT, UPDATE, DELETE, JOINs,
  aggregations, indexes, query plans, and schema design. Use when writing queries,
  diagnosing slow queries, or designing tables.
---

Write correct, performant SQL. State dialect (PostgreSQL, MySQL, SQLite, MSSQL) if known.

## Query writing rules

- Use explicit column lists in SELECT. Never `SELECT *` in production code.
- Table aliases must be meaningful (not just `a`, `b`): `u` for users, `o` for orders.
- Always include WHERE on UPDATE/DELETE. Flag if missing.
- Use parameterized queries for any user-supplied value — never string interpolation.
- Use CTEs (`WITH`) to break complex queries into readable named steps.
- Prefer JOINs over subqueries for performance (optimizer handles JOINs better).
- Use `EXISTS` over `COUNT(*)` for presence checks.

## Performance checklist

- Index columns used in WHERE, JOIN ON, and ORDER BY.
- Avoid functions on indexed columns in WHERE (blocks index use): `WHERE YEAR(created_at) = 2024` → `WHERE created_at >= '2024-01-01' AND created_at < '2025-01-01'`
- Watch for N+1: if the query is inside a loop, rewrite as a single JOIN or batch fetch.
- For pagination, use keyset pagination (`WHERE id > :last_id LIMIT n`) over OFFSET for large tables.
- Use `EXPLAIN ANALYZE` (Postgres) / `EXPLAIN` (MySQL) to confirm index usage. Include output when diagnosing slow queries.

## Schema design rules

- Primary keys: use surrogate integer/UUID. Composite PKs only when the pair is a natural key.
- Foreign keys: always add indexes on FK columns.
- Soft deletes: add `deleted_at TIMESTAMP NULL` + partial index `WHERE deleted_at IS NULL`.
- Timestamps: `created_at`, `updated_at` on every table. Use `DEFAULT NOW()`.
- Booleans: use `BOOLEAN NOT NULL DEFAULT FALSE`. Avoid NULLable booleans (three-valued logic is a trap).
- Enums: prefer a lookup table over DB-level ENUM if values may change.

## Output format

For a query request:
```sql
-- Explanation of what this query does
SELECT ...
```

For a slow query diagnosis:
```
ISSUE: <what's slow and why>
FIX: <index to add or query rewrite>
BEFORE: <original>
AFTER: <optimized>
```
