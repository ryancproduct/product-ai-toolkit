---
name: jtbd
description: "Extract Jobs-to-be-Done from feature requests or feedback $ARGUMENTS"
---

# JTBD Extractor

Extract Jobs-to-be-Done from feature requests, customer feedback, and user interviews. Transform solution-focused requests into problem-focused job statements.

## Invocation

```
/jtbd "Feature request or customer feedback"
```

Or natural language:
- "Extract the jobs from this feature request..."
- "What's the underlying JTBD for..."
- "Turn this feedback into jobs..."

---

## The Problem

Feature requests pile up, but they're solutions — not problems. Without extracting the underlying jobs, you build what users ask for, not what they need.

## What You Get

- JTBD statements (When/Want/So that)
- Functional, emotional, and social jobs
- Opportunity scoring (importance × satisfaction gap)
- Feature request translation
- Innovation opportunity identification

---

## JTBD Framework

### Core Job Statement Format

```
When [situation/trigger],
I want to [motivation/goal],
So I can [expected outcome].
```

**Example:**
```
When I'm conducting a safety inspection on a busy construction site,
I want to quickly capture photos with automatic context,
So I can complete thorough documentation without slowing down work.
```

### Job Types

| Type | Description | Example |
|------|-------------|---------|
| **Functional** | The practical task to accomplish | "Document safety hazards quickly" |
| **Emotional** | How the user wants to feel | "Feel confident I haven't missed anything" |
| **Social** | How the user wants to be perceived | "Be seen as thorough and professional by my manager" |

---

## Extraction Workflow

### Step 1: Gather Input

Accept one or more of:
- Feature request (e.g., "We need a dark mode")
- Customer feedback (e.g., "The app is too slow when I'm in the field")
- Interview transcript excerpt
- Support ticket
- Survey response

### Step 2: Identify the Context

Ask clarifying questions if needed:
1. **Who** is the user? (Role, experience level)
2. **Where** does this happen? (Physical/digital context)
3. **When** does this arise? (Trigger, frequency)
4. **Why** do they care? (Stakes, consequences)

### Step 3: Extract Functional Jobs

For each input, identify the core functional jobs:

```markdown
## Functional Jobs

### Job 1: [Core task]
**When:** [Situation/trigger]
**I want to:** [Motivation]
**So I can:** [Outcome]

**Current solution:** [How they solve it today]
**Pain points:** [What's broken about current solution]
```

### Step 4: Uncover Emotional Jobs

Dig beneath the surface:

```markdown
## Emotional Jobs

### Job 1: [Feeling they want]
**Statement:** When [situation], I want to feel [emotion], so I can [emotional outcome].

**Fear to avoid:** [What negative feeling are they escaping?]
**Confidence to gain:** [What positive feeling are they seeking?]
```

### Step 5: Identify Social Jobs

Consider perception and relationships:

```markdown
## Social Jobs

### Job 1: [How they want to be seen]
**Statement:** When [situation], I want to be seen as [perception], so I can [social outcome].

**Stakeholders:** [Who is watching/judging?]
**Reputation at stake:** [What's the social risk?]
```

### Step 6: Score Opportunities

Use the Opportunity Algorithm (Anthony Ulwick):

| Job | Importance (1-10) | Satisfaction (1-10) | Opportunity Score |
|-----|-------------------|---------------------|-------------------|
| Job 1 | X | Y | = Importance + (Importance - Satisfaction) |

**Scoring Guide:**
- **Importance:** How critical is completing this job? (10 = must do, 1 = nice to have)
- **Satisfaction:** How well do current solutions serve this job? (10 = perfectly, 1 = terribly)
- **Opportunity Score:** Higher = bigger opportunity (max = 20, threshold for action = 10+)

**Formula:** `Opportunity = Importance + MAX(Importance - Satisfaction, 0)`

### Step 7: Translate Feature Requests

Map the original request back to jobs:

```markdown
## Feature Request Translation

**Original Request:** "[Customer's exact words]"

**Underlying Jobs:**
1. Functional: [Job statement]
2. Emotional: [Job statement]
3. Social: [Job statement]

**Why they asked for this solution:** [Inference]

**Alternative solutions that address the same jobs:**
1. [Alternative 1]
2. [Alternative 2]
3. [Alternative 3]
```

---

## Output Template

```markdown
# JTBD Analysis: [Input Summary]

## Context
- **Source:** [Feature request / Feedback / Interview / Support ticket]
- **User segment:** [Role/persona]
- **Environment:** [Where this happens]

---

## Functional Jobs

### Job 1: [Primary functional job]
**When:** [Trigger situation]
**I want to:** [Goal/motivation]
**So I can:** [Desired outcome]

| Metric | Score |
|--------|-------|
| Importance | X/10 |
| Current Satisfaction | Y/10 |
| **Opportunity Score** | **Z** |

**Current workaround:** [How they handle it today]
**Pain with workaround:** [What's broken]

---

## Emotional Jobs

### [Feeling they seek]
**When:** [Situation]
**I want to feel:** [Emotion]
**So I can:** [Emotional outcome]

**Fear to avoid:** [Negative emotion]

---

## Social Jobs

### [How they want to be perceived]
**When:** [Situation]
**I want to be seen as:** [Perception]
**So I can:** [Social outcome]

**Key stakeholders:** [Who's watching]

---

## Opportunity Ranking

| Rank | Job | Type | Opportunity Score |
|------|-----|------|-------------------|
| 1 | [Job] | Functional | XX |
| 2 | [Job] | Emotional | XX |
| 3 | [Job] | Functional | XX |

---

## Feature Request Translation

**Original:** "[Exact customer words]"

**Real jobs to solve:**
1. [Job 1]
2. [Job 2]

**Alternative solutions:**
1. [Solution A] - addresses jobs 1, 2
2. [Solution B] - addresses job 1 only
3. [Solution C] - addresses all jobs differently

---

## Innovation Opportunities

**Underserved jobs (Opportunity Score > 12):**
- [Job]: [Why it's underserved and what opportunity exists]

**Overserved jobs (Opportunity Score < 6):**
- [Job]: [Already well-solved, deprioritize]

**Adjacent jobs to explore:**
- [Related job that emerged from analysis]
```

---

## Common Patterns

### Feature Request → Job Translation Examples

| Feature Request | Underlying Job |
|-----------------|----------------|
| "Add dark mode" | When working in low-light environments, I want reduced eye strain, so I can work longer without fatigue |
| "Make it faster" | When I'm under time pressure, I want to complete tasks without waiting, so I can meet my deadlines |
| "Add offline mode" | When I'm in areas with poor connectivity, I want to continue working, so I can be productive anywhere |
| "Better reporting" | When presenting to stakeholders, I want data that tells a clear story, so I can demonstrate my team's impact |

### Red Flags in Feature Requests

| Red Flag | What to Ask |
|----------|-------------|
| "Just add..." | What problem will this solve for you? |
| "Competitor has..." | When would you use this feature? |
| "Obviously need..." | Walk me through when you'd need this |
| "Quick win..." | What's the cost of not having this? |

---

## Tips for Quality JTBD Extraction

1. **Never accept the first answer** - The feature request is the symptom, not the disease
2. **Ask "why" 5 times** - Each layer reveals more about the true job
3. **Context is king** - The "when" is as important as the "what"
4. **Emotions matter** - Functional jobs without emotional context miss half the picture
5. **Validate with users** - Your extracted jobs are hypotheses until confirmed
6. **Look for contradictions** - When jobs conflict, you've found a design challenge

---

## Integration Points

**Feeds into:**
- `/opportunity-tree` - Jobs become the outcomes to explore
- `/user-stories` - Jobs inform story context and acceptance criteria
- `/prd` - Jobs shape the Problem Alignment section
