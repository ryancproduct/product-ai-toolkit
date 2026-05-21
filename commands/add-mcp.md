---
description: How to add MCP servers to Claude Code
---

# Adding MCP Servers

There are two ways to connect MCP servers.

---

## Option 1: claude.ai connectors (Recommended)

Go to **https://claude.ai/customize/connectors** and connect tools through the UI. Available in all your Claude Code sessions automatically — no CLI needed.

PM integrations available this way: Atlassian (Jira + Confluence), Amplitude, Slack, Intercom, Glean, Figma, GitHub, Google Calendar, Gmail, Google Drive, Zoom, Twine, and more.

---

## Option 2: CLI (for local/self-hosted servers)

For MCP servers running locally (databases, internal tools, custom servers).

```bash
# HTTP remote server
claude mcp add --transport http <name> <url>

# Local process (stdio)
claude mcp add --transport stdio <name> -- <command>

# Project-scoped (shared with team via .mcp.json)
claude mcp add --scope project --transport http <name> <url>
```

### Scopes

| Scope | File | Use Case |
|-------|------|----------|
| `local` (default) | `~/.claude.json` | Personal, this project only |
| `project` | `.mcp.json` | Shared with team via git |
| `user` | `~/.claude.json` | Personal, all projects |

### Examples

**PostgreSQL**
```bash
claude mcp add --transport stdio db -- npx -y @bytebase/dbhub \
  --dsn "postgresql://user:pass@host:5432/database"
```

**With environment variables**
```bash
claude mcp add --transport stdio --env API_KEY=xxx myserver -- npx -y my-mcp-server
```

### Management

```bash
claude mcp list          # List all servers
claude mcp get <name>    # Get server details
claude mcp remove <name> # Remove a server
```

Run `/mcp` inside Claude Code to check connection status and authenticate OAuth servers.

---

## Rules

1. All flags BEFORE server name
2. Use `--` to separate name from command (stdio)
3. Run `/mcp` after adding to confirm the connection
