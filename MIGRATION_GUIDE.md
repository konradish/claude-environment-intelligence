# CEI v1.0 → v2.0 Migration Guide

**Document Version**: 1.0
**Last Updated**: 2025-11-08

---

## Overview

This guide walks you through migrating from CEI v1.0 (simple command pack) to CEI v2.0 (comprehensive development intelligence platform).

**Migration Time**: ~30 minutes
**Difficulty**: Medium
**Backward Compatibility**: Yes (all v1.0 commands remain functional)

---

## What's Changing

### Architecture Evolution

```
v1.0: Flat Command Structure
~/.claude/commands/
├── scan-env.md
├── doc-workflow.md
└── search-code.md

    ↓ MIGRATES TO ↓

v2.0: Layered Knowledge Platform
~/.claude/cei/
├── src/
│   ├── commands/          # Layer 1: Direct execution
│   ├── skills/            # Layer 2: Autonomous management
│   └── .claude/           # Layer 3: Knowledge modules
├── examples/
├── docs/
└── CLAUDE.md              # Smart context entry
```

### Key Changes

| Feature | v1.0 | v2.0 |
|---------|------|------|
| **Commands** | Monolithic | Modular with knowledge refs |
| **Knowledge** | Inline | Separate `.claude/` modules |
| **Execution** | Single context | Multi-agent delegation |
| **Methodology** | Ad-hoc | FOCUS + HTK frameworks |
| **Token Usage** | ~3000 tokens | ~900 tokens (70% reduction) |
| **Autonomy** | Manual only | Skills + slash commands |

---

## Migration Paths

### Path A: In-Place Upgrade (Recommended)

**Best for**: Existing users who want to preserve workflows

**Steps**:

1. **Backup Current Installation**
   ```bash
   # Backup commands
   cp -r ~/.claude/commands ~/.claude/commands.v1-backup

   # Backup any custom modifications
   tar -czf ~/cei-v1-backup.tar.gz ~/.claude/commands
   ```

2. **Update Repository**
   ```bash
   cd ~/.claude/cei
   git fetch origin
   git checkout main
   git pull origin main
   ```

3. **Run Migration Script**
   ```bash
   # Interactive migration with safety checks
   ./scripts/migrate-v1-to-v2.sh

   # Or automated migration (advanced)
   ./scripts/migrate-v1-to-v2.sh --auto
   ```

4. **Verify Installation**
   ```bash
   # Check command availability
   claude --list-commands | grep cei

   # Test basic command
   /scan-env --version
   # Should output: CEI v2.0
   ```

5. **Optional: Install New Skills**
   ```bash
   # Install autonomous skills
   ./scripts/install-skills.sh

   # Verify skills are loaded
   # Start new Claude session and mention "environment analysis"
   # Claude should autonomously load environment-intelligence skill
   ```

**Migration Time**: ~10 minutes

---

### Path B: Fresh Install (Clean Slate)

**Best for**: New users or those wanting a fresh start

**Steps**:

1. **Remove Old Installation**
   ```bash
   # Optional: Backup first
   tar -czf ~/cei-v1-backup.tar.gz ~/.claude/cei

   # Remove old version
   rm -rf ~/.claude/cei
   rm -rf ~/.claude/commands/scan-env.md
   rm -rf ~/.claude/commands/doc-workflow.md
   rm -rf ~/.claude/commands/search-code.md
   ```

2. **Clone v2.0**
   ```bash
   git clone https://github.com/konradish/claude-environment-intelligence ~/.claude/cei
   ```

3. **Run Installation Script**
   ```bash
   cd ~/.claude/cei
   ./scripts/install.sh
   ```

4. **Verify Installation**
   ```bash
   # Test command availability
   /scan-env --help

   # Test skill availability
   # Start Claude and say: "Analyze my environment"
   # Should trigger environment-intelligence skill
   ```

**Migration Time**: ~5 minutes

---

### Path C: Side-by-Side (Testing)

**Best for**: Users who want to test v2.0 before full migration

**Steps**:

1. **Keep v1.0 Intact**
   ```bash
   # Don't remove anything
   ```

2. **Install v2.0 in Different Location**
   ```bash
   git clone https://github.com/konradish/claude-environment-intelligence ~/.claude/cei-v2
   ```

3. **Create Namespaced Commands**
   ```bash
   cd ~/.claude/cei-v2
   ./scripts/install.sh --prefix=cei2

   # This creates:
   # /cei2-scan-env
   # /cei2-evaluate-tool
   # etc.
   ```

4. **Test Both Versions**
   ```bash
   # v1.0 commands
   /scan-env

   # v2.0 commands
   /cei2-scan-env
   ```

5. **Choose Winner & Cleanup**
   ```bash
   # If v2.0 works well, remove v1.0
   ./scripts/migrate-v1-to-v2.sh --cleanup-v1

   # If sticking with v1.0, remove v2.0
   rm -rf ~/.claude/cei-v2
   ```

**Migration Time**: ~15 minutes + testing time

---

## Feature Migration

### 1. Commands

#### `/scan-env`

**v1.0 Usage**:
```bash
/scan-env
```

**v2.0 Usage** (backward compatible):
```bash
# Basic usage (same as v1.0)
/scan-env

# New: FOCUS mode
/scan-env --mode=focus

# New: HTK mode (systematic testing)
/scan-env --mode=htk

# New: With specific modules
/scan-env --load-modules=wsl2-specifics,docker-patterns

# New: Generate memory profile
/scan-env --output-format=memory > ~/.claude/CLAUDE.md
```

**Migration Notes**:
- Old syntax still works
- New flags are optional
- Output format unchanged unless specified

---

#### `/doc-workflow`

**v1.0 Usage**:
```bash
/doc-workflow docker
```

**v2.0 Usage**:
```bash
# Basic usage (same as v1.0)
/doc-workflow docker

# New: Interactive mode with validation
/doc-workflow docker --interactive

# New: With HTK methodology
/doc-workflow docker --mode=htk

# New: Generate template for reuse
/doc-workflow docker --output=template > ~/.claude/templates/docker-workflow.md
```

---

#### `/search-code`

**v1.0 Usage**:
```bash
/search-code "API endpoints"
```

**v2.0 Usage**:
```bash
# Basic usage (same as v1.0)
/search-code "API endpoints"

# New: Pattern analysis with categorization
/search-code "API endpoints" --analyze-patterns

# New: Delegate to subagent for deep analysis
/search-code "API endpoints" --delegate=pattern-analyzer

# New: Export to knowledge module
/search-code "API endpoints" --export-module=api-patterns.md
```

---

### 2. Knowledge Modules

**v1.0**: Knowledge embedded in commands

**v2.0**: Separate knowledge modules

**Migration**:

1. **Review Generated Modules**
   ```bash
   # After migration, review what was extracted
   ls -la ~/.claude/cei/src/.claude/guides/
   ```

2. **Customize for Your Environment**
   ```bash
   # Edit environment-specific modules
   nano ~/.claude/cei/src/.claude/environments/wsl2-ubuntu.md

   # Add project-specific patterns
   nano ~/.claude/cei/src/.claude/frameworks/your-stack.md
   ```

3. **Reference in CLAUDE.md**
   ```bash
   # Copy template
   cp ~/.claude/cei/src/.claude/templates/CLAUDE.md.template ~/your-project/CLAUDE.md

   # Customize for your project
   nano ~/your-project/CLAUDE.md
   ```

---

### 3. Skills (New in v2.0)

**What are Skills?**: Autonomous capabilities that Claude loads automatically when relevant.

**Available Skills**:
- `environment-intelligence` - Autonomous environment analysis
- `tool-evaluator` - Comprehensive tool assessment
- `workflow-documenter` - Interactive workflow capture

**How to Use**:

1. **Implicit Activation** (Recommended)
   ```
   You: "I need to understand my development environment"
   Claude: [Automatically loads environment-intelligence skill]
   Claude: "I'll analyze your environment systematically using FOCUS methodology..."
   ```

2. **Explicit Activation**
   ```
   You: "/load-skill environment-intelligence"
   You: "Now analyze my environment"
   ```

3. **Check What Skills Are Available**
   ```bash
   ls -la ~/.claude/cei/src/skills/
   ```

---

### 4. Subagents (New in v2.0)

**What are Subagents?**: Specialized agents that work in parallel on focused tasks.

**Available Subagents**:
- `security-analyzer` - Security posture assessment
- `performance-profiler` - Performance benchmarking
- `integration-tester` - Tool compatibility testing
- `documentation-generator` - Automated documentation

**How to Use**:

1. **Automatic Delegation** (via Skills)
   ```
   You: "Analyze my environment comprehensively"
   Claude: [Loads environment-intelligence skill]
   Claude: [Delegates to security-analyzer, performance-profiler, integration-tester in parallel]
   Claude: [Synthesizes results]
   ```

2. **Manual Delegation** (Advanced)
   ```bash
   /delegate security-analyzer "Check for permission issues"
   /delegate performance-profiler "Benchmark I/O performance"
   ```

---

## Troubleshooting

### Issue: Commands Not Found After Migration

**Symptoms**:
```bash
/scan-env
# Error: Command not found
```

**Solution**:
```bash
# Reload Claude configuration
claude --reload-config

# Or restart Claude session
exit
claude
```

---

### Issue: Skills Not Loading

**Symptoms**:
Claude doesn't automatically load skills when you mention relevant topics.

**Solution**:
```bash
# Verify skills are installed
ls -la ~/.claude/cei/src/skills/

# Check Claude config
cat ~/.claude/config.json | grep skills

# Reinstall skills
cd ~/.claude/cei
./scripts/install-skills.sh --force
```

---

### Issue: Module Loading Errors

**Symptoms**:
```
Error: Cannot load module @.claude/guides/environment-discovery.md
```

**Solution**:
```bash
# Verify module exists
ls -la ~/.claude/cei/src/.claude/guides/environment-discovery.md

# Check CLAUDE.md references
grep -r "@.claude/guides" ~/your-project/CLAUDE.md

# Fix path references
# Ensure paths are relative to project root
```

---

### Issue: Token Usage Higher Than Expected

**Symptoms**:
Commands seem to use more tokens than promised.

**Solution**:
```bash
# Use modular loading explicitly
/scan-env --load-modules=wsl2-specifics
# Instead of loading all modules

# Enable token usage reporting
export CLAUDE_DEBUG_TOKENS=1

# Review what modules are being loaded
# Check CLAUDE.md for unnecessary module references
```

---

## Rollback Procedure

If v2.0 doesn't work for you:

1. **Restore v1.0 Commands**
   ```bash
   # From backup
   cp -r ~/.claude/commands.v1-backup/* ~/.claude/commands/

   # Or from tarball
   tar -xzf ~/cei-v1-backup.tar.gz -C ~/
   ```

2. **Remove v2.0**
   ```bash
   rm -rf ~/.claude/cei
   ```

3. **Verify v1.0 Works**
   ```bash
   /scan-env
   # Should run v1.0 command
   ```

---

## FAQ

### Q: Will my existing workflows break?

**A**: No. All v1.0 commands remain functional in v2.0. New features are additive.

### Q: Do I need to learn FOCUS/HTK methodologies?

**A**: No. They're optional enhancements. You can use commands the same way as v1.0.

### Q: How much space does v2.0 require?

**A**: ~10MB (vs ~2MB for v1.0) due to additional knowledge modules and documentation.

### Q: Can I mix v1.0 and v2.0?

**A**: Yes, using Path C (Side-by-Side). Use different prefixes.

### Q: How do I update my existing CLAUDE.md files?

**A**: Run `/create-memory-profile` to generate v2.0-compatible CLAUDE.md, then merge manually.

### Q: Are skills required?

**A**: No. Skills are optional. You can use v2.0 with just slash commands.

### Q: How do I customize knowledge modules?

**A**: Edit files in `~/.claude/cei/src/.claude/`. Changes apply immediately.

### Q: Can I contribute new modules?

**A**: Yes! See `docs/guides/knowledge-authoring.md` for guidelines.

---

## Next Steps After Migration

1. **Explore New Commands**
   ```bash
   /scan-env --help
   /evaluate-tool --help
   /focus --help
   /htk-plan --help
   ```

2. **Try Skills**
   ```
   Start a new session and say:
   "Help me analyze my development environment systematically"
   ```

3. **Customize Knowledge Modules**
   ```bash
   # Add your environment-specific knowledge
   nano ~/.claude/cei/src/.claude/environments/my-setup.md
   ```

4. **Create Project CLAUDE.md**
   ```bash
   cd ~/your-project
   /create-memory-profile
   # Review and customize the generated CLAUDE.md
   ```

5. **Read Documentation**
   ```bash
   # Architecture overview
   cat ~/.claude/cei/docs/architecture/compositional-hierarchy.md

   # FOCUS methodology
   cat ~/.claude/cei/docs/methodologies/focus-framework.md

   # Best practices
   cat ~/.claude/cei/docs/best-practices/token-efficiency.md
   ```

---

## Support

### Getting Help

- **Documentation**: `~/.claude/cei/docs/`
- **Examples**: `~/.claude/cei/examples/`
- **Issues**: https://github.com/konradish/claude-environment-intelligence/issues

### Reporting Migration Issues

When reporting migration problems, include:

1. Migration path used (A, B, or C)
2. CEI version before migration (`/scan-env --version`)
3. Error messages
4. Output of `claude --debug`

---

## Conclusion

Migration to CEI v2.0 is designed to be:
- **Backward compatible** - Your existing workflows continue working
- **Gradual** - Adopt new features at your own pace
- **Reversible** - Easy rollback if needed
- **Beneficial** - 70% token reduction, autonomous skills, systematic methodologies

Take your time exploring the new features. You don't need to use everything on day one!

---

**Migration Support**: For questions, open an issue or start a discussion on GitHub.
