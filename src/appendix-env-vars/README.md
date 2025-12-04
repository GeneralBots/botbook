# Appendix C: Environment Variables

General Bots uses a **minimal set of environment variables**. All configuration is managed through `config.csv` files within each bot's `.gbot` folder, with secrets stored securely in Vault.

## Required Environment Variables

Only Vault-related environment variables are required by General Bots:

| Variable | Description | Example |
|----------|-------------|---------|
| `VAULT_ADDR` | Vault server URL | `http://localhost:8200` |
| `VAULT_TOKEN` | Authentication token | Auto-generated during bootstrap |
| `VAULT_NAMESPACE` | Vault namespace (optional) | `admin` |

## Setting Environment Variables

### Linux/macOS

```botbook/src/appendix-env-vars/example.sh#L1-2
export VAULT_ADDR=http://localhost:8200
export VAULT_TOKEN=hvs.your-vault-token
```

### Systemd Service

```botbook/src/appendix-env-vars/example.service#L1-3
[Service]
Environment="VAULT_ADDR=http://localhost:8200"
Environment="VAULT_TOKEN=hvs.your-vault-token"
```

### LXC Container

```botbook/src/appendix-env-vars/example-lxc.sh#L1-2
lxc config set container-name environment.VAULT_ADDR="http://localhost:8200"
lxc config set container-name environment.VAULT_TOKEN="hvs.your-vault-token"
```

## Auto-Managed Services

The following services are **automatically configured through Vault** during bootstrap:

| Service | Management |
|---------|------------|
| PostgreSQL | Connection credentials stored in Vault |
| S3-Compatible Storage | Access keys stored in Vault |
| Cache | Connection managed via Vault |
| Email (Stalwart) | Credentials stored in Vault |
| LLM API Keys | Stored in Vault |

You do **not** need environment variables for these services. Vault handles credential distribution and rotation automatically.

## Everything Else Goes in config.csv

**All application configuration belongs in `config.csv`**, not environment variables:

| Configuration | Where to Configure |
|--------------|-------------------|
| LLM provider/model | `config.csv`: `llm-url`, `llm-model` |
| Email settings | `config.csv`: `email-*` |
| Channel tokens | `config.csv`: `whatsapp-*`, `telegram-*`, etc. |
| Bot settings | `config.csv`: all bot-specific settings |
| Feature flags | `config.csv`: various keys |
| Theme settings | `config.csv`: `theme-*` |
| Server port | `config.csv`: `server_port` |

### Example config.csv

```botbook/src/appendix-env-vars/example-config.csv#L1-8
name,value
llm-url,http://localhost:8081
llm-model,model.gguf
server_port,8080
theme-color1,#0d2b55
whatsapp-business-id,your-business-id
admin-email,admin@example.com
```

## Configuration Philosophy

General Bots follows these principles:

1. **Vault-First** — All secrets are managed by Vault
2. **Minimal Environment** — Only Vault address and token use environment variables
3. **config.csv for Settings** — All application configuration is in `config.csv`
4. **Per-Bot Configuration** — Each bot has its own `config.csv` in its `.gbot` folder
5. **No Hardcoded Secrets** — Never store secrets in code or config files

## Bootstrap Process

During bootstrap, General Bots:

1. Connects to Vault using `VAULT_*` variables
2. Retrieves or generates credentials for all managed services
3. Configures database, storage, cache, and other services
4. Stores service credentials securely in Vault

This eliminates the need for manual credential management.

## Security Notes

1. **Never commit tokens** — Use `.env` files (gitignored) or secrets management
2. **Rotate regularly** — Vault tokens should be rotated periodically
3. **Limit access** — Only the botserver process needs these variables
4. **Use TLS** — Always use HTTPS for Vault in production

## Troubleshooting

### Vault Connection Failed

```
Error: Failed to connect to Vault
```

Verify:
- `VAULT_ADDR` is set correctly
- Vault server is running and accessible
- `VAULT_TOKEN` is valid and not expired
- Network allows connection to Vault host

### Service Not Available

If a managed service (database, storage, cache) is unavailable:

1. Check Vault is running and unsealed
2. Verify secrets exist in Vault at expected paths
3. Check service container/process status
4. Review logs for connection errors

## See Also

- [config.csv Format](../chapter-08-config/config-csv.md) — Bot configuration reference
- [Secrets Management](../chapter-08-config/secrets-management.md) — Vault integration details
- [Drive Integration](../chapter-08-config/drive.md) — Storage setup
- [Authentication](../chapter-12-auth/README.md) — Security features