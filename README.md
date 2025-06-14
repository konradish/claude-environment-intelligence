# LLM Environment Exploration

This repository contains a system prompt template designed for efficiently exploring and documenting development environments using Large Language Models (LLMs).

## Purpose

The main goal is to provide a token-efficient, structured approach for LLM agents to:

1. **Profile system environments** - Automatically detect OS, distributions, mounted filesystems, and available tools
2. **Generate comprehensive reports** - Create standardized documentation of system capabilities and limitations
3. **Handle common WSL2/Linux caveats** - Address performance issues with Windows mounts and Git symlink problems
4. **Provide actionable recommendations** - Help developers optimize their development setup

## Key Features

- **Token-optimized prompt design** - Uses markdown headers instead of heavy fence syntax (~15% fewer tokens)
- **YAML-based configuration** - Centralized, easily editable system profile
- **Comprehensive tool inventory** - Checks for modern development tools (uv, uvx, gh, docker, etc.)
- **Performance benchmarking** - Tests I/O performance across different mount points
- **Network connectivity testing** - Verifies access to essential development services

## Use Case

This template is particularly useful for:

- **Development environment setup** - Quickly assess what's available on a new system
- **CI/CD environment profiling** - Document build environment capabilities
- **Cross-platform development** - Understand differences between WSL2, native Linux, and other environments
- **Performance troubleshooting** - Identify filesystem and network bottlenecks

## Files

- `env-probe.md` - The main system prompt template for LLM agents
- Generated: `env_report.md` - The output report (created when the prompt is executed)

## Usage

Drop the `env-probe.md` file into your LLM prompt and let the agent explore your environment systematically. The agent will generate a comprehensive report covering system facts, tool availability, performance metrics, and optimization recommendations.