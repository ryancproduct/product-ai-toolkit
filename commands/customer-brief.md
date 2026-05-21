---
description: Pre-meeting customer intel brief — usage, support sentiment, open issues, and talking points for any account $ARGUMENTS
---

You are generating a pre-meeting customer brief. Use the `customer-brief-analyst` agent via the Task tool.

## Task

Delegate to the `customer-brief-analyst` agent with the customer name from $ARGUMENTS.

If no customer name is provided, ask:
> "Which customer account do you need a brief on?"

## Execution

Invoke the `customer-brief-analyst` agent:
- Pass the customer name
- Pass any additional context provided (meeting type, specific focus area)
- The agent will pull from Amplitude, Intercom, Glean, Jira, and Slack

Return the completed brief to the user.
