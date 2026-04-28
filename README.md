# qa-vault marketplace

A catalog of plugins published by `qa-vault`, installable in both **Claude Code** and **Codex CLI**.

This repo doesn't contain plugin code itself — it's a **marketplace manifest** that tells each tool where to find plugins hosted in separate repos under the `qa-vault` organization. Add this marketplace once and you'll have access to every current and future `qa-vault` plugin from a single place.

---

## Plugins in this marketplace

| Plugin | Description | Repo |
|---|---|---|
| **codelore** | Project documentation as an auto-loaded context layer for AI sessions. Four skills: write docs with frontmatter, bulk-migrate pre-existing docs, route relevant docs into the agent's context on planning/debug/onboarding, and skeptically review code or plans against the loaded docs. | [qa-vault/codelore](https://github.com/qa-vault/codelore) |

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

> **Requires Codex CLI 0.122+.** The `url` source variant used here shipped in stable 0.122 (2026-04-20). Earlier 0.121.x releases accept only `local` plugin sources and cannot install polyrepo catalogs like this one — upgrade to 0.122 or later.

1. **Add the marketplace** (one-time):

   ```
   codex plugin marketplace add qa-vault/marketplace
   ```

2. **Install a plugin**:

   Inside Codex, open the plugin browser:

   ```
   /plugins
   ```

   Find the plugin (e.g. `codelore`) under the `qa-vault` marketplace and toggle it on to install. (`/plugins` is an interactive browser — it does not accept inline arguments.)

**Updates:** refresh manually when needed:

```
codex plugin marketplace upgrade qa-vault
```

(Codex's auto-update behavior on launch isn't documented as of April 2026 — manual refresh is the reliable path.)

---

## License

MIT — see [LICENSE](./LICENSE).
