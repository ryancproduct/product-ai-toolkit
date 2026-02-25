# Plugin Conversion — Design

> **Context:** Converting AI PM Kit from a manual-copy installation to a Claude Code plugin with its own marketplace.

## Decision: Distribution via own marketplace

- **Plugin repo** (`ryancproduct/product-ai-toolkit`): The existing repo, with `.claude-plugin/plugin.json` added.
- **Marketplace repo** (`ryancproduct/ai-pm-kit-marketplace`): A tiny repo that references the plugin by URL.

## What changes

| Item | Before | After |
|------|--------|-------|
| Install | `git clone` + 4 `cp` commands | 2 plugin commands |
| Update | `git pull` + re-copy | `claude plugin update` |
| Uninstall | Manually delete from `~/.claude/` | 1 command |
| CLAUDE.md | Single file (personal + toolkit) | Split: plugin CLAUDE.md (toolkit) + template (personal) |
| config/ | Example settings.json | Removed (plugins don't ship settings) |

## What stays the same

- `commands/` — zero changes, frontmatter already plugin-compatible
- `skills/` — zero changes
- `agents/` — zero changes
