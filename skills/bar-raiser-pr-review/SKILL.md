---
name: bar-raiser-pr-review
description: Code review and pull request bar-raiser loop for AI agents. Independent read-only reviewer, test-first fixes, full-diff re-review, adversarial merge gate (G-1–G-7). Use for code review, PR review, bar-raiser review, pre-merge review, review-and-fix until green, or Amazon-style PR review (not review-only).
disable-model-invocation: true
---

# Bar-raiser PR review — review, fix, loop until green

Invocation: PR URL, PR number, or branch name (no argument → PR for current branch).

This skill always runs **both** halves:

1. **Review** like an Amazon bar raiser (via a fresh `pr-round-reviewer`).
2. **Fix loop** until exit criteria, including a **merge gate** at the current head SHA.

Do not stop after posting a review. The review feeds the fix loop.

Install **`pr-round-reviewer`** from the same skill package and launch it for every review round.

## Ground rules

- **Base branch:** Confirm the PR's `baseRefName` matches the team's default (ask if unset; commonly `main` or `develop`). Stop if the PR targets an unexpected base unless the user overrides.
- Obey repo rules first (`AGENTS.md`, `CONTRIBUTING.md`, lint/type/test gates). Never weaken types, lint, or config to pass.
- Never merge, force-push, or rewrite published history. Never run destructive DB/migration commands unless the user explicitly runs them.
- **One finding = one commit.** Stage only files for that finding.
- Every behavior fix includes a test that would have failed before the fix (or explain on the PR why not).
- Fix **Critical**, **Important**, and **Suggestion** unless the user explicitly defers a specific item on the PR. Product/design blockers → stop and ask.
- Ambiguous safety (auth, payments, PII) → fail closed, not permissive.
- No markdown recap files — chat and PR only.
- Cap **5** review→fix iterations; then stop and report blockers.
- **Merge gate required** before "green and good to go." A round-3 Approve is voided by any later commit until a new merge gate at that head.
- Do not urge merge until exit criteria pass.

## Who reviews and who fixes

- **You** orchestrate, post reviews, implement fixes, push, run the local gate.
- **Fresh `pr-round-reviewer`** runs Phase 1–2 of that skill for each round — never you, never the same subagent instance, never the agent that wrote the fixes.
- **Push before each reviewer launch.** Head = `headRefOid` after push.
- **Void round** if head or checkout dirtiness changes between launch and return.
- **Fallback:** If no independent subagent is available, stop and post that rounds need an independent reviewer — do not self-review fixes.

### Launch brief (pr-round-reviewer)

```
Repo: owner/name
PR: <number>
Round: 1 | 2 | 3
Head: <sha>
Main checkout: <absolute path>
Worktree: <path> | none
Merge gate: true | (omit)
Base branch: main
```

## Phase 1 — Load the PR (orchestrator)

- Parse input; if no PR, ask user to open one — do not open unasked
- Confirm base branch
- `gh pr view` metadata and existing threads
- Fetch and check out head branch (`git fetch`, `pull --ff-only`)
- `git fetch origin <base>`
- `gh pr diff` — full diff
- `git diff --merge-base origin/<base> --stat`; flag if far behind base
- Read every changed file in full; read project review docs
- `gh pr checks`

Todo list: one item per review dimension + one per changed file.

## Phase 2 — First review

Launch fresh **`pr-round-reviewer`** (round 2 if author already did a local round 1; else see round counting below). Post its output in Phase 3.

## Phase 3 — Post the review

- **Request changes:** `gh pr review <n> --request-changes --body-file <f>`
- **Approve / Approve with comments:** `gh pr review <n> --comment --body-file <f>` with verdict line **Approve** (use comment mode when you cannot approve your own PR)
- Prefix posted body with round line from reviewer output
- Verify the comment landed before fixes

## Phase 4 — Fix loop

```
LOOP:
  1. Triage findings (ID, severity, file, fix, test)
  2. For each finding (Critical → Important → Suggestion):
     - Failing test first → minimal fix → local quality gate (e.g. npm run verify)
     - One commit per finding; reference ID in message
  3. Push to PR head branch (hooks must pass)
  4. PR comment: finding ID → commit SHA → test
  5. CI green: gh pr checks
  6. RE-REVIEW: fresh pr-round-reviewer on ENTIRE diff (never fix-only)
  7. MERGE GATE: fresh pr-round-reviewer, Round 3 + Merge gate true,
     preferably different model than step 6
UNTIL exit criteria OR 5 iterations OR human decision
```

**Round counting (record on PR):**

- Prefer three **full-diff** agent rounds before human merge (author round 1 optional).
- Final round uses adversarial lens (round 3 / merge gate checklist).
- Critical/Important in a round → restart round-2 counting after fixes.
- CI-only commits tagged `(CI fix <check>)` are not a review round.

**Merge gate (step 7):** New reviewer, `Merge gate: true`, post with merge-gate first line. Any Critical/Important → back to step 1.

## Exit criteria — "green and good to go"

- [ ] Merge gate **Approve** at current `headRefOid` with complete G-checklist
- [ ] No commits after merge-gate SHA
- [ ] Latest full-diff re-review: zero Critical/Important
- [ ] Three full-diff reviewer rounds recorded OR documented exception
- [ ] No round run by the fixer agent
- [ ] Local quality gate green; CI green; mergeable with base
- [ ] Final PR comment: verdict, findings→commits, deferrals

## Final chat report

PR link, verdict, iteration count, **merge gate SHA**, findings table, CI and local gate result, deferrals/blockers, explicit "not merged" unless user asked to merge (then re-check head SHA).