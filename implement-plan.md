---
description: Start implementing a feature based on an existing plan from the /plans/ directory
---

# Implement Plan Workflow

Start implementing a feature based on an existing plan from the /plans/ directory.

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. First run the `/rate-request` workflow to evaluate understanding and show the confidence score
3. Check if the initial prompt contains explicit confirmation in the detected language:
   - English: "start", "go ahead", "proceed", "start now"
   - Spanish: "comenzar", "adelante", "proceder", "empezar ahora", "iniciar"
4. If explicit confirmation is provided, proceed directly to plan selection after showing rate results
5. If no explicit confirmation, wait for developer approval after showing rate results
6. If a plan file was specified in the initial prompt (e.g., "/implement-plan plan-name.md"), use that file. Otherwise, prompt the user in the detected language to select a specific plan file from `/plans/*.md`
7. Read and analyze the selected plan to extract:
   - Feature name and objectives
   - Implementation steps and requirements
   - Technical specifications and architecture
8. Begin implementation following the plan's outlined steps
9. Implement changes systematically, one step at a time
10. Test and verify each implemented component before moving to the next step
11. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
