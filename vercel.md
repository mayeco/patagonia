---
description: Workflow for interacting with Vercel CLI to deploy and manage applications
---

# Vercel CLI Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Interact with Vercel CLI to deploy, manage, and configure applications on the Vercel platform. This workflow handles project deployment, domain management, environment variables, and other Vercel operations.

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Identify the type of Vercel operation requested:
   - Project deployment and management
   - Domain and DNS configuration
   - Environment variables management
   - Team and user account management
   - Build and deployment settings
   - Analytics and monitoring
   - Function and API management

3. Validate Vercel CLI installation and authentication:
   - Check if Vercel CLI is installed
   - Verify user is logged in (vercel whoami)
   - Confirm project context if applicable
   - Validate permissions for requested operations

4. Prepare Vercel CLI command parameters:
   - Parse user request for specific operation
   - Identify required flags and options
   - Prepare file paths, names, and configurations
   - Set appropriate environment and scope

5. Execute Vercel CLI command:
   - Run the prepared command with proper parameters
   - Handle authentication prompts if needed
   - Capture command output and any errors
   - Apply appropriate timeouts for operations

6. Process command results:
   - Display command output to user
   - Interpret success/failure status
   - Provide next steps or follow-up actions
   - Handle any required user confirmations

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
2. **CONFIRM with user** before any destructive action
3. **Show preview** of what will be deleted/destroyed
4. **Provide rollback options** when possible
5. **Document consequences** clearly

### 📋 DESTRUCTIVE COMMAND EXAMPLES (PRINT ONLY):
```bash
# ❌ NEVER EXECUTE - Only print for user review
vercel remove https://my-app.vercel.app
vercel domains rm example.com
vercel env rm DATABASE_URL
vercel rollback https://my-app.vercel.app
vercel teams rm user@example.com
```

### 🎯 EXECUTION PROTOCOL:
1. **Parse** destructive command request
2. **PRINT** the command (do not execute)
3. **WARN** about consequences
4. **ASK** for explicit confirmation
5. **Only execute** after user approval
6. **Provide** rollback information

**REMEMBER: SAFETY FIRST! Always err on the side of caution with destructive operations!**

## Common Vercel CLI Operations

### Project Management
```bash
# Login to Vercel
vercel login

# Check authentication
vercel whoami

# Initialize new project
vercel

# Link existing project
vercel link

# List projects
vercel project ls

# Switch project
vercel switch <project-name>

# Create new project
vercel project add <project-name>
```

### Deployment
```bash
# Deploy current directory (preview)
vercel

# Deploy to production
vercel --prod

# Deploy specific directory
vercel <path-to-directory>

# Deploy with custom name
vercel --name <project-name>

# Redeploy specific deployment
vercel redeploy <deployment-url>

# Remove deployment
vercel remove <deployment-url>
```

### Environment Variables
```bash
# Add environment variable
vercel env add VARIABLE_NAME

# List environment variables
vercel env ls

# Remove environment variable
vercel env rm VARIABLE_NAME

# Pull environment variables
vercel env pull .env.local
```

### Domain Management
```bash
# Add custom domain
vercel domains add example.com

# List domains
vercel domains ls

# Remove domain
vercel domains rm example.com

# Verify domain
vercel domains inspect example.com
```

### Build and Development
```bash
# Start development server
vercel dev

# Build project locally
vercel build

# View build logs
vercel logs <deployment-url>

# Clear build cache
vercel build --clear-cache
```

### Team and Collaboration
```bash
# List teams
vercel teams ls

# Switch team
vercel teams switch <team-slug>

# Add team member
vercel teams add <email>

# List team members
vercel teams ls <team-slug>
```

### Functions and APIs
```bash
# Deploy serverless function
vercel --prod api/my-function.js

# List deployments
vercel ls

# View deployment details
vercel inspect <deployment-url>

# Rollback deployment
vercel rollback <deployment-url>
```

## Global Options

Vercel CLI provides several global options that can be used with any command. These options are commonly available across all Vercel CLI commands.

### Current Working Directory
```bash
--cwd <path>
```
Specify a working directory different from the current directory.

```bash
# Example: Deploy from a different directory
vercel --cwd ~/my-project --prod

# Example: Use relative path
vercel --cwd ./subfolder
```

### Debug Mode
```bash
--debug
-d
```
Enable verbose debug output for troubleshooting.

```bash
# Example: Debug deployment issues
vercel --debug

# Example: Debug with production flag
vercel --prod --debug
```

### Global Configuration
```bash
--global-config <path>
-Q <path>
```
Set the path to the global configuration directory.

```bash
# Example: Use custom global config
vercel --global-config /custom/config/path login
```

### Help
```bash
--help
-h
```
Display help information for commands.

```bash
# Example: Get general help
vercel --help

# Example: Get help for specific command
vercel deploy --help
```

### Local Configuration
```bash
--local-config <path>
-A <path>
```
Specify path to a local vercel.json configuration file.

```bash
# Example: Use custom config file
vercel --local-config ./custom-config.json

# Example: Deploy with specific config
vercel --local-config /path/to/vercel.json --prod
```

### Scope
```bash
--scope <team-slug>
-S <team-slug>
```
Execute commands within a specific team scope.

```bash
# Example: Deploy to team scope
vercel --scope my-team-slug --prod

# Example: List projects for specific team
vercel --scope my-team-slug project ls
```

### Authentication Token
```bash
--token <token>
-t <token>
```
Use a specific authentication token (useful for CI/CD).

```bash
# Example: Deploy with token (CI/CD)
vercel --token abc123def456 --prod

# Example: Use environment variable
vercel --token $VERCEL_TOKEN
```

### No Color Output
```bash
--no-color
NO_COLOR=1
```
Disable color and emoji output (respects NO_COLOR standard).

```bash
# Example: Plain text output
vercel login --no-color

# Example: Using environment variable
NO_COLOR=1 vercel
```

### Common Usage Patterns

```bash
# CI/CD deployment with token and no color
vercel --token $VERCEL_TOKEN --no-color --prod

# Debug deployment in specific directory
vercel --cwd ./my-app --debug

# Deploy with custom config and team scope
vercel --scope my-team --local-config ./vercel.prod.json --prod

# Get help for any command
vercel deploy --help
```

**NOTE:** Global options can be combined with any Vercel CLI command and should be placed before the specific command.

## Advanced Configuration

### vercel.json Configuration
```json
{
  "name": "my-app",
  "version": 2,
  "builds": [
    { "src": "package.json", "use": "@vercel/next" },
    { "src": "api/**/*.js", "use": "@vercel/node" }
  ],
  "routes": [
    { "src": "/api/(.*)", "dest": "/api/$1" },
    { "src": "/(.*)", "dest": "/$1" }
  ],
  "env": {
    "NODE_ENV": "production"
  }
}
```

### Environment-Specific Settings
```bash
# Development deployment
vercel --dev

# Production deployment
vercel --prod

# Staging environment
vercel --target staging
```

## Framework-Specific Deployments

### Next.js
```bash
# Deploy Next.js app
vercel --prod

# With custom build command
vercel --build-command "npm run build"
```

### React
```bash
# Deploy Create React App
vercel --prod

# With SPA routing
# Add _redirects file: /* /index.html 200
```

### Vue.js
```bash
# Deploy Vue app
vercel --prod

# With Vue Router history mode
# Add vercel.json with SPA routing rules
```

### Angular
```bash
# Deploy Angular app
vercel --prod

# With Angular Universal
vercel --build-command "npm run build:ssr"
```

## Monitoring and Analytics

### Deployment Monitoring
```bash
# View real-time logs
vercel logs --follow

# View logs for specific deployment
vercel logs <deployment-url>

# View analytics
vercel analytics <project-name>
```

### Performance Monitoring
```bash
# Check deployment status
vercel inspect <deployment-url>

# View build information
vercel build --debug
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

### GitHub Actions Example
```yaml
name: Deploy to Vercel
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install Vercel CLI
        run: npm i -g vercel
      - name: Deploy to Vercel
        run: vercel --prod --yes
        env:
          VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
```

### GitLab CI Example
```yaml
deploy:
  script:
    - npm i -g vercel
    - vercel --prod --yes
  environment:
    name: production
    url: https://my-app.vercel.app
  only:
    - main
```

## Cost Optimization

### Performance Tips
- Use appropriate compute resources
- Implement proper caching strategies
- Optimize bundle sizes
- Use CDN effectively

### Cost Monitoring
- Monitor usage in Vercel dashboard
- Set up billing alerts
- Review deployment frequency
- Optimize function execution times

**IMPORTANT:** Always provide responses in Spanish by default, unless the developer clearly specifies English.

**Language Support:**
- **Spanish**: DEFAULT - Interactuar con Vercel CLI y explicar en español para TODA entrada
- **English**: Interact with Vercel CLI in English only if explicitly requested
- **Other**: Interact with Vercel CLI in Spanish as default, but adapt to detected language when possible

**Prerequisites:**
- Node.js installed (version 14+)
- Vercel CLI installed (`npm i -g vercel`)
- Vercel account and authentication
- Project ready for deployment
- Proper build configuration