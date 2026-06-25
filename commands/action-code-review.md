---
description: Comprehensive code review of the current branch's diff against main — quality, security, performance, documentation.
---

<!-- Adapted from anthropics/claude-code-action (MIT), examples/pr-review-comprehensive.yml. See ATTRIBUTION.md. -->

Perform a comprehensive code review of the changes on the current branch.

## Scope

Review only the diff between the current branch and `main` (or `master` if `main` does not exist). Do not comment on unchanged code, even if it looks bad — it belongs to whoever wrote it.

Run `git diff main...HEAD` (or `git diff master...HEAD`) to see the diff. Run `git log main..HEAD --oneline` for commit history.

## Focus areas

### 1. Code quality
- Clean code principles and best practices.
- Proper error handling and edge cases.
- Code readability and maintainability.
- Dead code, duplicated logic, unused imports.

### 2. Security
- Potential security vulnerabilities.
- Input validation and sanitization.
- Authentication and authorization logic.
- Secrets, tokens, or credentials accidentally committed.

### 3. Performance
- Obvious performance bottlenecks.
- Database queries: N+1, missing indexes, unbounded scans.
- Memory leaks or resource lifecycle issues.
- Unnecessary work in hot paths.

### 4. Documentation
- Public APIs documented where appropriate.
- README updated if behavior or install steps changed.
- Comments explain the *why* of non-obvious code, not the *what*.

## Output format

Group findings by focus area. For each finding, give:

- The file and line(s) (`path/to/file.ts:42-58`).
- A one-sentence description of the issue.
- A concrete suggestion to fix it.

Use severity tags: `[blocker]`, `[major]`, `[minor]`, `[nit]`.

Keep feedback concise. Only surface noteworthy issues — if the code is fine in an area, say so in one line and move on. No filler praise.

End with a one-sentence overall verdict: "ship it", "ship after addressing blockers", or "needs another pass."
