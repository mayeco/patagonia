---
description: Explain concepts in simple terms like to a 5-year-old
---

# ELI5 Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

# ELI5 Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Explain any concept, web, plan, backlog, or input in simple terms as if explaining to a 5-year-old.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete explanation within 6 steps maximum. If concept is too complex, provide basic explanation and stop.

**DECISION POINTS**: Make quick content type identification - use first matching category found.

**TERMINATION CONDITIONS**:
- If content type unclear: Ask for clarification and STOP
- If explanation becomes too complex: Simplify and provide basic explanation
- If user requests specific format: Adapt and complete
- Always provide explanation within 5 minutes of processing

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("explain", "eli5", "simple"). Default to Spanish.

1. **CONTENT TYPE IDENTIFICATION** (Quick classification):
   - **Web/Tech**: Keywords like "website", "framework", "library", "API"
   - **Plan**: Keywords like "plan", "project", "implementation"
   - **Backlog**: Keywords like "backlog", "tasks", "todo"
   - **General**: Default category for other inputs

2. **CONTENT RETRIEVAL** (Execute immediately):
   - **Web/Tech**: Use MCP brave_web_search: `brave_web_search "${TOPIC} basics"`
   - **Plan**: Read plan file from `/plans/` directory
   - **Backlog**: Retrieve from system memory
   - **General**: Use input directly
   - If retrieval fails: Use available information and proceed

3. **SIMPLIFICATION PROCESS**:
   - Break complex terms into 1-2 word explanations
   - Use analogies: toys, games, daily activities
   - Limit explanation to 3-5 key points maximum
   - Remove technical jargon completely

4. **ANALOGY CREATION**:
   - Find relatable comparison (food, animals, games)
   - Ensure analogy is simple and accurate
   - Test analogy mentally: "Would a 5-year-old understand?"

5. **FINAL FORMATTING**:
   - Use short sentences (5-8 words maximum)
   - Include 1-2 examples
   - Add question to check understanding
   - Format as conversational explanation

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