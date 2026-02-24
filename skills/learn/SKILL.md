---
name: learn
description: Deep-dive research on a topic, saving knowledge for future reference
---

# Learn Skill

You are conducting deep research to build lasting knowledge on a topic. This is NOT a quick answer - spend real time investigating thoroughly.

## Input Parsing

Parse $ARGUMENTS to determine mode:
- **Research mode**: Just a topic (e.g., "React Server Components", "product research best practices")
- **Document mode**: Topic + "from" + path/URL (e.g., "API design from ./docs/api-guide.md")

## Research Process

### For Research Mode (no document provided):
1. **Web Search**: Search for current best practices, official docs, expert opinions
2. **Multiple Sources**: Gather from 3-5 authoritative sources minimum
3. **Deep Reading**: Actually read and synthesize, don't just skim
4. **Current Info**: Prioritize recent content (last 1-2 years)

### For Document Mode (document provided):
1. **Read Thoroughly**: Read the entire document carefully
2. **Extract Framework**: Identify the methodology, principles, process
3. **Capture Nuance**: Get the "why" not just the "what"
4. **Preserve Voice**: Maintain the original perspective/philosophy

## Output Structure

Create a comprehensive knowledge artifact with this structure:

```markdown
# [Topic Name]

> Learned: [Date]
> Mode: [Research | Document: source-name]
> Sources: [List of sources]

## TL;DR
[2-3 sentence executive summary]

## Core Concepts
[Key ideas, definitions, mental models]

## Best Practices
[What TO do - with reasoning]

## Anti-Patterns & Pitfalls
[What NOT to do - common mistakes]

## Process/Framework
[Step-by-step methodology if applicable]

## Code Examples
[If technical - real, working examples]

## Key Insights
[Non-obvious learnings, expert tips]

## When to Apply
[Context for when this knowledge is relevant]

## Sources & References
[Links, citations for deeper reading]
```

## Saving the Knowledge

1. Convert topic to kebab-case filename (e.g., "React Server Components" → "react-server-components.md")
2. Save to: `~/.claude/knowledge/[filename].md`
3. If project-specific, also mention they can move to `.claude/knowledge/` for project scope

## After Saving

1. Confirm what was learned and where it was saved
2. Give a brief summary of the key takeaways
3. Mention they can use `/recall [topic]` to retrieve this knowledge later

## Quality Standards

- **Depth over breadth**: Better to know one thing well than many things superficially
- **Actionable**: Knowledge should be usable, not just theoretical
- **Opinionated**: Capture best practices, not just options
- **Examples**: Always include concrete examples
- **Sources**: Always cite where information came from
