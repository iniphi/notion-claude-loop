# SURFACE.md — what Code adds

The Code surface is the same loop as Chat and Cowork, running in a terminal
with local files, git and hooks underneath it. It is optional — the loop is
complete without it. If you would rather run the loop from Chat or Cowork
only, you do not need this repository at all.

> Everything here writes to Notion only. Notion stays the single source of
> truth. The local files this surface keeps are a working profile and a
> cache, never a second copy of memory.

## What Code can do that Chat and Cowork cannot

- **Local files under version control.** This directory is a git repo —
  history, branches, diffs.
- **File-backed skills**, in `.claude/skills/`. The five loop skills run as
  real files rather than instructions injected per prompt.
- **Hooks.** A Stop hook nudges you if you close the terminal with a
  session still open in Notion, or a dirty working tree. See
  `.claude/settings.json`.
- **A terminal.** Running code, migrations, anything a developer wants —
  outside the scope of the loop itself.

## One Code-only addition to `/session-start`

On this surface, `/session-start` also reads local `git status` and the
last three commits, and folds them into the session brief. Chat and Cowork
have no equivalent — there is nothing local for them to read.

## Entry point

This repository is a standalone entry point for the Code surface. It does
not require the loop to already be running on Chat or Cowork first — the
setup prompt in `README.md` discovers your Notion structure directly. If
you *have* already set up Chat or Cowork, this surface reads the same
Notion pages they do; nothing needs migrating.
