---
description: Workflow to store, update, and delete persistent AI memories using the memory tool
---

# Memory Workflow

Guidelines for using the memory tool to persist important context across sessions.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete backlog creation within 10 steps maximum. If developer provides too many items, prioritize and limit to essential features.

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
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **INTENT CLASSIFICATION**:
   - Determine intent: create, update, delete, or use existing memories in response.
   - If intent is implicit or ambiguous and information is durable and high-signal, default to create.

2. **FIND EXISTING MEMORY**:
   - Search for semantically related memories.
   - If related memory exists, prefer update/append over create.

3. **PREPARE MEMORY PAYLOAD (from most recent conversations)**:
   - Source window: extract durable, high-signal facts from the latest conversation turns (typically last 5–10 relevant messages).
   - Title: concise, descriptive.
   - Content: clear, specific details that capture what is currently being discussed and that will help future tasks (e.g., decisions, confirmed preferences, constraints, standards).
   - Tags: snake_case keywords for retrieval.
   - UserTriggered: true only if the developer explicitly asked to save/update memory.
   - For delete operations: leave Content blank and set Action to delete with the target Id.
   - CorpusNames: `patagonia_workflows` (only when creating)

4. **EXECUTE MEMORY OPERATION**:
   - Create when no related memory exists.
   - If intent is ambiguous and no explicit operation is requested, default to create.
   - Update when a related memory exists (use its Id).
   - Delete only when explicitly requested or when correcting incorrect/outdated info.

5. **VALIDATE AND CONFIRM**:
   - Verify the operation succeeded.
   - Summarize what was stored/updated/deleted without exposing secrets.

6. **PRIVACY AND SAFETY**:
   - Do not store secrets, tokens, credentials, or sensitive PII.
   - Avoid volatile data; store stable, reusable context.

7. **USE MEMORIES IN RESPONSES**:
   - When relevant memories inform an action, acknowledge them briefly.
   - Treat outdated memories cautiously and update them when discovered.
