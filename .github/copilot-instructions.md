# Copilot Custom Instructions for CajaChica (Tesorería de Clase)

## Project Overview

This is the **CajaChica** project - a local-first accounting system for managing class treasury operations including monthly fees and extraordinary charges. The system uses CSV/Excel/SQLite storage with MCP server integration and an intelligent agent for payment processing.

## Automatic Changelog Management

When working with this codebase, automatically track and document changes in the `CHANGELOG.md` file following these guidelines:

### Change Detection and Analysis

Before suggesting changelog updates, analyze:
- **Recent commits** and their messages since the last changelog update
- **Modified files** and their purpose within the project architecture
- **Code changes** and their functional impact on users
- **Project context** (treasury/accounting management system)

### Categorization Rules

Classify all changes into Keep a Changelog categories:

#### Added 🆕
- New features, modules, APIs, or functionality
- New MCP tools or CLI commands
- New reports, exports, or data processing capabilities
- New validation rules or business logic
- New configuration options or settings
- **Keywords**: `add`, `create`, `new`, `implement`, `feature`, `introduce`, `build`

#### Changed 🔄
- Modifications to existing functionality or behavior
- Performance improvements and optimizations
- UI/UX enhancements and updates
- Refactoring that affects user experience
- Configuration or default value changes
- API modifications that maintain compatibility
- **Keywords**: `update`, `change`, `modify`, `improve`, `refactor`, `enhance`, `optimize`

#### Fixed 🐛
- Bug fixes and error corrections
- Data validation and calculation fixes
- UI/display issue resolutions
- Import/export problems resolved
- Memory leaks or performance issues corrected
- **Keywords**: `fix`, `bug`, `error`, `issue`, `resolve`, `correct`, `repair`

#### Removed 🗑️
- Deleted features, APIs, or functionality
- Deprecated code or configuration removal
- Unused dependencies or files cleanup
- Legacy feature removal
- **Keywords**: `remove`, `delete`, `drop`, `deprecate`, `eliminate`

#### Security 🔒
- Security patches and vulnerability fixes
- Authentication and authorization improvements
- Data protection and privacy enhancements
- Access control modifications
- **Keywords**: `security`, `vulnerability`, `auth`, `permission`, `encrypt`, `protect`

### Entry Format Guidelines

Write changelog entries that are:

1. **User-Focused**: Describe the impact on end users, not implementation details
2. **Specific**: Include concrete details about what changed
3. **Context-Aware**: Reference treasury/accounting concepts when relevant
4. **Professional**: Use consistent, clear terminology
5. **Actionable**: Help users understand what they need to do (if anything)

### Treasury Management Context

When describing changes, consider:
- **Financial Accuracy**: Emphasize changes affecting calculations, fees, or payments
- **Data Integrity**: Highlight improvements to data validation or consistency
- **Audit Trail**: Note changes affecting logging, tracking, or compliance
- **User Workflow**: Describe how changes impact daily treasury operations
- **Reporting**: Mention improvements to financial reports or summaries

### Language and Localization

- Write technical content in English (codebase language)
- Consider Spanish-speaking end users when describing user-facing features
- Use appropriate financial terminology for the education sector
- Respect cultural context for payment methods and processes

### Entry Examples

#### Feature Additions
- "Added bulk payment import from Excel with automatic student matching and validation"
- "Implemented configurable late payment penalties with graduated fee structure"
- "Created monthly fee reconciliation report with detailed payment tracking"
- "Added support for partial payments with automatic balance calculation"

#### Bug Fixes
- "Fixed calculation error in prorated monthly fees for mid-month student enrollments"
- "Resolved CSV export issues with special characters in Spanish student names"
- "Corrected balance discrepancies when payments span multiple billing periods"
- "Fixed duplicate transaction detection in bank statement imports"

#### Improvements
- "Enhanced payment categorization with intelligent transaction description parsing"
- "Improved CSV export performance for datasets with over 1000 students"
- "Updated reporting dashboard with real-time balance calculations and visual indicators"
- "Optimized database queries for faster payment history retrieval"

### Automation Guidelines

Update the changelog when:
- ✅ New features are implemented or modified
- ✅ Bug fixes are applied that affect user experience
- ✅ Performance improvements are made
- ✅ API changes occur (MCP tools, CLI commands)
- ✅ Data schema modifications happen
- ✅ Security improvements are implemented
- ✅ Configuration or default behavior changes

Do NOT update for:
- ❌ Pure code style or formatting changes
- ❌ Test file modifications without functional impact
- ❌ Build script or development tool updates
- ❌ Documentation-only changes (unless user-facing)
- ❌ Dependency updates without feature impact

### Update Process

When updating `CHANGELOG.md`:

1. **Preserve Structure**: Maintain existing format and organization
2. **Update Unreleased Section**: Add all new entries under `## [Unreleased]`
3. **Maintain Category Order**: Keep standard sequence (Added, Changed, Deprecated, Removed, Fixed, Security)
4. **Use Consistent Dating**: Apply ISO format (YYYY-MM-DD) for version releases
5. **Group Related Changes**: Combine similar modifications into comprehensive entries
6. **Verify Accuracy**: Ensure all significant user-facing changes are captured

### Quality Checklist

Before finalizing changelog entries:
- [ ] All user-impacting changes are documented
- [ ] Entries are categorized correctly
- [ ] Language is clear and professional
- [ ] Treasury/accounting context is included where relevant
- [ ] Technical jargon is minimized
- [ ] User impact is clearly described
- [ ] Related changes are properly grouped

## Code Style and Development Guidelines

### TypeScript/Node.js Standards
- Use descriptive variable names in English
- Follow consistent error handling patterns
- Add comprehensive JSDoc comments for public APIs
- Implement proper type definitions for all interfaces
- Use async/await for asynchronous operations

### Financial Calculations
- Always use decimal arithmetic for monetary calculations
- Implement proper rounding for currency values
- Add validation for all financial inputs
- Include unit tests for all calculation functions
- Document currency handling and precision requirements

### Data Handling
- Validate all CSV/Excel imports thoroughly
- Implement proper error handling for data operations
- Use transactions for database operations affecting multiple records
- Add logging for all data modification operations
- Ensure data consistency across CSV and SQLite storage

### MCP Integration
- Document all MCP tools with clear descriptions and examples
- Implement proper error responses for MCP operations
- Add validation for all MCP tool parameters
- Include usage examples in tool documentation
- Test MCP tools with realistic data scenarios

### Testing Requirements
- Write unit tests for all business logic functions
- Include integration tests for MCP tools and CLI commands
- Test CSV/Excel import/export with various data formats
- Validate financial calculations with edge cases
- Implement end-to-end tests for complete user workflows

---

Remember: These instructions help maintain consistency in code quality and documentation. The changelog serves as a communication tool for users, administrators, and future developers working with this treasury management system.