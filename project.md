---
description: Generate comprehensive project plans with multiple features and milestones
---

# Write Project Workflow

Generate comprehensive project plans that span multiple features and milestones. Projects are medium to large initiatives that require coordination across multiple development cycles and team members.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete project planning within 10 steps maximum.

**DECISION POINTS**: Make binary decisions - project scope is manageable or too complex.

**TERMINATION CONDITIONS**:

- If no project description provided: Ask and STOP
- If project scope unclear: Ask for clarification and STOP
- Always require developer confirmation before creating

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **PROJECT CAPTURE**:
   - Ask the developer for project title and comprehensive description
   - Validate project involves multiple features (not a single feature)
   - If too narrow: STOP - "This seems like a feature, not a project"

2. **PROJECT TYPE DETECTION**:
   - Analyze project description for type indicators:
     - **MVP**: Keywords like "minimum viable product", "MVP", "prototype", "quick solution"
     - **Refactor**: Keywords like "refactor", "clean up", "improve code", "optimize", "restructure"
     - **New Feature**: Keywords like "new feature", "add functionality", "enhancement", "capability"
     - **Enhancement**: Keywords like "improve", "enhance", "upgrade", "better"
     - **Maintenance**: Keywords like "bug fix", "security", "patch", "update", "maintenance"
     - **Migration**: Keywords like "migrate", "upgrade", "move to", "switch to", "transition"
     - **Integration**: Keywords like "integrate", "connect", "third-party", "external service"
     - **Research/Spike**: Keywords like "research", "investigate", "explore", "spike", "proof of concept"
   - If project type is unclear assume it is a **MVP**, give a message to the developer to let them know (Do not skip the message).

3. **PROJECT PLANNING AND STRUCTURING**:
   - **IDENTIFY SCOPE DEFINITION**
     - Identify project objectives and success criteria based on project type
     - Estimate project timeline based on project type complexity

   - **SEARCH FOR IMPLEMENTATION DOCUMENTATION**
     - Perform an MCP search for the current project's implementation and type (run a comprehensive search to find relevant documentation for implementation details and type; be mindful of outdated documentation):
       - `brave_web_search "{relevant_content} {project_name} {project_type}"`

   - **FEATURE IDENTIFICATION**:
     - Break project into 5-12 major features
     - Group features into logical milestones

   - **TECHNICAL ARCHITECTURE** (Type-Aware):
     - Define technology stack based on project type requirements
     - Identify integration points and dependencies
     - Plan infrastructure and deployment requirements

   - **RISK ASSESSMENT** (Adapted to Project Type):
     - Identify potential risks specific to project type:
       - **MVP**: Market validation, technical feasibility
       - **Refactor**: Regression risks, performance impacts
       - **New Feature**: Integration complexity, user adoption
       - **Maintenance**: Security vulnerabilities, system stability
     - Define mitigation strategies and plan contingencies

   - **MILESTONE PLANNING** (Adapted to Project Type):
     - Create milestones appropriate for project type:
       - **MVP**: Focus on core functionality milestones
       - **Refactor**: Code quality improvement milestones
       - **New Feature**: Feature development and integration milestones
       - **Maintenance**: Risk mitigation and rollback milestones
     - Assign features to milestones based on project type priorities

   - **RESOURCE PLANNING** (Adapted to Project Type):
     - Identify required team roles and skills based on project type:
       - **MVP**: Minimal team, focus on core development
       - **Refactor**: Code quality experts, testing specialists
       - **New Feature**: Full-stack developers, UX designers
       - **Maintenance**: Security experts, QA specialists
     - Estimate effort and timeline for each milestone

4. **PROJECT STRUCTURE CREATION**:
   - Create project with title, description, objectives
   - Include all features, milestones, and requirements
   - Add stakeholder analysis and communication plan
   - Assign unique project identifier

5. **DEVELOPER CONFIRMATION**:
   - Present the complete project structure
   - Request changes, clarifications, or additional information, and re-run the project planning steps
   - Ask for explicit confirmation to proceed with the storage process
   - If declined: STOP without creating

6. **PROJECT STORAGE**:
   - Save content to file `/projects/{{date}}-{{project_name | slugify}}.md` or the location defined by input if provided
   - Execute memory operation:
     - Create if no related memory exists, or update it if it exists (use its Id).
     - Fields when creating/updating:
       - Title: `Project: {{project_name}} ({{project_type}})`
       - Content: Structured block including project title, project_id, date, description, objectives, features, milestones, and requirements.
       - Tags: `project`, `{{project_name | slugify}}`, `{{project_type | slugify}}`, `{{project_id}}`
       - CorpusNames: `patagonia_workflows` (only when creating)
       - UserTriggered: `true`
   - Confirm creation was successful
   - Suggest next steps (create epics or features)

## Project Template Format

**Project Title**: [Descriptive title reflecting business value]

**Project Type**: [MVP/Refactor/New Feature/Enhancement/Maintenance/Migration/Integration/Research]

**Business Value**: [Clear statement of business impact and ROI]

**Success Criteria**:

- [Measurable KPI 1]: [Target value] - [Timeline]
- [Measurable KPI 2]: [Target value] - [Timeline]
- [Measurable KPI 3]: [Target value] - [Timeline]

**Timeline**: [Start date] to [End date] ([X weeks/months])

**Budget/Resources**:

- **Team Size**: [X developers, Y designers, Z QA]
- **Estimated Cost**: [Total budget and breakdown]
- **Key Resources**: [Specialized tools, third-party services]

**Milestones**:

1. **Milestone 1**: [Description] - [Due date] - [Deliverables]
2. **Milestone 2**: [Description] - [Due date] - [Deliverables]
3. **Milestone 3**: [Description] - [Due date] - [Deliverables]

**Major Features**:

1. **Feature 1**: [Description] - [Priority: High/Medium/Low] - [Estimated effort]
2. **Feature 2**: [Description] - [Priority: High/Medium/Low] - [Estimated effort]

**Technical Stack**:

- **Frontend**: [Framework, libraries]
- **Backend**: [Language, framework]
- **Database**: [Type, version]
- **Infrastructure**: [Hosting, CI/CD]

**Risks & Mitigation**:

- **Risk 1**: [Description] - **Impact**: [High/Medium/Low] - **Mitigation**: [Strategy]
- **Risk 2**: [Description] - **Impact**: [High/Medium/Low] - **Mitigation**: [Strategy]

**Quality Assurance**:

- **Testing Strategy**: [Unit, Integration, E2E, Performance]
- **Code Quality**: [Linting, reviews, coverage requirements]
- **Security**: [Audit, penetration testing, compliance]

**Communication Plan**:

- **Frequency**: [Daily standups, weekly updates, monthly reviews]
- **Stakeholders**: [Who gets updates and how often]
- **Escalation Process**: [How to handle blockers and issues]

**Dependencies**: [External factors, team availability, third-party services]
**Contingency Plans**: [Backup strategies for major risks]
**Success Metrics**: [How success will be measured and tracked]

## Project Type Implementation Guidelines

### **MVP (Minimum Viable Product)**

- **Focus**: Core functionality, user validation, fast delivery
- **Skip**: Advanced features, complex integrations, comprehensive testing
- **Timeline**: 1-4 weeks
- **Resources**: Minimal team, core developers
- **Risks**: Market validation, technical feasibility
- **Success Criteria**: Working product, user feedback

### **Refactor**

- **Focus**: Code quality, performance, maintainability
- **Skip**: New features, UI changes, major architecture changes
- **Timeline**: 2-8 weeks based on codebase size
- **Resources**: Code quality experts, testing specialists
- **Risks**: Regression, performance degradation
- **Success Criteria**: Improved code metrics, maintainability

### **New Feature**

- **Focus**: User value, integration, scalability
- **Include**: Full testing, documentation, user acceptance
- **Timeline**: 2-12 weeks depending on complexity
- **Resources**: Full-stack developers, UX designers, QA
- **Risks**: Integration issues, user adoption
- **Success Criteria**: Delivered functionality, user satisfaction

### **Enhancement**

- **Focus**: Improvement of existing features
- **Skip**: Major new functionality, architectural changes
- **Timeline**: 1-6 weeks
- **Resources**: Product team, developers
- **Risks**: Breaking changes, user disruption
- **Success Criteria**: Improved user experience

### **Maintenance**

- **Focus**: Stability, security, bug fixes
- **Skip**: New features, major changes
- **Timeline**: Ongoing, hours to days per task
- **Resources**: Security experts, QA specialists
- **Risks**: System downtime, security breaches
- **Success Criteria**: System stability, security compliance

### **Migration**

- **Focus**: Data integrity, compatibility, rollback plans
- **Include**: Migration scripts, data validation, testing
- **Timeline**: 2-16 weeks depending on complexity
- **Resources**: Migration experts, data specialists
- **Risks**: Data loss, service disruption
- **Success Criteria**: Successful migration, zero data loss

### **Integration**

- **Focus**: API design, error handling, data synchronization
- **Include**: Security, monitoring, documentation
- **Timeline**: 2-8 weeks
- **Dependencies**: External factors or prerequisites
- **Contingency Plans**: Backup strategies for major risks
- **Communication Plan**: How stakeholders will be updated
- **Quality Gates**: Definition of done criteria for each milestone
- **Resources**: Integration specialists, security experts
- **Risks**: API failures, data inconsistencies
- **Success Criteria**: Reliable integration, proper error handling

### **Research/Spike**

- **Focus**: Technical feasibility, learning, proof of concept
- **Skip**: Production deployment, comprehensive testing
- **Timeline**: 1-2 weeks
- **Resources**: Technical experts, researchers
- **Risks**: Time waste, wrong direction
- **Success Criteria**: Clear technical understanding, decision making

## Project Type Detection Keywords

### MVP Detection

- "minimum viable product", "MVP", "prototype", "quick solution", "proof of concept"

### Refactor Detection

- "refactor", "clean up", "improve code", "optimize", "restructure", "technical debt"

### New Feature Detection

- "new feature", "add functionality", "enhancement", "capability", "new requirement"

### Enhancement Detection

- "improve", "enhance", "upgrade", "better", "optimize", "polish"

### Maintenance Detection

- "bug fix", "security", "patch", "update", "maintenance", "hotfix"

### Migration Detection

- "migrate", "upgrade", "move to", "switch to", "transition", "modernize"

### Integration Detection

- "integrate", "connect", "third-party", "external service", "API", "webhook"

### Research/Spike Detection

- "research", "investigate", "explore", "spike", "proof of concept", "evaluate"
