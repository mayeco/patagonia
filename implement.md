---
description: Start implementing a feature, epic, project, or open text description
---

# Implement Plan Workflow

Start implementing a feature, epic, project based on existing plans, or process open text descriptions to create implementation plans.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete implementation within defined scope. If clarifications needed, identify specific plan and edit accordingly.

**INPUT FLEXIBILITY**: Support both structured plans and unstructured open text descriptions.

**PLAN IDENTIFICATION**: Always identify input type (epic/feature/project/plan/open text) and adapt implementation approach.

**ITERATION HANDLING**: If clarifications needed, edit existing plan or create structured plan from open text unless the developer explicitly requests "new one".

**TERMINATION CONDITIONS**:
- If no input specified: Ask the developer for description or plan reference and STOP
- If plan file doesn't exist: Create plan from open text description and save to `/plans/`
- If implementation hits blocker: Ask the developer for clarification and STOP
- Never proceed without developer confirmation

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **INPUT TYPE DETECTION**:
   - Analyze developer input for input type indicators:
     - **Epic**: Keywords like "epic", "large initiative", "strategic", "company objective"
     - **Project**: Keywords like "project", "initiative", "program", "implementation"
     - **Feature**: Keywords like "feature", "small", "task", "functionality"
     - **Plan Reference**: File paths, plan names, or explicit plan mentions
     - **Open Text**: General descriptions, requirements, or implementation requests
   - Check input for specific plan references (file paths, names, structured content)

2. **PLAN DISCOVERY** (For Structured Plans):
   - Scan all plan directories: `/plans/`, `/epics/`, `/features/`, `/projects/`
   - If specific plan mentioned: Look for exact match
   - If no specific plan: List available plans by type and ask the developer to select
   - Validate plan file exists and is readable

3. **OPEN TEXT PROCESSING** (For Unstructured Input):
   - Extract implementation requirements from open text description
   - Identify key components: what, why, how, success criteria
   - Determine appropriate implementation scope (feature, project, or epic level)
   - Create structured implementation plan from unstructured input
   - Ask for clarification on unclear requirements

4. **CONTENT ANALYSIS** (Type-Specific):
   - **Epic Plans**: Extract strategic objectives, stakeholder requirements, success metrics
   - **Project Plans**: Extract milestones, technical stack, resource requirements
   - **Feature Plans**: Extract implementation steps, dependencies, testing requirements
   - **Open Text**: Identify main goals, requirements, constraints, and success indicators
   - Identify any clarification points or missing information

2. **PLAN DISCOVERY**:
   - Scan all plan directories: `/plans/`, `/epics/`, `/features/`, `/projects/`
   - If specific plan mentioned: Look for exact match
   - If no specific plan: List available plans by type and ask user to select
   - Validate plan file exists and is readable

3. **PLAN ANALYSIS** (Type-Specific):
   - **Epic Plans**: Extract strategic objectives, stakeholder requirements, success metrics
   - **Project Plans**: Extract milestones, technical stack, resource requirements
   - **Feature Plans**: Extract implementation steps, dependencies, testing requirements
   - Identify any clarification points or missing information

4. **CLARIFICATION HANDLING**:
   - If plan has unclear sections: Identify specific areas needing clarification
   - For open text: Ask the developer for missing technical details, constraints, or success criteria
   - Edit existing plan with clarifications unless the developer requests "new one"
   - Ask the developer for missing information and update plan accordingly

5. **IMPLEMENTATION PREPARATION** (Type-Adapted):
   - **Epic**: Create project breakdown and prioritize features
   - **Project**: Set up development environment and team coordination
   - **Feature**: Prepare code environment and identify implementation order
   - **Open Text**: Create structured implementation plan and identify required resources
   - Create implementation roadmap based on input type

6. **STEP-BY-STEP EXECUTION**:
   - Follow plan-specific or text-derived implementation steps
   - Track progress against identified milestones or goals
   - Document completed work and update plan status
   - Test each component before proceeding

7. **PROGRESS TRACKING**:
   - Update plan with implementation progress
   - Mark completed items and identify next steps
   - Report status to relevant stakeholders based on input type

8. **QUALITY ASSURANCE** (Type-Specific):
   - **Epic**: Validate strategic alignment and business value delivery
   - **Project**: Ensure milestone deliverables and quality gates
   - **Feature**: Verify functionality and integration testing
   - **Open Text**: Validate against original requirements and success criteria
   - Document any deviations from original plan or requirements

9. **COMPLETION VALIDATION**:
   - Verify all requirements are met (from plan or open text)
   - Confirm success criteria are achieved
   - Update plan with final status and lessons learned

10. **FOLLOW-UP ACTIONS**:
    - Suggest next implementation phases
    - Identify potential improvements for future plans
    - Archive completed plan with implementation results
