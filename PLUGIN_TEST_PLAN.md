# AI PM Kit — Plugin Test Plan

Manual QA checklist for verifying the AI PM Kit installs and behaves correctly as a Claude Code plugin. Run the phases in order; each builds on the previous one.

---

## Phase 1: Pre-flight

| # | Check | Action | Pass criteria |
|---|-------|--------|---------------|
| 1.1 | Claude Code installed | `claude --version` | Prints version ≥ 1.0 |
| 1.2 | Git available | `git --version` | Prints version |
| 1.3 | Node.js available | `node --version` | Prints version ≥ 18 |
| 1.4 | Python available | `python3 --version` | Prints version ≥ 3.10 |
| 1.5 | No prior install | Check `~/.claude/plugins/` for `ai-pm-kit` | Directory does not exist |

---

## Phase 2: Installation

| # | Check | Action | Pass criteria |
|---|-------|--------|---------------|
| 2.1 | Install from branch | `claude plugin install <repo>#feat/plugin-conversion` | Exits 0, prints success message |
| 2.2 | Plugin registered | `claude plugin list` | `ai-pm-kit` appears with correct version (`1.0.0`) |
| 2.3 | Files on disk | `ls ~/.claude/plugins/ai-pm-kit/` | Contains `commands/`, `skills/`, `agents/`, `.claude-plugin/plugin.json`, `CLAUDE.md` |

---

## Phase 3: Plugin structure

| # | Check | Action | Pass criteria |
|---|-------|--------|---------------|
| 3.1 | CLAUDE.md loads | Start a new Claude Code session and run `/help` or ask "What commands do you have?" | Response references AI PM Kit commands |
| 3.2 | Commands discoverable | Ask Claude "List all slash commands from AI PM Kit" | All 15 commands listed (see Appendix A) |
| 3.3 | Skills discoverable | Ask Claude "List all skills from AI PM Kit" | All 19 skills listed (see Appendix B) |
| 3.4 | Agents discoverable | Ask Claude "What agents can you delegate to?" | All 5 agents listed (see Appendix C) |
| 3.5 | plugin.json valid | `cat ~/.claude/plugins/ai-pm-kit/.claude-plugin/plugin.json \| python3 -m json.tool` | Valid JSON, name is `ai-pm-kit` |

---

## Phase 4: Commands — standalone (no MCP required)

Test each command with minimal input to verify it loads its skill, prompts correctly, and produces output.

| # | Command | Test input | Pass criteria |
|---|---------|-----------|---------------|
| 4.1 | `/jtbd` | "Users complain our search is slow" | Outputs job statements in When ___ I want to ___ So I can ___ format |
| 4.2 | `/opportunity-tree` | Paste output from 4.1 | Produces a tree with Outcome → Opportunities → Solutions |
| 4.3 | `/user-stories` | "As a user I need faster search results" | Generates INVEST-validated stories with BDD acceptance criteria |
| 4.4 | `/probtoprd` | "Our onboarding drop-off is 60% at step 3" | Chains through JTBD → OST → stories → PRD; final output is a PRD |
| 4.5 | `/feature-request` | "Add dark mode to the dashboard" | Outputs a RICE-scored evaluation with recommendation |
| 4.6 | `/rapid-prototype` | "A settings page with toggle switches for notifications" | Creates an HTML file, opens or displays it |
| 4.7 | `/recall` | Run after `/learn` (Phase 6) | Lists previously saved knowledge topics |
| 4.8 | `/standup` | Run inside a git repo with recent commits | Produces a standup summary referencing recent work |
| 4.9 | `/stakeholder-update` | "We shipped the new auth flow last week" | Produces audience-tailored update (exec vs. engineering) |
| 4.10 | `/retrospective` | "Sprint 42 just ended" | Outputs a retro with What went well / What didn't / Actions |
| 4.11 | `/add-mcp` | Run it | Displays instructions for adding MCP servers to Claude Code |

---

## Phase 5: Commands — MCP-dependent

> These tests require configured MCP integrations. Mark as **SKIPPED** if the integration is unavailable.

| # | Command | Required MCP | Test input | Pass criteria |
|---|---------|-------------|-----------|---------------|
| 5.1 | `/experiment` | Amplitude | "Test whether a larger CTA button improves signup conversion" | Outputs hypothesis, metrics, sample-size calc, launch checklist |
| 5.2 | `/weekly-update` | Jira + Amplitude | "Generate this week's update" | Pulls sprint data and metrics; produces formatted update |
| 5.3 | `/competitive-analysis` | WebSearch | "Analyze Notion vs Coda vs Slite" | Produces competitive matrix with features, pricing, positioning |
| 5.4 | `/metrics-dashboard` | Amplitude (optional) | "Show me our AARRR funnel" | With MCP: real data. Without: prompts for manual input, still produces dashboard |

---

## Phase 6: Skills — representative coverage

| # | Skill | Test input | Pass criteria |
|---|-------|-----------|---------------|
| 6.1 | `/debate` | "Should we rebuild our monolith as microservices?" | Spawns Champion and Sceptic agents; both argue; moderator synthesises |
| 6.2 | `/learn` | "Learn about the HEART framework for UX metrics" | Researches topic, saves knowledge file to `~/.claude/knowledge/` |
| 6.3 | `/impact-sizing` | "If we reduce churn by 2% on our $10M ARR base" | Produces an Excel workbook (`.xlsx`) with scenario model |
| 6.4 | `/interview-analysis` | Provide 2–3 short interview transcript snippets | Dispatches parallel analysis agents; outputs themes, quotes, recommendations |
| 6.5 | `/design-an-interface` | "A dashboard for tracking OKR progress" | Generates 3+ radically different design concepts |
| 6.6 | `/parallel-prototype` | "A pricing page for a SaaS product" | Generates 3+ structurally different HTML prototypes in parallel |
| 6.7 | `/xlsx` | "Create a spreadsheet with Q1 revenue by region" | Produces a valid `.xlsx` file with formulas |
| 6.8 | `/pptx` | "Create a 5-slide investor pitch deck" | Produces a valid `.pptx` file |
| 6.9 | `/pdf` | Provide a PDF file path | Extracts text/tables from the PDF |
| 6.10 | `/docx` | "Create a one-page project charter" | Produces a valid `.docx` file |
| 6.11 | `/prioritization` | List of 5 features with rough estimates | Outputs a prioritised backlog using RICE or similar framework |
| 6.12 | `/recall` | Run after 6.2 | Returns HEART framework knowledge saved earlier |

---

## Phase 7: Agents — delegation via Task tool

Test each agent by asking Claude to delegate work to it.

| # | Agent | Test prompt | Pass criteria |
|---|-------|------------|---------------|
| 7.1 | `market-research-analyst` | "Research the project management tool market — size, growth, key players" | Returns structured market analysis with sources |
| 7.2 | `cpto-review` | Provide a short PRD or feature spec | Returns executive-level critique with strategic feedback |
| 7.3 | `ux-designer` | "Design the UX for a subscription cancellation flow" | Returns UX recommendations, user flows, or wireframe descriptions |
| 7.4 | `prototype-builder` | "Build a login page with email and Google SSO" | Returns a working HTML prototype |
| 7.5 | `data-brief-analyst` | Provide a CSV or describe a dataset | Returns data analysis with insights and narrative |

---

## Phase 8: Chained workflow — end-to-end

Verify that `/probtoprd` correctly chains through all four stages.

| # | Step | Expected behaviour |
|---|------|--------------------|
| 8.1 | Start | Run `/probtoprd` with "Our trial-to-paid conversion is only 3%" |
| 8.2 | JTBD stage | Claude performs Jobs-to-be-Done analysis and shows job statements |
| 8.3 | OST stage | Claude builds an Opportunity Solution Tree from the jobs |
| 8.4 | User stories stage | Claude generates user stories with acceptance criteria |
| 8.5 | PRD stage | Claude produces a complete PRD document |
| 8.6 | Output | Final PRD references all prior stages and is copy-pasteable to Confluence |

---

## Phase 9: Uninstall and reinstall

| # | Check | Action | Pass criteria |
|---|-------|--------|---------------|
| 9.1 | Uninstall | `claude plugin uninstall ai-pm-kit` | Exits 0, prints success |
| 9.2 | Plugin removed | `claude plugin list` | `ai-pm-kit` does not appear |
| 9.3 | Files removed | `ls ~/.claude/plugins/ai-pm-kit/` 2>/dev/null | Directory does not exist |
| 9.4 | No side effects | Start new Claude Code session, ask for `/jtbd` | Command is not recognised |
| 9.5 | Reinstall from main | `claude plugin install <marketplace-repo>` | Exits 0, plugin appears in list |
| 9.6 | Verify after reinstall | Repeat tests 3.1–3.4 | All pass |

---

## Phase 10: Clean removal

| # | Check | Action | Pass criteria |
|---|-------|--------|---------------|
| 10.1 | Final uninstall | `claude plugin uninstall ai-pm-kit` | Exits 0 |
| 10.2 | No artifacts | Check `~/.claude/plugins/` | No `ai-pm-kit` directory |
| 10.3 | Knowledge files intact | `ls ~/.claude/knowledge/` | Files created by `/learn` still exist (plugin uninstall should not delete user data) |

---

## Appendix A: All 15 Commands

1. `/add-mcp` — Add MCP server instructions
2. `/competitive-analysis` — Competitor analysis (WebSearch)
3. `/experiment` — Experiment design & analysis (Amplitude)
4. `/feature-request` — Feature request triage (RICE)
5. `/jtbd` — Jobs-to-be-Done analysis
6. `/metrics-dashboard` — Metrics dashboard (Amplitude optional)
7. `/opportunity-tree` — Opportunity Solution Tree
8. `/probtoprd` — Problem-to-PRD workflow
9. `/rapid-prototype` — Rapid HTML prototyping
10. `/recall` — Retrieve saved knowledge
11. `/retrospective` — Sprint retrospective
12. `/stakeholder-update` — Stakeholder communications
13. `/standup` — Daily standup summary
14. `/user-stories` — User story generation
15. `/weekly-update` — Weekly team update (Jira + Amplitude)

## Appendix B: All 19 Skills

1. `debate` — Stress-test ideas (Champion vs Sceptic)
2. `design-an-interface` — Multiple radically different designs
3. `docx` — Word document creation/editing
4. `impact-sizing` — ARR impact modelling with Excel output
5. `interview-analysis` — Parallel customer interview analysis
6. `jtbd` — JTBD extraction methodology
7. `learn` — Deep-dive research and knowledge persistence
8. `opportunity-tree` — OST methodology
9. `parallel-prototype` — Parallel HTML prototype generation
10. `pdf` — PDF extraction and creation
11. `pptx` — PowerPoint creation/editing
12. `prd` — PRD template and methodology
13. `prioritization` — Prioritisation frameworks
14. `probtoprd` — Chained discovery workflow
15. `rapid-prototype` — Zero-build HTML prototyping
16. `recall` — Knowledge retrieval
17. `user-stories` — INVEST story methodology
18. `web-browser` — Chrome remote control
19. `xlsx` — Excel spreadsheet creation/editing

## Appendix C: All 5 Agents

1. `cpto-review` — Executive-level PRD/strategy review (Opus)
2. `data-brief-analyst` — Data analysis and narrative insights (Sonnet)
3. `market-research-analyst` — Market research and competitive intelligence (Sonnet)
4. `prototype-builder` — Rapid HTML prototype assembly
5. `ux-designer` — UX design and user experience (Sonnet)
