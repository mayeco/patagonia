---
description: Ejecutar análisis de seguridad con Checkmarx One CLI
---

# Checkmarx One CLI Scan Workflow

Ejecutar análisis de seguridad en el proyecto actual usando Checkmarx One CLI con variables de entorno configuradas.

# Checkmarx One CLI Scan Workflow

Ejecutar análisis de seguridad en el proyecto actual usando Checkmarx One CLI con variables de entorno configuradas.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete workflow within 8 steps maximum. If scan takes longer than expected, provide status update and continue monitoring.

**SECURITY CONSTRAINTS**: 
- NEVER execute validation commands like `which cx`, `command -v cx`
- NEVER display or print environment variables (CX_CLIENT_SECRET, etc.)
- STOP immediately if environment variables are missing

**TERMINATION CONDITIONS**:
- If `cx` command not found: Stop with error message
- If environment variables missing: Stop with configuration error
- If scan fails: Provide error details and stop
- If scan succeeds: Generate report and complete

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("english", "scan", "security"). Default to Spanish.

1. **ENVIRONMENT VALIDATION**:
   - Check required environment variables exist: CX_TENANT, CX_BASE_URI, CX_CLIENT_ID, CX_CLIENT_SECRET
   - If any missing: STOP - "Missing required environment variables"
   - If all present: Proceed to step 2

2. **PROJECT ANALYSIS**:
   - Scan current directory for source code files
   - Detect primary programming languages (JavaScript, Python, Java, etc.)
   - Set default project name from directory name
   - Set default branch to "main"

3. **SCAN PARAMETER CONFIGURATION**:
   - Project name: Use directory name or user-specified
   - Branch: Use "main" default or user-specified
   - Scan types: SAST and SCA by default
   - File filters: Include common source file extensions

4. **SCAN EXECUTION**:
   - Execute: `cx scan create --project-name "${PROJECT_NAME}" --file-source "." --scan-info-format "json" --branch "${BRANCH_NAME}" --agent "Panagonia"`
   - Capture scan ID from response
   - Monitor scan progress (provide status updates)
   - If command fails: STOP with error details

5. **RESULT PROCESSING**:
   - Retrieve scan results using scan ID
   - Parse JSON output for vulnerabilities
   - Categorize by severity: Critical, High, Medium, Low
   - Extract vulnerability details and remediation suggestions

6. **REPORT GENERATION**:
   - Create structured report with findings
   - Include executive summary with total counts
   - Provide specific remediation steps for each vulnerability
   - Save report to local file

7. **FINAL RESPONSE**:
   - Provide scan summary with key metrics
   - List top 5 most critical vulnerabilities
   - Suggest next steps for remediation

**Prerequisites:**
- Checkmarx One CLI installed (`cx` command available)
- Environment variables configured:
  - `CX_TENANT` - Tenant name
  - `CX_BASE_URI` - Checkmarx One server URL
  - `CX_CLIENT_ID` - OAuth client ID
  - `CX_CLIENT_SECRET` - OAuth client secret
- Project with source code to scan

**Language Support:**
- **Spanish**: DEFAULT - Ejecutar análisis en español para toda entrada
- **English**: Execute analysis in English only if explicitly requested
- **Other**: Execute analysis in Spanish as default, but adapt to detected language when possible

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