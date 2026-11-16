# Agent skills — bar raiser engineering

Reusable [Agent Skills](https://skills.sh/) for teams that want **independent agent review**, **test-first fixes**, and **design review before code** — without a proprietary monorepo harness.

Inspired by Amazon-style bar-raiser reviews and battle-tested on large TypeScript/Python repos. Skills work in **Cursor**, **Claude Code**, and other agents that support `SKILL.md`.

## Install

Requires Node.js 22+ and [GitHub CLI](https://cli.github.com/) (`gh`) for PR skills.

```bash
# Browse what will install (no write)
npx skills add jakefrompracticelink/agent-skills --list

# Install everything into the current project
npx skills add jakefrompracticelink/agent-skills

# Pick one skill and target Cursor
npx skills add jakefrompracticelink/agent-skills --skill bar-raiser-pr-review -a cursor
```

Local development (this checkout):

```bash
npx skills add /Users/jakearmijo/Documents/skills --list
```

[![skills.sh](https://skills.sh/b/jakefrompracticelink/agent-skills)](https://skills.sh/jakefrompracticelink/agent-skills)

## Skills

| Skill | When to use |
| ----- | ----------- |
| **bar-raiser-pr-review** | Full PR lifecycle: bar-raiser review → one-finding-one-commit fixes → full-diff re-review → adversarial merge gate |
| **pr-round-reviewer** | Launch a **fresh read-only** reviewer for one round (or merge gate); never review your own fixes |
| **design-review** | Before implementation: two independent passes (product + implementation) on a design doc |
| **design-round-reviewer** | Single read-only design review with product or implementation lens |
| **test-first** | Implement features and bugs test-first; assert behavior, not structure |

### Pairs

- **PR:** Run `bar-raiser-pr-review` in the orchestrator; launch **`pr-round-reviewer`** for each review round.
- **Design:** Run `design-review`; launch two **`design-round-reviewer`** subagents (product + implementation).

## Configure your repo

Set these in chat or in your `AGENTS.md` / `CONTRIBUTING.md` so skills pick them up:

| Variable | Typical value |
| -------- | ------------- |
| Default base branch | `main` or `develop` |
| Local quality gate | `npm run verify`, `npm test`, `make check`, etc. |
| Commit style | Conventional Commits / project standard |

`bar-raiser-pr-review` asks for the base branch if the PR's `baseRefName` does not match your stated default.

## Author

Jake Armijo — [skills.sh](https://skills.sh/) distribution via install telemetry. MIT license.

See [ROADMAP.md](./ROADMAP.md) for inventory, publish checklist, and what we keep internal.