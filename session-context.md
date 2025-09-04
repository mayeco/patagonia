---
description: Session-level context management for efficiency optimization
---

# Session Context Management

Optimized context management to reduce redundant operations across workflow executions within the same session.

## Session Variables

### Language Preference Cache

- **session_language**: Detected user language (Spanish/English)
- **language_confidence**: Confidence level of detection (high/medium/low)
- **language_source**: Source of detection (explicit/inferred/default)

### Project Context Cache

- **project_type**: Detected project framework/type
- **project_structure**: Key directories and files identified
- **dependencies_scanned**: Whether dependency analysis was completed

### User Preferences Cache

- **auto_approve_safe**: Whether user prefers auto-approval for safe operations
- **confirmation_level**: User's preferred confirmation level (minimal/standard/verbose)
- **output_format**: Preferred output format (concise/detailed/structured)

## Efficiency Patterns

### Language Detection Optimization

```markdown
0. **OPTIMIZED LANGUAGE DETECTION**:
   - Check session_language cache first
   - If cached with high confidence: Skip detection, use cached value
   - If cached with medium confidence: Quick validation only
   - If not cached or low confidence: Full detection and cache result
   - Default to Spanish if no clear indicators found
```

### Project Context Reuse

```markdown
1. **PROJECT CONTEXT OPTIMIZATION**:
   - Check project_structure cache for known patterns
   - Reuse dependency analysis results when available
   - Skip redundant file system scans within session
```

### Batch Operation Templates

```markdown
2. **BATCH OPERATIONS**:
   - Group related file operations
   - Minimize I/O overhead
   - Use atomic operations where possible
```

## Implementation Guidelines

### Cache Invalidation

- Clear caches on explicit user language switch
- Invalidate project cache on significant file changes
- Reset preferences on user request

### Fallback Behavior

- Always fall back to standard detection if cache fails
- Maintain backward compatibility with existing workflows
- Graceful degradation when optimization unavailable

### Performance Monitoring

- Track cache hit rates
- Monitor execution time improvements
- Measure user satisfaction with reduced confirmations
