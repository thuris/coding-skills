# Personal coding skills (v4)

Three skills you invoke by name, plus a short set of standing instructions for every coding session. This is Opus's revision of Argon's v3; the earlier versions sit beside it.

## What's here

| File | Where it goes | Purpose |
|---|---|---|
| [interview](interview/SKILL.md) | Skills folder | Clarify the outcome, scope, constraints, and how to check the result before starting; suits new projects and work that isn't code |
| [interview-with-prep](interview-with-prep/SKILL.md) | Skills folder | For existing projects: read the project first, then ask only what it can't answer |
| [streamline](streamline/SKILL.md) | Skills folder | Simplify a working change without changing its behavior, with a subagent doing the review |
| [house-style.md](house-style.md) | Standing instructions | Fit in with existing code without copying its mistakes, and send code reviews to a subagent |

Each skill folder also holds `agents/openai.yaml`, which tells Codex not to load the skill on its own.

## Using them in each harness

| | Skills folder | How to invoke | What stops automatic loading |
|---|---|---|---|
| Claude Code | `~/.claude/skills` | `/interview` | `disable-model-invocation: true` in the frontmatter |
| Codex | `~/.agents/skills` | `$interview`, or pick it from `/skills` | `agents/openai.yaml` |
| Hermes | Hermes's skills folder, or one listed in `skills.external_dirs` | `/interview` | Nothing mechanical; see below |

In Claude Code and Codex, asking in plain words ("interview me about this") won't load these skills. Use the command.

## Hermes notes

- **It loads skills eagerly.** Its system prompt tells the model to load any skill that looks even partly relevant, and no setting limits a skill to explicit use. So each description starts with "When asked…", and each skill opens by telling the model to set it aside if nobody asked for it.
- **Descriptions are cut at 60 characters** in its skill list (57 plus "..."). Keep them that short.
- **Skills can't reach outside their own folder,** because `..` paths are refused. That's why interview-with-prep repeats the interview steps instead of pointing to the interview skill. When you change one, change the other.
- **It edits skills.** The model is told to fix skills it finds lacking, and a background curator revises them too. Pinning a skill only protects it from deletion. Keep Hermes's copy separate from the one the other harnesses use, and under git, so its changes show up as diffs you can keep or discard.

## Where house-style goes

- **Claude Code:** `~/.claude/CLAUDE.md`, which loads in every project alongside the project's own instructions. It can pull in a shared file with an `@` import.
- **Codex:** `~/.codex/AGENTS.md`.
- **Hermes:** the AGENTS.md that every profile on the install loads. Hermes looks for AGENTS.md by walking up from the session's working folder, so check that it still loads when a session works inside a repository.

## Design choices

- **Checking results.** Agree on the smallest set of checks that would show the behavior works. Trying the behavior where it's used beats a build or typecheck, which only shows that the code compiles. Add tests when logic branches, when a bug could come back unnoticed, or when the project expects them. There's no test-first rule.
- **Permission carries forward.** If you asked for discussion, a skill ends with a summary. If you already said to go ahead, it proceeds once the important questions are settled. If you said neither, it asks.
- **New code is open; shipped behavior isn't.** Streamline may change how code from the current change fails or falls back. Changes to behavior that has already shipped are flagged for you instead.
- **Review by a fresh reader.** Streamline hands the review to a subagent (the harness's default, or a copy of the main model) that didn't write the code and isn't told the author's reasons. The subagent gets the relevant sections of the skill in its instructions, since Claude Code won't preload a skill marked `disable-model-invocation` into a subagent. Where subagents aren't available, the agent reviews the code itself. The standing instructions apply the same rule to every code review.
- **Short on purpose.** Each skill stays around a page.

## Changes from v3

- **Loading:** Codex policy files added. Each skill now opens with a line for Hermes's eager loading.
- **Interview:** a build or typecheck no longer counts as trying the behavior. The ending covers the case where you didn't say whether to proceed. interview-with-prep's copy of the steps is back in line with interview. Interview now also suits new projects, where it asks about the language, frameworks, and data storage, and work that isn't code.
- **Streamline:** added the rule that new code is open and shipped behavior isn't. Shims are limited to ones added in the current change. Stored and transmitted data formats are preserved. The review goes to a subagent, there's a stopping point, and the report lists what was kept and why. "What to cut" is now "What to simplify."
- **House-style:** now covers comments and dependencies, and sends any code review to a subagent. "Single-caller wrappers" became "pass-through wrappers."
- **Prose:** abbreviations removed and the wording made plainer throughout.

## A first evaluation

For two weeks, add a line to a plain text file each time you use a skill: the date, the harness and model, the skill, and whether it changed anything. Did a question surface something you'd otherwise have hit late? Did you keep or revert streamline's changes? Comparing `git diff --stat` before and after shows the size of the change. Note any regression, unwanted trigger, or needless interruption. Then cut or rework whatever didn't earn its place.
