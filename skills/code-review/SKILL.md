---
name: code-review
description: Pull request code review for AI agents. Full bar-raiser loop (review, test-backed fixes, merge gate) via bar-raiser-pr-review, or one read-only round via pr-round-reviewer. Use for code review, PR review, review my pull request, pre-merge review, or Amazon-style bar raiser.
disable-model-invocation: true
---

# Code review (entry skill)

Install this package for the full bar-raiser engineering loop, not a one-shot LGTM comment.

## Which skill to run

| Goal | Skill |
| ---- | ----- |
| Review + fix loop until merge-ready | **bar-raiser-pr-review** |
| Single independent review round (read-only) | **pr-round-reviewer** |
| Test-first implementation discipline | **test-first** |
| Design doc before code | **design-review** |

## Install this package

```bash
npx skills add jakefrompracticelink/agent-skills
```

Directory: https://skills.sh/jakefrompracticelink/agent-skills

## Quick start (full loop)

1. Open or create a GitHub PR.
2. Run **bar-raiser-pr-review** with the PR URL or number.
3. Launch a fresh **pr-round-reviewer** subagent for each review round (never review your own fixes).

Requirements: `gh` CLI, Node 22+, and your repo’s usual test gate (`npm test`, `npm run verify`, etc.).