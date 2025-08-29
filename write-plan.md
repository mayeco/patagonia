---
description: Generate a detailed implementation plan for a feature request from the developer
---

# Write Plan Workflow

## Important Notes

- **Fetch external websites when needed** - This workflow can analyze external websites to gather requirements and context
- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis
- **Focus on comprehensive analysis** - Use external resources to provide better context and more complete plans

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete plan generation within 10 steps maximum. If project analysis takes too long, use available information and proceed.

**DECISION POINTS**: Make binary decisions quickly - project type is identified or ask user to specify.

**TERMINATION CONDITIONS**:
- If user doesn't provide feature name: Ask and STOP
- If project type unclear: Ask user to specify and STOP
- If user declines confirmation: STOP immediately
- Always require explicit user confirmation before proceeding

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
1. Capture the feature name by asking in the detected language:
   - English: "What feature do you want to plan?"
   - Spanish: "¿Qué característica quieres planificar?"
2. Analyze the feature request to understand the requirements and scope
3. **Detect Project Type** based on analysis:
   - **MVP (Minimum Viable Product)**: Basic functionality to test concept, minimal features
   - **Refactor**: Improving existing code without changing functionality
   - **New Feature**: Adding new functionality to existing system
   - **Enhancement**: Improving existing features or user experience
   - **Maintenance**: Bug fixes, security updates, performance improvements
   - **Migration**: Moving from one technology/platform to another
   - **Integration**: Connecting with third-party services or systems
   - **Research/Spike**: Investigating new technologies or approaches
4. Generate a flexible code-focused implementation plan in the detected language that includes:
   - **Project Type Identification**: MVP, refactor, new feature, maintenance, enhancement, etc.
   - **Feature Overview**: Title, description, and business value
   - **Requirements Analysis**: Functional and non-functional requirements (detailed for complex projects, basic for simple ones)
   - **Technical Architecture**: High-level design and technology choices (comprehensive for new systems, minimal for enhancements)
   - **Implementation Stages**: Code development focused stages:
     - **Stage 1: Code Planning & Design** - Code structure, class design, algorithm planning
     - **Stage 2: Core Development** - Writing the main code logic and functionality
     - **Stage 3: Code Integration** - Integrating components, resolving dependencies
     - **Stage 4: Code Testing** - Unit tests, integration tests, code validation
     - **Stage 5: Code Review & Refinement** - Code review, optimization, documentation
   - **Technical Stack**: Specific technologies, libraries, and tools for development
   - **Database Design**: Schema, relationships, and data flow (only if database code changes are needed)
   - **API Design**: Endpoints, data structures, authentication (only for API code development)
   - **Testing Strategy**: Unit, integration, and code testing approach (focused on validating code functionality)
   - **Code Quality Standards**: Coding conventions, documentation requirements, maintainability considerations
   - **Timeline Estimation**: Time breakdown by development stages and coding milestones
   - **Any clarifications needed from the developer**
4. Rate the understanding of the request on a scale of 1-10 in the detected language:
   - 1 = Very unclear, major gaps in understanding / Muy poco claro, grandes brechas en la comprensión
   - 10 = Perfectly clear, complete understanding / Perfectamente claro, comprensión completa
5. Save the plan to `/plans/{{date}}-{{feature_name | slugify}}.md`
6. Wait for explicit developer confirmation before proceeding with implementation
7. If clarification is needed, ask specific questions in the detected language and add the clarifications to the plan to improve understanding
8. After receiving clarifications, rate the improved understanding on a scale of 1-10 and assess if additional information is still needed
9. Re-evaluate project type if new information changes the scope or approach
10. If the developer provides new information or changes requirements, re-evaluate and update the plan accordingly
11. If the developer confirms the plan, proceed with implementation
12. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

## Project Type Detection Guidelines

### How to Identify Project Types:

**MVP Detection:**
- Keywords: "minimum viable product", "MVP", "prototype", "quick solution"
- Context: Testing concept, proof of concept, early validation
- Characteristics: Minimal features, basic functionality, fast delivery

**Refactor Detection:**
- Keywords: "refactor", "clean up", "improve code", "optimize", "restructure"
- Context: Existing codebase improvements without new functionality
- Characteristics: Same functionality, better code quality, performance improvements

**New Feature Detection:**
- Keywords: "new feature", "add functionality", "enhancement", "capability"
- Context: Adding new user-facing functionality
- Characteristics: New user interactions, new business logic, UI changes

**Maintenance Detection:**
- Keywords: "bug fix", "security", "patch", "update", "maintenance"
- Context: Keeping existing functionality working and secure
- Characteristics: No new features, fixing issues, security updates

**Migration Detection:**
- Keywords: "migrate", "upgrade", "move to", "switch to", "transition"
- Context: Changing technology stack or platform
- Characteristics: Same functionality, different underlying technology

### Project Type Impact on Code Planning:
- **MVP**: Focus on core functionality code, minimal abstraction layers, fast iterative development
- **Refactor**: Emphasize code quality metrics, design patterns, test coverage for refactored code
- **New Feature**: Comprehensive code testing, clean architecture, extensible code design
- **Maintenance**: Quick code fixes, minimal code changes, preserve existing patterns
- **Migration**: Code compatibility layers, gradual code migration, maintain existing functionality
- **Integration**: Clean API interfaces, error handling code, logging and monitoring code
- **Research/Spike**: Proof of concept code, performance benchmarks, architectural exploration
- **Enhancement**: Backward compatible code changes, feature flags, gradual rollout support

## Code-Focused Plan Adaptation Guidelines

### For MVP Projects:
- **Skip**: Complex design patterns, extensive abstraction layers, comprehensive documentation
- **Focus**: Core functionality code, basic algorithms, essential code paths
- **Timeline**: 1-2 weeks maximum for code development
- **Code Quality**: Functional code over perfect code, iterative improvements

### For Refactor Projects:
- **Skip**: New feature development, UI changes, database schema changes
- **Focus**: Code quality metrics, design patterns, test coverage for refactored code
- **Timeline**: Based on codebase size and complexity
- **Code Quality**: Maintainability, readability, performance optimization

### For New Feature Projects:
- **Include**: Clean code architecture, comprehensive unit tests, integration tests
- **Focus**: Extensible code design, separation of concerns, scalable architecture
- **Timeline**: 2-8 weeks depending on code complexity
- **Code Quality**: Well-documented, testable, maintainable code

### For Maintenance Projects:
- **Skip**: Major architectural changes, extensive refactoring
- **Focus**: Minimal code changes, preserve existing patterns, regression prevention
- **Timeline**: Hours to days for code fixes
- **Code Quality**: Safe changes, backward compatibility, minimal side effects

### Code Complexity Scaling:
- **Low Complexity**: 3-5 code sections, basic algorithms, simple integration
- **Medium Complexity**: 7-10 code sections, complex algorithms, multiple components
- **High Complexity**: 12+ code sections, advanced patterns, distributed systems

**Code-Only Focus**: This workflow focuses exclusively on code development aspects. DevOps, deployment, security policies, performance monitoring, and infrastructure concerns are handled separately and are not part of this code planning workflow.
