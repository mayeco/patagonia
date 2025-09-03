---
description: Description
---

# Title workflow

Description

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete within N steps, maximum. If it exceeds N steps, STOP. Ask for clarification.

**DECISION POINTS**: Make binary decisions. If \_\_\_ exceeds N steps, STOP. Ask for clarification.

**CONTENT VALIDATION**: Evaluate before proceeding. If \_\_\_ is not clear, ask for clarification.

**TERMINATION CONDITIONS**:

- Terminate when \_\_\_
- If \_\_\_ is not clear: Ask for clarification and STOP

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **START HERE**
   - Provide the initial input and objective.
