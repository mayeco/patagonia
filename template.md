---
description: Description
---

# Title workflow

Description

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete within N steps, maximum. If it exceeds N steps, STOP. Ask for clarification.

**DECISION POINTS**: Make binary decisions. If \_\_\_ exceeds N steps, STOP. Ask for clarification.

**CONTENT VALIDATION**: Evaluate before proceeding. If \_\_\_ is not clear, ask for clarification.

**EFFICIENCY OPTIMIZATION**: Leverage session context cache when available. Batch related operations to minimize overhead.

**TERMINATION CONDITIONS**:

- Terminate when \_\_\_
- If \_\_\_ is not clear: Ask for clarification and STOP

## STEPS

0. **OPTIMIZED LANGUAGE DETECTION**:
   - Check session language cache first (if available)
   - If cached with high confidence: Use cached language preference
   - If not cached or low confidence: Detect user's input language (default to Spanish if not clearly English)
   - Additionally, infer from recent previous messages; if unclear, default to Spanish
   - Cache detection result for session efficiency
   - Always provide responses in Spanish by default, unless developer clearly specifies English

1. **START HERE**
   - Provide the initial input and objective
   - Leverage session context cache when available for efficiency
