---
name: skill-debug
description: Disciplined debug loop — reproduce, minimize, hypothesize, instrument, fix. Use when stuck on a bug, chasing a regression, or you've already made two or more changes that didn't help.
disable-model-invocation: true
---

# Debug

Stop guessing. Run the loop.

## When to use

- The bug doesn't reproduce reliably.
- You've already made two or more changes that didn't fix it.
- You don't know which layer is at fault.
- A "small" fix is on its third revision.

## The loop

### 1. Reproduce

Get the bug to happen on demand. State the repro in one sentence:

> "When I do X, Y happens. I expected Z."

If it's intermittent, find what makes it intermittent (timing, ordering, input, environment). Do not proceed until the repro is reliable. An intermittent repro is a hypothesis, not a fact.

### 2. Minimize

Strip the repro to the smallest case that still triggers the bug. Remove every input, dependency, and step that isn't required to reproduce.

The goal is to make the cause visible by deleting the noise around it.

### 3. Hypothesize

Write down what you think is happening. Be specific:

- Good: "`user.session` is null when the middleware on line 42 assumes it isn't."
- Bad: "the auth state is wrong somewhere."

If you have multiple hypotheses, list them. Pick the cheapest one to disprove first.

### 4. Instrument

Add the cheapest possible signal — a print, a log line, a breakpoint — that will confirm or deny the hypothesis. Do not fix anything yet.

Run the minimized repro with the instrument. Read the output.

### 5. Decide

- **Confirmed** → go to step 6.
- **Denied** → next hypothesis. Back to step 3.
- **Surprise** (the output makes no sense) → you found something your mental model didn't predict. Update the model before forming the next hypothesis. Surprises are the most valuable signal in the loop; do not skip past them.

### 6. Fix

Make the smallest change that resolves the confirmed cause. One change. Re-run the minimized repro. Then re-run the full original repro.

If the fix doesn't hold under the full repro, the minimization missed something. Back to step 2.

### 7. Sweep

Ask: does the same root cause hide anywhere else?

Grep for the pattern. Look at sibling call sites. Look at callers of the function you fixed. Fix every site, not just the one that bit you.

### 8. Leave a trail

If the cause was non-obvious, leave a one-line comment explaining the *constraint that made the wrong code wrong*. Not the bug. Not the fix. The invariant.

Example: `// stripe webhooks may arrive out of order; treat `status` as monotonic`

## Anti-patterns

- **Changing two things at once.** You won't know which helped, and you'll trust the wrong cause next time.
- **Skipping reproduction.** You can't fix what you can't see. "I think it's X" is not a repro.
- **Skipping minimization.** Big repros hide the cause inside their own noise.
- **Verbose tracing.** A single targeted print beats a flood of log lines.
- **Declaring victory at step 6.** Step 7 catches the next four bugs.
