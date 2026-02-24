---
description: Full discovery workflow from problem to PRD $ARGUMENTS
---

You are running the complete Problem-to-PRD workflow, chaining four discovery skills into one comprehensive process.

## Task

Transform a feature request or customer problem into a complete, sprint-ready PRD with full discovery artifacts. Use the methodology in `/Users/ryanclement/.claude/skills/probtoprd.md`.

## The Workflow

```
INPUT (feature request / feedback / problem)
    │
    ▼
┌─────────────────────────────────┐
│ Phase 1: /jtbd (5-10 min)       │
│ Extract underlying jobs         │
│ Score opportunities             │
└───────────────┬─────────────────┘
                │ Jobs → Opportunities
                ▼
┌─────────────────────────────────┐
│ Phase 2: /opportunity-tree      │
│ (10-15 min)                     │
│ Map solutions, identify risks   │
└───────────────┬─────────────────┘
                │ Solutions → Epics
                ▼
┌─────────────────────────────────┐
│ Phase 3: /user-stories          │
│ (15-20 min)                     │
│ Sprint-ready work items         │
└───────────────┬─────────────────┘
                │ Stories → PRD content
                ▼
┌─────────────────────────────────┐
│ Phase 4: /prd (10-15 min)       │
│ Full PRD with launch checklist  │
└─────────────────────────────────┘
    │
    ▼
OUTPUT: Complete discovery package
```

## Phase Checkpoints

### After Phase 1 (JTBD):
- [ ] Identified jobs beyond surface request?
- [ ] Uncovered emotional drivers?
- [ ] High-opportunity-score jobs identified?

### After Phase 2 (Opportunity Tree):
- [ ] Outcome is measurable?
- [ ] 3+ solutions per opportunity?
- [ ] Risky assumptions identified?

### After Phase 3 (Stories):
- [ ] Each story fits in a sprint?
- [ ] Acceptance criteria testable?
- [ ] Out of scope explicitly stated?

### After Phase 4 (PRD):
- [ ] Problem Alignment traces to jobs?
- [ ] Solution Alignment reflects tree?
- [ ] Metrics connected to outcome?

## Execution

I will run through all 4 phases, providing checkpoints after each. At each checkpoint, I'll ask if you want to:
- **Continue** to the next phase
- **Refine** the current phase output
- **Pause** and save progress

## Final Deliverables

1. **JTBD Analysis** - Jobs and opportunity scores
2. **Opportunity Tree** - Solutions and experiments
3. **User Stories** - Sprint-ready with acceptance criteria
4. **PRD** - Complete PRD using the standard template
5. **Traceability Matrix** - Connecting all artifacts

If no input provided, ask: "What feature request, customer problem, or feedback would you like me to take through the full discovery-to-PRD workflow?"
