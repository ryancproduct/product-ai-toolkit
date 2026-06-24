---
name: sprint-health
description: Mid-sprint or end-of-sprint health check. Pulls Jira sprint data, compares planned vs in-progress vs done, surfaces blockers and risks, and produces a concise status update ready to share. Use when you need a quick read on delivery health without manually trawling Jira.
---

# Sprint Health Skill

Get an instant read on how a sprint is tracking. Pulls from Jira, surfaces the critical path, flags blockers, and produces a shareable status update.

## Input: $ARGUMENTS

Accepts:
- `/sprint-health` — Checks the current active sprint (will try to auto-detect)
- `/sprint-health [sprint name or ID]` — Target a specific sprint
- `/sprint-health [team name]` — Target a specific team's sprint

If Jira integration isn't available, ask the user to paste their sprint board or provide a summary, and work with that.

---

## Phase 1: Pull Sprint Data

Use Jira MCP tools to:
1. Find the active sprint (or specified sprint)
2. Get all issues in the sprint
3. Categorise by status: To Do / In Progress / In Review / Done
4. Pull blockers (issues flagged or with no progress in 3+ days)
5. Note capacity: planned story points vs completed

If sprint isn't found or Jira isn't available:
> "I couldn't connect to Jira. Can you paste your sprint board summary or describe what's in the sprint? I'll work with that."

---

## Phase 2: Analyse Health

### Velocity Check
- % of sprint completed by today relative to % of sprint elapsed
- Are we ahead, on track, or behind?
- Rule of thumb: At sprint midpoint, ~40-50% of work should be done (accounting for late-sprint integration/testing)

### Risk Identification
Flag issues that match any of these patterns:
- **Stale** — No status change in 3+ days (in-progress but not moving)
- **Blocked** — Explicitly flagged as blocked
- **Scope creep** — Issues added to sprint after it started
- **Missing estimates** — Stories without points that could hide capacity issues
- **Critical path** — Items that other items depend on

### Scope vs Plan
- Were any items added mid-sprint?
- Were any removed?
- Net: are we over-committed?

---

## Phase 3: Output

```markdown
# Sprint Health: [Sprint Name]
**Date**: [Today] | **Sprint**: Day [X] of [Y] | **Team**: [if known]

---

## Overall Health: 🟢 On Track / 🟡 Watch / 🔴 At Risk

**Completion rate**: [X]% done vs [Y]% of sprint elapsed
**Target**: [On track if ≥ Z% complete by today]

---

## Snapshot

| Status | Count | Story Points |
|---|---|---|
| Done | | |
| In Review | | |
| In Progress | | |
| To Do | | |
| **Total** | | |

---

## Blockers & Risks
[If none: "No blockers identified."]

🚨 **Blocked**: [Issue key + title — what's blocking it?]
⚠️ **Stale** (3+ days no movement): [Issue key + title]
⚠️ **No estimate**: [Issue key + title — adds uncertainty to forecast]

---

## Scope Changes Since Sprint Start
[Issues added]: [List or "None"]
[Issues removed]: [List or "None"]

---

## Forecast

**Likely to complete**: [Items highly likely to ship this sprint]
**At risk of slipping**: [Items that may not make it — why?]
**Almost certainly slipping**: [Items that are very unlikely to finish]

---

## What Needs to Happen Today
1. [Most urgent action — owner if known]
2. [Second action]
3. [Third action, if applicable]

---

## Status Update (Copy-Paste Ready)

> 🏃 **Sprint [Name] — Day [X] of [Y]**
> [X]% complete. [One sentence on overall health].
> [One sentence on the biggest risk or blocker].
> [One sentence on what the team is focusing on to finish strong].
```

---

## End-of-Sprint Mode

If the sprint is complete (or within 1 day of end), add a retrospective-ready section:

```markdown
## Sprint Retrospective Inputs

**Committed**: [N points / N issues]
**Delivered**: [N points / N issues] — [X]% completion rate

**Carried over**: [List issues not completed]

**What slowed us down**: [Inferred from blockers and stale issues]

**What should we do differently**: [1-2 suggestions based on patterns observed]
```

---

## Principles

- **Be specific about risk.** "At risk" without naming the ticket is useless. Link to the actual issue.
- **Don't pad healthy sprints.** If everything is on track, say so clearly. Not everything needs a risk section.
- **The status update is the product.** Make it copy-paste ready — the PM should be able to drop it straight into Slack.
- **Infer, but label it.** "This ticket has had no movement for 4 days — likely blocked or deprioritised" is a useful inference. Label it as such.
