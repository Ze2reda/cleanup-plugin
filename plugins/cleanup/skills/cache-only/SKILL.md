---
name: cache-only
description: Clears only the browser cache/temp data from this session.
---

# Cleanup — Cache Only

Clears browser cache, cookies, or temporary site data created during this
session. Leaves tabs and files untouched — use `/cleanup:tabs-only` or
`/cleanup:files-only` for those.

## What it does
- If a tool exists for clearing cache/cookies/site data for this session's
  browsing, uses it, scoped as narrowly as the tool allows (just the sites
  visited this session, not the user's whole browser profile).
- If no such tool is available, doesn't attempt it via a workaround — says
  plainly that cache-clearing isn't available in this environment, and only
  if useful, points to where the user could do it themselves (e.g. the
  browser's own "clear browsing data" settings), without taking action there.
- Never clears cookies/site data that would log the user out of something
  they're actively using, without flagging that first.

## Guardrails
- Only touches cache/site data — never closes tabs or deletes files.
- Reports back plainly what was cleared, what was left alone, and why.
