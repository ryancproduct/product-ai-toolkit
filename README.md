# The SC AI PM Kit

A complete AI-powered Product Management toolkit built on Claude Code. This is the operational system behind how PM works at SafetyCulture — connecting discovery, strategy, execution, analytics, and communication through a single AI-native workflow.

## What's In the Box

### CLAUDE.md — The PM Operating System
Global instructions that shape how Claude works with you: epistemic humility, thinking partner principles, smart delegation patterns, and preferences. This is the foundation everything else builds on.

### Commands (15 skills) — `/command-name`
Quick PM workflows invoked as slash commands. Each is a single markdown file.

| Command | What It Does |
|---------|-------------|
| `/experiment` | Design, plan and analyse A/B tests with Amplitude integration |
| `/competitive-analysis` | Research and analyse a competitor (Porter's Five Forces) |
| `/jtbd` | Extract Jobs-to-be-Done from feature requests or feedback |
| `/user-stories` | Generate INVEST-validated stories with BDD acceptance criteria |
| `/opportunity-tree` | Build Opportunity Solution Trees (Teresa Torres methodology) |
| `/probtoprd` | Full discovery workflow from problem statement to PRD |
| `/impact-sizing` | Translate product hypotheses into ARR estimates (Excel output) |
| `/metrics-dashboard` | Generate metrics dashboard summary |
| `/competitive-analysis` | Analyse competitor positioning, pricing, and strategy |
| `/feature-request` | Process and triage incoming feature requests |
| `/stakeholder-update` | Create stakeholder communications |
| `/standup` | Generate concise standup updates |
| `/weekly-update` | Generate weekly team updates |
| `/retrospective` | Facilitate sprint retrospectives |
| `/rapid-prototype` | Build UI prototypes using zero-build HTML system |
| `/recall` | Retrieve previously learned knowledge |
| `/add-mcp` | Guide for adding new MCP servers |

### Skills (Complex, multi-step workflows)
Folder-based skills with supporting files, templates, and examples.

| Skill | What It Does |
|-------|-------------|
| `/debate` | Parallel Champion vs Sceptic agents stress-test a product idea. Outputs risk register, MVP scope, assumption map, go/no-go. |
| `/interview-analysis` | Parallel agent dispatch to analyse customer interviews using Teresa Torres Continuous Discovery framework |
| `/impact-sizing` | Guided impact sizing with Python-driven calculations and Excel workbook output |
| `/learn` | Deep-dive research on any topic, saves knowledge for future sessions |
| `/rapid-prototype` | Full prototyping system with design system references |
| `/web-browser` | Remote-control Chrome for web interaction |
| `xlsx` / `docx` / `pptx` / `pdf` | Document creation and manipulation |

### Agents (9 specialist agents)
Custom agent definitions for the Task tool — each is a specialist you can delegate to.

| Agent | Speciality |
|-------|-----------|
| `market-research-analyst` | Competitive intelligence and market research |
| `cpto-review` | Executive-level review of PRDs, architecture, strategy |
| `ai-engineering-architect` | AI implementation strategy and architecture |
| `mobile-app-architect` | iOS/Android development and optimisation |
| `frontend-web-developer` | Web frontend development |
| `backend-architecture-engineer` | Backend systems and API design |
| `ux-designer` | UX design and user experience |
| `prototype-builder` | Rapid prototyping |
| `data-brief-analyst` | Data analysis and briefs |

### MCP Integrations
The kit connects Claude Code to your entire tool chain:

| Category | Tools |
|----------|-------|
| **Comms** | Slack |
| **Development** | Jira (MCP), GitHub, Docker |
| **Design** | Figma (MCP) |
| **Analytics** | Amplitude (MCP) |
| **Docs** | Confluence (MCP), Glean Search (MCP), Apple Notes |
| **Research** | Hey Marvin, Twine (MCP) |
| **Feedback** | Product Board (MCP), Gong |
| **Meetings** | Granola (MCP) |
| **Calendar** | Google Calendar |
| **Image Gen** | Nano Banana Pro |

## Installation

### Quick Start
1. Copy the contents of this kit to your `~/.claude/` directory
2. Skills go in `~/.claude/skills/`
3. Commands go in `~/.claude/commands/`
4. Agents go in `~/.claude/agents/`
5. Review `CLAUDE.md` and adapt to your context
6. Set up MCP servers for your tools (see `/add-mcp` command)

### Config Files
The `config/` folder contains example settings. **Do not copy directly** — merge with your existing settings:
- `settings.json` — Model preference and enabled plugins
- `installed_plugins.json` — Plugin registry (install plugins individually via Claude Code)

### MCP Servers
MCP servers need to be configured individually based on your accounts and API keys. The kit includes integrations for Jira, Confluence, Figma, Amplitude, Granola, Glean, Twine, and Product Board. Use the `/add-mcp` command for guidance on setting up each one.

## Architecture

```
Claude Code
├── CLAUDE.md              → PM operating system (global instructions)
├── commands/              → Quick slash commands (single-file skills)
├── skills/                → Complex multi-step workflows
├── agents/                → Specialist agents for delegation
└── MCP Servers            → Tool integrations (Jira, Amplitude, Figma, etc.)
```

The design philosophy: **context engineering over prompt engineering**. Rather than crafting perfect prompts each time, the kit builds persistent context (company knowledge, frameworks, conventions) that makes every interaction grounded and specific.

## Key Patterns

1. **Parallel Agent Dispatch** — Skills like `/interview-analysis` and `/debate` spawn multiple agents simultaneously for faster, deeper analysis
2. **MCP-Grounded Analysis** — Skills pull real data from Amplitude, Jira, Confluence rather than relying on AI knowledge alone
3. **Framework-Driven** — Every skill encodes a real PM framework (Teresa Torres, JTBD, INVEST, RICE, etc.) not generic instructions
4. **Flexible Input** — Most skills accept anything from a one-liner to a full document and adapt accordingly
5. **Structured Output** — All skills produce markdown formatted for Confluence, Slack, or Jira

## Built By
Ryan Clement, Principal Product Manager at SafetyCulture
