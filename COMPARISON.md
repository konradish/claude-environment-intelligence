# CEI v1.0 vs v2.0 - Feature Comparison

**Quick Reference Guide**

---

## Architecture Comparison

| Aspect | v1.0 | v2.0 | Improvement |
|--------|------|------|-------------|
| **Structure** | Flat commands | 3-layer hierarchy | Better organization |
| **Knowledge** | Inline in commands | Modular `.claude/` | Reusability |
| **Execution** | Single context | Multi-agent | Parallel processing |
| **Token Usage** | ~3000 tokens | ~900 tokens | **70% reduction** |
| **Autonomy** | Manual only | Skills + commands | Autonomous operation |
| **Methodology** | Ad-hoc | FOCUS + HTK | Systematic approach |

---

## Command Comparison

### `/scan-env`

| Feature | v1.0 | v2.0 |
|---------|------|------|
| **Basic scan** | ✅ | ✅ |
| **Deep analysis** | ❌ | ✅ |
| **FOCUS mode** | ❌ | ✅ |
| **HTK mode** | ❌ | ✅ |
| **Module loading** | ❌ | ✅ |
| **Output formats** | Text | Markdown, JSON, Memory, Checklist |
| **Parallel execution** | ❌ | ✅ |
| **Subagent delegation** | ❌ | ✅ |
| **Token usage** | ~800 | ~250 | **69% reduction** |

**Example**:

```bash
# v1.0
/scan-env
# → Runs complete scan (800 tokens)

# v2.0
/scan-env --mode=focus
# → Identifies critical areas first (150 tokens)
# → Loads only relevant modules (100 tokens)
# → Delegates to specialized subagents (parallel)
# → Total: ~250 tokens
```

---

### `/doc-workflow`

| Feature | v1.0 | v2.0 |
|---------|------|------|
| **Basic workflow** | ✅ | ✅ |
| **Interactive mode** | ❌ | ✅ |
| **Real-time validation** | ❌ | ✅ |
| **Error handling** | Basic | Comprehensive |
| **HTK methodology** | ❌ | ✅ |
| **Template generation** | ❌ | ✅ |
| **Workspace isolation** | ✅ | ✅ |
| **Memory integration** | Manual | Automated |

**Example**:

```bash
# v1.0
/doc-workflow docker
# → Documents workflow
# → Saves to workspace/
# → Manual integration to CLAUDE.md

# v2.0
/doc-workflow docker --interactive --mode=htk
# → Executes step-by-step with validation
# → Tests each step (HTK)
# → Generates reusable template
# → Auto-updates CLAUDE.md with findings
```

---

### `/search-code`

| Feature | v1.0 | v2.0 |
|---------|------|------|
| **Pattern search** | ✅ | ✅ |
| **Categorization** | Basic | Advanced |
| **Pattern analysis** | ❌ | ✅ |
| **Subagent delegation** | ❌ | ✅ |
| **Module export** | ❌ | ✅ |
| **Architecture detection** | ❌ | ✅ |

**Example**:

```bash
# v1.0
/search-code "API endpoints"
# → Lists matching code

# v2.0
/search-code "API endpoints" --analyze-patterns
# → Finds patterns
# → Categorizes by type (REST, GraphQL, etc.)
# → Detects architecture patterns
# → Exports to knowledge module
# → Suggests improvements
```

---

## New Commands in v2.0

### Planning & Methodology

| Command | Description | Token Usage |
|---------|-------------|-------------|
| `/focus` | FOCUS framework for problem decomposition | ~150 |
| `/htk-plan` | Create Hypothesis→Test Kernel plans | ~200 |
| `/evaluate-tool` | Comprehensive tool assessment | ~300 |
| `/benchmark-tool` | Performance benchmarking | ~250 |
| `/tool-compatibility` | Cross-tool integration analysis | ~200 |

### Environment Analysis

| Command | Description | Token Usage |
|---------|-------------|-------------|
| `/scan-env-deep` | Comprehensive environment analysis | ~400 |
| `/env-compare` | Compare environment profiles | ~250 |
| `/env-troubleshoot` | Guided troubleshooting | ~300 |

### Documentation & Memory

| Command | Description | Token Usage |
|---------|-------------|-------------|
| `/create-memory-profile` | Generate CLAUDE.md profiles | ~200 |
| `/workflow-template` | Generate workflow templates | ~150 |
| `/export-module` | Export knowledge to module | ~100 |

---

## Skills Comparison

### v1.0

**Skills**: None (all manual execution)

### v2.0

| Skill | Purpose | Auto-loads When |
|-------|---------|-----------------|
| **environment-intelligence** | Autonomous environment analysis | User mentions "environment", "setup", "analyze my system" |
| **tool-evaluator** | Comprehensive tool assessment | User mentions "evaluate tool", "check if X works" |
| **workflow-documenter** | Interactive workflow capture | User mentions "document workflow", "how to deploy" |

**Benefits**:
- No need to remember exact command syntax
- Claude autonomously determines best approach
- Progressive disclosure of information
- Token-efficient execution

---

## Knowledge Architecture

### v1.0

```
Commands contain all knowledge inline
├── scan-env.md (includes all env knowledge)
├── doc-workflow.md (includes all workflow knowledge)
└── search-code.md (includes all code analysis knowledge)

Problem: Knowledge duplication, token waste
```

### v2.0

```
Modular knowledge system
├── commands/           # Thin wrappers
│   └── scan-env.md    # References modules
├── .claude/
│   ├── guides/        # Process knowledge
│   ├── frameworks/    # Tech-specific patterns
│   ├── environments/  # Environment configs
│   ├── templates/     # Reusable templates
│   └── agents/        # Subagent definitions

Benefits: Reusability, token efficiency, maintainability
```

---

## Execution Model

### v1.0: Sequential Single-Agent

```
User → /scan-env → Claude (loads all knowledge) → Sequential execution → Output

Timeline:
[====== Scan ======][==== Analysis ====][== Report ==]
     10s                  8s                 2s
Total: 20s
Tokens: ~3000
```

### v2.0: Parallel Multi-Agent

```
User → environment-intelligence skill → Orchestrator → Parallel delegation

                    Orchestrator (FOCUS)
                          ↓
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                  ↓
  SecurityAnalyzer  PerformanceProfiler  IntegrationTester
  (200 tokens)      (250 tokens)         (180 tokens)
        ↓                 ↓                  ↓
        └─────────────────┴─────────────────┘
                          ↓
                    Synthesizer
                          ↓
                       Output

Timeline:
[= FOCUS =][====== Parallel Execution ======][= Synth =]
    3s              8s (parallel)               2s
Total: 13s (35% faster)
Tokens: ~930 (69% less)
```

---

## CLAUDE.md Integration

### v1.0

**Manual Process**:
1. Run `/scan-env`
2. Review output in `workspace/`
3. Manually copy relevant findings to CLAUDE.md
4. Update formatting
5. Test in new session

**Time**: ~15 minutes
**Token Impact**: No optimization

### v2.0

**Automated Process**:
1. Run `/scan-env --output-format=memory`
2. Auto-generates CLAUDE.md section
3. Suggests which modules to reference
4. Updates with selective loading directives
5. Validates format

**Time**: ~2 minutes
**Token Impact**: 60-80% reduction through smart loading

**Example v2.0 CLAUDE.md**:

```markdown
# Project Environment Profile

## Quick Reference
- Environment: WSL2 Ubuntu 22.04
- Key Tools: Docker, Node.js v20, Git
- Known Limitations: Git symlink issues

## Available Knowledge Modules

Load contextually:
- @.claude/environments/wsl2-ubuntu.md (when working on WSL2 issues)
- @.claude/frameworks/docker-desktop-patterns.md (when using Docker)
- @.claude/troubleshooting/git-symlinks.md (when debugging git)

## Context Selection

| Task | Load These Modules |
|------|-------------------|
| Deploy | @.claude/guides/deployment.md |
| Debug | @.claude/troubleshooting/{{issue}}.md |
| Evaluate tool | @.claude/guides/tool-evaluation.md |

---

*Smart loading keeps context under 500 tokens*
```

---

## Token Efficiency Analysis

### Real-World Example: "Analyze my development environment"

#### v1.0 Execution

```
1. Load /scan-env command                    200 tokens
2. Load all inline knowledge                2800 tokens
3. Execute system checks sequentially
4. Generate report
                                    Total: 3000 tokens
```

#### v2.0 Execution

```
1. Skill: environment-intelligence           100 tokens
2. FOCUS: Identify critical areas            150 tokens
3. Load only relevant modules:
   - wsl2-specifics.md                       150 tokens
   - docker-desktop-patterns.md              120 tokens
4. Delegate to subagents (parallel):
   - SecurityAnalyzer                        200 tokens
   - PerformanceProfiler                     250 tokens
   - IntegrationTester                       180 tokens
   (Only highest token count matters)
5. Synthesize results                         50 tokens
                                    Total:  ~900 tokens

Savings: 2100 tokens (70% reduction)
```

---

## Migration Complexity

| Migration Type | Time | Complexity | Risk |
|----------------|------|------------|------|
| **In-place upgrade** | 10 min | Low | Low (backward compatible) |
| **Fresh install** | 5 min | Very Low | Very Low |
| **Side-by-side testing** | 15 min | Medium | None (can rollback) |

---

## When to Choose Which Version

### Stick with v1.0 If:
- You only use basic `/scan-env` occasionally
- You don't need token optimization
- You prefer simple, flat structure
- You don't work on multiple projects

### Upgrade to v2.0 If:
- You need token efficiency (approaching limits)
- You want autonomous skills
- You need systematic methodologies (FOCUS/HTK)
- You work on multiple projects with varying stacks
- You want reusable knowledge modules
- You need parallel execution speed
- You want to contribute/extend the platform

---

## Feature Timeline

### v1.0 Features (Current)
- ✅ Basic environment scanning
- ✅ Workflow documentation
- ✅ Code pattern search
- ✅ Workspace isolation
- ✅ XML-structured output

### v2.0 Features (Proposed)
- ✅ All v1.0 features (backward compatible)
- ✅ Modular knowledge architecture
- ✅ FOCUS + HTK methodologies
- ✅ Multi-agent delegation
- ✅ Autonomous skills
- ✅ Smart CLAUDE.md generation
- ✅ Token optimization (70% reduction)
- ✅ Parallel execution
- ✅ Comprehensive tool evaluation
- ✅ Interactive workflow capture
- ✅ Template system

### Future (v2.1+)
- 🔮 MCP server integration (cloud APIs)
- 🔮 AI-powered environment optimization
- 🔮 Team environment sync
- 🔮 Continuous environment monitoring
- 🔮 Security vulnerability scanning
- 🔮 Performance regression detection

---

## Bottom Line

### v1.0
- **Best for**: Simple, occasional use
- **Strength**: Easy to understand
- **Limitation**: Token inefficient, manual everything

### v2.0
- **Best for**: Power users, multiple projects, token efficiency
- **Strength**: Autonomous, modular, systematic
- **Learning curve**: Medium (but gradual adoption possible)

### Recommendation
**Upgrade to v2.0** if you:
- Use CEI regularly
- Work on 2+ projects
- Need token efficiency
- Want autonomous operation

**Keep v1.0** if you:
- Use CEI rarely
- Have simple needs
- Prefer minimal complexity

---

## Quick Decision Matrix

```
Are you approaching token limits?
    YES → v2.0
    NO ↓

Do you work on multiple projects?
    YES → v2.0
    NO ↓

Do you want autonomous skills?
    YES → v2.0
    NO ↓

Do you need systematic methodologies?
    YES → v2.0
    NO ↓

Do you value simplicity over features?
    YES → v1.0
    NO → v2.0
```

---

## Try Before You Decide

Use **Path C: Side-by-Side** migration to test v2.0 without commitment:

```bash
# Install v2.0 alongside v1.0
git clone https://github.com/konradish/claude-environment-intelligence ~/.claude/cei-v2
cd ~/.claude/cei-v2
./scripts/install.sh --prefix=cei2

# Try both
/scan-env          # v1.0
/cei2-scan-env     # v2.0

# Compare results, choose winner
```

---

**Questions?** See `MIGRATION_GUIDE.md` or open an issue on GitHub.
