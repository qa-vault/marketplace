# Agent Context: qa-vault marketplace

This repository is a **dual-ecosystem plugin catalog** — the entry point for installing `qa-vault` plugins in both Claude Code and Codex CLI. It contains only manifests; no plugin code lives here.

## Repository layout

```
marketplace/
├── .claude-plugin/marketplace.json    # Claude Code catalog
├── .agents/plugins/marketplace.json   # Codex catalog
├── README.md
├── LICENSE
└── AGENTS.md                           # this file
```

## What this repo is

A catalog that points at plugin repos under the `qa-vault` GitHub org. Users add this marketplace once and install any listed plugin by name:

- Claude Code: `/plugin marketplace add qa-vault/marketplace` → `/plugin install <name>@qa-vault`
- Codex: `codex marketplace add qa-vault/marketplace` → `/plugins install <name>`

## Cross-platform invariants

1. **Every plugin must be listed in BOTH catalog files.** Adding a plugin to one but not the other creates uneven availability across tools.
2. **Plugin name must match** between the two manifests and the plugin's own `plugin.json` files.
3. **Plugin repo path** (`qa-vault/<repo>`) must match between both manifests and the actual GitHub repo location.

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
2. Add the matching entry to `.agents/plugins/marketplace.json` under `plugins[]`:
   ```json
   {
     "source": { "source": "github", "repo": "qa-vault/<plugin-name>" },
     "interface": { "displayName": "<plugin-name>" }
   }
   ```
3. Update the README plugin table with a link to the plugin repo.
4. Commit, tag a version bump if desired, push.

## Removing or renaming a plugin

- Remove its entry from BOTH manifest files.
- Update the README plugin table.
- If the plugin repo is renamed, update the `repo` field in both entries.

## Versioning

The marketplace itself is a simple catalog and doesn't need aggressive versioning. Bump the top-level `metadata.version` in `.claude-plugin/marketplace.json` on structural changes (added/removed plugins, field schema changes). Tag optional.

## Companion plugins

Each plugin listed here has its own repo under `qa-vault/` with its own `AGENTS.md`. Release cadence of a plugin is independent from this marketplace — consumers auto-discover new plugin versions via the plugin's own manifest.
