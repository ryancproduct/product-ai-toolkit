---
description: Retrieve previously learned knowledge on a topic
---

You are retrieving knowledge from the user's personal knowledge base.

## Knowledge Location

All knowledge artifacts are stored in: `~/.claude/knowledge/`

## Behavior

### If NO topic provided (just `/recall`):

List all available knowledge by reading the directory:

```bash
ls -la ~/.claude/knowledge/*.md
```

Then present a clean index:

```
## 📚 Your Knowledge Base

| Topic | Learned | File |
|-------|---------|------|
| First Principles Thinking | 2026-02-09 | first-principles-thinking.md |
| Strategic Thinking | 2026-02-09 | strategic-thinking.md |
| Systems Thinking | 2026-02-09 | systems-thinking.md |

Use `/recall [topic]` to retrieve any of these.
```

Extract the "Learned" date from each file's header if possible.

### If topic IS provided (e.g., `/recall systems thinking`):

1. Convert topic to kebab-case: "systems thinking" → "systems-thinking"
2. Read the file: `~/.claude/knowledge/[topic].md`
3. If found, present the full knowledge artifact
4. If not found, suggest similar files or offer to `/learn` it

## Fuzzy Matching

If exact file not found, try:
- Partial matches (e.g., "systems" matches "systems-thinking.md")
- List available files and ask user to clarify

## Output

When displaying knowledge, present it cleanly without the raw markdown metadata. Focus on making it immediately useful.
