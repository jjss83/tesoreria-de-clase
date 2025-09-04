---
mode: agent
description: "Automatically analyze git repository changes and update CHANGELOG.md with categorized entries"
---

# Changelog Update Agent

## Task
Analyze git repository changes and update CHANGELOG.md with categorized entries following Keep a Changelog format.

## Context
You are working on the **CajaChica** project - a local-first accounting system for class treasury management including:
- Monthly fee collection and tracking
- Payment processing and categorization  
- Student account management
- Financial reporting and CSV/Excel integration
- MCP server automation

## Instructions

### 1. Change Analysis
Examine recent commits and changes to identify:
- New features and functionality additions
- Bug fixes and error corrections
- Performance improvements and optimizations
- Security enhancements
- Breaking changes or removals

### 2. Categorization
Sort changes into Keep a Changelog categories:
- **Added**: New features, APIs, or functionality
- **Changed**: Modifications to existing functionality
- **Fixed**: Bug fixes and error corrections
- **Removed**: Deleted features or functionality
- **Security**: Security-related improvements
- **Deprecated**: Features marked for future removal

### 3. Entry Format
Write entries that:
- Focus on user impact, not technical implementation
- Use clear, professional language
- Include treasury/accounting context when relevant
- Start with action verbs (Added, Fixed, Improved, etc.)
- Are specific about what changed

### 4. Treasury Context
When relevant, emphasize:
- Financial accuracy and calculation changes
- Data integrity improvements
- User workflow impact
- Reporting enhancements
- Compliance or audit trail changes

## Examples

### Added
- Bulk payment import from Excel with automatic student ID matching and validation
- Configurable late payment penalty system with graduated fees based on overdue days
- Monthly reconciliation report with detailed transaction breakdown and variance analysis

### Fixed
- Resolved calculation error in prorated monthly fees for mid-month student enrollments
- Corrected CSV export encoding issues with Spanish characters in student names
- Fixed balance discrepancies when payments span multiple billing periods

### Changed
- Improved CSV export performance for large datasets (30s to 3s for 1000+ records)
- Enhanced payment categorization with 95% automatic transaction detection
- Updated dashboard with real-time balance calculations and status indicators

## Quality Standards
- All significant user-facing changes documented
- Entries correctly categorized
- Professional, clear language used
- Treasury context included where relevant
- Consistent formatting maintained
- No technical jargon without explanation

## Process
1. Review recent commits and file changes
2. Identify user-impacting modifications
3. Categorize changes appropriately
4. Write clear, context-aware entries
5. Update CHANGELOG.md under [Unreleased] section
6. Maintain existing format and structure