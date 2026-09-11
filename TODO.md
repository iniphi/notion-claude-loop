# TODO.md — the to-do contract

There is no task list in this file, and there never will be one. Every
to-do lives in the Global To-Do database in Notion (its ID is in
`CLAUDE.md` under `## Notion Pages`), and that database is the only place
a to-do is created, read, or closed.

- `/capture` writes a to-do there.
- `/session-start` reads the open ones for whichever project is active.
- `/session-wrap` marks finished ones Done and sets their Done date.

If you are tempted to jot a task into this file, a local README, or a code
comment — don't. A second list is the exact failure this loop exists to
prevent: it goes stale silently, and nothing here would ever know to check
Notion for the real answer.
