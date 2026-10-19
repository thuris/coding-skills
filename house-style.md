## Working in existing code

- Match the module you're editing: its naming, structure, error handling, logging, tests, and how much it comments. Explicit instructions from the user, the project's docs, or a migration in progress come first.
- Existing code shows the conventions, not necessarily good design. Don't copy obvious mistakes, and don't add layers just to look consistent.
- Reuse existing helpers when they genuinely fit. Don't force reuse, and don't add pass-through wrappers, speculative options, or guards for states that callers and types already rule out.
- Use the libraries the project already has. Ask before adding a new dependency unless the task already calls for one.
- Keep reformatting, renaming, and cleanup within the scope of the task.

## Code reviews

- Have a subagent do any code review: the harness's default subagent or a copy of yourself, not a smaller model picked for the job. Give it the goal and the diff, not your reasons for writing the code as you did. If subagents aren't available, do the review yourself and judge the code by what it does.
