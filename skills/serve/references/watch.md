# ingitdb serve --watch (or `ingitdb watch`)

Stream database change events to stdout. Useful for piping into log aggregators, event buses, or reactive UI updates.

## Command

```bash
ingitdb watch [--path <dir>]
# or
ingitdb serve --watch [--path <dir>]
```

## When to use

- Reactive UI that needs live updates as records change.
- CI/CD pipeline that should fire when a specific collection changes.

## Notes

- Stdout is structured (one event per line) — pipe to `jq` or your log aggregator.
- Exit when interrupted (`SIGINT`/`SIGTERM`).
