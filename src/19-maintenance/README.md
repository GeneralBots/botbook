# Chapter 19: Maintenance and Updates

BotServer includes a complete stack of self-hosted services that power your bots. This chapter covers how to maintain, update, and troubleshoot these components.

## Stack Components Overview

BotServer automatically installs and manages these services:

| Component | Service | Default Port | Purpose |
|-----------|---------|--------------|---------|
| **vault** | HashiCorp Vault | 8200 | Secrets management |
| **tables** | PostgreSQL | 5432 | Primary database |
| **directory** | Zitadel | 8080 | Identity & access management |
| **drive** | MinIO | 9000, 9001 | Object storage (S3-compatible) |
| **cache** | Valkey | 6379 | In-memory cache (Redis-compatible) |
| **llm** | llama.cpp | 8081, 8082 | Local LLM & embedding server |
| **email** | Stalwart | 25, 993 | Mail server |
| **proxy** | Caddy | 443, 80 | HTTPS reverse proxy |
| **dns** | CoreDNS | 53 | Local DNS resolution |
| **alm** | Forgejo | 3000 | Git repository (ALM) |
| **alm_ci** | Forgejo Runner | - | CI/CD runner |
| **meeting** | LiveKit | 7880 | Video conferencing |

## Directory Structure

```
botserver-stack/
├── bin/           # Service binaries
│   ├── vault/
│   ├── tables/
│   ├── drive/
│   ├── cache/
│   ├── llm/
│   └── ...
├── conf/          # Configuration files
├── data/          # Persistent data
└── logs/          # Service logs

botserver-installers/    # Downloaded archives (cache)
```

## Why Self-Hosted?

1. **Privacy** - Data never leaves your infrastructure
2. **Offline** - Works without internet after initial setup
3. **Cost** - No per-user or API fees
4. **Control** - Full access to all services
5. **Compliance** - Meet data residency requirements

## Chapter Contents

- [Updating Components](./updating-components.md) - How to update individual services
- [Component Reference](./component-reference.md) - Detailed info for each component
- [Security Auditing](./security-auditing.md) - Running security audits
- [Backup and Recovery](./backup-recovery.md) - Data protection strategies
- [Troubleshooting](./troubleshooting.md) - Common issues and solutions

## Quick Commands

```bash
# Check service status
./botserver status

# View logs
tail -f botserver-stack/logs/llm.log

# Restart all services
./botserver restart

# Update a specific component
./botserver update llm
```

## Related Documentation

- [Installation](../01-introduction/installation.md) - Initial setup
- [Secrets Management](../08-config/secrets-management.md) - Vault configuration
- [LLM Configuration](../08-config/llm-config.md) - AI model settings