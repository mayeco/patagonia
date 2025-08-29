---
description: Evaluate understanding of requests, plans, backlog items, or current pending tasks
---

# Rate Request Workflow

Evaluate how well requests, plans, backlog items, or current pending tasks are understood before proceeding.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete evaluation within 6 steps maximum. Provide rating and either ask questions or proceed.

**DECISION POINTS**: Make binary decisions - content is clear enough to proceed or needs clarification.

**CONTENT ANALYSIS**: Evaluate clarity, completeness, and feasibility quickly.

**TERMINATION CONDITIONS**:
- If rating is 6-10: Provide explanation and recommend proceeding
- If rating is 1-5: Ask specific questions and STOP
- If user provides clarification: Re-evaluate and provide new rating
- Never proceed with implementation without user confirmation

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Determine the input type and source:
   - If input contains "plans/" or ".md", read and analyze the specified plan file
   - If input contains "backlog", retrieve and analyze current backlog items from memory
   - If input contains "pending" or "current", analyze current pending tasks from system memory
   - Otherwise, analyze the developer's general request
3. Analyze the content (plan, backlog, pending tasks, or request) to assess clarity and completeness
4. Rate the understanding on a scale of 1-10 in the detected language:
   - 1 = Very unclear, major gaps in understanding / Muy poco claro, grandes brechas en la comprensión
   - 10 = Perfectly clear, complete understanding / Perfectamente claro, comprensión completa
5. Provide a clear explanation of what is being evaluated in plain language and in the detected language
6. Highlight any assumptions that were made during interpretation in the detected language
7. If the score is low (1-5), ask specific clarifying questions in the detected language
8. If clarifications are provided and the input was a plan file, update the existing plan with the new information
9. Re-evaluate the updated plan and provide a new rating if changes were made
10. Do NOT proceed with coding, deployment, or execution until the developer confirms understanding
11. Wait for explicit developer confirmation before taking any implementation actions
12. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
