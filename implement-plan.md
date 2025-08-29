---
description: Start implementing a feature based on an existing plan from the /plans/ directory
---

# Implement Plan Workflow

Start implementing a feature based on an existing plan from the /plans/ directory.

# Implement Plan Workflow

Start implementing a feature based on an existing plan from the /plans/ directory.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete workflow within 10 steps maximum. If implementation encounters issues, ask user for guidance and stop.

**DECISION POINTS**: Make binary decisions quickly - proceed with plan or ask for clarification.

**TERMINATION CONDITIONS**:
- If no plan specified: Ask user to specify plan and STOP
- If plan file doesn't exist: Provide error and STOP
- If user denies confirmation: STOP immediately
- If implementation hits blocker: Ask user for guidance and STOP
- Never proceed without explicit user confirmation

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("implement", "start", "plan"). Default to Spanish.

1. **RATE REQUEST EXECUTION**:
   - Execute `/rate-request` workflow on user's request
   - Display confidence score to user
   - Wait for user response (maximum 30 seconds)

2. **CONFIRMATION VALIDATION**:
   - Check user response for confirmation keywords
   - English: "yes", "start", "go ahead", "proceed", "confirm"
   - Spanish: "si", "comenzar", "adelante", "proceder", "confirmar"
   - If no confirmation: Ask again and STOP if still no

3. **PLAN SELECTION**:
   - If plan specified in request: Use that plan
   - If no plan specified: List available plans in `/plans/*.md`
   - Ask user to select specific plan
   - Validate plan file exists

4. **PLAN ANALYSIS**:
   - Read selected plan file
   - Extract key sections: objectives, steps, requirements
   - Identify implementation priority (critical first)
   - Validate plan completeness

5. **IMPLEMENTATION PREPARATION**:
   - Set up development environment
   - Create feature branch if needed
   - Prepare necessary files and directories

6. **STEP-BY-STEP EXECUTION**:
   - Start with first implementation step
   - Execute code changes as specified
   - Test each change immediately
   - If test fails: Ask user for guidance

7. **PROGRESS TRACKING**:
   - Mark completed steps
   - Update remaining work
   - Provide progress summary to user

8. **FINAL VALIDATION**:
   - Run comprehensive tests
   - Verify all requirements met
   - Prepare for integration

9. **COMPLETION REPORT**:
   - Summarize implemented features
   - List any remaining work
   - Suggest next steps

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
