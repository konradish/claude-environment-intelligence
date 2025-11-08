# Environment Intelligence Skill

**Reference implementation** demonstrating the complete CDI skill pattern.

## What This Is

An autonomous skill that analyzes development environments using:
- **FOCUS framework** for problem decomposition
- **HTK methodology** for hypothesis validation
- **Modular knowledge** for token efficiency
- **Parallel execution** for speed

## Auto-Load Triggers

This skill automatically activates when users mention:
- "analyze my environment"
- "check my development setup"
- "what's my system configuration"
- "environment discovery"
- "is my setup correct"

No need to invoke commands manually - just describe what you need.

## Usage Examples

### Example 1: Quick Environment Check
```
You: "Analyze my development environment"

Claude: [Loads environment-intelligence skill]
Claude: "I'll perform a quick scan of your development environment..."

→ Detects WSL2 Ubuntu
→ Loads only WSL2 module (~120 tokens)
→ Checks OS, tools, versions
→ Tests git in symlink (HTK validation)
→ Generates report in 2 minutes
→ Offers to update CLAUDE.md
```

### Example 2: Comprehensive Analysis
```
You: "Deep analysis of my setup, setting up a new project"

Claude: [Loads environment-intelligence skill]
Claude: "I'll perform comprehensive analysis with security and performance checks..."

→ FOCUS: Chooses Option 2 (Comprehensive)
→ Delegates to security-analyzer + performance-profiler (parallel)
→ Runs 5 HTK validations
→ Synthesizes findings from all sources
→ Generates detailed report in 5 minutes
→ Creates CLAUDE.md suggestions
```

### Example 3: Cloud-Aware
```
You: "Check my environment including AWS resources"

Claude: [Loads environment-intelligence skill]
Claude: "I'll analyze local and cloud infrastructure..."

→ FOCUS: Chooses Option 3 (Cloud-aware)
→ Loads AWS MCP server
→ Parallel analysis: local + cloud
→ HTK validations include cloud connectivity
→ Unified report with recommendations
```

## How It Works

### 1. FOCUS (Problem Decomposition)
```
Understand intent → Generate 3 options → Choose best approach
```

**Options**:
- Option 1: Quick scan (2 min, ~250 tokens)
- Option 2: Comprehensive (5 min, ~500 tokens)
- Option 3: Cloud-aware (10 min, ~600 tokens)

### 2. Progressive Module Loading
```
Always: environment-discovery.md, focus-htk-methodology.md
On detection: wsl2-ubuntu.md OR macos-dev.md OR linux-native.md
On demand: troubleshooting.md, cloud-integration.md
```

**Token efficiency**: Load only what's needed (60-80% reduction).

### 3. Parallel Execution
```
Option 1: Direct execution (no delegation)
Option 2: security-analyzer + performance-profiler (parallel)
Option 3: Option 2 + MCP cloud queries (parallel)
```

### 4. HTK Validation
Every critical finding gets tested:
```markdown
Hypothesis → Test → Verify → Decision
```

Example:
- Hypothesis: Git fails in symlinks on WSL2
- Test: Create symlink, run git status
- Verify: Exit code 0 = pass, non-zero = fail
- Decision: Document limitation if fails

### 5. Memory Integration
Auto-generates CLAUDE.md additions:
```markdown
## Environment Profile
- OS: WSL2 Ubuntu 22.04
- Known Limitations: Git symlink issues

## Module Loading
- WSL2 tasks → @.claude/environments/wsl2-ubuntu.md
```

## Output Structure

All artifacts saved to isolated workspace:
```
workspace/env-intelligence-20251108-143052/
├── report.md              # Main findings (XML format)
├── htk-validations/       # Individual test results
├── subagent-outputs/      # Delegated analysis results
└── suggested-claude.md    # CLAUDE.md additions
```

## Token Efficiency

**Before (monolithic)**:
- Load all knowledge: ~3000 tokens
- No reuse across commands

**After (modular skill)**:
- Quick scan: ~250 tokens (92% reduction)
- Comprehensive: ~500 tokens (83% reduction)
- Cloud-aware: ~600 tokens (80% reduction)
- Knowledge reused across all analysis types

## Key Patterns Demonstrated

This skill serves as the **reference implementation** showing:

1. ✅ **FOCUS decomposition** - Systematic option generation
2. ✅ **Progressive loading** - Modules loaded based on detection
3. ✅ **HTK validation** - Test hypotheses, don't just assert
4. ✅ **Subagent delegation** - Parallel specialized execution
5. ✅ **MCP integration** - Cloud resource discovery
6. ✅ **Memory integration** - Auto-update CLAUDE.md
7. ✅ **Workspace isolation** - Clean project directory
8. ✅ **Error handling** - Graceful degradation
9. ✅ **Structured output** - XML for reliable parsing
10. ✅ **Actionable results** - Every finding has remediation

## When to Use This Pattern

**Use this pattern for skills that**:
- Analyze complex systems
- Benefit from specialized subagents
- Need token efficiency (large knowledge base)
- Require validation/testing (not just queries)
- Should auto-load based on context

**Don't use this pattern for**:
- Simple one-step operations (use slash command)
- Quick lookups (use direct tool call)
- Purely creative tasks (no validation needed)

## Related Files

- Skill definition: `SKILL.md`
- Knowledge modules: `src/.claude/guides/`, `src/.claude/environments/`
- Subagents: `src/.claude/agents/security-analyzer.md`, etc.
- MCP configs: `src/.claude/mcp/cloud-providers/`

## Development Notes

### Adding New Environment Support

1. Create module: `src/.claude/environments/your-env.md`
2. Update SKILL.md detection logic:
   ```markdown
   - Your-env detected → @.claude/environments/your-env.md
   ```

### Adding New Tool Framework

1. Create module: `src/.claude/frameworks/your-tool.md`
2. Update SKILL.md detection:
   ```markdown
   - Your-tool detected → @.claude/frameworks/your-tool.md
   ```

### Adding New HTK Validation

Add to Phase 3 in SKILL.md:
```markdown
# HTK: Your Hypothesis

**Hypothesis**: [Clear statement]
**Test**: [Exact steps]
**Verify**: [Metric + threshold]
**Decision**: [Pass/Fail actions]
```

## Testing

Test this skill with:
```bash
# WSL2 environment
"analyze my development environment"
→ Should detect WSL2, load wsl2-ubuntu.md, test git symlinks

# macOS environment
"check my setup"
→ Should detect macOS, load macos-dev.md, check homebrew

# Cloud-aware
"comprehensive check including AWS"
→ Should load MCP, query EC2/RDS/Lambda
```

## Token Budget

Target token usage by option:
- **Option 1 (Quick)**: 200-300 tokens
- **Option 2 (Comprehensive)**: 400-600 tokens
- **Option 3 (Cloud-aware)**: 500-700 tokens

Actual usage depends on detected environment and loaded modules.

## Success Criteria

- ✅ Auto-loads on relevant keywords
- ✅ Loads only needed modules (not everything)
- ✅ Performs 3+ HTK validations
- ✅ Generates actionable report
- ✅ Completes within time budget
- ✅ Stays under token budget
- ✅ Offers CLAUDE.md integration

## Contributing

To improve this skill:
1. Add new environment modules to `.claude/environments/`
2. Add new framework modules to `.claude/frameworks/`
3. Add new HTK validation patterns
4. Improve error handling
5. Optimize token usage
6. Add more cloud providers (MCP)

## License

Same as parent CDI repository (MIT).
