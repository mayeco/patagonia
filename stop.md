---
description: Dev Server Stop & Clean Workflow
---

Stop any development server and clean build artifacts across any programming language, framework, or development environment. This workflow discovers and handles any technology stack automatically.

**⚠️ CRITICAL AI EXECUTION RULES**

**DO NOT GET STUCK IN DETECTION LOOPS**: Complete cleanup process within 8 steps maximum.

**DECISION POINTS**: Make binary decisions - cleanup scope is appropriate or requires user confirmation.

**TERMINATION CONDITIONS**:

- If no development activity detected: Report and STOP
- If user denies destructive operations: Honor choice and STOP
- Always require user confirmation for cache/dependency reset operations

**STEPS**

1. **RUNTIME ENVIRONMENT DETECTION**:
   - Detect operating system and available shells
   - Scan for any active processes that match development patterns
   - Identify available process management tools
   - If no development processes found: Continue with filesystem analysis

2. **DEVELOPMENT CONTEXT DISCOVERY**:
   - Scan project structure for any development indicators:
     - Configuration files (any `*.config.*`, `.*rc`, `Makefile`, `build.*`)
     - Dependency management files (any `*lock*`, `requirements.*`, `Gemfile`, `go.mod`)
     - Build/compilation artifacts (any `build/`, `dist/`, `target/`, `bin/`, `.cache/`)
     - Development scripts in package managers or build tools
   - Identify project type by file patterns and directory structure
   - If no development context found: Report and offer manual process termination

3. **PROCESS DISCOVERY AND ANALYSIS**:
   - Discover all running processes and analyze for development patterns:
     - Look for common development keywords in process names/commands
     - Identify processes using typical development port ranges
     - Detect processes with development-related arguments or flags
     - Cross-reference with discovered project context
   - Map processes to potential cleanup actions
   - If no development processes found: Skip to filesystem cleanup

4. **CLEANUP SCOPE DETERMINATION**:
   - Present discovered elements and cleanup options:
     - **minimal**: Stop identified development processes only
     - **standard**: Stop processes + remove detected build artifacts
     - **thorough**: Standard + temporary files + development logs
     - **reset**: Thorough + dependency caches + rebuild preparation
   - Explain what will be affected based on discovery
   - If "reset" selected: Require explicit confirmation with impact summary

5. **DEVELOPMENT PROCESS TERMINATION**:
   - For each identified development process:
     - Attempt graceful termination with appropriate signals
     - Wait for graceful shutdown with reasonable timeout
     - Force termination if processes persist
     - Verify process termination and port liberation
   - Handle process hierarchies and child processes appropriately
   - Report termination results and any processes that couldn't be stopped

6. **BUILD ARTIFACT CLEANUP**:
   - Based on discovered project structure, remove:
     - Compilation outputs and build directories
     - Generated assets and bundled files
     - Intermediate build files and caches
     - Framework-specific temporary directories
   - Preserve source code, configuration, and version control
   - Calculate and report storage space recovered

7. **DEVELOPMENT CACHE AND TEMPORARY CLEANUP** (if thorough/reset level):
   - Clean discovered temporary files:
     - Development logs and debug files
     - IDE and editor temporary files
     - System-generated files (OS-specific)
     - Development tool caches and metadata
   - Remove dependency manager caches (if reset level)
   - Preserve user data and project-specific configuration

8. **SYSTEM VERIFICATION AND READINESS**:
   - Verify no development processes remain active
   - Confirm specified cleanup actions completed successfully
   - Test basic development environment readiness:
     - Required runtimes and tools still accessible
     - Project structure integrity maintained
     - Development dependencies available (unless reset)
   - Report comprehensive cleanup summary with actionable next steps
   - If verification reveals issues: Provide specific guidance for resolution

**EXECUTION SUMMARY**: This workflow provides completely technology-agnostic development environment cleanup by discovering the specific context and adapting cleanup actions accordingly, ensuring safe operation across any development stack.
