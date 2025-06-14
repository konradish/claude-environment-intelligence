# Claude Code Command Pack

A curated set of production-tested slash commands for Claude Code that provide systematic workflows for environment discovery, tool validation, and code analysis.

## ⚡ Slash Command Architecture

This repository is designed as a **Claude Code Command Pack** - install once, use everywhere:

• **Global availability**: Commands work in any project directory
• **Zero clutter**: No copying files or cluttering working directories  
• **Parameterized**: Dynamic arguments via `$ARGUMENTS` keyword
• **Isolated workspaces**: Generated files don't interfere with your project
• **Composable**: Commands combine for complex workflows

## 🚀 Quick Install

```bash
# Create commands directory
mkdir -p ~/.claude/commands

# Copy commands (choose one method)
cp commands/* ~/.claude/commands/

# OR clone and link for easy updates
git clone <this-repo> ~/.claude/prompt-packs/llm-env
ln -s ~/.claude/prompt-packs/llm-env/commands/* ~/.claude/commands/
```

**Usage**: Start Claude Code anywhere, type `/` to see available commands.

## 📋 Available Commands

### Environment Discovery
- **`/env-probe`** - Discover system capabilities and create detailed env_report.md
  - Analyzes OS, mounts, tools, network, and performance
  - Identifies WSL2/Linux specifics and limitations

### Workflow Documentation
- **`/workflow-doc <tool> <workflow>`** - Document and test tool workflows with verification
  - Example: `/workflow-doc wrangler proxy-deploy`
  - Creates isolated workspace, documents steps, provides cleanup
  - Never uses placeholders - all commands are verified

### Code Analysis  
- **`/search-code <pattern>`** - Search and analyze code patterns across codebase
  - Example: `/search-code getUserData` 
  - Finds definitions, usages, tests with context
  - Intelligent scope filtering and categorization

## 🎯 Command Benefits

- **Workspace Isolation**: All generated files go into `workspace/` subdirectories
- **Clean Execution**: No file clutter in your working directory
- **Verified Steps**: Commands are tested, not theoretical
- **Comprehensive Cleanup**: Both workspace and service cleanup instructions
- **Multi-experiment Friendly**: Run multiple workflows without interference

## 📁 Repository Structure

```
commands/           # Claude Code slash commands (main interface)
  env-probe.md     # Environment discovery command
  workflow-doc.md  # Tool workflow documentation
  search-code.md   # Code pattern analysis
  
prompts/            # Original prompt templates (reference)
  env/             # Environment probes & setup prompts
  tasks/           # Reusable action prompts  
  guides/          # Higher-level agent workflows
  
examples/           # Reference implementations
docs/              # Architecture documentation
INSTALL.md         # Installation instructions
```

## 🔄 Legacy Prompts

The `prompts/` directory contains the original prompt templates that were converted to slash commands. These remain for:
- **Reference**: Understanding the design principles
- **Customization**: Creating your own command variations
- **Documentation**: Explaining the layered architecture approach

**Recommendation**: Use the `commands/` directory for day-to-day work.

## Contributing

PRs welcome, follow Conventional Commits.

## License

[MIT](LICENSE)