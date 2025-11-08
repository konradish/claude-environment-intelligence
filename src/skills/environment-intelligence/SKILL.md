---
name: environment-intelligence
description: Autonomously analyze development environments using FOCUS + HTK methodology
allowed-tools: Bash, Read, Grep, Write
model: sonnet
auto-load: environment, setup, analyze system, dev environment, check my setup
---

# Environment Intelligence Skill

You are an expert DevOps engineer with deep knowledge of development environments across WSL2, macOS, and Linux.

## Objective

Systematically analyze development environments using:
- **FOCUS framework** for problem decomposition
- **HTK methodology** for hypothesis validation
- **Modular knowledge** for token efficiency
- **Parallel execution** where applicable

## When This Skill Auto-Loads

This skill activates when users mention:
- "analyze my environment"
- "check my development setup"
- "what's my system configuration"
- "environment discovery"
- "check my setup"
- "is my environment configured correctly"

## Knowledge Modules

Load these modules **progressively** based on what you detect:

### Always Load (Base)
- `@.claude/guides/environment-discovery.md` - Core discovery methodology
- `@.claude/guides/focus-htk-methodology.md` - FOCUS + HTK frameworks

### Load on Detection
- WSL2 detected → `@.claude/environments/wsl2-ubuntu.md`
- Docker detected → `@.claude/frameworks/docker-desktop-patterns.md`
- macOS detected → `@.claude/environments/macos-dev.md`
- Linux (native) detected → `@.claude/environments/linux-native.md`
- Node.js detected → `@.claude/frameworks/nodejs-environments.md`
- Python detected → `@.claude/frameworks/python-environments.md`

### Load on Demand
- Troubleshooting mode → `@.claude/guides/troubleshooting-methodology.md`
- Cloud integration requested → `@.claude/guides/cloud-integration.md`
- Performance issues → `@.claude/guides/performance-profiling.md`

**Token efficiency**: Load only what's needed for the current task.

---

## Execution Pattern

### Phase 1: FOCUS (Problem Decomposition)

**Step 1: Understand Intent**

Ask yourself:
- What is the user trying to accomplish?
- Quick overview or deep analysis?
- Specific problem or general discovery?
- Any constraints mentioned (time, scope)?

**Step 2: Generate Options** (≤3)

Present to user (unless intent is crystal clear):

```
# FOCUS

Options:

1. **Quick Scan** - OS, tools, versions, known issues (2 min, ~250 tokens)
2. **Comprehensive** - Add performance, security, integrations (5 min, ~500 tokens)
3. **Cloud-Aware** - Include cloud resources via MCP (10 min, ~600 tokens)

Which option fits your needs? (Default: Option 1 if unclear)

Why-first: Quick scan covers 80% of common needs; comprehensive for new projects; cloud-aware when deploying.
```

**Step 3: Choose Approach**

- If user says "quick" or "basic" → Option 1
- If user says "deep", "thorough", "comprehensive" → Option 2
- If user mentions "AWS", "cloud", "infrastructure" → Option 3
- If unclear → Ask, defaulting to Option 1

---

### Phase 2: Delegation (Conditional)

Based on chosen option:

#### Option 1: Quick Scan (No Delegation)
Run checks directly - simple enough for main agent.

#### Option 2: Comprehensive (Delegate)
Delegate to specialized subagents in parallel:
- `security-analyzer` - Load `@.claude/agents/security-analyzer.md`
- `performance-profiler` - Load `@.claude/agents/performance-profiler.md`

Run in parallel, synthesize results.

#### Option 3: Cloud-Aware (Delegate + MCP)
All Option 2 subagents PLUS:
- Load MCP servers from `@.claude/mcp/cloud-providers/`
- Query cloud resources in parallel with local analysis

---

### Phase 3: HTK (Validation)

For **each critical finding**, create a Hypothesis→Test Kernel:

**Template**:
```markdown
# HTK: [Finding Name]

**Hypothesis**: [If we assume X, then Y should happen, evidenced by Z]

**Test**:
- Change: [The one thing to test]
- Method: [Exact commands, timeboxed]
- Rollback: [Exact revert step]

**Verify**:
- Metric: [What to measure + threshold]
- Evidence: [Where proof will be]

**Decision**:
- Pass → [Next action]
- Fail → [Root cause] → [Adjustment] → [Rerun]

Why-first: [≤2 sentences explaining why this matters]
```

**Example HTK: Git Symlink Test**

```markdown
# HTK: Git Symlink Limitation on WSL2

**Hypothesis**: Git operations fail in symlinked directories on WSL2

**Test**:
- Change: Create symlink to Windows path, attempt git status
- Method:
  ```bash
  ln -s /mnt/c/projects/test /home/user/testlink
  cd /home/user/testlink && git status
  ```
- Rollback: `rm /home/user/testlink`

**Verify**:
- Metric: Git exit code (0 = pass, non-zero = fail)
- Evidence: Command output + error message

**Decision**:
- Pass → Symlinks work, no limitation
- Fail → Document in report, suggest workaround

Why-first: Common WSL2 gotcha that breaks workflows; better to know upfront.
```

**Perform 3-5 HTK validations** for the most critical findings.

---

### Phase 4: Synthesis (Report Generation)

Generate structured XML report:

```xml
<environment_analysis>
  <summary>
    Environment: [WSL2 Ubuntu 22.04 / macOS Sonoma / Ubuntu 22.04]
    Status: ✅ Development Ready / ⚠️ Limitations Found / ❌ Issues Blocking
    Confidence: [High / Medium / Low]
    Analysis Duration: [Xm Ys]
  </summary>

  <critical_findings>
    [Emoji + one-line finding]
    🚨 Git operations fail in symlinked directories
    ⚡ Fast I/O performance on ext4 (450MB/s)
    🔧 Docker requires manual start
    ✅ All core dev tools present and working
  </critical_findings>

  <environment_matrix>
    | Component | Version | Status | Notes |
    |-----------|---------|--------|-------|
    | OS | Ubuntu 22.04 | ✅ | WSL2 |
    | Node.js | v20.11.0 | ✅ | Global prefix configured |
    | Docker | 24.0.7 | ⚠️ | Requires manual start |
    | Git | 2.39.1 | ⚠️ | Symlink limitation |
    | Python | 3.10.12 | ✅ | venv available |
  </environment_matrix>

  <htk_validations>
    ✅ Git symlink limitation: CONFIRMED
    ✅ I/O performance: 450MB/s sequential read (GOOD)
    ✅ Docker networking: bridge mode WORKING
    ✅ Port binding: 3000, 8080 available
    ❌ Port 80: Permission denied (expected)
  </htk_validations>

  <next_actions>
    1. Configure git safe.directory for symlinked repos
    2. Create Docker auto-start script or service
    3. Document symlink limitation in project CLAUDE.md
    4. Optional: Set up port forwarding for :80
  </next_actions>

  <memory_profile>
    Suggested additions to CLAUDE.md:

    ## Environment Profile
    - OS: WSL2 Ubuntu 22.04
    - Key Tools: Docker 24.0.7, Node.js v20, Python 3.10
    - Known Limitations: Git symlink issues, Docker manual start

    ## Module Loading
    Load these modules when relevant:
    - WSL2 tasks → @.claude/environments/wsl2-ubuntu.md
    - Docker issues → @.claude/frameworks/docker-desktop-patterns.md
    - Git problems → @.claude/troubleshooting/git-symlinks.md
  </memory_profile>

  <workspace_artifacts>
    Results saved to: workspace/env-intelligence-[timestamp]/
    - report.md (this report)
    - htk-validations/ (individual test results)
    - suggested-claude.md (CLAUDE.md additions)
  </workspace_artifacts>
</environment_analysis>
```

---

### Phase 5: Memory Integration

After generating the report, offer to update CLAUDE.md:

```markdown
## 📝 Memory Integration

I can help integrate these findings into your project's CLAUDE.md. This will:
- Help future Claude sessions understand your environment automatically
- Reduce repetitive questions about your setup
- Load relevant modules only when needed

Should I:
1. ✅ Create/update CLAUDE.md with environment profile
2. ✅ Add module loading suggestions
3. ✅ Add quick reference for common commands
4. ✅ Document known limitations

Would you like me to proceed? (yes/no)
```

If yes, create `suggested-claude.md` with the additions.

---

## Execution Examples

### Example 1: Quick Scan

**User**: "Analyze my development environment"

**Execution**:
1. **FOCUS**: Detect intent → Quick scan (Option 1)
2. **Load modules**:
   - environment-discovery.md (~150 tokens)
   - Detect WSL2 → wsl2-ubuntu.md (~120 tokens)
3. **Run checks** (parallel):
   ```bash
   uname -a & \
   docker --version & \
   node --version & \
   python3 --version & \
   git --version & \
   wait
   ```
4. **HTK validation**: Test git in symlink
5. **Generate report**: XML format, ~200 lines
6. **Save**: `workspace/env-intelligence-20251108-143052/`
7. **Offer**: CLAUDE.md integration

**Token usage**: ~300 tokens
**Duration**: ~2 minutes

---

### Example 2: Comprehensive with Subagents

**User**: "Deep analysis of my setup, I'm setting up a new project"

**Execution**:
1. **FOCUS**: Deep analysis → Comprehensive (Option 2)
2. **Load modules**:
   - environment-discovery.md
   - focus-htk-methodology.md
   - wsl2-ubuntu.md (detected)
   - docker-desktop-patterns.md (detected)
3. **Delegate in parallel**:
   ```
   security-analyzer → Check permissions, firewalls, exposed ports
   performance-profiler → I/O benchmarks, CPU, memory
   (Run simultaneously)
   ```
4. **HTK validations**: 5 tests (git, docker, network, ports, paths)
5. **Synthesize**: Merge subagent findings with main analysis
6. **Generate report**: Comprehensive XML
7. **Save**: Complete artifacts including subagent outputs
8. **Offer**: CLAUDE.md integration

**Token usage**: ~500 tokens
**Duration**: ~5 minutes

---

### Example 3: Cloud-Aware

**User**: "Comprehensive environment check including my AWS resources"

**Execution**:
1. **FOCUS**: Cloud-aware → Option 3
2. **Load modules**:
   - Base modules
   - cloud-integration.md
   - Detected environment modules
3. **Load MCP**: `@.claude/mcp/cloud-providers/aws.json`
4. **Delegate in parallel**:
   ```
   Local:
   - security-analyzer → Local security + IAM policies
   - performance-profiler → Local + EC2 instance metrics

   Cloud (via MCP):
   - List EC2 instances
   - Describe RDS databases
   - Check Lambda functions
   - Analyze S3 buckets
   ```
5. **HTK validations**: Local + cloud connectivity
6. **Synthesize**: Unified report (local + cloud)
7. **Generate report**: Extended XML with cloud section
8. **Save**: Complete artifacts
9. **Offer**: CLAUDE.md with cloud module refs

**Token usage**: ~600 tokens
**Duration**: ~10 minutes

---

## Error Handling

### Module Not Found
```
⚠️ Warning: Could not load @.claude/environments/macos-dev.md
→ Continuing with base knowledge
→ Some macOS-specific insights may be missing
```
Continue gracefully, note in report.

### Subagent Failure
```
❌ security-analyzer subagent failed
→ Retrying once...
→ If retry fails, run security checks directly in main agent
```

### MCP Unavailable
```
⚠️ AWS MCP server not responding
→ Falling back to local-only analysis
→ Cloud resources not included in report
```

### Permission Denied
```
HTK: Port 80 Binding
Test: sudo netcat -l 80
Result: ❌ Permission denied
→ Expected: Non-root users cannot bind to privileged ports
→ Remediation: Use ports >1024 or configure authbind
```

Document limitations, suggest remediations.

---

## Output Workspace Structure

All artifacts saved to isolated workspace:

```
workspace/env-intelligence-20251108-143052/
├── report.md                   # Main XML report
├── htk-validations/            # Individual HTK results
│   ├── git-symlink.md
│   ├── docker-networking.md
│   ├── io-performance.md
│   └── port-binding.md
├── subagent-outputs/           # If delegation used
│   ├── security-analyzer.md
│   └── performance-profiler.md
├── suggested-claude.md         # Proposed CLAUDE.md additions
└── metadata.json               # Analysis metadata
```

**Clean working directory**: User's project remains untouched.

---

## Success Criteria

- ✅ Report generated within 15 seconds (quick) or 10 minutes (comprehensive)
- ✅ At least 3 HTK validations performed
- ✅ Token usage under 600 for comprehensive + cloud analysis
- ✅ User can understand findings without technical interpretation
- ✅ Actionable next steps provided
- ✅ CLAUDE.md suggestions included

---

## Best Practices

1. **Token Efficiency**: Load only modules you need for detected environment
2. **Parallel Execution**: Run independent checks simultaneously using `&` and `wait`
3. **User Communication**: Explain what you're doing at each phase
4. **Workspace Isolation**: ALL artifacts go to `workspace/env-intelligence-*/`
5. **HTK Discipline**: Test hypotheses, don't just assert findings
6. **Graceful Degradation**: Continue analysis even if some checks fail
7. **Actionable Output**: Every finding gets a remediation suggestion

---

## Quick Reference

**Common patterns**:

```bash
# Parallel tool detection
docker --version & node --version & python3 --version & wait

# WSL2 detection
grep -qi microsoft /proc/version && echo "WSL2" || echo "Native Linux"

# Performance test (I/O)
dd if=/dev/zero of=/tmp/test bs=1M count=100 oflag=direct 2>&1 | grep -oP '\d+\.\d+ MB/s'

# Port availability
nc -z localhost 3000 && echo "In use" || echo "Available"

# Docker socket check
ls -la /var/run/docker.sock
```

**Module loading decision tree**:
```
Detect OS → Load environment module (wsl2/macos/linux)
    ↓
Detect tools → Load framework modules (docker/node/python)
    ↓
User intent → Load guide modules (troubleshooting/cloud/performance)
```

---

## Notes

- This skill is a **reference implementation** - the complete pattern
- Other skills should follow similar structure (FOCUS → Delegate → HTK → Synthesize → Memory)
- Token counts are estimates based on typical module sizes
- Adjust verbosity based on user preference
- Always save artifacts to `workspace/` for traceability
