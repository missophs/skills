---
name: perf
description: >
  Profile and optimize code performance. Identify bottlenecks, reduce latency,
  cut memory usage, and improve throughput. Use when code is too slow, uses too
  much memory, or needs to handle more load.
---

Find the bottleneck. Fix it. Measure before and after. No premature optimization.

## Process

1. **Measure first.** Never optimize without a benchmark or profile. State the current metric (ms, MB, req/s).
2. **Find the bottleneck.** 80% of time is spent in 20% of code. Profile before guessing.
3. **Fix the algorithm before tuning constants.** O(n²) → O(n log n) beats any micro-optimization.
4. **Measure after.** Confirm the fix actually improved the metric. Optimization that doesn't move the number is wasted.

## Profiling tools by language

- **Node.js**: `--prof`, Chrome DevTools, `clinic.js`, `0x`
- **Python**: `cProfile`, `py-spy`, `memray` (memory)
- **Go**: `go tool pprof`, `runtime/trace`
- **Browser JS**: Chrome Performance tab, Lighthouse, Web Vitals
- **Database**: `EXPLAIN ANALYZE`, slow query log, `pg_stat_statements`

## Common bottlenecks and fixes

### CPU
- **N+1 loops** → batch/JOIN
- **Repeated computation** → cache/memoize
- **O(n²) search** → use hash map/set
- **String concatenation in loop** → use array + join or StringBuilder

### Memory
- **Accumulating large arrays** → stream/process in chunks
- **Retaining references** → check for unintended closures, global caches without eviction
- **Large JSON parse** → streaming JSON parser

### I/O
- **Sequential async calls** → `Promise.all` / gather / goroutines
- **Missing connection pool** → add pool, tune pool size
- **No caching** → add cache layer (Redis, in-memory LRU) for expensive reads
- **Large payloads** → add compression (gzip/brotli), paginate responses

### Web / frontend
- **Render blocking resources** → defer/async scripts, preload critical CSS
- **Unoptimized images** → WebP, lazy load, proper sizing
- **Large bundle** → code splitting, tree shaking, dynamic import
- **Layout thrashing** → batch DOM reads and writes

## Output format

```
BOTTLENECK: <what's slow, measured>
ROOT CAUSE: <why>
FIX: <change to make>
EXPECTED GAIN: <rough estimate or "measure to confirm">
```
