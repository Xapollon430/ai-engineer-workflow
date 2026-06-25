---
description: Pick up the most recent spec or PRD and drive implementation in an isolated git worktree.
---

You are about to implement a written spec. Work in a fresh git worktree so the user's main checkout stays clean.

## 1. Find the spec

Look for, in order:

- `spec.md` at the repo root.
- The newest file under `docs/specs/`.
- `prd.md` at the repo root, or the newest `docs/prd-*.md`.

If multiple plausible candidates exist, list them and ask the user which one to implement against.

If none exists, tell the user — they probably want to run `sdd` or `to-prd` first.

## 2. Create the worktree

Derive a slug from the spec's title or filename (lowercase, kebab-case, max 30 chars).

Get the repo's directory name and the current branch:

```
REPO=$(basename "$PWD")
CURRENT=$(git rev-parse --abbrev-ref HEAD)
WT_PATH="../${REPO}-${SLUG}"
```

Create the worktree off the current branch with a new branch named after the slug:

```
git worktree add "$WT_PATH" -b "$SLUG"
```

If the branch already exists, drop the `-b` flag and check out the existing branch into the worktree.

For all subsequent file edits and shell commands, operate inside `$WT_PATH`. Use absolute paths in your tools. When running shell commands, prefix with `cd "$WT_PATH" &&`.

Tell the user the worktree path before continuing.

## 3. Plan

Read the spec end-to-end. Break the work into 2–6 concrete chunks, ordered by dependency. Each chunk should be one short phrase ("auth middleware", "session store", "login route").

Show the user the plan. Wait for go-ahead before writing code.

## 4. Implement chunk by chunk

For each chunk:

- Restate the chunk in one sentence.
- Implement it.
- Run any relevant type checks, linters, or sanity scripts.
- Check in with the user: what landed, what's next, any decisions you had to make that the spec didn't cover.

If you discover the spec was wrong or incomplete, update the spec in place. The spec is the living contract.

## 5. Hand off

When all chunks are done:

- Summarize what shipped versus what was deferred.
- Print the worktree path so the user can review, merge, and remove it.
- Do not merge. Do not delete the worktree. That's the user's call.

The user can clean up later with:

```
git worktree remove <path>
git branch -d <slug>
```
