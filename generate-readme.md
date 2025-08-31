---
description: Generate or update README.md based on current application analysis
---

# README Generator Workflow

Generate or update a comprehensive README.md file based on the current application/project structure and code analysis.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete README generation within 8 steps maximum.

**DECISION POINTS**: Make binary decisions - project structure is clear or needs clarification.

**VALIDATION**: Validate project files and structure before generation.

**TERMINATION CONDITIONS**:
- If no project structure found: Ask the developer for details and STOP
- If language detection fails: Default to Spanish and continue
- Always generate README in detected language

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **ANALYZE PROJECT STRUCTURE**:
   - Project type (web app, API, library, CLI tool, etc.)
   - Main programming languages and frameworks used
   - Key directories and their purposes
   - Configuration files and their roles
   - Entry points and main application files

2. **EXAMINE DEPENDENCY FILES**:
   - Project dependencies and their purposes
   - Available scripts and commands
   - Project metadata (name, version, description, author)

3. **ANALYZE KEY SOURCE FILES**:
   - Main functionality and features
   - Architecture patterns used
   - API endpoints or main functions (if applicable)
   - Database models or data structures

4. **GENERATE README CONTENT**:
   - Project title and description
   - Installation instructions
   - Usage examples
   - API documentation (if applicable)
   - Project structure overview
   - Dependencies and requirements
   - Development setup
   - Contributing guidelines
   - License information

5. **ADD BADGES AND LINKS**:
   - Include appropriate badges and links based on project type

6. **SAVE README**:
   - Save the generated README.md to the project root
   - Ensure correct file encoding and formatting