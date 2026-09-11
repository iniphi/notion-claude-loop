# ARCHITECTURE.md — the memory map

```
Root page ("Notion <-> Claude loop")
|-- Projects (database)        - one row per project; Hub links to its page
|-- Global To-Do (database)    - every to-do, across every project
|-- Notes (database)           - non-action thoughts, across every project
`-- one Hub page per project
    |-- Current State (child page)      - replaced, never appended, by /session-wrap
    |-- Session Log (inline database)   - one row per session
    |-- "Open to-dos" (filtered view)   - Global To-Do filtered to this project
    `-- "Notes" (filtered view)         - Notes filtered to this project
```

The row in Projects is the register entry. The Hub page it links to **is**
the project — that is where state actually lives.

## Why this shape

- **One Global To-Do, one Notes database, forever.** A to-do or a note is
  only ever *seen* through a project's filtered view; it is never copied
  into the project. This is what lets one list work across many projects,
  and why `TODO.md` in this repo carries no tasks of its own.
- **Current State is a page, not a database row.** It is prose, written for
  someone who has forgotten everything, and `/session-wrap` replaces it
  wholesale — never appends to it.
- **The Session Log is per-project, not shared.** Same columns as every
  other project's log, but a separate database, so one project's history
  never crowds another's.
- **The Hub property on a Projects row does not survive duplication
  cleanly.** Notion copies a URL property's text verbatim rather than
  repointing it, so on a fresh copy it can be empty or still aimed at the
  original workspace. `/session-start` checks for this and repairs it the
  first time it finds a broken Hub — that is a one-time repair, not a bug.

## Where behaviour is defined

The five skill bodies in `.claude/skills/` are what this repository was
built from, not a copy Claude keeps drifting away from the source. If you
want different behaviour on every surface at once, edit the Notion ForClaude
pages under the root and rebuild the skill files from them — see the
provenance note at the top of each `SKILL.md`.
