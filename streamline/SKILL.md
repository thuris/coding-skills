---
name: streamline
description: "When asked to streamline: simplify, keeping behavior."
disable-model-invocation: true
---

# Streamline

Use this only when the user asks for it. If you loaded it because it looked relevant to something else, set it aside and carry on with that.

The aim is to make a working change simpler: clearer, more direct, and easier to maintain, with the same behavior. That often means fewer lines, but not always. A helper with a good name, or a guard that protects something real, is worth keeping.

## Scope

- Work on the current change (the diff against the base branch) or on the files the user names. Keep edits inside that scope, apart from updating internal callers when a simplification needs it.
- Code this change introduced is still open: nothing relies on its behavior yet, so simplifying it may change how it fails or what it falls back to. Behavior that has already shipped is different. Changing it is the user's decision, so flag it instead.
- Don't judge from the diff alone. Read the callers, the types, the project's instructions, and the history of any existing lines involved, so you know what the rest of the code already guarantees.

## Who reviews

Have a subagent do the review, so the code is read by someone who didn't write it. Use the harness's default subagent or a copy of yourself, not a smaller model chosen for the occasion.

Give the reviewer the goal of the change, the diff, and the Scope, What to simplify, and What to preserve sections of this skill, since it won't see the skill otherwise. Leave out your reasons for writing the code the way you did; the point is a reader who doesn't share them. Ask for proposed changes ordered by value, plus the candidates it considered and would keep, each with a few words of reasoning.

If you can't start a subagent here, do the review yourself, and judge the code by what it does, not by why it was written.

## What to simplify

- **Pass-through indirection:** wrappers, helpers, classes, or interfaces with one caller that add a step without a meaningful boundary or a name that explains anything. Inline them.
- **Reshaped data:** converting between near-identical types as data passes between internal functions (input to options to config to result) when the original type would do.
- **Shims for internal callers:** fallback branches, union parameter types, or adapters added in this change so internal callers didn't have to be updated. Update those callers instead of keeping both paths.
- **Defensive code for states that can't happen:** null, type, or range checks on values that callers or types already rule out; try/catch blocks that only log and rethrow, or that swallow errors; fallback defaults nobody asked for that hide real failures.
- **Speculative generality:** parameters, config keys, flags, hooks, or extension points that nothing uses yet.
- **Duplication:** logic that reimplements a utility the project already has, or works around a direct idiom of the language or framework.
- **Noise:** comments that narrate obvious code, dead branches, leftover debugging output, and tests that only restate the implementation, such as ones that mostly check their own mocks.

## What to preserve

- **Real boundaries:** validation and recovery for user input, command-line arguments, HTTP payloads, the file system, databases, networks, and external APIs.
- **Public contracts:** exported signatures, API routes, config keys, user-facing messages, and logging that someone relies on.
- **Stored and transmitted formats:** anything earlier versions wrote or sent that this code must keep reading, such as database rows, files, caches, queued messages, and requests from older clients still in use. A fallback for an old format can look exactly like an unneeded shim.
- **Deliberate conventions:** patterns the project's documented architecture or a migration in progress calls for, even when they're verbose.
- **Bugs and behavior changes:** if you find a real bug, or a simplification would change shipped behavior, flag it separately instead of folding it in.

## Reporting and applying

If the user asked only for a review, report the findings as a numbered list, most valuable first: where (file and line), what to change, why it's safe given the callers and types, and any risk. Put trivial items together at the end, then briefly list the candidates worth keeping and why. If the change is already lean, say so and stop.

If the user asked you to streamline:

1. Run the agreed checks first (from the interview if there was one; otherwise the relevant tests, build, and typecheck), so you know where things stand.
2. Apply the reviewer's proposals, except any that would change shipped behavior. If you disagree with one, leave it out and say why in your report rather than dropping it silently.
3. Run the checks again. If a change breaks one, fix it or undo it, and keep failures that were already there separate from new ones.
4. Stop when what's left is marginal or would need a redesign. Mention a redesign; don't start one.
5. Report what you changed, what the checks showed, what you kept and why (a few words each), and anything left for the user to decide.
