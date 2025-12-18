# CLI Reference

botserver provides a command-line interface for managing components, secrets, and services.

## General Usage

```bash
botserver <command> [options]
```

## Commands Overview

| Command | Description |
|---------|-------------|
| `install` | Install a component |
| `remove` | Remove a component |
| `list` | List all available components |
| `status` | Check component status |
| `start` | Start all installed components |
| `stop` | Stop all components |
| `restart` | Restart all components |
| `vault` | Manage secrets in HashiCorp Vault |

## Global Options

| Option | Description |
|--------|-------------|
| `--container` | Use LXC container mode instead of local installation |
| `--tenant <name>` | Specify tenant name (default: "default") |
| `--help`, `-h` | Show help information |

---

## Component Management

### Install a Component

```bash
botserver install <component> [--container] [--tenant <name>]
```

**Examples:**

```bash
# Install vault locally
botserver install vault

# Install vault in an LXC container with tenant name
botserver install vault --container --tenant pragmatismo

# Install vector database
botserver install vector_db --container --tenant pragmatismo
```

**Available Components:**

| Component | Description |
|-----------|-------------|
| `vault` | HashiCorp Vault - Secrets management |
| `tables` | PostgreSQL - Primary database |
| `cache` | Valkey - Redis-compatible cache |
| `drive` | MinIO - S3-compatible object storage |
| `llm` | llama.cpp - Local LLM server |
| `email` | Stalwart - Mail server |
| `proxy` | Caddy - HTTPS reverse proxy |
| `dns` | CoreDNS - DNS server |
| `directory` | Zitadel - Identity management |
| `alm` | Forgejo - Git repository |
| `alm_ci` | Forgejo Runner - CI/CD |
| `meeting` | LiveKit - Video conferencing |
| `vector_db` | Qdrant - Vector database |
| `timeseries_db` | InfluxDB - Time series database |
| `observability` | Vector - Log aggregation |

### Remove a Component

```bash
botserver remove <component> [--container] [--tenant <name>]
```

### List Components

```bash
botserver list [--container] [--tenant <name>]
```

Shows all available components and their installation status.

### Check Status

```bash
botserver status <component> [--container] [--tenant <name>]
```

---

## Service Control

### Start Services

```bash
botserver start [--container] [--tenant <name>]
```

Starts all installed components.

### Stop Services

```bash
botserver stop
```

Stops all running components.

### Restart Services

```bash
botserver restart [--container] [--tenant <name>]
```

---

## Vault Commands

The `vault` subcommand manages secrets stored in HashiCorp Vault.

### Prerequisites

Vault commands require these environment variables:

```bash
export VAULT_ADDR=http://<vault-ip>:8200
export VAULT_TOKEN=<your-vault-token>
```

### Migrate Secrets from .env

Migrates secrets from an existing `.env` file to Vault.

```bash
botserver vault migrate [env_file]
```

**Arguments:**

| Argument | Description | Default |
|----------|-------------|---------|
| `env_file` | Path to .env file | `.env` |

**Example:**

```bash
# Migrate from default .env
botserver vault migrate

# Migrate from specific file
botserver vault migrate /opt/gbo/bin/system/.env
```

**Migrated Secret Paths:**

| .env Variables | Vault Path |
|----------------|------------|
| `TABLES_*` | `gbo/tables` |
| `CUSTOM_*` | `gbo/custom` |
| `DRIVE_*` | `gbo/drive` |
| `EMAIL_*` | `gbo/email` |
| `STRIPE_*` | `gbo/stripe` |
| `AI_*`, `LLM_*` | `gbo/llm` |

After migration, your `.env` file only needs:

```env
RUST_LOG=info
VAULT_ADDR=http://<vault-ip>:8200
VAULT_TOKEN=<vault-token>
SERVER_HOST=0.0.0.0
SERVER_PORT=5858
```

### Store Secrets

Store key-value pairs at a Vault path.

```bash
botserver vault put <path> <key=value> [key=value...]
```

**Examples:**

```bash
# Store database credentials
botserver vault put gbo/tables host=localhost port=5432 username=postgres password=secret

# Store email configuration
botserver vault put gbo/email server=mail.example.com user=admin password=secret

# Store API keys
botserver vault put gbo/llm api_key=sk-xxx endpoint=https://api.openai.com
```

### Retrieve Secrets

Get secrets from a Vault path.

```bash
botserver vault get <path> [key]
```

**Examples:**

```bash
# Get all secrets at a path (values are masked)
botserver vault get gbo/tables

# Get a specific key value
botserver vault get gbo/tables password

# Get drive credentials
botserver vault get gbo/drive
```

**Output:**

```
Secrets at gbo/tables:
  host=localhost
  port=5432
  database=botserver
  username=gbuser
  password=67a6...
```

> **Note:** Sensitive values (password, secret, key, token) are automatically masked in output.

### List Secret Paths

Shows all configured secret paths.

```bash
botserver vault list
```

**Output:**

```
Configured secret paths:
  gbo/tables           - Database credentials
  gbo/drive            - S3/MinIO credentials
  gbo/cache            - Redis credentials
  gbo/email            - SMTP credentials
  gbo/directory        - Zitadel credentials
  gbo/llm              - AI API keys
  gbo/encryption       - Encryption keys
  gbo/meet             - LiveKit credentials
  gbo/alm              - Forgejo credentials
  gbo/vectordb         - Qdrant credentials
  gbo/observability    - InfluxDB credentials
  gbo/stripe           - Payment credentials
  gbo/custom           - Custom database
```

### Health Check

Check Vault connection status.

```bash
botserver vault health
```

**Output (success):**

```
* Vault is healthy
  Address: http://10.16.164.100:8200
```

**Output (failure):**

```
x Vault not configured
  Set VAULT_ADDR and VAULT_TOKEN environment variables
```

---

## Complete Setup Example

Here's a complete workflow to set up Vault and migrate secrets:

```bash
# 1. Install Vault in a container
botserver install vault --container --tenant pragmatismo

# 2. Install Vector DB for embeddings
botserver install vector_db --container --tenant pragmatismo

# 3. Get Vault container IP
lxc list pragmatismo-vault

# 4. Set environment variables
export VAULT_ADDR=http://<vault-ip>:8200
export VAULT_TOKEN=<root-token-from-init>

# 5. Migrate existing secrets
botserver vault migrate /opt/gbo/bin/system/.env

# 6. Verify migration
botserver vault health
botserver vault get gbo/tables
botserver vault get gbo/drive
botserver vault get gbo/email

# 7. Update .env to use Vault only
cat > /opt/gbo/bin/system/.env << EOF
RUST_LOG=info
VAULT_ADDR=http://<vault-ip>:8200
VAULT_TOKEN=<root-token>
SERVER_HOST=0.0.0.0
SERVER_PORT=5858
EOF

# 8. Restart botserver
botserver restart
```

---

## Secret Paths Reference

### gbo/tables

Database connection credentials.

| Key | Description |
|-----|-------------|
| `host` | Database server hostname |
| `port` | Database port |
| `database` | Database name |
| `username` | Database user |
| `password` | Database password |

### gbo/drive

S3/MinIO storage credentials.

| Key | Description |
|-----|-------------|
| `server` | Storage server hostname |
| `port` | Storage port |
| `use_ssl` | Enable SSL (`true`/`false`) |
| `accesskey` | Access key ID |
| `secret` | Secret access key |
| `org_prefix` | Organization prefix for buckets |

### gbo/email

SMTP email configuration.

| Key | Description |
|-----|-------------|
| `from` | Sender email address |
| `server` | SMTP server hostname |
| `port` | SMTP port |
| `username` | SMTP username |
| `password` | SMTP password |
| `reject_unauthorized` | Reject invalid certs |

### gbo/llm

AI/LLM configuration.

| Key | Description |
|-----|-------------|
| `api_key` | API key for cloud LLM |
| `model` | Model identifier |
| `endpoint` | API endpoint URL |
| `local` | Use local LLM (`true`/`false`) |
| `url` | Local LLM server URL |
| `model_path` | Path to local model file |
| `embedding_model_path` | Path to embedding model |
| `embedding_url` | Embedding server URL |

### gbo/stripe

Payment processing credentials.

| Key | Description |
|-----|-------------|
| `secret_key` | Stripe secret key |
| `professional_plan_price_id` | Professional plan price ID |
| `personal_plan_price_id` | Personal plan price ID |

### gbo/cache

Redis/Valkey credentials.

| Key | Description |
|-----|-------------|
| `password` | Cache password |

### gbo/directory

Zitadel identity provider.

| Key | Description |
|-----|-------------|
| `url` | Zitadel server URL |
| `project_id` | Project ID |
| `client_id` | OAuth client ID |
| `client_secret` | OAuth client secret |
| `masterkey` | Master encryption key |

### gbo/encryption

Encryption keys.

| Key | Description |
|-----|-------------|
| `master_key` | Master encryption key |

---

## Troubleshooting

### Vault Connection Issues

```bash
# Check if Vault is running
lxc exec pragmatismo-vault -- systemctl status vault

# Check Vault seal status
lxc exec pragmatismo-vault -- vault status

# Unseal Vault if sealed
lxc exec pragmatismo-vault -- vault operator unseal <unseal-key>
```

### Component Installation Fails

```bash
# Check logs
tail -f botserver-stack/logs/<component>.log

# Verify container exists
lxc list | grep <tenant>-<component>

# Check container logs
lxc exec <tenant>-<component> -- journalctl -xe
```

### Missing Dependencies

```bash
# Install system dependencies
sudo apt-get install -y libpq-dev libssl-dev liblzma-dev
```
