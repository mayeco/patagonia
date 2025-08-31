---
description: Write pending tasks to system memory as epics with functionalities
---

# Write Backlog Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Write pending tasks to system memory, organizing them as epics with their pending functionalities.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete backlog creation within 6 steps maximum. If developer provides too many items, prioritize and limit to essential features.

**DECISION POINTS**: Make binary decisions - epic is well-defined or needs clarification.

**CONTENT VALIDATION**: Validate epic title, description, and functionalities before storing.

**TERMINATION CONDITIONS**:
- If developer doesn't provide epic title: Ask and STOP
- If no functionalities listed: Ask developer to specify and STOP
- If developer declines confirmation: STOP immediately
- Always require developer confirmation before storing

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **EPIC CAPTURE**:
   - Capture the epic title and description from the user in the detected language

2. **FEATURE COLLECTION**:
   - Collect the list of features that need to be implemented (comma-separated) in the detected language

3. **EPIC CREATION**:
   - Create structured epics in system memory with:
      - Epic title and description
      - Date of creation
      - List of pending functionalities (marked as incomplete)

4. **EPIC STORAGE**:
   - Store each epic in system memory for future reference and tracking

5. **DISPLAY EPICS**:
   - Display the epics with their pending functionalities in a clear, organized format

6. **VALIDATION**:
   - Ensure all epics and functionalities are properly stored and easily retrievable

7. **UPDATE HANDLING**:
   - If the developer provides new information or changes requirements, re-evaluate and update the backlog accordingly

8. **CONFIRMATION**:
   - If the developer confirms the backlog, proceed with implementation

**Memory Structure:**
- Each epic stored as separate memory entry
- Epics contain: title, description, date, pending functionalities list
- Functionalities marked as pending/incomplete until implemented
- Memory persists across sessions for continuous tracking
