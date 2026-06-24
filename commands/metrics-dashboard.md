---
description: Generate a product metrics summary using Amplitude data, with narrative framing and health indicators
---

You are helping a product manager analyse and summarise product metrics.

## Task

Pull metrics from Amplitude (or available data sources) and produce a metrics brief with health indicators and narrative framing. For a richer "so what" narrative, delegate to the `data-storyteller` agent.

## Process

1. **Identify the scope**: Which product area, feature, or time period? If not specified, ask.
2. **Pull data from Amplitude** using MCP tools:
   - Core engagement: DAU/WAU/MAU for the relevant area
   - Feature-specific events: adoption rate, completion rate, frequency
   - Trend: this period vs prior period
   - Segments if meaningful (plan tier, industry, user role)
3. **Assess health**: For each metric, classify as 🟢 On Track / 🟡 Watch / 🔴 Critical against known targets or prior period trend.
4. **Write the brief**.

If Amplitude isn't connected, ask the user to paste their metrics data — you'll work with whatever format they provide.

## Output Format

```markdown
## Product Metrics — [Area] | [Period]

### Summary
[2-3 sentences: what's the overall picture right now?]

### Key Metrics

| Metric | This Period | Prior Period | Change | Status |
|--------|-------------|--------------|--------|--------|
| MAU | | | | 🟢/🟡/🔴 |
| WAU | | | | 🟢/🟡/🔴 |
| [Feature adoption] | | | | 🟢/🟡/🔴 |
| [Retention] | | | | 🟢/🟡/🔴 |

### What's Moving

**Up ↑**
- [Metric] is [+X%] — [brief explanation or hypothesis]

**Down ↓**
- [Metric] is [-X%] — [brief explanation or hypothesis]

**Watch**
- [Metric] is flat but [context that makes this concerning or reassuring]

### Recommended Actions
1. [Action based on the data]
2. [Action based on the data]
```

## Tips

- Always compare to prior period AND to target/expected. A metric growing 5% sounds good until you know the target was 15%.
- If a metric moved significantly (>10% either direction), try to correlate it with a product change or external event.
- For a full narrative story with "so what" framing and exec-ready output, run `/data-storyteller` instead of or after this summary.
