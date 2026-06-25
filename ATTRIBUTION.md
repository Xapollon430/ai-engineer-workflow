# Attribution

The following skills in this plugin are adapted from [mattpocock/skills](https://github.com/mattpocock/skills), licensed under the MIT License (Copyright (c) 2026 Matt Pocock):

- `skills/skill-to-prd/SKILL.md` — adapted: removed steps and template sections tied to test seams and testing decisions, replaced the issue-tracker publishing step with a local file save, removed the dependency on `setup-matt-pocock-skills`. Skill renamed to `skill-to-prd` for plugin-wide naming consistency.
- `skills/skill-grill-me/SKILL.md` — adapted: inlined the body of the `grilling` skill so it works standalone (the original was a one-line pointer to a separate skill). Skill renamed to `skill-grill-me`.
- `skills/skill-handoff/SKILL.md` — copied verbatim; skill renamed to `skill-handoff`.

The full MIT License text is included in `LICENSE`.

## Anthropic — action-code-review

`commands/action-code-review.md` is adapted from [anthropics/claude-code-action](https://github.com/anthropics/claude-code-action) (file: `examples/pr-review-comprehensive.yml`), Copyright (c) 2025 Anthropic, PBC. Licensed under the MIT License.

Adaptations: extracted the prompt body from the GitHub Action YAML, scoped it to a branch diff workflow, removed the "Testing" focus area, added severity tags and an output format section.

## Anthropic — skill-creator

`skills/skill-creator/` is copied verbatim from [anthropics/skills](https://github.com/anthropics/skills) (commit reference: `skills/skill-creator`), Copyright 2026 Anthropic, PBC. Licensed under the Apache License, Version 2.0. The full license text lives alongside the skill in `skills/skill-creator/LICENSE.txt`.

No modifications have been made to the skill or its supporting files.
