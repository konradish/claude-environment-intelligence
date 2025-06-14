# Workflow Documentation

Document and validate specific tool workflows with verified steps.

## Parameters
```yaml
tool_name: string              # Tool name (wrangler, kubectl)
workflow_name: string          # Workflow description  
authentication_required: boolean
destructive_operations: boolean
dry_run_available: boolean
validation_method: string      # Success verification method
output_artifacts: [string]     # Expected files/resources
```

## Execution Flow

### 1. Pre-flight
- Verify tool version and auth status
- Check permissions/access
- Identify missing prerequisites

Example validation:
```bash
wrangler --version && wrangler whoami && wrangler pages project list
```

### 2. Workflow Mapping  
- Document exact commands for each step
- Note configuration requirements
- Identify decision points and verification steps

### 3. Execution
- Use dry-run mode if available, request approval if not
- Execute each step, capture output, verify success
- Stop on failures, request human guidance
- Never use placeholders

### 4. Guide Generation
Generate dense guide:
```
Tool: {tool_name} v{version}
Auth: {required_auth}
Workflow: {workflow_name}

Steps:
1. {command} → {expected_output} | verify: {success_indicator}
2. {command} → {expected_output} | verify: {success_indicator}

Cleanup: {rollback_commands}
Limitations: {discovered_issues}
```

## Decision Logic
- Auth required → verify before proceeding
- Destructive ops → require approval, use dry-run
- Step fails → stop, document, request intervention
- Never proceed with placeholders

## Error Handling
- Tool not ready: document requirements, escalate
- Step failure: document error, stop execution  
- Partial success: document working portions, mark failures
- Permission denied: document required permissions

## Human Interaction
Required approvals: destructive ops, external modifications
Escalation triggers: auth failures, step failures, access issues

## Output Requirements
- All commands verified through execution
- No placeholders or unverified steps
- Reproducible by other agents
- Dense, token-efficient format