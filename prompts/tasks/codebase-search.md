# Codebase Search

Search and analyze code patterns, functions, implementations.

## Parameters
```yaml
search_query: string      # Pattern/keyword to find
file_types: [string]      # Extensions to include [".js", ".ts"]
exclude_dirs: [string]    # Skip directories ["node_modules", ".git"]  
context_lines: number     # Context around matches (default: 3)
max_results: number       # Result limit
```

## Execution
1. Validate pattern syntax
2. Execute search with scope filters
3. Group matches by file/function
4. Categorize findings

## Output Format
```
Query: {search_query}
Matches: {count} in {file_count} files
Scope: {directories}

Definitions:
{file_path}:{line} - {description}

Usages:  
{file_path}:{line} - {context}

Tests:
{file_path}:{line} - {test_description}

Recommendations:
{actionable_suggestions}
```

## Error Handling
- No matches: suggest broader scope/alternative terms
- Too many results: recommend filters  
- Permission denied: list inaccessible paths, continue
- Invalid pattern: provide corrected syntax