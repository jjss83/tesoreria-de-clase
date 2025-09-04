# Version Management Guide

This guide explains how to create and manage releases using the changelog and release prompt system.

## 🎯 **Version Management Process**

### **1. Development Phase**
- Work on features and commit changes with descriptive messages
- Use the `changelog.prompt.md` to update the `[Unreleased]` section
- Keep accumulating changes in the Unreleased section

### **2. Release Decision**
When ready to create a release:
- Analyze the types of changes in `[Unreleased]`
- Determine the appropriate version number using semantic versioning
- Use the `release.prompt.md` to guide the release process

### **3. Version Types**

#### **Semantic Versioning for Treasury System**
- **MAJOR (X.0.0)**: Breaking changes, database schema changes, major API modifications
- **MINOR (0.X.0)**: New features, new reports, MCP tools, payment methods
- **PATCH (0.0.X)**: Bug fixes, calculation corrections, UI improvements

## 🔄 **Release Workflow**

### **Step 1: Update [Unreleased] Section**
```bash
# In VS Code Copilot Chat:
@workspace /prompts Use changelog.prompt.md to update CHANGELOG.md with recent changes
```

### **Step 2: Create Release Version**
```bash
# In VS Code Copilot Chat:
@workspace /prompts Use release.prompt.md to create version X.Y.Z release
```

### **Step 3: Git Commands**
```bash
# Commit the changelog update
git add CHANGELOG.md
git commit -m "release: prepare vX.Y.Z with [brief description]"

# Create the release tag
git tag -a vX.Y.Z -m "Release vX.Y.Z: [detailed description]"

# Push everything
git push origin main
git push origin vX.Y.Z
```

## 📝 **Prompt Usage Examples**

### **Regular Development**
```
User: @workspace /prompts Follow changelog.prompt.md instructions

Result: Updates [Unreleased] section with recent changes
```

### **Creating a Release**
```
User: @workspace /prompts Follow release.prompt.md to create v0.2.0

Result: Moves [Unreleased] content to [0.2.0] section, adds version links
```

## 🏷️ **Version Strategy for CajaChica**

### **Planned Version Roadmap**
- **v0.1.0** ✅ - Project foundation and documentation
- **v0.2.0** - Basic payment recording and student management
- **v0.3.0** - Reporting and reconciliation features
- **v0.4.0** - MCP server integration
- **v0.5.0** - CSV/Excel import/export
- **v1.0.0** - Production-ready with full feature set

### **Release Criteria**

#### **v0.2.0 (Minor Release)**
- Basic CRUD operations for students, charges, payments
- Simple payment allocation logic
- Basic validation and error handling

#### **v0.3.0 (Minor Release)**  
- Monthly fee generation
- Payment reconciliation
- Basic reporting (debtors, balances)

#### **v1.0.0 (Major Release)**
- Complete feature set from PRD
- Full test coverage
- Production documentation
- Performance optimization

## 🛠️ **Git Tag Management**

### **List Existing Tags**
```bash
git tag -l                    # List all tags
git tag -l "v0.*"            # List v0.x tags
git describe --tags          # Show latest tag
```

### **Tag Information**
```bash
git show v0.1.0              # Show tag details
git log --oneline v0.1.0     # Show commits up to tag
```

### **Delete Tags (if needed)**
```bash
git tag -d v0.1.0            # Delete local tag
git push origin :refs/tags/v0.1.0  # Delete remote tag
```

## 📊 **Release Validation Checklist**

Before creating any release:

### **Code Quality**
- [ ] All tests pass
- [ ] No lint errors
- [ ] Code review completed
- [ ] Documentation updated

### **Treasury System Specific**
- [ ] Financial calculations verified
- [ ] Data validation tested
- [ ] CSV/Excel formats validated
- [ ] Currency handling correct

### **Release Process**
- [ ] Changelog updated with all changes
- [ ] Version number follows semantic versioning
- [ ] Git tag created with descriptive message
- [ ] Release notes prepared

## 🔗 **Integration with GitHub**

### **After Pushing Tags**
1. **GitHub Releases**: Tags automatically create release drafts
2. **Release Notes**: Use changelog content for release descriptions
3. **Assets**: Attach any build artifacts or documentation

### **Automated Release Notes**
GitHub can generate release notes automatically:
```bash
# Create release with auto-generated notes
gh release create v0.2.0 --generate-notes
```

## 📈 **Future Enhancements**

### **Planned Improvements**
- Automated version bumping based on conventional commits
- Integration with GitHub Actions for release automation
- Semantic versioning validation
- Automated changelog generation from commit messages

### **Advanced Features**
- Pre-release versions (v0.2.0-alpha.1)
- Release candidates (v0.2.0-rc.1)  
- Hotfix workflow for critical patches
- Automated deployment triggered by releases

---

This version management system ensures professional, traceable releases while maintaining clear communication about changes to the treasury management system.