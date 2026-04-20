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

## Format differences between the two manifests

Each ecosystem has its own schema. Both files list the same plugins, but the field names and source formats differ.

### Claude Code (`.claude-plugin/marketplace.json`)

```json
{
  "name": "qa-vault",
  "plugins": [
    {
      "name": "codelore",
      "source": { "source": "github", "repo": "qa-vault/codelore" },
      "description": "...",
      "category": "development",
      "tags": ["..."]
    }
  ]
}
```

### Codex (`.agents/plugins/marketplace.json`)

```json
{
  "name": "qa-vault",
  "plugins": [
    {
      "name": "codelore",
      "source": { "source": "url", "url": "qa-vault/codelore" },
      "category": "development"
    }
  ]
}
```

**Authoritative Codex schema**: `codex-rs/core-plugins/src/marketplace.rs` in [openai/codex](https://github.com/openai/codex). Required fields at marketplace level: `name`, `plugins`. Required per plugin: `name`, `source`. Source variants: `local`, `url`, `git-subdir` (plus string shorthand for local). The `url` variant accepts full URLs and GitHub shorthand (`owner/repo`).

**Codex rejects unknown fields gracefully** — unknown fields are ignored. Don't add Claude-Code-specific fields like `description` or `tags` to the Codex file; they won't do anything but clutter the manifest.

## Cross-platform invariants

1. **Every plugin must be listed in BOTH manifest files.** Missing from one means uneven availability.
2. **Plugin `name` must match** across both files and the plugin's own `plugin.json` files.
3. **Plugin repo path** (`qa-vault/<repo>`) must match the actual GitHub repo location in both entries.
4. **If Codex adds new source variants** (e.g., `git-subdir`, ref pinning), update the Codex file here — Claude Code doesn't read this one.

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
     "name": "<plugin-name>",
     "source": { "source": "url", "url": "qa-vault/<plugin-name>" },
     "category": "development"
   }
   ```
3. Update the README plugin table with a link to the plugin repo.
4. Commit, push.

## Removing or renaming a plugin

- Remove its entry from BOTH manifest files.
- Update the README plugin table.
- If the plugin repo is renamed, update the repo/url field in both entries.

## Versioning

The marketplace itself is a simple catalog and doesn't need aggressive versioning. Tag optional.

## Companion plugins

Each plugin listed here has its own repo under `qa-vault/` with its own `AGENTS.md`. Release cadence of a plugin is independent from this marketplace — consumers auto-discover new plugin versions via the plugin's own manifest, not via this catalog.
