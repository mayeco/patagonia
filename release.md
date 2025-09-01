---
description: Create new releases based on Semantic Versioning with automated workflow
auto_execution_mode: 3
---

# Release Workflow

Create new releases based on Semantic Versioning (semver) with automated version bumping, changelog generation, git tagging, and release management. This workflow handles the complete release process from version determination to publishing.

## Important Rules:
- TARGET_ACTIVE_SHELL_COMMANDS

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete release process within 9 steps maximum.

**DECISION POINTS**: Make binary decisions - release type is appropriate or not.

**VALIDATION**: Validate project state and version before release.

**TERMINATION CONDITIONS**:
- If project not ready: Ask the developer to prepare and STOP
- If version conflict: Ask the developer to resolve and STOP
- Always require developer confirmation for release

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **ANALYZE CURRENT PROJECT STATE**:
   - Check current version from package.json, setup.py, or version files
   - Review recent commits and changes since last release
   - Validate project is in releasable state (tests pass, no breaking changes)
   - Check if CHANGELOG.md exists and is up-to-date

2. **DETERMINE RELEASE TYPE BASED ON SEMVER**:
   - **MAJOR** (X.y.z): Breaking changes, incompatible API changes
   - **MINOR** (x.Y.z): New features, backward compatible
   - **PATCH** (x.y.Z): Bug fixes, backward compatible
   - **PRE-RELEASE**: Alpha, beta, rc versions (x.y.z-alpha.1)
   - Ask the developer to specify type if not clear from commits

3. **GENERATE NEW VERSION NUMBER**:
   - Increment appropriate version component based on release type
   - Validate version format follows semver specification
   - Check version doesn't already exist in git tags
   - Generate pre-release versions if specified

4. **VERSION FILE UPDATES**:
   - Update package.json version field
   - Update any other version files (setup.py, constants)
   - Create or update `VERSION` file with the new version string (e.g., `vX.Y.Z` or `vX.Y.Z-<pre>`) and ensure a trailing newline
   - Example: `printf 'vX.Y.Z\\n' > VERSION`
   - Execute: `git add VERSION && git commit -m "Bump version to X.Y.Z"`
   - If command fails: STOP - "Git commit failed - check repository status"

5. **GENERATE CHANGELOG**:
   - Execute: generate-changelog WORKFLOW
   - If command fails: STOP - "Changelog generation failed"
   - Execute: `git add CHANGELOG.md && git commit -m "Update changelog"`
   - If command fails: STOP - "Git commit failed - check repository status"

6. **GIT OPERATIONS**:
   - Execute: `git branch`
   - If command fails: STOP - "Git branch creation failed"
   - Execute: `git tag -a vX.Y.Z -m "Release vX.Y.Z"`
   - If command fails: STOP - "Git tag creation failed"
   - Execute: `git push origin CURRENT_BRANCH && git push origin vX.Y.Z`
   - If command fails: STOP - "Git push failed - check remote repository access"

7. **PUBLISH RELEASE**:
   - Publish to package registries (npm, PyPI, etc.)
   - Upload artifacts if applicable
   - Notify team channels or integrations
   - Update documentation sites if needed

8. **POST-RELEASE CLEANUP**:
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
