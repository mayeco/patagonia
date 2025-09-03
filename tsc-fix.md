---
description: Fix all TypeScript compiler errors and type issues
auto_execution_mode: 3
---

# TSC-FIX Workflow

Fix all TypeScript compiler (TSC) errors including type errors, syntax errors, module resolution errors, and compilation issues in TypeScript files.

## Important Rules

- TARGET_ACTIVE_SHELL_COMMANDS

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete TSC error fixing within 7 steps maximum.

**DECISION POINTS**: Make binary decisions - errors are fixable or require developer input.

**VALIDATION**: Validate TypeScript files and compilation before fixing.

**TERMINATION CONDITIONS**:

- If no TypeScript files found: Ask the developer for files and STOP
- If errors are complex: Ask the developer for clarification and STOP
- Always require developer confirmation before applying fixes

## STEPS

0. **LANGUAGE DETECTION**:
   - Detect the user's input language (default to Spanish if not clearly English)
   - Additionally, infer from the language used in recent previous messages; if unclear, default to Spanish.
   - If no clear English indicators are found, default to Spanish for all responses
   - Always provide responses in Spanish by default, unless the developer clearly specifies English.

1. **DETECT TYPESCRIPT FILES AND COMPILATION ERRORS**:
   - Detect TypeScript files and compilation errors

2. **IDENTIFY TYPESCRIPT CONTENT TO ANALYZE**:
   - If input is a .ts/.tsx file path, read the file content
   - If input is a directory path, scan for TypeScript files and tsconfig.json
   - If input contains TypeScript code, analyze for compilation errors
   - If input mentions TSC errors, focus on those specific compilation issues

3. **ANALYZE TYPESCRIPT COMPILER ERRORS**:
   - **Type Errors**: Property access, type assignments, argument mismatches
   - **Module Errors**: Cannot find modules, wrong import paths
   - **Declaration Errors**: Cannot find names, missing declarations
   - Ensure type safety is maintained across all files
   - Verify no new compilation errors were introduced

4. **PROVIDE THE CORRECTED VERSION** with comprehensive TypeScript error explanations

5. **SUMMARIZE MULTI-FILE FIXES**: If multiple TypeScript files are involved, provide a summary of all compilation fixes

6. **DEVELOPER CONFIRMATION**: Ask if the developer wants to apply the TypeScript compilation fixes

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

**TSC-FIX Style Guidelines:**

- Focus on all TypeScript compiler errors and compilation issues
- Provide specific TSC error codes and their detailed meanings
- Show before/after examples with complete type annotations
- Explain the TypeScript compilation process and type theory
- Use TSC compiler output to identify exact error locations and suggestions
- Suggest TypeScript best practices and compiler optimization
- Provide tsconfig.json updates when configuration issues are found
- Ask for confirmation before applying comprehensive compilation fixes
