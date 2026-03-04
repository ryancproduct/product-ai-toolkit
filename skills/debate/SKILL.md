---
name: debate
description: Stress-test a product idea with parallel Champion vs Sceptic agents. Produces risk register, MVP scope, assumption map, and go/no-go recommendation.
---

# Product Debate Skill

Stress-test any product idea — from a one-liner to a full PRD — by running parallel Champion and Sceptic agents that argue FOR and AGAINST it. Synthesises into actionable output.

## Input: $ARGUMENTS

Accepts flexible input:
- `/debate [idea description]` — Freeform idea
- `/debate [path/to/prd.md]` — Full PRD or spec file
- `/debate` — Will ask for the idea interactively

If a file path is detected (contains `/` or `.md`), read the file. Otherwise treat input as freeform text.

---

## Phase 1: Context Gathering

### Capture the Idea

If no input provided, ask: "What product idea, feature, or investment would you like to stress-test?"

If input is brief (< 100 words), ask ONE clarifying question:
> "What's the strategic context? Why is this being considered now?"

Do NOT ask more than one question. Work with what you have — the agents will surface what's missing.

### Enrich Context (Optional, Best-Effort)

Attempt to pull supporting context from available MCPs. Do not block on these — if they fail or return nothing, proceed without them.

**Amplitude** — Use `mcp__Amplitude__search` to find metrics related to the feature area. Pull current baseline numbers if available.

**Jira** — Use Jira MCP tools to search for related tickets, past attempts at similar features, or relevant epics.

**Confluence** — Use Confluence MCP tools to search for existing research, strategy docs, or prior analysis related to the idea.

### Assemble Context Package

Combine into a single context block:

```
## Idea
[The idea as stated by the user, or full PRD content]

## Strategic Context
[User's answer to "why now?" if provided]

## Data Context (from Amplitude)
[Current metrics for the affected area, or "No data available"]

## Organisational Context (from Jira/Confluence/Glean)
[Related tickets, past attempts, existing research, or "No context found"]
```

---

## Phase 2: Parallel Agent Dispatch

**CRITICAL**: Dispatch BOTH agents in a SINGLE message using two Task tool calls.

### Champion Agent

```
Task(
  description: "Champion argues FOR product idea",
  subagent_type: "general-purpose",
  prompt: """
You are the CHAMPION — your job is to build the strongest possible case FOR this product idea. You are a passionate, strategic product leader who sees the potential.

## The Idea
[INSERT FULL CONTEXT PACKAGE FROM PHASE 1]

## Your Mission

Produce exactly 10 arguments FOR this idea, ranked from strongest to weakest. For each argument:

### Argument [N]: [Title]
**Strength: [Strong / Moderate / Speculative]**

[2-3 sentences making the case. Be specific — reference data, market dynamics, customer behaviour, competitive positioning.]

**Evidence**: [What supports this? Data, research, analogies, market trends]
**If true, impact**: [What's the upside if this argument holds?]

## Argument Categories to Cover

You MUST include at least one argument in each category:
1. **Customer Need** — Evidence that users want or need this
2. **Market Opportunity** — Timing, competitive dynamics, market gaps
3. **Strategic Alignment** — How this advances the company's mission/strategy
4. **Revenue/Growth Potential** — Business case and financial upside
5. **Compounding Effects** — Second-order benefits, platform effects, future optionality

## Rules
- Steelman the idea — make it as strong as possible
- Fill gaps the proposer didn't think of
- Be specific, not generic. "This could increase revenue" is weak. "This targets the 40% of trial users who drop off at step 3, representing ~$X ARR" is strong.
- If data is available in the context, USE IT
- Do NOT acknowledge weaknesses — that's the Sceptic's job
"""
)
```

### Sceptic Agent

```
Task(
  description: "Sceptic argues AGAINST product idea",
  subagent_type: "general-purpose",
  prompt: """
You are the SCEPTIC — your job is to find every reason this product idea could fail, waste resources, or cause harm. You are a rigorous, experienced product leader who has seen many ideas fail.

## The Idea
[INSERT FULL CONTEXT PACKAGE FROM PHASE 1]

## Your Mission

Produce exactly 10 arguments AGAINST this idea, ranked from most damaging to least. For each argument:

### Argument [N]: [Title]
**Severity: [Critical / Significant / Minor]**

[2-3 sentences explaining the risk or flaw. Be specific — reference real constraints, past failures, known limitations.]

**Evidence**: [What supports this concern? Data, historical precedent, industry patterns]
**If ignored, consequence**: [What happens if this risk materialises?]

## Argument Categories to Cover

You MUST include at least one argument in each category:
1. **Hidden Costs** — Engineering complexity, maintenance burden, support load, technical debt
2. **Opportunity Cost** — What are we NOT building by doing this? What's more valuable?
3. **Customer Risk** — Segments harmed, confusion created, trust eroded
4. **Competitive Risk** — How competitors could respond, copy, or outflank
5. **Execution Risk** — Dependencies, timeline assumptions, team capacity, integration complexity
6. **Second-Order Effects** — Cannibalisation, precedent-setting, metric gaming, unintended consequences

## Rules
- Attack assumptions, not the person
- Be specific, not generic. "This is risky" is weak. "This requires the integrations team who are committed to Project X until Q3, creating a 4-month delay" is strong.
- If data is available in the context, use it AGAINST the idea
- Look for what's NOT said — missing customer evidence, unaddressed segments, ignored constraints
- Consider historical precedent — has something similar been tried before? What happened?
- Do NOT acknowledge strengths — that's the Champion's job
"""
)
```

---

## Phase 3: Synthesis

After both agents return (use TaskOutput to collect results), synthesise into three deliverables.

### 3.1 Risk Register

Review all Sceptic arguments and extract discrete risks. Merge overlapping risks. Assess each:

```markdown
## Risk Register

| # | Risk | Source | Severity | Likelihood | Risk Score | Mitigation |
|---|------|--------|----------|------------|------------|------------|
| 1 | [Specific risk] | Sceptic Arg #[N] | Critical/High/Med/Low | High/Med/Low | [S×L] | [Suggested mitigation or "Accept"] |
```

**Scoring:**
- Severity: Critical=4, High=3, Medium=2, Low=1
- Likelihood: High=3, Medium=2, Low=1
- Risk Score = Severity × Likelihood (max 12)
- Sort by Risk Score descending

### 3.2 Minimum Viable Scope

Cross-reference Champion and Sceptic arguments to find the defensible core:

```markdown
## Minimum Viable Scope

### Survives the Debate (Build This)
- [Feature/aspect] — Defended by Champion Arg #[N], not effectively challenged by Sceptic
- [Feature/aspect] — Defended by Champion Arg #[N], risk mitigatable per Sceptic Arg #[M]

### Cut or Defer (Sceptic Won)
- [Feature/aspect] — Sceptic Arg #[N] was more convincing because [reason]
- [Feature/aspect] — Risk too high relative to benefit

### Needs Validation First
- [Feature/aspect] — Both sides made strong arguments; decision depends on [unknown]
```

### 3.3 Assumption Map

Extract every assumption from both Champion AND Sceptic arguments:

```markdown
## Assumption Map

| # | Assumption | Source | Confidence | Evidence | Cheapest Test |
|---|-----------|--------|-----------|----------|--------------|
| 1 | [Assumption] | Champion Arg #[N] | High/Med/Low | [What we know] | [How to validate quickly] |
| 2 | [Assumption] | Sceptic Arg #[N] | High/Med/Low | [What we know] | [How to validate quickly] |
```

**Confidence levels:**
- **High**: Supported by data or direct customer evidence
- **Medium**: Supported by indirect evidence, analogies, or expert opinion
- **Low**: Speculation, gut feel, or no evidence

Sort by confidence ascending (lowest confidence = highest priority to validate).

---

## Phase 4: Go / No-Go Recommendation

Synthesise everything into a clear recommendation:

```markdown
## Recommendation

**Verdict: [Proceed / Proceed with Conditions / Pause & Validate / Kill]**
**Confidence: [High / Medium / Low]**

### Reasoning
[3-5 sentences explaining the verdict. Reference specific arguments from both sides.]

### Conditions (if "Proceed with Conditions")
1. [Condition that must be met]
2. [Condition that must be met]

### Key Assumptions to Validate First
1. [Highest-risk assumption] — Test via: [method]
2. [Second-highest-risk assumption] — Test via: [method]

### Recommended Next Steps
1. [Concrete action with owner suggestion]
2. [Concrete action with owner suggestion]
3. [Concrete action with owner suggestion]
```

---

## Output Assembly

Combine all phases into a single markdown document:

```markdown
# Product Debate: [Idea Title]

**Date**: [Today's date]
**Idea Source**: [User-provided / PRD / etc.]
**Verdict**: [Proceed / Proceed with Conditions / Pause & Validate / Kill]

---

## The Idea
[Original idea as stated]

## Champion's Case (Top 5 of 10)
[Summarise the 5 strongest Champion arguments — 1-2 sentences each]

## Sceptic's Case (Top 5 of 10)
[Summarise the 5 strongest Sceptic arguments — 1-2 sentences each]

## Risk Register
[Full table from 3.1]

## Minimum Viable Scope
[Full content from 3.2]

## Assumption Map
[Full table from 3.3]

## Recommendation
[Full content from Phase 4]

---

*Generated by /debate skill — Champion vs Sceptic parallel analysis*
```

Save to user-specified location if requested, or output to conversation.

---

## Error Handling

- If MCP enrichment fails (Amplitude, Jira, Confluence, Glean), proceed without it. Note "No [source] context available" in the context package.
- If one agent fails, note which perspective is missing and proceed with single-sided analysis + caveat.
- If both agents fail, fall back to doing the analysis yourself in the main thread (sequential, not parallel).

## Tips

- The skill works best when the idea has SOME specificity. "Make the app better" will produce generic arguments. "Add real-time collaboration to inspections" will produce sharp ones.
- For contentious ideas, share the full output with stakeholders as a pre-read before a decision meeting.
- The assumption map is often the most valuable output — it tells you what to learn next.
- Run `/debate` before writing a full PRD to identify what the PRD needs to address.
