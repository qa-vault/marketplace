# Agent Context: qa-vault marketplace

This repository is a **Claude Code plugin catalog** — the entry point for installing `qa-vault` plugins via a single marketplace. It contains only manifests; no plugin code lives here.

## Why Claude Code only

Codex CLI's marketplace format only supports `source: "local"` — it cannot list plugins from external repos. That's incompatible with a polyrepo distribution model, so this catalog is Claude-Code-only. For Codex, each `qa-vault` plugin must be installed via its own repo (e.g., `codex marketplace add qa-vault/codelore`). Each plugin repo carries its own `.agents/plugins/marketplace.json` pointing at itself locally.

If Codex later adds a remote source variant (`git`, `github`, `url`, etc.), reconsider adding a Codex marketplace file here.

## Repository layout

```
marketplace/
├── .claude-plugin/marketplace.json    # Claude Code catalog
├── README.md
├── LICENSE
└── AGENTS.md                           # this file
```

## What this repo is

A catalog that points at plugin repos under the `qa-vault` GitHub org. Users add this marketplace once and install any listed plugin by name:

- Claude Code: `/plugin marketplace add qa-vault/marketplace` → `/plugin install <name>@qa-vault`

## Invariants

1. **Plugin `name` must match** the plugin's own `.claude-plugin/plugin.json`.
2. **Plugin repo path** (`qa-vault/<repo>`) must match the actual GitHub repo location.
3. **Don't list plugins here that don't have Claude Code support.** Codex-only plugins belong in their own repos; users add them individually to Codex.

## Adding a new plugin to the catalog

1. Add an entry to `.claude-plugin/marketplace.json` under `plugins[]`:
   ```json
   {
     "name": "<plugin-name>",
     "source": { "source": "github", "repo": "qa-vault/<plugin-name>" },
     "description": "<one-line summary>",
     "category": "development",
     "tags": ["..."]
   }
   ```
2. Update the README plugin table with a link to the plugin repo.
3. Commit, push.
4. In the plugin's own repo, ensure `.agents/plugins/marketplace.json` exists for Codex users (see that repo's AGENTS.md).

## Removing or renaming a plugin

- Remove its entry from `.claude-plugin/marketplace.json`.
- Update the README plugin table.
- If the plugin repo is renamed, update the `repo` field in the entry.

## Versioning

The marketplace itself is a simple catalog and doesn't need aggressive versioning. Bump the top-level `metadata.version` in `.claude-plugin/marketplace.json` on structural changes (added/removed plugins, field schema changes). Tag optional.

## Companion plugins

Each plugin listed here has its own repo under `qa-vault/` with its own `AGENTS.md` and release cadence. Consumers auto-discover new plugin versions via the plugin's own manifest, not via this catalog.
