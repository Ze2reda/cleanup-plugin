---
name: tabs-only
description: Closes only the browser tabs opened during this session.
---

# Cleanup — Tabs Only

Closes browser tabs opened during this session. Leaves cache and files
untouched — use `/cleanup:cache-only` or `/cleanup:files-only` for those.

## What it does
- Closes only tabs opened **during this session** — search pages, articles,
  forms, anything the current task opened.
- Never closes: a tab the user already had open before the session started; a
  tab that's mid-task and waiting on the user (an unfinished form, an unsolved
  CAPTCHA, a confirmation dialog); a messaging/email tab if there's any chance
  it's still in use.
- If no tab-management tool is available in this environment, doesn't
  improvise a workaround (keyboard shortcuts, closing whole windows) —
  instead lists which tabs were opened this session and says which are safe
  to close manually.

## Guardrails
- Only touches tabs — never clears cache or deletes files.
- When unsure whether a tab belongs to this session, leaves it open and flags
  it rather than guessing.
- Reports back plainly what was closed, what was left open, and why.
