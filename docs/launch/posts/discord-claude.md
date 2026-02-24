# Claude Code Discord Post

Hey folks — just open-sourced something I've been building with Claude Code that demonstrates some interesting patterns for agent coordination and MCP integration.

**AI PM Kit** — an operating system for Product Management work. 15 commands, 19 skills, 5 specialist agents, deep MCP integrations with Amplitude/Jira/Figma/Slack/Confluence.

**Novel patterns:**

**Parallel agent dispatch** — `/debate` spawns Champion and Sceptic agents that run concurrently on the same product idea, then synthesise findings. Way faster than sequential, and you get diverse perspectives automatically.

**MCP-grounded analysis** — agents query real data from your tools instead of making stuff up. The experiment skill validates events exist in your Amplitude taxonomy. The debate skill checks Jira for related work. Everything is traceable.

**Framework encoding** — PM methodologies (Jobs-to-be-Done, Teresa Torres, INVEST) implemented as structured workflows with validation. Not just templates — actual orchestrated logic.

Example: `/debate "Add a bulk actions feature"` coordinates two parallel agents pulling from Amplitude and Jira, then produces a risk register, MVP scope, and go/no-go recommendation.

It's all native Claude Code — skills, agents, MCP servers. No custom backend.

GitHub: https://github.com/ryancproduct/product-ai-toolkit
Article with details: [ARTICLE_LINK]

Would love feedback on the agent patterns — the parallel dispatch approach feels applicable way beyond PM.
