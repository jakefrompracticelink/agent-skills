---
name: test-first
description: Implement features and bug fixes test-first. Derive tests from requested behavior, confirm failure before production changes, assert observable outcomes not internals. Use when implementing features, fixing bugs, or when the user asks for TDD or test-first workflow.
---

# Test-first

Apply on every feature and bug fix unless the user explicitly opts out for a trivial change.

## Protocol

1. Name the behavior the request implies, including failure and edge cases.
2. Add a **failing** test for that behavior **before** production code changes.
3. Run the test; confirm it fails for the right reason (missing behavior, not a typo).
4. Write the **minimum** production code to pass.
5. Re-run; the test passes and would fail if the behavior were removed.

## Bug fixes

Start with a test that **fails on current code** and passes once the bug is fixed.

## What to assert

Observable outcomes:

- Return values and parsed errors
- HTTP status, redirects, response bodies (at boundaries)
- User-visible UI text or state (when testing UI)

Do **not** assert:

- Private helpers, call counts, or file layout
- Implementation details that do not affect behavior

## Test runner

Use what the package already uses:

| Stack | Typical |
| ----- | ------- |
| TypeScript / JS | Vitest, Jest, node:test colocated `*.test.ts` |
| Python | pytest next to modules or `tests/` |
| Go | `*_test.go` |
| Rust | `#[cfg(test)]` modules |

If unknown, search `package.json`, `pyproject.toml`, or CI config before adding tests.

## When tests are awkward

Still add one if possible. If truly impossible (e.g. pure config), state on the PR **what manual check** replaces the test — do not skip silently.

## Agent discipline

- Do not mark work done without running the relevant tests plus the repo's usual gate (`npm test`, `make check`, etc.) when the user or repo expects it.
- One behavior concern per commit when pairing with bar-raiser PR review.