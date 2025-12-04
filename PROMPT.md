# BotBook Development Prompt Guide

**Version:** 6.1.0  
**Purpose:** LLM context for BotBook documentation development

---

## Project Overview

BotBook is the **mdBook-based documentation** for the General Bots platform. It provides comprehensive guides, tutorials, and API references for users and developers.

### Workspace Position

```
botbook/       # THIS PROJECT - Documentation
botserver/     # Main server (source of truth)
botlib/        # Shared library
botui/         # Web/Desktop UI
botapp/        # Desktop app
botmodels/     # Data models visualization
botplugin/     # Browser extension
```

### What BotBook Provides

- **User Guides**: Getting started, installation, quick start
- **BASIC Reference**: Keywords, syntax, examples
- **API Documentation**: REST endpoints, WebSocket
- **Configuration**: Settings, environment variables
- **Architecture**: System design, components

---

## Structure

```
botbook/
├── book.toml          # mdBook configuration
├── src/
│   ├── SUMMARY.md     # Table of contents
│   ├── README.md      # Introduction
│   ├── chapter-01/    # Run and Talk (Quick Start)
│   ├── chapter-02/    # Package System
│   ├── chapter-03/    # Knowledge Base
│   ├── chapter-04-gbui/   # UI System
│   ├── chapter-05-gbtheme/ # Theming
│   ├── chapter-06-gbdialog/ # BASIC Dialogs
│   ├── chapter-07-gbapp/   # Applications
│   ├── chapter-08-config/  # Configuration
│   ├── chapter-09-api/     # REST API
│   ├── chapter-10-api/     # WebSocket API
│   ├── chapter-11-features/ # Feature Modules
│   ├── chapter-12-auth/    # Authentication
│   ├── chapter-13-community/ # Contributing
│   ├── chapter-14-migration/ # Migration Guide
│   ├── appendix-*/         # Reference materials
│   └── assets/             # Images, diagrams
├── i18n/              # Translations
│   ├── src-cn/        # Chinese
│   ├── src-ja/        # Japanese
│   └── src-pt/        # Portuguese
└── book/              # Generated output
```

---

## Documentation Rules

### CRITICAL REQUIREMENTS

```
- All documentation MUST match actual source code
- Extract real keywords from botserver/src/basic/keywords/
- Reference real models from botserver/src/shared/models.rs
- Use actual examples from botserver/templates/
- Version numbers must be 6.1.0
- No placeholder content - only verified features
```

### Writing Style

```
- Beginner-friendly, instructional tone
- Practical examples that work
- Step-by-step instructions
- Clear headings and structure
- Use mdBook admonitions for tips/warnings
```

### Code Examples

```markdown
<!-- For BASIC examples -->
```bas
TALK "Hello, world!"
name = HEAR
TALK "Welcome, " + name
```

<!-- For configuration -->
```csv
name,value
server_port,8080
llm-url,http://localhost:8081
```

<!-- For Rust (only in gbapp chapter) -->
```rust
use botlib::prelude::*;
```
```

---

## Building Documentation

```bash
# Install mdBook
cargo install mdbook

# Build documentation
cd botbook
mdbook build

# Serve locally with hot reload
mdbook serve --open

# Build specific language
mdbook build --dest-dir book-pt src-pt
```

---

## Chapter Content Guidelines

### Chapter 1: Run and Talk
- Quick start (5 minutes to running bot)
- Bootstrap process explanation
- First conversation walkthrough
- Session management basics

### Chapter 2: Package System
- .gbai folder structure
- .gbot configuration
- .gbdialog scripts
- .gbkb knowledge bases
- .gbtheme customization

### Chapter 6: BASIC Dialogs
- Keyword reference (from source)
- TALK, HEAR, SET, GET
- Control flow (IF, FOR, WHILE)
- Tool creation
- LLM integration

### Chapter 8: Configuration
- config.csv format
- Environment variables
- Database configuration
- Service settings

---

## Source Code References

When documenting features, verify against actual source:

| Topic | Source Location |
|-------|-----------------|
| BASIC Keywords | `botserver/src/basic/keywords/` |
| Database Models | `botserver/src/shared/models.rs` |
| API Routes | `botserver/src/core/urls.rs` |
| Configuration | `botserver/src/core/config/` |
| Bootstrap | `botserver/src/core/bootstrap/` |
| Templates | `botserver/templates/` |

---

## Diagram Guidelines

For SVG diagrams in `src/assets/`:

```
- Transparent background
- Dual-theme support (light/dark CSS)
- Width: 1040-1400px
- Font: Arial, sans-serif
- Colors: Blue #4A90E2, Orange #F5A623, Purple #BD10E0, Green #7ED321
```

---

## Translation Workflow

1. English is source of truth (`src/`)
2. Translations in `src-{lang}/`
3. Keep structure identical
4. Update `book.toml` for each language
5. Build separately per language

---

## Quality Checklist

Before committing documentation:

- [ ] All code examples tested and working
- [ ] Version numbers are 6.1.0
- [ ] Links are valid (relative paths)
- [ ] Images have alt text
- [ ] SUMMARY.md is updated
- [ ] mdbook build succeeds without errors
- [ ] Content matches actual source code

---

## Rules

- **Accuracy**: Must match botserver source code
- **Completeness**: No placeholder sections
- **Clarity**: Accessible to BASIC enthusiasts  
- **Version**: Always reference 6.1.0
- **Examples**: Only working, tested code
- **Structure**: Follow mdBook conventions