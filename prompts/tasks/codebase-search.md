# Codebase Search Task

**Objective**: Efficiently search and analyze code across a project for patterns, functions, or implementations.

## Prerequisites

- Read access to target codebase
- Basic understanding of project structure
- Search tools available (grep, ripgrep, or equivalent)

## Parameters

```yaml
search_query: string      # Pattern, function name, or keyword to find
file_types: [string]      # File extensions to include (e.g., [".js", ".ts"])
exclude_dirs: [string]    # Directories to skip (e.g., ["node_modules", ".git"])
context_lines: number     # Lines of context around matches (default: 3)
max_results: number       # Limit results to prevent overwhelming output
```

## Task Flow

1. **Scope Definition**
   - Identify search boundaries (directories, file types)
   - Validate search pattern syntax

2. **Pattern Search**
   - Execute primary search across specified files
   - Collect matching locations with context

3. **Result Analysis**
   - Group related matches by file/function
   - Identify patterns and relationships
   - Highlight potential issues or improvements

4. **Summary Report**
   - List all matches with file:line references
   - Categorize findings (definitions, usages, tests)
   - Provide actionable recommendations

## Output Format

```markdown
## Search Results: {search_query}

### Summary
- **Total matches**: {count}
- **Files affected**: {file_count}
- **Search scope**: {directories}

### Findings by Category

#### Definitions
- `{file_path}:{line}` - {brief_description}

#### Usages
- `{file_path}:{line}` - {context}

#### Tests
- `{file_path}:{line}` - {test_description}

### Recommendations
- {actionable_suggestion}
```

## Error Handling

- **No matches found**: Suggest alternative search terms or broader scope
- **Too many results**: Recommend narrowing search with additional filters
- **Permission denied**: List inaccessible paths and continue with available files
- **Invalid pattern**: Provide corrected syntax examples