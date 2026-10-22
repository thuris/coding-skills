---
name: interview
description: "When asked to interview: clarify the task before starting."
disable-model-invocation: true
---

# Interview

Use this only when the user asks for it. If you loaded it because it looked relevant to something else, set it aside and carry on with that.

The interview ends in a handoff document for implementation in a new session. Aim for shared understanding, not a quick start, and keep going while the problem or the user's intent is unclear, however many turns that takes. Don't begin implementation in this session unless the user asks for it after the handoff is saved.

Investigate read-only; the handoff is the only file you write. When a quick look would answer a question (a file, a config setting, an installed version), look instead of asking.

## Asking

- Ask only what would change the outcome, the design, the scope, or how we'll check the result, and skip anything already settled.
- Ask at most three things per turn, most important first, and fewer when one answer shapes the next. Count each subquestion, and each request tucked into prose, as its own item.
- Early on, invite the user to describe circumstances you haven't thought to ask about, and wait for their answer. The invitation counts as one of the three.
- Suggest an answer when the code or sound engineering points to one, with a short reason. Leave questions about intent, product direction, and taste open.
- Keep what you saw, what you inferred, and what you don't know apart, and don't present a guess as a default. If being wrong about an assumption could change the approach or disrupt something already in use, ask instead of assuming.
- The user decides when the interview is over. Don't offer to start work, and don't take earlier permission as a cue to wrap up. If you run out of useful questions, say so and leave room for more.

## What to cover

Skip whatever is already clear. For work that isn't code, cover the outcome, scope, constraints, and how the result will be judged, and leave out the rest. Before narrowing the approach, find out what already exists and what it connects to.

1. **Outcome.** What should be true when this is done, for whom, and why.
2. **Scope.** What's in, what's out, and what must not change.
3. **Where it runs.** Operating system, runtime versions, host or device, network and permission limits, data volumes, and how it gets deployed. Repository config shows the intended setup, and something missing from the repository may still exist in the real one; when the real setup matters and you can't see it, ask.
4. **Constraints.** Dependencies allowed or ruled out, cost and performance limits, compatibility, and preferences about naming, interface, and style. On a new project, also the language, frameworks, and data storage, if they aren't decided yet. These are often a matter of preference, so ask before suggesting one.
5. **Checks.** The smallest set that would show the implementation works.
   - Prefer trying the behavior where it's actually used, when that's direct and cheap: run the command, call the endpoint, load the page. A build or typecheck shows that the code compiles, not that it works.
   - Include automated tests when the logic branches, when a bug could come back unnoticed, or when the project expects them. There's no test-first rule, and tests shouldn't be written for their own sake.
   - Say which important checks the implementation session won't be able to run.
6. **Shape.** The most direct change that's easy to maintain: no speculative options, no pass-through layers, and no guards for states that callers and types already rule out.

## Handoff

Once the problem is clear, start the handoff as a Markdown file and give its path. Save it in the handoff folder your instructions name. If they name none, propose a folder outside the repository, and once the user agrees, offer to add it to their standing instructions (such as AGENTS.md or CLAUDE.md) so later sessions use it too.

Write for a new session that hasn't seen this conversation. Open with a note to that session: before building, read the listed files and ask about anything unclear. Then capture:

- The problem, intended outcome, and why it matters.
- Scope, constraints, existing circumstances, and what must not change.
- Decisions and their reasons, including relevant rejected approaches.
- Verified facts, assumptions, and unresolved questions, kept clearly apart.
- How success will be checked, plus relevant files and references.

Update the handoff as decisions are made, but don't force decisions to fill its sections; it records understanding and needn't be a detailed implementation plan. When the user says they're finished, bring it up to date and give its path again.

If the interview has to continue in a new session, for example because context is running low, mark the handoff as an interview continuation and list the remaining questions. Running low on context is a reason to continue elsewhere, not to declare the interview complete. When resuming from a continuation, start from its open questions instead of starting over.
