---
description: Do not proceed with coding, deployment, or execution. Wait for explicit developer confirmation
---

# No Continue Workflow

Do not proceed with coding, deployment, or execution. Wait for explicit developer confirmation.

## ⚠️ CRITICAL AI EXECUTION RULES

**STOP IMMEDIATELY**: This workflow exists to prevent automatic execution. Never proceed with any implementation.

**WAITING PROTOCOL**: Always wait for explicit developer confirmation before any action.

**STATUS REPORTING**: Provide current status and pending items clearly.

**TERMINATION CONDITIONS**:

- Always stop after providing status information
- Never execute any commands or make changes
- If developer requests specific action: Redirect to appropriate workflow
- This workflow is for status reporting only

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **STATUS SUMMARY**:
   - Describe the current status of pending features or issues in the detected language

2. **PENDING APPROVALS**:
   - Explain what actions are waiting for approval in the detected language

3. **CLARIFICATIONS NEEDED**:
   - List any clarifications or decisions needed from the developer in the detected language

4. **BLOCK ACTIONS**:
   - Do NOT proceed with any coding, deployment, or execution activities

5. **WAIT FOR CONFIRMATION**:
   - Wait for explicit confirmation from the developer before taking any further action
