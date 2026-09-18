---
format: https://specscore.md/feature-specification
status: Stable
---

# Feature: Publishable inGitDB CLI skills plugin

> [SpecScore.**Studio**](https://specscore.studio): | [Explore](https://specscore.studio/app/github.com/ingitdb/ingitdb-ai-skills/spec/features/cli-helpers-ingitdb-plugin?op=explore) | [Edit](https://specscore.studio/app/github.com/ingitdb/ingitdb-ai-skills/spec/features/cli-helpers-ingitdb-plugin?op=edit) | [Ask question](https://specscore.studio/app/github.com/ingitdb/ingitdb-ai-skills/spec/features/cli-helpers-ingitdb-plugin?op=ask) | [Request change](https://specscore.studio/app/github.com/ingitdb/ingitdb-ai-skills/spec/features/cli-helpers-ingitdb-plugin?op=request-change) |
**Status:** Stable
**Source Ideas:** —

## Summary

Standardize the canonical inGitDB skills bundle as a publishable multi-host plugin with product-qualified skill names.

## Problem

The canonical bundle uses generic skill names, which collide in harnesses that discover skills from a shared flat namespace. The source also lacks Codex and Cursor manifests, and the old install command aliases an already discoverable skill, producing duplicate loader inventory.

## Behavior

The repository has one canonical `skills/` tree containing `ingitdb-describe`, `ingitdb-install`, `ingitdb-list`, `ingitdb-record`, and `ingitdb-validate`. Each skill keeps its existing instructions and in-tree references; source-only documentation links use the canonical repository URL where a per-skill installation would not include the linked file.

Claude Code, Codex, and Cursor manifests retain the inGitDB plugin identity and point to that same tree. The Codex manifest is validated with the Codex plugin validator; Cursor uses its supported root Agent Plugin manifest. The duplicate legacy install command is removed, so a native loader exposes each canonical skill once.

This source-only standardization advances the inGitDB plugin patch version from `0.0.1` to `0.0.2` because the native skill inventory changes. The shared `skills sync` provider and inGitDB CLI integration remain outside this Feature.

## Acceptance Criteria

### AC: product-qualified-native-skills

Given the plugin source is loaded by a supported native harness
When it inventories the skills directory
Then it finds only `ingitdb-describe`, `ingitdb-install`, `ingitdb-list`, `ingitdb-record`, and `ingitdb-validate`, each with its original instructions and valid in-tree references.

### AC: manifest-parity

Given the Claude Code, Codex, and Cursor manifests
When their skill roots and plugin identity are inspected
Then every manifest identifies the inGitDB plugin and targets the same canonical `skills/` tree.

## Open Questions

Native plugin publication and the inGitDB CLI's matched embedded snapshot belong to the fleet coordination and CLI-owning work; this source Feature only prepares the canonical bundle.

---
*This document follows the https://specscore.md/feature-specification*
