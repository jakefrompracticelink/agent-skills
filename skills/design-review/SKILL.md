---
name: design-review
description: Dual independent design doc review before coding — one product lens and one implementation lens via fresh read-only subagents. Synthesizes DR findings and updates the design's review section. Use before starting a feature, RFC, or slice implementation.
disable-model-invocation: true
---

# Design review — before code

Arguments: path to a design doc (e.g. `docs/designs/2026-feature-x.md`).

Run after the design exists and before implementation. Required when the change touches auth, schema, new dependencies, or unresolved product decisions.

## Steps

1. Read the design path. If missing, stop.
2. Read every file path listed in the design (files, APIs, schema, tests).
3. Launch **two** fresh **`design-round-reviewer`** subagents:
   - **Brief A:** Design path, Repo root (absolute), `Focus: product`
   - **Brief B:** same, `Focus: implementation`
4. If subagents are unavailable, run each lens in a **new chat** with only the design and cited files — not the author chat that wrote the design.
5. Synthesize findings `DR1`, `DR2`, … with severity Critical / Important / Suggestion.
6. Update the design doc **Design review** section: date, two reviewers, finding IDs addressed or deferred.
7. **STOP** if Critical/Important lack user approval or design edits. Do not start coding until fixed or explicitly deferred in the design with rationale.

## Who reviews

The agent that **authored** the design must **not** run as reviewer. Same isolation pattern as `bar-raiser-pr-review` / `pr-round-reviewer`.

## Design doc template (recommended sections)

```markdown
# Title

Status: draft | approved

## Problem
## Goals / non-goals
## Proposed solution
## Files
## APIs / data
## Tests
## Open questions
## Design review
(last run, findings, deferrals)
```

No commits unless the user asks. Prefer editing only the design review section unless findings require plan changes.