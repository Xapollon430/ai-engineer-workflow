# ai-engineer-workflow

A small collection of skills for work in this repository.

## Skills

### `to-sdd`

Use for non-trivial work when you want a written contract before implementation. It asks only repo-unanswerable questions, writes a single `spec.md` (or `docs/specs/<slug>.md` when that directory exists), includes implementation checkboxes plus an append-only progress log, reads it back for correction, and stops. Implementation is a separate step.

Invoke with phrases such as “spec this out,” “write a spec,” “do this spec-driven,” or “SDD.”

### `grill-me`

Use to stress-test a plan or design before building. It interviews you one question at a time, explores the decision tree, resolves dependencies, and recommends an answer for each question.

Invoke by asking to grill or stress-test a plan.

### `teach-me`

Use to learn a new skill or concept over multiple sessions. The current directory becomes a teaching workspace. Learning state lives in `MISSION.md`, `RESOURCES.md`, `NOTES.md`, `reference/`, `learning-records/`, `lessons/`, and `assets/` as they are created.

Lessons are short, self-contained HTML files in `lessons/`, numbered `0001-<dash-case-name>.html`. They should be grounded in the mission, use trusted sources, include citations, provide practice and feedback, link to related lessons/reference documents, and remind you to ask follow-up questions. Raw source files are evidence and should remain unchanged.

Invoke by asking to learn or be taught something. This skill is user-invoked and does not run automatically.

### `code-review`

Use to review changes since a fixed point such as a commit, branch, tag, or merge-base. It checks the diff along two separate axes: Standards, meaning whether the code follows this repo's documented standards plus baseline code-smell heuristics, and Spec, meaning whether the change matches the originating issue or spec.

Invoke when reviewing a branch, PR, work-in-progress changes, or by asking to “review since X.”

### `wiki-ingest-source`

Use when adding a clipped article, document, transcript, or source file from `raw/` to the local LLM wiki.

Before changing the wiki, read `AGENTS.md` if one exists in the wiki workspace. Treat `raw/` as immutable. Identify sources by canonical or normalized URL first, then domain/path, title, or content similarity. Create or update one summarized page in `wiki/sources/`, extract durable concepts and entities, add wiki links, update `index.md`, and append an `ingest` entry to `log.md`. Never invent missing facts; mark them `TBD` or `uncertain`.

### `wiki-maintain-source`

Use when reconciling new versions, changed titles, duplicate sources, conflicting claims, or wiki health.

Keep all raw snapshots unchanged. Compare sources by canonical/normalized URL, source ID, title, and content similarity. Preserve version history and conflicting claims rather than silently replacing older claims. Update related pages, `index.md`, and `log.md`. Health checks cover broken wiki links, orphan pages, duplicate concepts, stale claims, missing source index entries, unresolved conflicts, and unsupported claims. Automatically fix only safe link and metadata issues; report substantive judgment calls first.

## Repository rules

- These six skills are the complete contents of this repository.
- Skill instructions live at `skills/<skill-directory>/SKILL.md`.
- Keep operational metadata and usage guidance here in `README.md`.
- Do not add `CLAUDE.md` or `AGENTS.md` files to this repository.
