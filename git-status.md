---
description: Check the current Git status and analyze any pending changes in the repository
---

# Git Status Workflow

Check the current Git status and analyze any pending changes in the repository.

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("git", "status", "changes"). Default to Spanish.

1. **REPOSITORY VALIDATION**:
   - Execute: `git rev-parse --git-dir`
   - If fails: STOP - "Current directory is not a git repository"
   - If succeeds: Proceed to step 2

2. **STATUS EXECUTION**:
   - Execute: `git status --porcelain`
   - If command fails: STOP - "Git command failed - ensure git is installed"
   - Parse output for file states (modified, added, deleted, untracked)
   - Count total changes (limit analysis to first 20 files)
   - If no changes: STOP - "Repository is clean"

3. **CHANGES ANALYSIS** (Limited scope):
   - For first 5 modified files: Execute `git diff --stat <filename>`
   - If command fails: STOP - "Git diff failed - ensure git is installed"
   - Extract basic change statistics (lines added/removed)
   - Skip binary files and large files (>1MB)
   - If more than 20 files changed: Focus on summary only

4. **CONTENT SUMMARIZATION**:
   - Group files by type (code, config, docs, assets)
   - Provide high-level summary of changes
   - Identify potentially important files (package.json, README, etc.)
   - Calculate total impact (lines changed, files affected)

5. **FINAL REPORT**:
   - Present organized summary in detected language
   - Highlight any critical changes or issues
   - Suggest next steps (commit, review, etc.)

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
