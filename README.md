# AI PM Kit

**A practical AI operating system for Product Management — turning Claude Code into a PM superpower.**

Built for [Claude Code](https://claude.ai/download), this kit gives you 19 slash commands, 23 skills, 8 specialist agents, and 12 MCP integrations — all wired together to handle the full PM workflow from discovery to delivery.

---

## Why This Exists

Product Managers spend too much time reformatting, context-switching, and reinventing frameworks. This kit encodes proven PM methodologies (Teresa Torres, JTBD, INVEST, RICE) into reusable AI workflows that work with your actual tools — Jira, Amplitude, Figma, Slack, Confluence.

**The core idea:** Context engineering over prompt engineering. Instead of crafting better prompts, build better context systems.

---

## What's Inside

### Commands — Quick PM Workflows

19 slash commands for common PM tasks. Each is a single markdown file.

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
| `/customer-brief` | Pre-meeting intel brief on any customer account — usage, sentiment, open issues, talking points |
| `/roadmap-narrative` | Turn a roadmap into exec, team, and customer-facing narratives |
| `/decision-brief` | 1-page decision brief with options, trade-offs, and a clear recommendation |
| `/sprint-health` | Mid-sprint health check — surfaces blockers, produces a copy-paste Slack update |

### Skills — Complex Multi-Step Workflows

Skills range from single-file methodologies to folder-based workflows with templates and agent orchestration.

| Skill | What It Does |
|-------|-------------|
| `/debate` | Parallel Champion vs Sceptic agents stress-test a product idea. Outputs risk register, MVP scope, assumption map, go/no-go. |
| `/interview-analysis` | Parallel agent dispatch to analyse customer interviews using Teresa Torres Continuous Discovery framework |
| `/impact-sizing` | Guided impact sizing with Python-driven calculations and Excel workbook output |
| `/learn` | Deep-dive research on any topic, saves knowledge for future sessions |
| `/recall` | Retrieve previously learned knowledge from your growing knowledge base |
| `/probtoprd` | Full discovery chain from problem statement → JTBD extraction → PRD |
| `/prd` | Generate comprehensive PRDs using a proven template |
| `/jtbd` | Full Jobs-to-be-Done extraction methodology |
| `/user-stories` | INVEST-validated story generation with BDD acceptance criteria |
| `/opportunity-tree` | Build Opportunity Solution Trees (Teresa Torres methodology) |
| `/prioritization` | Prioritise features using RICE, MoSCoW, Kano, ICE, or Weighted Scoring |
| `/design-an-interface` | Generate multiple radically different interface designs ("Design It Twice" methodology) |
| `/rapid-prototype` | Full prototyping system with design system references |
| `/parallel-prototype` | Spawn 3 structurally different prototypes in parallel |
| `/web-browser` | Remote-control Chrome for web interaction |
| `/xlsx` `/docx` `/pptx` `/pdf` | Document creation and manipulation |
| `/roadmap-narrative` | Turn a rough roadmap into exec, team, and customer-facing narratives — one input, three polished outputs |
| `/decision-brief` | Structured 1-pager for any product decision — options, trade-offs, recommendation, next step |
| `/churn-signal` | Account health assessment — usage + sentiment signals → health score + recommended intervention |
| `/sprint-health` | Sprint delivery check — planned vs done, blockers surfaced, copy-paste Slack update produced |

### Agents — Specialists for Delegation

8 custom agents you can delegate to via the Task tool.

| Agent | Speciality |
|-------|-----------|
| `market-research-analyst` | Competitive intelligence and market research |
| `cpto-review` | Executive-level review of PRDs, architecture, strategy (uses Opus) |
| `ux-designer` | UX design and user experience |
| `prototype-builder` | Rapid prototyping |
| `data-brief-analyst` | Data analysis and briefs |
| `customer-brief-analyst` | Pre-meeting intel on any account — usage, sentiment, open issues, talking points |
| `voice-of-customer` | Synthesise ambient customer signals into confidence-ranked insight themes |
| `data-storyteller` | Turn Amplitude metrics into narrative insight briefs with "so what" framing |

### MCP Integrations

Connect these tools via **https://claude.ai/customize/connectors** — once connected, all skills and agents use them automatically.

| Category | Tools |
|----------|-------|
| **Comms** | Slack |
| **Product & Dev** | Atlassian (Jira + Confluence), GitHub |
| **Design** | Figma |
| **Analytics** | Amplitude |
| **Search & Knowledge** | Glean |
| **Customer Support** | Intercom |
| **Research** | Twine |
| **Email & Calendar** | Gmail, Google Calendar, Google Drive |
| **Meetings** | Zoom |

For local or self-hosted tools (databases, internal APIs), use `/add-mcp` for CLI setup instructions.

### Recommended Plugins

These third-party Claude Code plugins pair well with the kit. Install them separately — they're not included in this repo.

| Plugin | What It Does | Install |
|--------|-------------|---------|
| **Superpowers** | Brainstorming → design doc → implementation plan → subagent execution. The full idea-to-code workflow with structured checkpoints. | `claude plugins install superpowers from claude-plugins-official` |
| **Impeccable** | Frontend design skill with 17 commands for auditing, critiquing, and polishing UI. Deep references for typography, colour, spacing, motion, and anti-patterns. Levels up `/rapid-prototype` output. | See [impeccable.style](https://impeccable.style) |

> **Why Superpowers matters:** The brainstorm → plan → execute loop is how I build most features. Superpowers handles the process scaffolding (design docs, implementation plans, TDD, code review) while this kit handles the PM-specific content (frameworks, data integrations, specialist agents). They complement each other well.

---

## Quick Start

**Prerequisites:** [Claude Code](https://claude.ai/download) installed

### Install (2 commands)

```bash
claude plugin marketplace add ryancproduct/ai-pm-kit-marketplace
claude plugin install ai-pm-kit
```

That's it. All 19 commands, 23 skills, and 8 agents are now available.

### Verify

```
/jtbd "Users keep asking for dark mode"
```

### Optional: Personalise

Copy the CLAUDE.md template into your project to customise the toolkit for your team:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/ryancproduct/product-ai-toolkit/main/CLAUDE.md.template
```

Edit the "About Me" section with your role, company, and preferences.

### Optional: Connect your tools

The kit works best with MCP integrations for your PM stack. Run `/add-mcp` in Claude Code for guided setup — it will walk you through connecting Jira, Amplitude, Figma, Confluence, Slack, and other tools.

### Uninstall

```bash
claude plugin uninstall ai-pm-kit
claude plugin marketplace remove ai-pm-kit-marketplace
```

---

## Architecture

```
product-ai-toolkit/               ← This repo (the plugin)
├── .claude-plugin/
│   └── plugin.json               ← Plugin manifest
├── CLAUDE.md                     ← Plugin instructions (loaded automatically)
├── CLAUDE.md.template            ← Personal preferences template (copy to your project)
├── commands/                     ← Quick slash commands (single-file workflows)
│   ├── experiment.md
│   ├── customer-brief.md
│   ├── decision-brief.md
│   └── ... (19 total)
├── skills/                       ← Complex multi-step workflows
│   ├── debate/
│   ├── roadmap-narrative/
│   ├── decision-brief/
│   ├── churn-signal/
│   ├── sprint-health/
│   └── ... (23 total)
├── agents/                       ← Specialist agents for delegation
│   ├── customer-brief-analyst.md
│   ├── voice-of-customer.md
│   ├── data-storyteller.md
│   └── ... (8 total)
└── marketplace/                  ← Marketplace repo scaffold (publish separately)
    └── .claude-plugin/
        └── marketplace.json
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

**Personalise your instance:**
Copy `CLAUDE.md.template` to your project and edit the "About Me" section with your role, company, and preferences.

**Add your own commands:**
Create `~/.claude/commands/your-command.md` — it's live immediately as `/your-command`.

**Add your own agents:**
Create `~/.claude/agents/your-agent.md` with the agent's speciality and constraints.

**Add MCP integrations:**
Run `/add-mcp` for guided setup, or configure manually in your Claude Code settings.

**Swap frameworks:**
Fork the plugin and edit any skill's markdown file. Prefer RICE over ICE? Edit the prioritisation skill. Use a different PRD template? Update `skills/prd.md`.

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

## Recommended Schedules

Several skills are designed to run automatically as recurring remote agents. Use `/schedule` in Claude Code to set these up — they run in Anthropic's cloud infrastructure and post results to Slack, save to Confluence, or just land in your Claude Code inbox.

| Schedule | Cadence | What It Does | Skills Used |
|----------|---------|-------------|-------------|
| **Weekly VoC digest** | Monday 8am | Synthesises last 7 days of customer signal from Intercom, Slack, and Jira into confidence-ranked insight themes | `voice-of-customer` |
| **Sprint health check** | Wednesday 8am | Pulls active Jira sprint, flags stale/blocked tickets, compares % complete vs sprint elapsed | `sprint-health` |
| **Weekly metrics story** | Friday 4pm | Pulls core Amplitude metrics for the week and produces a narrative brief | `data-storyteller` |
| **Churn watch** | Monday 8am | Scores at-risk accounts by usage + sentiment signals, ranks by intervention priority | `churn-signal` |

Run `/schedule` and describe what you want — it will walk you through setting up the agent, connecting the right MCP sources, and choosing the right cadence.

---

## Data Security

All workflows that connect to production systems (Amplitude, Jira, Confluence, Slack) treat MCP data as confidential by default. Customer data is anonymised in outputs unless explicitly requested, financial data in impact sizing workbooks is flagged as commercially sensitive, and knowledge files warn against storing customer-specific information. No credentials or customer data are stored in the repository. See the Data Security & Privacy section in `CLAUDE.md` for full guidance.

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

**Ryan Clement** — Principal Product Manager at SafetyCulture

[LinkedIn](https://www.linkedin.com/in/ryancproduct/) · [GitHub](https://github.com/ryancproduct)

---

## Licence

MIT — use it, fork it, customise it, ship it.
