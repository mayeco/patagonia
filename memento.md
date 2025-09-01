---
description: Reset the current conversation reasoning context (without deleting persistent Memories)
---

# Memento: Conversation Context Reset

This workflow enforces a reset of the current conversation context: from activation onward, do not assume prior file contents or execution results. It does not delete persistent Memories.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete any iterative reasoning loop within 3 steps maximum. If a loop would exceed 3 steps, STOP and ask for clarification.

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **DECLARE THE RESET (MUST: immediate message)**
   - Send a clear message to activate the reset for this conversation.
   - Suggested template:

```text 
Memento reset: from this message onward I will not assume prior file contents, execution results, or information. Everything will be re-verified from the current state.
```

   - Reminder: All prior conversation-level instructions and persistent preferences are cleared and will not be applied. Only rules stated after this reset will be considered.

```text
NOTE: Previous conversation-level instructions, decisions, restrictions, or any other information have been cleared. Only rules stated after this message will be applied.
```

2. **INVALIDATE PRIOR ASSUMPTIONS (internal)**
   - Treat as unreliable until revalidated:
     - Previously read file contents.
     - Results from previously executed commands/scripts.
     - Prior external API/service responses.
     - Previous file paths or directories.
     - Decisions or conclusions derived from earlier states.
     - Temporary variables or intermediate artifacts.
     - Environment settings (e.g., paths, envs, tooling).
     - Everything that has not been re-verified.
     - Conversation-level instructions or implicit rules (e.g., "always use xyz", "always reply in Klingon", default paths/envs/tooling). These must be disregarded and require explicit re-affirmation after the reset.

3. **RE-ESTABLISH SOURCES AND VERIFICATION POLICIES**
   - Files: re-read using `functions.Read` with absolute paths before citing.
   - Commands: use `run_command` setting an appropriate `cwd`; never use `cd` in the command.
   - Find by name: use `functions.find_by_name` to find files and directories before citing.
   - Directory: use `functions.list_dir` to list directory contents before citing.
   - Search: use `functions.grep_search` to search for content before citing.
   - Web: use `read_url_content` to fetch documentation/resources again.
   - Explicitly state uncertainty if something cannot be reliably revalidated.

5. **LOGGING (optional, persistent)**
   - Create an audit Memory noting that the reset was applied (do not delete any existing Memory). Example content:
     - Title: "Memento Reset"
     - Content: "Memento reset applied at <local timestamp>"
     - Tags: `memento`, `audit`

6. **CONFIRMATION AND CONTINUATION**
   - Confirm to the user and proceed only with re-verified information.
   - Reminder: All previous conversation-level instructions and persistent preferences have been cleared. Only rules restated after the reset will be applied.

```text
Memento reset applied. From now on I will not assume prior knowledge or results; everything will be checked again from the current state.
```

## TERMINATION CONDITIONS

- Finish when the reset confirmation is sent and no unverified assumptions remain.
- If the reset scope is unclear: ask for clarification and STOP.