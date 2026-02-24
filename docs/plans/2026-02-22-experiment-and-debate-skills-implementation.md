# Experiment & Debate Skills Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create two new Claude Code skills — `/experiment` (guided experiment design wizard) and `/debate` (parallel agent product debate) — matching existing PM AI kit conventions.

**Architecture:** Skill 1 is a single command `.md` file following the pattern of `competitive-analysis.md` and `jtbd.md`. Skill 2 is a complex skill folder with `SKILL.md` following the pattern of `interview-analysis/`.

**Tech Stack:** Claude Code skills (markdown), Task tool for parallel agents, Amplitude MCP, Jira MCP, Confluence MCP, Glean MCP

---

## Task 1: Create the `/experiment` command skill

**Files:**
- Create: `/Users/ryanclement/.claude/commands/experiment.md`

**Step 1: Write the experiment command file**

Create `/Users/ryanclement/.claude/commands/experiment.md` with the full skill content below:

```markdown
---
description: Design, plan and analyse product experiments with Amplitude integration $ARGUMENTS
---

You are an experiment design and analysis expert helping a product manager run rigorous A/B tests and experiments.

## Task

Guide the PM through designing, planning, or analysing a product experiment. Adapts to where the user is in the experiment lifecycle.

Accepts arguments:
- `/experiment` — Start a new experiment from scratch (full wizard)
- `/experiment [feature/idea]` — Start with a feature name pre-filled
- `/experiment analyse [experiment name]` — Skip to Phase 5 (result interpretation)

## Mode Detection

If no arguments or a feature name is provided, run the full wizard (Phases 1-4).
If "analyse" is in the arguments, skip to Phase 5 (Result Interpretation).

---

## Phase 1: Hypothesis Framing

**Do not proceed until the hypothesis is well-formed.**

Guide the user to articulate their hypothesis in this exact format:

> **If we** [intervention — what we're changing]
> **then** [metric — what we expect to move]
> **will** [direction — increase/decrease]
> **by** [magnitude — minimum meaningful change]
> **because** [mechanism — why we believe this will work]

Ask clarifying questions one at a time until each element is crisp:

1. **What are we changing?** Classify: UI change, flow change, pricing, copy, algorithm, default setting, feature addition/removal
2. **Who is affected?** All users, specific plan tier, specific segment, new users only, specific geography
3. **What's the blast radius if we're wrong?** Reversible (flag flip) vs irreversible (data migration). Low risk (cosmetic) vs high risk (revenue-impacting)

### Hypothesis Quality Check

Before proceeding, validate:
- [ ] Intervention is specific and implementable
- [ ] Metric is measurable and already tracked (or can be)
- [ ] Magnitude is realistic (not "10x improvement")
- [ ] Mechanism explains the causal chain
- [ ] The hypothesis is falsifiable

If any element is vague, push back with a specific suggestion.

---

## Phase 2: Metric Selection

Use the Amplitude MCP tools to ground metric selection in real data.

### Primary Metric

The ONE metric this experiment must move. Ask:
- "What behaviour change would prove your hypothesis right?"
- Use `mcp__Amplitude__search` to find matching events in the Amplitude taxonomy
- Use `mcp__Amplitude__get_event_properties` to confirm the event exists and has the right properties
- If the event doesn't exist, flag it: "This event isn't tracked yet. You'll need to instrument it before running the experiment."

### Secondary Metrics

Supporting signals that add context. Suggest 1-2 based on the primary:
- If primary is conversion → secondary: time-to-convert, drop-off step
- If primary is engagement → secondary: session frequency, feature depth
- If primary is retention → secondary: activation rate, feature adoption

### Guardrail Metrics

Things that MUST NOT degrade. Suggest defaults based on feature area:
- **Always**: App crash rate, page load time, support ticket creation rate
- **Revenue features**: MRR, churn rate, upgrade rate
- **Onboarding features**: Activation rate, time-to-value, first-session completion
- **Core workflow features**: Task completion rate, error rate, time-on-task

Present the full metric plan as a table:

| Type | Metric | Current Baseline | Event Name | Target |
|------|--------|-----------------|------------|--------|
| Primary | [metric] | [value or "TBD"] | [Amplitude event] | [direction + magnitude] |
| Secondary | [metric] | [value or "TBD"] | [Amplitude event] | [expected direction] |
| Guardrail | [metric] | [value or "TBD"] | [Amplitude event] | Must not degrade > [threshold] |

---

## Phase 3: Sample Size & Duration

Calculate the minimum sample size and experiment duration.

### Inputs Needed

Ask for (or pull from Amplitude if available):
1. **Baseline conversion/metric rate** — current value of the primary metric
2. **Minimum detectable effect (MDE)** — "What's the smallest improvement worth shipping?" Frame it as: "If this experiment improved [metric] by only X%, would you still ship it?"
3. **Daily eligible traffic** — How many users/day will be in the experiment? Use Amplitude to estimate if possible.
4. **Number of variants** — Usually 2 (control + treatment), but ask.

### Calculation

Use these formulas (80% power, 95% confidence, two-tailed):

For **proportions** (conversion rates):
```
n per variant = (Z_α/2 + Z_β)² × [p₁(1-p₁) + p₂(1-p₂)] / (p₂ - p₁)²

Where:
- Z_α/2 = 1.96 (95% confidence)
- Z_β = 0.84 (80% power)
- p₁ = baseline rate
- p₂ = baseline rate × (1 + MDE)
```

For **continuous metrics** (means):
```
n per variant = (Z_α/2 + Z_β)² × 2σ² / δ²

Where:
- σ = standard deviation (estimate as baseline × 0.5 if unknown)
- δ = minimum detectable difference in absolute terms
```

Then:
```
Duration (days) = (n per variant × number of variants) / daily eligible traffic
```

### Duration Sanity Checks

- **< 7 days**: Warn about day-of-week effects. Recommend minimum 2 weeks.
- **7-42 days**: Good range. Proceed.
- **> 42 days (6 weeks)**: Flag as potentially too long. Suggest:
  - Increase MDE (accept a larger minimum effect)
  - Narrow the audience to higher-traffic segment
  - Choose a more sensitive metric (higher baseline rate)
  - Consider a different experimental approach (e.g., pre/post with holdout)

### Output

```
📊 Experiment Sizing

Baseline rate:     [X%]
Minimum effect:    [Y% relative lift]
Sample per variant: [N users]
Variants:          [2]
Total sample:      [2N users]
Daily traffic:     [T users/day]

⏱️  Estimated duration: [D days] ([start] → [end])

⚠️  [Any warnings about duration, traffic, or seasonality]
```

---

## Phase 4: Launch Checklist

Generate a pre-launch checklist tailored to the experiment:

```markdown
## Pre-Launch Checklist: [Experiment Name]

### Instrumentation
- [ ] Primary metric event firing correctly: `[event name]`
- [ ] Secondary metric events firing: `[event names]`
- [ ] Guardrail metric events verified: `[event names]`
- [ ] Experiment exposure event logging variant assignment

### Feature Flag
- [ ] Feature flag created: `[flag name]`
- [ ] Targeting configured: [description of who's included/excluded]
- [ ] Rollout: [X]% control / [Y]% treatment
- [ ] QA verified both variants render correctly

### Safeguards
- [ ] Guardrail metric alerts configured in Amplitude
- [ ] Rollback plan documented: [how to kill the experiment quickly]
- [ ] On-call knows experiment is running

### Documentation
- [ ] Experiment registered in Confluence: [link]
- [ ] Hypothesis documented with predicted outcome
- [ ] Expected end date: [date from Phase 3]
- [ ] Decision criteria defined: "We will ship if [primary metric] improves by ≥[MDE] with p<0.05 AND no guardrail degradation > [threshold]"

### Review
- [ ] Eng reviewed implementation
- [ ] Data team verified event schema
- [ ] PM approved targeting and rollout plan
```

---

## Phase 5: Result Interpretation

### Data Collection

Ask the user how they want to provide results:

**Option A: Manual input**
Ask for:
- Control group: sample size, metric value
- Treatment group: sample size, metric value
- Duration the experiment ran
- Any guardrail metric changes

**Option B: Amplitude query**
Use `mcp__Amplitude__query_charts` or `mcp__Amplitude__query_dataset` to pull:
- Primary metric by variant over the experiment period
- Guardrail metrics by variant
- Segment breakdowns if relevant

### Analysis

Provide:

**1. Statistical Significance**
- Calculate z-score and p-value
- State whether result is significant at p<0.05
- Calculate 95% confidence interval for the effect size
- Flag if sample size was insufficient (underpowered)

**2. Practical Significance**
- Is the observed effect ≥ the MDE from Phase 3?
- What's the estimated annual impact? (effect × annual traffic × revenue/conversion value)
- Is this worth the ongoing maintenance/complexity cost?

**3. Guardrail Check**
- Did any guardrail metric degrade?
- If yes, by how much? Is it within acceptable bounds?

**4. Segment Analysis** (if data available)
- Did the effect vary by plan tier, geography, or user segment?
- Any segments where the treatment was harmful?

**5. Recommendation**

| Outcome | Recommendation |
|---------|---------------|
| Significant + practical + guardrails OK | **Ship it** — Roll out to 100% |
| Significant + practical + guardrail concern | **Investigate** — Understand the guardrail impact before shipping |
| Significant but below MDE | **Iterate** — Effect exists but too small. Consider amplifying the intervention. |
| Not significant, adequate sample | **Kill it** — The hypothesis was wrong. Capture learnings. |
| Not significant, underpowered | **Extend or re-run** — Insufficient data to conclude. |

Present as:

```markdown
## Experiment Results: [Name]

**Recommendation: [Ship / Iterate / Kill / Investigate / Extend]**
**Confidence: [High / Medium / Low]**

### Key Numbers
| Metric | Control | Treatment | Lift | p-value | Significant? |
|--------|---------|-----------|------|---------|-------------|
| [Primary] | [value] | [value] | [%] | [p] | [Yes/No] |

### Guardrail Metrics
| Metric | Control | Treatment | Change | Status |
|--------|---------|-----------|--------|--------|
| [Guardrail] | [value] | [value] | [%] | ✅ OK / ⚠️ Degraded |

### Reasoning
[2-3 sentences explaining the recommendation]

### Assumptions & Caveats
- [Any data quality issues]
- [Novelty effects or seasonality concerns]
- [Segments not covered]

### Next Steps
1. [Concrete action]
2. [Concrete action]
```

---

## Tips

- Always validate events exist in Amplitude before committing to metrics
- Push back on vanity metrics — page views and clicks rarely matter
- If the user can't articulate the mechanism (the "because"), the hypothesis isn't ready
- Encourage running experiments for full weeks (avoid mid-week starts/stops)
- Remind users that a negative result is still a result — it prevents building the wrong thing
```

**Step 2: Verify the file was created correctly**

Run: `wc -l /Users/ryanclement/.claude/commands/experiment.md`
Expected: ~250-280 lines

**Step 3: Test the skill is discoverable**

Run: `ls -la /Users/ryanclement/.claude/commands/experiment.md`
Expected: File exists with recent timestamp

---

## Task 2: Create the `/debate` skill folder structure

**Files:**
- Create: `/Users/ryanclement/.claude/skills/debate/SKILL.md`

**Step 1: Create the debate skill directory**

Run: `mkdir -p /Users/ryanclement/.claude/skills/debate`

**Step 2: Write the debate SKILL.md file**

Create `/Users/ryanclement/.claude/skills/debate/SKILL.md` with the full skill content below:

```markdown
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

**Glean** — Use `mcp__glean_default__search` as a catch-all to find any organisational context about the idea.

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
```

**Step 3: Verify the skill folder structure**

Run: `ls -la /Users/ryanclement/.claude/skills/debate/`
Expected: `SKILL.md` file exists

**Step 4: Verify the skill file**

Run: `wc -l /Users/ryanclement/.claude/skills/debate/SKILL.md`
Expected: ~220-260 lines

---

## Task 3: Verify both skills are discoverable

**Step 1: List all commands to confirm experiment appears**

Run: `ls /Users/ryanclement/.claude/commands/`
Expected: `experiment.md` in the list alongside existing commands

**Step 2: List all skills to confirm debate appears**

Run: `ls /Users/ryanclement/.claude/skills/`
Expected: `debate/` directory in the list alongside existing skill folders

**Step 3: Verify frontmatter format**

Run: `head -5 /Users/ryanclement/.claude/commands/experiment.md`
Expected: YAML frontmatter with `description:` field

Run: `head -5 /Users/ryanclement/.claude/skills/debate/SKILL.md`
Expected: YAML frontmatter with `name:` and `description:` fields

---
