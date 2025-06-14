# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Architecture

This is an **LLM Agent Prompt Pack** - a collection of production-tested prompts for autonomous AI agents. The project uses a layered architecture:

```
Environment → Tasks → Guides → Agent Execution
```

- **Environment prompts** (`prompts/env/`): Declare system capabilities, boundaries, and constraints
- **Task prompts** (`prompts/tasks/`): Atomic, reusable operations for specific actions
- **Guide prompts** (`prompts/guides/`): Multi-step workflows combining tasks with decision logic
- **Examples** (`examples/`): Reference implementations and expected outputs

## Key Components

### Environment Discovery
- `prompts/env/env-probe.md` - Core system prompt for environment exploration
- Guides agents through systematic discovery of OS, tools, mounts, and performance characteristics
- Designed for WSL2/Linux environments with Windows mount considerations

### Workflow Structure
- **Task prompts**: Single-responsibility, parameterized, idempotent operations
- **Guide prompts**: End-to-end workflows with quality gates and rollback procedures
- **Composable design**: Tasks combine into workflows, workflows reference other workflows

## Development Patterns

### Prompt Design Principles
1. **Declarative Configuration**: Prompts declare "what" not "how"
2. **Layered Abstraction**: Environment → Tasks → Guides → Execution
3. **Composability**: All prompts use shared vocabulary and can be combined
4. **Observability**: Clear success/failure criteria and structured outputs

### File Structure Conventions
- All prompts are Markdown files with YAML parameter blocks
- Each prompt includes: Objective, Prerequisites, Parameters, Output Format, Error Handling
- Workflows specify Task Sequence, Decision Points, Quality Gates, Rollback Procedures

## Important Notes

### WSL2 Performance Considerations
- Heavy I/O on `/mnt/c` is slower due to 9P protocol - prefer ext4 home directory for performance-critical operations
- Git operations fail when working directory is a symlink to `/mnt/c` - use real paths

### Agent Behavior
- **Read-only by default** - never mutate files unless explicitly instructed
- **Rate limiting** - respect network limits and choose sane defaults
- **Systematic exploration** - follow the 5-stage flow: OS/kernel → Mounts → Tools → Services → Performance

This repository contains no build scripts, package managers, or traditional development commands as it's a collection of prompt templates and documentation.