---
description: Generate feature documents for small, specific features without implementation planning
---

# Write Feature Workflow

Generate concise feature documents for small, specific features. This workflow focuses on documenting feature requirements and details without creating implementation plans or suggesting code changes.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete feature documentation within 4 steps maximum.

**DECISION POINTS**: Make binary decisions - feature is simple enough or needs project planning.

**TERMINATION CONDITIONS**:

- If the feature description is unclear: Ask for clarification and STOP
- If feature complexity is "Complex": Suggest the write-project workflow and STOP
- Always require the developer's confirmation before proceeding

## STEPS

{% include _includes/language-detection.md %}

1. **FEATURE CAPTURE**:
   - Ask the developer for a specific feature description
   - Validate that the feature is small and concrete (not complex)
   - If too complex: STOP - "This seems like a project, use the write-project workflow"

2. **FEATURE TYPE DETECTION**:
   - Analyze the feature description for type indicators:
     - **UI/UX**: Keywords like "interface", "design", "user experience", "layout", "styling"
     - **Functionality**: Keywords like "function", "logic", "algorithm", "calculation", "processing"
     - **Integration**: Keywords like "API", "database", "external service", "third-party", "connect"
     - **Data**: Keywords like "storage", "retrieval", "query", "filter", "sort", "display"
     - **Security**: Keywords like "authentication", "authorization", "validation", "encryption"
     - **Performance**: Keywords like "speed", "optimization", "loading", "response time"
   - Validate the feature type against the description
   - If unclear: Ask the developer to specify the feature type and STOP

3. **FEATURE DOCUMENTATION**:
   - Capture key details:
     - Feature name and brief description
     - Feature type
     - User story or acceptance criteria (if provided)
     - Any specific requirements or constraints
   - Keep the documentation minimal and focused

4. **DEVELOPER CONFIRMATION**:
   - Present the feature document draft
   - Ask for explicit confirmation to save
   - If declined: STOP without saving

5. **FEATURE STORAGE**:
   - Save to `/features/{{date}}-{{feature_name | slugify}}.md`
   - Confirm file creation was successful
   - End workflow after saving
