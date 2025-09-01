---
description: Workflow for interacting with Vercel CLI to deploy and manage applications
---

# Vercel CLI Workflow

Vercel CLI is a command-line interface for interacting with the Vercel platform. It allows you to deploy and manage applications on the Vercel platform.

## Important Rules
- TARGET_ACTIVE_SHELL_COMMANDS

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Interact with Vercel CLI to deploy, manage, and configure applications on the Vercel platform. This workflow handles project deployment, domain management, environment variables, and other Vercel operations.

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **OPERATION IDENTIFICATION**: Identify the type of Vercel operation requested:
   - Project deployment and management
   - Domain and DNS configuration
   - Environment variables management
   - Team and developer account management
   - Build and deployment settings
   - Analytics and monitoring
   - Function and API management

2. **ENVIRONMENT VALIDATION**:
   - Execute: `vercel --version`
   - If command fails: STOP - "Vercel CLI not installed - ensure vercel is available"
   - Execute: `vercel whoami`
   - If command fails: STOP - "Not logged in to Vercel - run 'vercel login' first"
   - Check current project if applicable

3. **COMMAND CONSTRUCTION**:
   - Map operation to specific vercel command
   - Add required flags and options
   - Include project name, team, region as needed
   - Validate command syntax mentally

4. **SAFETY CHECK**:
   - Scan command for destructive keywords: remove, delete, destroy
   - If found: Ask developer for explicit confirmation
   - If developer denies: STOP with safety message
   - If developer confirms: Proceed to execution

5. **COMMAND EXECUTION**:
   - Execute prepared vercel command
   - Set reasonable timeout (60-120 seconds for deployments)
   - Capture stdout, stderr, and exit code
   - If command fails: Parse error output and STOP with specific error message
   - Do NOT attempt alternative commands or installations

6. **RESULT PROCESSING**: Process command results:
   - Display command output to developer
   - Interpret success/failure status
   - Provide next steps or follow-up actions
   - Handle any required developer confirmations

# 🚨🚨🚨 CRITICAL WARNING: DESTRUCTIVE OPERATIONS 🚨🚨🚨

## ⚠️⚠️⚠️ NEVER EXECUTE DESTRUCTIVE COMMANDS ⚠️⚠️⚠️

**IMPORTANT SAFETY PROTOCOLS:**

### ❌ DESTRUCTIVE COMMANDS - PRINT ONLY, NEVER EXECUTE:
- **DELETE Operations**: `vercel remove <deployment-url>`, `vercel domains rm <domain>`
- **REMOVE/DESTROY**: `vercel env rm <variable-name>`, `vercel teams rm <member>`
- **DROP/TERMINATE**: `vercel rollback <deployment-url>` (can break current deployment)
- **Any command with**: `--force`, `--yes`, `--delete`, `--remove`, `--destroy`

### 🛡️ SAFETY MEASURES:
1. **ALWAYS PRINT the command first** - Never execute directly
2. **CONFIRM with developer** before any destructive action
3. **Show preview** of what will be deleted/destroyed
4. **Provide rollback options** when possible
5. **Document consequences** clearly

### 📋 DESTRUCTIVE COMMAND EXAMPLES (PRINT ONLY):
```bash
# ❌ NEVER EXECUTE - Only print for developer review
vercel remove https://my-app.vercel.app
vercel domains rm example.com
vercel env rm DATABASE_URL
vercel rollback https://my-app.vercel.app
vercel teams rm developer@example.com
```

### 🎯 EXECUTION PROTOCOL:
1. **Parse** destructive command request
2. **PRINT** the command (do not execute)
3. **WARN** about consequences
4. **ASK** for explicit confirmation
5. **Only execute** after developer approval
6. **Provide** rollback information

**REMEMBER: SAFETY FIRST! Always err on the side of caution with destructive operations!**

## Common Vercel CLI Operations

```bash
# Auth & Project
vercel login
vercel whoami
vercel link                 # link existing repo/folder
vercel project ls
vercel switch <project>

# Deploy
vercel                      # preview
vercel --prod               # production
vercel <dir>                # deploy specific folder
vercel redeploy <deploy-url>
vercel rollback <deploy-url>  # confirm before using

# Env vars
vercel env add NAME
vercel env ls
vercel env pull .env.local

# Domains
vercel domains add example.com
vercel domains ls
vercel domains inspect example.com

# Teams
vercel teams ls
vercel teams switch <team-slug>
vercel teams add <email>

# Logs & Inspect
vercel logs <deploy-url>
vercel inspect <deploy-url>
vercel build --clear-cache

# Functions
vercel --prod api/my-function.js
vercel ls
```

## Global Options

Common flags (mix and match before the command):

- `--cwd <path>` Use different working directory
- `--debug` or `-d` Verbose output
- `--global-config <path>` or `-Q <path>` Custom global config dir
- `--local-config <path>` or `-A <path>` Use specific vercel.json
- `--scope <team-slug>` or `-S <team-slug>` Team scope
- `--token <token>` or `-t <token>` Auth token (CI)
- `--no-color` or env `NO_COLOR=1` Disable colors
- `--help` or `-h` Help for any command

Examples:
```bash
vercel --token $VERCEL_TOKEN --no-color --prod
vercel --cwd ./app --debug
vercel --scope my-team --local-config ./vercel.prod.json --prod
```

## Advanced Configuration

- Use `vercel.json` for custom builds, routes, and env.
- Reference: https://vercel.com/docs/projects/project-configuration
- Quick examples:
```bash
vercel --prod                  # prod deploy
vercel --target staging        # staging target
vercel --build-command "npm run build"  # custom build
```

## Framework-Specific Deployments

- Most frameworks are auto-detected; run `vercel --prod`.
- For custom builds or SPA routing, use `--build-command` or `vercel.json`.

## Monitoring and Analytics

```bash
vercel logs --follow
vercel logs <deploy-url>
vercel inspect <deploy-url>
vercel analytics <project-name>
```

## Security Best Practices

### Environment Variables
- Never commit sensitive environment variables
- Use `vercel env` commands for secure variable management
- Use different variables for different environments

### Authentication
- Use Vercel CLI authentication for secure deployments
- Implement proper team permissions
- Regular token rotation

### Domain Security
- Verify domain ownership before adding
- Use HTTPS always (enforced by default)
- Implement proper CORS policies

## Troubleshooting

### Common Issues
- **Authentication errors**: Run `vercel login`
- **Build failures**: Check build logs with `vercel logs`
- **Domain issues**: Verify DNS configuration
- **Environment variables**: Ensure variables are set correctly
- **Unknown option errors**: Update Vercel CLI to latest version (`pnpm i -g vercel@latest`)
- **--project flag error**: Use `vercel project ls` instead of `--project` flag

### Debug Commands
```bash
# Debug deployment
vercel --debug

# View logs for specific deployment
vercel logs <deployment-url>

# Check CLI version
vercel --version

# Clear cache
vercel build --clear-cache
```

## CI/CD Integration

Minimal GitHub Actions:
```yaml
name: Deploy to Vercel
on: { push: { branches: [ main ] } }
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm i -g vercel
      - run: vercel --prod --yes
        env: { VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }} }
```

## Cost Optimization

- Use caching/CDN, optimize bundles
- Monitor usage and set billing alerts
- Avoid unnecessary redeploys and long-running builds

**Prerequisites:**
- Node.js installed (version 14+)
- Vercel CLI installed (`npm i -g vercel`)
- Vercel account and authentication
- Project ready for deployment
- Proper build configuration