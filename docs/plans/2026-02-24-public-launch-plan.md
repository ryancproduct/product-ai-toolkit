# AI PM Kit — Public Launch Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Prepare the AI PM Kit for public open-source launch and create all supporting content for a staggered distribution campaign.

**Architecture:** Clean the existing repo of SC-specific references, write a compelling public README, draft the LinkedIn launch article, create tailored community post templates, and build a trackable launch calendar.

**Tech Stack:** Markdown, Git, GitHub

---

### Task 1: Initialise the public repo

**Files:**
- Create: `.gitignore`

**Step 1: Initialise git**

```bash
cd /Users/ryanclement/Desktop/sc-ai-pm-kit
git init
```

**Step 2: Create .gitignore**

```
.DS_Store
*.swp
*.swo
*~
.env
```

**Step 3: Initial commit**

```bash
git add -A
git commit -m "chore: initial commit — SC internal version"
```

This preserves the original state before we start modifying.

---

### Task 2: Strip SafetyCulture-specific references from core files

**Files:**
- Modify: `README.md`
- Modify: `CLAUDE.md`
- Modify: `skills/prd.md`
- Modify: `commands/rapid-prototype.md`
- Modify: `agents/prototype-builder.md`

**Step 1: Update README.md**

Changes:
- Title: "The SC AI PM Kit" → "AI PM Kit"
- Line 3: "how PM works at SafetyCulture" → "a practical AI-native PM workflow"
- Line 117: "Ryan Clement, Principal Product Manager at SafetyCulture" → "Ryan Clement — [LinkedIn](URL) · [GitHub](URL)"

**Step 2: Update CLAUDE.md**

This file becomes a *template* for users to customise. Changes:
- Line 4: "Principal Product Manager at SafetyCulture" → "[Your role] at [Your company]"
- Add a comment at top: `<!-- Customise this file for your context -->`

**Step 3: Update skills/prd.md**

- Line 3: "Generate a SafetyCulture PRD" → "Generate a PRD"
- Line 6: "SafetyCulture PRD Generator" → "PRD Generator"
- Line 8: "SafetyCulture's standard template" → "a standard PRD template"
- Line 232: Replace Sheqsy/Lone Worker example with a generic example (e.g. "Migrate existing users from legacy platform to new unified experience")

**Step 4: Update commands/rapid-prototype.md and agents/prototype-builder.md**

- Replace "SafetyCulture UI prototypes" → "UI prototypes"
- Replace "SafetyCulture's zero-build HTML" → "zero-build HTML"
- Replace absolute paths `/Users/ryanclement/Desktop/AI_space/Rapid Prototype Starter pack/` → relative paths or `[YOUR_PROTOTYPE_TEMPLATES_PATH]`

**Step 5: Commit**

```bash
git add README.md CLAUDE.md skills/prd.md commands/rapid-prototype.md agents/prototype-builder.md
git commit -m "chore: generalise core files — remove SC-specific branding"
```

---

### Task 3: Strip SafetyCulture-specific references from impact-sizing skill

This is the most affected skill — contains internal URLs, FY metrics, and restricted resources.

**Files:**
- Modify: `skills/impact-sizing/SKILL.md`
- Modify: `skills/impact-sizing/README.md`
- Modify: `skills/impact-sizing/generate_impact_sizing.py`

**Step 1: Update SKILL.md**

- "SafetyCulture's impact sizing methodology" → "an impact sizing methodology"
- "SafetyCulture's strategic focus" → "[Your company's strategic focus]"
- Replace specific industries (Manufacturing, Retail + QSR, etc.) with `[Your target verticals]`
- Remove or template all internal URLs:
  - Salesforce report link → `[YOUR_CRM_REPORT_URL]`
  - Productboard link → `[YOUR_FEEDBACK_TOOL_URL]`
  - Twine link → `[YOUR_RESEARCH_TOOL_URL]`
  - Internal Google Slides → `[YOUR_STRATEGY_DECK_URL]`
  - FY25/FY26 deep-dive links → Remove
- Replace FY26 metrics table with example placeholder values

**Step 2: Update README.md**

- Same pattern: generalise SafetyCulture references, template internal URLs
- Replace "Key SafetyCulture Reference Data (FY26)" → "Key Reference Data (Example)"
- Replace actual metrics with realistic but fictional example values

**Step 3: Update generate_impact_sizing.py**

- Docstring: "SafetyCulture's methodology" → "impact sizing methodology"
- Lines 578-586: Remove all RESTRICTED/internal URLs from data sources section
- Replace with template: `# Add your internal data source URLs here`

**Step 4: Commit**

```bash
git add skills/impact-sizing/
git commit -m "chore: generalise impact-sizing skill — template internal references"
```

---

### Task 4: Strip SafetyCulture-specific references from rapid-prototype skill

**Files:**
- Modify: `skills/rapid-prototype/SKILL.md`

**Step 1: Update SKILL.md**

- Replace SafetyCulture design system references with generic equivalents
- Replace absolute file paths with relative paths or template placeholders
- Keep the design system pattern but make it configurable

**Step 2: Commit**

```bash
git add skills/rapid-prototype/
git commit -m "chore: generalise rapid-prototype skill"
```

---

### Task 5: Rewrite the public README

The README is the single most important file for adoption. It needs to sell the kit in 30 seconds and get someone started in 5 minutes.

**Files:**
- Modify: `README.md`

**Step 1: Write the new README**

Structure:
```markdown
# AI PM Kit

> A practical AI operating system for Product Management — turning Claude Code into a PM superpower.

[Architecture diagram image]

## Why This Exists

Most PMs using AI are copy-pasting into ChatGPT and getting generic answers back...
[3-4 sentences on context engineering > prompt engineering]

## What's Inside

### Commands — Quick PM Workflows
[Table: 15 commands grouped by category]

### Skills — Complex Multi-Step Workflows
[Table: key skills with one-line descriptions]

### Agents — Specialist Delegation
[Table: 9 agents]

### MCP Integrations
[Table: tool categories — note these are configurable]

## Demo

### `/debate` — Stress-test a product idea
[GIF placeholder]

### `/experiment` — Design an A/B test
[GIF placeholder]

### `/rapid-prototype` — Idea to prototype in minutes
[GIF placeholder]

## Quick Start

1. Clone this repo
2. Copy contents to `~/.claude/`
3. Customise `CLAUDE.md` for your context
4. Configure MCP servers for your tools
5. Run `/debate my feature idea` and see what happens

## Architecture
[Directory tree + design philosophy paragraph]

## Key Patterns
[5 patterns: parallel agents, MCP-grounded, framework-driven, flexible input, structured output]

## Customising for Your Team
[Short guide on adapting CLAUDE.md, swapping frameworks, adding MCP integrations]

## Built By
Ryan Clement — [LinkedIn] · [GitHub]
```

**Step 2: Commit**

```bash
git add README.md
git commit -m "docs: rewrite README for public launch"
```

---

### Task 6: Record demo GIFs

**This is a manual task for Ryan.** Cannot be automated.

Record 2-3 short (30-60 second) screen recordings showing:
1. `/debate` — Give it a feature idea, show the parallel agents running, show the output
2. `/experiment` — Design an A/B test, show Amplitude integration
3. `/rapid-prototype` — Idea to clickable HTML

Tools: Use macOS screen recording or a tool like Kap (free, exports to GIF).

Save to: `docs/demos/` directory in the repo.

**Step 1: Create demos directory**

```bash
mkdir -p docs/demos
```

**Step 2: Record GIFs (manual)**

**Step 3: Add to README with image links**

---

### Task 7: Draft the LinkedIn article

**Files:**
- Create: `docs/launch/linkedin-article.md`

**Step 1: Write the article**

Target: 800-1200 words. Structure:

```markdown
# Most PMs Are Using AI Wrong. Here's What Actually Works.

[Hook — the problem with copy-paste AI usage]

[The shift — context engineering, not prompt engineering]

[Show don't tell — 3 concrete examples with what happened]

[The toolkit — "I've open-sourced the whole system"]

[The invitation — take it, adapt it, tell me what you'd add]

[Link to repo]
```

Tone: Conversational, practitioner voice. No jargon, no hype.

**Step 2: Commit**

```bash
git add docs/launch/
git commit -m "docs: draft LinkedIn launch article"
```

---

### Task 8: Create community post templates

**Files:**
- Create: `docs/launch/posts/show-hn.md`
- Create: `docs/launch/posts/reddit-productmanagement.md`
- Create: `docs/launch/posts/reddit-claudeai.md`
- Create: `docs/launch/posts/discord-claude.md`
- Create: `docs/launch/posts/twitter.md`
- Create: `docs/launch/posts/product-hunt.md`
- Create: `docs/launch/posts/slack-communities.md`

**Step 1: Write tailored posts for each platform**

Each post adapted to the community's norms:
- **Show HN:** Technical, concise, focus on the architecture and patterns
- **Reddit r/ProductManagement:** Problem-first, practical, "here's what I built"
- **Reddit r/ClaudeAI:** Focus on Claude Code skills, MCP integrations, parallel agents
- **Discord:** Casual, link-forward, "check this out"
- **X/Twitter:** 280 chars + GIF + link. Punchy.
- **Product Hunt:** Tagline, description, maker comment
- **Slack communities:** Conversational, "been working on this, thought you might find it useful"

**Step 2: Commit**

```bash
git add docs/launch/posts/
git commit -m "docs: add community post templates"
```

---

### Task 9: Create outreach templates

**Files:**
- Create: `docs/launch/outreach/anthropic.md`
- Create: `docs/launch/outreach/newsletter-authors.md`
- Create: `docs/launch/outreach/conference-cfps.md`

**Step 1: Write outreach messages**

- **Anthropic:** Short email/DM pitching as a Claude Code case study
- **Newsletter authors:** Personalised template for Lenny, Shreyas, Claire Vo — "built this, thought your audience would find it useful"
- **Conference CFPs:** Talk abstract: "How I Built an AI Operating System for Product Management"

**Step 2: Commit**

```bash
git add docs/launch/outreach/
git commit -m "docs: add outreach templates"
```

---

### Task 10: Build the launch calendar

**Files:**
- Create: `docs/launch/launch-calendar.md`

**Step 1: Write the calendar**

Markdown table with:
- Date (relative: "Launch Day", "Day +1", etc.)
- Action
- Platform
- Template reference (link to the post file)
- Estimated time
- Status checkbox

Cover: Pre-launch prep, Week 1 (daily), Week 2 (daily), Weeks 3+ (weekly cadence).

**Step 2: Commit**

```bash
git add docs/launch/launch-calendar.md
git commit -m "docs: add launch calendar"
```

---

### Task 11: Push to GitHub

**Step 1: Create the GitHub repo**

```bash
gh repo create ai-pm-kit --public --description "A practical AI operating system for Product Management — turning Claude Code into a PM superpower" --source .
```

**Step 2: Push**

```bash
git push -u origin main
```

**Step 3: Add repo topics/tags**

```bash
gh repo edit ai-pm-kit --add-topic claude-code,product-management,ai,mcp,claude,pm-tools
```

---

### Task 12: Final review

**Step 1: Read through entire repo on GitHub**

Check:
- No internal URLs remain
- No credentials or API keys
- README renders correctly with images
- All links work
- .gitignore is catching the right files

**Step 2: Share repo link with a trusted colleague for a sanity check**

---

## Execution Order

```
Task 1  → Task 2 → Task 3 → Task 4  (sequential: repo setup then cleaning)
Task 5  (depends on 2-4: README rewrite after cleaning)
Task 6  (manual: can happen in parallel with anything)
Task 7  (depends on 5: article references the repo)
Task 8  (depends on 7: posts reference the article)
Task 9  (depends on 5: outreach references the repo)
Task 10 (depends on 8, 9: calendar references all templates)
Task 11 (depends on all above)
Task 12 (depends on 11)
```

## Time Estimates

| Task | Est. Time |
|------|-----------|
| Task 1: Init repo | 5 min |
| Task 2: Clean core files | 20 min |
| Task 3: Clean impact-sizing | 30 min |
| Task 4: Clean rapid-prototype | 15 min |
| Task 5: Rewrite README | 45 min |
| Task 6: Record demo GIFs | 30-60 min (manual) |
| Task 7: LinkedIn article | 45 min |
| Task 8: Community posts | 30 min |
| Task 9: Outreach templates | 20 min |
| Task 10: Launch calendar | 15 min |
| Task 11: Push to GitHub | 5 min |
| Task 12: Final review | 15 min |
| **Total** | **~4-5 hours** |
