---
name: skill-to-issues
description: Break a PRD, spec, or plan into independently-grabbable issue files using vertical slices. Use after skill-to-prd or skill-sdd when you want trackable units of work instead of one big doc.
disable-model-invocation: true
---

<!-- Adapted from mattpocock/skills (MIT). See ATTRIBUTION.md. -->

# To Issues

Break a plan into independently-grabbable issues using vertical slices (tracer bullets). Issues are written as local files under `docs/issues/` so the AI can walk them as checkpoints during implementation.

## Process

### 1. Find the source

Look for, in order:

- A path the user passed as an argument.
- `prd.md` at the repo root, or the newest `docs/prd-*.md`.
- `spec.md` at the repo root, or the newest file under `docs/specs/`.

If multiple plausible candidates exist, list them and ask which one. If none exists, tell the user — they probably want `skill-to-prd` or `skill-sdd` first.

### 2. Explore the codebase

If you haven't already, explore the area being changed. Issue titles and descriptions should use the project's domain vocabulary and respect any ADRs in the area you're touching.

Look for prefactors that would make the implementation easier. "Make the change easy, then make the easy change." Prefactors get their own issues and come first in the dependency order.

### 3. Draft vertical slices

Break the source into **tracer bullet** issues. Each issue is a thin vertical slice that cuts end-to-end through every integration layer, NOT a horizontal slice of one layer.

<vertical-slice-rules>

- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests).
- A completed slice is demoable or verifiable on its own.
- Prefactors run first, as their own slices.

</vertical-slice-rules>

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title** — short descriptive name.
- **Blocked by** — which other slices (if any) must complete first.
- **User stories covered** — which user stories this addresses (if the source has them).

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the dependencies correct?
- Should any slices be merged or split further?

Iterate until the user approves the breakdown. Do not write files yet.

### 5. Write the issue files

Once approved, write each slice to `docs/issues/<NN>-<slug>.md`, where `<NN>` is a zero-padded ordinal in dependency order (`01-`, `02-`, …) and `<slug>` is a short kebab-case name. Use the template below.

After writing, print the list of files created.

<issue-template>
## Parent

A reference to the source doc (PRD/spec path). Omit if there isn't one.

## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

Avoid specific file paths or code snippets — they go stale fast. Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it here and note briefly that it came from a prototype. Trim to the decision-rich parts — not a working demo, just the important bits.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Blocked by

- A reference to the blocking issue file (e.g., `01-prefactor-foo.md`).

Or "None — can start immediately" if no blockers.

</issue-template>
