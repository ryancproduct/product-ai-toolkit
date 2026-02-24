# Reddit r/ClaudeAI Post

**Title:** Built a PM operating system with parallel agent dispatch and MCP-grounded analysis — open source

I've been experimenting with Claude Code's agent and MCP capabilities and built something that might interest this community — an open-source AI operating system for Product Management that demonstrates some novel patterns for agent coordination and tool grounding.

**Architecture highlights:**

**Parallel Agent Dispatch** — Multiple specialist agents run concurrently using the Task tool. Each agent has domain-specific system prompts, tool access rules, and quality gates. Results are aggregated using structured synthesis. Example: `/debate` spawns Champion and Sceptic agents that argue for/against a product idea in parallel, then synthesise.

**MCP-Grounded Analysis** — Agents query real data through MCP servers (Amplitude for analytics, Jira for engineering context, Figma for design, Slack for conversations, Confluence for docs). This eliminates the classic AI problem of hallucinating metrics — everything is traceable to source.

**Framework Encoding** — PM frameworks (Jobs-to-be-Done, Teresa Torres, INVEST, RICE, etc.) are implemented as structured workflows. Not just "here's a template", but actual workflow orchestration that guides the model through proper application of the methodology.

**Skills as Reusable Modules** — 19 Claude Code skills that can be composed into larger workflows, plus 15 commands for common tasks and 5 specialist agents for delegation.

The kit includes commands like `/debate` (parallel stress-test of product ideas), `/experiment` (full A/B test design with Amplitude validation), `/impact-sizing` (ARR estimation with Excel output), and `/interview-analysis` (parallel analysis of customer interviews).

Everything runs locally on Claude Code — no custom backends. All the intelligence is in context engineering and workflow orchestration.

Open source: https://github.com/ryancproduct/product-ai-toolkit
Detailed write-up: [ARTICLE_LINK]

Keen to hear thoughts on the parallel agent patterns and whether folks see applications beyond PM workflows.
