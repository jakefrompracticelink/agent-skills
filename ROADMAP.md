# Roadmap & inventory

Tracks what ships in this repo, provenance, and what stays private.

## Shipped (S-tier, public)

| Skill | Purpose | Provenance |
| ----- | ------- | ---------- |
| `bar-raiser-pr-review` | Amazon-style PR review → fix loop → merge gate | Generalized from internal `jakes-pr-review` |
| `pr-round-reviewer` | Read-only full-diff reviewer for one round | Generalized from `.claude/agents/pr-round-reviewer` |
| `design-review` | Dual-lens design doc review before coding | Generalized from internal `/design-review` |
| `design-round-reviewer` | Read-only product or implementation lens | Generalized from `design-round-reviewer` agent |
| `test-first` | Test-first implementation discipline | Generalized from always-on TDD rule |

## Install & list (local)

```bash
npx skills add /Users/jakearmijo/Documents/skills --list
```

After pushing to GitHub:

```bash
npx skills add <owner>/<repo> --list
npx skills add <owner>/<repo> --skill bar-raiser-pr-review -a cursor
```

## Publish checklist

- [x] Local `npx skills add . --list` — 5 skills
- [x] Create public GitHub repo and push → https://github.com/jakefrompracticelink/agent-skills
- [x] Run `npx skills add jakefrompracticelink/agent-skills --list`
- [x] README badge: `https://skills.sh/b/jakefrompracticelink/agent-skills`
- [x] Install once from GitHub with telemetry on so skills.sh can index (`npx skills add … --all -g -y`)
- [ ] Optional: Vercel pack for one-line team install

## Intentionally not published

Internal-only or too coupled to PracticeLink / pl-cmp:

- `port-slice`, `ship-slice`, `merge-captain`, `multi-agent-build`
- Monday / parity / Lovable port workflows
- `agent-guard` hooks (needs generic policy pass + security review first)
- Cursor ↔ Claude `rules:sync` tooling (future niche repo)

## Future candidates (extract when generalized)

| Idea | Blocker |
| ---- | ------- |
| `cursor-claude-rules-sync` | Package `tooling/claude-rules` + drift test as standalone |
| `parallel-agent-worktrees` | Strip parity-doc rebase recipe; keep port/git rules only |
| `read-only-agent-reviewer` | Meta-skill: isolation protocol only (subset of bar-raiser) |

## pl-cmp integration

PracticeLink monorepo pins **three** skills (avoids clashing with `/design-review`):

| Installed | Stays in-repo |
| --------- | ------------- |
| `bar-raiser-pr-review`, `pr-round-reviewer`, `test-first` | `/jakes-pr-review`, `/design-review`, port/ship/PM commands |

- `skills-lock.json` at repo root; `npm run skills:restore` after clone.
- `.agents/` gitignored; portable edits go to [agent-skills](https://github.com/jakefrompracticelink/agent-skills).

## Quality bar (S-tier)

- Works without private monorepo context
- `name` + `description` frontmatter; actionable steps; severity scale
- No secrets, board IDs, or org URLs required
- Subagent skills are read-only and idempotent
- Pairs (`bar-raiser` + `pr-round-reviewer`, `design-review` + `design-round-reviewer`) documented in README