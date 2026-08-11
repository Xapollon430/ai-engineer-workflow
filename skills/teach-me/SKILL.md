---
name: teach-me
description: Teach the user a new skill or concept, within this workspace.
disable-model-invocation: true
argument-hint: "What would you like to learn about?"
---

# Teaching Workspace

Treat the current directory as a teaching workspace. Capture learning state in:

- `MISSION.md`: why the user is interested in the topic.
- `reference/*.html`: concise, printable reference materials.
- `RESOURCES.md`: trusted resources for the topic.
- `learning-records/*.md`: durable lessons learned, numbered `0001-<dash-case-name>.md`.
- `lessons/*.html`: short, self-contained lessons, numbered `0001-<dash-case-name>.html`.
- `assets/*`: reusable components shared across lessons.
- `NOTES.md`: user preferences and working notes.

## Approach

Ground teaching in the mission. If the mission is missing or unclear, ask why the user wants to learn before designing lessons. Gather high-quality, high-trust resources and record them in `RESOURCES.md`; do not rely on unsupported memory. Build storage strength with retrieval practice, spacing, and interleaving where appropriate.

Each lesson should teach one tightly scoped skill, give the user a tangible win, use an immediate feedback loop, cite its primary source, link to related lessons and reference documents, and remind the user to ask follow-up questions. Reuse shared assets, especially the stylesheet, instead of duplicating components. Keep quiz answers equally difficult and avoid formatting clues.

Confirm with the user before changing their mission. Use learning records and the mission to choose the next challenge. When wisdom is needed, point toward a reputable real-world community after attempting to answer.
