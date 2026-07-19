---
name: dry-run
description: Previews cleanup without closing, clearing, or deleting anything.
---

# Cleanup — Dry Run

A preview-only pass. Lists every tab that *would* be closed, every cache item
that *would* be cleared, and every file that *would* be removed if
`/cleanup:full` were run — without taking any action.

## What it does
- Scans the current session for tabs it opened, cache/temp data it created,
  and scratch files it generated.
- Reports each one, grouped by category (Tabs / Cache / Files), with a
  one-line reason it's considered session-created rather than pre-existing.
- Takes **no action of any kind**. Nothing is closed, cleared, or deleted by
  this command — it only reports.

## Guardrails
- Same eligibility rule as `/cleanup:full`: only lists items this session
  created or opened. Anything ambiguous is reported as "unsure — left out of
  this preview" rather than guessed at either way.
- Ends with a clear next step: run `/cleanup:full` to actually do all of it, or
  a narrower command — `/cleanup:tabs-only`, `/cleanup:files-only`,
  `/cleanup:cache-only` — to do just one part.
