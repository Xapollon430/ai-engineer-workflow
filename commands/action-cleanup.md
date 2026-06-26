---
description: List stale worktrees, merged branches, and abandoned spec/PRD files. Confirm before removing anything.
---

You are about to help the user tidy their repo. List candidates, get explicit confirmation, then remove. Do not delete anything without approval.

## 1. Inventory

### Worktrees

Run `git worktree list --porcelain`. For each worktree other than the main one:

- Path, branch, last commit on that branch, last filesystem modification of the worktree directory.
- Mark as **stale** if either:
  - The branch is merged into `main` (or `master`).
  - The worktree directory has not been modified in 14 days.

### Branches

Run `git branch --merged main` (or `--merged master`). List every branch other than the current branch and the default branch.

Squash-merged branches sometimes don't appear in `--merged`. If a worktree's branch is detected as stale above but doesn't appear here, trust the worktree detection.

### Spec / PRD files

Find any of:

- `spec.md` at the repo root
- `docs/specs/*.md`
- `prd.md` at the repo root
- `docs/prd-*.md`

For each, report:

- Last modified date.
- Whether a git branch with a matching slug exists.
- Mark **stale** if last modified > 30 days **and** no matching branch exists.

### Handoff file

Find `handoff.md` at the repo root or `docs/handoff.md`. Report last modified date. Mark **stale** if last modified > 3 days — handoffs are meant to be consumed by the next session, not kept around.

## 2. Present

Print one table with all candidates. Columns:

```
id  kind       name                                  why                          age
w1  worktree   ../myrepo-auth-rework                  branch merged into main      21d
w2  worktree   ../myrepo-experiment                   untouched in 14d             18d
b1  branch     old-experiment                        merged into main             8d
s1  spec       docs/specs/notifications.md           no matching branch           45d
```

If nothing is stale, say so in one line and stop.

## 3. Confirm

Ask the user which to remove. Accept any of:

- `all` — every row marked stale.
- A list of ids: `w1, b1, s1`.
- `none` — exit without changes.
- `skip <id>` — every stale row except the listed ones.

If the user types anything ambiguous, ask once for clarification. Do not guess.

## 4. Remove

For each confirmed item:

- **Worktree:** `git worktree remove <path>`. Do not use `--force` unless the user types it themselves.
- **Branch:** `git branch -d <name>`. Refuse `-D` unless the user explicitly requests it (it can drop unmerged work).
- **Spec / PRD file:** confirm with the user that the work it described actually shipped, then `rm <path>`. Do not auto-commit the removal — leave that to the user.
- **Handoff file:** `rm <path>`. No extra confirmation needed beyond the step 3 approval.

If a removal fails, report the failure verbatim and stop. Do not retry with stronger flags.

## 5. Report

Print:

- What was removed.
- What the user declined.
- Any remaining stale items the user can revisit later.

If `git worktree list` still shows phantom entries (deleted dirs git doesn't know about), suggest the user run `git worktree prune` themselves. Do not run it automatically.
