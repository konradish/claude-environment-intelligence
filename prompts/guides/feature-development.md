# Feature Development Workflow

**Overview**: End-to-end workflow for implementing a new feature from requirements to deployment.

## Prerequisites

- Development environment properly configured
- Source control access (git with appropriate permissions)
- Testing framework available
- CI/CD pipeline configured

## Workflow Parameters

```yaml
feature_description: string    # Clear description of feature requirements
target_branch: string         # Branch to create feature branch from (usually main/master)
feature_branch: string        # Name for new feature branch
test_strategy: string         # Unit, integration, or end-to-end testing approach
```

## Task Sequence

### 1. Environment Analysis
**Task**: `env-probe.md`
- Verify development tools are available
- Confirm project structure and conventions
- Identify potential blockers

### 2. Codebase Discovery
**Task**: `codebase-search.md`
- Search for similar existing features
- Identify relevant files and patterns
- Understand current architecture

### 3. Feature Planning
**Decision Point**: Based on complexity and existing patterns
- **Simple**: Direct implementation
- **Complex**: Break into subtasks

### 4. Implementation
**Sequence**:
1. Create feature branch
2. Implement core functionality
3. Add comprehensive tests
4. Update documentation
5. Verify code quality (linting, type checking)

### 5. Integration Testing
**Quality Gates**:
- All tests pass
- No linting errors
- Type checking passes
- Manual testing completed

### 6. Code Review Preparation
**Tasks**:
- Generate comprehensive diff summary
- Document changes and rationale
- Prepare test evidence
- Create pull request

## Decision Logic

```
IF feature touches authentication THEN
  REQUIRE security review
ELSE IF feature affects API contract THEN
  REQUIRE backwards compatibility verification
ELSE IF feature is user-facing THEN
  REQUIRE UI/UX review
END IF
```

## Quality Gates

1. **Code Quality**
   - No compile/build errors
   - All tests passing
   - Linting rules satisfied
   - Type safety maintained

2. **Functional Quality**
   - Feature requirements met
   - Edge cases handled
   - Error handling implemented
   - Performance acceptable

3. **Integration Quality**
   - No breaking changes to existing features
   - Database migrations (if any) are reversible
   - API contracts maintained

## Rollback Procedures

1. **Pre-merge**: Simply abandon feature branch
2. **Post-merge**: Create revert commit with detailed explanation
3. **Production issues**: Coordinate with deployment pipeline for rollback

## Output Artifacts

- Feature branch with complete implementation
- Test suite with high coverage
- Documentation updates
- Pull request with detailed description
- Deployment notes (if applicable)