# AI PM Kit

You have the AI PM Kit plugin installed. This gives you PM-specific commands, skills, and agents.

## Smart Delegation

For complex multi-step work, prefer delegation to agents. For everything else, just do it.

**Workflow for complex tasks:**
1. **Check existing knowledge first** — Use `/recall` to see what you already know
2. **Learn if needed** — Use `/learn` to explore and understand unfamiliar topics
3. **Delegate to agents** — Use the Task tool with appropriate agents for parallel or deep work

**Don't delegate** simple, single-step tasks, quick questions, or synthesis work.

## Data Security & Privacy

Many workflows in this kit connect to production systems (Amplitude, Jira, Confluence, Slack, Glean) and process sensitive data. Follow these principles:

- **Assume MCP data is sensitive.** Data pulled from Amplitude, Jira, Confluence, and Slack is live production data — treat it as confidential by default.
- **Anonymise customer data in outputs.** When producing interview analyses, impact sizing, or any deliverable that references specific customers, anonymise names and identifying details unless the user explicitly asks for real names.
- **Be careful with web search.** Competitive analysis and market research use external search. Avoid including your company name, internal product names, or strategic context in search queries — these are visible to search providers.
- **Knowledge files persist indefinitely.** `/learn` saves to `~/.claude/knowledge/` with no expiry. Don't store customer-specific data, financial figures, or confidential strategy in knowledge files — they accumulate over time and aren't encrypted.
- **Financial data needs care.** Impact sizing outputs contain customer names, deal values, ARR, and churn data. Store workbooks securely and don't share via unsecured channels.
- **Review before posting.** Workflows that post to Slack, create Confluence pages, or create Jira issues are visible to others. Check sensitivity before pushing to shared systems.

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
