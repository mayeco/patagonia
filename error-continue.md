---
description: AI protocol to resume from the last failed step
auto_execution_mode: 1
---

# Continue From Failure Protocol

When the previous step fails (e.g., a tool error such as "Cascade error: Internal: stream error: stream ID 1893; INTERNAL_ERROR; received from peer", a network interruption, or a partial execution), treat the prompt as a signal to resume from the failure point. Do not attempt to "solve the error message" generically; instead, follow these steps to continue the task from the last valid state:

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete error recovery in at most 9 steps.

**DECISION POINTS**: Make binary decisions: either the error is recoverable or it requires escalation.

**VALIDATION**: Validate the error type and recovery options.

**TERMINATION CONDITIONS**:

- If the error is unrecoverable: Ask the developer for manual intervention and STOP.
- If recovery fails: Provide fallback options and STOP.
- Always attempt recovery before escalating.

## STEPS

{% include _includes/language-detection.md %}

1. **REVIEW FAILURE CONTEXT**:
   - Treat the developer's prompt as a signal that the previous step failed, not a request to debug an error message.
   - Reconstruct the last known good state and the exact point where execution stopped.
   - Summarize what is done vs. pending and what was being attempted when it failed.
   - Focus on what is needed to continue from that point; only analyze the error details if strictly required to proceed. Do not try to solve the error.

2. **MAKE NEW DECISION**:
   - Use the insights from the reasoning review.
   - Decide on the best course of action: retry the operation, use a different approach, or escalate if necessary.

3. **RETRY FAILED OPERATION**:
   - If the new decision indicates that a retry is appropriate, attempt the last tool call, command execution, or action again.
   - If the tool call failed, use alternative tools; retry with smaller changes or smaller steps; or use a batch or manual approach.
   - If the conversation stream broke, summarize the previous context and restart from the last checkpoint.

4. **NOTIFY DEVELOPER TRANSPARENTLY**:
   - Clearly inform the developer of the error and recovery steps taken, without alarming them.

5. **RESUME TASK SEAMLESSLY**:
   - Continue the implementation or reasoning from the last valid state, using available context or memories.

6. **PREVENT FUTURE ERRORS**:
   - If applicable, adjust behavior (e.g., smaller tool calls, error handling in code).

## Possible errors to handle

- Error during code edit: Retry the edit with smaller changes, use other tools, or use MultiEdit.
- Error in data fetching: Switch to manual file reading or search tools.
- Always prioritize the developer's task completion over error details.
