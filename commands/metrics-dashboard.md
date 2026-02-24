---
description: Generate metrics dashboard summary
---

You are helping a product manager analyze and present product metrics.

## Task

Create a metrics dashboard summary from available data sources or help set up metric tracking.

## Process

1. **Identify Data Sources**: Look for analytics files, logs, database exports, or CSV files
2. **Key Metrics**: Organize by category (Acquisition, Activation, Retention, Revenue, Referral)
3. **Trends**: Calculate week-over-week or month-over-month changes
4. **Insights**: Highlight what's working and what needs attention

## Metrics Framework (AARRR Pirate Metrics)

### Acquisition
- New users/signups
- Traffic sources
- Landing page conversion rate

### Activation
- Onboarding completion rate
- Time to first value
- Feature adoption rate

### Retention
- Daily/Weekly/Monthly Active Users (DAU/WAU/MAU)
- Churn rate
- Cohort retention

### Revenue
- MRR/ARR
- ARPU (Average Revenue Per User)
- LTV (Lifetime Value)

### Referral
- Referral rate
- Viral coefficient
- NPS (Net Promoter Score)

## Output Format

```markdown
## Product Metrics Dashboard - [Period]

### Executive Summary
[2-3 sentences on overall health and key movements]

### Key Performance Indicators

| Metric | Current | Previous | Change | Target | Status |
|--------|---------|----------|--------|--------|--------|
| MAU | [value] | [value] | [+/-%] | [goal] | 🟢/🟡/🔴 |
| Activation Rate | [%] | [%] | [+/-%] | [%] | 🟢/🟡/🔴 |
| Retention (D7) | [%] | [%] | [+/-%] | [%] | 🟢/🟡/🔴 |
| MRR | [$] | [$] | [+/-%] | [$] | 🟢/🟡/🔴 |

### Top Wins
1. **[Metric]**: [What happened and why it matters]
2. **[Metric]**: [What happened and why it matters]

### Areas of Concern
1. **[Metric]**: [What's declining and potential causes]
2. **[Metric]**: [What's declining and potential causes]

### Deep Dive: [Focus Area]
[Detailed analysis of one particular metric or trend]

### Recommended Actions
1. **[Action]**: Based on [metric/insight]
2. **[Action]**: Based on [metric/insight]

### Experiment Results
| Experiment | Hypothesis | Result | Next Steps |
|------------|------------|--------|------------|
| [Name] | [What we thought] | [What happened] | [What to do] |
```

## Analysis Tips

- Use 🟢 (on track), 🟡 (needs attention), 🔴 (critical) status indicators
- Always compare to previous period AND target
- Look for correlations between metrics
- Segment data when possible (by cohort, channel, plan type)
- Note statistical significance
- Link metrics to recent product changes

## If No Data Available

If you can't find data files, help the PM by:
1. Recommending what metrics to track
2. Suggesting data collection methods
3. Creating a metrics tracking template
4. Outlining an analytics implementation plan

## Visualization Suggestions

Recommend chart types for different metrics:
- **Trends**: Line charts
- **Comparisons**: Bar charts
- **Composition**: Pie charts or stacked bars
- **Distribution**: Histograms
- **Correlation**: Scatter plots
- **Funnels**: Funnel charts
