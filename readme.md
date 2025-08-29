---
description: Generate or update README.md based on current application analysis
---

# README Generator Workflow

Generate or update a comprehensive README.md file based on the current application/project structure and code analysis.

# README Generator Workflow

Generate or update a comprehensive README.md file based on the current application/project structure and code analysis.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete README generation within 8 steps maximum. If project analysis takes too long, use available information and proceed.

**DECISION POINTS**: Make binary decisions quickly - include section or skip based on available information.

**TERMINATION CONDITIONS**:
- If no project structure found: Generate basic template and stop
- If README.md already exists: Ask user if they want to overwrite
- If generation completes: Save file and provide summary
- Always provide README content or clear error message

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("readme", "documentation", "generate"). Default to Spanish.

1. **PROJECT ANALYSIS**:
   - Scan current directory for project files
   - Identify main programming languages
   - Detect project type (web app, API, library, CLI)
   - Check for existing README.md

2. **DEPENDENCY ANALYSIS**:
   - Read package.json, requirements.txt, or similar files
   - Extract project name, version, description
   - Identify key dependencies and scripts
   - Note installation requirements

3. **CODE STRUCTURE ANALYSIS** (Limited scope):
   - Examine main entry points (index.js, main.py, etc.)
   - Identify key directories (src/, lib/, api/)
   - Note any configuration files
   - Skip detailed code analysis to avoid loops

4. **CONTENT GENERATION**:
   - Create title and description from project data
   - Generate installation instructions
   - Add basic usage examples
   - Include project structure overview
   - Add development setup section

5. **FORMATTING AND VALIDATION**:
   - Ensure proper markdown syntax
   - Add relevant badges if applicable
   - Validate all links and references
   - Check for completeness

6. **FILE OUTPUT**:
   - Save to ./README.md
   - Preserve existing README if user chooses not to overwrite
   - Include generation timestamp

7. **COMPLETION REPORT**:
   - Confirm successful generation
   - Provide file location and summary
   - Suggest next steps (customization, review)

**Language Support:**
- **Spanish**: DEFAULT - Generar README en español para toda entrada
- **English**: Generate README in English only if explicitly requested
- **Other**: Generate README in Spanish as default, but adapt to detected language when possible

**README Sections Generated:**
- Título del proyecto y descripción
- Instalación y requisitos
- Uso y ejemplos
- Estructura del proyecto
- API (si aplica)
- Desarrollo y contribución
- Licencia