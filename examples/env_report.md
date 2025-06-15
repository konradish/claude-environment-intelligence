# Environment Report

Generated: 2025-06-14 20:29 UTC

## 🔍 Key Findings (Debian bookworm on WSL2)

- **Storage Performance**: ext4 writes: 5.5 GB/s ⟂ 9P writes: 77 MB/s → ❗ **71× slowdown on /mnt/c**
- **Missing Tools**: direnv, yt-dlp → consider installing for workflow optimization  
- **SSH Issues**: Host-key check failing → set up ssh-askpass for proper Git workflows
- **Optimal Strategy**: Use `~/` (ext4) for I/O-heavy operations, avoid `/mnt/c` for performance-critical tasks

---

## System Table

| Property | Value |
|----------|-------|
| **Kernel** | Linux 5.15.167.4-microsoft-standard-WSL2 |
| **Architecture** | x86_64 GNU/Linux |
| **Distribution** | Debian GNU/Linux 12 (bookworm) |
| **Host Kind** | WSL2 |
| **Hostname** | dev-machine |

## Filesystem Diagram

```
/ (ext4, 1007G, 2% used)           # Root filesystem
├── /mnt/c (9P, 3.7T, 43% used)    # Windows C: drive
├── /mnt/d (9P, 1.9T, 91% used)    # Windows D: drive  
├── /mnt/e (9P, 954G, 93% used)    # Windows E: drive
├── /mnt/f (9P, 3.7T, 69% used)    # Windows F: drive
└── ~/projects -> /mnt/c/projects   # Symlink to Windows projects
```

## Tool Matrix

| Tool | Status | Version | Auth Status |
|------|--------|---------|-------------|
| **gh** | ✅ | 2.73.0 | ✅ Authenticated (user) |
| **wrangler** | ✅ | 4.16.1 | ✅ Authenticated (user@example.com) |
| **uv** | ✅ | 0.7.6 | N/A |
| **uvx** | ✅ | 0.7.6 | N/A |
| **npx** | ✅ | 11.4.1 | N/A |
| **docker** | ✅ | 28.1.1 | N/A |
| **docker-compose** | ✅ | v2.35.1-desktop.1 | N/A |
| **direnv** | ❌ | Not installed | N/A |
| **jq** | ✅ | 1.6 | N/A |
| **yt-dlp** | ❌ | Not installed | N/A |
| **sgpt** | ✅ | 1.4.5 (via uvx) | N/A |
| **aider** | ✅ | 0.84.0 | N/A |
| **repomix** | ✅ | 0.3.8 | N/A |

## Metrics & Timestamps

### Performance Benchmarks
- **ext4 (/tmp)**: 5.5 GB/s write speed
- **9P (/mnt/c)**: 77.0 MB/s write speed
- **Performance Ratio**: ext4 is ~71x faster than 9P

### Network Connectivity
- **GitHub SSH**: ❌ Host key verification failed (no ssh-askpass)
- **Cloudflare API**: ✅ Reachable (301 redirect to developers.cloudflare.com)

### System Resources
- **Root Disk**: 1007G total, 11G used (2%)
- **Memory**: 16G available for WSL processes
- **Docker**: Running with desktop integration

## Recommendations

### Performance Optimization
1. **Use ext4 for I/O intensive operations**: The native Linux filesystem is ~71x faster than the 9P mount
2. **Prefer `~/` over `~/projects/`** for temporary work requiring heavy disk I/O
3. **Use `/tmp` for scratch space** rather than Windows-mounted directories

### Git Operations
1. **Avoid using `~/projects` symlink as cwd** for git operations - use real path `/mnt/c/projects` instead
2. **SSH key setup needed**: Host key verification is failing for GitHub SSH access
3. **HTTPS git operations work** via GitHub CLI authentication

### Missing Tools
- **direnv**: Consider installing for per-directory environment management
- **yt-dlp**: Consider installing if media downloading is needed
- **ssh-askpass**: Install for proper SSH key handling

### Network & Auth Status
- ✅ GitHub CLI fully authenticated with comprehensive scopes
- ✅ Wrangler authenticated with full Cloudflare access
- ⚠️ SSH access to GitHub requires key setup
- ✅ Internet connectivity confirmed via API endpoints