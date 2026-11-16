# Contributing

Thanks for helping improve agent skills other teams can trust.

## What belongs here

- **Portable** procedural knowledge (review rubrics, loops, read-only reviewer briefs).
- No company-specific IDs, private URLs, or monorepo-only commands.
- Skills must pass `npx skills add . --list` from the repo root.

## What stays out

- Internal parity / PM / board automation (keep in your private repo).
- Hooks or scripts that execute network calls without user visibility unless documented.

## Change process

1. Edit `skills/<name>/SKILL.md` (keep `name` stable unless renaming intentionally).
2. Run `npx skills add . --list` locally.
3. Add a `CHANGELOG.md` entry under `[Unreleased]` or a dated version.
4. Open a PR; keep one concern per commit when possible.

## Syncing from a private fork

When your internal skill (e.g. `jakes-pr-review`) gains a **generic** improvement:

1. Port the change into the matching public skill (`bar-raiser-pr-review` or `pr-round-reviewer`).
2. Drop org-specific branches, board IDs, and assignee names.
3. Bump `CHANGELOG.md` and tag if you use semver on releases.

## Skill quality bar

- YAML `name` + `description` (discovery and install).
- Actionable steps, explicit severities, read-only vs orchestrator split.
- Subagent skills must not edit, commit, push, or post.