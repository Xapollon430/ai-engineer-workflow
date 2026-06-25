# ai-engineer-workflow

An opinionated Claude Code plugin: skills, commands, and a SessionStart tone hook for an AI-assisted engineering workflow.

## Install

```
/plugin marketplace add Xapollon430/ai-engineer-workflow
/plugin install ai-engineer-workflow@ai-engineer-workflow
```

User-level — applies to every project on your machine.

## What's in it

### Skills

All skills are prefixed with `skill-` for easy discovery.

| Skill             | When it fires                                                                       |
|-------------------|-------------------------------------------------------------------------------------|
| `skill-sdd`       | You want a spec before code. Produces a single `spec.md` in the repo.               |
| `skill-to-prd`    | You've already discussed a feature and want it written up as a PRD.                 |
| `skill-grill-me`  | You want a plan stress-tested before building.                                      |
| `skill-handoff`   | You want to compact a conversation for a fresh agent to pick up.                    |
| `skill-debug`     | You're stuck on a bug — reproduce, minimize, hypothesize, instrument, fix.          |
| `skill-creator`   | You want to write a new Claude skill — guided creation, evaluation, and packaging.  |

`skill-sdd`, `skill-to-prd`, `skill-grill-me`, and `skill-handoff` are user-invoked (`disable-model-invocation: true`). Call them by saying the skill name in chat or via `/<name>` if your client supports it. `skill-creator` is model-invocable — the agent will reach for it when you ask to build a skill.

### Commands

All commands are prefixed with `action-` for easy discovery.

| Command                | What it does                                                                                  |
|------------------------|-----------------------------------------------------------------------------------------------|
| `/action-implement`    | Picks up the most recent `spec.md` / `prd.md` and implements it inside a fresh git worktree.  |
| `/action-pr-ready`     | Strips noisy comments from new code, commits with a one-sentence message, pushes the branch.  |
| `/action-code-review`  | Comprehensive review of the current branch's diff: quality, security, performance, docs.      |
| `/action-cleanup`      | Lists stale worktrees, merged branches, and old spec/PRD files. Confirms before removing.     |

### Hook

A `SessionStart` hook prints `assets/tone.md` so every new session opens with the same tone guidance (terse, no filler, banned phrases listed). Edit `assets/tone.md` to taste.

## Customizing

Most files are short and editable. The one you'll probably touch first:

- `assets/tone.md` — what tone you want the model to take.

## Attribution

`skill-to-prd`, `skill-grill-me`, and `skill-handoff` are adapted from [mattpocock/skills](https://github.com/mattpocock/skills) under the MIT license. `skill-creator` is copied verbatim from [anthropics/skills](https://github.com/anthropics/skills) under Apache 2.0. `action-code-review` is adapted from [anthropics/claude-code-action](https://github.com/anthropics/claude-code-action) under MIT. See `ATTRIBUTION.md`.

## License

MIT for plugin code. The bundled `skills/skill-creator/` carries its own Apache 2.0 license. See `LICENSE` and `skills/skill-creator/LICENSE.txt`.
