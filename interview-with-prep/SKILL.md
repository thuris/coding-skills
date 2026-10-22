---
name: interview-with-prep
description: "When asked for a prepared interview: read first, then ask."
disable-model-invocation: true
---

# Interview with prep

Use this only when the user asks for it. If you loaded it because it looked relevant to something else, set it aside and carry on with that.

The interview ends in a handoff document for implementation in a new session. Aim for shared understanding, not a quick start, and keep going while the problem or the user's intent is unclear, however many turns that takes. Don't begin implementation in this session unless the user asks for it after the handoff is saved.

First learn what the project can tell you, then ask the user only about what it can't. Investigate read-only; the handoff is the only file you write.

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

- **Found:** what you saw directly, and where. Config shows what the project declares, not what's running in production, and something missing from the repository may still exist in the real setup.
- **Inferred:** what the evidence suggests but doesn't show.
- **Surprises:** places where docs, config, and code disagree.

Mention only what bears on the decisions ahead, and don't ask the user to confirm each fact.

## Asking

- Ask only what would change the outcome, the design, the scope, or how we'll check the result, and skip anything already settled.
- Ask at most three things per turn, most important first, and fewer when one answer shapes the next. Count each subquestion, and each request tucked into prose, as its own item.
- Early on, invite the user to describe circumstances you haven't thought to ask about, and wait for their answer. The invitation counts as one of the three.
- Suggest an answer when the evidence points to one, with a short reason. Leave questions about intent, product direction, and taste open.
- Keep what you saw, what you inferred, and what you don't know apart, and don't present a guess as a default. If being wrong about an assumption could change the approach or disrupt something already in use, ask instead of assuming.
- The user decides when the interview is over. Don't offer to start work, and don't take earlier permission as a cue to wrap up. If you run out of useful questions, say so and leave room for more.

## What to settle

Cover whatever is still open of: outcome, scope, where it runs, constraints, checks, and shape. Before narrowing the approach, find out what already exists, what it connects to, and what must not change.

- **Checks:** the smallest set that would show the implementation works. Prefer trying the behavior where it's actually used, when that's direct and cheap; a build or typecheck shows only that the code compiles. Include tests when the logic branches, when a bug could come back unnoticed, or when the project expects them, but not for their own sake. Say which important checks the implementation session won't be able to run.
- **Shape:** the most direct change that's easy to maintain, with no speculative options, pass-through layers, or guards for states that callers and types already rule out.

## Handoff

Once the problem is clear, start the handoff as a Markdown file and give its path. Save it in the handoff folder your instructions name. If they name none, propose a folder outside the repository, and once the user agrees, offer to add it to their standing instructions (such as AGENTS.md or CLAUDE.md) so later sessions use it too.

Write for a new session that hasn't seen this conversation. Open with a note to that session: before building, compare the current commit with the recorded one, read the listed files, and ask about anything unclear. Then capture:

- The problem, intended outcome, and why it matters.
- Scope, constraints, existing circumstances, and what must not change.
- Decisions and their reasons, including relevant rejected approaches.
- Verified facts, assumptions, and unresolved questions, kept clearly apart.
- How success will be checked, plus relevant files and references.
- The branch and commit the investigation was based on.

Update the handoff as decisions are made, but don't force decisions to fill its sections; it records understanding and needn't be a detailed implementation plan. When the user says they're finished, bring it up to date and give its path again.

If the interview has to continue in a new session, for example because context is running low, mark the handoff as an interview continuation and list the remaining questions. Running low on context is a reason to continue elsewhere, not to declare the interview complete. When resuming from a continuation, start from its open questions and read only what they need instead of repeating the preparation.
