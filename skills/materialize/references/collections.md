# ingitdb materialize --collections

Regenerate per-collection `README.md` files from collection metadata and records.

## Command

```bash
# All collection READMEs
ingitdb materialize --collections [--path <dir>]

# Specific collections (glob list — note the '=')
ingitdb materialize --collections=GLOB[,GLOB...] [--path <dir>]
```

## Targeting

`--collections` is tri-state: omit it (skip READMEs), pass it bare (all collections), or
pass `=PATTERNS` to limit to matching collection IDs. `PATTERNS` is a list separated by
`,` (canonical) or `;`. Each pattern is a glob:

| Pattern | Matches |
|---|---|
| `**` | every collection |
| `agile.teams` | exactly that collection |
| `agile.teams/*` | the collection and its direct subcollections |
| `agile.teams/**` | the collection and all nested subcollections |

## When to use

- After editing records or a collection's schema, to refresh its README table.
- In CI, to verify generated READMEs are up to date (rerun, then check for a diff).

## Examples

```bash
# All READMEs
ingitdb materialize --collections

# One collection plus everything nested under it
ingitdb materialize --collections='agile.teams/**'

# Two specific collections (semicolon separator also works)
ingitdb materialize --collections='countries;teams'
```

## Notes

- This replaces the deprecated `ingitdb docs update --collection=GLOB` (note the plural flag name `--collections`).
- A file is only rewritten when its rendered content differs from what is on disk.
