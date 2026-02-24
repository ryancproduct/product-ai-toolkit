---
name: impact-sizing
description: "Guide users through SafetyCulture's impact sizing methodology to translate product hypotheses into ARR estimates with Excel workbook output"
---

# Impact Sizing Skill

**Purpose**: Guide users through SafetyCulture's impact sizing methodology to translate product hypotheses into ARR estimates, then generate a complete Excel workbook with all calculations.

## When to Use This Skill
- When a PRD is in the PROPOSED stage
- Before significant Product & Design effort has been invested
- When comparing product opportunities for prioritisation
- When you need to justify why something should be built (or not)

---

## Data Collection Approach

This skill collects data through a **flexible, multi-format approach**:

### Accepted Input Methods
1. **Direct answers** - User types numbers or descriptions in response to questions
2. **File uploads** - CSV exports, Excel files, or screenshots from Salesforce/Twine/Productboard
3. **Pasted text** - Copy/paste from Confluence tables, Slack threads, or reports
4. **Partial data** - Work with whatever data is available; estimate or skip missing sections

### How Claude Handles Different Formats

**For Salesforce exports (CSV/Excel):**
- Claude will read the file and extract relevant columns (Account Name, ARR, Closed Lost Reason, etc.)
- Filter for feature-related keywords automatically
- Sum values and identify relevant accounts

**For Confluence/Notion tables:**
- User can paste the table text directly
- Claude will parse the structure and extract data

**For Twine/Slack:**
- User provides account names and ARR values mentioned
- Claude will help structure the data

**For screenshots:**
- Claude can read text from screenshots if data isn't exportable
- User should confirm extracted values

### When Data Isn't Available
If the user doesn't have access to certain data sources, Claude should:
1. Note the gap in the assumptions sheet
2. Provide a conservative estimate based on available data
3. Mark confidence as "Low" for that category
4. Continue with the sizing using what's available

---

## Phase 1: Discovery Questions

When this skill is invoked, Claude MUST ask the following questions to gather inputs. Use the AskUserQuestion tool with clear, structured questions.

### 1.1 Core Hypothesis
Ask the user to provide their hypothesis in the standard format:
```
"By <making a change> we will see <metric> <increase/decrease/stay same> because <customer problem solved>"
```

The metric should be one of the Big 5 metrics:
- **Bookings** (GTM)
- **Pipeline Created** (GTM)
- **Gross Dollar Retention / GDR** (GTM)
- **Users** (Product)
- **MAU** (Product)

### 1.2 Feature Details
- **Feature name**: What is the feature or capability being sized?
- **Product area**: Which product area does this belong to? (e.g., Capture, Reporting, Assets, Training, etc.)
- **Is this new functionality or enhancing existing?**: Determines whether to use top-down or bottom-up TAM/SAM/SOM

### 1.3 Strategic Focus
Confirm alignment with SafetyCulture's strategic focus:
- **Priority Industries**: Manufacturing, Retail + QSR, Transport & Logistics, Hospitality
- **Priority Geographies**: USA, UK&I, ANZ, Canada
- **Customer Segment**: Enterprise+ (>1,000 employees), Small & Medium (>250 employees)

### 1.4 Data Sources
Ask what data the user has access to. For each source, explain how to get the data:

**Salesforce - Closed Lost/Won:**
> Export from [Global Closed Sales Report](https://safetyculture.lightning.force.com/lightning/r/Report/00OOl000005GObNMAW/view)
> - Click "Export" → "Details Only" → CSV
> - Or just tell me the feature-related closed lost value if you've already looked it up

**Productboard - Feature Requests:**
> Go to your feature in [Productboard](https://safetyculture.productboard.com) and note:
> - Number of requests for this specific feature
> - Total requests in the product area (for calculating proportion)

**Twine - Churn Risk:**
> Search [Twine](https://app.twine.so) for keywords related to your feature
> - List customer names and their ARR from accounts expressing frustration
> - Or upload the Twine report export

**Churned Customers:**
> Check the [FY25 Product deep-dive](https://docs.google.com/presentation/d/1oPtHMFxzdQV_0g64xigmAkDbO8UBiNaz_1uZAi5S08s/edit) or churn spreadsheet
> - Find customers who churned citing this capability
> - List their names and ARR values

**Current Pipeline:**
> Any deals currently in pipeline that depend on this feature?
> - Usually surfaced directly by GTM team

---

## Phase 1.5: Processing Uploaded Data

When the user uploads files or pastes data, Claude should process it as follows:

### Salesforce CSV/Excel Exports

**Expected columns to look for:**
- `Account Name` or `Opportunity Name`
- `Stage` (filter for "Closed Lost" or "Closed Won")
- `Closed Lost Reason` or `Closed Lost/Churn Reason`
- `Additional Details` (search for feature keywords here)
- `Reporting Total Price (converted)` or `Amount` or `ARR`

**Processing steps:**
1. Read the file using pandas
2. Filter Stage = "Closed Lost" and Reason contains "Product"
3. Search Additional Details for feature-related keywords
4. Sum the ARR/Amount column for matching rows
5. Present findings to user for confirmation

**Example code Claude should use:**
```python
import pandas as pd

df = pd.read_csv('salesforce_export.csv')  # or read_excel

# Filter for product-related closed lost
closed_lost = df[
    (df['Stage'].str.contains('Closed Lost', case=False, na=False)) &
    (df['Closed Lost Reason'].str.contains('Product', case=False, na=False))
]

# Search for feature keywords
keywords = ['asset', 'multi-asset', 'multiple assets']  # customize per feature
feature_related = closed_lost[
    closed_lost['Additional Details'].str.contains('|'.join(keywords), case=False, na=False)
]

total_value = feature_related['Reporting Total Price (converted)'].sum()
print(f"Found {len(feature_related)} closed-lost deals totaling ${total_value:,.0f}")
```

### Twine Exports

**Expected format:** Usually JSON or CSV with call summaries
**Look for:** Customer name, ARR (may need to cross-reference with Salesforce), key quotes about frustration

### Productboard Data

**Expected format:** Feature request counts, often from the Insights/Trends view
**Look for:** Total request count for the feature, total requests in product area

### Pasted Confluence/Slack Text

**Processing approach:**
1. Look for table structures (pipe-delimited or tab-delimited)
2. Extract customer names and numeric values
3. Ask user to confirm which column is ARR

---

## Phase 2: TAM/SAM/SOM Estimation

Based on whether this is NEW functionality or ENHANCEMENT to existing:

### For NEW Functionality (Top-Down Approach)
Use AI (Perplexity/Claude) to estimate market size with prompts like:

**TAM Prompt Template:**
```
Estimate the Total Addressable Market (TAM) for a software tool that [DESCRIBE CAPABILITY]:
- TAM methodology: Top-down from global spend or relevant software categories
- List all key assumptions and provide sensitivity ranges (low / base / high)
- Output: Provide TAM in AUD (annual), with low/base/high scenarios
- Sources & citations: Use recent sources, cite at least 5 reputable sources
```

**SAM Prompt Template (follow-up):**
```
Turn this into a SAM estimate with the following focus areas:
- Industry focus: manufacturing, retail, QSR, and hospitality (but don't exclude others)
- Geographical focus: United States, Canada, APAC, and English-speaking EMEA
- Customer focus: Enterprise customers, but don't preclude SMBs
- List all key assumptions and provide sensitivity ranges (low / base / high)
- Output: Provide SAM in AUD (annual), with low/base/high scenarios
```

**SOM Calculation:**
- Estimate target customers in regions/industries
- Apply realistic capture rate (typically 5%)
- Apply average seat count (typically 5 seats)
- Apply seat price ($24/month or $288/year standard, or $367/year for enterprise blend)
- Apply win rate (23%) and deal cycle adjustment

### For ENHANCEMENT (Bottom-Up Approach)
Use internal data sources:

**TAM**: Use Industry Playbooks + All Customers Report to estimate total addressable orgs
**SAM**: Use Productboard feature requests as % of total requests in that product area
**SOM**: Apply 5% capture rate × average seats × price × win rate

---

## Phase 3: Churn Analysis

### 3.1 Churned Customers
Search for customers who churned specifically due to this capability missing:
- **Data Source**: [FY25 Product deep-dive spreadsheet](https://docs.google.com/presentation/d/1oPtHMFxzdQV_0g64xigmAkDbO8UBiNaz_1uZAi5S08s/edit)
- **Data Source**: [Global Q3 Churn/CL Renewals Report](Salesforce)
- Look for keywords related to the feature in churn reasons
- Sum the ARR of churned accounts

### 3.2 Tangible Churn Risk
Identify customers at risk of churning if capability isn't delivered:
- **Data Source**: Twine - search for feature-related frustration
- **Data Source**: #account-risks Slack channel
- Cross-reference with Salesforce account ARR values

### 3.3 Retention Uplift
Calculate expected year-on-year churn reduction:
```
Retention Uplift = (Churned Customers ARR / Total FY25 Churn) × FY26 GDR Target
```
- FY25 Total Company Churn: ~$19.6M
- FY26 GDR uplift target: 2% reduction

---

## Phase 4: Opportunities Analysis

### 4.1 Closed Won Opportunity (from Closed Lost data)
- **Data Source**: [Global Closed Sales Report](Salesforce - last 2 fiscal years)
- Filter: Stage = "Closed Lost", Reason = Product-related
- Search Additional Details for feature-related keywords
- Calculate: Feature-related Closed Lost / Total Closed Deals × FY26 Bookings Target ($63M)

### 4.2 Current Opportunities
- Any pipeline opportunities specifically dependent on this feature
- Usually surfaced directly by GTM team

### 4.3 Other Conversion Opportunities
- Free-to-paid conversion impact
- Relevant for features in onboarding or early user journey

---

## Phase 5: Generate Excel Workbook

After gathering all inputs, generate an Excel workbook with the following structure:

### Sheet 1: Summary
| Category | Description | ARR Impact |
|----------|-------------|------------|
| TAM/SAM/SOM (Top-down) | [SOM result] | $XXX |
| TAM/SAM/SOM (Bottom-up) | [SOM result] | $XXX |
| Churned Customers | [Sum of churned ARR] | $XXX |
| Tangible Churn Risk | [Sum of at-risk ARR] | $XXX |
| Retention Uplift | [Calculated uplift] | $XXX |
| Closed Won Opportunity | [Bookings uplift] | $XXX |
| Current Opportunities | [Pipeline value] | $XXX |
| **TOTAL ARR IMPACT** | | **$XXX** |

### Sheet 2: Detailed Calculations
Include all inputs, assumptions, formulas with cell references, and source citations.

### Sheet 3: Data Sources
Table of all data sources used with links and access dates.

---

## Key Reference Data (SafetyCulture FY26)

| Metric | Value | Source |
|--------|-------|--------|
| ARR Target FY26 | $250M AUD | SafetyCulture Strategy |
| Net Add Target FY26 | $50M | SafetyCulture Strategy |
| New Bookings Target FY26 | $63M | SafetyCulture Strategy |
| Closed Won Rate | 23% | Global Closed Sales Report |
| Average Deal Cycle | 89 days | Global Closed Sales Report |
| Average Seat Price (Standard) | $24/month ($288/year) | Pricing |
| Average Seat Price (Enterprise blend) | $367/year | All Customers Report |
| FY25 Total Company Churn | $19.6M | FY25 Product deep-dive |
| FY26 GDR Uplift Target | 2% reduction | SafetyCulture Strategy |
| 100M Users Target | By 2032 | SafetyCulture Strategy |

---

## Key Resource Links

| Description | Link |
|-------------|------|
| Average seat sizes by industry | [Google Slides](https://docs.google.com/presentation/d/1hoVbrNbzF2t2AB6lOQyvXvyqM6DUHnC3YA3euhtUQwA/edit?slide=id.g34871649d76_0_159) |
| Global Closed Sales Report | [Salesforce Report](https://safetyculture.lightning.force.com/lightning/r/Report/00OOl000005GObNMAW/view) |
| All Customers Report | [Tableau](https://prod-useastb.online.tableau.com/#/site/safetyculture/views/AllCustomersReport/SCOrganisationDetails) |
| FY25 Product Churn Deep-dive | [Google Slides](https://docs.google.com/presentation/d/1oPtHMFxzdQV_0g64xigmAkDbO8UBiNaz_1uZAi5S08s/edit) |
| Global Q3 Churn/CL Renewals | [Salesforce Report](Salesforce) |
| Industry Playbooks | Internal Google Drive |

---

## Excel Generation Instructions

When generating the Excel file, Claude should:

1. **Use the xlsx skill** for proper Excel creation
2. **Include formulas** (not hardcoded calculations) so the workbook is dynamic
3. **Apply proper formatting**:
   - Blue text for user inputs
   - Black text for formulas
   - Yellow highlight for key assumptions
   - Currency format for ARR figures
4. **Include source citations** in adjacent cells
5. **Add a hypothesis header** at the top of the main sheet
6. **Calculate quarterly and annualized figures** where applicable
7. **Run recalc.py** to ensure all formulas compute correctly

---

## Example Output

For a feature like "Multiple Assets in Inspections", the final impact sizing came to **$800K ARR** broken down as:
- Top-down SOM: $750K
- Bottom-up SOM: $135K
- Churned Customers: $25K
- Tangible Churn Risk: $570K
- Retention Uplift: $24K
- Closed Won Opportunity: $49K

(Note: Not all categories are additive - some overlap. Use judgment on which to include in total.)

---

## Workflow Summary

```
1. User invokes /impact-sizing skill
2. Claude asks discovery questions (hypothesis, feature details, strategic alignment)
3. Claude guides TAM/SAM/SOM estimation (top-down or bottom-up based on feature type)
4. Claude asks for churn data inputs
5. Claude asks for opportunities data inputs
6. Claude generates comprehensive Excel workbook
7. Claude provides summary and key findings
```

## Important Notes

- **Cite all data sources** - transparency is critical
- **Make assumptions explicit** - it's okay to estimate, just be clear about it
- **Apply confidence levels** when appropriate (High/Medium/Low)
- **Sanity check results** - if a number seems unrealistic, revisit assumptions
- **The goal isn't perfection** - it's consistent comparison across opportunities
