# Plugin Conversion Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Convert AI PM Kit from manual-copy installation to a Claude Code plugin with its own marketplace.

**Architecture:** Add `.claude-plugin/plugin.json` manifest, split CLAUDE.md into plugin instructions and user template, remove `config/`, scaffold a marketplace repo, and rewrite the README quickstart.

**Tech Stack:** Markdown, JSON (plugin manifest), Git

---

### Task 1: Create plugin manifest

**Files:**
- Create: `.claude-plugin/plugin.json`

**Step 1: Create the manifest file**

```json
{
  "name": "ai-pm-kit",
  "description": "15 PM commands, 19 skills, and 5 specialist agents — turning Claude Code into a PM superpower",
  "version": "1.0.0",
  "author": {
    "name": "Ryan Clement"
  },
  "homepage": "https://github.com/ryancproduct/product-ai-toolkit",
  "repository": "https://github.com/ryancproduct/product-ai-toolkit",
  "license": "MIT",
  "keywords": ["product-management", "pm", "jtbd", "prd", "discovery", "prototyping"]
}
```

**Step 2: Verify structure**

Run: `cat .claude-plugin/plugin.json | python3 -m json.tool`
Expected: Valid JSON output, no errors.

**Step 3: Commit**

```bash
git add .claude-plugin/plugin.json
git commit -m "feat: add plugin manifest"
```

---

### Task 2: Split CLAUDE.md into plugin instructions and user template

The current CLAUDE.md mixes personal preference templates ("About Me", "[Your role]") with toolkit workflow instructions (smart delegation, `/recall` + `/learn` workflow). Plugins ship a CLAUDE.md that gets loaded into context — it should contain toolkit instructions only.

**Files:**
- Rename: `CLAUDE.md` → `CLAUDE.md.template`
- Create: `CLAUDE.md` (plugin-level, toolkit workflow only)

**Step 1: Rename current CLAUDE.md to template**

```bash
git mv CLAUDE.md CLAUDE.md.template
```

**Step 2: Create new plugin CLAUDE.md**

The new `CLAUDE.md` should contain ONLY the toolkit-relevant workflow instructions — how to use the PM commands, skills, and agents together. Strip the "About Me" template and personal preferences.

```markdown
# AI PM Kit

You have the AI PM Kit plugin installed. This gives you PM-specific commands, skills, and agents.

## Smart Delegation

For complex multi-step work, prefer delegation to agents. For everything else, just do it.

**Workflow for complex tasks:**
1. **Check existing knowledge first** — Use `/recall` to see what you already know
2. **Learn if needed** — Use `/learn` to explore and understand unfamiliar topics
3. **Delegate to agents** — Use the Task tool with appropriate agents for parallel or deep work

**Don't delegate** simple, single-step tasks, quick questions, or synthesis work.

## Available Agents

Use the Task tool to delegate to these specialists:

- **market-research-analyst** — Competitive intelligence, market sizing, research
- **cpto-review** — Executive-level review of PRDs, architecture, strategy (uses Opus)
- **ux-designer** — UX design and user experience
- **prototype-builder** — Rapid prototyping
- **data-brief-analyst** — Data analysis and briefs

## Key Patterns

- All commands accept flexible input — from one-liners to full documents
- All output is markdown, ready for Confluence, Slack, or Jira
- Skills that need real data will attempt to use MCP integrations (Amplitude, Jira, Figma, etc.) if configured
```

**Step 3: Commit**

```bash
git add CLAUDE.md CLAUDE.md.template
git commit -m "refactor: split CLAUDE.md into plugin instructions and user template"
```

---

### Task 3: Remove config directory

Plugins don't ship settings files — they're enabled via the plugin system. The example `config/settings.json` is no longer needed.

**Files:**
- Delete: `config/settings.json`
- Delete: `config/` directory

**Step 1: Remove config**

```bash
git rm -r config/
```

**Step 2: Commit**

```bash
git commit -m "chore: remove config/ (plugins don't ship settings)"
```

---

### Task 4: Scaffold marketplace repo

Create a `marketplace/` directory containing everything needed for the marketplace repo (`ryancproduct/ai-pm-kit-marketplace`). The user can push this as a separate GitHub repo.

**Files:**
- Create: `marketplace/.claude-plugin/marketplace.json`
- Create: `marketplace/README.md`
- Create: `marketplace/LICENSE`

**Step 1: Create marketplace manifest**

```json
{
  "name": "ai-pm-kit-marketplace",
  "owner": {
    "name": "Ryan Clement"
  },
  "metadata": {
    "description": "AI PM Kit — product management commands, skills, and agents for Claude Code",
    "version": "1.0.0"
  },
  "plugins": [
    {
      "name": "ai-pm-kit",
      "source": {
        "source": "url",
        "url": "https://github.com/ryancproduct/product-ai-toolkit.git"
      },
      "description": "15 PM commands, 19 skills, and 5 specialist agents for product management",
      "version": "1.0.0"
    }
  ]
}
```

**Step 2: Create marketplace README**

Brief README explaining what the marketplace contains and how to install.

**Step 3: Copy LICENSE from root**

```bash
cp LICENSE marketplace/LICENSE
```

**Step 4: Commit**

```bash
git add marketplace/
git commit -m "feat: scaffold marketplace repo for separate publishing"
```

---

### Task 5: Update README.md

Rewrite the Quick Start section and Architecture section. Keep all other sections (What's Inside, Key Patterns, Philosophy, etc.) unchanged.

**Files:**
- Modify: `README.md`

**Step 1: Replace Quick Start section**

Replace lines 104-127 (the current Quick Start) with the new plugin-based instructions:

```markdown
## Quick Start

**Prerequisites:** [Claude Code](https://claude.ai/download) installed

### Install (2 commands)

```bash
claude plugin marketplace add ryancproduct/ai-pm-kit-marketplace
claude plugin install ai-pm-kit
```

That's it. All 15 commands, 19 skills, and 5 agents are now available.

### Verify

```
claude /jtbd "Users keep asking for dark mode"
```

### Optional: Personalise

Copy the CLAUDE.md template into your project to customise the toolkit for your team:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/ryancproduct/product-ai-toolkit/main/CLAUDE.md.template
```

Edit the "About Me" section with your role, company, and preferences.

### Optional: Connect your tools

The kit works best with MCP integrations for your PM stack. Run `/add-mcp` in Claude Code for guided setup, or add manually:

| Tool | Install command |
|------|----------------|
| Jira | `claude mcp add jira -- npx -y @anthropic/mcp-jira` |
| Amplitude | `claude mcp add amplitude -- npx -y @anthropic/mcp-amplitude` |
| Figma | `claude mcp add figma -- npx -y @anthropic/mcp-figma` |
| Confluence | `claude mcp add confluence -- npx -y @anthropic/mcp-confluence` |
| Slack | `claude mcp add slack -- npx -y @anthropic/mcp-slack` |

### Uninstall

```bash
claude plugin uninstall ai-pm-kit
claude plugin marketplace remove ai-pm-kit-marketplace
```
```

**Step 2: Update Architecture section**

Replace lines 130-150 (the `~/.claude/` tree) to reflect plugin structure:

```markdown
## Architecture

```
product-ai-toolkit/               ← This repo (the plugin)
├── .claude-plugin/
│   └── plugin.json               ← Plugin manifest
├── CLAUDE.md                     ← Plugin instructions (loaded automatically)
├── CLAUDE.md.template            ← Personal preferences template (copy to your project)
├── commands/                     ← Quick slash commands (single-file workflows)
│   ├── experiment.md
│   ├── jtbd.md
│   ├── competitive-analysis.md
│   └── ... (15 total)
├── skills/                       ← Complex multi-step workflows
│   ├── debate/
│   ├── interview-analysis/
│   ├── impact-sizing/
│   └── ... (19 total)
├── agents/                       ← Specialist agents for delegation
│   ├── market-research-analyst.md
│   ├── cpto-review.md
│   └── ... (5 total)
└── marketplace/                  ← Marketplace repo scaffold (publish separately)
    └── .claude-plugin/
        └── marketplace.json
```
```

**Step 3: Update Customising section**

Replace lines 182-197 to reference plugin context instead of `~/.claude/`:

Users can still customise by forking the plugin or adding their own commands/skills alongside it.

**Step 4: Commit**

```bash
git add README.md
git commit -m "docs: update README with plugin install quickstart"
```

---

### Task 6: Add marketplace/ to .gitignore note

Add a comment in the README explaining that `marketplace/` should be published as a separate repo.

**Step 1: Already handled in Task 4 README** — the marketplace README explains this.

**Step 2: Final verification**

Run: `ls -la .claude-plugin/` — should show `plugin.json`
Run: `ls marketplace/.claude-plugin/` — should show `marketplace.json`
Run: `cat README.md | head -5` — should show unchanged title

**Step 3: No additional commit needed.**
