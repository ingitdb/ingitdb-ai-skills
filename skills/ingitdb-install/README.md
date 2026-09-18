# ingitdb Install Skill

Install / reinstall / update the [`ingitdb`](https://github.com/ingitdb/ingitdb-cli) CLI. Implementation lives in [`SKILL.md`](SKILL.md) and has the canonical name `ingitdb-install`. Design rationale and explicit non-goals live in the [CLI install skill idea](https://github.com/ingitdb/ingitdb-ai-skills/blob/main/docs/ideas/cli-install-skill.md).

## Sister skills

This skill mirrors the install skill in sibling CLI-wrapper plugins:

- [SpecScore plugin](https://github.com/synchestra-io/ai-plugin-specscore)
- [Synchestra plugin](https://github.com/synchestra-io/ai-plugin-synchestra)
- [DataTug plugin](https://github.com/datatug/datatug-ai-skills)

**All implementations should remain similar in shape.** Show the user the install commands; do not execute installers from inside the skill. Verify with `<cli> version` after the user confirms install is complete. When changing one, consider whether the same change should land in the others.
