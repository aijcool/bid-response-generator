# Bid Response Generator

A Claude Code skill for automated bid response document generation. Analyzes RFP documents and generates professional proposal materials.

## Features

- **Requirements Analysis** (Excel) - Structured requirement tracking with compliance matrix
- **Technical Proposal** (Word) - Professional proposal documents with TOC
- **Architecture Diagrams** (Draw.io) - System architecture visualizations with PNG export
- **Infrastructure Sizing** (Excel) - Resource planning and cost calculations
- **Financial Proposal** (Excel) - Pricing breakdowns and payment schedules

## Prerequisites

### Required Skills

This skill depends on the following skills installed at `~/.claude/skills/`:

| Skill | Purpose |
|-------|---------|
| xlsx | Excel creation and editing |
| docx | Word document creation |
| drawio | Architecture diagram generation |

### System Dependencies

**Python packages:**

```bash
pip install pandas openpyxl python-docx defusedxml pillow
```

**Node.js packages:**

```bash
npm install -g docx
```

**macOS:**

```bash
brew install --cask libreoffice
brew install pandoc poppler coreutils
```

**Linux (Debian/Ubuntu):**

```bash
sudo apt-get install libreoffice pandoc poppler-utils xvfb
```

## Installation

### Step 1: Clone the repository

```bash
git clone https://github.com/aijcool/bid-response-generator.git
cd bid-response-generator
```

### Step 2: Copy files to Claude Code directories

Claude Code requires commands and skills to be placed in separate directories:

```bash
# Copy command file
cp commands/brd.md ~/.claude/commands/

# Copy skill directory
cp -r skills/brd ~/.claude/skills/
```

### Step 3: Verify installation

In Claude Code, run:

```
/brd --check
```

### Installation Result

After installation, your Claude Code directory should look like:

```
~/.claude/
├── commands/
│   └── brd.md                  # /brd command
└── skills/
    ├── brd/                    # BRD skill
    │   ├── SKILL.md
    │   └── templates/
    ├── xlsx/                   # Required dependency
    ├── docx/                   # Required dependency
    └── drawio/                 # Required dependency
```

## Usage

### Quick Start

1. **Create source directory structure** in your project:

```bash
mkdir -p source/{rfp,requirements,technical,architecture,infrastructure,financial}
```

2. **Place your source materials** in the appropriate directories (see Source Files section below)

3. **Run the command** in Claude Code:

```
/brd
```

4. **Review the generated plan** and confirm to proceed

5. **Find outputs** in the `BRD/` directory

### Command Options

| Command | Description |
|---------|-------------|
| `/brd` | Interactive generation with plan review |
| `/brd --plan-only` | Generate and display plan without executing |
| `/brd --check` | Verify dependencies and configuration |
| `/brd --lang=zh` | Set output language (en/zh/ar) |

### Project Directory Structure

```
your-project/
├── source/                          # Input: Your source materials
│   ├── rfp/                         # RFP/tender documents
│   │   └── RFP_Document.pdf
│   ├── requirements/                # Requirements analysis
│   │   └── requirements_analysis.md
│   ├── technical/                   # Technical proposal
│   │   └── technical_proposal.md
│   ├── architecture/                # Architecture descriptions
│   │   ├── overall_solution.md
│   │   ├── platform_architecture.md
│   │   ├── deployment_architecture.md
│   │   └── integration_architecture.md
│   ├── infrastructure/              # Infrastructure sizing
│   │   └── infrastructure_sizing.md
│   └── financial/                   # Financial proposal
│       └── financial_proposal.md
│
├── BRD/                             # Output: Generated documents
│   ├── 1_Requirements_Analysis.xlsx
│   ├── 2_Technical_Proposal.docx
│   ├── 3_Architecture_Diagrams/
│   │   ├── *.drawio
│   │   └── images/*.png
│   ├── 4_Infrastructure_Sizing.xlsx
│   └── 5_Financial_Proposal.xlsx
│
└── .brd-config.json                 # Configuration (optional)
```

## Configuration

Create `.brd-config.json` in your project root:

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

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| projectName | string | required | Project name for document headers |
| clientName | string | required | Client organization name |
| companyName | string | required | Your company name |
| language | string | "en" | Output language (en/zh/ar) |
| currency | string | "USD" | Currency for financial documents |
| outputDirectory | string | "BRD" | Output directory name |

## Source Files

### Supported Input Formats

| Format | Extension | Notes |
|--------|-----------|-------|
| PDF | .pdf | RFP documents |
| Word | .docx | RFP documents |
| Markdown | .md | All source content |

### Source File Templates

After installation, template files are located at:

```
~/.claude/skills/brd/templates/
```

- `requirements_analysis.md` - Requirements source template
- `technical_proposal.md` - Technical proposal template
- `infrastructure_sizing.md` - Infrastructure sizing template
- `financial_proposal.md` - Financial proposal template

## Output Documents

| Document | Format | Sheets/Sections |
|----------|--------|-----------------|
| Requirements Analysis | Excel (.xlsx) | Executive Summary, Functional, Non-Functional, Integration, Security, Compliance |
| Technical Proposal | Word (.docx) | Executive Summary, Company Profile, Solution, Implementation, Integration, PM, Support |
| Architecture Diagrams | Draw.io + PNG | Overall, Platform, Deployment, Integration |
| Infrastructure Sizing | Excel (.xlsx) | Summary, Production, Non-Production, Procurement |
| Financial Proposal | Excel (.xlsx) | Summary, One-time, Recurring, Schedule, Terms |

## Multi-Language Support

| Language | Code | RTL Support |
|----------|------|-------------|
| English | en | No |
| Chinese (Simplified) | zh | No |
| Arabic | ar | Yes |

## Repository Structure

```
bid-response-generator/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── commands/
│   └── brd.md              # -> Copy to ~/.claude/commands/
├── skills/
│   └── brd/
│       ├── SKILL.md        # -> Copy to ~/.claude/skills/brd/
│       └── templates/
└── agents/
    └── brd-planner/
        └── AGENT.md        # Planning agent (reference only)
```

## Troubleshooting

### Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| `/brd` command not found | Command not installed | Copy `commands/brd.md` to `~/.claude/commands/` |
| Skill not found | Skill not installed | Copy `skills/brd/` to `~/.claude/skills/` |
| Required skill missing | xlsx/docx/drawio not installed | Install required skills to `~/.claude/skills/` |
| Source not found | source/ directory missing | Run `mkdir -p source/{rfp,requirements,technical,architecture,infrastructure,financial}` |

### Dependency Check

Run `/brd --check` to verify all dependencies are installed correctly.

## Uninstall

To remove this skill:

```bash
rm ~/.claude/commands/brd.md
rm -rf ~/.claude/skills/brd
```

## Contributing

Contributions are welcome! Please:

1. Fork this repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.
