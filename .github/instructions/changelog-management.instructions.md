---
description: "Automatically update changelog with git repository changes"
applyTo: "**/CHANGELOG.md"
---

# Changelog Update Instructions

When editing or updating the CHANGELOG.md file, automatically analyze recent git repository changes and add appropriate entries.

## Change Detection Process

1. **Analyze Recent Commits**: Review commit messages, file changes, and code modifications since the last changelog update
2. **Categorize Changes**: Sort changes into Keep a Changelog categories (Added, Changed, Fixed, Removed, Security)
3. **Generate Entries**: Create user-focused, detailed changelog entries
4. **Maintain Structure**: Preserve existing format and organization

## Treasury Management Context

This project manages class treasury operations including:
- Monthly fee collection and tracking
- Payment processing and categorization
- Student account management
- Financial reporting and reconciliation
- CSV/Excel data import/export
- Local-first data storage (SQLite/CSV)

## Entry Guidelines

### Format Requirements
- Use action verbs (Added, Fixed, Improved, etc.)
- Focus on user impact, not technical implementation
- Include relevant financial/accounting context
- Be specific about what changed
- Group related changes logically

### Content Standards
- Emphasize changes affecting financial accuracy
- Highlight data integrity improvements
- Note audit trail enhancements
- Describe workflow impact for treasury operators
- Mention compliance or reporting improvements

### Language Considerations
- Write in English (technical documentation)
- Consider Spanish-speaking end users for feature descriptions
- Use appropriate educational finance terminology
- Respect cultural context for payment methods

## Example Entries

### Added
- "Added bulk payment import from Excel with automatic student ID matching and duplicate detection"
- "Implemented configurable late payment penalties with graduated fee structure based on days overdue"
- "Created comprehensive monthly reconciliation report with detailed transaction breakdown"

### Changed
- "Enhanced payment categorization engine with improved automatic transaction type detection"
- "Updated reporting dashboard with real-time balance calculations and visual payment status indicators"
- "Improved CSV export performance for large student datasets (1000+ records)"

### Fixed
- "Fixed calculation error in prorated monthly fees for students enrolling mid-month"
- "Resolved CSV encoding issues causing corruption of Spanish characters in student names"
- "Corrected balance calculation discrepancies when payments span multiple billing periods"

## Automation Rules

### Include in Changelog
- New features or functionality
- Bug fixes affecting user experience
- Performance improvements
- API/MCP tool changes
- Data schema modifications
- Security enhancements
- Configuration changes

### Exclude from Changelog
- Code style/formatting changes
- Test-only modifications
- Build script updates
- Development tool changes
- Documentation updates (unless user-facing)
- Dependency updates without functional impact

## Quality Checklist

Before finalizing entries:
- [ ] All user-impacting changes documented
- [ ] Correct categorization applied
- [ ] Treasury context included where relevant
- [ ] Clear, professional language used
- [ ] User impact clearly described
- [ ] No technical jargon without explanation