---
description: Write pending tasks to system memory as epics with functionalities
---

# Write Backlog Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Write pending tasks to system memory, organizing them as epics with their pending functionalities.

# Write Backlog Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Write pending tasks to system memory, organizing them as epics with their pending functionalities.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete backlog creation within 6 steps maximum. If user provides too many items, prioritize and limit to essential features.

**DECISION POINTS**: Make binary decisions quickly - epic is well-defined or needs clarification.

**TERMINATION CONDITIONS**:
- If user doesn't provide epic title: Ask and STOP
- If no functionalities listed: Ask user to specify and STOP
- If user declines confirmation: STOP immediately
- Always require user confirmation before storing

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("backlog", "epic", "tasks"). Default to Spanish.

1. **EPIC CAPTURE**:
   - Ask user for epic title and description
   - Validate title is descriptive and specific
   - If title unclear: Ask for clarification and STOP

2. **FUNCTIONALITIES COLLECTION**:
   - Ask user to list functionalities (comma-separated)
   - Parse and validate each functionality
   - Limit to maximum 10 functionalities per epic
   - If no functionalities: Ask user to specify and STOP

3. **EPIC STRUCTURE CREATION**:
   - Create structured epic with title, description, date
   - Mark all functionalities as "pending"
   - Assign unique identifier to epic

4. **USER CONFIRMATION**:
   - Display complete epic structure
   - Ask user to confirm storage
   - If declined: STOP without storing
   - If approved: Proceed to storage

5. **MEMORY STORAGE**:
   - Store epic in system memory
   - Ensure persistence across sessions
   - Verify storage was successful

6. **COMPLETION CONFIRMATION**:
   - Confirm epic was stored successfully
   - Provide epic identifier for future reference
   - Suggest next steps for implementation

**Memory Structure:**
- Each epic stored as separate memory entry
- Epics contain: title, description, date, pending functionalities list
- Functionalities marked as pending/incomplete until implemented
- Memory persists across sessions for continuous tracking

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
