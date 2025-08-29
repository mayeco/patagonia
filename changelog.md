---
description: Generate changelog from git commit history analysis
---

# Changelog Generator Workflow

Generate a comprehensive changelog based on git commit history analysis, categorizing changes and providing detailed insights.

# Changelog Generator Workflow

Generate a comprehensive changelog based on git commit history analysis, categorizing changes and providing detailed insights.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Always complete the workflow within 10 steps maximum. If analysis takes longer than expected, proceed with available data.

**DECISION POINTS**: Make binary decisions (yes/no) quickly and proceed. Do not over-analyze edge cases.

**TERMINATION CONDITIONS**: 
- If no git repository found: Stop and notify user
- If no commits found: Generate empty changelog template
- If git command fails: Use alternative approach or stop

## Steps

0. **LANGUAGE DETECTION**: Check user input for English indicators (keywords like "english", "changelog", "generate"). Default to Spanish if unclear.

1. **GIT REPOSITORY VALIDATION**: 
   - Execute: `git rev-parse --git-dir`
   - If fails: STOP - "No git repository found in current directory"
   - If succeeds: Proceed to step 2

2. **COMMIT HISTORY EXTRACTION**:
   - Execute: `git log --pretty=format:"%h|%an|%ad|%s" --date=short --stat -20 --no-merges`
   - Parse output line by line
   - Extract: hash, author, date, message, file changes
   - If command fails: Try `git log --oneline -20` as fallback
   - Store results in structured format for processing

3. **COMMIT CATEGORIZATION** (Use exact keyword matching):
   - **Added**: Keywords: "feat:", "add:", "new:", "create:"
   - **Changed**: Keywords: "update:", "modify:", "refactor:", "improve:"
   - **Deprecated**: Keywords: "deprecate:", "deprecated:"
   - **Removed**: Keywords: "remove:", "delete:", "rm:"
   - **Fixed**: Keywords: "fix:", "bug:", "issue:", "resolve:"
   - **Security**: Keywords: "security:", "vuln:", "patch:"
   - **Default category**: "Changed" for uncategorized commits

4. **CHANGELOG STRUCTURE GENERATION**:
   - **Check for unreleased changes**: If any commits exist after last tag/version, create "Unreleased" section
   - **Version detection**: Execute `git tag --sort=-version:refname | head -5` to find recent versions
   - **Date handling**: Use commit dates for entries, current date for new releases
   - **Grouping**: Group by category, then by date (newest first)

5. **FORMAT VALIDATION**:
   - Ensure proper markdown structure
   - Validate all required sections exist
   - Check for duplicate entries
   - Verify chronological ordering

6. **FILE OUTPUT**:
   - Write to `./CHANGELOG.md`
   - Use UTF-8 encoding
   - Include generation timestamp in comments

7. **FINAL VALIDATION**:
   - Confirm file was created successfully
   - Verify markdown syntax is valid
   - Check file size is reasonable (< 1MB)

8. **RESPONSE GENERATION**:
   - Confirm successful generation
   - Provide file location and summary
   - Suggest next steps (review, commit)

**Language Support:**
- **Spanish**: DEFAULT - Generar CHANGELOG en español para toda entrada
- **English**: Generate CHANGELOG in English only if explicitly requested
- **Other**: Generate CHANGELOG in Spanish as default, but adapt to detected language when possible

**Changelog Categories (Keep a Changelog Format):**
- ✨ **Added**: Nuevas funcionalidades o características
- 🔄 **Changed**: Cambios en funcionalidad existente
- ⏰ **Deprecated**: Funcionalidades próximamente eliminadas
- 🗑️ **Removed**: Funcionalidades eliminadas
- 🐛 **Fixed**: Corrección de errores
- 🔒 **Security**: Corrección de vulnerabilidades de seguridad

**Analysis Features:**
- Commit message analysis and categorization
- File change impact assessment
- Author contribution tracking
- Breaking change detection
- Feature complexity evaluation