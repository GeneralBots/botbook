# Vibe - AI-Powered Development Environment

Vibe is the autonomous coding mode that transforms your development workflow. Describe what you want to build, and AI agents create it automatically.

![Vibe Architecture](./assets/vibe/vibe-architecture.png)

---

## Quick Start

1. Click **Vibe** icon on desktop
2. Describe your project in the chat
3. Watch agents build, review, and deploy

```bash
# Example: Create an e-commerce app
"Build an e-commerce app for handmade crafts with shopping cart"
```

---

## Pipeline Stages

| Stage | Agent | Description |
|-------|-------|-------------|
| **PLAN** | Architect | Analyzes requirements, creates spec |
| **BUILD** | Developer | Generates code, creates database |
| **REVIEW** | Reviewer | Security scan, quality checks |
| **DEPLOY** | DevOps | Pushes to Forgejo, deploys |
| **MONITOR** | QA | Runs tests, validates |

---

## Features

### Monaco Editor
- Full IDE editing with syntax highlighting
- Multi-file workspace support
- File tree navigation

### Database UI
- Visual PostgreSQL schema browser
- SQL query editor
- Table relationship viewer

### Git Operations
- Branch management
- Commit history
- Pull/push to Forgejo

### Terminal
- Isolated LXC container per session
- Full shell access
- Persistent workspace

### Browser Automation
- Chromiumoxide integration
- Visual test runner
- Screenshot capture

### MCP Integration
- Connect external tools
- AI model integration
- Custom tool definitions

---

## BYOK (Bring Your Own Key)

Configure your own LLM API keys in **Sources → API Keys**:

- OpenAI
- Anthropic (Claude)
- Google Gemini
- Azure OpenAI
- OpenAI Compatible

---

## Use Cases

### 1. Rapid Prototyping
```bash
"Create a CRM with contacts, leads, and deal pipeline"
```

### 2. Full-Stack Apps
```bash
"Build an e-commerce store with cart, checkout, and Stripe payments"
```

### 3. Internal Tools
```bash
"Make an employee onboarding checklist app with approvals"
```

### 4. Data Dashboards
```bash
"Create a sales analytics dashboard with charts and exports"
```

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Vibe UI                              │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐    │
│  │  PLAN   │→ │  BUILD  │→ │ REVIEW  │→ │ DEPLOY  │    │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘    │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│               Orchestrator (5 Agents)                    │
│  Architect → Developer → Reviewer → QA → DevOps          │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                    BotServer                             │
│  - AppGenerator (code gen)                             │
│  - Database Manager                                    │
│  - File System                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+S` | Save file |
| `Ctrl+P` | Quick open |
| `Ctrl+Shift+P` | Command palette |
| `Ctrl+`` | Toggle terminal |

---

## Related Documentation

- [Vibe Terminal](./vibe-terminal.md) - Isolated container terminal
- [Vibe Editor](./vibe-editor.md) - Monaco editor guide
- [Vibe Database](./vibe-database.md) - Database UI
- [Vibe Git](./vibe-git.md) - Git operations
- [Vibe MCP](./vibe-mcp.md) - MCP integrations
- [Designer](./designer.md) - Visual app editor
- [App Generation](./app-generation.md) - Code generation
