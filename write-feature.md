---
description: Generate implementation plans for small, specific features
---

# Write Feature Workflow

Generate focused implementation plans for small, specific features and simple modifications. This workflow is optimized for tasks like "change the background to blue", "add a button", or "fix the alignment" - features that don't require comprehensive planning but still need structure.

## Important Notes

- **Fetch external websites when needed** - This workflow can analyze external websites to gather requirements and context
- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis
- **Focus on practical implementation** - Emphasize actionable steps for small, concrete features

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
1. Capture the feature description in the detected language:
   - English: "What small feature do you want to implement?"
   - Spanish: "¿Qué característica pequeña quieres implementar?"
2. Analyze the feature request to understand the scope and requirements
3. **Detect Feature Complexity**:
   - **Simple**: Single file changes, CSS modifications, basic functionality
   - **Moderate**: Multiple file changes, basic logic implementation
   - **Complex**: New components, significant logic, testing requirements
4. Generate a focused implementation plan in the detected language that includes:
   - **Feature Description**: Clear, concise description of what needs to be done
   - **Files to Modify**: Specific files that need changes
   - **Implementation Steps**: Step-by-step actions to complete the feature
   - **Technical Details**: Specific code changes, CSS classes, or logic needed
   - **Testing Requirements**: Basic verification steps
   - **Estimated Time**: Rough time estimate (minutes/hours)
   - **Any clarifications needed from the developer**
5. Rate the understanding of the request on a scale of 1-10 in the detected language:
   - 1 = Very unclear, major gaps in understanding / Muy poco claro, grandes brechas en la comprensión
   - 10 = Perfectly clear, complete understanding / Perfectamente claro, comprensión completa
6. Save the feature plan to `/features/{{date}}-{{feature_name | slugify}}.md`
7. Wait for explicit developer confirmation before proceeding with implementation
8. If clarification is needed, ask specific questions in the detected language
9. After receiving clarifications, rate the improved understanding and proceed
10. If the developer confirms the feature plan, proceed with implementation
11. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

## Feature Complexity Guidelines

### Simple Features (15-30 minutes):
- CSS changes (colors, fonts, spacing)
- Text modifications
- Basic attribute changes
- Simple form field additions

### Moderate Features (30-120 minutes):
- New components with basic functionality
- API endpoint modifications
- Database field additions
- Basic validation logic

### Complex Features (2+ hours):
- New pages/screens
- Complex business logic
- Integration with external services
- Significant UI/UX changes

## Implementation Focus Areas

### For Simple Features:
- Identify exact file and location
- Specify exact code changes
- Include before/after examples
- Note any dependencies

### For Moderate Features:
- Break down into smaller tasks
- Identify required components
- Include basic testing steps
- Note potential impact areas

### For Complex Features:
- Consider using write-plan workflow instead
- Provide high-level breakdown
- Identify potential challenges
- Recommend breaking into smaller features

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible