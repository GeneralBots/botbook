# BotBook Development Prompt Guide

**Version:** 6.1.0  
**Purpose:** LLM context for BotBook documentation development

---

## CRITICAL: Keyword Naming Rules

**Keywords NEVER use underscores. Always use spaces.**

### ✅ Correct Syntax
```basic
SEND MAIL to, subject, body, attachments
GENERATE PDF template, data, output
MERGE PDF files, output
DELETE "url"
DELETE "table", "filter"
ON ERROR RESUME NEXT
CLEAR ERROR
SET BOT MEMORY key, value
GET BOT MEMORY key
KB STATISTICS
KB DOCUMENTS COUNT
```

### ❌ WRONG - Never Use Underscores
```basic
SEND_MAIL          ' WRONG!
GENERATE_PDF       ' WRONG!
MERGE_PDF          ' WRONG!
DELETE_HTTP        ' WRONG!
SET_HEADER         ' WRONG!
```

### Keyword Mappings (Documentation to Implementation)
| Write This | NOT This |
|------------|----------|
| `SEND MAIL` | `SEND_MAIL` |
| `GENERATE PDF` | `GENERATE_PDF` |
| `MERGE PDF` | `MERGE_PDF` |
| `DELETE` | `DELETE_HTTP` |
| `SET HEADER` | `SET_HEADER` |
| `CLEAR HEADERS` | `CLEAR_HEADERS` |
| `GROUP BY` | `GROUP_BY` |
| `FOR EACH` | `FOR_EACH` |
| `EXIT FOR` | `EXIT_FOR` |
| `ON ERROR RESUME NEXT` | (no underscore version) |

### Special Keywords
- `GENERATE FROM TEMPLATE` = Use `FILL` keyword
- `GENERATE WITH PROMPT` = Use `LLM` keyword
- `DELETE` is unified - auto-detects HTTP URLs vs database tables vs files

---

## Official Icons - MANDATORY

**NEVER generate icons with LLM. ALWAYS use official SVG icons from `src/assets/icons/`.**

### Available Icons

| Icon | File | Usage |
|------|------|-------|
| Logo | `gb-logo.svg` | Main GB branding |
| Bot | `gb-bot.svg` | Bot/assistant representation |
| Analytics | `gb-analytics.svg` | Charts, metrics, dashboards |
| Calendar | `gb-calendar.svg` | Scheduling, events |
| Chat | `gb-chat.svg` | Conversations, messaging |
| Compliance | `gb-compliance.svg` | Security, auditing |
| Designer | `gb-designer.svg` | Workflow automation |
| Drive | `gb-drive.svg` | File storage, documents |
| Mail | `gb-mail.svg` | Email functionality |
| Meet | `gb-meet.svg` | Video conferencing |
| Paper | `gb-paper.svg` | Document editing |
| Research | `gb-research.svg` | Search, investigation |
| Sources | `gb-sources.svg` | Knowledge bases |
| Tasks | `gb-tasks.svg` | Task management |
| Chart | `gb-chart.svg` | Data visualization |
| Check | `gb-check.svg` | Success, completion |
| Database | `gb-database.svg` | Data storage |
| Folder | `gb-folder.svg` | File organization |
| Gear | `gb-gear.svg` | Settings |
| Globe | `gb-globe.svg` | Web, internet |
| Lightbulb | `gb-lightbulb.svg` | Ideas, tips |
| Lock | `gb-lock.svg` | Security |
| Note | `gb-note.svg` | Notes, comments |
| Package | `gb-package.svg` | Packages, modules |
| Palette | `gb-palette.svg` | Themes, styling |
| Rocket | `gb-rocket.svg` | Launch, deploy |
| Search | `gb-search.svg` | Search functionality |
| Signal | `gb-signal.svg` | Connectivity |
| Target | `gb-target.svg` | Goals, objectives |
| Tree | `gb-tree.svg` | Hierarchy, structure |
| Warning | `gb-warning.svg` | Alerts, cautions |

### Usage in Documentation

```markdown
<!-- Reference icons in docs -->
![Chat](../assets/icons/gb-chat.svg)

<!-- Or with HTML for sizing -->
<img src="../assets/icons/gb-analytics.svg" alt="Analytics" width="24">
```

### Icon Guidelines

- All icons use `stroke="currentColor"` for CSS theming
- ViewBox: `0 0 24 24`
- Stroke width: `1.5`
- Rounded line caps and joins
- Consistent with GB brand identity

**DO NOT:**
- Generate new icons with AI/LLM
- Use emoji or unicode symbols as icons
- Use external icon libraries (FontAwesome, etc.)
- Create inline SVG diagrams when an official icon exists

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

' Error handling
ON ERROR RESUME NEXT
result = SOME_OPERATION()
IF ERROR THEN
    TALK "Error: " + ERROR MESSAGE
END IF
ON ERROR GOTO 0

' Email - note: spaces not underscores
SEND MAIL "user@example.com", "Subject", "Body", []

' PDF generation - note: spaces not underscores  
GENERATE PDF "template.html", data, "output.pdf"

' Unified DELETE - auto-detects context
DELETE "https://api.example.com/resource/123"  ' HTTP DELETE
DELETE "customers", "status = 'inactive'"       ' Database DELETE
DELETE "temp/file.txt"                          ' File DELETE
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
| Error Handling | `botserver/src/basic/keywords/errors/` |

### Key Implementation Files
| Keyword Category | File |
|-----------------|------|
| `SEND MAIL`, `SEND TEMPLATE` | `send_mail.rs` |
| `GENERATE PDF`, `MERGE PDF` | `file_operations.rs` |
| `DELETE`, `INSERT`, `UPDATE` | `data_operations.rs` |
| `POST`, `PUT`, `GRAPHQL`, `SOAP` | `http_operations.rs` |
| `ON ERROR RESUME NEXT` | `errors/on_error.rs` |
| `KB STATISTICS`, `KB DOCUMENTS COUNT` | `kb_statistics.rs` |
| `LLM` | `llm_keyword.rs` |
| `FILL` (template filling) | `data_operations.rs` |

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
- [ ] **NO underscores in keyword names** (use spaces)
- [ ] Model names are generic or current (no gpt-4o, claude-3, etc.)
- [ ] Error handling uses `ON ERROR RESUME NEXT` pattern correctly

---

## Rules

- **Accuracy**: Must match botserver source code
- **Completeness**: No placeholder sections
- **Clarity**: Accessible to BASIC enthusiasts  
- **Version**: Always reference 6.1.0
- **Examples**: Only working, tested code
- **Structure**: Follow mdBook conventions
- **Keywords**: NEVER use underscores - always spaces
- **Models**: Use generic references or current model names
- **Errors**: Document `ON ERROR RESUME NEXT` for error handling

---

## Quick Reference: Implemented Keywords

### Error Handling
```basic
ON ERROR RESUME NEXT    ' Enable error trapping
ON ERROR GOTO 0         ' Disable error trapping
CLEAR ERROR             ' Clear error state
IF ERROR THEN           ' Check if error occurred
ERROR MESSAGE           ' Get last error message
ERR                     ' Get error number
THROW "message"         ' Raise an error
```

### HTTP Operations
```basic
POST "url", data
PUT "url", data  
PATCH "url", data
DELETE "url"            ' Unified - works for HTTP, DB, files
SET HEADER "name", "value"
CLEAR HEADERS
GRAPHQL "url", query, variables
SOAP "wsdl", "operation", params
```

### File & PDF Operations
```basic
READ "path"
WRITE "path", content
COPY "source", "dest"
MOVE "source", "dest"
LIST "path"
COMPRESS files, "archive.zip"
EXTRACT "archive.zip", "dest"
UPLOAD file
DOWNLOAD "url"
GENERATE PDF template, data, "output.pdf"
MERGE PDF files, "output.pdf"
```

### Data Operations
```basic
FIND "table", "filter"
SAVE "table", data
INSERT "table", data
UPDATE "table", data, "filter"
DELETE "table", "filter"
MERGE "table", data, "key"
FILL data, template           ' Template filling (was GENERATE FROM TEMPLATE)
MAP data, "mapping"
FILTER data, "condition"
AGGREGATE data, "operation"
```

### Knowledge Base
```basic
USE KB
USE KB "collection"
CLEAR KB
KB STATISTICS
KB COLLECTION STATS "name"
KB DOCUMENTS COUNT
KB DOCUMENTS ADDED SINCE days
KB LIST COLLECTIONS
KB STORAGE SIZE
```

### LLM Operations
```basic
result = LLM "prompt"         ' Generate with LLM (was GENERATE WITH PROMPT)
USE MODEL "model-name"
```

### Communication
```basic
TALK "message"
HEAR variable
SEND MAIL to, subject, body, attachments
SEND TEMPLATE recipients, template, variables
```