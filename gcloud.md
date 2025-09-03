---
description: Execute Google Cloud CLI commands based on developer requests
---

# Google Cloud CLI Workflow

Execute Google Cloud CLI (gcloud) commands based on developer requests. This workflow handles common GCP operations like authentication, project management, deployments, and resource configuration.

## Important Rules

- COMMAND_EXECUTION

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

## 🚨🚨🚨 CRITICAL WARNING: DESTRUCTIVE OPERATIONS 🚨🚨🚨

## ⚠️⚠️⚠️ NEVER EXECUTE DESTRUCTIVE COMMANDS ⚠️⚠️⚠️

**IMPORTANT SAFETY PROTOCOLS:**

### ❌ DESTRUCTIVE COMMANDS - PRINT ONLY, NEVER EXECUTE

- **DELETE Operations**: `gcloud projects delete`, `gcloud compute instances delete`, `gcloud storage buckets delete`
- **STOP/TERMINATE**: `gcloud compute instances delete`, `gcloud container clusters delete`
- **REMOVE/DESTROY**: `gcloud iam service-accounts delete`, `gcloud sql instances delete`
- **DROP/REMOVE**: `gcloud storage rm`, `gcloud compute disks delete`
- **Any command with**: `--delete`, `--remove`, `--destroy`, `--terminate`, `--drop`

### 🛡️ SAFETY MEASURES

1. **ALWAYS PRINT the command first** - Never execute directly
2. **CONFIRM with developer** before any destructive action
3. **Show preview** of what will be deleted/destroyed
4. **Provide rollback options** when possible
5. **Document consequences** clearly

### 📋 DESTRUCTIVE COMMAND EXAMPLES (PRINT ONLY)

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

### 🎯 EXECUTION PROTOCOL

1. **Parse** destructive command request
2. **PRINT** the command (do not execute)
3. **WARN** about consequences
4. **ASK** the developer for explicit confirmation
5. **Only execute** after developer approval
6. **Provide** rollback information

**REMEMBER: SAFETY FIRST! Always err on the side of caution with destructive operations!**

## Common GCP Commands

```bash
# Auth & Config
gcloud --version
gcloud auth login                          # or: gcloud auth activate-service-account --key-file key.json
gcloud auth list
gcloud config set project <PROJECT_ID>
gcloud config set compute/region <REGION>
gcloud config set compute/zone <ZONE>
gcloud config list

# Projects
gcloud projects list
gcloud projects create <ID> --name="<NAME>"
gcloud projects describe <PROJECT_ID>

# Compute Engine
gcloud compute instances list
gcloud compute instances create <NAME> --zone=<ZONE> --machine-type=e2-micro
gcloud compute ssh <NAME> --zone=<ZONE>
gcloud compute instances stop <NAME> --zone=<ZONE>

# Cloud Storage
gcloud storage buckets list
gcloud storage buckets create gs://<BUCKET> --location=<REGION>
gcloud storage cp <SRC> gs://<BUCKET>/
gcloud storage cp gs://<BUCKET>/<OBJ> <DST>

# GKE
gcloud container clusters list
gcloud container clusters create <CLUSTER> --zone=<ZONE> --num-nodes=3
gcloud container clusters get-credentials <CLUSTER> --zone=<ZONE>
kubectl get pods

# Cloud Run
gcloud run deploy <SERVICE> --source . --platform managed --region <REGION>
gcloud run services list
gcloud run services describe <SERVICE> --region <REGION> --format="value(status.url)"

# IAM Service Accounts
gcloud iam service-accounts create <SA> --display-name "<Name>"
gcloud projects add-iam-policy-binding <PROJECT> --member="serviceAccount:<SA>@<PROJECT>.iam.gserviceaccount.com" --role="roles/editor"
gcloud iam service-accounts keys create key.json --iam-account=<SA>@<PROJECT>.iam.gserviceaccount.com
```

## Common Configuration

Quick reference (covered above; minimal):

```bash
gcloud config list
gcloud config set project <PROJECT_ID>
gcloud config set compute/region <REGION>
gcloud config set compute/zone <ZONE>
gcloud config configurations list
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

- **Auth issues**: `gcloud auth login` then `gcloud auth list`
- **Wrong project**: `gcloud config get-value project`
- **Region/zone unset**: `gcloud config get-value compute/region|zone`
- **Permissions**: verify IAM roles; **Quotas**: check Cloud Console

Quick diagnostics:

```bash
gcloud auth list
gcloud config list
gcloud config get-value project
gcloud config get-value compute/zone
gcloud config get-value compute/region
```

**Prerequisites:**

- Google Cloud SDK installed (`gcloud` command available)
- Authentication configured (login or service account)
- GCP project configured
