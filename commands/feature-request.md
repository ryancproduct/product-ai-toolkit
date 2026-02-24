---
description: Process and triage feature request
---

You are helping a product manager intake and triage a new feature request.

## Task

Help capture, evaluate, and prioritize a feature request from customers, sales, or internal teams.

## Process

1. **Capture Details**: Get the complete feature request
2. **Understand Context**: Who's asking and why?
3. **Evaluate Impact**: How many users? What value?
4. **Assess Effort**: Initial complexity estimate
5. **Recommend Priority**: Using RICE or similar framework

## Information to Gather

If not provided, ask:
- Who is requesting this? (customer name, sales team, etc.)
- What problem are they trying to solve?
- What's their current workaround?
- How many users/customers would benefit?
- Is this blocking a deal or renewal?
- Any deadline or urgency?

## Output Format

```markdown
## Feature Request: [Feature Name]

**Request ID**: FR-[Number]
**Date**: [Date]
**Requested By**: [Name/Team]
**Status**: New

### Request Summary
[2-3 sentence description of what they want]

### Problem Statement
[What problem does this solve? Why do they need it?]

### User Story
As a [user type],
I want to [action],
So that [benefit].

### Current Workaround
[How are they solving this today, if at all?]

### Impact Analysis

**Users Affected**: [Number/Percentage]
**Segments**: [Which customer segments care about this?]
**Business Impact**:
- Revenue: [Potential ARR impact or deals enabled]
- Retention: [Impact on churn or expansion]
- Acquisition: [Impact on new customer signups]

**Urgency**: Critical / High / Medium / Low
- [Reasoning for urgency level]

### Initial Effort Estimate
**Complexity**: [1-5 scale or T-shirt size S/M/L/XL]
**Estimated Engineering Time**: [X weeks/months]
**Dependencies**: [Any technical or team dependencies]

### RICE Score

| Factor | Score | Notes |
|--------|-------|-------|
| Reach | [#] | [Users per quarter] |
| Impact | [0.25-3] | [Massive/High/Medium/Low] |
| Confidence | [%] | [High/Medium/Low confidence] |
| Effort | [#] | [Person-months] |
| **RICE** | **[Score]** | (Reach × Impact × Confidence) / Effort |

### Strategic Alignment
- [ ] Aligns with product vision
- [ ] Supports current OKRs
- [ ] Competitive differentiator
- [ ] Table stakes / parity feature
- [ ] Technical debt payoff

### Similar Requests
- [Link to similar request #1]
- [Link to similar request #2]

### Alternatives Considered
1. **[Alternative approach]**: [Pros/cons]
2. **[Alternative approach]**: [Pros/cons]

### Recommendation
**Priority**: P0 / P1 / P2 / P3 / Backlog / Decline

**Reasoning**: [Why this priority level?]

**Next Steps**:
1. [Action item]
2. [Action item]

### Open Questions
- [ ] [Question that needs answering]
- [ ] [Question that needs answering]

### Related Links
- Customer conversation: [Link]
- Sales ticket: [Link]
- Analytics: [Link]
```

## Triage Criteria

**P0 (Critical)**:
- Blocking major customer/revenue
- Security or compliance issue
- Broken core functionality

**P1 (High)**:
- High RICE score (>50)
- Strategic initiative
- Affects large segment

**P2 (Medium)**:
- Good RICE score (20-50)
- Nice to have
- Affects niche segment

**P3 (Low)**:
- Low RICE score (<20)
- Edge case
- Can be solved with workaround

**Decline**:
- Doesn't align with strategy
- Too complex for value
- Better solved differently

## Follow-up Actions

After triaging, suggest:
- Adding to appropriate backlog
- Scheduling for roadmap planning
- Following up with requester
- Tagging for tracking
