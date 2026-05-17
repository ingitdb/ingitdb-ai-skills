# ingitdb serve --mcp

Start the Model Context Protocol server. Exposes inGitDB CRUD operations as MCP tools that any MCP-compatible AI agent can call.

## Command

```bash
ingitdb serve --mcp [--path <dir>]
```

## When to use

- Wiring inGitDB as a database backend for a Claude Code / Cursor / VSCode AI agent.
- Letting an LLM read or modify records without writing custom integration code.

## Notes

- The MCP server speaks stdio by default. Register it in your MCP client's config.
- Schema validation runs on every write — invalid records are rejected with a structured error the agent can read.
