---
name: interview-with-prep
description: "When asked for a prepared interview: read first, then ask."
disable-model-invocation: true
---

# Interview with prep

Use this only when the user asks for it. If you loaded it because it looked relevant to something else, set it aside and carry on with that.

First learn what the project can tell you, then ask the user only about what it can't. Everything here is read-only.

## Preparing

Start with the code nearest the change and widen only as far as you need to ask good questions:

- Project instructions and docs: AGENTS.md, CLAUDE.md, README, CONTRIBUTING
- Manifests, lockfiles, and build, lint, and typecheck config
- Deployment and CI config: Dockerfiles, workflows, service files, host scripts, example environment files
- Nearby modules, callers, types, and tests
- Recent history in the area (`git log`, `git blame`) when something looks inconsistent or half-migrated

Stop reading when more files won't sharpen the questions.

## Reporting

Before asking anything, give a short readout:

- **Found:** what you saw directly, and where. A version in a config file tells you what the project declares, not what's running in production.
- **Inferred:** what the evidence suggests but doesn't show.
- **Surprises:** places where docs, config, and code disagree.

Mention only what bears on the decisions ahead, and don't ask the user to confirm each fact.

## Asking

- Ask only about what the preparation left open and what would change the outcome, the design, the scope, or how we'll check the result.
- Ask up to three questions at a time, most important first, and fewer when one answer shapes the next. Keep each question to a sentence or three.
- Suggest an answer when the evidence points to one, with a short reason. Leave questions about intent, product direction, and taste open.
- Don't present a guess about where the code runs as though it were a default, especially where the real setup may differ from the config.
- Stop when the remaining unknowns can be covered by small assumptions, stated plainly.

## What to settle

Cover whatever is still open of: outcome, scope, where it runs, constraints, checks, and shape.

- **Checks:** the smallest set that would show the behavior works. Where it's direct and cheap, try the behavior where it's actually used; a build or typecheck shows only that the code compiles. Add or update tests when the logic branches, when a bug could come back unnoticed, or when the project expects them, but not for their own sake. Say which important checks can't be run here.
- **Shape:** the most direct change that's easy to maintain, with no speculative options, pass-through layers, or guards for states that callers and types already rule out.

## Finishing

Write a short summary: outcome, scope, where it runs, constraints, checks, and any assumptions. Save it to a file only if asked.

- If the user asked only for preparation or discussion, stop there.
- If they've already asked you to go ahead and the important questions are settled, start the work without asking again.
- Otherwise, end with the summary and ask whether to start.
