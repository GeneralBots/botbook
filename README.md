# General Bots

![General Bots Logo](https://github.com/GeneralBots/BotServer/blob/main/logo.png?raw=true)

**Enterprise-Grade LLM Orchestrator & AI Automation Platform**

A strongly-typed, self-hosted conversational platform focused on convention over configuration and code-less approaches.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         General Bots Platform                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                │
│   │   botapp    │    │   botui     │    │  botserver  │                │
│   │   (Tauri)   │───▶│  (Pure Web) │───▶│   (API)     │                │
│   │   Desktop   │    │  HTMX/HTML  │    │   Rust      │                │
│   └─────────────┘    └─────────────┘    └──────┬──────┘                │
│                                                 │                       │
│                                    ┌───────────┴───────────┐           │
│                                    │                       │           │
│                              ┌─────▼─────┐          ┌──────▼─────┐     │
│                              │  botlib   │          │  botbook   │     │
│                              │ (Shared)  │          │   (Docs)   │     │
│                              └───────────┘          └────────────┘     │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 📦 Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [**botserver**](https://github.com/GeneralBots/BotServer) | Core API server - LLM orchestration, automation, integrations | ✅ Production |
| [**botui**](https://github.com/GeneralBots/botui) | Pure web UI - HTMX-based interface (suite & minimal) | ✅ Production |
| [**botapp**](https://github.com/GeneralBots/botapp) | Tauri desktop wrapper - native file access, system tray | ✅ Production |
| [**botlib**](https://github.com/GeneralBots/botlib) | Shared Rust library - common types, HTTP client, utilities | ✅ Production |
| [**botbook**](https://github.com/GeneralBots/BotBook) | Documentation - mdBook format, multi-language | ✅ Production |

---

## 🚀 Quick Start

### Prerequisites

- **Rust** (latest stable) - [Install from rustup.rs](https://rustup.rs/)
- **Git** - [Download from git-scm.com](https://git-scm.com/downloads)

### Run the Server

```bash
# Clone and run
git clone https://github.com/GeneralBots/BotServer
cd BotServer
cargo run
```

On first run, BotServer automatically:
- Installs required components (PostgreSQL, S3 storage, Cache, LLM)
- Sets up database with migrations
- Downloads AI models
- Starts HTTP server at `http://127.0.0.1:8080`

### Run the Desktop App

```bash
# Clone botui (pure web)
git clone https://github.com/GeneralBots/botui
cd botui
cargo run  # Starts web server at :3000

# In another terminal, clone and run botapp (Tauri desktop)
git clone https://github.com/GeneralBots/botapp
cd botapp
cargo tauri dev
```

---

## ✨ Key Features

### 🤖 Multi-Vendor LLM API
Unified interface for OpenAI, Groq, Claude, Anthropic, and local models.

### 🔧 MCP + LLM Tools Generation
Instant tool creation from code and functions - no complex configurations.

### 💾 Semantic Caching
Intelligent response caching achieving **70% cost reduction** on LLM calls.

### 🌐 Web Automation Engine
Browser automation combined with AI intelligence for complex workflows.

### 📊 Enterprise Data Connectors
Native integrations with CRM, ERP, databases, and external services.

### 🔄 Git-like Version Control
Full history with rollback capabilities for all configurations and data.

---

## 🎯 4 Essential Keywords

General Bots provides a minimal, focused system:

```basic
USE KB "knowledge-base"    ' Load knowledge base into vector database
CLEAR KB "knowledge-base"  ' Remove KB from session
USE TOOL "tool-name"       ' Make tool available to LLM
CLEAR TOOLS                ' Remove all tools from session
```

---

## 🏛️ Architecture Details

### botserver (Core)
The main API server handling:
- LLM orchestration and prompt management
- Multi-channel communication (WhatsApp, Teams, Email, Web)
- File storage and drive management
- Task scheduling and automation
- Authentication and authorization

### botui (Web Interface)
Pure web UI with zero native dependencies:
- **Suite**: Full-featured multi-app interface
- **Minimal**: Lightweight single-page chat
- HTMX-powered for minimal JavaScript
- Works in any browser

### botapp (Desktop)
Tauri wrapper adding native capabilities:
- Local file system access
- System tray integration
- Native dialogs and notifications
- Desktop-specific features

### botlib (Shared Library)
Common Rust code shared across projects:
- HTTP client for BotServer communication
- Shared types and models
- Branding and configuration utilities
- Error handling

---

## 🔧 Development Setup

```bash
# Clone all repositories
git clone https://github.com/GeneralBots/BotServer botserver
git clone https://github.com/GeneralBots/botui
git clone https://github.com/GeneralBots/botapp
git clone https://github.com/GeneralBots/botlib
git clone https://github.com/GeneralBots/BotBook botbook

# Build all (from each directory)
cd botlib && cargo build
cd ../botserver && cargo build
cd ../botui && cargo build
cd ../botapp && cargo build
```

---

## 📖 Documentation

- **[Complete Documentation](https://github.com/GeneralBots/BotBook)** - Full mdBook documentation
- **[Quick Start Guide](https://github.com/GeneralBots/BotServer/blob/main/docs/QUICK_START.md)** - Get started in minutes
- **[API Reference](https://github.com/GeneralBots/BotServer/blob/main/docs/src/chapter-10-api/README.md)** - REST API documentation
- **[Architecture Guide](https://github.com/GeneralBots/BotServer/blob/main/docs/src/chapter-07-gbapp/README.md)** - System architecture

---

## 🆚 Why General Bots?

| vs. Alternative | General Bots Advantage |
|-----------------|----------------------|
| **ChatGPT/Claude** | Automates entire business processes, not just chat |
| **n8n/Make** | Simpler approach with minimal programming |
| **Microsoft 365** | User control, not locked ecosystems |
| **Salesforce** | Open-source AI orchestration connecting all systems |

---

## 🛡️ Security

- **AGPL-3.0 License** - True open source with contribution requirements
- **Self-hosted** - Your data stays on your infrastructure
- **Enterprise-grade** - 5+ years of stability
- **No vendor lock-in** - Open protocols and standards

Report security issues to: **security@pragmatismo.com.br**

---

## 🤝 Contributing

We welcome contributions! See our [Contributing Guidelines](https://github.com/GeneralBots/BotServer/blob/main/docs/src/chapter-13-community/README.md).

### Contributors

<a href="https://github.com/generalbots/botserver/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=generalbots/botserver" />
</a>

---

## 📄 License

General Bots is licensed under **AGPL-3.0**.

According to our dual licensing model, this program can be used either under the terms of the GNU Affero General Public License, version 3, or under a proprietary license.

Copyright (c) pragmatismo.com.br. All rights reserved.

---

## 🔗 Links

- **Website:** [pragmatismo.com.br](https://pragmatismo.com.br)
- **Documentation:** [docs.pragmatismo.com.br](https://docs.pragmatismo.com.br)
- **Stack Overflow:** Tag questions with `generalbots`
- **Video Tutorial:** [7 AI General Bots LLM Templates](https://www.youtube.com/watch?v=KJgvUPXi3Fw)

---

> **Code Name:** [Guaribas](https://en.wikipedia.org/wiki/Guaribas) (a city in Brazil, state of Piauí)
>
> *"No one should have to do work that can be done by a machine."* - Roberto Mangabeira Unger