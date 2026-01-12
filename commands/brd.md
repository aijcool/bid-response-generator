---
description: Generate bid response documents from RFP analysis. Creates Requirements Analysis (Excel), Technical Proposals (Word), Architecture Diagrams (Draw.io), Infrastructure Sizing (Excel), and Financial Proposals (Excel).
argument-hint: [--plan-only] [--check] [--lang=en|zh|ar]
---

# BRD - Bid Response Document Generator

Generate professional bid response materials from source documents in the `source/` directory.

## Command Options

- `/brd` - Analyze source files and generate all documents interactively
- `/brd --plan-only` - Generate plan without executing
- `/brd --check` - Verify dependencies and configuration
- `/brd --lang=zh` - Set output language (en/zh/ar)

## Execution Workflow

### Step 1: Dependency Check

First, verify required skills are available at user level (`~/.claude/skills/`):

1. **xlsx skill** - For Excel creation (Requirements Analysis, Infrastructure, Financial)
2. **docx skill** - For Word document creation (Technical Proposal)
3. **drawio skill** - For architecture diagram generation

If any skill is missing, display:

```
BRD Plugin Dependency Check
═══════════════════════════════════════

Required Skills:
✗ xlsx - NOT FOUND
  Install from: ~/.claude/skills/xlsx/

✓ docx - Available
✓ drawio - Available

Please install missing skills before proceeding.
```

If `--check` flag is provided, stop after showing dependency status.

### Step 2: Source Directory Discovery

Search for source materials in `source/` directory:

```
source/
├── rfp/           # RFP/tender documents (PDF/Word/Markdown)
├── requirements/  # Requirements analysis source
├── technical/     # Technical proposal source
├── architecture/  # Architecture description source
├── infrastructure/# Infrastructure sizing source
└── financial/     # Financial proposal source
```

**Supported formats**: PDF (.pdf), Word (.docx), Markdown (.md)

If `source/` directory doesn't exist, prompt user:

```
Source directory not found.

Would you like to create the directory structure?
This will create: source/{rfp,requirements,technical,architecture,infrastructure,financial}/

[Y/n]
```

### Step 3: Configuration Check

Look for `.brd-config.json` in project root. If not found, prompt for configuration:

```
BRD Configuration Setup
═══════════════════════════════════════

Project Name: [required]
Client Name: [required]
Your Company Name: [required]
Language (en/zh/ar): [default: en]
Currency (USD/SAR/CNY/EUR): [default: USD]

Save configuration? [Y/n]
```

Configuration file format:

```json
{
  "projectName": "Smart Assistant Solution",
  "clientName": "Ministry of Finance",
  "companyName": "Your Company",
  "language": "en",
  "currency": "USD",
  "outputDirectory": "BRD"
}
```

### Step 4: Source File Analysis

Analyze all files in `source/` directory:

1. **RFP Analysis** (source/rfp/)
   - Extract project information
   - Identify requirements (functional, non-functional)
   - List integration requirements
   - Determine scope and deliverables

2. **Content Analysis** (other source directories)
   - Parse markdown structure
   - Count sections and subsections
   - Identify tables, lists, diagrams
   - Estimate output size

### Step 5: Generate Plan

Present detailed generation plan:

```
═══════════════════════════════════════════════════════════════
                    BRD GENERATION PLAN
═══════════════════════════════════════════════════════════════

Project: {{projectName}}
Client: {{clientName}}
Language: {{language}}

SOURCE FILES DETECTED:
───────────────────────────────────────────────────────────────
Directory          Files Found    Status
───────────────────────────────────────────────────────────────
source/rfp/        2 files        ✓ Ready
source/requirements/ 1 file       ✓ Ready
source/technical/  1 file         ✓ Ready
source/architecture/ 4 files      ✓ Ready
source/infrastructure/ 1 file     ✓ Ready
source/financial/  1 file         ✓ Ready
───────────────────────────────────────────────────────────────

DOCUMENTS TO GENERATE:
───────────────────────────────────────────────────────────────

1. Requirements Analysis (Excel)
   ├── Source: source/requirements/, source/rfp/
   ├── Sheets: ~8 categorized requirement sheets
   └── Output: BRD/1_Requirements_Analysis.xlsx

2. Technical Proposal (Word)
   ├── Source: source/technical/
   ├── Chapters: 7 standard sections
   └── Output: BRD/2_Technical_Proposal.docx

3. Architecture Diagrams (Draw.io + PNG)
   ├── Source: source/architecture/
   ├── Diagrams: 4+ architecture diagrams
   └── Output: BRD/3_Architecture_Diagrams/

4. Infrastructure Sizing (Excel)
   ├── Source: source/infrastructure/
   ├── Sheets: Production, Non-Production, Summary
   └── Output: BRD/4_Infrastructure_Sizing.xlsx

5. Financial Proposal (Excel)
   ├── Source: source/financial/
   ├── Sheets: Pricing, Cost Breakdown, Terms
   └── Output: BRD/5_Financial_Proposal.xlsx

═══════════════════════════════════════════════════════════════

Proceed with generation? [Y/n]
```

If `--plan-only` flag is set, stop here.

### Step 6: Execute Generation

For each document type, use the appropriate skill:

#### 6.1 Requirements Analysis (Excel)

1. Read the xlsx SKILL.md completely
2. Parse requirements from source files
3. Create Python script using openpyxl
4. Structure requirements into categorized sheets:
   - Executive Summary
   - Functional Requirements
   - Non-Functional Requirements
   - Integration Requirements
   - Security Requirements
   - Compliance Matrix
5. Apply professional formatting (blue headers, borders, alternating rows)
6. Run recalc.py if formulas present
7. Save to BRD/1_Requirements_Analysis.xlsx

#### 6.2 Technical Proposal (Word)

1. Read the docx SKILL.md completely
2. Parse markdown source content
3. Create JavaScript file using docx-js
4. Generate document structure:
   - Title Page
   - Table of Contents
   - Executive Summary
   - Company Profile
   - Solution Architecture
   - Implementation Methodology
   - Project Management
   - Support & Maintenance
5. Apply professional styling (headers, footers, page numbers)
6. Save to BRD/2_Technical_Proposal.docx

#### 6.3 Architecture Diagrams (Draw.io)

1. Read the drawio SKILL.md completely
2. For each architecture file in source/architecture/:
   - Parse structure and components
   - Generate Draw.io XML using Python
   - Create shapes, connections, swimlanes
3. Save .drawio files to BRD/3_Architecture_Diagrams/
4. Export to PNG (if LibreOffice available)
5. Create images/ subdirectory for PNGs

#### 6.4 Infrastructure Sizing (Excel)

1. Read the xlsx SKILL.md completely
2. Parse infrastructure requirements
3. Create Python script using openpyxl
4. Generate sheets:
   - Summary (total costs, resources)
   - Production Environment (servers, storage, network)
   - Non-Production Environment (dev, staging, DR)
   - Procurement List (vendor items)
5. Apply formulas for calculations
6. Run recalc.py
7. Save to BRD/4_Infrastructure_Sizing.xlsx

#### 6.5 Financial Proposal (Excel)

1. Read the xlsx SKILL.md completely
2. Parse pricing structure
3. Create Python script using openpyxl
4. Generate sheets:
   - Executive Summary (total pricing)
   - One-time Fees (implementation, setup)
   - Recurring Fees (subscriptions, support)
   - Payment Schedule
   - Terms & Conditions
5. Apply formulas for totals and subtotals
6. Use professional quotation formatting
7. Run recalc.py
8. Save to BRD/5_Financial_Proposal.xlsx

### Step 7: Summary Report

After generation completes:

```
═══════════════════════════════════════════════════════════════
                  BRD GENERATION COMPLETE
═══════════════════════════════════════════════════════════════

Output Directory: BRD/

Generated Documents:
───────────────────────────────────────────────────────────────
✓ 1_Requirements_Analysis.xlsx     (8 sheets, 45 requirements)
✓ 2_Technical_Proposal.docx        (7 chapters, ~50 pages)
✓ 3_Architecture_Diagrams/
  ├── overall_solution.drawio
  ├── platform_architecture.drawio
  ├── deployment_architecture.drawio
  ├── integration_architecture.drawio
  └── images/ (4 PNG files)
✓ 4_Infrastructure_Sizing.xlsx     (4 sheets)
✓ 5_Financial_Proposal.xlsx        (5 sheets)
───────────────────────────────────────────────────────────────

NEXT STEPS:
1. Review generated documents for accuracy
2. Customize company-specific content
3. Add detailed technical specifications
4. Finalize pricing in Financial Proposal
5. Embed architecture PNGs into Technical Proposal

═══════════════════════════════════════════════════════════════
```

## Error Handling

If generation fails:
1. Log error with context
2. Offer to retry specific step
3. Preserve partially generated files
4. Provide guidance on manual completion

```
Error: Failed to generate Technical Proposal

Reason: docx skill not available
Location: Step 6.2

Options:
[1] Skip this document and continue
[2] Retry after installing docx skill
[3] Cancel generation

Choice:
```

## Multi-Language Support

The plugin supports three languages:

| Language | Code | Document Headers | RTL Support |
|----------|------|-----------------|-------------|
| English  | en   | Default         | No          |
| Chinese  | zh   | 中文标题         | No          |
| Arabic   | ar   | العربية          | Yes         |

Set language via:
- Command flag: `/brd --lang=zh`
- Config file: `"language": "zh"` in .brd-config.json
