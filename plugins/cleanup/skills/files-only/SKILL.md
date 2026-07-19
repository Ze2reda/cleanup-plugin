---
name: files-only
description: Removes only the scratch files created during this session.
---

# Cleanup — Files Only

Removes temporary/scratch files created during this session from the working
directory. Leaves tabs and cache untouched — use `/cleanup:tabs-only` or
`/cleanup:cache-only` for those.

## What it does
- Removes only clearly-temporary artifacts created **this session**: drafts,
  intermediates, `.tmp` files, partial or duplicate downloads, working notes
  generated purely as scratch.
- Never deletes or modifies: any file the user uploaded, any file that
  existed before the session started, or any file it's not certain it
  created itself — even if it looks unused.
- If the current task's own instructions name specific protected files (a
  log, a running record, source documents), honors those on top of the
  defaults above.

## Guardrails
- Only touches files — never closes tabs or clears cache.
- When unsure whether something is scratch or a deliverable, leaves it in
  place and flags it instead of deleting it.
- Reports back plainly what was removed, what was left in place, and why.
