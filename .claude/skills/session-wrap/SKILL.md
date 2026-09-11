---
name: session-wrap
description: Writes back what changed and closes the session, in Notion. Run before you stop, even for a short or inconclusive session, only when typed.
---

> Ported from the Notion ForClaude page `/session-wrap` (root: "Notion <->
> Claude loop"). Notion is canonical — if you want different behaviour,
> edit the page there and rebuild this file from it; every surface then
> inherits the change.

## What it does

Writes back what changed, so the next session can start from it.

## When to run it

Before you stop. Even if the session was short, and especially if it was
inconclusive — an inconclusive session that is written down is worth more
than a good one that is not.

## Where things are

Everything lives under one root page — it arrives as **Notion ↔ Claude
loop** with a number appended, and it may get renamed, so navigate by the
root URL in `CLAUDE.md`, not by title. Each row in the Projects database
carries a **Hub** link to that project's page; the Hub page holds the
**Current State** child page and the inline **Session Log** this skill
writes to.

## Procedure

1. **Find the project and the open row.** If the conversation is already
   about one project, use it; otherwise ask. Open its Hub page and take the
   Session Log row with Status Open. If there is not one, create it now and
   say so, giving it a **Number** one higher than the highest already in
   this log. If the Hub is empty, will not open, or lands on a page outside
   this workspace, it did not survive duplication — find the project page
   by name under the root page, set the row's Hub to it, say you have done
   it, and carry on.
2. **Say what happened, and check it.** Summarise the session in a few
   lines and show the user before writing. They correct it; you do not
   argue.
3. **Update the to-dos.** Read them from the Global To-Do; if that query
   hits the usage limit, query the **Open to-dos** view on the Hub page
   **in view mode** instead — view queries are not metered — and say which
   route you used. Fetching the Hub page does not return the view's rows,
   so never read an empty page fetch as an empty list. To reach the view:
   the Hub fetch lists the linked database block with its own URL; fetch
   that; it lists the views as `view://<id>`; the view URL is the database
   URL plus `?v=` and that id with dashes removed. Read the id off the
   fetch, never guess it from the view's name. The same view-mode route
   covers the Projects register and the Session Log if those reads are
   metered out. Then mark anything finished as Done and set its
   **Done date** to today — without that there is no way to ask later what
   you actually got through this week, because Status alone does not say
   when. Add anything new that came up, with Project set. If something
   turned out to be blocked, set `Blocked by`. Do not silently close a task
   the user did not say was finished.
4. **Write the row.** Outcome (what actually happened, including what did
   not get done), Next (the single first thing the next session should
   pick up), Blockers (or "None"), Status Closed.
5. **Rewrite Current State.** Replace the page, do not append to it. Three
   sections: where things stand, what is open, next. Write it for someone
   who has forgotten everything — because in a fortnight, that is who reads
   it.
6. **Stamp the project row.** Set **Last session** on the row in Projects
   to today. Nothing automatic does this — the session happened on the Hub
   page, not on the row — and `/session-start` orders the project list by
   it, so a project skipped here quietly sinks.
7. **Confirm, from a re-read.** Fetch the row and the Current State page
   back and quote their URLs. Confirm only what the re-read shows; a write
   you described but did not make is not a write, and this step exists to
   make that impossible to miss.

## Rules

- **A read or a write that failed is not a done thing.** If you could not
  reach a page, could not run a query, or could not make a change, say
  which and why. Never close a session reporting work you did not manage
  to land, and never substitute something adjacent and describe it as the
  thing asked for.
- **Next is one thing, not a list.** A list is a way of not deciding.
- **Be honest in Outcome.** "Tried X, it did not work, do not try it again"
  is more valuable to the next session than a tidy summary.
- **Current State is replaced, never appended.** It describes the present.
  A log of the past is what the Session Log is for.
- Never write Current State without also closing the row, or the two fall
  out of step.

## Code-only additions (not part of the ported page)

- Once the Session Log row is closed in step 4, delete the marker file
  `.claude/.session-open` if it is present. This is what tells the Stop
  hook in `.claude/settings.json` that nothing is left open.
