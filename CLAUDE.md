# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

For comprehensive Claude Code documentation, see:
- **[Claude Code Overview](https://docs.anthropic.com/en/docs/claude-code/overview)** - Core concepts and capabilities
- **[CLI Usage Guide](https://docs.anthropic.com/en/docs/claude-code/cli-usage)** - Commands, flags, and slash commands
- **[Security Model](https://docs.anthropic.com/en/docs/claude-code/security)** - Permissions and tool safety

## Project Architecture

This is a **Claude Code Command Pack** - a collection of production-tested slash commands for systematic workflows. The project has dual architecture:

```
Slash Commands (Primary) → Legacy Prompts (Reference)
```

- **Slash commands** (`src/commands/`): Ready-to-use Claude Code commands with `$ARGUMENTS` support
- **Legacy prompts**: Original templates converted to commands, preserved in git history
- **Installation system** (`INSTALL.md`): Global deployment to `~/.claude/commands/`
- **Examples** (`examples/`): Reference implementations and expected outputs

## Key Components

### Command System
- `src/commands/scan-env.md` - Environment discovery and reporting
- `src/commands/doc-workflow.md` - Tool workflow documentation with workspace isolation
- `src/commands/search-code.md` - Code pattern analysis and categorization
- All commands use `$ARGUMENTS` for parameter passing

### Command Architecture
- **Workspace isolation**: Commands create `workspace/` subdirectories for generated files
- **Verified execution**: All commands must be tested, no placeholders allowed
- **Dual cleanup**: Separate workspace cleanup from service/resource cleanup
- **Composable design**: Commands can be combined for complex workflows

## Development Patterns

### Command Design Principles
1. **Direct Execution**: Commands execute immediately with `$ARGUMENTS`
2. **Workspace Isolation**: All generated files go into dedicated workspace directories
3. **Verified Steps**: No placeholders - all commands must be tested and verified
4. **Dual Cleanup**: Separate workspace cleanup from service/resource cleanup

### Command Structure Conventions
- All commands are Markdown files in `src/commands/` directory
- Each command includes: Objective, Execution steps, Output format, Error handling
- Use `$ARGUMENTS` for parameter passing instead of YAML blocks
- Workspace pattern: `workspace/{tool}-{workflow}-{timestamp}`

## Important Notes

### WSL2 Performance Considerations
- Heavy I/O on `/mnt/c` is slower due to 9P protocol - prefer ext4 home directory for performance-critical operations
- Git operations fail when working directory is a symlink to `/mnt/c` - use real paths

### Command Pack Behavior
- **Workspace isolation** - always create dedicated directories for generated files
- **Verified execution** - test all commands, never use placeholders
- **Clean working directory** - keep user's project directory uncluttered
- **Rate limiting** - respect network limits and choose sane defaults
- **Systematic exploration** - follow established patterns for discovery and documentation

## Usage as Command Pack

This repository is designed to be installed as a Claude Code command pack:

1. **Installation**: Copy `src/commands/*` to `~/.claude/commands/`  
2. **Usage**: Available as `/command-name` in any Claude Code session
3. **Benefits**: Global availability, workspace isolation, parameterized execution
4. **No build system**: This is a collection of command templates, no compilation needed