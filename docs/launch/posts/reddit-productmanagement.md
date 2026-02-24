# Reddit r/ProductManagement Post

**Title:** I built an open-source AI toolkit for PM work that actually uses real PM frameworks

I've spent the last while building something I wish existed when I started in Product — an AI system that actually understands PM workflows, not just generic "write me a PRD" prompts.

**The problem:** Most AI tools for PMs are either too generic (ChatGPT with no context about your product) or too narrow (single-purpose copilots). Nothing that actually mirrors how we work — synthesis from multiple sources, framework-driven thinking, evidence-based decisions.

**What I built:** An open-source AI toolkit called AI PM Kit. It runs on Claude Code and includes 15 commands, 19 skills, 5 specialist agents, and deep integrations with the tools we actually use (Amplitude, Jira, Figma, Slack, Confluence).

**How it's different:**

- **Real frameworks, not vibes** — Jobs-to-be-Done, Teresa Torres Opportunity Solution Trees, INVEST criteria, Porter's Five Forces — all encoded into the workflows with proper structure
- **Grounded in your actual data** — agents pull real metrics from Amplitude, real issues from Jira, real designs from Figma. No hallucinated "insights"
- **Parallel expert perspectives** — `/debate` spawns Champion and Sceptic agents that argue for and against your feature idea using real data, then synthesise into a risk register and recommendation
- **Practical workflows** — `/experiment` designs a full A/B test and validates your analytics events exist; `/impact-sizing` generates an Excel workbook with ARR calculations

Example: run `/debate "Add a bulk actions feature"` and it coordinates two specialist agents — one making the case with your analytics data, the other poking holes grounded in your actual constraints. Output: risk register, MVP scope, go/no-go recommendation.

It's open source because I think this pattern (AI + PM frameworks + real data) is more valuable as a community resource than a SaaS product.

More details: [ARTICLE_LINK]
GitHub: https://github.com/ryancproduct/product-ai-toolkit

Would love feedback from other PMs on which workflows would be most useful to add next.
