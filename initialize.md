---
description: Initialize projects across any language/framework using official tooling with safe empty-folder validation, and web-powered discovery for unknown stacks
auto_execution_mode: 3
---

# Initialize Workflow

Initialize a new project for virtually any language or framework. This workflow uses an in-memory catalog of common stacks and, when a stack isn’t recognized, discovers the latest official initialization method from the web (preferring official sources) and executes it safely.

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete initialization within 9 steps maximum. If decisions or downloads stall, STOP and ask for clarification.

**DECISION POINTS**: Proceed or STOP. If the directory is not empty, prerequisites are missing, or intent is unclear → STOP with a specific message.

**CONTENT VALIDATION**: Prefer official generators/CLIs/templates and latest stable versions. Validate commands before running.

**TERMINATION CONDITIONS**:

- Terminate when initialization is complete or an error occurs.
- If intent or stack is not clear: Ask for clarification and STOP

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **COLLECT INTENT**
   - Identify the target language/framework (e.g., Next.js, Rails, Spring Boot, Phoenix, Nuxt, Vue, Quarkus, Flask, etc.).
   - Capture options: database (default: Postgres), CSS (default: Tailwind), package manager (npm/pnpm/yarn/bun), and extras (ORM, auth, testing, Docker).
   - If the intent is ambiguous or multiple candidates exist, present choices and STOP awaiting confirmation.

2. **VALIDATE CURRENT DIRECTORY**
   - Always validate directory contents; DO NOT ASSUME.
   - Require explicit developer approval before continuing in a non-empty directory, and propose creating a new subdirectory named for the technology stack to start the initialization process there.
   - Ensure that the current directory is empty except for VCS/OS metadata (allowed: `.git`, `.gitignore`, `.gitattributes`, `.gitkeep`, `.DS_Store`, `.vscode`, `.idea`).
   - Command (outputs any disallowed entries; empty output means OK):

     ```bash
     find . -mindepth 1 -maxdepth 1 -not -name '.git' -not -name '.gitignore' -not -name '.gitattributes' -not -name '.gitkeep' -not -name '.DS_Store' -not -name '.vscode' -not -name '.idea' -print
     ```

3. **CHECK PREREQUISITES (BY STACK)**
   - General: `git --version`.
   - Node stacks (Next.js, Nuxt, Vue/Vite, SvelteKit, Astro, Remix, NestJS, Express): `node -v && npm -v` (or `pnpm -v`/`yarn -v`/`bun -v`).
   - Rails: `ruby -v && gem -v && rails -v`.
   - Spring/Quarkus: `java -version`, plus `curl -V` and `unzip -v`.
   - Python (Django, Flask, FastAPI): `python3 --version`.
   - Elixir/Phoenix: `elixir -v && mix -v`.
   - Go: `go version`.
   - .NET: `dotnet --version`.
   - PHP/Laravel: `php -v && composer --version`.
   - Combine steps into a single line for efficiency if possible.
   - If any critical prerequisite is missing, STOP and provide a concise install hint.

4. **DISCOVER AND VERIFY OFFICIAL INITIALIZATION METHOD**
   - Mandatory step: always perform an internet lookup and verification, even if the stack is recognized by the in-memory catalog.
   - Prefer official domains (examples: nextjs.org, rubyonrails.org, start.spring.io, nuxt.com, vuejs.org, quarkus.io, djangoproject.com, fastapi.tiangolo.com, phoenixframework.org, dotnet.microsoft.com, go.dev, laravel.com, kit.svelte.dev, docs.astro.build, remix.run, expressjs.com, docs.rs/axum).
   - Cross-check with release notes/changelogs and the official “Getting Started” pages. If you cannot verify online, STOP and ask for clarification.
   - MCP searches (run them in order until a relevant result is found that matches the current framework and language; be mindful of documentation for older versions):
     - `brave_web_search "initialize {framework}"`
     - `brave_web_search "{framework} setup latest stable version"`
     - `brave_web_search "official setup guide {framework}"`
   - Extract the official quickstart/initializer command and confirm it is current.
   - Validate command safety (no destructive flags) and required prerequisites.
   - Prefer official generators/CLIs/templates and latest stable versions.

5. **DETERMINE LATEST STABLE VERSIONS**
   - Detect and use the latest stable version of the framework using the GitHub Releases API and any available fetch tool.
     <https://api.github.com/repos/ORG/REPO/releases>
     - Rails: <https://api.github.com/repos/rails/rails/releases>
     - Next.js: <https://api.github.com/repos/vercel/next.js/releases>
     - Nuxt: <https://api.github.com/repos/nuxt/nuxt/releases>
     - Vue: <https://api.github.com/repos/vuejs/vue/releases>
     - Spring Boot: <https://api.github.com/repos/spring-projects/spring-boot/releases>
     - Quarkus: <https://api.github.com/repos/quarkusio/quarkus/releases>
     - Django: <https://api.github.com/repos/django/django/releases>
     - Laravel: <https://api.github.com/repos/laravel/laravel/releases>
     - Flask: <https://api.github.com/repos/pallets/flask/releases>

     If the Github Releases API returns empty (empty array, or Not Found error), fall back to the tags API endpoint, and use the latest tag (e.g., v3.1.0):
     <https://api.github.com/repos/ORG/REPO/tags>

   - Use the latest stable versions for the framework, language, and package manager, matching the local environment unless specified otherwise by the developer. Inform the developer of any mismatches.
   - Match the local environment version for the current framework and language, unless specified otherwise by the developer; inform the developer if it does not match the local environment version.

6. **EXECUTE INITIALIZER (NON-INTERACTIVE)**
   - Parameters (These defaults can be overridden if the developer provides explicit values at the start of the message, use only if the initializer requires them):
     - NAME: {CURRENT_DIRECTORY_NAME}
     - DESCRIPTION: {CURRENT_DIRECTORY_NAME}
     - GROUP_ID: com.patagonia
     - ARTIFACT_ID: {CURRENT_DIRECTORY_NAME}
     - PACKAGE_NAME: com.patagonia.{CURRENT_DIRECTORY_NAME}
     - BASE_DIR: current directory if is empty, else create a new subdirectory with the name of the project
     - CSS: tailwind
     - DOCKER: true
   - Execute the discovered official command in the current directory after completing the verification steps above.
   - Search the initializer's documentation for unattended installation options (e.g., --yes, --non-interactive, --unattended flags) and apply the appropriate method to enable non-interactive mode for initializers requiring parameters.
   - Prefer official generators/CLIs/templates and latest stable versions.
   - Do not retry if a command fails or stalls, STOP and inform the developer.
   - For commands like unzip or curl, do not retry if a command fails or stalls, STOP and inform the developer.
   - DO NOT SKIP: Fail if no possible match is found, for example, if the local environment version is unsupported by the framework or the package manager is not installed. Inform the developer and stop.

7. **SUMMARY WHAT WAS DONE**
   - Prerequisites checked (language, package manager, tooling).
   - Versions verified via official sources and GitHub Releases.
   - Project initialized using the official generator/CLI and latest stable defaults.

8. **NEXT STEPS SUMMARY**
   - Output to the developer a "Next steps" summary (mentioning all the items below) and ask: "Would you like me to run any of these now?" Do not run any commands until explicit approval.

   - Local environment setup
     - Package installation:
       - Node: install with your selected package manager (npm/pnpm/yarn/bun).
       - Python: create venv and install requirements if provided.
       - Ruby: `bundle install`.
       - Java: ensure JDK and build tool (Maven/Gradle) are available.
     - Environment variables:
       - Create `.env` or language-appropriate config; add secrets locally, not to VCS.

   - Run the app (typical commands; consult the framework’s Getting Started page)
     - Node (Next.js/Nuxt/…): `npm run dev` (or `pnpm/yarn/bun` equivalent).
     - Rails: `bin/rails server`.
     - Spring Boot: `./mvnw spring-boot:run` or `./gradlew bootRun`.
     - Django/FastAPI/Flask: `python3 manage.py runserver` or framework’s dev server.

   - Git initialization and Gitignore Setup
     - Ensure an appropriate `.gitignore` exists for the chosen stack.
       - Use Github gitignore repository reference templates according to the stack: <https://github.com/github/gitignore>
       - Common templates: `Node.gitignore`, `Rails.gitignore`, `Python.gitignore`, `Java.gitignore`, `Elixir.gitignore`, `Go.gitignore`, `VisualStudio.gitignore`, `Laravel.gitignore`, `Django.gitignore`.
       - Create or append from a template (choose one matching your stack):

         ```bash
         # Create from a template (overwrites existing .gitignore)
         # Example for Node:
         curl -fsSL https://raw.githubusercontent.com/github/gitignore/main/Node.gitignore > .gitignore

         # Or append to an existing .gitignore
         # Example for Rails:
         curl -fsSL https://raw.githubusercontent.com/github/gitignore/main/Rails.gitignore >> .gitignore
         ```

       - Add local, project-specific exclusions (safe to append; duplicates are okay):

         ```bash
         printf "\n# Local additions\n.env\n.env.local\n.env.*\n.DS_Store\nnode_modules/\n.next/\n.nuxt/\ndist/\nbuild/\ncoverage/\n.vscode/\n.idea/\n.venv/\n" >> .gitignore
         ```

     - Initialize if needed and commit baseline: `git init && git add . && git commit -m "chore: initial scaffold"`.
     - Optionally create the remote and push the initial commit.

   - Quality baseline
     - Formatters/linters: ensure Prettier/ESLint (JS), Black/Ruff (Python), RuboCop (Ruby), Spotless/Checkstyle (Java) are configured.
     - Tests: run the default test task to confirm the scaffold is healthy.

   - Documentation and CI/CD
     - Update `README.md` with stack, commands, env vars, and how to run locally and in production.
     - Add a minimal CI (e.g., install deps, lint, test) using your platform of choice.

   - Optional productionization
     - Containerization (Dockerfile/docker-compose) and health checks.
     - Basic security scan of dependencies and config.
