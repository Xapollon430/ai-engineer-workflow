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

| Skill      | When it fires                                                                 |
|------------|-------------------------------------------------------------------------------|
| `sdd`      | You want a spec before code. Produces a single `spec.md` in the repo.         |
| `to-prd`   | You've already discussed a feature and want it written up as a PRD.           |
| `grill-me` | You want a plan stress-tested before building.                                |
| `handoff`  | You want to compact a conversation for a fresh agent to pick up.              |

All skills are user-invoked (`disable-model-invocation: true`). Call them by saying the skill name in chat or via `/<name>` if your client supports it.

### Commands

| Command         | What it does                                                                                  |
|-----------------|-----------------------------------------------------------------------------------------------|
| `/implement`    | Picks up the most recent `spec.md` / `prd.md` and implements it inside a fresh git worktree.  |
| `/pr-ready`     | Strips noisy comments from new code, commits with a one-sentence message, pushes the branch.  |
| `/code-review`  | Empty scaffold — drop your review process into `commands/code-review.md`.                     |

### Hook

A `SessionStart` hook prints `assets/tone.md` so every new session opens with the same tone guidance (terse, no filler, banned phrases listed). Edit `assets/tone.md` to taste.

## Customizing

Most files are short and editable. The two you'll probably touch first:

- `assets/tone.md` — what tone you want the model to take.
- `commands/code-review.md` — your review checklist.

## Attribution

`to-prd`, `grill-me`, and `handoff` are adapted from [mattpocock/skills](https://github.com/mattpocock/skills) under the MIT license. See `ATTRIBUTION.md`.

## License

MIT. See `LICENSE`.
