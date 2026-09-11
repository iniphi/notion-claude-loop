---
name: project
description: Builds a whole new project in one move - register row, Hub page, Current State, filtered views, Session Log. No manual step. Only when typed.
---

> Ported from the Notion ForClaude page `/project` (root: "Notion <->
> Claude loop"). Notion is canonical — if you want different behaviour,
> edit the page there and rebuild this file from it; every surface then
> inherits the change.

## What it does

Makes a new project: the register row, its Hub page, the link between them,
the two filtered views, its Current State and its session log.

## Procedure

1. **Ask for two things**: the project name, and one line on what it is.
   Do not ask for more.
2. **Create the Hub page** as a child of the root page (the one in
   `CLAUDE.md`, whatever it is now called), titled with the project name.
   The connector can only parent to the root, so the new page lands at the
   foot of the root page — step 8 moves it into place. Do not try to
   create it inside the column or callout that holds the first project;
   that block is not addressable and the create will fail. A short
   orientation paragraph, then a line naming what sits below it, and
   nothing else. **Do not write Current State content into this page
   body.** Current State is a child page, made in step 4. A copy of it in
   the hub body is never read and never updated, and it will sit there
   contradicting the real one within a fortnight.
3. **Create the row** in the Projects database: Name, Description, Status
   Active, and **Hub** set to the new page's URL. Set North Star if the
   user offered one; leave it empty rather than inventing it. Keep the row
   to its properties; the page is the project.
4. **Create a `Current State` child page** on the Hub. Three empty
   sections: where things stand, what is open, next. Say plainly that it
   is a placeholder until the first session closes.
5. **Create the filtered to-do view** on the Hub — a linked view of the
   Global To-Do, filtered to `Project` contains the new row and `Status`
   is neither Done nor Binned. Name it "Open to-dos".
6. **Create the filtered notes view** on the Hub — a linked view of Notes
   filtered to `Project` contains the new row. Name it "Notes".
7. **Create a `Session Log` database** on the Hub with the same columns as
   the one on the first project: Session, Number, Date, Surface
   (Chat / Cowork / Code / Design / Hand), Status (Open / Closed), Goals,
   Outcome, Next, Blockers. It is a separate database — one log per
   project is the design — so only the columns need to match, not the
   page around it.
8. **Add it to the home page.** The create in step 2 left the new Hub as a
   child-page block at the foot of the root page. Notion refuses a page
   link pasted into a callout as new content, so do not insert one —
   **move that existing child-page block** into the Contents callout,
   beside the projects already listed, and re-read the root page to
   confirm it sits there and nowhere else. Nothing does this
   automatically, and a home page that lists only the first project stops
   being the way in.
9. **Confirm** with the project's link, and say the next move is
   `/session-start`.

## Rules

- The filters bind to **the row**, not to the project's name, and the row
  finds its page through **Hub**. A renamed project keeps working; a moved
  page needs the Hub link updated.
- Do not copy to-dos or notes into the project. They live in the two
  shared databases and are only ever *seen* here — that is what makes one
  list work across many projects.
- Never create a second Global To-Do or Notes database. There is exactly
  one of each, forever.
- If the user asks for a project that already exists, open it instead of
  making a duplicate.
