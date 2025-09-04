---
description: Workflow to detect framework, discover database schema, and persist a compact schema snapshot
auto_execution_mode: 3
---

# Project Schema Workflow

Operational workflow for discovering the project's database schema and making it available for future reasoning.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK**: Complete schema discovery within 5 search attempts/paths, maximum; then ask the developer for a path and STOP.

**NON-DESTRUCTIVE**: Never modify project files or execute migrations/DB commands.

**PRIVACY AND SIZE**: Do not store secrets or full dumps. Persist concise summaries and file paths.

**CONFIRMATION POINTS**: Confirm before overwriting an existing schema snapshot.

**TERMINATION CONDITIONS**:

- If no schema/migrations are found and no user-provided path: Ask and STOP
- If multiple frameworks detected with conflicting hints: Ask the developer to choose and STOP
- If files are unreadable or permissions are restricted: Report the issue and STOP

## STEPS

0. **OPTIMIZED LANGUAGE DETECTION**:
   - Check session language cache first (if available)
   - If cached with high confidence: Use cached language preference
   - If not cached: Detect user's input language (default to Spanish if not clearly English)
   - Additionally, infer from recent previous messages; if unclear, default to Spanish
   - Cache detection result for session efficiency
   - Always provide responses in Spanish by default, unless developer clearly specifies English

1. **OPTIMIZED FRAMEWORK DETECTION**:
   - Check session project context cache first (if available)
   - If cached: Use known framework/ORM information
   - If not cached: Inspect repository indicators to infer framework/ORM:
     - JavaScript/TypeScript: `package.json` deps: `prisma`, `@prisma/client`, `typeorm`, `sequelize`, `knex`; files: `prisma/schema.prisma`, `knexfile.*`, `ormconfig.*`, `src/migrations/`
     - Python: `pyproject.toml`/`requirements.txt`: `django`, `sqlalchemy`, `alembic`; files: `manage.py`, `migrations/`, `alembic.ini`, `alembic/versions/`
     - Ruby on Rails: `Gemfile`: `rails`; files: `db/schema.rb`, `db/structure.sql`, `db/migrate/`
     - PHP Laravel: `composer.json`: `laravel/framework`; files: `database/migrations/`
     - .NET EF Core: `*.csproj`: `Microsoft.EntityFrameworkCore.*`; files: `Migrations/`
     - Java Spring: `pom.xml`/Gradle: `liquibase`, `flyway`; files: `db/changelog*/`, `db/migration*/`
     - Go: `go.mod`: `gorm.io/gorm`; files: `migrations/`
   - Cache framework detection result for session efficiency
   - If multiple candidates, pick the one with an explicit schema file; otherwise ask the developer to choose

2. **LOCATE SCHEMA OR MIGRATIONS**:
   - Preferred sources (in order):
     - `prisma/schema.prisma`
     - Rails: `db/schema.rb` or `db/structure.sql`
     - Project-level: `database/schema.sql`, `schema.sql`, `structure.sql`
     - Liquibase/Flyway changelogs under `db/changelog*` or `db/migration*`
     - Migrations directories: `db/migrate/`, `database/migrations/`, `migrations/`, `alembic/versions/`, `prisma/migrations/*/migration.sql`, `src/migrations/`
   - Search patterns: files `schema.prisma`, `schema.sql`, `structure.sql`, `db/schema.rb`; dirs `prisma/`, `db/migrate/`, `database/migrations/`, `migrations/`, `alembic/`, `prisma/migrations/`.
   - If none are found, ask the developer for the schema path or ORM used and STOP.

3. **READ AND EXTRACT SCHEMA**:
   - Parse and normalize key entities: tables, columns (name, type, nullable), PKs, FKs, uniques/indexes, enums, and relations.
   - For migrations-only projects, infer latest state using ordering heuristics (timestamps/sequence) without executing code.
   - Record the exact source files/paths used.

4. **PERSIST COMPACT SNAPSHOT**:
   - Use the Memory Workflow to create/update a schema snapshot.
   - Title: `Schema Snapshot (<framework>)`
   - Content: concise summary (counts, key relations/enums/indexes) + source file paths.
   - Tags: `schema_snapshot`, `framework_<name>`, `database_schema`
   - Prefer an update if a prior snapshot exists; otherwise create.

5. **CACHE FOR SESSION USE**:
   - Keep the parsed structure in working context for answering future queries and validations.

6. **REFRESH POLICY**:
   - On changes to schema files or new migrations detected, re-run steps 2–4 and update the snapshot.

7. **OUTPUT SUMMARY**:
   - Report detected framework, sources used, counts (tables/entities), memory action (created/updated), and any next steps.
