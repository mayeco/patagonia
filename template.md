---
description: Template
---

# Template

Template

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete ___ within N steps maximum. If ___ exceeds N steps, STOP. Ask for clarification.

**DECISION POINTS**: Make binary decisions ___ or ___. If ___ exceeds N steps, STOP. Ask for clarification.

**CONTENT VALIDATION**: Evaluate ___ before proceeding. If ___ is not clear, ask for clarification.

**TERMINATION CONDITIONS**:
- Terminate when ___
- If ___ is not clear: Ask for clarification and STOP

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. ___START HERE__
   - Provide the initial input and objective.
