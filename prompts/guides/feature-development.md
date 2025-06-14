# Feature Development

End-to-end feature implementation workflow.

## Parameters
```yaml
feature_description: string    # Feature requirements
target_branch: string         # Base branch (main/master)
feature_branch: string        # New branch name
test_strategy: string         # Unit/integration/e2e
```

## Task Sequence
1. **Environment Analysis** → env-probe.md
2. **Codebase Discovery** → codebase-search.md  
3. **Implementation**:
   - Create feature branch
   - Implement core functionality
   - Add tests
   - Verify code quality
4. **Integration Testing**
5. **PR Preparation**

## Decision Logic
- Auth features → security review required
- API changes → backwards compatibility check
- User-facing → UI/UX review

## Quality Gates
- No build errors, all tests pass, linting clean
- Feature requirements met, edge cases handled
- No breaking changes, API contracts maintained

## Output
- Complete feature branch
- Test suite with coverage
- Pull request with description