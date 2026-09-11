# Notion ↔ Claude loop — Code surface

This is the Code-surface companion to the **Notion ↔ Claude loop**: a
second brain that lives in Notion, with Claude reading and writing it
through five skills. If you only ever want to run the loop from Chat or
Cowork, you do not need this repository — it exists for people who want
local files, git history, and file-backed skills as well.

Notion is the single source of truth. Nothing in this repository is a
second copy of your state — see `CLAUDE.md` for the one-line version of
that rule, and `ARCHITECTURE.md` for the full shape.

## Before you start

- A paid Claude tier, with Claude Code installed
  (`npm i -g @anthropic-ai/claude-code`, or from claude.com/code).
- A Notion account, with the **Notion ↔ Claude loop** page duplicated into
  your workspace. If you have not done that yet, duplicate it before
  continuing here.
- A local, non-synced folder for this repository. Keep it off OneDrive,
  Dropbox and iCloud — git is your history, and a sync client will fight
  it.

## Set up

1. **Get your own copy of this repository.** If you are reading this on
   GitHub, use the "Use this template" button — that gives you a clean
   history rather than a fork of this one. Clone your copy into the local
   folder from the prerequisites above.
2. **Open Claude Code in that folder.** The Notion MCP server is already
   declared in `.mcp.json`; the first time you run a command it will ask
   you to authorise it with `/mcp`. That browser sign-in is the one
   unavoidable manual step.
3. **Paste this once**, with your root page URL filled in:

   ```
   Set up this Day0 repo against my Notion "Notion <-> Claude loop" page.
   The root page is:
     <PASTE THE URL OF YOUR "Notion <-> Claude loop" PAGE>

   The local files (CLAUDE.md, SURFACE.md, ARCHITECTURE.md, TODO.md) and
   the five skills under .claude/skills/ already exist in this repo - do
   not rewrite them. Your job is narrower:

   1. Confirm you can fetch the root page. If you cannot, stop and say so
      rather than guessing.
   2. Discover the Projects, Global To-Do and Notes database IDs from the
      root page, and confirm each with me - title and ID - before writing
      anything.
   3. Fill the placeholder slots in CLAUDE.md's Notion Pages block with the
      discovered IDs and root URL. Do not touch anything else in the file.
   4. Verify the loop: ask me which project to check, read its Current
      State, and say where I left off. Dry-run /session-start and show
      that it reads Notion. (Local git state will be empty on a fresh
      repo - that is expected, not a failure.)
   5. Ask me who I am, what I do, and how I like to work, and write the
      answers into CLAUDE.md under Identity.
   6. Commit the filled-in CLAUDE.md as "chore: wire repo to my Notion
      workspace".
   ```

4. **Check it landed**, in a fresh terminal or a fresh chat — not the one
   that just ran setup, because it has read its own skills and could be
   running from memory of them rather than the installed files. Type
   `/session-start` and nothing else. If the first line of the reply
   begins `SESSION START`, you are running. If it does not, the skills in
   `.claude/skills/` are not being picked up — check they are named
   exactly `session-start`, `session-wrap`, `capture`, `note`, `project`
   and sit one folder each under `.claude/skills/`.

## What's in here

| File | Purpose |
|---|---|
| `CLAUDE.md` | Identity, the Notion page/database IDs, write conventions. Read every message. |
| `SURFACE.md` | What Code can do that Chat and Cowork cannot. |
| `ARCHITECTURE.md` | The memory map: root page, three databases, one Hub per project. |
| `TODO.md` | The to-do contract - why there is no task list in this repo. |
| `.claude/skills/*/SKILL.md` | The five loop skills, ported from the same Notion pages Chat and Cowork read. One source, three renderings. |
| `.claude/settings.json` | The Stop hook that nudges you to `/session-wrap` before you close a session still open. |
| `.mcp.json` | Declares the Notion MCP server for this project. |

## Keeping this in sync

The skill bodies here were ported from Notion, not written independently.
If you change how a skill behaves, the durable fix is to edit the Notion
ForClaude page and re-port it here — see the provenance note at the top of
each `SKILL.md`. Editing only the local copy works, but it will drift from
what Chat and Cowork run.
