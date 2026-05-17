---
name: serve
description: Start an inGitDB server — MCP for AI agents, HTTP API for apps, or a watcher that logs database events. Use when you need a long-running process exposing the database over a protocol.
user-invocable: true
---

# inGitDB serve

Wraps `ingitdb serve` — start one or more long-running servers over an inGitDB database.

## Pre-flight check

```bash
command -v ingitdb >/dev/null 2>&1
```

On miss, invoke `/ingitdb:install` and stop until `ingitdb version` succeeds.

## Pick a server

| You need to… | Read |
|---|---|
| Expose CRUD operations to AI agents via MCP | [references/mcp.md](references/mcp.md) |
| Expose a REST/HTTP API for apps | [references/http.md](references/http.md) |
| Stream change events from the database to stdout | [references/watch.md](references/watch.md) |

## Notes

- `ingitdb serve` accepts multiple `--mcp`, `--http`, `--watch` flags to run more than one server in the same process.
- Run from inside the database directory or pass `--path`.
