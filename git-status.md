---
description: Check the current Git status and analyze any pending changes in the repository
---

# Git Status Workflow

Check the current Git status and analyze any pending changes in the repository.

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Run `git status` to see the current state of the repository
3. For each modified file, run `git diff <filename>` to show detailed changes
4. Review and analyze both outputs to understand what files have been modified, added, or deleted
5. Provide a comprehensive explanation of the changes in the detected language, including:
   - Overview from git status (file states and untracked files)
   - Detailed changes from git diff (line-by-line modifications)
   - Added files and their content
   - Deleted files
   - Any untracked files
6. PROVIDE THE EXPLANATION IN SPANISH by default (unless the user clearly specifies English)
7. Highlight any potential issues or important changes that need attention

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
