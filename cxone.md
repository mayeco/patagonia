---
description: Execute security analysis with Checkmarx One CLI
auto_execution_mode: 3
---

# Checkmarx One CLI Scan Workflow

Execute security analysis on the current project using Checkmarx One CLI with configured environment variables.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete security scan within 10 steps maximum. If scan takes too long, provide status and continue monitoring.

**ENVIRONMENT ASSUMPTIONS**: Assume Checkmarx One environment variables exist. Do NOT validate or check environment variables.

**COMMAND EXECUTION**: Execute cx commands directly without validation. If commands fail, parse error output for specific issues.

**TERMINATION CONDITIONS**:
- If cx command fails: Parse error and stop with specific guidance
- If credentials invalid: Stop with credential configuration message
- If project not found: Stop with project setup guidance
- Always provide scan results or clear error explanation

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **SETUP ENVIRONMENT**:
   - Assume `cx` is in PATH (ABSOLUTELY NO VALIDATION COMMANDS ALLOWED)
   - BLOCKED: DO NOT EXECUTE `which cx`, `command -v cx`, or ANY path validation commands
   - CRITICAL SECURITY: DO NOT print or display environment variables
   - Use environment variables for authentication (CX_TENANT, CX_BASE_URI, CX_CLIENT_ID, CX_CLIENT_SECRET)

2. **ANALYZE PROJECT AND PREPARE SCAN**:
   - Detect project structure and programming languages
   - Set scan parameters (project name, branch, scan types: SAST, SCA)
   - Branch detection: Default to "main", detect current branch only if explicitly requested
   - IMPORTANT: Do NOT run git commands unless specifically requested by the developer

3. **ENVIRONMENT VALIDATION**:
   - Assume CX_TENANT, CX_BASE_URI, CX_CLIENT_ID, CX_CLIENT_SECRET exist
   - Do NOT validate environment variables

4. **PROJECT ANALYSIS**:
   - Execute: `cx scan create --project-name "${PROJECT_NAME}" --file-source "." --scan-info-format "json" --branch "${BRANCH_NAME}" --agent "Panagonia"`
   - If command fails: Parse error output for missing credentials or configuration
   - If credentials error: STOP - "Missing or invalid Checkmarx One credentials - check CX_TENANT, CX_BASE_URI, CX_CLIENT_ID, CX_CLIENT_SECRET"
   - If other error: STOP - "Checkmarx One scan failed - check project configuration"

5. **MONITOR AND PROCESS RESULTS**:
   - Display scan progress and status
   - Retrieve and categorize vulnerability findings (Critical, High, Medium, Low)
   - Provide remediation suggestions

6. **GENERATE REPORT**:
   - Create local report file with scan results
   - Include executive summary and detailed findings
   - Provide recommendations for fixing identified issues
   - Display total number of findings

**Prerequisites:**
- Checkmarx One CLI installed (`cx` command available)
- Environment variables configured:
  - `CX_TENANT` - Tenant name
  - `CX_BASE_URI` - Checkmarx One server URL
  - `CX_CLIENT_ID` - OAuth client ID
  - `CX_CLIENT_SECRET` - OAuth client secret
- Project with source code to scan

**Scan Types Supported:**
- 🔍 **SAST**: Static Application Security Testing
- 📦 **SCA**: Software Composition Analysis

**Common Scan Commands:**
```bash
# Basic scan
cx scan create --project-name "my-project" --file-source "."

# Full security scan
cx scan create --project-name "my-project" --file-source "." --scan-types "sast,sca"

# Incremental scan
cx scan create --project-name "my-project" --file-source "."

# Scan with specific branch
cx scan create --project-name "my-project" --file-source "." --branch "main"
```