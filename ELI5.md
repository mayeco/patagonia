---
description: Explain concepts in simple terms like to a 5-year-old
---

# ELI5 Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Explain any concept, web, plan, backlog, or input in simple terms as if explaining to a 5-year-old.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete explanation within 6 steps maximum. If concept is too complex, provide basic explanation and stop.

**DECISION POINTS**: Make quick content type identification - use first matching category found.

**CONTENT LIMITATIONS**: Keep explanations simple and short. Use analogies appropriate for a 5-year-old.

**TERMINATION CONDITIONS**:
- If content type unclear: Ask user for clarification and STOP
- If explanation becomes too complex: Simplify and provide basic explanation
- If user requests specific format: Adapt and complete
- Always provide explanation within 5 minutes of processing

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Identify the type of content to explain:
   - If input mentions "web" or contains URLs, explain the website/technology simply
   - If input mentions "plan" or contains "plans/", explain the plan in simple terms
   - If input mentions "backlog", explain the backlog items from memory simply
   - Otherwise, explain the provided input or concept in simple terms
3. Retrieve the relevant content:
   - For plans: read the specified plan file from `/plans/`
   - For backlog: retrieve current backlog items from system memory
   - For web/technology: analyze the web concept or technology mentioned
   - For general input: understand the concept to be explained
4. Break down the concept into the simplest possible terms using analogies a 5-year-old would understand
5. Explain using simple words, short sentences, and relatable examples (toys, games, everyday activities)
   - Use MCP search brave_web_search for comprehensive web searches:
     - `brave_web_search "explain like i'm five {concept}"`
     - `brave_web_search "{concept} explanation for children"`
     - `brave_web_search "easy explanation of {concept}"`
6. Use visual metaphors and avoid technical jargon completely
7. PROVIDE THE EXPLANATION IN SPANISH by default (unless the user clearly specifies English)
8. If the explanation is too complex, simplify it further until it's truly understandable to a child
9. Ask if the explanation needs to be even simpler or if they have questions

**Language Support:**
- **Spanish**: DEFAULT - Explicar en español para TODA entrada, usando lenguaje infantil simple
- **English**: SOLO si el usuario especifica claramente "explain in English" o usa términos técnicos en inglés
- **Other**: Siempre responder en español por defecto

**IMPORTANT:** Always default to Spanish explanations unless the user explicitly requests English.

**ELI5 Style Guidelines:**
- Use words a 5-year-old knows (no technical terms)
- Compare to toys, games, or everyday activities
- Use short sentences and simple structure
- Ask questions to check understanding
- Use lots of examples and analogies