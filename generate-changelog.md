---
description: Generate changelog from git commit history analysis
auto_execution_mode: 3
---

# Changelog Generator Workflow

Generate a comprehensive changelog based on git commit history analysis, categorizing changes and providing detailed insights.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete changelog generation within 8 steps, maximum. If git analysis takes too long, use available data and proceed.

**DATA PROCESSING**: Process commits in chronological order without over-analysis.

**TERMINATION CONDITIONS**:

- If a git repository is not found: Stop with a clear error message
- If no commits are found: Stop with an explanation
- If a git command fails: Stop with specific error details
- Always provide changelog content or a clear error

## STEPS

{% include _includes/language-detection.md %}

1. **SHELL DETECTION AND TARGETING (DO NOT SKIP)**:
   - RULE: TARGET_ACTIVE_SHELL_COMMANDS
   - Detect the active shell using `echo $SHELL`
   - Detect git installation using `git --version`
   - If git is not installed: STOP - "Git is not installed - ensure git is installed and in a valid repository"

2. **GIT REPOSITORY HISTORY ANALYSIS**:
   - **Shell-agnostic description**: This Git command lists the last 20 non-merge commits with a one-line header per commit (hash, author, YYYY-MM-DD date, subject), followed by per-file change stats. The header fields are separated by a literal pipe character `|`. For clarity and portability, you may prefer `-n 20` instead of `-20` (both are equivalent).
   - **Shell targeting guidance**: When executing programmatically, do not assume Bash. Detect the active shell and wrap the command accordingly.
     - fish: `fish -c "git log --pretty=format:'%h|%an|%ad|%s' --date=short --stat -n 20 --no-merges"`
     - Bash: `bash -lc "git log --pretty=format:'%h|%an|%ad|%s' --date=short --stat -n 20 --no-merges"`
     - POSIX sh: `sh -lc "git log --pretty=format:'%h|%an|%ad|%s' --date=short --stat -n 20 --no-merges"`

   - **Quoting guidance**: Quote the pretty-format as `--pretty=format:'%h|%an|%ad|%s'` so `|` is treated as a literal within the argument (not a pipe). When wrapping in a shell, use outer double quotes so the inner single quotes survive. Do not split arguments across lines; treat each flag as a single token.

3. **COMMIT CATEGORIZATION**:
   - Classify each commit by type using commit message patterns
     - **Added**: Keywords like "add", "new", "create", "feature"
     - **Changed**: Keywords like "update", "modify", "change", "improve"
     - **Deprecated**: Keywords like "deprecate", "obsolete"
     - **Removed**: Keywords like "remove", "delete", "eliminate"
     - **Fixed**: Keywords like "fix", "bug", "issue", "resolve"
     - **Security**: Keywords like "security", "vulnerability", "auth", "encrypt"

4. **GENERATE CHANGELOG**:
   - USE A DETERMINISTIC ALGORITHM TO GENERATE THE CHANGELOG
   - DO NOT add empty sections
   - Check for unreleased changes first before adding any unreleased section
   - Skip unreleased section completely if no pending changes are found
   - ALWAYS include release dates: Use current date (YYYY-MM-DD format) for new releases
   - Add commit dates: Include dates from git commit history for each change
   - Use version numbers and release dates (YYYY-MM-DD format)
   - Group similar changes together in alphabetical order
   - List changes chronologically (newest first) but maintain consistent formatting

5. **FORMAT THE CHANGELOG**:
   - Clear section headers for each category
   - Bullet points with descriptive commit summaries
   - Links to specific commits when possible
   - Date ranges covered by the changelog

6. **ENSURE DETERMINISTIC OUTPUT**:
   - Running the same command multiple times with the same git history should produce identical CHANGELOG.md files.

7. **SAVE THE GENERATED FILE**:
   - Save the generated CHANGELOG.md to the project root

8. **DO NOT COMMIT THE CHANGELOG**:
   - Let the developer review and commit manually

**Changelog Categories (Keep a Changelog Format):**

- ✨ **Added**: New features or capabilities
- 🔄 **Changed**: Changes to existing functionality
- ⏰ **Deprecated**: Features to be removed in the future
- 🗑️ **Removed**: Features removed
- 🐛 **Fixed**: Error corrections
- 🔒 **Security**: Security corrections

**Analysis Features:**

- Commit message analysis and categorization
- File change impact assessment
- Author contribution tracking
- Breaking change detection
- Feature complexity evaluation
