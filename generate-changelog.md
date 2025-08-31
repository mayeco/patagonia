---
description: Generate changelog from git commit history analysis
---

# Changelog Generator Workflow

Generate a comprehensive changelog based on git commit history analysis, categorizing changes and providing detailed insights.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete changelog generation within 8 steps maximum. If git analysis takes too long, use available data and proceed.

**COMMAND VALIDATION**: Execute git commands directly without validation. If commands fail, stop with specific error message.

**DATA PROCESSING**: Process commits in chronological order without over-analysis.

**TERMINATION CONDITIONS**:
- If git repository not found: Stop with clear error message
- If no commits found: Stop with explanation
- If command fails: Stop with specific error details
- Always provide changelog content or clear error

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **ANALYZE GIT HISTORY**:
   - Run `git log --pretty=format:"%h|%an|%ad|%s" --date=short --stat -20 --no-merges` to get comprehensive commit data
   - Use deterministic sorting: commits processed in chronological order (oldest to newest)
   - Extract commit messages, authors, dates, and categorize changes consistently

2. **GIT REPOSITORY VALIDATION**:
   - Execute: `git log --pretty=format:"%h|%an|%ad|%s" --date=short --stat -20 --no-merges`
   - If command fails: STOP - "Git command failed - ensure git is installed and in a valid repository"
   - If no commits found: STOP - "No git commits found in this repository"
   - Parse output for commit data (hash, author, date, message, stats)

3. **COMMIT CATEGORIZATION**:
   - Classify each commit by type using commit message patterns
      - **Added**: Keywords like "add", "new", "create", "feature"
      - **Changed**: Keywords like "update", "modify", "change", "improve"
      - **Deprecated**: Keywords like "deprecate", "obsolete"
      - **Removed**: Keywords like "remove", "delete", "eliminate"
      - **Fixed**: Keywords like "fix", "bug", "issue", "resolve"
      - **Security**: Keywords like "security", "vulnerability", "auth", "encrypt"

4. **GENERATE CHANGELOG**:
   - **DO NOT include standard Keep a Changelog header text**: "El formato se basa en [Keep a Changelog]..." 
   - **DO NOT include Semantic Versioning reference text**: "este proyecto se adhiere a [Semantic Versioning]..."
   - **CRITICAL**: Only include "## [Sin liberar]" or "## Unreleased" section IF THERE ARE ACTUAL UNRELEASED CHANGES
   - **DO NOT add empty "## [Sin liberar]" sections** when no unreleased changes exist
   - **Check for unreleased changes first** before adding any unreleased section
   - **Skip unreleased section completely** if no pending changes are found
   - Include "Unreleased" section only if unreleased changes exist
   - **ALWAYS include release dates**: Use current date (YYYY-MM-DD format) for new releases
   - **Add commit dates**: Include dates from git commit history for each change
   - Use version numbers and release dates (YYYY-MM-DD format)
   - Group similar changes together in alphabetical order
   - List changes chronologically (newest first) but maintain consistent formatting

5. **FORMAT THE CHANGELOG**:
   - Clear section headers for each category
   - Bullet points with descriptive commit summaries
   - Links to specific commits when possible
   - Date ranges covered by the changelog

6. **SAVE THE GENERATED FILE**:
   - Save the generated CHANGELOG.md to the project root

7. **DO NOT COMMIT THE CHANGELOG**:
   - Let the developer review and commit manually

8. **ENSURE DETERMINISTIC OUTPUT**:
   - Running the same command multiple times with the same git history should produce identical CHANGELOG.md files

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