# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-01-12

### Added

- Initial release of Bid Response Generator plugin
- `/brd` command for interactive document generation
- BRD skill with comprehensive documentation
- Support for 5 document types:
  - Requirements Analysis (Excel)
  - Technical Proposal (Word)
  - Architecture Diagrams (Draw.io)
  - Infrastructure Sizing (Excel)
  - Financial Proposal (Excel)
- Professional document templates
- Multi-language support (English, Chinese, Arabic)
- Configuration via `.brd-config.json`
- BRD Planner agent for interactive planning
- Dependency checking (`--check` flag)
- Plan-only mode (`--plan-only` flag)

### Dependencies

- Requires xlsx skill (user-level)
- Requires docx skill (user-level)
- Requires drawio skill (user-level)

## [Unreleased]

### Planned

- Additional template customization options
- More architecture diagram types
- PDF export for all documents
- Integration with project management tools
- AI-powered RFP analysis improvements
