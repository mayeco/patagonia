---
description: Evaluate understanding of requests, plans, backlog items, or current pending tasks
---

# Rate Request Workflow

Evaluate how well requests, plans, backlog items, or current pending tasks are understood before proceeding.

# Rate Request Workflow

Evaluate how well requests, plans, backlog items, or current pending tasks are understood before proceeding.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete evaluation within 6 steps maximum. Provide rating and either ask questions or proceed.

**DECISION POINTS**: Make binary decisions - content is clear enough to proceed or needs clarification.

**TERMINATION CONDITIONS**:
- If rating is 6-10: Provide explanation and recommend proceeding
- If rating is 1-5: Ask specific questions and STOP
- If user provides clarification: Re-evaluate and provide new rating
- Never proceed with implementation without user confirmation

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("rate", "evaluate", "understand"). Default to Spanish.

1. **CONTENT IDENTIFICATION** (Quick classification):
   - **Plan**: Keywords like "plan", "plans/", ".md file"
   - **Backlog**: Keywords like "backlog", "tasks", "todo"
   - **Pending**: Keywords like "pending", "current", "status"
   - **Request**: Default for other inputs

2. **CONTENT RETRIEVAL**:
   - **Plan**: Read specified .md file from `/plans/` directory
   - **Backlog**: Retrieve from system memory
   - **Pending**: Check current system state
   - **Request**: Use input directly

3. **CLARITY ASSESSMENT**:
   - Evaluate completeness (all required info present?)
   - Check specificity (clear requirements, deliverables?)
   - Assess feasibility (technically possible?)
   - Rate on 1-10 scale based on above criteria

4. **RATING DELIVERY**:
   - Provide numerical rating (1-10)
   - Explain evaluation criteria used
   - List specific strengths and weaknesses
   - If rating 6-10: Recommend proceeding
   - If rating 1-5: List specific clarification questions

5. **FOLLOW-UP HANDLING**:
   - If clarifications provided: Re-evaluate and provide new rating
   - If user confirms understanding: Acknowledge and stop
   - If user requests changes: Incorporate and re-evaluate

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
