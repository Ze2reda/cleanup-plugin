---
name: full
description: Closes tabs, clears cache, and removes files from this session.
---

# Cleanup — Full

Runs a complete cleanup: closes browser tabs opened this session, clears any
browser cache/temp data created this session, and removes scratch files
created this session.

For a preview instead of real changes, use `/cleanup:dry-run`. For just one
category, use `/cleanup:tabs-only`, `/cleanup:files-only`, or
`/cleanup:cache-only` instead of this one.

## What it does

### Tabs
- Closes only tabs opened **during this session** — search pages, articles,
  forms, anything the current task opened.
- Never closes: a tab the user already had open before the session started; a
  tab that's mid-task and waiting on the user (an unfinished form, an unsolved
  CAPTCHA, a confirmation dialog); a messaging/email tab if there's any chance
  it's still in use.
- If no tab-management tool is available in this environment, doesn't
  improvise a workaround — instead lists which tabs were opened this session
  and says which are safe to close manually.

### Cache / temporary browser data
- If a tool exists for clearing cache/cookies/site data for this session's
  browsing, uses it, scoped as narrowly as the tool allows.
- If no such tool is available, doesn't attempt it via a workaround — says
  plainly that cache-clearing isn't available here, and only if useful, points
  to where the user could do it themselves.
- Never clears cookies/site data that would log the user out of something
  they're actively using, without flagging that first.

### Working-directory / scratch files
- Removes only clearly-temporary artifacts created **this session**: drafts,
  intermediates, `.tmp` files, partial or duplicate downloads.
- Never deletes or modifies: any file the user uploaded, any file that existed
  before the session started, or any file it's not certain it created itself.
- When unsure whether something is scratch or a deliverable, leaves it and
  flags it instead of deleting it.

## Guardrails
- Only touches things this session created or opened — never guesses in the
  direction of deleting/closing/clearing something it's unsure about.
- Never overrides another active rule in the conversation (a hard stop, an
  unfinished CAPTCHA, a form left intentionally filled in for the user).
- Honors any additional protected files/folders named by the current task's own
  instructions, on top of these defaults.
- Reports back plainly what was closed/cleared/removed, what was left in place
  and why, and anything needing manual follow-up.
