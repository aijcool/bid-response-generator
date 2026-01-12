---
name: brd
description: "Bid Response Document generation skill. Automates creation of proposal materials from RFP analysis including Requirements Analysis (Excel), Technical Proposals (Word), Architecture Diagrams (Draw.io), Infrastructure Sizing (Excel), and Financial Proposals (Excel). Use when user needs to generate bid/proposal documents or analyze RFP files."
---

# Bid Response Document (BRD) Generation Skill

## Overview

The BRD skill provides a comprehensive framework for generating professional bid response materials. It analyzes source documents (RFP, requirements, technical specs) and produces a complete set of deliverables following industry best practices.

## Prerequisites

This skill requires the following skills to be installed at user level (`~/.claude/skills/`):

| Skill | Purpose | Required For |
|-------|---------|--------------|
| xlsx | Excel creation & editing | Requirements Analysis, Infrastructure, Financial |
| docx | Word document creation | Technical Proposal |
| drawio | Diagram generation | Architecture Diagrams |

### System Dependencies

```bash
# Python
pip install pandas openpyxl python-docx defusedxml pillow

# Node.js
npm install -g docx

# System tools (macOS)
brew install --cask libreoffice
brew install pandoc poppler coreutils

# System tools (Linux)
sudo apt-get install libreoffice pandoc poppler-utils xvfb
```

## Directory Structure

### Input: source/

Place source materials in project root `source/` directory:

```
source/
├── rfp/                         # RFP/tender documents
│   ├── RFP_Document.pdf        # PDF format
│   ├── RFP_Document.docx       # Word format
│   └── RFP_Document.md         # Markdown format
├── requirements/                # Requirements analysis
│   └── requirements_analysis.md
├── technical/                   # Technical proposal
│   └── technical_proposal.md
├── architecture/                # Architecture descriptions
│   ├── overall_solution.md
│   ├── platform_architecture.md
│   ├── deployment_architecture.md
│   └── integration_architecture.md
├── infrastructure/              # Infrastructure sizing
│   └── infrastructure_sizing.md
└── financial/                   # Financial proposal
    └── financial_proposal.md
```

### Output: BRD/

Generated files are saved to `BRD/` directory:

```
BRD/
├── 1_Requirements_Analysis.xlsx
├── 2_Technical_Proposal.docx
├── 3_Architecture_Diagrams/
│   ├── overall_solution.drawio
│   ├── platform_architecture.drawio
│   ├── deployment_architecture.drawio
│   ├── integration_architecture.drawio
│   └── images/
│       └── *.png
├── 4_Infrastructure_Sizing.xlsx
└── 5_Financial_Proposal.xlsx
```

## Document Generation Workflows

### 1. Requirements Analysis (Excel)

**Source**: `source/rfp/`, `source/requirements/`
**Output**: `BRD/1_Requirements_Analysis.xlsx`

#### Sheet Structure

| Sheet | Content |
|-------|---------|
| Executive Summary | Project overview, scope, key metrics |
| Functional Requirements | Feature requirements by category |
| Non-Functional Requirements | Performance, scalability, availability |
| Integration Requirements | External system integrations |
| Security Requirements | Security and compliance requirements |
| Compliance Matrix | Requirement-to-solution mapping |

#### Generation Process

1. Parse RFP document to extract requirements
2. Categorize requirements by type
3. Create Excel workbook with openpyxl
4. Apply formatting:
   - Blue header rows (RGB: 68, 114, 196)
   - White bold font for headers
   - Alternating row colors
   - Thin borders
5. Add formulas for counts and summaries
6. Run recalc.py for formula calculation

#### Markdown Source Format

```markdown
# Requirements Analysis

## 1. Functional Requirements

### 1.1 User Management
| Req ID | Requirement | Priority | Compliance |
|--------|-------------|----------|------------|
| FR-001 | User registration | High | Compliant |
| FR-002 | User authentication | High | Compliant |

### 1.2 Content Management
...
```

### 2. Technical Proposal (Word)

**Source**: `source/technical/`
**Output**: `BRD/2_Technical_Proposal.docx`

#### Document Structure

```
Chapter 1: Executive Summary
Chapter 2: Company Profile
Chapter 3: Solution Architecture
Chapter 4: Implementation Methodology
Chapter 5: System Integration
Chapter 6: Project Management
Chapter 7: Support & Maintenance
```

#### Generation Process

1. Read technical proposal markdown
2. Parse headings, paragraphs, tables, lists
3. Create Word document using docx-js (Node.js)
4. Apply professional styling:
   - Heading styles (Heading 1-4)
   - Normal paragraph style
   - Table formatting
   - Header/footer with page numbers
5. Generate table of contents
6. Export to .docx format

#### Markdown Source Format

```markdown
# Technical Proposal

## Chapter 1: Executive Summary

### 1.1 Introduction

[Introduction text here...]

### 1.2 Solution Overview

| Component | Description |
|-----------|-------------|
| Platform | AI Agent Platform |
| Channels | Web, Mobile, WhatsApp |

## Chapter 2: Company Profile
...
```

### 3. Architecture Diagrams (Draw.io)

**Source**: `source/architecture/`
**Output**: `BRD/3_Architecture_Diagrams/`

#### Diagram Types

| Diagram | Purpose |
|---------|---------|
| overall_solution.drawio | High-level system overview |
| platform_architecture.drawio | Internal platform components |
| deployment_architecture.drawio | Infrastructure and K8s layout |
| integration_architecture.drawio | External system connections |

#### Generation Process

1. Read architecture description markdown
2. Parse components, connections, layers
3. Generate Draw.io XML using Python
4. Apply standard styling:
   - Swimlanes for layers
   - Color-coded components
   - Arrow connections with labels
5. Save as .drawio files
6. Export to PNG (via LibreOffice if available)

#### Markdown Source Format

```markdown
# Overall Solution Architecture

## Layers

### User Layer
- Web Portal
- Mobile App
- WhatsApp Bot

### API Layer
- API Gateway
- Load Balancer

### Application Layer
- Agent Engine
- Knowledge Base
- Analytics Service

## Connections

- Web Portal -> API Gateway
- Mobile App -> API Gateway
- API Gateway -> Agent Engine
```

### 4. Infrastructure Sizing (Excel)

**Source**: `source/infrastructure/`
**Output**: `BRD/4_Infrastructure_Sizing.xlsx`

#### Sheet Structure

| Sheet | Content |
|-------|---------|
| Summary | Total resources, costs overview |
| Production | Production environment specs |
| Non-Production | Dev, Staging, DR specs |
| Procurement | Vendor item list |

#### Generation Process

1. Parse infrastructure requirements
2. Calculate resource allocations
3. Create Excel workbook with openpyxl
4. Add formulas for:
   - Total CPU cores
   - Total memory
   - Total storage
   - Cost calculations
5. Apply professional formatting
6. Run recalc.py

#### Markdown Source Format

```markdown
# Infrastructure Sizing

## Production Environment

### Application Servers
| Component | CPU | Memory | Storage | Qty |
|-----------|-----|--------|---------|-----|
| API Server | 8 | 32GB | 100GB | 3 |
| Agent Engine | 16 | 64GB | 200GB | 2 |

### Database Servers
...
```

### 5. Financial Proposal (Excel)

**Source**: `source/financial/`
**Output**: `BRD/5_Financial_Proposal.xlsx`

#### Sheet Structure

| Sheet | Content |
|-------|---------|
| Executive Summary | Total pricing, highlights |
| One-time Fees | Implementation, setup costs |
| Recurring Fees | Subscriptions, support |
| Payment Schedule | Payment milestones |
| Terms | Terms and conditions |

#### Generation Process

1. Parse financial proposal structure
2. Create Excel workbook with openpyxl
3. Apply financial formatting:
   - Currency format ($#,##0)
   - Percentage format (0.0%)
   - Negative numbers in parentheses
4. Add formulas for totals
5. Apply professional quotation styling
6. Run recalc.py

#### Markdown Source Format

```markdown
# Financial Proposal

## One-time Fees

| Item | Description | Amount |
|------|-------------|--------|
| Implementation | Project setup and configuration | $50,000 |
| Integration | Third-party system integration | $30,000 |
| Training | User and admin training | $10,000 |

## Recurring Fees (Annual)

| Item | Description | Amount |
|------|-------------|--------|
| Platform License | Per-user licensing | $120,000 |
| Support | 24/7 technical support | $36,000 |
```

## Configuration

### .brd-config.json

Create in project root for persistent settings:

```json
{
  "projectName": "Smart Assistant Solution",
  "clientName": "Ministry of Finance",
  "companyName": "Your Company Name",
  "language": "en",
  "currency": "USD",
  "outputDirectory": "BRD",
  "templates": {
    "requirements": "custom_ra_template.md",
    "technical": "custom_tech_template.md"
  }
}
```

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| projectName | string | required | Project name for documents |
| clientName | string | required | Client organization name |
| companyName | string | required | Your company name |
| language | string | "en" | Output language (en/zh/ar) |
| currency | string | "USD" | Currency for financial docs |
| outputDirectory | string | "BRD" | Output directory name |
| templates | object | null | Custom template overrides |

## Multi-Language Support

### Supported Languages

| Code | Language | RTL | Headers Example |
|------|----------|-----|-----------------|
| en | English | No | "Requirements Analysis" |
| zh | Chinese | No | "需求分析" |
| ar | Arabic | Yes | "تحليل المتطلبات" |

### Language-Specific Formatting

- **English**: Standard LTR formatting
- **Chinese**: Chinese fonts, simplified characters
- **Arabic**: RTL layout, Arabic numerals

## Error Handling

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| Skill not found | Required skill missing | Install skill to ~/.claude/skills/ |
| Source not found | source/ directory missing | Create directory structure |
| Parse error | Invalid markdown format | Check source file syntax |
| Permission error | Cannot write output | Check directory permissions |

### Recovery Options

1. **Skip document**: Continue with remaining documents
2. **Retry**: Attempt generation again
3. **Manual completion**: Provide guidance for manual steps

## Best Practices

1. **Organize source files** by category in source/ subdirectories
2. **Use consistent markdown** formatting in source files
3. **Review generated plan** before confirming execution
4. **Customize templates** for specific client requirements
5. **Verify formulas** after Excel generation with recalc.py
6. **Review diagrams** in Draw.io before exporting to PNG

## Code Style

Generated scripts follow these conventions:

- **Python**: Minimal comments, concise code, openpyxl for Excel
- **JavaScript**: ES6+ syntax, async/await, docx-js for Word
- **All outputs**: Professional formatting, consistent styling
