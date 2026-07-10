---
name: docs
description: >
  Generate inline documentation, docstrings, JSDoc, and README sections.
  Use when adding docs to existing code, preparing a module for public API,
  or documenting a function before handing it off.
---

Generate accurate, concise documentation. Describe behavior, not implementation.

## Docstring format by language

### Python (Google style)
```python
def func(arg: str) -> int:
    """One-line summary.

    Args:
        arg: Description of the parameter.

    Returns:
        Description of the return value.

    Raises:
        ValueError: When arg is empty.
    """
```

### TypeScript/JavaScript (JSDoc)
```ts
/**
 * One-line summary.
 *
 * @param arg - Description of the parameter.
 * @returns Description of the return value.
 * @throws {Error} When arg is invalid.
 * @example
 * const result = func('hello'); // 5
 */
```

### Go
```go
// FuncName does X. It returns Y given Z.
// Returns error when W.
func FuncName(arg string) (int, error) {
```

### Rust
```rust
/// One-line summary.
///
/// # Arguments
/// * `arg` - Description
///
/// # Returns
/// Description of return value.
///
/// # Errors
/// Returns `Err` when condition.
///
/// # Examples
/// ```
/// let result = func("hello");
/// assert_eq!(result, 5);
/// ```
```

## Writing rules

- First line: one sentence, imperative mood ("Validates", "Returns", "Fetches").
- Document the contract, not the code. What goes in, what comes out, what fails.
- Include an `@example` / doctest for non-obvious usage.
- Document all parameters — especially optionals and their defaults.
- Document error conditions explicitly: what throws, what returns null, what returns empty.
- Don't restate the function name: `// GetUser gets the user` → useless.
- Don't describe HOW it works internally — only WHAT it does from the caller's view.

## README section format

For a function/module README section:
```markdown
### `functionName(arg, options?)`

One-sentence description.

**Parameters**
- `arg` (string) — what it is
- `options.timeout` (number, default: 5000) — ms before request aborts

**Returns** `Promise<Result>` — description.

**Throws** `AuthError` — when token is invalid.

**Example**
\`\`\`ts
const result = await functionName('input', { timeout: 3000 });
\`\`\`
```
