# Chapter 12: Authentication & Security

User authentication, permission management, and resource protection for botserver.

## Overview

botserver provides enterprise-grade security with flexible authentication options, granular permissions, and comprehensive rate limiting to prevent abuse.

## Initial Setup

When General Bots starts for the first time, it automatically creates an administrator account and displays the credentials in the console. See [Initial Setup & Bootstrap](./initial-setup.md) for details.

```
╔════════════════════════════════════════════════════════════╗
║       🤖 GENERAL BOTS - INITIAL SETUP COMPLETE            ║
╠════════════════════════════════════════════════════════════╣
║  Username:             admin                               ║
║  Email:                admin@localhost                     ║
║  Password:             (displayed in console)              ║
╚════════════════════════════════════════════════════════════╝
```

> **Important**: Save the password shown in your console during first startup. It will not be displayed again.

## Authentication Methods

| Method | Use Case |
|--------|----------|
| **Session Token** | Web/API access |
| **OAuth2/OIDC** | SSO integration via Zitadel |
| **API Key** | Service accounts |
| **Bot Auth** | Bot-to-bot communication |

## Quick Start

```basic
' Check if user is authenticated
IF user.authenticated THEN
  TALK "Welcome, " + user.name
ELSE
  TALK "Please log in first"
END IF
```

## Security Features

- **Directory Service**: Zitadel handles all user identity management
- **No Password Storage**: Passwords never stored in General Bots
- **Session Management**: Cryptographic tokens, configurable expiry
- **Rate Limiting**: Per-user and global limits with HTTP 429 responses
- **System Limits**: Loop protection, file size limits, resource constraints
- **Audit Logging**: Track all authentication events
- **Organizations**: Multi-tenant support with org-based isolation

## Permission Levels

| Level | Access |
|-------|--------|
| `admin` | Full system access, user management |
| `org_owner` | Organization management |
| `bot_owner` | Bot configuration and deployment |
| `bot_operator` | Bot operation and monitoring |
| `user` | Standard access |
| `guest` | Read-only, anonymous chat |

## Organization Structure

```
Organization (e.g., "Acme Corp")
├── Users (with roles)
├── Bots (owned by org)
│   ├── sales-bot
│   └── support-bot
└── Drive Storage
    ├── acme-sales-bot.gbai/
    └── acme-support-bot.gbai/
```

## Configuration

```csv
name,value
auth-session-ttl,3600
auth-max-attempts,5
auth-lockout-duration,900
```

## Chapter Contents

- [Initial Setup & Bootstrap](./initial-setup.md) - First-time admin setup
- [User Authentication](./user-auth.md) - Login flows
- [Password Security](./password-security.md) - Password policies
- [API Endpoints](./api-endpoints.md) - Auth API reference
- [Bot Authentication](./bot-auth.md) - Service accounts
- [Security Features](./security-features.md) - Protection mechanisms
- [Security Policy](./security-policy.md) - Best practices
- [Compliance Requirements](./compliance-requirements.md) - GDPR, LGPD, HIPAA
- [Permissions Matrix](./permissions-matrix.md) - Access control
- [User vs System Context](./user-system-context.md) - Execution contexts
- [System Limits & Rate Limiting](./system-limits.md) - Resource constraints and abuse prevention

## Anonymous Chat Access

Anonymous users can use the chat functionality without logging in. The system automatically creates temporary sessions for anonymous users. Authentication is only required for:

- User management (Settings)
- Bot configuration
- Administrative functions
- Organization management

## See Also

- [REST API](../10-rest/README.md) - API authentication
- [Configuration](../08-config/README.md) - Auth settings