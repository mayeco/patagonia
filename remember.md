---
description: Persist durable instructions across the workspace and auto-apply them in future tasks
---

# Remember Workflow

Persist developer-provided instructions and preferences to memory (scoped to this workspace) and auto-apply them across tasks. Follow the Memory Workflow defaults: when intent is ambiguous but information is durable/high-signal, default to create; prefer update if a semantically related memory already exists.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete remember operation within 6 structured steps. If instructions are overly broad, request clarification and STOP.

**DECISION POINTS**: Determine if the instruction is durable vs ephemeral, safe vs sensitive, and whether to create or update.

**CONTENT VALIDATION**: Ensure instructions are clear, scoped (workspace by default), and non-conflicting. If conflicting with existing memory, ask whether to overwrite or merge.

**PRIVACY**: Do not store secrets, tokens, or sensitive personal data. If present, mask and ask the developer how to proceed.

**TERMINATION CONDITIONS**:
- If instructions are unclear/ephemeral: Ask for clarification and STOP
- If developer declines confirmation: STOP immediately
- Always require developer confirmation before storing or updating

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **COLLECT INSTRUCTIONS TO REMEMBER**:
   - Extract and normalize: short title (≤60 chars), detailed description/body, category (e.g., style/tooling/workflow/privacy), scope (workspace by default), and suggested tags.
   - Validate that instructions are durable (persist beyond current task), broadly applicable, and non-sensitive.

2. **RETRIEVE EXISTING MEMORY**:
   - Use the Memory Workflow to search for semantically related entries tagged `remember`/`workspace_prefs` in this workspace corpus.
   - If a related memory exists, plan to update it; otherwise plan to create a new entry.

3. **EXECUTE MEMORY OPERATION**:
   - If related memory exists: update using its Id. If intent is ambiguous and info is durable/high-signal: default to create.
   - Fields when creating/updating:
     - Title: `Remember: <short title>`
     - Content: structured block including instructions, scope (`workspace`), applicability (`all tasks unless conflict`), and any examples.
     - Tags: `remember`, `workspace_prefs`, `guideline`
     - CorpusNames: `patagonia_workflows` (only when creating)
     - UserTriggered: `true`

4. **CONFIRM STORAGE**:
   - Output a concise summary of what was stored/updated and show the memory Id for reference.

5. **AUTO-APPLY NOW**:
   - Acknowledge that these instructions are now active for the current session and should be applied on subsequent requests unless they conflict with explicit user instructions.

6. **RETRIEVE FOR FUTURE SESSIONS**:
   - At the start of future sessions, retrieve and apply all `remember` memories in this workspace automatically.

7. **MODIFY OR REMOVE (OPTIONAL)**:
   - On explicit developer request only, update or delete the relevant memory. Otherwise, keep it active.
