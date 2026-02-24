# User Story Generator

Generate sprint-ready user stories with INVEST validation, BDD acceptance criteria, and clear scope boundaries. Transform solutions into implementable work items.

## Invocation

```
/user-stories "Feature or solution to break down"
```

Or natural language:
- "Break this into user stories..."
- "Write stories for..."
- "Create acceptance criteria for..."

---

## The Problem

User stories are either too big to estimate, too vague to test, or so detailed they constrain engineering creativity. Sprint planning grinds to a halt.

## What You Get

- INVEST-validated stories
- BDD acceptance criteria (Given/When/Then)
- Edge cases identified
- Technical notes for engineering
- Out of scope explicitly stated
- Sprint-ready format

---

## User Story Framework

### Standard Format

```
As a [user type],
I want to [action/goal],
So that [benefit/outcome].
```

**Example:**
```
As a safety inspector,
I want to add photos directly into table cells,
So that I can document issues in context without switching between fields.
```

### INVEST Criteria

Every story must pass the INVEST test:

| Criterion | Question | Red Flag |
|-----------|----------|----------|
| **I**ndependent | Can this be built without other stories? | "Depends on story X being done first" |
| **N**egotiable | Is there flexibility in how to implement? | Overly prescriptive technical details |
| **V**aluable | Does this deliver user value on its own? | "Set up database tables" (no user value) |
| **E**stimable | Can engineering estimate this? | Too vague or too complex |
| **S**mall | Can this fit in a sprint? | Epic disguised as a story |
| **T**estable | Can we verify this is done? | "Improve the experience" (not testable) |

---

## Story Generation Workflow

### Step 1: Understand the Solution

Gather context about what you're breaking down:

```markdown
## Solution Context

**Solution name:** [Name from opportunity tree or PRD]
**Parent opportunity:** [What user need does this address?]
**Target outcome:** [What metric should move?]
**Users affected:** [Who will use this?]
**Platforms:** [Web / iOS / Android / API]
```

### Step 2: Identify Story Slices

Break the solution into thin, vertical slices that each deliver value:

**Slicing strategies:**
1. **By user journey step** - Login → Browse → Select → Configure → Save
2. **By user type** - Admin version → User version → Guest version
3. **By CRUD operation** - Create → Read → Update → Delete
4. **By happy path + variations** - Core flow → Edge cases → Error handling
5. **By platform** - Web → iOS → Android

```markdown
## Story Map

| Step/Slice | Story | Priority |
|------------|-------|----------|
| [Journey step 1] | [Story title] | Must have |
| [Journey step 2] | [Story title] | Must have |
| [Variation A] | [Story title] | Should have |
| [Edge case] | [Story title] | Could have |
```

### Step 3: Write Each Story

For each slice, create a complete story:

```markdown
## Story: [Title]

**ID:** [PROJECT-XXX]
**Priority:** Must have / Should have / Could have / Won't have
**Estimate:** [Points or T-shirt size]
**Sprint target:** [Sprint number or TBD]

### User Story

As a [user type],
I want to [action],
So that [benefit].

### INVEST Check

| Criterion | Pass? | Notes |
|-----------|-------|-------|
| Independent | ✅/⚠️/❌ | [Any dependencies?] |
| Negotiable | ✅/⚠️/❌ | [Flexibility in approach?] |
| Valuable | ✅/⚠️/❌ | [Clear user benefit?] |
| Estimable | ✅/⚠️/❌ | [Can engineering size this?] |
| Small | ✅/⚠️/❌ | [Fits in a sprint?] |
| Testable | ✅/⚠️/❌ | [Clear done criteria?] |

### Acceptance Criteria (BDD)

**Scenario 1: [Happy path name]**
```gherkin
Given [initial context/state]
And [additional context if needed]
When [action taken by user]
Then [expected outcome]
And [additional outcomes if needed]
```

**Scenario 2: [Variation or edge case]**
```gherkin
Given [context]
When [action]
Then [outcome]
```

**Scenario 3: [Error handling]**
```gherkin
Given [context that leads to error]
When [action]
Then [error is handled gracefully]
And [user sees helpful message]
```

### Edge Cases

| Case | Expected Behavior |
|------|-------------------|
| [Edge case 1] | [How system should respond] |
| [Edge case 2] | [How system should respond] |
| [Boundary condition] | [How system should respond] |

### Technical Notes

_For engineering context, not prescriptive:_

- [Hint about implementation approach]
- [Relevant existing patterns]
- [API or data considerations]
- [Performance expectations]

### Out of Scope

_Explicitly NOT included in this story:_

- ❌ [Thing that might be assumed but isn't included]
- ❌ [Future enhancement]
- ❌ [Edge case deferred to later story]

### Dependencies

| Dependency | Type | Status |
|------------|------|--------|
| [Story/System/Team] | Blocks / Blocked by | [Ready / Pending / At risk] |

### Design Reference

- Figma: [Link]
- Prototype: [Link]
- Related screenshots: [Links]
```

### Step 4: Validate Story Set

Check the complete set of stories:

```markdown
## Story Set Validation

### Coverage Check
- [ ] Happy path fully covered
- [ ] All user types addressed
- [ ] All platforms addressed
- [ ] Error states handled
- [ ] Edge cases identified (even if deferred)

### Dependency Map
```
[Story 1] ──blocks──> [Story 3]
[Story 2] ──blocks──> [Story 3]
[Story 4] (independent)
```

### Sprint Fit
| Sprint | Stories | Total Points |
|--------|---------|--------------|
| Sprint X | Story 1, 2 | Y points |
| Sprint X+1 | Story 3, 4 | Z points |

### Risks
- [Risk 1 and mitigation]
- [Risk 2 and mitigation]
```

---

## Output Template: Complete Story Set

```markdown
# User Stories: [Feature/Solution Name]

## Overview

**Solution:** [What we're building]
**Opportunity:** [User need this addresses]
**Outcome target:** [Metric we expect to move]
**Total stories:** [Count]
**Estimated effort:** [Total points or sprints]

---

## Story Map

```
[Epic: Feature Name]
│
├── Must Have (MVP)
│   ├── Story 1: [Title] — X points
│   ├── Story 2: [Title] — X points
│   └── Story 3: [Title] — X points
│
├── Should Have
│   ├── Story 4: [Title] — X points
│   └── Story 5: [Title] — X points
│
└── Could Have
    └── Story 6: [Title] — X points
```

---

## Stories

### Story 1: [Title]

**Priority:** Must have
**Estimate:** X points

#### User Story

As a [user type],
I want to [action],
So that [benefit].

#### Acceptance Criteria

**Scenario 1: [Name]**
```gherkin
Given [context]
When [action]
Then [outcome]
```

**Scenario 2: [Name]**
```gherkin
Given [context]
When [action]
Then [outcome]
```

#### Edge Cases

| Case | Behavior |
|------|----------|
| [Case] | [Behavior] |

#### Technical Notes

- [Note for engineering]

#### Out of Scope

- ❌ [Explicitly excluded]

#### INVEST: ✅ Independent ✅ Negotiable ✅ Valuable ✅ Estimable ✅ Small ✅ Testable

---

### Story 2: [Title]
...

---

## Dependencies

```
Story 1 ──┬──> Story 3
Story 2 ──┘
Story 4 (independent)
Story 5 ──> Story 6
```

---

## Definition of Done

For all stories in this set:

- [ ] Code complete and reviewed
- [ ] Unit tests passing
- [ ] Acceptance criteria verified
- [ ] Edge cases tested
- [ ] Documentation updated
- [ ] Design sign-off
- [ ] Product sign-off
- [ ] Deployed to staging
- [ ] No regressions in smoke tests

---

## Open Questions

- [ ] [Question for design]
- [ ] [Question for engineering]
- [ ] [Decision needed from stakeholders]
```

---

## BDD Writing Guide

### Good Acceptance Criteria

```gherkin
# Specific, testable, focused
Given I am on the template editor
And I have an empty table with 3 rows
When I click on a cell and tap "Add Photo"
Then the camera interface opens
And the photo is inserted into that cell when captured
And the cell expands to show a thumbnail preview
```

### Bad Acceptance Criteria

```gherkin
# Vague, hard to test
Given I am using the app
When I add a photo
Then it works correctly  # What does "correctly" mean?
```

### Common Patterns

**Happy path:**
```gherkin
Given [user is in valid starting state]
When [user takes primary action]
Then [expected positive outcome]
```

**Validation:**
```gherkin
Given [user is in starting state]
When [user enters invalid input]
Then [validation error is shown]
And [user is guided to correct the issue]
```

**Empty state:**
```gherkin
Given [no data exists yet]
When [user views the feature]
Then [helpful empty state is shown]
And [user is guided to add first item]
```

**Permissions:**
```gherkin
Given [user lacks required permission]
When [user attempts restricted action]
Then [user sees clear explanation]
And [user is guided to get access]
```

**Offline:**
```gherkin
Given [user is offline]
When [user performs action]
Then [action is queued for sync]
And [user sees offline indicator]
```

---

## Story Sizing Guide

| Size | Characteristics | Example |
|------|-----------------|---------|
| **XS (1pt)** | Config change, copy update, simple UI tweak | "Change button label from 'Submit' to 'Save'" |
| **S (2pt)** | Single component, clear path, minimal logic | "Add date picker to form" |
| **M (3pt)** | Multiple components, some logic, clear scope | "Add photo upload with preview" |
| **L (5pt)** | Multiple interactions, complex logic, needs design | "Build multi-step wizard" |
| **XL (8pt)** | Cross-cutting, needs spike, high uncertainty | "Add real-time collaboration" → Should break down further |

**Rule of thumb:** If a story is XL or larger, break it into smaller stories.

---

## Anti-Patterns to Avoid

| Anti-Pattern | Problem | Fix |
|--------------|---------|-----|
| **Technical story** | "Set up database" has no user value | Reframe as user capability it enables |
| **Epic in disguise** | Too big to estimate or fit in sprint | Slice thinner by journey, user, or scope |
| **Prescriptive solution** | "Use React hooks to..." constrains engineering | Focus on what, not how |
| **Missing acceptance** | "Make it good" isn't testable | Add specific Given/When/Then |
| **Kitchen sink** | Story tries to do too many things | One primary action per story |

---

## Integration Points

**Inputs from:**
- `/opportunity-tree` - Solutions become epics to break into stories
- `/jtbd` - Jobs inform story context and "so that" benefit
- Design specs - Inform acceptance criteria and edge cases

**Feeds into:**
- `/prd` - Stories appear in Solution Alignment section
- Sprint planning - Stories are ready for estimation and assignment
- Engineering - Clear scope for implementation
- QA - Acceptance criteria become test cases
