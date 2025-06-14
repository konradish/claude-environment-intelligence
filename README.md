# Workflow Prompts

A curated collection of specialized system prompts designed to streamline common development and operational workflows using Large Language Models (LLMs).

## Purpose

This repository provides production-ready, token-optimized prompt templates for automating routine tasks and complex workflows. Each prompt is designed for efficiency, reliability, and real-world applicability.

## Prompt Collection

### Environment Profiling
- **`env-probe.md`** - Comprehensive system environment exploration and documentation
  - Automatically detects OS, tools, filesystem mounts, and performance characteristics
  - Generates structured reports with actionable recommendations
  - Optimized for WSL2/Linux environments with known caveat handling

## Key Design Principles

- **Token efficiency** - Minimized prompt overhead for cost-effective operation
- **Structured outputs** - Consistent, parseable results across different LLM providers
- **Error resilience** - Graceful handling of missing tools or failed commands
- **Documentation focus** - Self-documenting prompts with clear usage instructions

## Planned Additions

Future prompts will cover:
- Code review and quality assessment workflows
- CI/CD pipeline generation and troubleshooting
- Project setup and scaffolding automation
- Security audit and compliance checking
- Performance optimization and monitoring

## Usage

Each prompt template includes:
1. **Configuration section** - Customize for your specific environment
2. **Execution flow** - Step-by-step workflow definition
3. **Output format** - Structured result specifications
4. **Usage examples** - Real-world application scenarios

Simply copy the desired prompt template and adapt the configuration section to your needs.