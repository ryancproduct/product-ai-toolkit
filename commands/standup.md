---
description: Generate a concise PM standup update by pulling from Jira and recent activity
---

You are helping a product manager prepare their daily standup update.

## Task

Pull recent activity from available sources and generate a concise standup covering Yesterday, Today, and Blockers.

## Data Sources (use what's available, skip what isn't)

1. **Jira** (primary) — Search for issues updated in the last 24-48 hours assigned to or created by the user. Look for recently transitioned tickets (moved to Done, In Review, or In Progress).
2. **Slack** — Any key decisions, updates, or async threads from yesterday that are worth surfacing.
3. **Confluence** — Any pages created or updated recently by the user.
4. **User input** — If no integrations are connected, ask: "What did you work on yesterday and what's on the agenda today?"

## Output Format

```
📋 Standup — [Day, Date]

Yesterday:
- [Accomplishment or progress — outcome-focused, not activity-focused]
- [e.g., "Shipped [feature] to staging — ready for QA sign-off"]

Today:
- [Plan 1 — specific and actionable]
- [Plan 2]

Blockers:
- [Specific blocker with owner, or "None"]
```

## Style

- 3-5 bullets max per section
- Outcomes over activities: "closed 3 discovery interviews" not "did customer research"
- Name the specific ticket or feature, not just the category of work
- Blockers should name who can unblock them
- If it was a meeting-heavy day, summarise key decisions made, not just meetings attended

If the user provides additional context, incorporate it. Keep the whole thing to under 10 lines.
