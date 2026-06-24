# Changelog

## 1.2.0

Modernisation pass — fixed broken agent definitions and brought all content up to date.

**Fixed agents (broken frontmatter / placeholder content)**
- `ux-designer` — Replaced with proper YAML frontmatter and a focused, practical system prompt. Previous version had no frontmatter and a generic "design visionary" persona that didn't match PM use cases.
- `data-brief-analyst` — Fixed broken frontmatter (heading before `---`), name mismatch (`deep-data-storyteller`), and CLOSED-BOOK rule that prevented MCP tool use.
- `prototype-builder` — Removed `[YOUR_PROTOTYPE_TEMPLATES_PATH]` placeholders. Now uses Tailwind CDN and works out of the box with no local setup.

**Updated commands**
- `standup` — Removed git commit references (wrong for PMs). Now pulls from Jira, Slack, and Confluence.
- `metrics-dashboard` — Rewired to use Amplitude MCP. Removed generic AARRR template that didn't use live data.
- `add-mcp` — Updated to mention the primary path (claude.ai/customize/connectors) first. CLI instructions kept for local/self-hosted servers.

**Updated documentation**
- README MCP table — Removed Docker/GitHub (not MCP integrations), added Intercom, Google Calendar, Gmail, Google Drive, Zoom, Twine which are the actual connected tools.
- README — Added "Recommended Schedules" section with four recurring automation patterns.
- CLAUDE.md.template — Added available agents list (was missing entirely).

---

## 1.1.0

Intelligence layer — 3 new agents, 4 new skills, 4 new commands.

**New Agents**
- `customer-brief-analyst` — Pre-meeting intel brief on any customer account. Pulls Amplitude, Intercom, Glean, Jira, and Slack into a 1-page brief with usage health, open issues, and talking points.
- `voice-of-customer` — Synthesises ambient customer signals (Intercom, Slack, Jira, Glean) into confidence-ranked insight themes. Designed for roadmap planning and stakeholder alignment.
- `data-storyteller` — Turns Amplitude metrics into narrative insight briefs. Classifies the story type (growth, decline, divergence, mystery), frames the "so what", and produces exec or team-calibrated output.

**New Skills**
- `roadmap-narrative` — One input, three polished outputs: exec summary, engineering brief, and customer-facing narrative.
- `decision-brief` — Structured 1-pager for any product decision. Options, trade-offs, assumptions, recommendation, and one next step.
- `churn-signal` — Account health assessment combining usage data and sentiment signals into a scored health rating with recommended intervention.
- `sprint-health` — Mid-sprint or end-of-sprint delivery check. Surfaces blockers, compares planned vs done, produces a copy-paste Slack update.

**New Commands**
- `/customer-brief` — Wrapper for the customer-brief-analyst agent
- `/roadmap-narrative` — Wrapper for the roadmap-narrative skill
- `/decision-brief` — Wrapper for the decision-brief skill
- `/sprint-health` — Wrapper for the sprint-health skill

**Fixes**
- `.gitignore` now excludes `skills/*.zip` build artifacts
- README, CLAUDE.md, and plugin.json updated to reflect new counts and agent descriptions

---

## 1.0.0

Initial release as a Claude Code plugin.

- 15 PM commands (experiment, jtbd, competitive-analysis, user-stories, and more)
- 19 skills (debate, interview-analysis, impact-sizing, learn, and more)
- 5 specialist agents (market-research-analyst, cpto-review, ux-designer, prototype-builder, data-brief-analyst)
- Marketplace scaffold for easy distribution
- Data security guardrails for MCP-connected workflows
