---
name: capture
description: Turns a passing sentence into a to-do in the Global To-Do database, without stopping what you were doing. Only when typed.
---

> Ported from the Notion ForClaude page `/capture` (root: "Notion <->
> Claude loop"). Notion is canonical — if you want different behaviour,
> edit the page there and rebuild this file from it; every surface then
> inherits the change.

## What it does

Turns a passing sentence into a to-do without stopping what you were doing.

## Procedure

1. Take what the user said and write it as a **Name** starting with a verb.
   Keep it terse.
2. Put the detail in **Notes**: what it means, and how you would know it is
   done. One to three lines.
3. Set **Project** if it is obvious from context. If it is not, ask — once,
   briefly — or leave it empty rather than guessing wrong.
4. Set **Priority**. Default to Medium unless they signalled urgency.
5. Set **Surface** and **Effort** if you can infer them honestly. Surface
   means where the work will be done, not where you happen to be running →
   a to-do about files belongs to Cowork even if you are on Chat when you
   capture it. Leave either empty rather than guessing.
6. Confirm in one line. Do not read the whole row back.

## Rules

- Do not interrogate. One question maximum, and only if Project is
  genuinely ambiguous.
- Do not set a deadline the user did not give you.
- If it is not an action, it is a note. Use `/note` instead.
