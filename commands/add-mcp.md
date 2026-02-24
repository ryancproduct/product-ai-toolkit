---
description: How to add MCP servers to Claude Code
---

# Adding MCP Servers

## Quick Commands

```bash
# HTTP (remote servers)
claude mcp add --transport http <name> <url>

# Stdio (local processes)
claude mcp add --transport stdio <name> -- <command>

# With project scope (shared via .mcp.json)
claude mcp add --scope project --transport http <name> <url>
```

## Scopes

| Scope | File | Use Case |
|-------|------|----------|
| `local` (default) | `~/.claude.json` | Personal, this project only |
| `project` | `.mcp.json` | Shared with team via git |
| `user` | `~/.claude.json` | Personal, all projects |

## Examples

**GitHub**
```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp/
```

**Sentry**
```bash
claude mcp add --transport http sentry https://mcp.sentry.dev/mcp
# Then /mcp in Claude Code to authenticate
```

**PostgreSQL**
```bash
claude mcp add --transport stdio db -- npx -y @bytebase/dbhub \
  --dsn "postgresql://user:pass@host:5432/database"
```

**With env vars**
```bash
claude mcp add --transport stdio --env API_KEY=xxx myserver -- npx -y my-mcp-server
```

## Management

```bash
claude mcp list          # List all servers
claude mcp get <name>    # Get server details
claude mcp remove <name> # Remove a server
```

Inside Claude Code:
```
/mcp                     # View status, authenticate OAuth servers
```

## Key Rules

1. All flags BEFORE server name
2. Use `--` to separate name from command (stdio)
3. Option order matters
