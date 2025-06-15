# Installation Guide

Install the LLM Agent Command Pack to use as global Claude Code slash commands.

**New to Claude Code?** See the [official documentation](https://docs.anthropic.com/en/docs/claude-code) for setup and usage basics.

## Quick Install

```bash
# Create commands directory if it doesn't exist
mkdir -p ~/.claude/commands

# Copy all commands from this repo
cp /path/to/llm_environment_exploration/src/commands/* ~/.claude/commands/

# Or clone and link (for easy updates)
git clone https://github.com/your-repo/llm_environment_exploration.git ~/.claude/prompt-packs/llm-env
ln -s ~/.claude/prompt-packs/llm-env/src/commands/* ~/.claude/commands/
```

## Available Commands

Once installed, these commands are available in any Claude Code session:

### Environment Discovery
- `/scan-env` - Discover system capabilities and create env_report.md

### Workflow Documentation  
- `/doc-workflow <tool> <workflow>` - Document and test tool workflows
  - Example: `/doc-workflow wrangler proxy-deploy`
  - Creates isolated workspace, documents steps, provides cleanup

### Code Analysis
- `/search-code <pattern>` - Search and analyze code patterns
  - Example: `/search-code getUserData`
  - Finds definitions, usages, tests with context

## Usage

1. Start Claude Code in any project directory
2. Type `/` to see available commands
3. Use `/command-name arguments` to execute
4. Commands handle workspace isolation and cleanup automatically

## Benefits

- **Global availability** - Works in any project
- **No file clutter** - Clean execution without copying prompts
- **Parameterized** - Dynamic arguments via `$ARGUMENTS`
- **Isolated workspaces** - Generated files don't interfere with your project
- **Composable** - Commands can be combined for complex workflows

## Updates

To update commands:
```bash
cd ~/.claude/prompt-packs/llm-env
git pull
# Commands are automatically updated via symlinks
```