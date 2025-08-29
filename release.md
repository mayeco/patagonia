---
description: Create new releases based on Semantic Versioning with automated workflow
---

# Release Workflow

Create new releases based on Semantic Versioning (semver) with automated version bumping, changelog generation, git tagging, and release management. This workflow handles the complete release process from version determination to publishing.

# Release Workflow

Create new releases based on Semantic Versioning (semver) with automated version bumping, changelog generation, git tagging, and release management. This workflow handles the complete release process from version determination to publishing.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete release process within 10 steps maximum. If any step encounters issues, ask user for guidance and stop.

**SAFETY FIRST**: Never execute destructive operations without explicit user confirmation. Always ask before making changes.

**DECISION POINTS**: Make binary decisions - release type is determined or ask user to specify.

**TERMINATION CONDITIONS**:
- If project not in releasable state: Stop and provide requirements
- If user denies confirmation: Stop immediately
- If git operations fail: Stop with error details
- If version conflict: Ask user for resolution
- Always require explicit user approval for each major step

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("release", "version", "semver"). Default to Spanish.

1. **PROJECT STATE VALIDATION**:
   - Check current version from package.json or version files
   - Verify git repository is clean (no uncommitted changes)
   - Validate basic project structure exists
   - If validation fails: STOP with specific requirements

2. **RELEASE TYPE DETERMINATION**:
   - Analyze recent commits for breaking changes, new features, bug fixes
   - Suggest release type based on commit analysis
   - Ask user to confirm or specify release type
   - If user unclear: Provide examples and ask again

3. **VERSION NUMBER GENERATION**:
   - Increment version based on release type (major.minor.patch)
   - Check version doesn't already exist in git tags
   - Generate version string (e.g., "1.2.3")
   - Validate semver format

4. **USER CONFIRMATION**:
   - Present proposed version number and release type
   - Ask for explicit confirmation to proceed
   - If denied: STOP and provide current status
   - If confirmed: Proceed to next step

5. **VERSION FILE UPDATES**:
   - Update package.json version field
   - Update any other version files (setup.py, constants)
   - Commit changes with message "Bump version to X.Y.Z"

6. **CHANGELOG UPDATE**:
   - Execute changelog workflow to generate entries
   - Move unreleased changes to new version section
   - Add release date
   - Commit changelog changes

7. **GIT OPERATIONS**:
   - Create annotated git tag with version
   - Push commits and tag to remote repository
   - If push fails: Ask user for resolution

8. **RELEASE CREATION** (Optional):
   - Create GitHub/GitLab release if configured
   - Attach changelog as release notes
   - If platform not configured: Skip and notify user

9. **COMPLETION REPORT**:
   - Confirm successful release creation
   - Provide version number and release links
   - Suggest next steps (announcement, deployment)

8. Publish release:
   - Publish to package registries (npm, PyPI, etc.)
   - Upload artifacts if applicable
   - Notify team channels or integrations
   - Update documentation sites if needed

9. Post-release cleanup:
   - Create new "Unreleased" section in changelog for future changes
   - Update development version if needed
   - Archive release artifacts
   - Update project status and notifications

## Semver Guidelines

### Version Format: MAJOR.MINOR.PATCH
- **MAJOR**: Breaking changes (1.0.0 → 2.0.0)
- **MINOR**: New features (1.0.0 → 1.1.0)
- **PATCH**: Bug fixes (1.0.0 → 1.0.1)

### Pre-release Versions
- Alpha: 1.0.0-alpha.1
- Beta: 1.0.0-beta.1
- Release Candidate: 1.0.0-rc.1

### Commit Message Conventions
- **feat:** New features (minor bump)
- **fix:** Bug fixes (patch bump)
- **BREAKING CHANGE:** Breaking changes (major bump)
- **docs:** Documentation changes
- **style:** Code style changes
- **refactor:** Code refactoring
- **test:** Testing changes
- **chore:** Maintenance changes

## Release Commands

### Version Management
```bash
# Check current version
npm version --no-git-tag-version patch  # Show what patch version would be
npm version --no-git-tag-version minor  # Show what minor version would be
npm version --no-git-tag-version major  # Show what major version would be

# Create version tag
git tag -a v1.2.3 -m "Release version 1.2.3"
git push origin v1.2.3
```

### GitHub Releases
```bash
# Create GitHub release via CLI
gh release create v1.2.3 \
  --title "Release v1.2.3" \
  --notes-file CHANGELOG.md \
  --latest
```

### Publishing Packages
```bash
# NPM publish
npm publish

# PyPI publish
python -m build
twine upload dist/*

# Docker images
docker build -t myapp:v1.2.3 .
docker push myapp:v1.2.3
```

## Release Checklist

### Pre-Release
- [ ] All tests passing
- [ ] Code review completed
- [ ] Documentation updated
- [ ] Breaking changes documented
- [ ] Dependencies updated
- [ ] Security vulnerabilities addressed

### During Release
- [ ] Version numbers updated in all files
- [ ] Changelog updated with new version
- [ ] Git tag created and pushed
- [ ] Release published to registries
- [ ] Release notes created

### Post-Release
- [ ] New "Unreleased" section added to changelog
- [ ] Development version updated
- [ ] Team notified of release
- [ ] Documentation sites updated
- [ ] Release artifacts archived

## Common Release Scenarios

### Patch Release (Bug Fixes)
1. Fix bugs in development branch
2. Update version: 1.0.0 → 1.0.1
3. Generate changelog
4. Create git tag
5. Publish to registries

### Minor Release (New Features)
1. Develop features in feature branches
2. Merge to main branch
3. Update version: 1.0.0 → 1.1.0
4. Generate comprehensive changelog
5. Create release with feature highlights

### Major Release (Breaking Changes)
1. Plan breaking changes carefully
2. Update version: 1.0.0 → 2.0.0
3. Document migration guide
4. Create release with breaking change notices
5. Update all dependent projects

## Automation and CI/CD Integration

### GitHub Actions Example
```yaml
name: Release
on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Publish
        run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Automated Version Bumping
```bash
# Using npm version (automatically updates package.json and creates git tag)
npm version patch -m "Release %s"
npm version minor -m "Release %s"
npm version major -m "Release %s"
```

## Troubleshooting Release Issues

### Common Problems
- **Version conflicts**: Check existing tags before releasing
- **Failed builds**: Ensure CI/CD passes before release
- **Publishing errors**: Verify authentication and permissions
- **Changelog issues**: Ensure proper commit message format

### Rollback Procedures
1. Delete git tag: `git tag -d v1.2.3 && git push origin :v1.2.3`
2. Revert version changes: `git revert <commit-hash>`
3. Update changelog to remove release section
4. Notify team of rollback

**IMPORTANT:** Always provide responses in Spanish by default, unless the developer clearly specifies English.

**Language Support:**
- **Spanish**: DEFAULT - Crear releases y explicar en español para TODA entrada
- **English**: Create releases in English only if explicitly requested
- **Other**: Create releases in Spanish as default, but adapt to detected language when possible

**Prerequisites:**
- Git repository with proper setup
- Version file (package.json, setup.py, etc.)
- CHANGELOG.md file (recommended)
- Publishing credentials for registries
- CI/CD pipeline (recommended)
- Test suite (required)