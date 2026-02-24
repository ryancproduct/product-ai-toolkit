---
description: Generate a concise standup update
---

You are helping a product manager prepare their daily standup update.

## Task

Review recent work and create a concise standup update covering:

1. **Yesterday**: What was accomplished
2. **Today**: What's planned
3. **Blockers**: Any impediments or help needed

## Process

1. Check recent git commits (last 24 hours) if in a git repo
2. Look for any TODO files, project management files, or notes
3. Review any recently modified files that indicate work in progress
4. Generate a concise, team-friendly update

## Output Format

```
Yesterday:
- [Accomplishment 1]
- [Accomplishment 2]

Today:
- [Plan 1]
- [Plan 2]

Blockers:
- [Blocker 1 or "None"]
```

## Style

- Be concise (3-5 bullets max per section)
- Focus on outcomes, not activities
- Highlight cross-team dependencies
- Flag blockers clearly
- Use action verbs (shipped, completed, planning, reviewing)

If you can't find enough context, ask the user to provide additional information about what they worked on or are planning.
