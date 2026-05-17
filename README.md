# inGitDB AI Plugin

AI plugin for [inGitDB](https://ingitdb.com) — skills that teach AI agents how to use the `ingitdb` CLI for Git-backed database operations: schema validation, record CRUD, materialized views, and serving the database to AI agents over MCP.

This repository contains the plugin source. It is installed on top of the [`ingitdb` CLI](https://github.com/ingitdb/ingitdb-cli); the CLI is a prerequisite.

## Contents

| Directory | Description |
|---|---|
| [`skills/`](skills/README.md) | Agent skills — one per major `ingitdb` CLI surface area, progressively loaded per-verb |
| [`commands/`](commands/install.md) | Slash-command aliases for skills |
| [`.claude-plugin/`](.claude-plugin/plugin.json) | Claude Code plugin manifest |

## Install

Via the [Sneat AI marketplace](https://github.com/sneat-co/ai-marketplace):

```
/plugin marketplace add sneat-co/ai-marketplace
/plugin install ingitdb@sneat-co
```

## First use

The `ingitdb` CLI must be on your `PATH` before any wrapper skill can run. Options:

- Invoke `/ingitdb:install` inside Claude Code — the [install skill](skills/install/SKILL.md) shows the platform-appropriate install commands and waits for you to run them.
- Or install directly per the [inGitDB CLI installation guide](https://github.com/ingitdb/ingitdb-cli#installation).

Verify with `ingitdb version`.

## Relationship to the CLI

The plugin wraps the `ingitdb` CLI — it does not replace it. Skills encode *when* to call a command, *which* flags to pass, and *how* to interpret exit codes. The CLI source of truth is [`ingitdb/ingitdb-cli`](https://github.com/ingitdb/ingitdb-cli).

A change in the CLI surface typically produces a matching skill update in this repository; the two evolve together but release independently.

## Relationship to other plugins

`ingitdb` is a base-layer **CLI wrapper** plugin, in the same shape as:

- [`specscore`](https://github.com/synchestra-io/ai-plugin-specscore)
- [`synchestra`](https://github.com/synchestra-io/ai-plugin-synchestra)
- [`datatug`](https://github.com/datatug/datatug-ai-skills)

## Releases

Releases are tagged as `ingitdb--v<version>` on this repository to support Claude Code's dependency resolution.

## License

MIT — see [LICENSE](LICENSE).
