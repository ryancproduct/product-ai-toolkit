# Design: Experiment & Debate Skills for PM AI Kit

**Date:** 2026-02-22
**Author:** Ryan Clement + Claude
**Status:** Approved

---

## Skill 1: `/experiment` — Experiment Design & Analysis

**Type:** Simple command (single `.md` file)
**Location:** `/Users/ryanclement/.claude/commands/experiment.md`
**Invocation:** `/experiment` or `/experiment [feature/idea name]`
**Audience:** Teams using Amplitude MCP for analytics

### Design

A guided wizard that walks through 5 phases, establishing a standard experiment process where none exists today.

#### Phase 1: Hypothesis Framing

Forces structured hypothesis format:

> **If we** [intervention] **then** [metric] **will** [direction] **by** [magnitude] **because** [mechanism]

Also captures:
- What are we changing? (UI, flow, pricing, copy, algorithm)
- Who's affected? (all users, segment, plan tier)
- What's the risk if we're wrong? (reversible/irreversible, blast radius)

Asks clarifying questions until hypothesis is crisp. Won't proceed without a well-formed hypothesis.

#### Phase 2: Metric Selection

Uses Amplitude MCP to pull actual events from the taxonomy.

- **Primary metric**: The one thing this experiment must move. Suggests candidates based on hypothesis, validates they exist in Amplitude.
- **Secondary metrics**: Supporting signals (e.g., if primary is conversion, secondary might be time-to-convert).
- **Guardrail metrics**: Things that must NOT degrade (e.g., support ticket rate, crash rate, retention). Suggests defaults based on feature area.

#### Phase 3: Sample Size & Duration

Calculates minimum detectable effect (MDE) and required sample size:
- Asks for current baseline metric value (or pulls from Amplitude if available)
- Asks for minimum meaningful lift ("what's the smallest improvement worth shipping?")
- Estimates daily eligible traffic
- Calculates required duration at 80% power, 95% confidence
- Flags if duration > 6 weeks and suggests alternatives (larger MDE, narrower audience, different metric)

#### Phase 4: Launch Checklist

Generates pre-launch checklist:
- [ ] Feature flag created and targeting configured
- [ ] Amplitude events firing correctly (verify in debugger)
- [ ] Control and variant groups are equivalent (no selection bias)
- [ ] Guardrail metric alerts set up
- [ ] Experiment registered (Confluence page / decision log)
- [ ] Rollback plan documented
- [ ] Expected end date: [calculated]

#### Phase 5: Result Interpretation (Post-Run)

User returns after experiment runs. Either:
- Pastes results manually, OR
- Skill queries Amplitude MCP for experiment metrics

Outputs:
- Statistical significance assessment
- Practical significance (is the effect big enough to matter?)
- Guardrail metric check (did anything degrade?)
- Segment breakdown if relevant
- **Recommendation**: Ship / Iterate / Kill — with reasoning
- Assumptions and caveats

#### Output Format

Markdown experiment doc with all 5 phases. Structured for pasting into Confluence or a decision log.

### Future Enhancement (Phase 2)

Add `skills/experiment/` folder with Python stats script (scipy) for:
- Proper power analysis calculations
- Bayesian inference option
- Automated Amplitude querying for result interpretation

---

## Skill 2: `/debate` — Pro/Against Product Debate

**Type:** Complex skill (folder with `SKILL.md`)
**Location:** `/Users/ryanclement/.claude/skills/debate/SKILL.md`
**Invocation:** `/debate [idea, feature name, or path to PRD]`
**Audience:** Teams using MCP integrations (Amplitude, Jira, Confluence, Glean)

### Design

Parallel agent debate that stress-tests a product idea by spawning Champion and Sceptic agents simultaneously, then synthesises into actionable output.

#### Phase 1: Context Gathering

Accepts flexible input (one-liner to full PRD):
- File path → reads full document
- Freeform text → captures as-is
- Optionally enriches via MCPs:
  - Amplitude: Current metrics for affected area
  - Jira: Related tickets, past attempts
  - Confluence: Existing research or strategy docs
  - Glean: Broader organisational context

Asks one clarifying question if needed: "What's the strategic context? Why is this being considered now?"

#### Phase 2: Parallel Agent Dispatch

Spawns two agents simultaneously via Task tool in a single message:

**Champion Agent** — Strongest case FOR:
- Market opportunity and timing
- Customer evidence supporting the need
- Competitive advantage / differentiation
- Revenue and growth potential
- Strategic alignment
- Best-case scenario and compounding effects
- Steelmans the idea — fills gaps the user didn't think of

**Sceptic Agent** — Attacks every assumption AGAINST:
- Hidden costs and complexity (eng, support, maintenance)
- Cannibalisation or negative second-order effects
- Competitive response risks
- Customer segments harmed or confused
- Opportunity cost — what are we NOT doing?
- Failure modes and worst-case scenarios
- Historical precedent — tried before? What happened?

Both receive identical context. Each produces 10 structured arguments ranked by strength.

#### Phase 3: Synthesis

Main thread collects both outputs and produces three deliverables:

**1. Risk Register**

| # | Risk | Source | Severity | Likelihood | Mitigation |
|---|------|--------|----------|------------|------------|
| 1 | [risk] | Sceptic Arg #N | High/Med/Low | High/Med/Low | [suggestion] |

Ranked by severity × likelihood. Each traces to the specific argument that surfaced it.

**2. Minimum Viable Scope**

- Features the Champion defended that the Sceptic couldn't kill
- Scope cuts the Sceptic suggested that Champion's arguments don't contradict
- Smallest version worth building, informed by both perspectives

**3. Assumption Map**

| Assumption | Confidence | Evidence | Test |
|------------|-----------|----------|------|
| [assumption] | High/Med/Low | [what exists] | [cheapest validation] |

#### Phase 4: Go / No-Go Recommendation

- **Recommendation**: Proceed / Proceed with conditions / Pause & validate / Kill
- **Confidence level**: High / Medium / Low
- **Key conditions** (if proceed with conditions): What must be true?
- **Next actions**: 2-3 concrete next steps

#### Output Format

Full markdown document combining all four phases. Designed for Confluence, Slack sharing, or Jira epic attachment.

---

## Implementation Notes

- Both skills follow existing conventions: YAML frontmatter with `name` and `description`, kebab-case naming
- Experiment skill: single `.md` command file
- Debate skill: `skills/debate/SKILL.md` folder structure (parallel agent orchestration)
- Both use Australian English spelling
- Both integrate with existing SC MCP stack (Amplitude, Jira, Confluence, Glean)
