# Parallel Dispatch Example

This shows how to dispatch multiple interview analysis agents in parallel.

## Scenario

You have 15 interview files to analyze in `./interviews/customers`.

## Step 1: Enumerate Files

```bash
find ./interviews/customers -name "*.rtf" | wc -l
# Output: 15
```

## Step 2: Create Batches

With batch size of 5:
- Batch 1: Files 1-5
- Batch 2: Files 6-10
- Batch 3: Files 11-15

## Step 3: Parallel Dispatch

**CRITICAL**: Send ALL Task calls in a SINGLE message.

The key is invoking multiple Task tools with `run_in_background: true` in parallel:

```
// Pseudocode - all three dispatched simultaneously
Task(
  subagent_type: "general-purpose",
  description: "Analyze interviews 1-5",
  run_in_background: true,
  prompt: "Analyze files [1,2,3,4,5] using Teresa Torres framework..."
)

Task(
  subagent_type: "general-purpose",
  description: "Analyze interviews 6-10",
  run_in_background: true,
  prompt: "Analyze files [6,7,8,9,10] using Teresa Torres framework..."
)

Task(
  subagent_type: "general-purpose",
  description: "Analyze interviews 11-15",
  run_in_background: true,
  prompt: "Analyze files [11,12,13,14,15] using Teresa Torres framework..."
)
```

## Step 4: Agent Prompt Template

Each agent receives a prompt like:

```markdown
Analyze these customer interview files using the Teresa Torres Continuous Discovery framework.

**Files to analyze:**
1. /path/to/Customers/Company1/interview.rtf
2. /path/to/Customers/Company2/interview.rtf
[...etc...]

**For each interview, extract:**

1. **Pain Points** (unprompted, with direct quotes)
2. **Workflow Use Cases** (trigger -> condition -> action)
3. **Integration Systems Mentioned**
4. **Terminology Reactions** ("workflow", "agent" interpretations)
5. **Unprompted Questions** (strongest signal - customer-initiated)
6. **Leading Question Flags**
7. **Key Takeaway** (1-2 sentences)

**Output**: Structured markdown for each interview following template.
```

## Step 5: Collect Results

After agents complete, use TaskOutput or Read to collect:

```bash
# Check output files
cat /private/tmp/claude/.../tasks/agent1.output
cat /private/tmp/claude/.../tasks/agent2.output
cat /private/tmp/claude/.../tasks/agent3.output
```

## Step 6: Aggregate

Merge all agent outputs into the findings document:
1. Add each interview to the log table
2. Append detailed analysis sections
3. Update Emerging Patterns with counts

## Time Savings

| Approach | Time for 15 interviews |
|----------|------------------------|
| Sequential | ~45 minutes (3 min each) |
| Parallel (3 agents) | ~15 minutes |
| **Savings** | **67%** |

## Keys to Success

1. **Independence**: Each agent gets separate files - no overlap
2. **Clear scope**: Specific files, specific output format
3. **Same template**: All agents use identical analysis template
4. **Background mode**: Use `run_in_background: true` for async
5. **Aggregate at end**: Merge outputs after all complete
