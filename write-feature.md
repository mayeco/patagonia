---
description: Generate implementation plans for small, specific features
---

# Write Feature Workflow

Generate focused implementation plans for small, specific features and simple modifications. This workflow is optimized for individual features that can be completed in a single development session.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete feature planning within 6 steps maximum.

**DECISION POINTS**: Make binary decisions - feature is simple enough or needs project planning.

**TERMINATION CONDITIONS**:
- If feature description unclear: Ask for clarification and STOP
- If feature complexity is "Complex": Suggest write-project workflow and STOP
- Always require user confirmation before proceeding

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("feature", "implement", "small"). Default to Spanish.

1. **FEATURE CAPTURE**:
   - Ask user for specific feature description
   - Validate feature is small and concrete (not complex)
   - If too complex: STOP - "This seems like a project, use write-project workflow"

2. **FEATURE TYPE DETECTION**:
   - Analyze feature description for type indicators:
     - **UI/UX**: Keywords like "interface", "design", "user experience", "layout", "styling"
     - **Functionality**: Keywords like "function", "logic", "algorithm", "calculation", "processing"
     - **Integration**: Keywords like "API", "database", "external service", "third-party", "connect"
     - **Data**: Keywords like "storage", "retrieval", "query", "filter", "sort", "display"
     - **Security**: Keywords like "authentication", "authorization", "validation", "encryption"
     - **Performance**: Keywords like "speed", "optimization", "loading", "response time"
   - Validate feature type against description
   - If unclear: Ask user to specify feature type and STOP

3. **COMPLEXITY ASSESSMENT**:
   - Evaluate feature against simplicity guidelines
   - Consider feature type complexity:
     - **UI/UX**: CSS changes, component modifications
     - **Functionality**: Algorithm implementation, business logic
     - **Integration**: API calls, data synchronization
     - **Data**: Database queries, data processing
     - **Security**: Input validation, authentication flows
     - **Performance**: Code optimization, caching strategies
   - Classify as Simple or Moderate (max 30-120 minutes)
   - If too complex: STOP - "Feature too complex, consider write-project workflow"

4. **DEPENDENCY ANALYSIS**:
   - Identify required dependencies based on feature type:
     - **UI/UX**: CSS frameworks, component libraries, design systems
     - **Functionality**: Utility libraries, calculation modules
     - **Integration**: API clients, authentication libraries
     - **Data**: Database drivers, ORM libraries, query builders
     - **Security**: Security libraries, encryption modules
     - **Performance**: Caching libraries, optimization tools
   - Check for existing dependencies in project
   - Note any new dependencies that need to be added
5. **IMPLEMENTATION PLANNING**:
   - Create type-specific implementation approach:
     - **UI/UX**: Identify CSS selectors, component structure, responsive breakpoints
     - **Functionality**: Define function signatures, input/output specifications, error handling
     - **Integration**: Specify API endpoints, request/response formats, error scenarios
     - **Data**: Define data models, query parameters, validation rules
     - **Security**: Outline validation logic, authentication checks, encryption needs
     - **Performance**: Identify bottlenecks, caching strategies, optimization techniques
   - Identify specific files to modify (usually 1-3 files)
   - Define exact code changes needed
   - Specify implementation steps (3-7 clear steps)
   - Include testing requirements based on feature type
   - Estimate time (15-120 minutes maximum)

6. **TESTING REQUIREMENTS**:
   - Define testing approach based on feature type:
     - **UI/UX**: Visual regression, accessibility, responsive design
     - **Functionality**: Unit tests, edge cases, error scenarios
     - **Integration**: API testing, data validation, error handling
     - **Data**: Data integrity, query performance, edge cases
     - **Security**: Input validation, authentication, authorization
     - **Performance**: Load testing, response times, scalability
   - Specify test cases and acceptance criteria

7. **SUCCESS CRITERIA**:
   - Define measurable success metrics based on feature type:
     - **UI/UX**: Visual consistency, user feedback, accessibility compliance
     - **Functionality**: Correct calculations, error handling, performance
     - **Integration**: Successful API calls, data synchronization, error recovery
     - **Data**: Accurate data display, query performance, data integrity
     - **Security**: Input validation, security testing, audit compliance
     - **Performance**: Response times, resource usage, scalability metrics
8. **USER CONFIRMATION**:
   - Present complete feature plan including:
     - Feature type and description
     - Dependencies and requirements
     - Implementation steps and timeline
     - Testing requirements and success criteria
   - Ask for explicit confirmation to proceed
   - If declined: STOP without saving

9. **FEATURE STORAGE**:
   - Save to `/features/{{date}}-{{feature_name | slugify}}.md`
   - Confirm file creation successful
   - Suggest immediate implementation
   - Provide next steps for development

## Feature Type Implementation Guidelines

### **UI/UX Feature**
- **Focus**: Visual design, user interaction, accessibility
- **Common Changes**: CSS styling, component props, layout adjustments
- **Testing**: Visual regression, accessibility tools, responsive design
- **Success Metrics**: Visual consistency, user feedback, design compliance

### **Functionality Feature**
- **Focus**: Business logic, calculations, data processing
- **Common Changes**: Algorithm implementation, function logic, data manipulation
- **Testing**: Unit tests, edge cases, error scenarios
- **Success Metrics**: Correct calculations, error handling, performance

### **Integration Feature**
- **Focus**: External systems, APIs, third-party services
- **Common Changes**: API calls, data synchronization, error handling
- **Testing**: API testing, mock services, integration scenarios
- **Success Metrics**: Successful data exchange, error recovery, reliability

### **Data Feature**
- **Focus**: Information display, storage, retrieval
- **Common Changes**: Queries, data models, display logic
- **Testing**: Data validation, query performance, edge cases
- **Success Metrics**: Data accuracy, query performance, user experience

### **Security Feature**
- **Focus**: Authentication, authorization, data protection
- **Common Changes**: Input validation, access controls, encryption
- **Testing**: Security testing, vulnerability assessment, compliance
- **Success Metrics**: Security compliance, vulnerability coverage, audit results

### **Performance Feature**
- **Focus**: Speed, efficiency, resource optimization
- **Common Changes**: Caching, optimization, resource management
- **Testing**: Load testing, performance benchmarks, resource monitoring
- **Success Metrics**: Response times, resource usage, scalability

## Feature Type Detection Keywords

### UI/UX Detection:
- "interface", "design", "layout", "styling", "CSS", "component", "UI", "UX", "visual"

### Functionality Detection:
- "function", "logic", "algorithm", "calculate", "process", "business logic", "computation"

### Integration Detection:
- "API", "integration", "external", "third-party", "webhook", "service", "connect", "sync"

### Data Detection:
- "database", "query", "display", "storage", "retrieve", "filter", "sort", "data"

### Security Detection:
- "security", "authentication", "authorization", "validation", "encryption", "access", "login"

### Performance Detection:
- "performance", "speed", "optimize", "fast", "loading", "response time", "efficiency"