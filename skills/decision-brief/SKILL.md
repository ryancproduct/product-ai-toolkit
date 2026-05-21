---
name: decision-brief
description: Generate a crisp 1-page decision brief for any product decision — options, trade-offs, risks, and a clear recommendation. Faster than a full PRD for tactical calls. Use when you need to align stakeholders on a decision, not just report a conclusion.
---

# Decision Brief Skill

Produce a structured 1-page brief for any product decision — from "should we build this feature?" to "which technical approach should we take?" to "do we cut scope or delay the launch?".

## Input: $ARGUMENTS

Accepts:
- `/decision-brief [the decision]` — State the decision directly
- `/decision-brief` — Will ask interactively

If no input, ask:
> "What's the decision you're trying to make? Describe it in one sentence — even rough is fine."

If input is a statement (not a question), reframe it as a decision question: "Whether to [X]" or "Which approach to take for [X]".

---

## Phase 1: Frame the Decision

Before exploring options, nail the framing:

1. **Decision owner**: Who is making this decision? (If not stated, leave blank)
2. **Decision type**: Classify it
   - **Strategic** — affects product direction, positioning, or major investment
   - **Tactical** — affects execution approach, scope, or timeline
   - **Reversible** — can be undone with low cost (e.g., feature flag rollout)
   - **Irreversible** — hard to undo (e.g., data migration, customer-facing deprecation)
3. **Decision deadline**: When does this need to be made?
4. **Decision context**: What triggered this? What happened to make this decision necessary now?

---

## Phase 2: Enrich Context

Attempt to pull relevant context before generating the brief. Do not block on any source.

- **Jira**: Any related tickets, past decisions, or linked work
- **Confluence / Glean**: Prior research, strategy docs, or similar decisions made before
- **Amplitude**: Any usage data relevant to the decision
- **Intercom**: Any customer signal that informs the options

If you find useful context, weave it into the brief. If nothing is found, proceed without it.

---

## Phase 3: Generate the Brief

```markdown
# Decision Brief: [Decision Question]

**Owner**: [Name or role]
**Date**: [Today's date]
**Deadline**: [When this must be decided]
**Type**: Strategic / Tactical | Reversible / Irreversible

---

## Context
[2-3 sentences: what's the situation and what triggered this decision?]

---

## Options

### Option A: [Name]
**What it is**: [Plain-English description]
**Why it's appealing**: [The genuine upside]
**Risks**: [What could go wrong]
**Effort**: [Rough estimate — days/weeks/months]
**Reversibility**: [Easy to undo / Hard to undo]

### Option B: [Name]
[Same structure]

### Option C: [Name — if applicable]
[Same structure, or "Don't act / defer" as a default third option]

---

## Trade-off Summary

| | Option A | Option B | Option C |
|---|---|---|---|
| Speed | | | |
| Customer impact | | | |
| Risk | | | |
| Reversibility | | | |
| Alignment with strategy | | | |

---

## Key Assumptions
[What must be true for each option to work? Which assumptions are most uncertain?]

---

## Recommendation

**Recommended option**: [Option X]

**Reasoning**: [2-3 sentences — why this option, why now, what seals it]

**Conditions**: [Any conditions that would change this recommendation — "unless X, in which case Option B"]

**Next step**: [The single most important action to take after this decision is made]

---

## Open Questions
- [ ] [Question that needs answering to execute this decision]
- [ ] [Question that someone else needs to answer]

---

## Stakeholders to Inform
- [Name/role — what they need to know]
- [Name/role — what they need to decide or approve]
```

---

## Phase 4: Offer Refinement

After presenting the brief, offer:
> "Want me to pressure-test the recommendation with `/debate`, turn this into a Confluence page, or draft a Slack message to share the decision?"

---

## Principles

- **Name the recommendation clearly.** Briefs that hedge ("it depends") are useless. Pick an option and defend it.
- **Three options minimum.** "Do X" vs "Don't do X" is lazy. Include a third option (often "defer and learn more") to force real comparison.
- **Reversibility matters.** Label it explicitly — it changes how much deliberation the decision deserves.
- **Separate assumptions from facts.** If the recommendation rests on an unvalidated assumption, name it. That's the risk.
- **One next step.** Always. Decisions that end with no action become permanent debates.
