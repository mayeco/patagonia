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

- If content type unclear: Ask the developer for clarification and STOP
- If explanation becomes too complex: Simplify and provide basic explanation
- If the developer requests specific format: Adapt and complete
- Always provide explanation within 5 minutes of processing

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **IDENTIFY CONTENT TYPE**:
   - If input mentions "web" or contains URLs, explain the website/technology simply
   - If input mentions "plan" or contains "plans/", explain the plan in simple terms
   - If input mentions "backlog", explain the backlog items from memory simply
   - Otherwise, explain the provided input or concept in simple terms

2. **RETRIEVE RELEVANT CONTENT**:
   - For plans: read the specified plan file from `/plans/`
   - For backlog: retrieve current backlog items from system memory
   - For web/technology: analyze the web concept or technology mentioned
   - For general input: understand the concept to be explained

3. **BREAK DOWN THE CONCEPT**:
   - Use analogies a 5-year-old would understand

4. **EXPLAIN SIMPLY**:
   - Use simple words, short sentences, and relatable examples (toys, games, everyday activities)
   - Use MCP search brave_web_search for comprehensive web searches:
      - `brave_web_search "explain like i'm five {concept}"`
      - `brave_web_search "{concept} explanation for children"`
      - `brave_web_search "easy explanation of {concept}"`

5. **USE VISUAL METAPHORS**:
   - Avoid technical jargon completely

6. **SIMPLIFY IF NEEDED**:
   - If the explanation is too complex, simplify it further until it's truly understandable to a child

7. **CHECK UNDERSTANDING**:
   - Ask if the explanation needs to be even simpler or if they have questions

**ELI5 Style Guidelines:**

- Use words a 5-year-old knows (no technical terms)
- Compare to toys, games, or everyday activities
- Use short sentences and simple structure
- Ask questions to check understanding
- Use lots of examples and analogies
