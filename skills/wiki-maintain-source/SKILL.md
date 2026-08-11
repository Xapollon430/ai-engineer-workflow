---
name: wiki-maintain-source
description: Reconcile new versions, changed titles, duplicate sources, conflicting claims, and wiki health. Use when an existing source has been clipped again or when checking whether the wiki is current.
disable-model-invocation: true
---

# Maintain and reconcile the wiki

Read `AGENTS.md` before changing the wiki when one exists in the wiki workspace.

Keep all raw files unchanged; raw files are historical evidence and the wiki is the current synthesis.

1. Compare the new source with likely matches using canonical/normalized URL, source ID, title similarity, and content similarity.
2. For the same source, keep the new raw snapshot, preserve the source page, add aliases, record meaningful changes, and update claims supported by the newer version.
3. For a different source, create a separate page and link related sources.
4. When sources disagree, preserve both claims, cite each source, explain supported reasons for disagreement, and mark the conflict resolved, partially resolved, or unresolved.
5. Never silently replace an older claim.
6. Update affected concept, entity, and synthesis pages, then update `index.md` and append a dated entry to `log.md`.

Record meaningful version history with dates. Use `status: current`, `supersedes`, and `current_snapshot` where appropriate; mark older pages `status: superseded` when justified.

When checking wiki health, look for broken `[[links]]`, orphan pages, duplicate concepts, stale claims, source pages missing from `index.md`, unresolved conflicts, and unsupported claims. Automatically fix only safe link and metadata issues; report substantive judgment calls before changing them.
