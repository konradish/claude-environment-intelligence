# LLM Agent Prompt Pack

A curated set of production-tested prompts that tame LLM-based autonomous agents. Built for developers who need predictable, tool-aware AI systems.

## Why agent systems?

• **Autonomy loop**: Agents perceive environment, plan actions, execute tools, and adapt based on results
• **Tool orchestration**: Modern agents coordinate multiple APIs, CLIs, and services without human intervention  
• **Reproducible reasoning**: Well-designed agents follow consistent decision patterns across similar tasks
• **Predictable outcomes**: Environment prompts eliminate guesswork by declaring exact capabilities upfront

Environment prompts make agents *predictable*.

## What's an environment prompt?

• **Declares system context**: Available mounts, paths, installed CLIs, and service endpoints
• **Sets boundaries**: Rate limits, network access, and tool permissions to prevent runaway behavior
• **Eliminates discovery**: Agents skip trial-and-error probing and jump straight to productive work

This approach prevents agents from spending tokens on environment discovery and reduces unpredictable failures.

## Quick start

```bash
git clone https://github.com/konradish/workflow-prompts.git
cd workflow-prompts
cp env-probe.md.example env-probe.md    # tweak paths & tokens
```

## Available Prompts

### Environment Prompts
- **[Environment Probe](prompts/env/env-probe.md)** - Systematic environment discovery and capability assessment

### Task Prompts
- **[Codebase Search](prompts/tasks/codebase-search.md)** - Efficient code pattern and implementation discovery
- **[Workflow Documentation](prompts/tasks/workflow-documentation.md)** - Document and validate specific tool workflows

### Workflow Guides
- **[Feature Development](prompts/guides/feature-development.md)** - End-to-end feature implementation workflow
- **[Tool Exploration](prompts/guides/tool-exploration.md)** - Systematic tool/technology exploration and validation

## Repo structure

```
prompts/
  env/       # environment probes & setup prompts
  tasks/     # reusable action prompts (search, code-refactor, etc.)
  guides/    # higher-level agent workflows
examples/    # minimal JSON calls & expected outputs
docs/        # deep dives, architecture diagrams
```

## Contributing

PRs welcome, follow Conventional Commits.

## License

[MIT](LICENSE)