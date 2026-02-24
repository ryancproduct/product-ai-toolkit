# AI PM Kit

**A practical AI operating system for Product Management — turning Claude Code into a PM superpower.**

Built for [Claude Code](https://claude.ai/download), this kit gives you 15 slash commands, 14+ complex skills, 9 specialist agents, and 12 MCP integrations — all wired together to handle the full PM workflow from discovery to delivery.

---

## Why This Exists

Product Managers spend too much time reformatting, context-switching, and reinventing frameworks. This kit encodes proven PM methodologies (Teresa Torres, JTBD, INVEST, RICE) into reusable AI workflows that work with your actual tools — Jira, Amplitude, Figma, Slack, Confluence.

**The core idea:** Context engineering over prompt engineering. Instead of crafting better prompts, build better context systems.

---

## What's Inside

### Commands — Quick PM Workflows

15 slash commands for common PM tasks. Each is a single markdown file.

| Command | What It Does |
|---------|-------------|
| `/experiment` | Design, plan and analyse A/B tests with Amplitude integration |
| `/competitive-analysis` | Research competitors using Porter's Five Forces |
| `/jtbd` | Extract Jobs-to-be-Done from feature requests or feedback |
| `/user-stories` | Generate INVEST-validated stories with BDD acceptance criteria |
| `/opportunity-tree` | Build Opportunity Solution Trees (Teresa Torres methodology) |
| `/probtoprd` | Full discovery workflow from problem statement to PRD |
| `/impact-sizing` | Translate product hypotheses into ARR estimates (Excel output) |
| `/metrics-dashboard` | Generate metrics dashboard summary |
| `/feature-request` | Process and triage incoming feature requests |
| `/stakeholder-update` | Create stakeholder communications |
| `/standup` | Generate concise standup updates |
| `/weekly-update` | Generate weekly team updates |
| `/retrospective` | Facilitate sprint retrospectives |
| `/rapid-prototype` | Build UI prototypes using zero-build HTML system |
| `/recall` | Retrieve previously learned knowledge |

### Skills — Complex Multi-Step Workflows

Folder-based skills with supporting files, templates, and agent orchestration.

| Skill | What It Does |
|-------|-------------|
| `/debate` | Parallel Champion vs Sceptic agents stress-test a product idea. Outputs risk register, MVP scope, assumption map, go/no-go. |
| `/interview-analysis` | Parallel agent dispatch to analyse customer interviews using Teresa Torres Continuous Discovery framework |
| `/impact-sizing` | Guided impact sizing with Python-driven calculations and Excel workbook output |
| `/learn` | Deep-dive research on any topic, saves knowledge for future sessions |
| `/rapid-prototype` | Full prototyping system with design system references |
| `/parallel-prototype` | Spawn 3 structurally different prototypes in parallel |
| `/web-browser` | Remote-control Chrome for web interaction |
| `xlsx` / `docx` / `pptx` / `pdf` | Document creation and manipulation |

### Agents — Specialists for Delegation

9 custom agents you can delegate to via the Task tool.

| Agent | Speciality |
|-------|-----------|
| `market-research-analyst` | Competitive intelligence and market research |
| `cpto-review` | Executive-level review of PRDs, architecture, strategy |
| `ai-engineering-architect` | AI implementation strategy |
| `mobile-app-architect` | iOS/Android development |
| `ux-designer` | UX design and user experience |
| `prototype-builder` | Rapid prototyping |
| `data-brief-analyst` | Data analysis and briefs |

### MCP Integrations

Pre-configured connections to your PM stack:

| Category | Tools |
|----------|-------|
| **Comms** | Slack |
| **Development** | Jira (MCP), GitHub, Docker |
| **Design** | Figma (MCP) |
| **Analytics** | Amplitude (MCP) |
| **Docs** | Confluence (MCP), Glean Search (MCP) |
| **Research** | Twine (MCP), Product Board (MCP) |
| **Meetings** | Granola (MCP) |
| **Calendar** | Google Calendar |

---

## Demos

### `/debate` — Stress-test a product idea
<!-- TODO: Add demo GIF -->
*Give it a one-line feature idea. Get back a risk register, MVP scope, and go/no-go recommendation grounded in real data.*

### `/experiment` — Design an A/B test
<!-- TODO: Add demo GIF -->
*Full experimental design with hypothesis, metrics, sample size calculations — validated against your Amplitude taxonomy.*

### `/rapid-prototype` — Idea to prototype in minutes
<!-- TODO: Add demo GIF -->
*From description to clickable HTML prototype using your design system components.*

---

## Quick Start

**Prerequisites:** [Claude Code](https://claude.ai/download) installed

```bash
# Clone the kit
git clone https://github.com/ryancproduct/product-ai-toolkit.git

# Create directories if they don't exist
mkdir -p ~/.claude/commands ~/.claude/skills ~/.claude/agents

# Copy without overwriting existing files
cp -rn product-ai-toolkit/commands/* ~/.claude/commands/
cp -rn product-ai-toolkit/skills/* ~/.claude/skills/
cp -rn product-ai-toolkit/agents/* ~/.claude/agents/
```

> **Note:** The `-n` flag prevents overwriting existing files. If you already have a `CLAUDE.md`, merge manually rather than replacing — your existing instructions are valuable.

**Then customise:**
1. Review `product-ai-toolkit/CLAUDE.md` and merge anything useful into your `~/.claude/CLAUDE.md`
2. Configure MCP servers for your tools (run `/add-mcp` for guidance)
3. Try `/jtbd "Users keep asking for dark mode"` — you're running

---

## Architecture

```
~/.claude/
├── CLAUDE.md              → PM operating system (global instructions)
├── commands/              → Quick slash commands (single-file skills)
│   ├── experiment.md
│   ├── jtbd.md
│   ├── competitive-analysis.md
│   └── ... (15 total)
├── skills/                → Complex multi-step workflows
│   ├── debate/
│   ├── interview-analysis/
│   ├── impact-sizing/
│   └── ... (14+ total)
├── agents/                → Specialist agents for delegation
│   ├── market-research-analyst.md
│   ├── cpto-review.md
│   └── ... (9 total)
└── config/                → Example settings
```

---

## Key Patterns

### 1. Parallel Agent Dispatch
Skills spawn multiple specialist agents simultaneously. `/debate` runs Champion and Sceptic agents in parallel, then synthesises their outputs into a structured recommendation.

### 2. MCP-Grounded Analysis
Skills pull real data from your tools. `/experiment` queries Amplitude directly to validate events exist. `/debate` checks Jira for related work. No hallucinated insights.

### 3. Framework-Driven
Every skill encodes a real PM framework:
- **Teresa Torres** — Opportunity Solution Trees, Continuous Discovery
- **JTBD** — Jobs-to-be-Done
- **INVEST** — User story validation
- **RICE** — Prioritisation
- **Porter's Five Forces** — Competitive analysis

### 4. Flexible Input
Commands accept anything from a one-liner to a full document:
```
/jtbd "Users want dark mode"
/jtbd [paste 500 lines of interview transcripts]
```

### 5. Structured Output
All output is markdown formatted for direct use in Confluence, Slack, or Jira. No reformatting required.

---

## Customising for Your Team

**Modify global instructions:**
Edit `~/.claude/CLAUDE.md` to change default behaviour, add team context, or encode your own frameworks.

**Add your own commands:**
Create `~/.claude/commands/your-command.md` — it's live immediately as `/your-command`.

**Add your own agents:**
Create `~/.claude/agents/your-agent.md` with the agent's speciality and constraints.

**Add MCP integrations:**
Run `/add-mcp` for guided setup, or configure manually in your Claude Code settings.

**Swap frameworks:**
Each skill's framework logic lives in its markdown file. Prefer RICE over ICE? Edit the prioritisation skill. Use a different PRD template? Update `skills/prd.md`.

---

## Philosophy: Context Engineering

Most AI tools make you write better prompts. This kit builds better context systems.

The problem with prompts: they're ephemeral, inconsistent, and don't compound. You rewrite the same context every time.

The solution: encode context once, reuse forever.

- **CLAUDE.md** = Your PM operating system
- **Commands** = Reusable workflows with structure
- **Skills** = Multi-step processes with agent orchestration
- **Agents** = Specialist context with domain expertise
- **MCP Servers** = Live connections to your actual data

When you run `/debate`, you're not writing a prompt. You're invoking a system that knows what frameworks to apply, what data to check, and what format to produce — because that context is encoded, not typed.

---

## Contributing

PRs welcome. This is an open-source project built for the PM community.

**Ideas for contributions:**
- New commands for common PM tasks
- New agents for specialist domains
- New MCP integrations
- Framework improvements
- Bug fixes and documentation

---

## Built By

**Ryan Clement** — Principal Product Manager

[LinkedIn](https://linkedin.com/in/ryanclement) · [GitHub](https://github.com/ryancproduct)

---

## Licence

MIT — use it, fork it, customise it, ship it.
