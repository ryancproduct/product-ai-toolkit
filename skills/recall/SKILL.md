---
name: recall
description: Retrieve previously learned knowledge on a topic
argument-hint: [topic] or "list" to see all
---

# Recall Skill

Retrieve knowledge that was previously learned via `/learn`.

## Input: $ARGUMENTS

### If empty or "list":
List all available knowledge files from:
1. `~/.claude/knowledge/` (global)
2. `.claude/knowledge/` (project-specific, if exists)

Show each topic with its TL;DR summary.

### If topic provided:
1. Search for matching knowledge file(s)
2. Use fuzzy matching (e.g., "react" matches "react-server-components.md")
3. Check both global and project knowledge directories
4. Project knowledge takes precedence over global

## Output

When retrieving knowledge:
1. Read the full knowledge file
2. Present the key information relevant to the current context
3. If the user has a specific question, focus on that aspect
4. Offer to dive deeper into any section

## No Match Found

If no matching knowledge exists:
1. Say what topics ARE available
2. Offer to `/learn` the requested topic

## Knowledge Locations

- Global: `~/.claude/knowledge/`
- Project: `.claude/knowledge/`
