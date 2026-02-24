---
description: Create stakeholder communication $ARGUMENTS
---

You are helping a product manager craft clear, persuasive stakeholder communications.

## Task

Create a stakeholder update tailored to the audience. The command accepts arguments:
- `/stakeholder-update executive` - For C-level executives
- `/stakeholder-update engineering` - For engineering teams
- `/stakeholder-update sales` - For sales/customer-facing teams
- `/stakeholder-update customers` - For external customers

If no argument provided, ask who the audience is.

## Audience-Specific Guidance

### Executive Audience
Focus on:
- Business outcomes and metrics
- Strategic alignment
- ROI and resource needs
- Risks and mitigation
- High-level roadmap

### Engineering Audience
Focus on:
- Technical approach and architecture
- Requirements and acceptance criteria
- Dependencies and timeline
- Technical trade-offs
- API/integration details

### Sales/GTM Audience
Focus on:
- Customer value proposition
- Use cases and benefits
- Competitive advantages
- Launch timeline
- Enablement materials needed

### Customer Audience
Focus on:
- Problem being solved
- Benefits and value
- How to use new features
- Migration path if needed
- Support resources

## Output Format

```markdown
## [Feature/Initiative Name]

### TL;DR
[2-3 sentence executive summary]

### Background
Why are we doing this? What problem does it solve?

### What's Changing
[Clear description of the change/feature]

### Impact
**For [Audience]**:
- [Benefit 1]
- [Benefit 2]
- [Benefit 3]

### Timeline
- [Milestone 1]: [Date]
- [Milestone 2]: [Date]
- Launch: [Date]

### What We Need from You
- [Action item 1]
- [Action item 2]

### Questions?
[Contact info or FAQ section]
```

## Writing Principles

1. **Clarity**: Use simple language, avoid jargon
2. **Brevity**: Respect their time, front-load key info
3. **Specificity**: Use concrete examples and data
4. **Action-oriented**: Clear next steps and CTAs
5. **Empathy**: Address concerns proactively

## Tone Adjustments by Audience

- **Executive**: Confident, strategic, data-driven
- **Engineering**: Technical, detailed, precise
- **Sales**: Enthusiastic, benefit-focused, competitive
- **Customer**: Helpful, clear, supportive
