---
mode: agent
description: "Create a new version release by moving Unreleased changes to a versioned section"
---

# Release Version Agent

## Task
Create a new version release by moving [Unreleased] changelog entries to a proper versioned section and preparing for git tagging.

## Context
You are managing releases for the **CajaChica** treasury management system. Follow semantic versioning and maintain proper changelog structure.

## Instructions

### 1. Version Determination
Analyze unreleased changes to determine appropriate version number:

**Semantic Versioning Rules:**
- **MAJOR (X.0.0)**: Breaking changes, major architecture changes, incompatible API changes
- **MINOR (0.X.0)**: New features, backward-compatible functionality additions
- **PATCH (0.0.X)**: Bug fixes, small improvements, backward-compatible corrections

**Treasury System Context:**
- **MAJOR**: Database schema changes, API breaking changes, major workflow modifications
- **MINOR**: New payment methods, reporting features, MCP tools, user interface enhancements
- **PATCH**: Calculation fixes, UI bugs, performance improvements, documentation updates

### 2. Release Process

#### Step 1: Analyze Current [Unreleased] Section
Review what types of changes are included:
- Count Added, Changed, Fixed, Removed, Security, Deprecated items
- Assess impact on existing functionality
- Determine if changes are breaking or backward-compatible

#### Step 2: Determine Version Number
Based on analysis:
```
If (breaking changes OR major new features): MAJOR version
Else if (new features OR enhancements): MINOR version  
Else: PATCH version
```

#### Step 3: Create Versioned Section
Move [Unreleased] content to new version section:
```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- [Move Added items from Unreleased]

### Changed  
- [Move Changed items from Unreleased]

### Fixed
- [Move Fixed items from Unreleased]

### Removed
- [Move Removed items from Unreleased]

### Security
- [Move Security items from Unreleased]

## [Unreleased]

[Empty sections ready for next changes]
```

#### Step 4: Update Version Links
Add comparison links at bottom of changelog:
```markdown
[Unreleased]: https://github.com/jjss83/tesoreria-de-clase/compare/vX.Y.Z...HEAD
[X.Y.Z]: https://github.com/jjss83/tesoreria-de-clase/releases/tag/vX.Y.Z
```

### 3. Git Tag Instructions
After updating changelog, create git tag:
```bash
# Create annotated tag
git tag -a vX.Y.Z -m "Release version X.Y.Z: Brief description"

# Push tag to remote
git push origin vX.Y.Z

# Or push all tags
git push --tags
```

### 4. Release Notes Generation
Based on changelog entries, suggest release notes format:

```markdown
# Release vX.Y.Z - Release Name

## 🎯 Highlights
- Key feature or improvement summary

## 📋 Full Changelog

### 🆕 Added
- [Bullet points from Added section]

### 🔄 Changed  
- [Bullet points from Changed section]

### 🐛 Fixed
- [Bullet points from Fixed section]

## 📥 Download
- [Release download links]

## 🔗 Links
- [Comparison link]: https://github.com/jjss83/tesoreria-de-clase/compare/vX.Y.Z-1...vX.Y.Z
```

### 5. Treasury Release Guidelines

#### Version Planning
- **v0.1.0**: Initial system with basic payment recording
- **v0.2.0**: Add reporting and reconciliation features  
- **v0.3.0**: MCP server integration
- **v1.0.0**: Production-ready with full feature set

#### Release Timing
- **Patch releases**: As needed for critical fixes
- **Minor releases**: Monthly or when significant features are complete
- **Major releases**: When breaking changes or major milestones are reached

#### Release Validation
Before releasing:
- [ ] All tests pass
- [ ] Documentation is updated  
- [ ] Financial calculations are verified
- [ ] Backward compatibility is maintained (unless major version)
- [ ] Security review completed

## Examples

### Minor Release (v0.2.0)
```markdown
## [0.2.0] - 2025-09-15

### Added
- Monthly reconciliation reports with detailed transaction breakdown
- Bulk payment import from Excel with automatic student matching
- Configurable late payment penalty system

### Changed
- Enhanced payment categorization with improved accuracy
- Updated dashboard with real-time balance calculations

### Fixed
- Resolved calculation errors in prorated monthly fees
- Corrected CSV export encoding for Spanish characters
```

### Patch Release (v0.1.1)  
```markdown
## [0.1.1] - 2025-09-10

### Fixed
- Fixed balance calculation discrepancies in payment allocation
- Corrected date formatting in financial reports
- Resolved CSV import issues with special characters

### Changed
- Improved error messages for failed payment processing
```

## Process Summary

1. **Analyze unreleased changes** → Determine version type
2. **Create versioned section** → Move content from [Unreleased]
3. **Update changelog structure** → Add version links
4. **Create git tag** → `git tag -a vX.Y.Z -m "message"`
5. **Push tag** → `git push origin vX.Y.Z`
6. **Generate release notes** → Based on changelog content