# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.2] - 2025-01-12

### Changed

- Fixed installation instructions: commands and skills must be copied to separate directories
- Added step-by-step installation guide
- Added uninstall instructions
- Updated template file paths to reflect correct installation location
- Improved troubleshooting section with command-specific issues

## [1.0.1] - 2025-01-12

### Changed

- Updated README.md with correct installation instructions
- Removed non-existent `/plugin marketplace` commands
- Changed from "plugin" terminology to "skill" for accuracy
- Added detailed troubleshooting section
- Added project structure documentation
- Improved configuration documentation

### Removed

- Removed `.claude-plugin/` directory (marketplace.json, plugin.json) as Claude Code does not currently support plugin marketplace

## [1.0.0] - 2025-01-12

### Added

- Initial release of Bid Response Generator skill
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
