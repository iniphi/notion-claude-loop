---
name: session-start
description: Opens a working session by reading where the last one left off, from Notion. Run first, before anything else, only when typed.
---

> Ported from the Notion ForClaude page `/session-start` (root: "Notion <->
> Claude loop"). Notion is canonical — if you want different behaviour,
> edit the page there and rebuild this file from it; every surface then
> inherits the change.

## What it does

Opens a working session by reading what the last one left behind.

## When to run it

First thing, every time you sit down — before asking for anything else.

## Where things are

Everything lives under one root page. It arrives called **Notion ↔ Claude
loop** with a number appended by duplication, and it may get renamed — so
navigate by the root URL in `CLAUDE.md`, never by title. Projects, Global
To-Do and Notes are databases on it. Each row in Projects carries a **Hub**
link to that project's page; the Hub page holds a **Current State** child
page, an inline **Session Log** database, and filtered views of the two
lists. The row is the register entry; the Hub page is the project.

## Procedure

1. **Find the project.** If the conversation is already about one project,
   use it. Otherwise read the Projects database, list the Active rows with
   the most recent **Last session** first, and ask which one. A row with no
   Last session has not had one yet — say so rather than silently dropping
   it to the bottom. Then open the page in that row's Hub property → that
   page is the project. **If the Hub is empty, will not open, or lands on a
   page outside this workspace, it did not survive duplication** — Notion
   copies a URL property's text verbatim instead of repointing it, so on a
   fresh install it is either blank or still aimed at the original author's
   page. A Hub that opens cleanly is not proof it is right: check the page
   it reaches actually sits under this root before trusting it. Find the
   project page by name under the root page, set the row's Hub to that URL,
   tell the user you have done it, and carry on. It is a one-time repair on
   a freshly duplicated workspace, not an error. **If the Projects query
   hits the usage limit**, read the register through its default view in
   view mode instead, and say so.
2. **Read Current State.** Open the Current State child page on the Hub in
   full. This is the primary source, and it outranks anything remembered
   from earlier in the conversation.
3. **Read the open to-dos.** From the Global To-Do, take rows where Project
   is this project and Status is neither Done nor Binned. Check
   `Blocked by`: if it points at a task that is not yet Done, that row is
   not actionable — report it as blocked rather than proposing it. **If the
   query does not come back** — a usage limit, a timeout, a permission
   error — do not stop and do not guess. Fall back to querying the **Open
   to-dos** view on the Hub page **in view mode** — a view query is not
   metered, a database query is. Fetching the Hub page does **not** return
   the view's rows; it returns an empty database tag, and reading that as
   "no to-dos" is the exact failure the rules below forbid. The view sits
   inside the linked database block titled *View of Global To-Do* on the
   Hub. **How to reach it, exactly:** fetching the Hub page lists that
   block as a database tag with its own URL → fetch that URL → the result
   lists the database's views, each with a name and an id in the form
   `view://<id>` → the view URL is the database URL with `?v=` and that id
   (dashes removed) appended → query it with the tool's view mode. Never
   guess the id from the view's name; it is only ever read off the fetch.
   Say which route you used and why. If both routes fail, give the count as
   unknown and name what you could not read. Never report zero to-dos on
   the strength of a read that failed.
4. **Read the last session.** Take the most recent row in the Session Log
   on the Hub page and read its Next and Blockers. Same fallback as step 3:
   if the query is metered out, read the log's default view in view mode.
   **On Blocked by:** the relation is not cleared when the blocker is
   marked Done, so a row can show Blocked by and be actionable. Check the
   blocker's Status; if it is Done, treat the row as actionable and clear
   the stale Blocked by so the view stops lying.
5. **Give the brief**, short, in this order. **Its first line is always**
   `SESSION START — <project name> — <today's date>`, on its own, before
   anything else. This line is the proof that the skill is running rather
   than being improvised → the user checks for it, so never drop it,
   reword it or bury it under a greeting.
   - where you left off, from Current State
   - what the last session said to pick up next
   - the open to-dos, actionable ones first, with a count
   - anything blocked, and what it is waiting on
6. **Stop and ask.** Do not start work. Ask what they want to do this
   session.
7. **Open the log row.** Once they answer, create a Session Log row:
   **Number** one higher than the highest Number already in this log,
   Session titled `Session <Number> - <today's date>`, Date today, Surface
   whichever you are running on, Status Open, Goals one line each. Take the
   number from the Number property. Never work it out by reading a number
   out of a title — that is how logs end up with two Session 7s. Then quote
   the new row's URL from the create result; a row you have not got a URL
   for does not exist.

## Rules

- Never invent state. If Current State is empty, say it is empty.
- Run only when asked. This skill fires when the user types
  `/session-start`, not because a chat has opened. A chat that asks an
  ordinary question gets an ordinary answer.
- **A read that failed is not an empty result.** If a page or a query does
  not come back, name what you could not read and why, and carry on with
  the rest of the brief marked incomplete. Reporting nothing-found for
  something you never saw is the one failure that makes the whole loop
  untrustworthy, because it looks exactly like good news.
- Never skip the brief because the conversation appears to know already.
  Not having to remember is the entire point.
- One session, one row. If a row is still Open, resume it rather than
  opening a second.

## Code-only additions (not part of the ported page)

- Also read local `git status` and the last three commits, and fold them
  into the brief alongside the Notion state.
- Once the Session Log row is opened in step 7, create an empty marker
  file at `.claude/.session-open`. The Stop hook in `.claude/settings.json`
  checks for this file and nudges you to run `/session-wrap` if it is still
  present when you close the terminal.
