# Bid Response Generator

A Claude Code plugin for automated bid response document generation. Analyzes RFP documents and generates professional proposal materials.

## Features

- **Requirements Analysis** (Excel) - Structured requirement tracking
- **Technical Proposal** (Word) - Professional proposal documents
- **Architecture Diagrams** (Draw.io) - System architecture visualizations
- **Infrastructure Sizing** (Excel) - Resource planning spreadsheets
- **Financial Proposal** (Excel) - Pricing and cost breakdowns

## Prerequisites

### Required Skills

This plugin requires the following skills installed at user level (`~/.claude/skills/`):

| Skill | Purpose |
|-------|---------|
| xlsx | Excel creation and editing |
| docx | Word document creation |
| drawio | Architecture diagram generation |

### System Dependencies

```bash
# Python
pip install pandas openpyxl python-docx defusedxml pillow

# Node.js
npm install -g docx

# macOS
brew install --cask libreoffice
brew install pandoc poppler coreutils

# Linux
sudo apt-get install libreoffice pandoc poppler-utils xvfb
```

## Installation

### From GitHub

```bash
# Add marketplace
/plugin marketplace add your-username/bid-response-generator

# Install plugin
/plugin install bid-response-generator
```

### Local Development

```bash
# Run with local plugin
claude --plugin-dir ./bid-response-generator
```

## Usage

### Quick Start

1. Create source directory structure in your project:

```bash
mkdir -p source/{rfp,requirements,technical,architecture,infrastructure,financial}
```

2. Place your source materials in the appropriate directories

3. Run the command:

```bash
/brd
```

4. Review the generated plan and confirm to proceed

5. Find outputs in `BRD/` directory

### Directory Structure

```
your-project/
├── source/                      # Input: Your source materials
│   ├── rfp/                     # RFP documents (PDF/Word/Markdown)
│   ├── requirements/            # Requirements analysis source
│   ├── technical/               # Technical proposal source
│   ├── architecture/            # Architecture descriptions
│   ├── infrastructure/          # Infrastructure sizing source
│   └── financial/               # Financial proposal source
│
├── BRD/                         # Output: Generated documents
│   ├── 1_Requirements_Analysis.xlsx
│   ├── 2_Technical_Proposal.docx
│   ├── 3_Architecture_Diagrams/
│   ├── 4_Infrastructure_Sizing.xlsx
│   └── 5_Financial_Proposal.xlsx
│
└── .brd-config.json             # Configuration (optional)
```

### Command Options

```bash
/brd                    # Interactive generation
/brd --plan-only        # Generate plan without executing
/brd --check            # Verify dependencies
/brd --lang=zh          # Set output language (en/zh/ar)
```

### Configuration

Create `.brd-config.json` in project root:

```json
{
  "projectName": "Your Project Name",
  "clientName": "Client Organization",
  "companyName": "Your Company",
  "language": "en",
  "currency": "USD",
  "outputDirectory": "BRD"
}
```

## Supported Formats

### Input Formats

| Format | Extension | Support |
|--------|-----------|---------|
| PDF | .pdf | Full |
| Word | .docx | Full |
| Markdown | .md | Full |

### Output Formats

| Document | Format |
|----------|--------|
| Requirements Analysis | Excel (.xlsx) |
| Technical Proposal | Word (.docx) |
| Architecture Diagrams | Draw.io (.drawio) + PNG |
| Infrastructure Sizing | Excel (.xlsx) |
| Financial Proposal | Excel (.xlsx) |

## Multi-Language Support

| Language | Code | RTL |
|----------|------|-----|
| English | en | No |
| Chinese | zh | No |
| Arabic | ar | Yes |

## Templates

The plugin includes professional templates for all document types. Templates can be customized by creating override files in the `templates` configuration.

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting pull requests.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.
