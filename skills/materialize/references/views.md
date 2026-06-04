# ingitdb materialize --views

Rebuild materialized view output files under each view's configured `$views/` directory.

## Command

```bash
# All views
ingitdb materialize --views [--path <dir>]

# Specific views (glob list — note the '=')
ingitdb materialize --views=GLOB[,GLOB...] [--records-delimiter=N] [--path <dir>]
```

## Targeting

`--views` is tri-state: omit it (skip views), pass it bare (all views), or pass
`=PATTERNS` to limit to matching view names. `PATTERNS` is a list separated by `,`
(canonical) or `;`; each entry is a glob matched against view names.

## Flags

| Flag | Description |
|---|---|
| `--views[=GLOB]` | Bare = all views; `=GLOB[,GLOB]` = matching view names. |
| `--records-delimiter=N` | INGR output only: `1` = write the `#-` record delimiter, `-1` = disable, `0`/omitted = view/project default (app default `1`). No effect when no view is regenerated. |
| `--path <dir>` | Database directory (defaults to the current directory). |

## When to use

- After record changes, to refresh a view's output.
- To rebuild a single view you are iterating on, without touching others.

## Examples

```bash
# All views
ingitdb materialize --views

# Only two views
ingitdb materialize --views=by_status,by_assignee

# One view, with the INGR record delimiter disabled
ingitdb materialize --views=by_status --records-delimiter=-1
```

## Notes

- Non-targeted views are left untouched.
- Views are also rebuilt by `ingitdb validate` and `ingitdb pull`.
- To regenerate views and collection READMEs together, combine the flags: `ingitdb materialize --views=by_status --collections=teams`.
