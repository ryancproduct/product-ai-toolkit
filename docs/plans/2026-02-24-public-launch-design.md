# AI PM Kit — Public Launch Design

**Date:** 2026-02-24
**Author:** Ryan Clement
**Status:** Approved

## Positioning

"A practical AI operating system for Product Management — turning Claude Code into a PM superpower."

**Tone:** Practitioner sharing their toolkit. No hype, no "10x" claims. Concrete, grounded, show-don't-tell.

**Core narrative:**
1. **The problem:** Most PMs using AI are copy-pasting into ChatGPT and getting generic answers disconnected from their tools, data, and frameworks.
2. **The insight:** The unlock is context engineering — encode your PM frameworks (JTBD, Teresa Torres, INVEST), connect your real tools (Amplitude, Jira, Figma), and build workflows with specialist agents.
3. **The proof:** A working open-source system with 15 commands, 14+ multi-step skills, 9 specialist agents, and deep MCP integrations.
4. **The invitation:** Take it, adapt it, make it yours.

## Release Model

Full open source on GitHub as `ai-pm-kit`.

## Deliverables

### 1. Cleaned Public Repo
- New repo: `ai-pm-kit`
- Strip SafetyCulture-specific branding, internal URLs, proprietary references
- Generalise terminology so any PM team can adopt it

### 2. README.md
- **Hero section** — One-liner + architecture diagram (hub-and-spoke)
- **What is this?** — 3-4 sentences on context engineering and practical PM workflows
- **What's included** — Skills table grouped by category (Discovery, Execution, Analytics, Prototyping, Communication)
- **Demo GIFs** — 2-3 screen recordings (debate, experiment, rapid-prototype)
- **Quick start** — Clone, copy to `~/.claude/`, configure MCP servers
- **MCP integrations** — What tools it connects to
- **Philosophy** — Short paragraph on context engineering

### 3. LinkedIn Article
- **Hook:** "Most PMs are using AI wrong..."
- **Problem:** Generic AI outputs disconnected from real work
- **The shift:** Context engineering, one paragraph
- **Show don't tell:** 2-3 examples with screenshots/GIFs (debate, experiment, rapid-prototype)
- **The toolkit:** "I've open-sourced the whole thing" + repo link
- **Invitation:** "Take it, adapt it, tell me what you'd add"

### 4. Community Post Templates
Shorter versions tailored for each platform:
- Hacker News (Show HN)
- Reddit (r/ProductManagement, r/ClaudeAI)
- Claude Code Discord
- X/Twitter
- Lenny's Slack / Mind the Product Slack
- Product Hunt listing

### 5. Outreach Templates
- Anthropic (case study pitch)
- Newsletter authors (Lenny, Shreyas, Claire Vo)
- Conference CFPs

### 6. Launch Calendar
Spreadsheet with dates, actions, time estimates, and status tracking.

## Distribution Strategy

### Tier 1: High-signal, high-reach (Launch day + 48 hrs)
- LinkedIn article
- Show HN
- Claude Code Discord
- X/Twitter

### Tier 2: PM communities (Days 3-7)
- Lenny's Newsletter Slack
- r/ProductManagement
- Mind the Product Slack
- Product Hunt

### Tier 3: AI communities (Week 2)
- r/ClaudeAI
- r/artificial / Dev.to
- Anthropic outreach
- Newsletter author outreach

### Tier 4: Ongoing amplification
- SafetyCulture engineering/product blog (if approved)
- Conference CFPs (ProductCon, Mind the Product, AI Engineer Summit)

## Launch Calendar

### Pre-launch (Week 0)
- Fork/clean repo
- Write README
- Record 2-3 demo GIFs
- Draft LinkedIn article
- Prepare community post templates

### Week 1

| Day | Action | Est. Time |
|-----|--------|-----------|
| Mon | Push repo, publish LinkedIn article | 1-2 hrs |
| Mon | Post to Claude Code Discord | 15 min |
| Tue | Submit Show HN | 15 min |
| Wed | Post to X/Twitter with GIF + link | 15 min |
| Thu | Share in Lenny's Slack + Mind the Product Slack | 20 min |
| Fri | Post to r/ProductManagement | 15 min |
| Daily | Respond to comments and questions | 15-20 min/day |

### Week 2

| Day | Action | Est. Time |
|-----|--------|-----------|
| Mon | Post to r/ClaudeAI | 15 min |
| Tue | Submit to Product Hunt | 30 min |
| Wed | Post to r/artificial or Dev.to | 15 min |
| Thu | Reach out to Anthropic | 20 min |
| Fri | Reach out to newsletter authors | 30 min |

### Ongoing (Weeks 3+, ~2 hrs/week)
- One LinkedIn post per week (specific workflow or learning)
- Respond to GitHub issues/discussions
- Submit to conference CFPs as they open

## Success Metrics
- GitHub stars (target: 100+ in first month)
- LinkedIn article views/engagement
- Inbound messages/connection requests
- Community discussion and contributions
- Speaking/advisory opportunities that emerge
