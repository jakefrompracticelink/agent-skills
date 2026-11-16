# agent-skills

**Bar-raiser engineering for coding agents** — not another one-shot “LGTM” review.

**On [skills.sh](https://skills.sh/jakefrompracticelink/agent-skills)** — installs are counted anonymously; each `npx skills add` helps the package show up on the [leaderboard](https://skills.sh/). If this helped you, run the install command once and star the repo.

[![skills.sh](https://img.shields.io/badge/skills.sh-5_agent_skills-111111)](https://skills.sh/jakefrompracticelink/agent-skills)
[![License: MIT](https://img.shields.io/github/license/jakefrompracticelink/agent-skills)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/jakefrompracticelink/agent-skills)](https://github.com/jakefrompracticelink/agent-skills/stargazers)

Reusable [Agent Skills](https://skills.sh/) built from production workflows on large TypeScript/Python codebases: **independent reviewer subagents**, **test-first fix loops**, **full-diff re-review**, and an adversarial **merge gate** (G-1–G-7). Works in **Cursor**, **Claude Code**, Codex, and [70+ agents](https://github.com/vercel-labs/skills) via the skills CLI.

**Install (one line):**

```bash
npx skills add jakefrompracticelink/agent-skills
```

Browse without installing:

```bash
npx skills add jakefrompracticelink/agent-skills --list
```

Install one skill into Cursor:

```bash
npx skills add jakefrompracticelink/agent-skills --skill bar-raiser-pr-review -a cursor -y
```

Directory page: **https://skills.sh/jakefrompracticelink/agent-skills**

## Why these skills

| Typical “code review” skill | This package |
| --------------------------- | ------------ |
| Posts comments | **Fix loop** — one finding, one commit, one test |
| Same agent reviews its own fixes | **Fresh read-only** `pr-round-reviewer` every round |
| Reviews only the latest diff | **Full-diff** re-review after every fix |
| “Looks good” before merge | **Merge gate** — adversarial checklist at PR head |

Inspired by Amazon bar-raiser culture; generalized for any GitHub + `gh` workflow.

## Skills

| Skill | When to use |
| ----- | ----------- |
| **code-review** | Entry skill — routes to the right PR review skill (search-friendly) |
| **bar-raiser-pr-review** | Orchestrator: review → fix → loop → merge gate |
| **pr-round-reviewer** | One read-only review round (launch as subagent) |
| **design-review** | Dual-lens design doc review before implementation |
| **design-round-reviewer** | Single product or implementation design pass |
| **test-first** | Test-first features and bug fixes |

**Pairs:** `bar-raiser-pr-review` + `pr-round-reviewer` for PRs; `design-review` + two `design-round-reviewer` runs for designs.

## Requirements

- Node.js **22+** (skills CLI)
- **[GitHub CLI](https://cli.github.com/)** (`gh`) for PR skills
- Optional: subagent support in your agent for true reviewer isolation

Configure default base branch and your quality gate (`npm test`, `npm run verify`, etc.) in `AGENTS.md` or chat.

## Author

**Jake Armijo** ([@jakefrompracticelink](https://github.com/jakefrompracticelink)) — PracticeLink engineering.

If this saves you a bad merge, [★ star the repo](https://github.com/jakefrompracticelink/agent-skills/stargazers) so others find it.

## Share (copy/paste)

> **Bar-raiser engineering for coding agents** — not another one-shot “LGTM” review.  
> Independent reviewer subagents · test-first fix loop · full-diff re-review · adversarial merge gate (G-1–G-7).  
> `npx skills add jakefrompracticelink/agent-skills`  
> https://skills.sh/jakefrompracticelink/agent-skills

[CHANGELOG](./CHANGELOG.md) · [CONTRIBUTING](./CONTRIBUTING.md) · [ROADMAP](./ROADMAP.md)