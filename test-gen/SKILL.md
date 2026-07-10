---
name: test-gen
description: >
  Generate unit and integration tests for a given function, module, or API endpoint.
  Covers happy path, edge cases, and error paths. Use when adding tests to existing
  code or writing tests alongside new code.
---

Generate thorough tests for the target code. Cover happy path, edge cases, and error paths.

## Test structure

Use the AAA pattern: **Arrange → Act → Assert**. One assertion per test where possible. No logic in tests (no loops, no conditionals).

## Coverage targets

For every function/method, generate:

1. **Happy path** — typical valid input, expected output.
2. **Boundary values** — empty string, zero, max int, null/undefined, empty array.
3. **Invalid input** — wrong type, out-of-range, malformed data.
4. **Error paths** — what throws/rejects and with what message.
5. **Side effects** — DB writes, external calls, state mutations (use mocks/spies).

## Framework detection

Detect from imports/config:
- JS/TS: Jest, Vitest, Mocha — use `describe/it/expect`
- Python: pytest — use `test_` functions, `assert`, fixtures
- Go: `testing` package — `TestXxx(t *testing.T)`
- Ruby: RSpec — `describe/it/expect`

Match the project's existing test style exactly. Don't mix frameworks.

## Mocking rules

- Mock at the boundary: HTTP clients, DB connections, file system, time/random.
- Never mock the code under test.
- Use `jest.spyOn` / `unittest.mock.patch` / `gomock` as appropriate.
- Assert mock was called with correct args, not just called.

## Naming convention

```
<function>_<scenario>_<expected>
# examples:
getUserById_validId_returnsUser
getUserById_notFound_throwsNotFoundError
getUserById_dbError_propagatesError
```

## Output

Generate complete, runnable test file. Include necessary imports. Add a brief comment above each test group explaining what's being tested and why the cases matter.
