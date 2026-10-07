# Good first issues

A small, curated list of verified starter tasks for new contributors. Every item below has been confirmed against the current code and test suite — pick one, optionally pair with the `guide-me` skill, and open a PR.

> This list is intentionally small and **verified**. Do not add an item unless you have confirmed the gap exists in the code or tests. If you want something else, open an issue or ask in the issue tracker.

## 1. Export `BulkheadSnapshot` from the public entry point

Tracked in [#138](https://github.com/riosgabriel/vereda/issues/138).

`HttpClient.partitions()` (`src/core/client.ts`) returns `BulkheadSnapshot[]`, but `BulkheadSnapshot` is defined in `src/queue/bulkhead.ts` and never re-exported from `src/core/index.ts`. A consumer can call `client.partitions()` but cannot import the type of what it returns to, say, write a function signature that accepts it — `npm run docs` (TypeDoc) even warns about this: `BulkheadSnapshot ... is referenced by core.HttpClient.partitions but not included in the documentation`.

**Fix:** re-export `BulkheadSnapshot` (as a type) from `src/core/index.ts`, alongside the other exported types. Consider whether to keep the name or rename it to `PartitionSnapshot` for clarity — either is a fine, backwards-compatible addition (adding an export is never a breaking change).

