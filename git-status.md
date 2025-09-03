---
description: Check the current Git status and analyze any pending changes in the repository
auto_execution_mode: 3
---

# Git Status Workflow

Check the current Git status and analyze any pending changes in the repository.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete Git status analysis within 5 steps, maximum.

**DECISION POINTS**: Make binary decisions - the repository is valid or not.

**VALIDATION**: Check Git installation and repository state.

**TERMINATION CONDITIONS**:

- If not a Git repository: Ask the developer to navigate to the repository and STOP
- If Git is not installed: Ask the developer to install it and STOP
- Always provide a summary, even with errors

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **REPOSITORY VALIDATION**:
   - Execute: `git rev-parse --git-dir`
   - If it fails: STOP - "Current directory is not a Git repository"
   - If it succeeds: Proceed to step 2

2. **STATUS EXECUTION**:
   - Execute: `git status --porcelain`
   - If the command fails: STOP - "Git command failed - ensure Git is installed"
   - Parse output for file states (modified, added, deleted, untracked)
   - Count total changes (limit analysis to the first 20 files)
   - If no changes: STOP - "Repository is clean"

3. **CHANGES ANALYSIS** (Limited scope):
   - For the first 5 modified files: Execute `git diff --stat <filename>`
   - If the command fails: STOP - "Git diff failed - ensure Git is installed"
   - Extract basic change statistics (lines added/removed)
   - Skip binary files and large files (>1MB)
   - If more than 20 files changed: Focus on summary only

4. **CONTENT SUMMARIZATION**:
   - Group files by type (code, config, docs, assets)
   - Provide a high-level summary of changes
   - Identify potentially important files (package.json, README, etc.)
   - Calculate the total impact (lines changed, files affected)

5. **FINAL REPORT**:
   - Present organized summary in detected language
   - Highlight any critical changes or issues
   - Suggest next steps (commit, review, etc.)
