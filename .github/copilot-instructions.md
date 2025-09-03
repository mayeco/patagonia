# Copilot Validation Instructions

Purpose: Guide the Copilot agent to validate repository RULES and WORKFLOWS during proposals, code changes, and PR reviews.

## Scope
- Validate RULES in [rules.md](../rules.md).
- Validate all workflows in the repo root (e.g., `/initialize.md`, `/implement.md`, `/vercel.md`, `/schema.md`, `/tsc-fix.md`, `/docs.md`, `/generate-readme.md`, `/generate-changelog.md`, `/git-status.md`, `/remember.md`, `/memory.md`, `/error-continue.md`, `/no-continue.md`, `/backlog.md`, etc.).
- Apply to: pull requests, code suggestions, and automated actions.

## When To Run Validation
- On PR open/update.
- When modifying any `.md` workflow, `.github/*`, or [rules.md](../rules.md).
- When automated suggestions propose commands or code edits.

## RULES Checklist (from [rules.md](../rules.md))
- Command Execution
  - Shell detection: avoid assuming POSIX; detect shell when needed.
  - No implicit `cd`; use explicit working directory.
  - Prefer quiet flags; preserve stderr; no blind `2>/dev/null`.
  - Single-line efficient chains with `&&`; avoid prompting.
  - URL-encode query/form data; avoid inline JSON; prefer `jq -n` to build JSON.
  - Guard auto-run: do not auto-run destructive or unquoted/unsafe commands.

- Auto-run vs Approval
  - Auto-run only read-only or clearly non-destructive actions.
  - Require explicit approval for destructive/system-changing/file-mutating commands.

- Code Generation Constraints
  - Respect complexity/length limits and “Non-Compliant Code Augmentation Ban”.
  - If target unit exceeds limits, require refactor-first; no augmentation allowed.

- Core Coding Directives
  - Readability > cleverness; single responsibility; consistency in naming, formatting.
  - Security checks: input validation, authN/Z, encryption where relevant.
  - Testing mandate: tests for new code; cover error paths and edge cases.

- Standards & Patterns
  - Inline readability (no cryptic one-liners).
  - Naming by language conventions.
  - Consistent formatting (e.g., Prettier/PEP8 style).
  - Organization: clear import order, modular design.
  - Algorithmic complexity awareness.
  - No magic numbers; use constants.
  - Comment quality: explain why, keep in sync.
  - Structured logging.

## WORKFLOWS Checklist
For each workflow file:
- Title and purpose are clear.
- Steps are reproducible and unambiguous.
- If a step runs commands:
  - Conforms to Command Execution rules above.
  - Uses non-interactive flags and safe defaults.
  - Explicitly calls out shell when non-portable syntax is used.
- If a step suggests auto-run:
  - Only for read-only or clearly non-destructive steps.
  - Otherwise mark as “requires approval”.
- References to paths, files, or commands are accurate and exist.

Special workflows to cross-check quickly:
- `/initialize.md`: safe project init; no destructive defaults; non-interactive flags.
- `/implement.md`: enforce plan identification, discovery, clarification, and termination conditions; do not proceed without explicit confirmation when required.
- `/schema.md`: safe discovery; clearly separates read-only inspection vs write actions.
- `/vercel.md` and `/gcloud.md`: never expose secrets; require approval for deploys.
- `/tsc-fix.md`: avoids destructive file edits; uses lints safely.
- `/docs.md` and `/generate-readme.md`: read-only or clearly marked write steps.

## Failure Modes To Flag
- Any command that writes/deletes/mutates without explicit approval.
- Inline JSON in shells when a safer builder is applicable.
- Commands requiring URL-encoding that skip it.
- Use of `cd` where CWD should be specified externally.
- Non-portable shell features without explicit shell wrapper.
- Adding code to a function/class already exceeding constraints.
- Workflows missing termination or approval gates.

## PR Review Output Template
Post a single structured comment with this format:

```
Copilot RULES/WORKFLOWS Validation

Summary
- Overall status: PASS | WARN | FAIL
- Files checked: [list]

RULES Findings
- [PASS|WARN|FAIL] Command Execution: <brief note>
- [PASS|WARN|FAIL] Auto-run vs Approval: <brief note>
- [PASS|WARN|FAIL] Code Constraints: <brief note>
- [PASS|WARN|FAIL] Coding Standards/Patterns: <brief note>

WORKFLOWS Findings
- <workflow-file>: [PASS|WARN|FAIL] — <brief note>
- …

Blocking Items (if any)
- <short actionable list>

Non-Blocking Suggestions
- <bullets>

Next Steps
- If FAIL: address blocking items and re-request review.
- If WARN: consider fixes; not blocking unless policy requires.
```

## Agent Behavior
- Prefer minimal, actionable feedback.
- Cite exact files and lines when possible.
- Do not propose or run destructive commands automatically.
- When in doubt, default to safety and request explicit approval.

## Next Steps
- Use this checklist on every PR or suggestion affecting `rules.md`, workflows, or `.github/*`.
- If a violation is found, block with clear, line-referenced fixes.
