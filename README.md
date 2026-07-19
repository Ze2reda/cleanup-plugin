# Cleanup Plugin Marketplace

A GitHub-hosted marketplace for the `cleanup` plugin — a general-purpose
"tidy up after yourself" tool for Claude (closes tabs, clears cache, removes
scratch files created during a session).

This repo can be added directly as a plugin source. You don't need to
download or unzip anything by hand — Claude fetches it straight from GitHub.

## Install it (for anyone with this repo URL)

**In Cowork or Claude Code**, run:
```
/plugin marketplace add Ze2reda/cleanup-plugin
/plugin install cleanup@cleanup-marketplace
```

That's it — `/cleanup:full`, `/cleanup:dry-run`, `/cleanup:tabs-only`,
`/cleanup:files-only`, and `/cleanup:cache-only` are now available.

**In Claude Cowork's UI**, alternatively: Customize → Plugins → Browse
plugins → Add a marketplace by URL → paste this repo's URL.

## What's in this repo

```
.claude-plugin/marketplace.json   ← lists the plugin(s) in this repo
plugins/cleanup/                  ← the actual plugin
├── .claude-plugin/plugin.json
├── skills/
│   ├── full/SKILL.md
│   ├── dry-run/SKILL.md
│   ├── tabs-only/SKILL.md
│   ├── files-only/SKILL.md
│   └── cache-only/SKILL.md
└── README.md                     ← full docs on what each command does
```

See `plugins/cleanup/README.md` for what each command actually does and its
safety guarantees.

## Updating
Push changes to this repo, then anyone who's installed it runs
`/plugin marketplace update` to pick up the latest version.
