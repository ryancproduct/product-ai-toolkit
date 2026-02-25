---
name: interview-analysis
description: Analyze customer interview files in parallel using Teresa Torres Continuous Discovery framework. Use when you have multiple interview files to analyze.
---

# Interview Analysis Skill

Analyze customer interview transcripts in parallel using the Teresa Torres Continuous Discovery framework.

## Input: $ARGUMENTS

Parse arguments:
- **folder-path**: Directory containing interview files (required)
- **--output**: Path to findings markdown file (default: `<folder>/Interview-Analysis-Findings.md`)
- **--batch-size**: Number of interviews per parallel agent (default: 5)

## Execution Strategy

### 1. Discovery Phase

First, enumerate all interview files:

```bash
find <folder-path> -name "*.rtf" -o -name "*.txt" -o -name "*.md" | sort
```

### 2. Parallel Dispatch

**CRITICAL**: Use the Task tool to dispatch multiple agents IN A SINGLE MESSAGE.

For each batch of files, create a Task with:
- **subagent_type**: "general-purpose"
- **prompt**: Include the specific files AND the analysis template below
- **run_in_background**: true (for large batches)

Example dispatch pattern:
```
// Dispatch 3 agents analyzing 5 files each - ALL IN ONE MESSAGE
Task("Analyze interviews 1-5", files=[...], template)
Task("Analyze interviews 6-10", files=[...], template)
Task("Analyze interviews 11-15", files=[...], template)
```

### 3. Analysis Template (for each agent)

Each parallel agent receives this template:

---

**For each interview file, extract:**

1. **Metadata**
   - Company/Participant/Role
   - Interview type (Discovery/Concept Validation/Usability)

2. **Pain Points** (Unprompted)
   - Direct quotes with context
   - Classify: operational, integration, data, training, compliance

3. **Workflow Use Cases**
   - Trigger → Condition → Action patterns mentioned
   - Quote the exact customer language

4. **Integration Systems Mentioned**
   - System name, type, priority signal

5. **Terminology Reactions**
   - "Workflow" interpretation (SOP vs automation)
   - "Agent" interpretation
   - Alternatives suggested

6. **Unprompted Questions** (Strongest Signal)
   - Questions customer asked without prompting
   - These are highest-confidence insights

7. **Leading Question Flags**
   - Questions that may have biased responses
   - "Does this resonate?" patterns

8. **Key Takeaway** (1-2 sentences)

**Output Format**: Structured markdown with direct quotes.

---

### 4. Aggregation Phase

After all agents return:

1. **Collect all outputs** using TaskOutput tool
2. **Merge into findings document**:
   - Add each interview to the log table
   - Append detailed analysis sections
3. **Update Emerging Patterns**:
   - Tally pain points by frequency
   - Aggregate workflow use cases
   - Compile integration systems
   - Summarize terminology reactions

### 5. Pattern Synthesis

After individual analyses, update the Emerging Patterns section:

```markdown
### Pain Points (by frequency)
| Pain Point | Count | Companies |
|------------|-------|-----------|
```

Count occurrences across all interviews for:
- Pain points
- Workflow use cases
- Integration systems
- Terminology confusion patterns
- Leading question patterns

## Parallel Dispatch Rules

1. **Independence**: Each agent works on different files - no shared state
2. **Batch sizing**: 5-7 files per agent is optimal
3. **Single message**: Dispatch ALL agents in one tool call block
4. **Background mode**: Use `run_in_background: true` for >3 files/agent
5. **Output files**: Check with `Read` tool when agents complete

## Example Invocation

```
/interview-analysis ./interviews/customers --output ./findings.md --batch-size 5
```

## Error Handling

- If a file can't be read, log it and continue
- If an agent fails, note the batch and retry individually
- Always verify file count matches interview count at the end

## Output

The skill produces:
1. **Interview Log Table**: All interviews with metadata
2. **Detailed Analysis**: Per-interview findings with quotes
3. **Emerging Patterns**: Aggregated cross-interview insights
4. **Recommendations**: Actionable takeaways from patterns

## Verification

After completion:
1. Count files in folder
2. Count entries in log table
3. Ensure all accounted for (note multi-part interviews)
