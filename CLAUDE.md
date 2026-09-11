# CLAUDE.md — <PROJECT NAME>

Notion is the single source of truth for this project. Everything in this
file library is a pointer and a cache, never a second copy of state — if
this file and Notion ever disagree, Notion wins.

## Identity

<Filled at the end of setup: who you are, what you do, how you like to
work — how you want to be pushed back on, what you never want asked, where
finished files go. Not filled yet on a fresh clone.>

## Notion Pages

Root page (the duplicated "Notion ↔ Claude loop" page):
  <PASTE THE URL OF YOUR "Notion ↔ Claude loop" PAGE>

Databases, discovered from the root and confirmed before anything is
written:
- Projects: `<PASTE PROJECTS DATABASE ID>`
- Global To-Do: `<PASTE GLOBAL TO-DO DATABASE ID>`
- Notes: `<PASTE NOTES DATABASE ID>`

A project's Hub page (Current State, Session Log, filtered views) is read
from the **Hub** property on its row in Projects — never hardcode a Hub URL
here, it is discovered fresh every session, because it is the one property
Notion does not repoint on duplication.

## Notion write conventions

- Database entries: `parent: {type: "data_source_id", data_source_id: "<id>"}`
- Page children: `parent: {type: "page_id", page_id: "<id>"}`
- Date fields: set the field's `start` and `is_datetime` separately, never
  a bare string.
- Multi-select properties: a JSON array of strings, e.g. `["Idea","Question"]`.
- Never write an inline `[ ]` checkbox to-do, on any page. To-dos live in
  the Global To-Do database only — an inline checkbox is invisible to
  `/session-start` and the rest of this loop, and it is how a to-do gets
  lost without anyone noticing.

## The rest of this file library

- `SURFACE.md` — what this surface (Code) can do that Chat and Cowork cannot.
- `ARCHITECTURE.md` — the memory map: root page, three databases, one Hub
  per project.
- `TODO.md` — the to-do contract. There is no local task list; it points at
  Notion and says why.

This file indexes the other three. It does not inline them.

## Commands

`/session-start`, `/session-wrap`, `/capture`, `/note`, `/project` — typed
when wanted, never run unprompted. An ordinary question gets an ordinary
answer. If a typed command has no matching skill installed, say so in the
first line and stop — never improvise it from memory.

## The single-write contract

Every write this loop makes lands in Notion. Nothing it does creates a
second copy of state anywhere else.
