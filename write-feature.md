---
description: Generate implementation plans for small, specific features
---

# Write Feature Workflow

Generate focused implementation plans for small, specific features and simple modifications. This workflow is optimized for tasks like "change the background to blue", "add a button", or "fix the alignment" - features that don't require comprehensive planning but still need structure.

## Important Notes

- **Fetch external websites when needed** - This workflow can analyze external websites to gather requirements and context
- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis
- **Focus on practical implementation** - Emphasize actionable steps for small, concrete features

# Write Feature Workflow

Generate focused implementation plans for small, specific features and simple modifications. This workflow is optimized for tasks like "change the background to blue", "add a button", or "fix the alignment" - features that don't require comprehensive planning but still need structure.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete feature planning within 6 steps maximum. If feature is too complex, suggest using write-plan workflow instead.

**DECISION POINTS**: Make binary decisions quickly - feature is simple enough or too complex for this workflow.

**TERMINATION CONDITIONS**:
- If feature description unclear: Ask for clarification and STOP
- If feature complexity is "Complex": Suggest write-plan and STOP
- If user declines confirmation: STOP immediately
- Always require user confirmation before proceeding

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("feature", "implement", "small"). Default to Spanish.

1. **FEATURE DESCRIPTION CAPTURE**:
   - Ask user for specific feature description
   - Validate description is concrete and actionable
   - If description too vague: Ask for specifics and STOP

2. **COMPLEXITY ASSESSMENT**:
   - Evaluate feature against complexity guidelines
   - Classify as Simple, Moderate, or Complex
   - If Complex: Suggest write-plan workflow and STOP

3. **IMPLEMENTATION PLAN GENERATION**:
   - Identify specific files to modify
   - Create step-by-step implementation actions
   - Include technical details and code changes
   - Estimate time based on complexity

4. **USER CONFIRMATION**:
   - Present complete feature plan
   - Ask for explicit confirmation to proceed
   - If declined: STOP without saving
   - If approved: Proceed to save

5. **PLAN STORAGE**:
   - Save to `/features/{{date}}-{{feature_name | slugify}}.md`
   - Confirm file creation successful
   - Provide plan summary and next steps

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