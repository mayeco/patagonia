---
description: Fix all TypeScript compiler errors and type issues
---

# TSC-FIX Workflow

Fix all TypeScript compiler (TSC) errors including type errors, syntax errors, module resolution errors, and compilation issues in TypeScript files.

# TSC-FIX Workflow

Fix all TypeScript compiler (TSC) errors including type errors, syntax errors, module resolution errors, and compilation issues in TypeScript files.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete TypeScript error fixing within 8 steps maximum. If fixing takes too long, provide best effort fixes and stop.

**DECISION POINTS**: Make binary decisions quickly - error can be fixed or requires user input.

**TERMINATION CONDITIONS**:
- If no TypeScript files found: Stop with clear message
- If tsc command fails: Stop with error details
- If user declines fixes: Stop immediately
- Always ask for user confirmation before applying changes

## Steps

0. **LANGUAGE DETECTION**: Check for English keywords ("typescript", "tsc", "type"). Default to Spanish.

1. **INPUT ANALYSIS**:
   - If specific file path: Read and analyze that file
   - If directory: Scan for .ts/.tsx files and tsconfig.json
   - If code snippet: Analyze directly for errors
   - Identify TypeScript version and configuration

2. **ERROR DETECTION**:
   - Execute `tsc --noEmit --pretty` to get all compilation errors
   - Parse error output for error codes, file locations, messages
   - Categorize errors: type, module, syntax, configuration
   - Prioritize critical errors over warnings

3. **ERROR ANALYSIS** (Limited scope):
   - Focus on first 10 most critical errors
   - Analyze error context and root cause
   - Determine fix feasibility (automatic vs manual)
   - Skip complex refactoring errors

4. **FIX APPLICATION**:
   - Apply fixes for clear, unambiguous errors
   - Add missing type annotations
   - Fix import/export statements
   - Correct syntax errors
   - Update configuration if needed

5. **VALIDATION**:
   - Execute `tsc --noEmit` to verify fixes
   - Check that no new errors were introduced
   - Ensure type safety is maintained

6. **USER CONFIRMATION**:
   - Present all proposed fixes clearly
   - Ask user to confirm application of changes
   - If declined: Stop without applying changes
   - If approved: Apply all fixes

7. **COMPLETION REPORT**:
   - Provide summary of all fixes applied
   - List any remaining errors or warnings
   - Suggest next steps for remaining issues

## Comprehensive TSC Error Categories

### TYPE_ERRORS
- **TS2339**: Property does not exist on type
- **TS2322**: Type assignment mismatch
- **TS2345**: Argument type mismatch
- **TS2323**: Cannot redeclare block-scoped variable
- **TS2300**: Duplicate identifier
- **TS2335**: Super cannot be referenced

### MODULE_ERRORS
- **TS2307**: Cannot find module
- **TS2306**: File not found
- **TS2303**: Circular dependency detected
- **TS1202**: Import/export in ambient module
- **TS2436**: Import name conflict
- **TS2305**: Module has no default export

### DECLARATION_ERRORS
- **TS2304**: Cannot find name
- **TS2308**: Member is private
- **TS2309**: Property is missing in type
- **TS2310**: Type has no properties in common
- **TS2311**: Type has no call signatures
- **TS2312**: Type is not assignable to other type

### SYNTAX_ERRORS
- **TS1003**: Identifier expected
- **TS1005**: Semicolon expected
- **TS1011**: Element implicitly has any type
- **TS1029**: Trailing comma not allowed
- **TS1030**: Async functions must have exactly one parameter
- **TS1109**: Expression expected

### STRICT_MODE_ERRORS
- **TS2454**: Variable is used before being assigned
- **TS18046**: Property is optional but must be provided
- **TS18047**: Strict mode requires explicit types
- **TS18048**: Cannot assign to read-only property
- **TS18049**: Property does not exist on never type
- **TS18050**: Type assertion requires strict mode

### CONFIGURATION_ERRORS
- **TS5012**: Cannot find tsconfig.json
- **TS6047**: File extension not allowed
- **TS6054**: File not included in compilation
- **TS18002**: Target requires lib
- **TS18003**: Experimental decorators not enabled
- **TS5055**: Cannot write file because it would overwrite

## Comprehensive TSC Correction Strategies

### TYPE_CORRECTIONS
- Add explicit type annotations for variables and functions
- Use union types (`string | number`) for multiple possible types
- Implement interface extensions and type intersections
- Apply generic constraints and type parameters correctly
- Use type guards and discriminated unions for type safety

### MODULE_CORRECTIONS
- Fix import paths to correct relative/absolute locations
- Add missing type definition files (`@types/package`)
- Create proper module declarations for untyped modules
- Fix export/import syntax and naming conflicts
- Resolve circular dependency issues

### DECLARATION_CORRECTIONS
- Add missing variable and function declarations
- Fix scope issues and variable shadowing
- Implement proper class member visibility (public/private)
- Add interface implementations and abstract class extensions
- Fix method overriding and overloading signatures

### SYNTAX_CORRECTIONS
- Add missing brackets, parentheses, and semicolons
- Fix malformed function and class declarations
- Correct import/export statement syntax
- Fix operator precedence and expression syntax
- Resolve statement termination issues

### STRICT_MODE_CORRECTIONS
- Add definite assignment assertions (`!`) for initialization checks
- Implement null/undefined checks with optional chaining
- Add explicit type annotations for strict type checking
- Use readonly modifiers for immutable properties
- Implement proper type narrowing techniques

### CONFIGURATION_CORRECTIONS
- Update tsconfig.json compiler options for compatibility
- Add missing type library references (`"lib": ["es2020"]`)
- Configure module resolution settings
- Enable/disable strict mode features appropriately
- Set proper target and module compilation settings

**Language Support:**
- **Spanish**: DEFAULT - Corregir errores de TSC y explicar en español
- **English**: SOLO si el usuario especifica claramente "fix TSC errors in English"
- **Other**: Siempre responder en español por defecto

**IMPORTANT:** Always default to Spanish corrections and explanations unless the user explicitly requests English.

**TSC-FIX Style Guidelines:**
- Focus on all TypeScript compiler errors and compilation issues
- Provide specific TSC error codes and their detailed meanings
- Show before/after examples with complete type annotations
- Explain the TypeScript compilation process and type theory
- Use TSC compiler output to identify exact error locations and suggestions
- Suggest TypeScript best practices and compiler optimization
- Provide tsconfig.json updates when configuration issues are found
- Ask for confirmation before applying comprehensive compilation fixes