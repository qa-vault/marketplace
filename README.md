# qa-vault marketplace

A catalog of plugins published by `qa-vault`, installable in both **Claude Code** and **Codex CLI**.

This repo doesn't contain plugin code itself — it's a **marketplace manifest** that tells each tool where to find the plugins (each lives in its own repo under the `qa-vault` organization). Add this marketplace once and you'll have access to every current and future `qa-vault` plugin from a single place.

---

## Plugins in this marketplace

| Plugin | Description | Repo |
|---|---|---|
| **codelore** | Skills for critically exploring and documenting code. | [qa-vault/codelore](https://github.com/qa-vault/codelore) |

---

## Install

### Claude Code

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

### Codex CLI

1. **Add the marketplace** (one-time):

   ```
   codex marketplace add qa-vault/marketplace
   ```

2. **Install a plugin**:

   ```
   /plugins install codelore
   ```

   (Run inside Codex. You can also browse with `/plugins`.)

**Updates:** refresh manually when needed:

   ```
   codex marketplace update qa-vault
   ```

(Codex's auto-update behavior on launch isn't documented as of April 2026 — manual refresh is the reliable path.)

---

## License

MIT — see [LICENSE](./LICENSE).
