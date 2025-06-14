# Tool Exploration

Systematic tool/technology exploration producing validated usage guides.

## Parameters
```yaml
tool_name: string              # Tool to explore
version: string               # Version (default: latest)
documentation_sources: [string]  # Official docs URLs
exploration_scope: string     # basic/advanced/comprehensive
validation_depth: string      # surface/thorough/production
```

## Task Sequence

### 1. Documentation Discovery
- Search official docs, tutorials, guides
- Cache documentation locally if possible
- Identify key concepts, prerequisites, usage patterns
- Note documentation gaps

### 2. Environment Setup
- Verify prerequisites and dependencies
- Install using recommended method
- Validate installation with version/status commands
- Document workarounds required

**Human approval required for system modifications**

### 3. Basic Validation
- Execute simplest documented examples
- Validate outputs match documentation
- Test error conditions and edge cases
- Document actual vs expected behavior

**No placeholders - request guidance on failures**

### 4. Feature Exploration
For each major feature:
- Read relevant documentation
- Create minimal test case
- Execute and validate results
- Document findings and deviations
- Note limitations/workarounds

**Stop on failures, request human guidance**

### 5. Integration Testing
- Test practical workflows combining features
- Validate performance characteristics
- Identify production concerns

### 6. Guide Generation
Dense format output:
```
Tool: {tool_name} v{version}
Install: {installation_steps}
Quick: {minimal_example}

Features:
- {feature}: {command} → {result} | {config_notes}

Advanced:
- {complex_scenario}: {commands} | {performance_notes}

Issues:
- {limitation}: {workaround}
- {error}: {solution}
```

## Decision Logic
- Incomplete docs → prioritize hands-on discovery
- Extensive setup → request human confirmation
- Critical failure → stop, request guidance, never use placeholders
- Steep learning curve → focus on essentials first

## Quality Gates
- Documentation reviewed, installation verified
- Core examples work as documented
- Each feature validated with working examples
- All guide examples executed and verified

## Failure Handling
- Installation failures → request assistance, document workarounds
- Feature failures → stop, seek guidance, no placeholders
- Integration issues → document clearly, provide alternatives

## Human Interaction
**Required approvals**: system modifications, proceeding after failures
**Escalation triggers**: installation failures, non-working core functionality, security concerns

## Success Criteria
- All guide examples verified working
- No placeholders in deliverables
- Clear limitation documentation
- Reproducible by other agents