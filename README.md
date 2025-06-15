# Claude Code Command Pack

**What it solves:** Eliminates the tedious cycle of discovering system capabilities, validating tool workflows, and searching codebases by providing battle-tested slash commands that work consistently across environments.

**Why it matters:** Instead of copy-pasting prompts or reinventing discovery scripts, you get verified workflows that follow [Claude Code Best Practices](https://docs.anthropic.com/en/docs/claude-code) and integrate seamlessly with your development process.

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
cp src/commands/* ~/.claude/commands/

# OR clone and link for easy updates
git clone https://github.com/konradish/workflow-prompts ~/.claude/prompt-packs/workflow-prompts
ln -s ~/.claude/prompt-packs/workflow-prompts/src/commands/* ~/.claude/commands/
```

**Usage**: Start Claude Code anywhere, type `/` to see available commands.

## 📋 Available Commands

### Environment Discovery
- **`/scan-env`** - Discover system capabilities and create detailed env_report.md
  - Analyzes OS, mounts, tools, network, and performance
  - Identifies WSL2/Linux specifics and limitations

### Workflow Documentation
- **`/doc-workflow <tool> <workflow>`** - Document and test tool workflows with verification
  - Example: `/doc-workflow wrangler proxy-deploy`
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
src/commands/       # Claude Code slash commands (main interface)
examples/           # Reference implementations and expected outputs
docs/               # Architecture deep dives and design principles
INSTALL.md         # Installation instructions
```

**→ See [Architecture Documentation](docs/README.md) for detailed design principles and patterns.**

## 🔄 Legacy Prompts

The original prompt templates were converted to slash commands and are preserved in git history. For reference or customization:
- **Git history**: `git log --follow src/commands/` to see evolution
- **Design principles**: See [Architecture Documentation](docs/README.md)
- **Customization**: Fork and modify commands in `src/commands/`

**Recommendation**: Use the `src/commands/` directory for day-to-day work.

## Contributing

PRs welcome, follow Conventional Commits.

## License

[MIT](LICENSE)