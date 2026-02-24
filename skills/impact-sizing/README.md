# Impact Sizing Skill for Claude

A custom skill that guides you through SafetyCulture's impact sizing methodology and generates comprehensive Excel workbooks.

## What This Skill Does

When you invoke `/impact-sizing`, Claude will:

1. **Ask discovery questions** about your feature hypothesis, target metrics, and strategic alignment
2. **Guide TAM/SAM/SOM estimation** using either top-down (market data) or bottom-up (internal data) approaches
3. **Collect churn data** including churned customers, at-risk accounts, and retention uplift calculations
4. **Analyze opportunities** from closed-lost deals and current pipeline
5. **Generate a complete Excel workbook** with all calculations, formulas, and source citations

## Installation

### Option 1: Drop into your project's .skills folder

1. Copy this entire `impact-sizing-skill` folder to your project:
   ```
   your-project/
   └── .skills/
       └── skills/
           └── impact-sizing/
               ├── SKILL.md
               ├── generate_impact_sizing.py
               └── README.md
   ```

2. The skill will now be available when working in that project

### Option 2: Add to your global Claude skills

1. Copy this folder to your Claude Code global skills directory:
   - **macOS**: `~/.claude/skills/impact-sizing/`
   - **Linux**: `~/.claude/skills/impact-sizing/`

2. The skill will be available in all Claude Code sessions

## Usage

### Invoking the skill

Simply type `/impact-sizing` in your Claude conversation, or ask Claude to help you with impact sizing.

### Example conversation

```
You: I need to size the impact of adding batch export functionality to reports

Claude: [Invokes impact-sizing skill and asks clarifying questions]
- What's your hypothesis for this feature?
- Is this new functionality or enhancing existing?
- What data sources do you have access to?

You: [Provides answers]

Claude: [Guides you through TAM/SAM/SOM, churn, and opportunities analysis]

Claude: [Generates Excel workbook with all calculations]
```

## How Data Collection Works

The skill is **flexible about how you provide data**. You can:

### Option 1: Type answers directly
Claude asks specific questions, you provide the numbers:
```
Claude: How much ARR from churned customers cited this feature as their reason?
You: About $25K - two customers: ILG ($24.6K) and SmallCo ($400)
```

### Option 2: Upload files
Export from Salesforce, Twine, or Productboard and upload:
```
You: [Uploads salesforce_closed_lost_export.csv]
Claude: I found 15 closed-lost deals mentioning "batch export" totaling $87K.
        Does this look right?
```

### Option 3: Paste text
Copy a table from Confluence or Slack:
```
You: Here's what I found in the churn spreadsheet:
     | Customer | ARR | Reason |
     | Acme Co | $15,000 | Missing batch export |
     | BigCorp | $42,000 | Export limitations |

Claude: Got it - $57K in churn attributed to this feature.
```

### Option 4: Provide partial data
Don't have everything? That's fine:
```
You: I don't have access to the churn data, but I have the Salesforce export
Claude: No problem - I'll mark churn as "Unknown" with low confidence and
        proceed with what we have.
```

### Where to get the data

| Data Type | Source | How to Export |
|-----------|--------|---------------|
| Closed Lost deals | [Global Closed Sales Report](https://safetyculture.lightning.force.com/lightning/r/Report/00OOl000005GObNMAW/view) | Export → Details Only → CSV |
| Feature requests | [Productboard](https://safetyculture.productboard.com) | Note the counts from Insights |
| Churn risk | [Twine](https://app.twine.so) | Search keywords, note accounts |
| Churned customers | [FY25 deep-dive](https://docs.google.com/presentation/d/1oPtHMFxzdQV_0g64xigmAkDbO8UBiNaz_1uZAi5S08s/edit) | Copy relevant rows |
| Pipeline | GTM team | Ask your Sales partners |

## Files Included

| File | Purpose |
|------|---------|
| `SKILL.md` | Skill instructions for Claude - methodology, questions, and workflow |
| `generate_impact_sizing.py` | Python script to generate Excel workbooks |
| `README.md` | This file |

## Generated Excel Workbook Structure

The skill generates workbooks with these sheets:

1. **Summary** - Overview of all impact categories and total ARR
2. **TAM_SAM_SOM** - Detailed market sizing calculations (top-down and bottom-up)
3. **Churn_Analysis** - Churned customers, at-risk accounts, retention uplift
4. **Opportunities** - Closed-lost analysis and current pipeline
5. **Data_Sources** - All sources and links used
6. **Assumptions** - Key assumptions with rationale and confidence levels

## Key SafetyCulture Reference Data (FY26)

| Metric | Value |
|--------|-------|
| ARR Target | $250M AUD |
| Net Add Target | $50M |
| New Bookings Target | $63M |
| Closed Won Rate | 23% |
| Average Deal Cycle | 89 days |
| Standard Seat Price | $24/month ($288/year) |
| Enterprise Seat Price | $367/year (blended) |
| FY25 Total Churn | $19.6M |
| GDR Uplift Target | 2% reduction |

## Contributing

To improve this skill:

1. Edit `SKILL.md` to update the methodology or add new approaches
2. Edit `generate_impact_sizing.py` to modify the Excel output format
3. Test by invoking the skill and generating sample workbooks

## Support

For questions about the impact sizing methodology, refer to:
- [Impact Sizing Playbook](https://www.notion.so/From-Hypothesis-to-ARR-The-Impact-Sizing-Playbook) (internal)
- Your Product Analytics or Data team
