---
name: roadmap-narrative
description: Turn a roadmap into a compelling narrative for different audiences — exec, engineering, and customer-facing. Eliminates the copy-paste-reframe cycle. Use when you need to communicate what's coming and why, not just list features.
---

# Roadmap Narrative Skill

Turn a roadmap — however rough — into polished, audience-specific narratives. One input, three outputs.

## Input: $ARGUMENTS

Accepts:
- `/roadmap-narrative` — Will ask for the roadmap interactively
- `/roadmap-narrative [path/to/roadmap.md]` — Read from file
- `/roadmap-narrative [pasted content]` — Accept pasted text, table, or bullet list

If no input is provided, ask:
> "Paste your roadmap or describe what you're shipping over the next 1-3 quarters. It can be rough — bullet points, a table, or even just a list of feature names. I'll do the rest."

If input is brief (just feature names), ask ONE follow-up question:
> "What's the strategic theme tying this roadmap together? What problem are you fundamentally solving for customers this period?"

Don't ask more than one question. Work with what you have.

---

## Phase 1: Parse the Roadmap

Extract from the input:
- **Items**: Each initiative, feature, or theme
- **Time horizon**: Now/Next/Later, Q1/Q2/Q3, or whatever structure is given
- **Implied theme**: What's the common thread across this work?
- **Notable gaps**: Anything conspicuously absent that stakeholders might ask about?

If no time horizon is given, group items into Now / Next / Later based on apparent priority or sequence.

---

## Phase 2: Identify the Narrative Arc

Every roadmap has a story. Find it:

- **Problem arc**: "Customers couldn't do X. We're fixing that."
- **Platform arc**: "We're laying foundations now so we can move fast later."
- **Growth arc**: "We're doubling down on what's working."
- **Catch-up arc**: "We're closing the gap on table-stakes functionality."
- **Strategic pivot**: "We're moving from X to Y."

Name the arc explicitly — it becomes the spine of every version of the narrative.

---

## Phase 3: Generate Three Narratives

Generate all three versions. Each should be self-contained — do not require the reader to have read another version.

### Version 1: Executive Summary (100-150 words)

Audience: CPO, CEO, board. Assumes they haven't read anything about this.

Structure:
1. **The strategic theme** — What's the one thing this roadmap is about?
2. **The customer problem** — Why now? What changed?
3. **The three big bets** — What are we actually shipping? (3 items max)
4. **The outcome** — What will be measurably different in 6 months?

Format: Prose, not bullets. Sounds like something you'd say in a meeting, not a status update.

---

### Version 2: Engineering / Team Brief (300-400 words)

Audience: Engineering leads, designers, PMs. They want context and sequencing.

Structure:
1. **Why this roadmap** — The strategic rationale and key decisions made
2. **Sequencing logic** — Why are we doing things in this order?
3. **Dependencies & risks** — What are we betting on? What could derail us?
4. **How we'll know it's working** — Success metrics per initiative (use Amplitude data if available)
5. **What we're NOT doing** — Explicit out-of-scope to prevent scope creep

Format: Mix of prose and bullets. Opinionated. Name trade-offs.

---

### Version 3: Customer-Facing / External (150-200 words)

Audience: Customers, sales, CSMs. They want to know what's coming that helps them.

Structure:
1. **The customer problem we're solving** — Empathetic, outcome-focused
2. **What's coming** — Framed as customer outcomes, not feature names
3. **Timing** — Honest but not committed. Use "coming soon", "this quarter", "later this year"
4. **Call to action** — What should customers do with this info? (Try the beta, talk to their CSM, etc.)

Format: Friendly, non-technical. No internal jargon. Sounds like a product newsletter, not a Jira epic.

---

## Phase 4: Output

Present all three versions back-to-back, clearly labelled.

After presenting, offer:
> "Want me to adjust the tone, emphasis, or length on any of these? I can also draft a Confluence page, Slack announcement, or slide deck outline if useful."

---

## Tips

- If the roadmap is heavily feature-named ("Add bulk export", "New dashboard widget"), translate feature names into customer outcomes before writing any version.
- If you spot a strategic gap or incoherence in the roadmap (e.g., two conflicting themes, or a quarter with nothing customer-facing), flag it gently: "One thing I noticed — the Q2 work is all infrastructure with no customer-facing output. Do you want me to flag that in the exec version or omit it?"
- Never invent initiatives that weren't in the input. If the roadmap is thin, say so — don't pad it.
