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
workspace_isolation: boolean   # Create isolated workspace (default: true)
workspace_name: string         # Custom workspace name (optional)
```

## Execution Flow

### 1. Pre-flight
- Verify tool version and auth status
- Check permissions/access
- Identify missing prerequisites
- **Setup workspace isolation** (if enabled)

Example validation:
```bash
wrangler --version && wrangler whoami && wrangler pages project list
```

**Workspace Setup:**
- Create `workspace/{tool}-{timestamp}` or custom workspace directory
- Change to workspace directory for all file operations
- Document workspace location for cleanup

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
Workspace: {workspace_path} (if isolated)

Steps:
1. {command} → {expected_output} | verify: {success_indicator}
2. {command} → {expected_output} | verify: {success_indicator}

Workspace Cleanup: rm -rf {workspace_path}
Service Cleanup: {rollback_commands}
Limitations: {discovered_issues}
```

## Decision Logic
- Auth required → verify before proceeding
- Destructive ops → require approval, use dry-run
- Workspace isolation → create dedicated directory, document path
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
- Clear workspace isolation and cleanup instructions
- Separate service/resource cleanup from workspace cleanup

## Workspace Management
**Default behavior:** Create `workspace/{tool}-{workflow}-{timestamp}` directory
**Benefits:** 
- Clean working directory
- Multiple workflow experiments can coexist
- Easy cleanup without affecting other work
- Clear audit trail of what was generated vs. pre-existing

**Usage Pattern:**
1. Agent creates workspace directory
2. All generated files go into workspace
3. Commands execute from workspace when needed
4. Guide includes both workspace and service cleanup steps