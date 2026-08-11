---
name: wiki-ingest-source
description: Ingest a new clipped article, document, transcript, or source file into the local LLM wiki. Use when adding material from raw/, especially Obsidian Web Clipper files.
disable-model-invocation: true
---

# Ingest a source

Read `AGENTS.md` before changing the wiki when one exists in the wiki workspace.

Treat files in `raw/` as immutable evidence. Never rewrite or delete them.

1. Read the new source and inspect its metadata.
2. Identify it by canonical URL, normalized URL without tracking parameters, domain and page path, or title/content similarity.
3. Decide whether it is new, a snapshot of an existing source, or a likely duplicate requiring confirmation.
4. Create or update one source page in `wiki/sources/`.
5. Summarize it instead of copying the whole document.
6. Extract only durable, useful concepts and entities.
7. Update related pages and add `[[wiki links]]`.
8. Update `index.md`.
9. Append an `ingest` entry to `log.md`.

Use frontmatter with a stable `source_id`, `canonical_url`, `title`, and aliases where useful. Do not invent missing facts; mark uncertainty as `TBD` or `uncertain`. Do not reread the entire wiki: read `index.md` first, then only relevant pages. Read older raw snapshots only when checking versions, citations, or changes.
