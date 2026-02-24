# Interview Synthesis Template

Use after all individual interview analyses are complete to create the Emerging Patterns section.

## Aggregation Process

### Step 1: Collect All Pain Points

From each interview, extract pain points and count frequency:

```markdown
| Pain Point | Count | Companies |
|------------|-------|-----------|
| Multiple disconnected systems | 42/56 | Anyday, Quest, Blue Coral... |
| Manual data aggregation | 38/56 | Fishbowl, CASCO... |
```

### Step 2: Aggregate Workflow Use Cases

Collect all workflow automation scenarios mentioned:

```markdown
| Use Case | Count | Companies | Key Quote |
|----------|-------|-----------|-----------|
| Temperature → Auto-call | 14 | HF, Anyday... | "Is a call being placed automatically?" |
```

### Step 3: Compile Integration Systems

Group by type and priority:

```markdown
| System | Type | Count | Priority |
|--------|------|-------|----------|
| Deputy | Rostering | 12 | P0 |
| Planon | Work Orders | 4 | P1 |
```

Priority classification:
- **P0**: Mentioned >10 times OR explicitly "non-negotiable"
- **P1**: Mentioned 5-10 times OR "would be valuable"
- **P2**: Mentioned <5 times OR "nice to have"

### Step 4: Summarize Terminology Patterns

Count interpretation patterns:

```markdown
| Term | Interpretation | Count | Example |
|------|----------------|-------|---------|
| "Workflow" | Confused with SOPs | 24/56 | "That's why I see that as SOPs" |
| "Workflow" | Understood as automation | 12/56 | "One action triggers something else" |
```

### Step 5: Extract Strongest Signals

Rank unprompted questions by frequency and importance:

```markdown
| Question | Companies | Implication |
|----------|-----------|-------------|
| "Is a call being placed automatically?" | HF | Core value prop gap |
```

### Step 6: Identify Leading Question Patterns

Flag patterns that may have biased results:

```markdown
| Pattern | Frequency | Impact |
|---------|-----------|--------|
| "Does this resonate?" | 28 | May inflate positive feedback |
```

### Step 7: Generate Recommendations

Based on patterns, create actionable recommendations:

```markdown
1. **Rename "Workflows"** → Lead with "Automation"
2. **Pre-built templates** → Don't start with blank canvas
3. **Integration is table stakes** → Deputy, Tanda as P0
```

## Opportunity Solution Tree Structure

After synthesis, update OST:

```
OUTCOME: [Business outcome from patterns]

├── OPPORTUNITY 1: [Pain point with highest frequency]
│   ├── Solution: [Validated solution from interviews]
│   └── Evidence: [Quote count and key quote]
│
├── OPPORTUNITY 2: [Next pain point]
│   └── ...
```

## Feature Value Hierarchy

Rank features by customer importance:

```markdown
1. **Dashboard** — #1 priority across segments
2. **Integrations** — Non-negotiable
3. **AI Assistant** — High interest
4. **Workflows** — Strong but terminology confusion
5. **Computer Vision** — Niche but high where applicable
```

## Segment-Specific Patterns

Identify patterns unique to customer segments:

```markdown
| Segment | Unique Characteristics |
|---------|------------------------|
| QSR | Gamification, young workforce, seasonal |
| Enterprise | Power Automate competition, complex governance |
| Manufacturing | Event-triggered, ERP integration critical |
```

## Quality Assessment

Rate the research quality:

```markdown
### Evidence Quality

- **Strong signals**: Unprompted questions, customer objections
- **Medium signals**: Task-based observations, concrete examples
- **Weak signals**: Responses to "does this resonate?" questions

### Bias Assessment

- **Medium-Low Risk**: Good mix of open questions
- Weight unprompted statements more heavily than prompted responses
```
