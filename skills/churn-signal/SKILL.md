---
name: churn-signal
description: Assess churn or expansion risk for a customer account or segment by pulling usage data, support sentiment, and engagement signals. Produces an account health rating and recommended intervention. Use before QBRs, renewal conversations, or proactive CS outreach.
---

# Churn Signal Skill

Assess account health for a specific customer or a segment of customers. Pulls quantitative usage signals and qualitative sentiment signals, combines them into a health score, and recommends what to do.

## Input: $ARGUMENTS

Accepts:
- `/churn-signal [account name]` — Health check for a specific account
- `/churn-signal [segment]` — e.g., "enterprise accounts in manufacturing" or "trial users from last quarter"
- `/churn-signal` — Will ask interactively

If no input, ask:
> "Which account or segment do you want to assess? You can name a specific customer, a plan tier, an industry, or a cohort."

---

## Phase 1: Signal Gathering

Pull from all available sources in parallel. Never block on a failing source.

### Usage Signals (Amplitude)
- MAU/WAU trend over last 90 days — growing, flat, or declining?
- Feature adoption breadth — using 1 feature or many?
- Login frequency vs 90-day average
- Any sudden drop-off events (when did it happen?)
- Power users — how many, trending up or down?

### Sentiment Signals (Intercom)
- Open or unresolved support tickets
- Ticket volume trend — more or fewer issues recently?
- Sentiment in recent conversations — frustrated, neutral, satisfied?
- Any explicit churn signals ("we're evaluating alternatives", "our contract is up")

### Internal Signals (Glean / Slack / Jira)
- Any CS or sales notes about this account
- Known commitments that haven't been delivered
- Competitive mentions
- Recent escalations

### Contractual Context (if available)
- Renewal date (if known from any source)
- ARR value
- Plan tier

---

## Phase 2: Score Health

Score each signal dimension on a 1-5 scale:
- **5** = Strong positive signal
- **3** = Neutral / unclear
- **1** = Strong negative signal

| Dimension | Score | Evidence |
|---|---|---|
| Usage trend | | |
| Feature adoption breadth | | |
| Support sentiment | | |
| Engagement recency | | |
| Unresolved commitments | | |

**Overall health**: Average the scores → map to:
- **4.0-5.0** → 🟢 Healthy
- **3.0-3.9** → 🟡 Monitor
- **2.0-2.9** → 🟠 At Risk
- **1.0-1.9** → 🔴 Critical

---

## Phase 3: Output

```markdown
# Account Health: [Account Name / Segment]
**Date**: [Today] | **Analyst**: AI PM Kit | **Confidence**: [High/Medium/Low]

---

## Health Score: [Score/5] — [🟢 Healthy / 🟡 Monitor / 🟠 At Risk / 🔴 Critical]

---

## Signal Summary

| Dimension | Score | Key Finding |
|---|---|---|
| Usage trend | [1-5] | [e.g., MAU down 23% in last 30 days] |
| Feature breadth | [1-5] | [e.g., Only using 1 of 4 core modules] |
| Support sentiment | [1-5] | [e.g., 3 open tickets, one flagged frustrated] |
| Engagement recency | [1-5] | [e.g., Last login 18 days ago] |
| Commitments | [1-5] | [e.g., Pending feature request from Dec] |

---

## Top Risk Factors
1. [Most concerning signal — why it matters]
2. [Second risk]
3. [Third risk, if applicable]

## Positive Signals
- [What's working for this account]
- [Any green flags that offset risk]

---

## Recommended Intervention

**Priority**: Immediate / This week / This quarter / None needed

**Recommended action**: [Specific action — not generic advice]
- [e.g., "CS to schedule a proactive call this week — reference the usage decline and ask about their Q2 plans"]
- [e.g., "PM to follow up on the outstanding feature request — it was raised 90 days ago"]
- [e.g., "Share the new Reporting module release notes — they're power users of reporting but haven't adopted the new exports"]

**Owner**: [CS / PM / Sales / Auto-communication]

---

## Data Gaps
- [Sources that returned no data]
- [Information that would sharpen this assessment]
```

---

## Bulk Mode (Segments)

If analysing a segment rather than a single account:
- Pull the top 10-20 accounts by ARR in the segment
- Score each one using the same framework
- Produce a ranked table from highest to lowest risk
- Highlight the top 3 that need immediate intervention

---

## Principles

- **Don't manufacture precision.** If you only have usage data and no sentiment, say the score is based on usage only.
- **Name the specific risk.** "At risk" without explanation is useless. Say exactly what's concerning.
- **Recommend something actionable.** The output should tell a CS or PM what to do tomorrow, not just how bad the situation is.
- **Anonymise in shared outputs.** If this brief will be shared broadly, replace account names with "Account A (Enterprise, Manufacturing)" style labels.
