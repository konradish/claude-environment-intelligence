# Environment Discovery and Report

Systematically discover and report environment capabilities, creating `env_report.md`.

## Discovery Process

**A. OS/Kernel Information**
- `uname -a` - system information
- `cat /etc/os-release` - distribution details

**B. Mount Points & Storage**
- `mount | grep '^/dev'` - mounted filesystems
- Verify key symlinks (~/projects, etc.)

**C. Tool Inventory**
- Check for: `gh`, `wrangler`, `uv`, `uvx`, `npx`, `docker`, `direnv`, `jq`, `sgpt`, `aider`, `repomix`
- For each tool: `which <tool> && <tool> --version`
- Verify authentication status where applicable

**D. Network Connectivity**
- `curl --head api.github.com` - GitHub API access
- `curl --head api.cloudflare.com` - Cloudflare API access
- Record response times

**E. Performance Testing**
- `dd` write tests: `/tmp` vs `/mnt/c/temp`
- Compare ext4 vs 9P filesystem performance

## Output Format

Generate `env_report.md` with:
```
OS: <distro> <version> <kernel>
Mounts: <key_mounts>
Tools: <name>:<version>:<status> (✓/✗/⚠)  
Network: <service>:<latency>ms
Perf: /tmp:<speed>MB/s /mnt/c:<speed>MB/s
Caveats: git-symlink-fail, 9p-slow-io
```

## Execution Rules
- Read-only operation unless explicitly instructed
- Rate limit network calls (reasonable intervals)
- Retry failed commands 2x, skip if missing
- No secrets or sensitive data in output
- Known limitations: `/mnt/c` slower than ext4, Git fails on `~/projects` symlink