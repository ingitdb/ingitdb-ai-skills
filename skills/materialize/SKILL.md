---
name: materialize
description: Regenerate inGitDB's derived files — collection README.md files and materialized views — from records. Use after editing records or schema, in CI, or when generated files are stale. Supersedes the deprecated `docs update`.
user-invocable: true
---

# inGitDB materialize

Wraps `ingitdb materialize` — a single flat command that regenerates the files inGitDB
derives from its records: per-collection `README.md` files and materialized view output
under each view's `$views/` directory. Files are only rewritten when their content
changes, so runs are idempotent.

## Pre-flight check

Verify the CLI is installed:

```bash
command -v ingitdb >/dev/null 2>&1
```

On miss, instruct the user to invoke `/ingitdb:install` or install per <https://github.com/ingitdb/ingitdb-cli#installation>, then retry.

## Command

```bash
ingitdb materialize [--collections[=GLOB[,GLOB...]]] [--views[=GLOB[,GLOB...]]] [--records-delimiter=N] [--path <dir>]
```

Both `--collections` and `--views` are **tri-state**:

| Form | Meaning |
|---|---|
| flag absent | that artifact type is not touched |
| bare flag (`--collections`) | every artifact of that type |
| `--collections=GLOB[,GLOB]` | only the matching ones |

Running `ingitdb materialize` with **no flags** regenerates everything — all collection
READMEs **and** all views.

> ⚠️ Because the bare flag means "all", a value MUST be attached with `=`:
> use `--views=v1,v2`, **not** `--views v1,v2` (a space makes `v1,v2` a positional arg).
> Patterns in a list are separated by `,` (canonical) or `;`.

## Pick a target

| You need to… | Read |
|---|---|
| Regenerate collection `README.md` files | [references/collections.md](references/collections.md) |
| Regenerate materialized views | [references/views.md](references/views.md) |
| Regenerate everything | run `ingitdb materialize` with no selector flags |

## Notes

- A `created/updated/deleted/unchanged` summary is printed to stderr; stdout stays silent (script-friendly).
- `materialize --collections` **replaces** the deprecated `ingitdb docs update --collection`.
- Views are also rebuilt by `ingitdb validate` and `ingitdb pull`; use `materialize` for an explicit, targeted regeneration step.
