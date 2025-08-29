---
description: Ejecutar análisis de seguridad con Checkmarx One CLI
---

# Checkmarx One CLI Scan Workflow

Ejecutar análisis de seguridad en el proyecto actual usando Checkmarx One CLI con variables de entorno configuradas.

## Steps

1. Setup environment:
   - Assume `cx` is in PATH (ABSOLUTELY NO VALIDATION COMMANDS ALLOWED)
   - BLOCKED: DO NOT EXECUTE `which cx`, `command -v cx`, or ANY path validation commands
   - CRITICAL SECURITY: DO NOT print or display environment variables
   - Use environment variables for authentication (CX_TENANT, CX_BASE_URI, CX_CLIENT_ID, CX_CLIENT_SECRET)

2. Analyze project and prepare scan:
   - Detect project structure and programming languages
   - Set scan parameters (project name, branch, scan types: SAST, SCA)
   - Branch detection: Default to "main", detect current branch only if explicitly requested
   - IMPORTANT: Do NOT run git commands unless specifically requested by user

3. Execute Checkmarx One scan:
   - Run `cx scan create --project-name "${PROJECT_NAME}" --file-source "." --scan-info-format "json" --branch "${BRANCH_NAME}" --agent "Panagonia" --file-filter "${FILE_FILTERS}"`
   - CORRECT FLAGS: Use --file-source (NOT --source)

4. Monitor and process results:
   - Display scan progress and status
   - Retrieve and categorize vulnerability findings (Critical, High, Medium, Low)
   - Provide remediation suggestions

5. Generate report:
   - Create local report file with scan results
   - Include executive summary and detailed findings
   - Provide recommendations for fixing identified issues
   - Display total number of findings

10. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

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