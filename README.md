# qa-vault marketplace

**One catalog for every qa-vault plugin: add it once in Claude Code or Codex CLI and install the plugins that make your AI agent a QA practitioner, a disciplined engineer, and a documentation-aware collaborator.**

[![License](https://img.shields.io/badge/license-Apache--2.0-green)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-marketplace-cc785c)](#install)
[![Codex CLI](https://img.shields.io/badge/Codex_CLI-marketplace-1f2328)](#install)

This repository holds only the marketplace manifests. The plugins live in their own repositories under the [qa-vault](https://github.com/qa-vault) organization and are built around [QA Vault](https://qa-vault.com), an MCP-native test-management platform where AI agents are first-class users.

## Quick start

```
/plugin marketplace add qa-vault/marketplace
/plugin install qa-vault-skills@qa-vault
```

Full steps for both harnesses are under [Install](#install).

## Plugins

| Plugin | Version | What it gives your agent | Skills |
|---|---|---|---|
| [**qa-vault-skills**](https://github.com/qa-vault/qa-vault-skills) | 0.7.1 | The QA practice for QA Vault: author, maintain, search, and organize manual test cases through the QA Vault MCP with a human review-and-approve loop, then turn them into Playwright e2e tests that are generated, run, healed, and reported back into the vault. | 11 |
| [**quality-loop**](https://github.com/qa-vault/quality-loop) | 0.5.0 | A quality loop for AI-assisted development: skeptical exploratory QA of plans and code, contract-driven unit and integration tests verified by mutation testing, a deterministic pre-PR Semgrep gate with your own rules, critical triage of Greptile reviews, and a human-approved ratchet that turns findings into rules. | 7 |
| [**codelore**](https://github.com/qa-vault/codelore) | 0.6.0 | Project documentation as a context layer: implementation docs with frontmatter, an auto-maintained index, and a router that loads the relevant docs before the agent plans, debugs, or onboards. | 3 |

### How they fit together

Each plugin is self-contained and installs on its own. Together they cover one development iteration end to end:

1. **codelore** gives the agent grounded product context from the project's own docs.
2. **quality-loop** questions the plan, holds the tests to their contract, gates the PR, and triages the review.
3. **qa-vault-skills** keeps the test repository in QA Vault current and automated as the product changes.

## Install

<details>
<summary><strong>Claude Code</strong></summary>

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

3. **Scope**: Claude Code asks where to install each plugin:
   - **User**: available in every project on your machine
   - **Project**: only active when you open this project, shared with teammates via `.claude/settings.json`
   - **Local**: only for you, only in this project

**Updates:** Claude Code auto-refreshes this marketplace on startup and pulls updates to installed plugins.

</details>

<details>
<summary><strong>Codex CLI</strong></summary>

> Requires Codex CLI 0.122 or later. The `url` source variant used here shipped in stable 0.122 (2026-04-20). Earlier releases accept only `local` plugin sources and cannot install polyrepo catalogs like this one.

1. **Add the marketplace** (one-time):

   ```
   codex plugin marketplace add qa-vault/marketplace
   ```

2. **Install a plugin**: inside Codex, open the plugin browser:

   ```
   /plugins
   ```

   Find the plugin under the `qa-vault` marketplace and toggle it on. `/plugins` is an interactive browser and does not accept inline arguments.

**Updates:** refresh manually when needed:

```
codex plugin marketplace upgrade qa-vault
```

</details>

## License

Apache-2.0. See [LICENSE](LICENSE).
