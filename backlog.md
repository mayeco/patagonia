---
description: Report the current backlog from existing context and optionally capture updates to memory
---

# Backlog Reporting Workflow

Report the current backlog from the existing context (memories and repository files). Then, if the developer provides changes, update the backlog in memory and re-display it.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete backlog reporting within 6 structured steps. If the developer provides too many items, prioritize and limit to essentials.

**DECISION POINTS**: Make binary decisions - backlog items are clear or need clarification.

**CONTENT VALIDATION**: Validate item titles, descriptions, and statuses before storing updates.

**TERMINATION CONDITIONS**:

- If no backlog found in context and the developer provides no items: Ask for items and STOP
- If developer declines confirmation: STOP immediately
- Always require developer confirmation before storing or updating backlog entries

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **DISCOVER EXISTING BACKLOG**:
   - Retrieve backlog-related memories (epics, features, tasks) using the Memory Workflow.
   - Scan repository context for backlog sources: `backlog.md`, `TODO*`, `plans/`, `epics/`, `features/`, `projects/`.
   - If nothing is found, state clearly: "No backlog found in current context" and proceed to Step 3.

2. **OUTPUT CURRENT BACKLOG**:
   - Present a concise, structured report:
     - Epics: title and short description
     - Features/Tasks per epic with status (pending/in_progress/completed)
     - Unassigned tasks, if any
   - Include references to sources (memory Ids and/or file paths).

3. **GAP CHECK AND QUESTIONS**:
   - Ask the developer to confirm accuracy and provide missing items or corrections.
   - If the developer supplies updates, proceed to Step 4; otherwise STOP.

4. **CAPTURE NEW/UPDATED ITEMS**:
   - Create/update backlog entries in memory (use the Memory Workflow conventions).
   - Store: epic title, description, created/updated date, and features/tasks with statuses.

5. **DISPLAY UPDATED BACKLOG**:
   - Re-output the full backlog after changes for confirmation, same structure as Step 2.

6. **VALIDATION**:
   - Ensure backlog entries are stored and easily retrievable with clear tags and titles.

7. **UPDATE HANDLING**:
   - On new information, repeat Steps 1–6 to keep the backlog current.

8. **CONFIRMATION**:
   - Ask the developer to confirm the backlog or specify next actions (e.g., implementation).

**Memory Structure:**

- Backlog entries (epics, features, tasks) stored as separate memory entries
- Each entry contains: title, description, status (pending/in_progress/completed), created/updated dates
- Relationships preserved via references (e.g., feature → parent epic)
- Memory persists across sessions for continuous tracking
