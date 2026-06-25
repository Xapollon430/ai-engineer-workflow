---
name: skill-sdd
description: Spec-driven development. Use when starting a non-trivial feature or change and you want a written contract before code. Drives the conversation to produce a single spec.md the agent can later implement against (see /action-implement).
disable-model-invocation: true
---

# Spec-driven development

Write the spec before the code. The spec is the contract between intent and implementation.

## When to use this skill

- The user says: "spec this out", "write a spec", "do this spec-driven", "SDD".
- The user is about to start non-trivial work where upfront alignment is cheaper than mid-implementation rework.

## Process

### 1. Probe the intent

Ask only what you cannot derive from the repo. Get:

- The problem, in plain terms.
- Who it affects and how they hit it today.
- What success looks like, concretely enough that you'd know if you missed.
- Any non-obvious constraints (perf, compat, deadlines, dependencies).

Ask questions one at a time. Multiple questions at once is bewildering.

If a question can be answered by exploring the codebase, explore the codebase instead.

### 2. Draft the spec

Write to `spec.md` at the repo root, unless a `docs/specs/` directory exists, in which case use `docs/specs/<slug>.md`.

Use these sections:

- **Problem** — one paragraph, user-facing.
- **Decisions** — bulleted: "this not that," with a short reason on each.
- **Data shapes** — types, schemas, payloads. Only the shapes that drive design; no field-by-field encyclopedia.
- **Behaviors** — inputs → outputs, edge cases, error paths.
- **Out of scope** — bulleted, explicit. "We're not doing X."
- **Open questions** — things the user has not yet decided. A spec with open questions is fine. A spec with assumed answers is not.

### 3. Read it back

Show the file. Ask once: "anything wrong or missing?" Edit in place based on the answer. Do not start a new round of interview unless the user opens one.

### 4. Stop

Implementation is `/action-implement`'s job. The spec is the handoff.

## Principles

- The spec is human-readable, not pseudo-code. If you're writing function signatures, you've gone too far.
- One spec per feature. Don't grow specs across unrelated work.
- The spec is the living contract — `/action-implement` will update it in place as decisions get refined during the build.
