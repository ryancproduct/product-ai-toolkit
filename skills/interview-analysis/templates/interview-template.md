# Interview Analysis Template

Use this template when analyzing customer interview transcripts.

## Interview Metadata

```markdown
### Interview N: [Company] - [Participant Name]
**File**: `[filename]`
**Participant**: [Name] ([Role])
**Company Context**: [Brief company description]
**Interview Type**: [Discovery | Concept Validation | Usability Test]
```

## Analysis Sections

### 1. Current State & Pain Points

Extract **unprompted** pain points with direct quotes:

```markdown
**Key Pain Points** (Unprompted):
1. **[Pain Category]** — "[exact quote]"
2. **[Pain Category]** — "[exact quote]"
```

Categories:
- Integration/Systems disconnect
- Manual data aggregation
- Time on admin vs action
- Lack of visibility/reporting
- Compliance/regulatory burden
- Training/knowledge gaps

### 2. Workflow Use Cases

Identify automation scenarios the customer describes wanting:

```markdown
**Workflow Use Cases Identified**:

1. **[Workflow Name]**:
   - Trigger: [What starts it]
   - Condition: [When it applies]
   - Action: [What happens]
   - Quote: "[customer's words]"
```

### 3. Integration Systems

List systems mentioned with context:

```markdown
**Systems Mentioned**:
| System | Type | Context |
|--------|------|---------|
| Deputy | Rostering | "Integration is non-negotiable" |
```

### 4. Terminology Reactions

Document how customer interprets key terms:

```markdown
**Terminology Reactions**:

**"Workflow" interpretation**:
> "[quote showing their mental model]"
Classification: [SOP/Checklist | Automation | Mixed]

**"Agent" interpretation**:
> "[quote]"
Classification: [Understood | Confused | Alternative suggested]
```

### 5. Unprompted Questions (High Value)

These represent strongest signals - questions customer asked without prompting:

```markdown
**Unprompted Questions** (High Value):
1. "[Customer question]" — Implication: [what this reveals]
```

### 6. Reactions to Concepts Shown

For concept validation interviews:

```markdown
**Reactions to Concepts Shown**:
| Concept | Reaction | Evidence |
|---------|----------|----------|
| Dashboard | Positive | "[quote]" |
| Workflows | Confused | "[quote]" |
```

### 7. Leading Question Flags

Note questions that may have biased responses:

```markdown
**Leading Question Flags**:
- "[Question asked]" — [Issue: assumes positive, binary, provides options]
```

### 8. Key Takeaway

One paragraph summary of most important findings:

```markdown
**Key Takeaway**: [Company type] with [key characteristic]. Core pain: [biggest issue]. [Most important insight]. [Strongest signal/quote]. [Willingness to pay/adopt if mentioned].
```

## Pattern Extraction for Aggregation

After analyzing, extract for cross-interview aggregation:

```yaml
pain_points:
  - category: "Multiple disconnected systems"
    quote: "..."

workflow_use_cases:
  - name: "Temperature excursion → Auto-call vendor"
    trigger: "Sensor threshold"
    action: "Place call"

integrations:
  - system: "Deputy"
    type: "Rostering"
    priority: "P0"

terminology:
  workflow: "SOP" | "automation" | "mixed"
  agent: "understood" | "confused" | "alternative"

unprompted_questions:
  - question: "Is a call being placed automatically?"
    implication: "Wants execution, not just notification"
```
