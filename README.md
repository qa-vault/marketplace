# qa-vault marketplace

A catalog of **Claude Code** plugins published by `qa-vault`.

This repo doesn't contain plugin code itself — it's a **marketplace manifest** that tells Claude Code where to find plugins hosted in separate repos under the `qa-vault` organization. Add this marketplace once and you'll have access to every current and future `qa-vault` plugin from a single place.

> **Codex users:** This catalog is Claude-Code-only. Codex's marketplace format doesn't support listing plugins from external repos, so each `qa-vault` plugin must be added to Codex separately via `codex marketplace add qa-vault/<plugin-name>`. See the plugin repos below for Codex install instructions.

---

## Plugins in this marketplace

| Plugin | Description | Repo |
|---|---|---|
| **codelore** | Skills for critically exploring and documenting code. | [qa-vault/codelore](https://github.com/qa-vault/codelore) |

---

## Install (Claude Code)

1. **Add the marketplace** (one-time):

   ```
   /plugin marketplace add qa-vault/marketplace
   ```

2. **Browse and install** from the interactive UI:

   ```
   /plugin
   ```

   Or install a plugin by name directly:

   ```
   /plugin install codelore@qa-vault
   ```

3. **Scope** — Claude Code asks where to install each plugin:
   - **User** — available in every project on your machine
   - **Project** — only active when you open this project, shared with teammates via `.claude/settings.json`
   - **Local** — only for you, only in this project

**Updates:** Claude Code auto-refreshes this marketplace on startup and pulls updates to installed plugins. No action needed.

---

## Install (Codex CLI)

For Codex, go to each plugin's own repo and follow its install instructions. Codex requires adding each plugin repo individually as its own marketplace:

```
codex marketplace add qa-vault/codelore
```

Start here: [qa-vault/codelore](https://github.com/qa-vault/codelore).

---

## License

MIT — see [LICENSE](./LICENSE).
