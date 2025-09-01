# PatagonAI Workflows

[![License: Unlicense](https://img.shields.io/badge/license-Unlicense-blue.svg)](https://unlicense.org/)
[![Version](https://img.shields.io/badge/version-v0.1.0--alpha.5-blue.svg)](https://github.com/mayeco/patagonia/releases/tag/v0.1.0-alpha.5)

Centralized workflows to standardize common tasks across projects (planning, implementation, docs, security, deployments, schema discovery, etc.). Use these via slash-commands in your IDE assistant.

## How to use

- Run a workflow: type its slash-command in chat, optionally with a target file/path.
  - Example: `/generate-readme` to generate or update the project README
  - Example: `/schema` to detect the framework and persist a schema snapshot
- Language handling is defined only in Step 0 of each workflow. Default to Spanish unless the input is clearly English.

## Repository structure

- `.windsurf/` — internal workspace folder
- `CHANGELOG.md` — changelog
- `LICENSE.md` — license
- `README.md` — this file
- `VERSION` — version file
- Workflow specs (Markdown) at repo root:
  - `backlog.md`, `cxone.md`, `docs.md`, `ELI5.md`, `epic.md`, `error-continue.md`, `feature.md`, `gcloud.md`, `generate-changelog.md`, `generate-readme.md`, `git-status.md`, `implement.md`, `initialize.md`, `memory.md`, `memento.md`, `no-continue.md`, `project.md`, `rate-request.md`, `release.md`, `remember.md`, `rules.md`, `schema.md`, `template.md`, `terraform.md`, `tsc-fix.md`, `vercel.md`

## Workflow index (slash-commands)

- /ELI5 — Explain concepts simply
- /backlog — Create backlog epics/features with priorities
- /generate-changelog — Generate changelog from git history
- /cxone — Run Checkmarx One CLI security analysis
- /docs — Retrieve and summarize technology documentation
- /epic — Create high-level epics from goals
- /error-continue — Continue after an IDE/tooling error with guardrails
- /feature — Draft a focused feature spec
- /gcloud — Execute Google Cloud CLI actions per instructions
- /git-status — Inspect repo status and pending changes
- /implement — Start implementing based on a plan or open text
- /initialize — Initialize projects across any language/framework using official tooling
- /memory — Create/update/delete persistent assistant memories
- /memento — Reset the current conversation reasoning context
- /no-continue — Pause execution until explicit confirmation
- /project — Plan multi-feature projects with milestones
- /rate-request — Assess clarity and completeness of a request
- /generate-readme — Generate or update README.md for the project
- /release — Prepare releases using Semantic Versioning
- /remember — Persist durable instructions across the workspace
- /rules — AI-Optimized Pure Coding Rules reference
- /schema — Detect framework, locate schema/migrations, extract and persist a compact schema snapshot
- /template — Boilerplate workflow template for new workflows
- /terraform — Generate Terraform IaC from project analysis
- /tsc-fix — Fix TypeScript compiler errors automatically
- /vercel — Deploy/manage apps with Vercel CLI

## Contributing a new workflow

- Start from `template.md` and adjust:
  - Frontmatter `description` succinctly explains the workflow.
  - Add a domain-specific “⚠️ CRITICAL AI EXECUTION RULES” section.
  - Steps: put all language handling in Step 0 only. Keep steps actionable and bounded.
- Save as `<name>.md` and reference the filename as the slash-command.

## Notes

- These workflows are workspace-agnostic but can store context using the Memory Workflow, scoped to the current workspace corpus.
