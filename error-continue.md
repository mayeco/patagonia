---
description: AI protocol for continuing reasoning, implementation, or conversation after an error in the IDE
auto_execution_mode: 1
---

# AI Workflow: Error Recovery Protocol

When an error occurs (e.g., "Cascade error: Internal: stream error: stream ID 1893; INTERNAL_ERROR; received from peer"), follow these steps to recover and continue the task:

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete error recovery within 9 steps, maximum.

**DECISION POINTS**: Make binary decisions - the error is recoverable or requires escalation.

**VALIDATION**: Validate the error type and recovery options.

**TERMINATION CONDITIONS**:

- If the error is unrecoverable: Ask the developer for manual intervention and STOP
- If recovery fails: Provide fallback options and STOP
- Always attempt recovery before escalating

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **REVIEW PREVIOUS REASONING**:
   - Return to the last reasoning step before the error.
   - Analyze the logic, assumptions, and actions that led to the failure.
   - Identify possible causes such as incorrect assumptions, tool misuse, or unforeseen edge cases.

2. **MAKE NEW DECISION**:
   - Using the insights from the reasoning review.
   - Decide on the best course of action: retry the operation, use a different approach, or escalate if necessary.

3. **RETRY FAILED OPERATION**:
   - If the new decision indicates retry is appropriate, attempt the last tool call, command execution or action again.

4. **FALLBACK STRATEGIES**:
   - If tool call failed, use alternative tools or manual approaches.
   - If conversation stream broke, summarize previous context and restart from last checkpoint.

5. **NOTIFY DEVELOPER TRANSPARENTLY**:
   - Clearly inform the developer of the error and recovery steps taken, without alarming them.

6. **RESUME TASK SEAMLESSLY**:
   - Continue the implementation or reasoning from the last valid state, using available context or memories.

7. **PREVENT FUTURE ERRORS**:
   - If applicable, adjust behavior (e.g., smaller tool calls, error handling in code).

## Example Implementation

- Error during code edit: Retry edit with smaller changes, other tools or use MultiEdit.
- Error in data fetching: Switch to manual file reading or search tools.
- Always prioritize the developer's task completion over error details.
