# Cleanup Plugin

A general-purpose "tidy up after yourself" plugin for Claude. It isn't built
for one specific workflow (job search, coding, research, etc.) — every
command applies the same rule no matter what you were doing beforehand:
**only touch what this session created.**

Unlike a plain Skill (one folder = one command), a plugin bundles several
named commands behind a single install. This one bundles five, all under the
`cleanup:` namespace.

---

## The five commands

| Command | What it does |
|---|---|
| `/cleanup:full` | Full cleanup — tabs + cache + files — and actually does it |
| `/cleanup:dry-run` | Preview only — lists what *would* be closed/removed/cleared, touches nothing |
| `/cleanup:tabs-only` | Browser tabs only |
| `/cleanup:files-only` | Working-folder scratch files only |
| `/cleanup:cache-only` | Browser cache/temp data only |

Each shows up in the command menu with a short, single-purpose description —
no long paragraph, since each command only has to explain one thing.

---

## How it works

**Trigger.** Claude loads every bundled skill's short description at session
start (minimal context cost). It reads a skill's full instructions only when
your message matches that skill's description, or you invoke it directly by
name (e.g. `/cleanup:tabs-only`).

**Decision process, once loaded.** For every tab, file, or cache item a
command considers touching, it asks one question: *"Did this session create
this?"*
- Yes → eligible to close/clear/delete.
- No, or unsure → left alone, and mentioned in the final report instead of
  guessed at.

**Reporting.** Every run — real or dry-run — ends with a plain-language
summary: what was closed/removed/cleared, what was deliberately left in
place and why, and anything that needs your manual follow-up.

---

## Installing (one upload, not five)

**Claude Cowork (desktop app):**
1. Download this plugin folder as a zip.
2. In Cowork, go to **Plugins** (left sidebar) → **+** → **Upload plugin**.
3. Drag in the zip, click **Upload**.
4. All five commands are now available under `/cleanup:`.

**Claude Code CLI:**
```
claude plugin marketplace add <path-or-url-to-this-repo>
claude plugin install cleanup@cleanup
```

Note this uses the **Plugins** install path, not the plain **Skills** upload
panel — a plugin is a different, bundled format from a single `SKILL.md`.

---

## Safety guarantees (all five commands)
- Only closes/deletes/clears things **this session** created or opened.
- Never closes a tab that's mid-task and waiting on you (an unfinished form,
  an unsolved CAPTCHA, an open confirmation dialog).
- Never overrides another active rule in the conversation — if cleanup would
  interfere with a hard stop or an in-progress step defined elsewhere, it
  skips that item and says so explicitly rather than clearing it silently.
- When genuinely unsure whether something belongs to this session, defaults
  to leaving it in place and flagging it — never guesses toward deleting.

## Known limitation
Closing tabs and clearing cache both depend on a suitable tool being
available in the environment you're running in. If no such tool exists, none
of these commands will attempt a workaround (like blind keyboard shortcuts) —
they'll list what they would have closed/cleared and tell you what to do
manually. This is a real, current limitation, not a hypothetical one.

## Extending it for a specific workflow
Each command's only default protection rule is *"only touch what this
session created."* If a specific project needs stronger guarantees — e.g.
"never touch this particular log file, ever" — add that as an explicit
instruction in that project's own instructions file. These commands are
written to respect additional protections layered on top of them; they don't
need to know about every possible project in advance.

**Example** (from a job-search automation that uses this plugin): the
project's own instructions state that a de-dup log, every per-application
handoff file, and the candidate's CV/resume folders must never be touched by
cleanup, regardless of which command runs — on top of the plugin's own
default rule. That pattern works for any project: keep the plugin generic,
put the project-specific exclusions in the project's own instructions.
