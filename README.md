# Claude Environment Intelligence (CEI)

**Intelligent development environment discovery and analysis for Claude Code**

CEI transforms the tedious process of environment discovery into systematic intelligence gathering. Instead of manually checking system capabilities, tool versions, and integration points, CEI provides production-tested slash commands that analyze, document, and optimize your development environment.

## 🎯 What CEI Solves

- **Environment Blind Spots**: Automatically discover hidden limitations (WSL2 quirks, permission issues, tool conflicts)
- **Setup Inconsistencies**: Generate environment profiles that work consistently across team members
- **Tool Integration Failures**: Verify tool workflows before they break your development flow
- **Documentation Drift**: Keep environment documentation synchronized with actual system state

## ⚡ Core Intelligence Capabilities

### 🔍 Environment Discovery
- **System Analysis**: OS, architecture, performance baselines, security posture
- **Tool Detection**: Version analysis, compatibility checking, integration testing
- **Limitation Mapping**: WSL2 specifics, permission boundaries, network constraints
- **Performance Profiling**: I/O benchmarks, network latency, compute capabilities

### 📊 Workflow Intelligence
- **Interactive Documentation**: Real-time workflow capture with error handling
- **Integration Testing**: Cross-tool compatibility and version conflict detection
- **Template Generation**: Environment-specific workflow templates
- **Memory Integration**: Seamless integration with Claude Code's global CLAUDE.md for persistent environment awareness

### 🛠 Tool Evaluation
- **Comprehensive Assessment**: Security, performance, integration analysis
- **Benchmarking**: Performance baselines and optimization recommendations
- **Compatibility Matrix**: Multi-tool integration analysis
- **Troubleshooting**: Systematic debugging with resolution guidance

## 🚀 Quick Start

### Installation
```bash
# Create commands directory
mkdir -p ~/.claude/commands

# Install CEI commands
cp src/commands/* ~/.claude/commands/

# OR clone for easy updates
git clone https://github.com/username/claude-environment-intelligence ~/.claude/cei
ln -s ~/.claude/cei/src/commands/* ~/.claude/commands/
```

### Basic Usage
```bash
# 1. Discover your environment
/scan-env

# 2. Integrate findings with Claude Code's memory system
# Claude Code will help you merge scan results into ~/.claude/CLAUDE.md
# for persistent environment awareness across all sessions
```

### Complete Intelligence Workflow
```bash
# Step 1: Initial discovery
/scan-env

# Step 2: Deep analysis (optional)
/scan-env-deep

# Step 3: Integration with global CLAUDE.md
# Use Claude Code to help integrate findings:
# 1. Review generated reports in workspace/
# 2. Ask Claude to merge relevant findings into ~/.claude/CLAUDE.md  
# 3. Test Claude's improved environment awareness

# Additional commands
/env-troubleshoot "git operations fail in WSL2"
/evaluate-tool docker
```

## 📋 Command Reference

### Core Discovery Commands
- **`/scan-env`** - Systematic environment discovery with structured output
- **`/scan-env-deep`** - Comprehensive analysis including security and performance
- **`/env-troubleshoot <issue>`** - Guided troubleshooting for common problems
- **`/env-compare <profile1> <profile2>`** - Environment comparison and migration planning

### Tool Intelligence Commands  
- **`/evaluate-tool <tool>`** - Complete tool assessment with benchmarks
- **`/benchmark-tool <tool> <workload>`** - Performance analysis and optimization
- **`/tool-compatibility <tool1> <tool2>`** - Cross-tool integration analysis

### Workflow Documentation Commands
- **`/doc-workflow-interactive <tool>`** - Real-time workflow capture
- **`/workflow-template <category>`** - Generate workflow templates
- **`/create-memory-profile`** - Generate CLAUDE.md environment profiles

### Advanced Analysis Commands
- **`/search-code-advanced <pattern>`** - Enhanced code pattern analysis
- **`/pattern-analysis <codebase>`** - Architectural pattern detection

## 🏗 Architecture

CEI follows a **workspace isolation** pattern that keeps your project directory clean while providing comprehensive analysis:

```
workspace/
├── scan-env-2024-01-15/          # Environment discovery results
├── tool-evaluation-2024-01-15/   # Tool analysis reports  
├── workflow-docs-2024-01-15/     # Generated documentation
└── memory-profiles-2024-01-15/   # CLAUDE.md profiles
```

### Key Design Principles
- **Parallel Execution**: Leverage Claude 4's multi-tool capabilities for speed
- **Structured Output**: XML-tagged responses for reliable parsing
- **Extended Thinking**: Deep analysis before action for better results
- **Memory Integration**: Seamless integration with Claude Code's global ~/.claude/CLAUDE.md
- **Verified Execution**: All commands tested, no placeholders
- **Human-AI Collaboration**: Claude Code assists with integrating scan findings into memory system

## 🧠 Memory Integration Workflow

CEI's key innovation is seamless integration with Claude Code's memory system:

### 1. Discovery Phase
```bash
# Run environment scan
/scan-env
# Results saved to workspace/scan-env-{timestamp}/
```

### 2. Integration Phase
```bash
# Ask Claude Code to help integrate findings
# Example conversation:
# "Please review the scan results in workspace/ and help me integrate 
#  the key environment details into my ~/.claude/CLAUDE.md file"
```

### 3. Verification Phase
```bash
# Test Claude's improved environment awareness
# Start a new Claude Code session and verify it knows about:
# - Your WSL2 setup and limitations
# - Available tools and versions  
# - Performance characteristics
# - Security constraints
```

### Benefits of Memory Integration
- **Persistent Awareness**: Claude remembers your environment across all sessions
- **Reduced Repetition**: No need to re-explain environment details
- **Smarter Suggestions**: Context-aware recommendations based on your setup
- **Team Consistency**: Shared memory profiles ensure consistent behavior

## 📊 Output Formats

CEI supports multiple output formats for different use cases:

- **`--format=markdown`** - Human-readable documentation
- **`--format=json`** - Machine-parseable structured data  
- **`--format=memory`** - CLAUDE.md compatible profiles
- **`--format=checklist`** - Actionable task lists

## 🎯 Use Cases

### Development Team Onboarding
```bash
# Generate team environment profile
/scan-env --format=memory > team-environment-profile.md

# Integrate with personal Claude Code memory
# Ask Claude Code to help merge findings into ~/.claude/CLAUDE.md
# ensuring consistent environment awareness for all team members
```

### CI/CD Environment Validation
```bash
/scan-env-deep --format=json > ci-environment-report.json
/evaluate-tool docker --format=checklist > docker-validation.md
```

### Tool Migration Planning
```bash
/env-compare current-env.json target-env.json
/tool-compatibility webpack vite
```

### Performance Optimization
```bash
/benchmark-tool node build-process
/scan-env-deep --focus=performance
```

## 📁 Repository Structure

```
claude-environment-intelligence/
├── src/
│   ├── commands/
│   │   ├── core/                    # Essential discovery commands
│   │   ├── evaluation/              # Tool evaluation commands
│   │   ├── documentation/           # Workflow documentation
│   │   └── analysis/                # Advanced analysis
│   ├── templates/                   # CLAUDE.md and profile templates
│   └── schemas/                     # JSON schemas for outputs
├── examples/                        # Sample outputs and use cases
├── docs/                           # Architecture and best practices
└── tests/                          # Command validation tests
```

## 🤝 Contributing

CEI follows the [Claude Code Command Pack](https://docs.anthropic.com/en/docs/claude-code) architecture:

1. **Fork & Clone**: Standard GitHub workflow
2. **Command Development**: Add new commands to `src/commands/`
3. **Testing**: All commands must be verified in target environments
4. **Documentation**: Include examples and expected outputs
5. **Submit PR**: Follow conventional commits

### Command Development Guidelines
- Use XML tags for structured output
- Implement parallel execution where possible
- Include comprehensive error handling
- Generate workspace-isolated outputs
- Provide multiple output formats

## 📈 Roadmap

- **v1.0**: Core discovery and tool evaluation commands
- **v1.1**: Advanced analysis and comparison features
- **v1.2**: Interactive documentation and template generation
- **v1.3**: Performance optimization and security analysis
- **v2.0**: AI-powered environment optimization recommendations

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🔗 Links

- **[Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)**
- **[Best Practices Guide](docs/best-practices.md)**
- **[Command Reference](docs/command-reference.md)**
- **[Troubleshooting Guide](docs/troubleshooting.md)**