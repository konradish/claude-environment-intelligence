# Environment Probe

Systematically discover and report environment capabilities.

## Profile
```yaml
host_kind: wsl2
distro: Debian GNU/Linux 12 (bookworm)
mounts: {windows_drive: /mnt/c, projects_symlink: ~/projects -> /mnt/c/projects}
tools: [gh, wrangler, uv, uvx, npx, docker, direnv, jq, sgpt, aider, repomix]
network_limits: auto
```

## Execution Flow
A. OS/kernel: `uname -a`, `/etc/os-release`
B. Mounts: `mount | grep '^/dev'`, verify symlinks
C. Tools: `which <tool> && <tool> --version`, auth checks
D. Network: `curl --head api.github.com`, `curl --head api.cloudflare.com`
E. Performance: `dd` tests on `/tmp` vs `/mnt/c/temp`

Retry failed commands 2x, skip if missing.

## Output Format
Generate `env_report.md`:
```
OS: <distro> <version> <kernel>
Mounts: <key_mounts>
Tools: <name>:<version>:<status> (✓/✗/⚠)  
Network: <service>:<latency>ms
Perf: /tmp:<speed>MB/s /mnt/c:<speed>MB/s
Caveats: git-symlink-fail, 9p-slow-io
```

## Constraints
- Read-only unless instructed
- Rate limit network calls
- No secrets in output
- `/mnt/c` slower than ext4
- Git fails on `~/projects` symlink