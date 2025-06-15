---
name: Command Request
about: Request a new CEI command or enhancement
title: '[COMMAND] '
labels: ['enhancement', 'command-request']
assignees: ''
---

## Command Overview

**Command Name**: `/command-name`
**Category**: [core/evaluation/documentation/analysis]
**Priority**: [high/medium/low]

## Problem Statement

Describe what problem this command would solve or what analysis it would provide.

## Proposed Functionality

### Input
- **Arguments**: Describe expected parameters
- **Format**: How should arguments be passed?

### Expected Output
- **Format**: [markdown/json/memory/checklist]
- **Structure**: Describe the expected output structure
- **Workspace**: What files/directories should be created?

### Use Cases
1. **Primary Use Case**: 
2. **Secondary Use Cases**:

## Technical Requirements

### Environment Support
- [ ] WSL2
- [ ] Linux
- [ ] macOS
- [ ] Windows (native)

### Dependencies
- **Required Tools**: List any tools that must be available
- **Optional Tools**: List tools that enhance functionality
- **System Requirements**: Any specific system requirements

### Performance Considerations
- **Expected Runtime**: How long should this command take?
- **Resource Usage**: Memory, disk, network requirements
- **Scalability**: How should it handle large environments/codebases?

## Design Considerations

### XML Structure
Provide proposed XML tag structure for structured output:

```xml
<command_output>
  <summary>Brief description</summary>
  <!-- Additional structure -->
</command_output>
```

### Error Handling
- **Common Failures**: What might go wrong?
- **Graceful Degradation**: How should it handle missing tools/permissions?
- **Recovery**: What should users do when it fails?

### Integration
- **Related Commands**: How does this relate to existing commands?
- **Composability**: Can this be combined with other commands?
- **Memory Integration**: Should this update CLAUDE.md profiles?

## Additional Context

Add any other context, examples, or references that would help implement this command.

## Implementation Notes

- [ ] Command follows CEI design principles
- [ ] Includes comprehensive error handling  
- [ ] Generates workspace-isolated output
- [ ] Supports multiple output formats
- [ ] Includes verification steps
- [ ] Documentation and examples provided