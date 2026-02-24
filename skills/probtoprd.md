---
name: probtoprd
description: "Full discovery workflow from problem to PRD $ARGUMENTS"
---

# Problem to PRD Workflow

A complete discovery-to-documentation workflow that transforms vague feature requests into comprehensive, sprint-ready PRDs. Chains JTBD extraction → Opportunity mapping → Story generation → PRD creation.

## Invocation

```
/probtoprd "Feature request or customer problem"
```

Or natural language:
- "Take this through the full discovery process..."
- "Turn this feature request into a PRD..."
- "Full problem to PRD workflow for..."

---

## The Problem

Feature requests arrive as solutions, not problems. Teams skip discovery and jump straight to PRDs, leading to:
- Building what customers asked for, not what they need
- Solutions without validated opportunities
- PRDs that lack problem clarity
- Stories that don't connect to outcomes

## What You Get

A complete, connected artifact set:
1. **JTBD Analysis** - Underlying jobs driving the request
2. **Opportunity Tree** - Mapped opportunities with multiple solutions
3. **User Stories** - Sprint-ready stories with acceptance criteria
4. **PRD** - Full PRD connected to discovery work

---

## The Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                    PROBLEM TO PRD WORKFLOW                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  INPUT: Feature request, customer feedback, or vague problem    │
│           │                                                      │
│           ▼                                                      │
│  ┌─────────────────┐                                            │
│  │  1. /jtbd       │  Extract underlying jobs                   │
│  │                 │  • Functional, emotional, social jobs      │
│  │                 │  • Opportunity scoring                     │
│  └────────┬────────┘                                            │
│           │ Jobs become opportunities                            │
│           ▼                                                      │
│  ┌─────────────────┐                                            │
│  │  2. /opportunity│  Map outcome → opportunities → solutions   │
│  │     -tree       │  • Multiple solutions per opportunity      │
│  │                 │  • Assumptions identified                  │
│  │                 │  • Experiments prioritized                 │
│  └────────┬────────┘                                            │
│           │ Solutions become epics                               │
│           ▼                                                      │
│  ┌─────────────────┐                                            │
│  │  3. /user-      │  Break down into sprint-ready work         │
│  │     stories     │  • INVEST-validated stories                │
│  │                 │  • BDD acceptance criteria                 │
│  │                 │  • Dependencies mapped                     │
│  └────────┬────────┘                                            │
│           │ Stories inform solution section                      │
│           ▼                                                      │
│  ┌─────────────────┐                                            │
│  │  4. /prd        │  Generate comprehensive PRD                │
│  │                 │  • Problem Alignment from JTBD             │
│  │                 │  • Solution Alignment from tree + stories  │
│  │                 │  • Launch Readiness checklist              │
│  └────────┬────────┘                                            │
│           │                                                      │
│           ▼                                                      │
│  OUTPUT: Complete PRD + linked discovery artifacts               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Step-by-Step Execution

### Phase 1: JTBD Extraction (5-10 min)

**Goal:** Transform the feature request into underlying jobs.

**Input:** Raw feature request, customer feedback, or interview notes

**Process:**
1. Run `/jtbd` with the input
2. Extract functional, emotional, and social jobs
3. Score opportunities (importance × satisfaction gap)
4. Identify top 2-3 jobs to focus on

**Checkpoint Questions:**
- [ ] Have we identified jobs beyond the surface request?
- [ ] Do we understand the emotional drivers?
- [ ] Are there high-opportunity-score jobs to focus on?

**Output:** JTBD Analysis document with prioritized jobs

---

### Phase 2: Opportunity Mapping (10-15 min)

**Goal:** Map jobs to opportunities and generate multiple solutions.

**Input:** JTBD Analysis from Phase 1

**Process:**
1. Define measurable outcome (what metric will move?)
2. Run `/opportunity-tree` with the outcome
3. Convert top jobs into opportunities
4. Generate 3+ solutions per opportunity
5. Identify assumptions and prioritize experiments

**Checkpoint Questions:**
- [ ] Is the outcome measurable and time-bound?
- [ ] Do opportunities connect clearly to jobs?
- [ ] Have we generated multiple solutions (not just the first idea)?
- [ ] Are risky assumptions identified?

**Output:** Opportunity Solution Tree with solutions and experiment backlog

---

### Phase 3: Story Generation (15-20 min)

**Goal:** Break the chosen solution(s) into sprint-ready work.

**Input:** Priority solution(s) from Opportunity Tree

**Process:**
1. Select solution(s) to move forward with
2. Run `/user-stories` for each solution
3. Slice into thin, valuable stories
4. Write BDD acceptance criteria
5. Validate INVEST criteria
6. Map dependencies

**Checkpoint Questions:**
- [ ] Can each story be completed in a sprint?
- [ ] Are acceptance criteria testable?
- [ ] Is scope explicitly bounded (out of scope stated)?
- [ ] Are dependencies identified?

**Output:** Story set with story map, acceptance criteria, and dependencies

---

### Phase 4: PRD Generation (10-15 min)

**Goal:** Synthesize everything into a comprehensive PRD.

**Input:** All artifacts from Phases 1-3

**Process:**
1. Run `/prd` with feature name and context
2. Pull Problem Alignment from JTBD Analysis:
   - The Problem = High-opportunity jobs
   - High-level Approach = Chosen solution direction
   - Goals & Success = Outcome from opportunity tree
3. Pull Solution Alignment from Stories:
   - Key Features = Story titles
   - Key Flows = From acceptance criteria
   - Implementation Approach = From story dependencies
4. Complete Launch Readiness checklist

**Checkpoint Questions:**
- [ ] Does Problem Alignment trace back to validated jobs?
- [ ] Does Solution Alignment reflect the opportunity tree decision?
- [ ] Are metrics connected to the outcome we defined?
- [ ] Is Launch Readiness checklist complete?

**Output:** Complete PRD ready for review

---

## Execution Modes

### Mode 1: Full Workflow (Recommended)

Run all 4 phases sequentially. Takes 40-60 minutes but produces the most rigorous output.

```
/probtoprd "We need to add offline mode to inspections"
```

### Mode 2: Quick Pass

For time-constrained situations, compress the workflow:

1. **JTBD** - Identify top 1 job only
2. **Opportunity Tree** - Skip experiment design, just map solutions
3. **Stories** - MVP stories only, defer edge cases
4. **PRD** - Focus on Problem + Solution Alignment, defer Launch Readiness

Mark the PRD as "DRAFT - Needs full discovery" when using quick mode.

### Mode 3: Resume Mid-Workflow

If you've already done some discovery work:

```
/probtoprd --from-jtbd "[paste JTBD analysis]"
/probtoprd --from-tree "[paste opportunity tree]"
/probtoprd --from-stories "[paste story set]"
```

---

## Output: Combined Artifact Set

At the end of the workflow, you'll have a linked set of documents:

```markdown
# [Feature Name] - Complete Discovery Package

## 📋 Summary

**Original Input:** [The feature request/feedback that started this]
**Primary Job:** [The core JTBD identified]
**Target Outcome:** [Measurable goal]
**Chosen Solution:** [Solution from opportunity tree]
**Effort Estimate:** [Total story points]
**Target Sprint:** [Sprint number]

---

## 🔗 Linked Artifacts

| Artifact | Purpose | Link |
|----------|---------|------|
| JTBD Analysis | Jobs and opportunity scores | [Link] |
| Opportunity Tree | Solutions and experiments | [Link] |
| User Stories | Sprint-ready work items | [Link] |
| PRD | Complete requirements doc | [Link] |

---

## 🔄 Traceability Matrix

| Job (JTBD) | Opportunity (Tree) | Solution (Tree) | Story (Stories) | PRD Section |
|------------|-------------------|-----------------|-----------------|-------------|
| [Job 1] | [Opp 1] | [Sol 1A] | [Story 1-3] | Key Features |
| [Job 2] | [Opp 2] | [Sol 2B] | [Story 4-5] | Key Flows |

---

## ⚠️ Open Risks

| Risk | Source | Mitigation |
|------|--------|------------|
| [Risk 1] | Identified in JTBD | [Mitigation] |
| [Risk 2] | Identified in Tree | [Mitigation] |

---

## 🧪 Experiments to Run

| Experiment | Tests | Priority |
|------------|-------|----------|
| [Exp 1] | [Assumption from tree] | High |
| [Exp 2] | [Assumption from tree] | Medium |

---

## ✅ Workflow Checklist

- [x] JTBD Analysis complete
- [x] Opportunity Tree mapped
- [x] Stories generated
- [x] PRD drafted
- [ ] PRD reviewed by stakeholders
- [ ] Stories estimated by engineering
- [ ] Experiments scheduled
```

---

## When to Use Each Skill Standalone

| If you need... | Use |
|----------------|-----|
| Just understand the jobs | `/jtbd` alone |
| Just explore solutions | `/opportunity-tree` alone |
| Just write stories | `/user-stories` alone |
| Just draft a PRD | `/prd` alone |
| Full discovery → PRD | `/probtoprd` |

---

## Tips for Success

1. **Don't skip JTBD** - It's tempting to jump to solutions, but you'll miss the real opportunity
2. **Multiple solutions matter** - The first idea is rarely the best; force yourself to generate alternatives
3. **Connect the threads** - Each phase should reference the previous; traceability prevents drift
4. **Timebox each phase** - Set limits or you'll overanalyze; discovery is about learning, not perfection
5. **Mark assumptions** - Every decision has assumptions; surface them so you can test them
6. **Review at checkpoints** - The checkpoint questions catch gaps early

---

## Example: End-to-End

**Input:** "Customers keep asking for dark mode"

**Phase 1 - JTBD:**
- Job: "When working in low-light environments, I want to reduce eye strain, so I can work longer without fatigue"
- Opportunity Score: 14 (Importance: 8, Satisfaction: 2)

**Phase 2 - Opportunity Tree:**
- Outcome: Reduce eye-strain-related complaints by 50%
- Opportunity: Users struggle in low-light environments
- Solutions: Dark mode, Reduce brightness, High contrast mode, Auto-adjust by ambient light

**Phase 3 - Stories:**
- Story 1: As a user, I want to toggle dark mode, so I can reduce eye strain
- Story 2: As a user, I want dark mode to sync across devices, so my preference follows me
- Story 3: As a user, I want dark mode to schedule automatically, so I don't have to remember

**Phase 4 - PRD:**
- Problem: Users experience eye strain in low-light, especially field workers doing evening inspections
- Solution: Dark mode with manual toggle and auto-scheduling
- Metrics: Eye strain complaints -50%, Settings adoption +30%
- Launch: iOS 3.5, Android 3.5, Web Sprint 17

---

## Integration Notes

This workflow integrates with:
- **Confluence** - All artifacts can be created as pages via Atlassian MCP
- **Jira** - Stories can be created as issues
- **Figma** - PRD can link to design files via Figma MCP
- **Sprint planning** - Stories are ready for estimation

---

## Quick Reference Card

```
┌────────────────────────────────────────────────┐
│           PROBLEM TO PRD QUICK REF             │
├────────────────────────────────────────────────┤
│                                                │
│  /jtbd        → Jobs (what users really need)  │
│       ↓                                        │
│  /opportunity → Solutions (how to serve jobs)  │
│       ↓                                        │
│  /user-stories→ Stories (what to build)        │
│       ↓                                        │
│  /prd         → PRD (complete requirements)    │
│                                                │
│  /probtoprd   → All 4 in sequence              │
│                                                │
└────────────────────────────────────────────────┘
```
