# Show HN Post

**Title:** Show HN: AI PM Kit – Open-source AI operating system for Product Management

I've built an open-source AI operating system for Product Management that runs on Claude Code. It's a collection of commands, skills, and specialist agents that encode actual PM frameworks into executable AI workflows.

The architecture is built around three core patterns: (1) Parallel agent dispatch — multiple specialist agents run concurrently on the same problem, then synthesise findings; (2) MCP-grounded analysis — agents query real data from Amplitude, Jira, Figma, Slack, and Confluence rather than hallucinating context; (3) Framework encoding — PM methodologies (Jobs-to-be-Done, Teresa Torres, INVEST) are implemented as structured workflows with validation logic.

The kit includes 15 commands (like `/debate`, `/experiment`, `/impact-sizing`), 19 skills, and 5 specialist agents. Each agent has domain-specific prompting, tool access, and quality gates. For example, `/debate` spawns Champion and Sceptic agents that argue for and against a feature idea using real analytics data, then synthesises into a risk register and go/no-go recommendation.

Technically interesting bits: agents use Claude Code's Task tool with MCP servers for parallel dispatch; all framework logic is version-controlled as markdown; the entire system is zero-dependency — just markdown files, a Python script, and some JS. Built this because PM tools are mostly project management software with AI chat bolted on — this inverts that by making AI workflows first-class and grounding them in actual PM practice.

Open to feedback on the agent coordination patterns. Code and docs: https://github.com/ryancproduct/product-ai-toolkit
