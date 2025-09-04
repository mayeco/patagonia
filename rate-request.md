---
description: Evaluate understanding of requests, plans, backlog items, or current pending tasks
---

# Rate Request Workflow

Evaluate how well requests, plans, backlog items, or current pending tasks are understood before proceeding.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete evaluation within 6 steps, maximum. Provide a rating and either ask questions or proceed.

**DECISION POINTS**: Make binary decisions - the content is clear enough to proceed or needs clarification.

**CONTENT ANALYSIS**: Evaluate clarity, completeness, and feasibility quickly.

**TERMINATION CONDITIONS**:

- If rating is 6-10: Provide an explanation and recommend proceeding
- If rating is 1-5: Ask specific questions and STOP
- If the developer provides clarification: Re-evaluate and provide a new rating
- Never proceed with implementation without the developer's confirmation

## STEPS

{% include _includes/language-detection.md %}

1. **INPUT TYPE AND SOURCE**:
   - If input contains "plans/" or ".md", read and analyze the specified plan file
   - If input contains "backlog", retrieve and analyze current backlog items from memory
   - If input contains "pending" or "current", analyze current pending tasks from system memory
   - Otherwise, analyze the developer's general request

2. **CONTENT ANALYSIS**:
   - Assess clarity and completeness of the content (plan, backlog, pending tasks, or request)

3. **RATE UNDERSTANDING (1-10)**:
   - Provide rating in the detected language
   - 1 = Very unclear, major gaps in understanding
   - 10 = Perfectly clear, complete understanding

4. **EXPLAIN EVALUATION**:
   - Provide a clear plain-language explanation in the detected language

5. **LIST ASSUMPTIONS**:
   - Highlight any assumptions made during interpretation

6. **ASK CLARIFYING QUESTIONS (IF 1-5)**:
   - Ask specific clarifying questions in the detected language

7. **UPDATE PLAN (IF APPLICABLE)**:
   - If clarifications are provided and the input was a plan file, update the existing plan

8. **RE-EVALUATE AND RE-RATE (IF CHANGED)**:
   - Re-evaluate the updated plan and provide a new rating if changes were made

9. **DO NOT PROCEED WITHOUT CONFIRMATION**:
   - Do not proceed with coding, deployment, or execution until the developer confirms understanding

10. **WAIT FOR CONFIRMATION**:

- Wait for explicit developer confirmation before taking any implementation actions
