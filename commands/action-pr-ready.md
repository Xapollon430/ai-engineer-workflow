---
description: Strip over-explaining comments from new code, commit with a one-sentence message, push to the current branch's remote.
---

You are finalizing this branch for review. Do these steps in order. Do not skip.

## 1. Inspect the diff

Run `git status` and `git diff` (both unstaged and staged). Get a clear picture of what changed.

If the current branch is `main` or `master`, stop. Tell the user `/pr-ready` does not operate on default branches.

## 2. Strip over-explaining comments

Scope: only lines this branch added or modified. Do not touch comments on unchanged lines — even if they look bad. Those belong to whoever wrote them.

Remove a comment if any of these are true:

- It restates what the code already says (e.g. `// increment counter` above `counter++`).
- It narrates the change ("added this for the X flow", "removed Y", "TODO from PR #123").
- It explains the obvious for a literate reader of the language.

Keep a comment if any of these are true:

- It documents a non-obvious constraint, invariant, workaround, or footgun.
- It points to an external issue, ticket, or spec the code depends on.
- It is a docstring or JSDoc on a public API.

When in doubt, keep it. Deleting a useful comment is worse than leaving a noisy one.

## 3. Commit

Stage files with explicit paths. Do not use `git add .` or `git add -A` — those can sweep in secrets or untracked files the user did not intend.

Write a one-sentence commit message. Focus on the *why* or the *outcome*, not the *what*. Match the style of recent commits in `git log`.

## 4. Push

Push to the current branch's upstream. If no upstream is set, set it to `origin/<current-branch>` and push.

Never force-push. Never push to `main` or `master`. If the push fails, report the failure verbatim. Do not retry or rewrite history.

## 5. Report

Print:

- The commit SHA and message.
- The remote ref it was pushed to.
- A one-sentence summary of what's in the branch. This is the PR description starter — the user copies it into the PR.
