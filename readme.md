---
description: Generate or update README.md based on current application analysis
---

# README Generator Workflow

Generate or update a comprehensive README.md file based on the current application/project structure and code analysis.

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Analyze the project structure and identify key components:
   - Project type (web app, API, library, CLI tool, etc.)
   - Main programming languages and frameworks used
   - Key directories and their purposes
   - Configuration files and their roles
   - Entry points and main application files
3. Examine package.json, requirements.txt, or similar dependency files to understand:
   - Project dependencies and their purposes
   - Available scripts and commands
   - Project metadata (name, version, description, author)
4. Analyze key source files to understand:
   - Main functionality and features
   - Architecture patterns used
   - API endpoints or main functions (if applicable)
   - Database models or data structures
5. Generate a comprehensive README.md in the detected language with sections:
   - Project title and description
   - Installation instructions
   - Usage examples
   - API documentation (if applicable)
   - Project structure overview
   - Dependencies and requirements
   - Development setup
   - Contributing guidelines
   - License information
6. Include appropriate badges and links based on project type
7. Save the generated README.md to the project root
8. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

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