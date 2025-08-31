---
description: Workflow for obtaining documentation of frameworks, libraries, languages and technologies
---

# Documentation Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Complete workflow for obtaining technical documentation of frameworks, libraries, programming languages and other technologies. This workflow helps find, access and use documentation efficiently.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete documentation search within 8 steps maximum. If search takes longer than expected, use first available results.

**DECISION POINTS**: Make binary decisions quickly - use first relevant result found. Do not compare multiple options extensively.

**SEARCH LIMITATIONS**: Execute search commands directly. If search fails, use basic web search as fallback.

**TERMINATION CONDITIONS**:
- If no documentation found after 3 search attempts: Provide best available alternative
- If user specifies specific technology: Focus search on that technology only
- If search commands fail: Use basic web search as fallback
- If results found: Stop and present documentation

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **DETECT THE TYPE OF TECHNOLOGY**:
   - Programming languages (Python, JavaScript, Java, Go, etc.)
   - Frameworks (React, Angular, Vue, Django, Spring, etc.)
   - Libraries (NumPy, Pandas, Express, Lodash, etc.)
   - Tools (Docker, Kubernetes, Terraform, etc.)
   - Cloud services (AWS, GCP, Azure)
   - Databases (MongoDB, PostgreSQL, Redis, etc.)

2. **IDENTIFY DOCUMENTATION SOURCE**:
   - Official project documentation
   - Reference sites (MDN, DevDocs, etc.)
   - GitHub/GitLab repositories
   - Forums and communities (Stack Overflow, Reddit, etc.)
   - Courses and tutorials (freeCodeCamp, Udemy, etc.)
   - Technical blogs and articles

3. **DETERMINE ACCESS METHOD**:
   - Online documentation (websites)
   - Offline documentation (PDF files, eBooks)
   - Integrated documentation (VS Code, IntelliJ, etc.)
   - Command line (man pages, help commands)
   - Documentation APIs

4. **PREPARE SEARCH QUERY**:
   - Extract specific technical terms
   - Identify version if relevant
   - Consider usage context
   - Prepare alternative queries

5. **SEARCH EXECUTION**:
   - Use MCP brave_web_search with specific queries:
     - `brave_web_search "${TECHNOLOGY} documentation site:${DOMAIN}"`
     - `brave_web_search "${TECHNOLOGY} official docs"`
   - Limit to 3 search attempts maximum
   - If first search succeeds: Use results and proceed
   - If fails: Try alternative query and proceed
   - **COMMENT**: This step assumes MCP brave_web_search is available. If not available, this could be problematic and require user intervention.

6. **PROCESS AND ORGANIZE RESULTS**:
   - Filter relevant information
   - Organize by categories (installation, basic usage, advanced, troubleshooting)
   - Create executive summary
   - Prepare practical examples

**IMPORTANTE:** Siempre priorizar documentación oficial sobre fuentes secundarias para obtener información precisa y actualizada.