# Claude Environment Intelligence - Complete Revamp Proposal

**Version**: 2.0
**Date**: 2025-11-08
**Status**: Proposal - Awaiting Review

---

## Executive Summary

Transform **Claude Environment Intelligence (CEI)** from a basic command pack into a **comprehensive Claude Code Development Intelligence Platform** by integrating:

1. **Modular Knowledge Architecture** (from prompt-kit)
2. **FOCUS + HTK Methodology** for systematic analysis (from prompt-kit)
3. **Agent Delegation Patterns** for token-efficient execution (from prompt-kit)
4. **Compositional Hierarchy** (Slash Commands → Skills → Subagents)
5. **Dual-Mode System**: Direct execution commands + Reusable knowledge templates

---

## Current State Analysis

### ✅ Strengths
- Workspace isolation pattern (clean project directories)
- XML-structured outputs (reliable parsing)
- Memory integration concept (CLAUDE.md)
- Practical environment discovery focus

### ⚠️ Limitations
- **Single-layer architecture**: Only slash commands, no skills or subagents
- **No knowledge reusability**: Each command is self-contained
- **Limited methodology**: No systematic planning framework (FOCUS/HTK)
- **Token inefficiency**: No modular loading or context optimization
- **No agent delegation**: Everything runs in main context
- **Missing templates**: No reusable prompt templates or knowledge modules

---

## Proposed Architecture

### 🏗 Three-Layer System

```
┌─────────────────────────────────────────────────────────────┐
│                    USER INTERFACE LAYER                      │
├─────────────────────────────────────────────────────────────┤
│  Slash Commands (Direct Execution)                          │
│  /scan-env, /evaluate-tool, /doc-workflow, /troubleshoot   │
└────────────────┬────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│                   ORCHESTRATION LAYER                        │
├─────────────────────────────────────────────────────────────┤
│  Skills (Autonomous Management)                              │
│  - environment-intelligence                                  │
│  - tool-evaluator                                           │
│  - workflow-documenter                                      │
│                                                              │
│  Methodologies                                               │
│  - FOCUS: Structured problem decomposition                  │
│  - HTK: Hypothesis → Test Kernel                           │
└────────────────┬────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│                   KNOWLEDGE LAYER                            │
├─────────────────────────────────────────────────────────────┤
│  .claude/                                                    │
│  ├── guides/           # Process knowledge                  │
│  │   ├── environment-discovery.md                          │
│  │   ├── tool-evaluation-patterns.md                       │
│  │   ├── troubleshooting-methodology.md                    │
│  │   └── workflow-documentation.md                         │
│  ├── frameworks/       # Tech-specific patterns             │
│  │   ├── wsl2-specifics.md                                 │
│  │   ├── docker-desktop-patterns.md                        │
│  │   └── git-workflows.md                                  │
│  ├── environments/     # Environment configs                │
│  │   ├── wsl2-ubuntu.md                                    │
│  │   ├── macos-dev.md                                      │
│  │   └── linux-native.md                                   │
│  ├── templates/        # Reusable templates                │
│  │   ├── CLAUDE.md.template                               │
│  │   ├── environment-profile.md                            │
│  │   └── tool-evaluation-report.md                         │
│  └── agents/           # Subagent definitions               │
│      ├── security-analyzer.md                              │
│      ├── performance-profiler.md                           │
│      └── integration-tester.md                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Core Innovations

### 1. **Modular Knowledge Architecture**

**Problem**: Current commands are monolithic, repeating the same knowledge.

**Solution**: Extract reusable knowledge into `.claude/` modules.

```
.claude/
├── guides/
│   ├── environment-discovery.md      # How to discover environments
│   ├── tool-evaluation-patterns.md   # Tool assessment methodology
│   ├── troubleshooting-methodology.md # Systematic debugging
│   └── workflow-documentation.md     # Workflow capture patterns
├── frameworks/
│   ├── wsl2-specifics.md             # WSL2 quirks and solutions
│   ├── docker-desktop-patterns.md    # Docker Desktop integration
│   ├── nodejs-environments.md        # Node.js environment patterns
│   └── python-environments.md        # Python environment patterns
├── environments/
│   ├── wsl2-ubuntu.md                # WSL2 Ubuntu profile
│   ├── macos-dev.md                  # macOS development profile
│   └── linux-native.md               # Native Linux profile
├── troubleshooting/
│   ├── wsl2-git-symlinks.md         # Git symlink issues
│   ├── docker-networking.md          # Docker network problems
│   ├── permission-errors.md          # Permission troubleshooting
│   └── path-resolution.md            # Path-related issues
└── templates/
    ├── CLAUDE.md.template            # Smart context template
    ├── environment-profile.md        # Environment documentation
    └── tool-evaluation-report.md     # Tool assessment template
```

**Benefits**:
- **Token efficiency**: Load only relevant modules (60-80% reduction)
- **Reusability**: Same modules across projects
- **Maintainability**: Update once, apply everywhere
- **Scalability**: Add knowledge without bloating commands

---

### 2. **FOCUS + HTK Methodology**

**Problem**: Ad-hoc environment analysis lacks systematic approach.

**Solution**: Integrate FOCUS (problem decomposition) + HTK (hypothesis testing).

#### FOCUS Template
```markdown
# FOCUS

Options (≤3):
* <label>: <one-sentence outcome> — Why-first: <≤2 sentences>
* ...

Chosen: <label>

Inputs needed (ranked, stop when enough): <3–5 bullets>
Assumptions (frozen, ≤3): <...>
```

#### HTK Template
```markdown
# HTK (Hypothesis→Test Kernel)

Goal: <one sentence>

Hypothesis: <if we do X, Y happens as shown by Z>

Test:
* Change: <the one change>
* Method: <where/how; minimal steps; timebox>
* Rollback: <exact step>

Verify:
* Metric: <metric + threshold>
* Evidence: <where it will live>

Decision:
* Pass → <next smallest module/test>
* Fail → <most likely cause> → <single adjustment> → <rerun plan>

Why first: <≤2 sentences>
```

**Usage Example**:
```bash
# Instead of:
/scan-env

# New approach with methodology:
/scan-env --mode=htk
# → Uses FOCUS to identify critical areas
# → Generates HTK for each hypothesis
# → Tests systematically
# → Documents learnings
```

---

### 3. **Agent Delegation Pattern**

**Problem**: All analysis runs in main context, consuming tokens.

**Solution**: Delegate specialized tasks to focused subagents.

```
User Intent: "Analyze my development environment"
    ↓
Primary Architect Agent (Main Claude)
    ├→ SecurityAnalyzer (loads: security-patterns.md)
    ├→ PerformanceProfiler (loads: performance-testing.md)
    └→ IntegrationTester (loads: tool-compatibility.md)
         ↓
Deterministic Slash Commands (/report, /commit)
         ↓
   Human Audit Point
```

**Example Subagent**: `.claude/agents/security-analyzer.md`
```markdown
---
name: security-analyzer
description: Analyze environment for security issues
tools: Bash(ls:*, cat:*), Read, Grep
model: sonnet
---

You are a security expert. When analyzing an environment:

1. Load relevant knowledge: @.claude/guides/security-analysis.md
2. Check for common vulnerabilities
3. Test permission boundaries
4. Document findings with severity levels
5. Return actionable recommendations

Only load knowledge modules needed for current task.
```

**Benefits**:
- **Token efficiency**: 60-80% reduction through selective loading
- **Parallel execution**: Multiple subagents work simultaneously
- **Specialization**: Each agent excels in narrow domain
- **Clean separation**: Security, performance, integration isolated

---

### 4. **Compositional Hierarchy**

**From prompt-kit's best practices:**

```
LEVEL 1: Slash Commands (Primitives)
└─ /scan-env, /evaluate-tool
    ↓
LEVEL 2: Skills (Autonomous Management)
└─ environment-intelligence (orchestrates multiple commands)
    ↓
LEVEL 3: Subagents (Parallel Specialization)
└─ security-analyzer, performance-profiler
    ↓
LEVEL 4: MCP Servers (External Integration)
└─ cloud-provider-apis, monitoring-systems
```

**Design Principle**: Start with primitives, compose up as needed.

---

### 5. **Smart CLAUDE.md Context Selection**

**Problem**: Monolithic CLAUDE.md files grow unwieldy.

**Solution**: Lightweight entry point with selective module loading.

**Template**: `.claude/templates/CLAUDE.md.template`
```markdown
# Project Environment Profile: {{project_name}}

## Quick Reference
- **Environment**: {{environment_type}}
- **OS**: {{os_details}}
- **Key Tools**: {{tool_list}}
- **Known Limitations**: {{limitation_summary}}

## Available Knowledge Modules

### Environment Discovery
- @.claude/guides/environment-discovery.md - Systematic discovery
- @.claude/environments/{{environment_type}}.md - Environment-specific

### Tool Management
- @.claude/guides/tool-evaluation-patterns.md - Assessment methodology
- @.claude/frameworks/{{primary_framework}}-patterns.md - Framework specifics

### Troubleshooting
- @.claude/troubleshooting/{{common_issue_1}}.md
- @.claude/troubleshooting/{{common_issue_2}}.md

## Context Selection Guide

**Before starting a task, tell me what you're trying to accomplish.**

| Task Intent | Load These Modules |
|-------------|-------------------|
| Discover environment | @.claude/guides/environment-discovery.md |
| Evaluate tool | @.claude/guides/tool-evaluation-patterns.md |
| Debug WSL2 issue | @.claude/troubleshooting/wsl2-git-symlinks.md |
| Document workflow | @.claude/guides/workflow-documentation.md |

---

*This CLAUDE.md uses modular knowledge architecture for token efficiency.*
```

**Benefits**:
- Main CLAUDE.md stays under 500 tokens
- Explicit mapping from tasks to knowledge
- Self-service module selection
- Progressive disclosure of information

---

## Proposed Repository Structure

```
claude-environment-intelligence/
├── src/
│   ├── commands/                        # Slash Commands (Layer 1)
│   │   ├── core/
│   │   │   ├── scan-env.md             # Enhanced with FOCUS/HTK
│   │   │   ├── scan-env-deep.md        # Comprehensive analysis
│   │   │   └── env-troubleshoot.md     # Guided troubleshooting
│   │   ├── evaluation/
│   │   │   ├── evaluate-tool.md        # Tool assessment
│   │   │   ├── benchmark-tool.md       # Performance testing
│   │   │   └── tool-compatibility.md   # Integration analysis
│   │   ├── documentation/
│   │   │   ├── doc-workflow.md         # Workflow capture
│   │   │   ├── workflow-template.md    # Template generation
│   │   │   └── create-memory-profile.md # CLAUDE.md generation
│   │   └── analysis/
│   │       ├── env-compare.md          # Environment comparison
│   │       ├── search-code.md          # Code pattern analysis
│   │       └── pattern-analysis.md     # Architecture detection
│   ├── skills/                          # Skills (Layer 2)
│   │   ├── environment-intelligence/
│   │   │   └── SKILL.md                # Autonomous env management
│   │   ├── tool-evaluator/
│   │   │   └── SKILL.md                # Tool assessment orchestration
│   │   └── workflow-documenter/
│   │       └── SKILL.md                # Documentation automation
│   └── .claude/                         # Knowledge Modules (Layer 3)
│       ├── guides/
│       │   ├── environment-discovery.md
│       │   ├── tool-evaluation-patterns.md
│       │   ├── troubleshooting-methodology.md
│       │   ├── workflow-documentation.md
│       │   ├── focus-htk-methodology.md
│       │   └── agent-delegation.md
│       ├── frameworks/
│       │   ├── wsl2-specifics.md
│       │   ├── docker-desktop-patterns.md
│       │   ├── nodejs-environments.md
│       │   └── python-environments.md
│       ├── environments/
│       │   ├── wsl2-ubuntu.md
│       │   ├── macos-dev.md
│       │   └── linux-native.md
│       ├── troubleshooting/
│       │   ├── wsl2-git-symlinks.md
│       │   ├── docker-networking.md
│       │   ├── permission-errors.md
│       │   └── path-resolution.md
│       ├── templates/
│       │   ├── CLAUDE.md.template
│       │   ├── environment-profile.md
│       │   ├── tool-evaluation-report.md
│       │   ├── knowledge-module.md
│       │   └── focus-htk-plan.md
│       └── agents/
│           ├── security-analyzer.md
│           ├── performance-profiler.md
│           ├── integration-tester.md
│           └── documentation-generator.md
├── examples/
│   ├── environment-reports/             # Sample outputs
│   ├── tool-evaluations/
│   ├── workflow-documentation/
│   ├── memory-profiles/                 # CLAUDE.md examples
│   └── htk-analyses/                    # HTK methodology examples
├── docs/
│   ├── architecture/
│   │   ├── compositional-hierarchy.md   # Layer explanation
│   │   ├── modular-knowledge.md         # Knowledge architecture
│   │   ├── agent-delegation.md          # Delegation patterns
│   │   └── smart-context-selection.md   # Context optimization
│   ├── methodologies/
│   │   ├── focus-framework.md           # FOCUS methodology
│   │   ├── htk-framework.md             # HTK methodology
│   │   └── boundary-decomposition.md    # Problem decomposition
│   ├── guides/
│   │   ├── getting-started.md
│   │   ├── command-reference.md
│   │   ├── skill-development.md
│   │   └── knowledge-authoring.md
│   └── best-practices/
│       ├── token-efficiency.md
│       ├── workspace-isolation.md
│       └── memory-integration.md
├── tests/
│   ├── commands/                        # Command validation
│   ├── skills/                          # Skill testing
│   └── integration/                     # End-to-end tests
├── CLAUDE.md                            # Smart entry point
├── INSTALL.md                           # Installation guide
└── README.md                            # Main documentation
```

---

## Implementation Plan

### Phase 1: Foundation (Week 1)
**Goal**: Establish modular knowledge architecture

#### 1.1 Knowledge Module Migration
- [ ] Create `.claude/` directory structure
- [ ] Extract common knowledge from existing commands into modules
- [ ] Create module templates for consistency
- [ ] Build smart CLAUDE.md entry point

#### 1.2 Enhanced Commands
- [ ] Update `/scan-env` with module references
- [ ] Add `--mode=htk` flag for systematic analysis
- [ ] Implement XML-structured output parsing
- [ ] Add parallel execution where possible

**Deliverables**:
- Modular `.claude/` directory with 10+ knowledge modules
- Enhanced `/scan-env` command with FOCUS/HTK support
- Smart CLAUDE.md template
- Knowledge module authoring guide

---

### Phase 2: Methodologies (Week 2)
**Goal**: Integrate FOCUS + HTK frameworks

#### 2.1 FOCUS Framework
- [ ] Create `focus-htk-methodology.md` guide
- [ ] Add `/focus` command for problem decomposition
- [ ] Integrate FOCUS into `/scan-env --mode=focus`
- [ ] Create FOCUS templates and examples

#### 2.2 HTK Framework
- [ ] Create HTK templates (`htk-plan.md`)
- [ ] Add `/htk-plan` command for systematic testing
- [ ] Integrate HTK into analysis workflows
- [ ] Create version hygiene patterns

**Deliverables**:
- FOCUS + HTK methodology guides
- `/focus` and `/htk-plan` commands
- HTK-based analysis examples
- Version hygiene documentation

---

### Phase 3: Agent Delegation (Week 3)
**Goal**: Implement multi-agent architecture

#### 3.1 Subagent Development
- [ ] Create `.claude/agents/` directory
- [ ] Build `security-analyzer.md` subagent
- [ ] Build `performance-profiler.md` subagent
- [ ] Build `integration-tester.md` subagent
- [ ] Build `documentation-generator.md` subagent

#### 3.2 Primary Orchestration
- [ ] Update CLAUDE.md with delegation strategy
- [ ] Create delegation decision tree
- [ ] Implement parallel subagent execution
- [ ] Add subagent result synthesis

**Deliverables**:
- 4+ specialized subagents
- Delegation orchestration system
- Parallel execution examples
- Token efficiency benchmarks

---

### Phase 4: Skills Layer (Week 4)
**Goal**: Build autonomous management skills

#### 4.1 Environment Intelligence Skill
- [ ] Create `skills/environment-intelligence/SKILL.md`
- [ ] Implement autonomous environment discovery
- [ ] Add progressive disclosure of modules
- [ ] Integrate with subagents

#### 4.2 Tool Evaluator Skill
- [ ] Create `skills/tool-evaluator/SKILL.md`
- [ ] Implement comprehensive tool assessment
- [ ] Add benchmark orchestration
- [ ] Integrate compatibility analysis

#### 4.3 Workflow Documenter Skill
- [ ] Create `skills/workflow-documenter/SKILL.md`
- [ ] Implement interactive workflow capture
- [ ] Add template generation
- [ ] Integrate with memory system

**Deliverables**:
- 3 autonomous skills
- Skill composition examples
- Token efficiency analysis
- User experience improvements

---

### Phase 5: Polish & Documentation (Week 5)
**Goal**: Production-ready platform

#### 5.1 Documentation
- [ ] Complete architecture documentation
- [ ] Write methodology guides (FOCUS/HTK)
- [ ] Create comprehensive examples
- [ ] Build migration guide from v1.0

#### 5.2 Installation & Distribution
- [ ] Enhanced installation script
- [ ] Global command deployment
- [ ] Module discovery system
- [ ] Version management

#### 5.3 Testing & Validation
- [ ] Command validation tests
- [ ] Skill integration tests
- [ ] Multi-environment testing
- [ ] Performance benchmarks

**Deliverables**:
- Complete documentation suite
- One-command installation
- Comprehensive test coverage
- Migration guide

---

## Success Metrics

### Technical Metrics
- **Token Efficiency**: 60-80% reduction in context usage
- **Knowledge Reusability**: 10+ modules used across 3+ commands
- **Parallel Execution**: 3+ subagents working simultaneously
- **Command Coverage**: 15+ production-ready commands
- **Skills**: 3+ autonomous management skills
- **Response Time**: <2s for command execution

### User Experience Metrics
- **Installation**: <5 minutes from clone to usage
- **Learning Curve**: 15 minutes to productivity
- **Documentation Quality**: Self-service >80%
- **Module Discovery**: Relevant modules found in <30s

### Platform Metrics
- **Modularity**: Knowledge updates affect 3+ commands
- **Extensibility**: New commands built in <1 hour
- **Maintainability**: Bug fixes in single location
- **Scalability**: Handles 10+ concurrent projects

---

## Key Differentiators

### Before (CEI v1.0)
```
User: /scan-env
    ↓
Single command (monolithic)
    ↓
3000+ tokens loaded
    ↓
Sequential execution
    ↓
One-time knowledge
```

### After (CEI v2.0)
```
User: "Analyze my environment systematically"
    ↓
Skill: environment-intelligence (autonomous)
    ↓
FOCUS: Identify critical areas (300 tokens)
    ↓
Delegate to Subagents (parallel):
├─ SecurityAnalyzer (200 tokens)
├─ PerformanceProfiler (250 tokens)
└─ IntegrationTester (180 tokens)
    ↓
Load only needed modules:
├─ @.claude/guides/security-analysis.md
├─ @.claude/guides/performance-testing.md
└─ @.claude/guides/integration-patterns.md
    ↓
HTK: Systematic testing
    ↓
Results synthesis + Memory integration
    ↓
Total: ~930 tokens (69% reduction)
```

---

## Migration Strategy

### For Existing Users

#### Option 1: In-Place Upgrade
```bash
# Backup current installation
cp -r ~/.claude/commands ~/.claude/commands.backup

# Pull latest changes
cd ~/.claude/cei
git pull origin main

# Run migration script
./scripts/migrate-v1-to-v2.sh
```

#### Option 2: Fresh Install
```bash
# Remove old installation
rm -rf ~/.claude/cei

# Clone v2.0
git clone https://github.com/konradish/claude-environment-intelligence ~/.claude/cei

# Install globally
~/.claude/cei/scripts/install.sh
```

### Backward Compatibility
- All v1.0 commands remain functional
- New `--mode=` flags add capabilities
- Gradual migration path
- Deprecation warnings for old patterns

---

## Risk Assessment

### Technical Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Module loading complexity | Medium | High | Progressive rollout, fallback to monolithic |
| Subagent coordination failures | Low | Medium | Robust error handling, timeouts |
| Token budget miscalculation | Medium | Medium | Conservative estimates, monitoring |
| Knowledge module duplication | High | Low | Clear ownership, regular audits |

### User Experience Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Increased complexity | High | High | Excellent documentation, gradual adoption |
| Learning curve | Medium | Medium | Interactive tutorials, examples |
| Breaking changes | Low | High | Backward compatibility, migration guide |
| Module discovery confusion | Medium | Medium | Smart CLAUDE.md, clear naming |

---

## Timeline & Resources

### Development Timeline
- **Week 1**: Foundation (40 hours)
- **Week 2**: Methodologies (30 hours)
- **Week 3**: Agent Delegation (35 hours)
- **Week 4**: Skills Layer (30 hours)
- **Week 5**: Polish & Documentation (25 hours)
- **Total**: ~160 hours over 5 weeks

### Required Resources
- Development environment (WSL2, macOS, Linux)
- Testing infrastructure
- Documentation tools
- Community feedback channel

---

## Open Questions for Review

1. **prompt-vault Integration**: Should we integrate patterns from prompt-vault (pending access)?
2. **MCP Server Integration**: Should we add MCP servers for cloud provider APIs?
3. **Skill Prioritization**: Which skills should be built first?
4. **Module Granularity**: How granular should knowledge modules be? (100-500 tokens?)
5. **Naming Convention**: Should we keep "CEI" or rename to "Claude Development Intelligence"?
6. **Global vs Project**: Should skills be global (~/.claude/skills/) or project-specific?

---

## Next Steps

1. **Review & Feedback**: Gather feedback on this proposal
2. **Access prompt-vault**: Integrate additional patterns if available
3. **Prioritize Phases**: Confirm implementation order
4. **Kickoff**: Begin Phase 1 development
5. **Community Preview**: Share early version for feedback

---

## Conclusion

This revamp transforms CEI from a basic command pack into a **comprehensive, token-efficient, modular platform** that:

- **Reduces token usage by 60-80%** through modular knowledge
- **Enables autonomous operation** via skills layer
- **Provides systematic methodologies** (FOCUS/HTK) for analysis
- **Supports parallel execution** through agent delegation
- **Scales efficiently** as knowledge grows
- **Maintains backward compatibility** with gradual migration

The result is a **production-ready Claude Code Development Intelligence Platform** that sets a new standard for environment discovery and analysis.

---

**Prepared by**: Claude Code
**Proposal Status**: Awaiting Review
**Next Review**: Upon prompt-vault access or user feedback
