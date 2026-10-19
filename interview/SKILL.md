---
name: interview
description: "When asked to interview: clarify the task before starting."
disable-model-invocation: true
---

# Interview

Use this only when the user asks for it. If you loaded it because it looked relevant to something else, set it aside and carry on with that.

The point is to understand the work before it starts, so we don't build the wrong thing or build it for the wrong place.

Don't start the work during the interview. When a quick read-only look would answer a question (a file, a config setting, an installed version), look instead of asking.

## Asking

- Ask only what would change the outcome, the design, the scope, or how we'll check the result. Skip anything already settled.
- Ask up to three questions at a time, most important first, and fewer when one answer shapes the next. Keep each question to a sentence or three.
- Suggest an answer when the code or sound engineering points to one, with a short reason. Leave questions about intent, product direction, and taste open.
- Keep what you saw, what you inferred, and what you don't know apart. Don't present a guess about where the code runs as though it were a default.
- Stop when the remaining unknowns can be covered by small assumptions, stated plainly.

## What to cover

Skip whatever is already clear. For work that isn't code, cover the outcome, scope, constraints, and how the result will be judged, and leave out the rest.

1. **Outcome.** What should be true when this is done, for whom, and why.
2. **Scope.** What's in, what's out, and what must not change.
3. **Where it runs.** Operating system, runtime versions, host or device, network and permission limits, data volumes, and how it gets deployed. Repository config shows the intended setup; when the real one matters and you can't see it, ask.
4. **Constraints.** Dependencies allowed or ruled out, cost and performance limits, compatibility, and preferences about naming, interface, and style. On a new project, also the language, frameworks, and data storage, if they aren't decided yet. These are often a matter of preference, so ask before suggesting one.
5. **Checks.** The smallest set of checks that would show the behavior works.
   - Where it's direct and cheap, try the behavior where it's actually used: run the command, call the endpoint, load the page. A build or typecheck shows that the code compiles, not that it works.
   - Add or update automated tests when the logic branches, when a bug could come back unnoticed, or when the project expects them. There's no test-first rule, and tests shouldn't be written for their own sake.
   - Say which important checks can't be run here.
6. **Shape.** The most direct change that's easy to maintain: no speculative options, no pass-through layers, and no guards for states that callers and types already rule out.

## Finishing

Write a short summary of what you settled, plus any assumptions. Save it to a file only if asked.

- If the user asked only to discuss or plan, stop there.
- If they've already asked you to go ahead and the important questions are settled, start the work without asking again.
- Otherwise, end with the summary and ask whether to start.
