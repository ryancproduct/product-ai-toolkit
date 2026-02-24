---
name: prd
description: "Generate a SafetyCulture PRD using the standard template $ARGUMENTS"
---

# SafetyCulture PRD Generator

Generate comprehensive Product Requirements Documents using SafetyCulture's standard template. This skill creates PRDs with full problem alignment, solution details, and launch readiness checklists.

## Invocation

```
/prd "Feature name or description"
```

Or natural language:
- "Write a PRD for..."
- "Create a PRD about..."
- "Draft a product requirements doc for..."

---

## PRD Template Structure

### Header Metadata

```markdown
# [Feature Name] PRD

| Field | Value |
|-------|-------|
| **Status** | PROPOSED / INVESTIGATING / PLANNED / ON HOLD / DEV IN PROGRESS / SHIPPED - AWAITING RESULTS / WON'T DO / DONE |
| **Team** | [Squad name] |
| **Planned Release Date** | [Date] |
| **One liner** | [Single sentence describing the feature] |
| **Hypothesis** | [If we do X, then Y will happen, measured by Z] |
| **Dashboard** | [Link to tracking dashboard] |
| **Results** | [Filled in post-launch] |
| **Platform** | [ ] iOS (Release: XX) [ ] Android (Release: XX) [ ] Web |
| **Jira ticket** | [Link] |
```

---

## Problem Alignment 🤔

### The Problem
Guide the user to articulate:
- What problem (or opportunity) are you trying to solve?
- Why is it important to users AND the business?
- What insights led you to prioritize this? (data, research, customer feedback)
- **What problems are you NOT solving?** (explicit scope boundaries)

### High-level Approach
- Brief description of the solution direction
- Enough for readers to imagine possible solutions and understand scope
- Example: If problem is "users struggle to create templates", approach might be "AI-powered template creation from photos"

### Goals & Success
- Primary metrics to move (with targets if known)
- Secondary metrics
- Guardrail metrics (what shouldn't get worse)
- Link to tracking dashboard

### Results
- Leave blank initially
- Fill in post-launch with actual outcomes vs. targets

---

## Solution Alignment 💡

### Key Features
- Bullet list of features included in this release
- Be specific about what's in vs. out of scope

### Key Flows

**Prototype/Screenshots:**
Include links to Figma, prototypes, or describe the flows

**Platform Flow Comparison:**

| Platform | Flow Before Change | Flow After Change |
|----------|-------------------|-------------------|
| Web | [Current experience] | [New experience] |
| Android | [Current experience] | [New experience] |
| iOS | [Current experience] | [New experience] |

**Customer Action Required:**
- Do customers need to do something to enable/find this feature?
- If yes, outline what they need to do

### Implementation Approach

| Question | Answer |
|----------|--------|
| **Rollout strategy** | [Details of rollout, experiment, staged release] |
| **Feature flag** | [Flag name if applicable] |
| **Target cohort** | [Is there a specific customer list? Link if yes] |

### Open Issues & Key Decisions

| # | Issue | Decision |
|---|-------|----------|
| 1 | [Open question or risk] | [Decision made or "TBD"] |
| 2 | [Open question or risk] | [Decision made or "TBD"] |

---

## Launch Readiness 🚀

### Key Milestones

| Date | Milestone | Audience | Description |
|------|-----------|----------|-------------|
| [Date] | [Milestone name] | [Internal/Beta/GA] | [Details] |

### Comms Plan
- Internal announcement plan
- Customer communication plan
- Marketing coordination

### Launch Checklist

#### Product
- [ ] Are any other teams impacted? (platform, analytics, access, API/integrations)
- [ ] If yes, have they been across designs and plans?
- [ ] Have FAQs been written?
- [ ] Has localisation been considered?

#### Product Marketing
- [ ] Is Product Marketing aware of this release?
- [ ] Are customer comms needed? If yes, documented above?
- [ ] Has release been added to release comms plan calendar?

#### Support
- [ ] Have support articles been written or updated? [Link if required]
- [ ] Does support require training?

#### Sales
- [ ] Has the Sales team been enabled?

#### Data Analytics
- [ ] Is event tracking set up & tested?
- [ ] Has the dashboard for tracking been linked to this page?
- [ ] Should this feature be included in MAU events? If yes, updated?

#### Final Checks
- [ ] Announce release in #product-updates on Slack
- [ ] Update the status of this PRD

---

## References
- [Link to related docs, research, designs]

---

## Workflow

### Step 1: Gather Context
Ask the user for:
1. **Feature name** - What are we calling this?
2. **Problem statement** - What problem does this solve?
3. **Target users** - Who benefits?
4. **Key features** - What does it do?
5. **Platforms** - iOS? Android? Web?
6. **Team** - Which squad owns this?
7. **Timeline** - When is it planned?

### Step 2: Draft Problem Alignment
Focus on the "why" before the "what":
- Articulate the problem clearly
- Connect to business value
- Define success metrics
- Set explicit boundaries

### Step 3: Draft Solution Alignment
Detail the "what" and "how":
- List key features
- Describe user flows
- Document implementation approach
- Capture open issues

### Step 4: Complete Launch Readiness
Ensure nothing is missed:
- Set milestones
- Plan communications
- Work through checklist

### Step 5: Output & Iterate
- Generate complete PRD in markdown
- Offer to refine specific sections
- Suggest creating Confluence page

---

## Output Options

**Markdown (default):** Returns PRD as markdown text

**Confluence:** If user has Atlassian MCP connected, can create directly:
```
mcp__atlassian__createConfluencePage
```

**Word Document:** Use the /docx skill to export as .docx

---

## Tips for Quality PRDs

1. **Be specific about non-goals** - What are you explicitly NOT doing?
2. **Quantify success** - Vague goals lead to unclear outcomes
3. **Document decisions** - Capture the "why" behind controversial choices
4. **Keep it scannable** - Use tables, bullets, and clear headings
5. **Link don't duplicate** - Reference designs/research, don't copy
6. **Update status** - Keep the PRD current throughout development

---

## Example One-Liners by Type

**New Feature:**
"Enable users to schedule inspections in advance with automatic assignment"

**Improvement:**
"Reduce template creation time by 50% through AI-powered field suggestions"

**Migration:**
"Migrate existing Sheqsy users to Lone Worker platform with zero data loss"

**Technical:**
"Implement canonical template IDs to enable cross-organization sharing"

---

## Example Hypothesis Format

"If we [do this specific thing], then [this measurable outcome will happen], which we'll know by [this metric moving by this amount]"

**Good:** "If we add one-click template duplication, then template creation will increase by 20%, measured by templates created per user per month"

**Bad:** "If we improve the UX, users will be happier"
