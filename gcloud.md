---
description: Execute Google Cloud CLI commands based on developer requests
---

# Google Cloud CLI Workflow

Execute Google Cloud CLI (gcloud) commands based on developer requests. This workflow handles common GCP operations like authentication, project management, deployments, and resource configuration.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete GCP operation within 6 steps maximum.

**DECISION POINTS**: Make binary decisions - command is safe or requires confirmation.

**SAFETY VALIDATION**: Validate command safety and developer permissions before execution.

**TERMINATION CONDITIONS**:
- If gcloud not installed: Ask developer to install and STOP
- If not authenticated: Ask developer to authenticate and STOP
- If destructive command: Ask for confirmation and STOP if denied
- Always require developer confirmation for destructive operations

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **OPERATION DETECTION**: Detect type of GCP operation:
   - Authentication and initial configuration
   - Project management (create, list, configure)
   - Resource management (compute, storage, networking)
   - Deployments and services (App Engine, Cloud Run, Kubernetes)
   - Monitoring and logging
   - IAM and permissions configuration

2. **ENVIRONMENT VALIDATION**:
   - Execute: `gcloud --version`
   - If command fails: STOP - "gcloud CLI not installed - ensure Google Cloud SDK is available"
   - Execute: `gcloud auth list`
   - If command fails: STOP - "Not authenticated with Google Cloud - run 'gcloud auth login' first"
   - Execute: `gcloud config get-value project`
   - If no project: Ask developer to set project

3. **COMMAND CONSTRUCTION**:
   - Map operation to specific gcloud command
   - Add required flags and options
   - Include project, zone, region as needed
   - Validate command syntax mentally

4. **SAFETY CHECK**:
   - Scan command for destructive keywords: delete, remove, destroy, rm
   - If found: Ask developer for explicit confirmation
   - If developer denies: STOP with safety message
   - If developer confirms: Proceed to execution

5. **COMMAND EXECUTION**:
   - Execute prepared gcloud command
   - Set reasonable timeout (30-60 seconds)
   - Capture stdout, stderr, and exit code
   - If command fails: Parse error output and STOP with specific error message
   - Do NOT attempt alternative commands or installations

6. **RESULT PROCESSING**: Process results:
   - Display command output
   - Interpret exit codes
   - Provide feedback to developer
   - Suggest next steps if applicable

# 🚨🚨🚨 CRITICAL WARNING: DESTRUCTIVE OPERATIONS 🚨🚨🚨

## ⚠️⚠️⚠️ NEVER EXECUTE DESTRUCTIVE COMMANDS ⚠️⚠️⚠️

**IMPORTANT SAFETY PROTOCOLS:**

### ❌ DESTRUCTIVE COMMANDS - PRINT ONLY, NEVER EXECUTE:
- **DELETE Operations**: `gcloud projects delete`, `gcloud compute instances delete`, `gcloud storage buckets delete`
- **STOP/TERMINATE**: `gcloud compute instances delete`, `gcloud container clusters delete`
- **REMOVE/DESTROY**: `gcloud iam service-accounts delete`, `gcloud sql instances delete`
- **DROP/REMOVE**: `gcloud storage rm`, `gcloud compute disks delete`
- **Any command with**: `--delete`, `--remove`, `--destroy`, `--terminate`, `--drop`

### 🛡️ SAFETY MEASURES:
1. **ALWAYS PRINT the command first** - Never execute directly
2. **CONFIRM with developer** before any destructive action
3. **Show preview** of what will be deleted/destroyed
4. **Provide rollback options** when possible
5. **Document consequences** clearly

### 📋 DESTRUCTIVE COMMAND EXAMPLES (PRINT ONLY):
```bash
# ❌ NEVER EXECUTE - Only print for developer review
gcloud projects delete my-project-id
gcloud compute instances delete my-instance --zone=us-central1-a
gcloud storage buckets delete gs://my-bucket
gcloud container clusters delete my-cluster --zone=us-central1-a
gcloud iam service-accounts delete my-service-account@project.iam.gserviceaccount.com
gcloud sql instances delete my-sql-instance
gcloud compute disks delete my-disk --zone=us-central1-a
```

### 🎯 EXECUTION PROTOCOL:
1. **Parse** destructive command request
2. **PRINT** the command (do not execute)
3. **WARN** about consequences
4. **ASK** the developer for explicit confirmation
5. **Only execute** after developer approval
6. **Provide** rollback information

**REMEMBER: SAFETY FIRST! Always err on the side of caution with destructive operations!**

## Common GCP Commands

### Authentication
```bash
# Interactive login
gcloud auth login

# Login with service account
gcloud auth activate-service-account --key-file=service-account.json

# List authenticated accounts
gcloud auth list

# Set default account
gcloud config set account user@example.com
```

### Project Management
```bash
# List projects
gcloud projects list

# Set default project
gcloud config set project my-project-id

# Create new project
gcloud projects create my-new-project --name="My New Project"

# Describe project
gcloud projects describe my-project-id
```

### Compute Engine
```bash
# List instances
gcloud compute instances list

# Create instance
gcloud compute instances create my-instance --zone=us-central1-a --machine-type=n1-standard-1

# SSH to instance
gcloud compute ssh my-instance --zone=us-central1-a

# Stop instance
gcloud compute instances stop my-instance --zone=us-central1-a
```

### Cloud Storage
```bash
# List buckets
gcloud storage buckets list

# Create bucket
gcloud storage buckets create gs://my-bucket --location=us-central1

# Upload file
gcloud storage cp file.txt gs://my-bucket/

# Download file
gcloud storage cp gs://my-bucket/file.txt .
```

### Kubernetes Engine (GKE)
```bash
# List clusters
gcloud container clusters list

# Create cluster
gcloud container clusters create my-cluster --zone=us-central1-a --num-nodes=3

# Get credentials
gcloud container clusters get-credentials my-cluster --zone=us-central1-a

# List pods
kubectl get pods
```

### Cloud Run
```bash
# Deploy service
gcloud run deploy my-service --source . --platform managed --region us-central1

# List services
gcloud run services list

# Get service URL
gcloud run services describe my-service --region us-central1 --format="value(status.url)"
```

## Common Configuration

### Global Configuration
```bash
# View current configuration
gcloud config list

# Set default zone
gcloud config set compute/zone us-central1-a

# Set default region
gcloud config set compute/region us-central1

# View available configurations
gcloud config configurations list
```

### Service Accounts
```bash
# Create service account
gcloud iam service-accounts create my-service-account --display-name="My Service Account"

# Assign roles
gcloud projects add-iam-policy-binding my-project --member="serviceAccount:my-service-account@my-project.iam.gserviceaccount.com" --role="roles/editor"

# Generate key
gcloud iam service-accounts keys create key.json --iam-account=my-service-account@my-project.iam.gserviceaccount.com
```

## Best Practices

### Security
- Never expose keys or credentials in logs
- Use service accounts instead of user accounts for CI/CD
- Apply least privilege principle
- Rotate keys regularly

### Efficiency
- Configure default zone/region to avoid prompts
- Use `--format` to filter output
- Use `--filter` for specific queries
- Cache credentials when possible

### Monitoring
- Use `gcloud logging` to review logs
- Configure alerts in Cloud Monitoring
- Review quotas and usage limits
- Monitor costs with Cloud Billing

## Troubleshooting

### Common Problems
- **Authentication error**: Run `gcloud auth login`
- **Project not found**: Verify `gcloud config get-value project`
- **Quota exceeded**: Review quotas in Cloud Console
- **Insufficient permissions**: Verify assigned IAM roles

### Diagnostic Commands
```bash
# Verify authentication
gcloud auth list

# Verify configuration
gcloud config list

# Verify project
gcloud config get-value project

# Verify zone/region
gcloud config get-value compute/zone
gcloud config get-value compute/region
```

**Prerequisites:**
- Google Cloud SDK installed (`gcloud` command available)
- Authentication configured (login or service account)
- GCP project configured
- Appropriate permissions in the project