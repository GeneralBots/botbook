# botbook Development Prompt Guide

**Version:** 6.1.0  
**Purpose:** LLM context for botbook documentation development

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

botbook is the **mdBook-based documentation** for the General Bots platform. It provides comprehensive guides, tutorials, and API references for users and developers.

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

### What botbook Provides

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
│   ├── 01-introduction/   # Run and Talk (Quick Start)
│   ├── 02-templates/      # Package System
│   ├── 03-knowledge-base/ # Knowledge Base
│   ├── 04-gbui/           # UI System
│   ├── 05-gbtheme/        # Theming
│   ├── 06-gbdialog/       # BASIC Dialogs
│   ├── 07-gbapp/          # Applications
│   ├── 08-config/         # Configuration
│   ├── 09-tools/          # Tools
│   ├── 10-rest/           # REST API
│   ├── 11-features/       # Feature Modules
│   ├── 12-auth/           # Authentication
│   ├── 13-community/      # Contributing
│   ├── 14-migration/      # Migration Guide
│   ├── 15-appendix/       # Reference materials
│   ├── 16-appendix-docs-style/
│   ├── 17-testing/        # Testing guide
│   ├── 18-appendix-external-services/
│   ├── 19-maintenance/    # Maintenance
│   └── assets/            # Images, diagrams
├── i18n/              # Translations
│   ├── cn/            # Chinese
│   ├── en/            # English
│   ├── ja/            # Japanese
│   └── pt/            # Portuguese
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

## NO ASCII DIAGRAMS — MANDATORY

**NEVER use ASCII art diagrams in documentation. ALL diagrams must be SVG.**

### Prohibited ASCII Patterns

```
❌ NEVER USE:
┌─────────┐    ╔═══════╗    +-------+
│  Box    │    ║ Box   ║    | Box   |
└─────────┘    ╚═══════╝    +-------+

├── folder/    │           →    ▶    ──►
│   └── file   ▼           ←    ◀    ◄──
```

### What to Use Instead

| Instead of... | Use... |
|---------------|--------|
| ASCII box diagrams | SVG diagrams in `assets/` |
| ASCII flow charts | SVG with arrows and boxes |
| ASCII directory trees | Markdown tables or SVG |
| ASCII tables with borders | Markdown tables |
| ASCII progress indicators | SVG or text description |

### Directory Trees → Tables

```markdown
❌ WRONG:
mybot.gbai/
├── mybot.gbdialog/
│   └── start.bas
└── mybot.gbot/
    └── config.csv

✅ CORRECT:
| Path | Description |
|------|-------------|
| `mybot.gbai/` | Root package |
| `mybot.gbdialog/` | BASIC scripts |
| `mybot.gbdialog/start.bas` | Entry point |
| `mybot.gbot/` | Configuration |
| `mybot.gbot/config.csv` | Bot settings |
```

### Rationale

- ASCII breaks in different fonts/editors
- Not accessible for screen readers
- Cannot adapt to dark/light themes
- Looks unprofessional in modern docs
- SVGs scale perfectly at any size

---

## SVG Diagram Guidelines — Theme Transparency

All SVG diagrams MUST be theme-agnostic and work with light/dark modes.

### Required Structure

Every SVG must include:

1. **CSS classes for text** (not hardcoded colors)
2. **Dark mode media query** in `<style>` block
3. **Standard gradient definitions** in `<defs>`

### Required CSS Block

```xml
<style>
  .title-text { fill: #1E1B4B; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }
  .main-text { fill: #334155; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }
  .secondary-text { fill: #64748B; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }
  .white-text { fill: #FFFFFF; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }
  .mono-text { fill: #475569; font-family: 'SF Mono', 'Fira Code', Consolas, monospace; }

  @media (prefers-color-scheme: dark) {
    .title-text { fill: #F1F5F9; }
    .main-text { fill: #E2E8F0; }
    .secondary-text { fill: #94A3B8; }
    .mono-text { fill: #CBD5E1; }
  }
</style>
```

### Standard Gradients (use these IDs)

| Gradient ID | Colors | Purpose |
|-------------|--------|---------|
| `primaryGrad` | `#6366F1` → `#8B5CF6` | Primary/purple elements |
| `cyanGrad` | `#06B6D4` → `#0EA5E9` | Cyan/info elements |
| `greenGrad` | `#10B981` → `#34D399` | Success/green elements |
| `orangeGrad` | `#F59E0B` → `#FBBF24` | Warning/orange elements |

### Background Rules

- Use `fill="#FAFBFC"` for main background (not pure white)
- Add dot pattern overlay: `fill="url(#dots)"` with `opacity="0.08"`
- Cards use `fill="#FFFFFF"` with `stroke="#E2E8F0"` for definition
- Use `filter="url(#cardShadow)"` for card depth

### DO NOT

- ❌ Hardcode text colors without CSS class
- ❌ Use pure black (`#000000`) for text
- ❌ Forget the `@media (prefers-color-scheme: dark)` block
- ❌ Create new gradient IDs when standard ones exist
- ❌ Use ASCII art diagrams when SVG is appropriate

### DO

- ✅ Use CSS classes for ALL text elements
- ✅ Include dark mode media query in every SVG
- ✅ Use standard gradient IDs consistently
- ✅ Test SVGs in both light and dark browser modes
- ✅ Convert ASCII diagrams to proper SVGs
- ✅ Place SVGs in `src/assets/chapter-XX/` directories

### Dimensions

- Width: 600-1200px (responsive)
- Use `style="max-width: 100%; height: auto;"` when embedding

### Reference

See `src/16-appendix-docs-style/svg.md` for complete guidelines.

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

---

## Conversation Examples (WhatsApp Style)

All conversation examples throughout the book use the WhatsApp-style HTML format. This provides a familiar, visually consistent representation of bot interactions.

### Standard Format

```html
<div class="wa-chat">
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>User message goes here</p>
      <div class="wa-time">10:30</div>
    </div>
  </div>
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>Bot response goes here</p>
      <div class="wa-time">10:30</div>
    </div>
  </div>
</div>
```

### Message Classes

| Class | Usage |
|-------|-------|
| `wa-chat` | Container for the conversation |
| `wa-message` | Individual message wrapper |
| `wa-message user` | User message (right-aligned, colored) |
| `wa-message bot` | Bot message (left-aligned) |
| `wa-bubble` | Message bubble with styling |
| `wa-time` | Timestamp display |

### Formatting Guidelines

1. **User messages** — Use `wa-message user` class
2. **Bot messages** — Use `wa-message bot` class
3. **Timestamps** — Include `wa-time` div with realistic times
4. **Multi-line responses** — Use separate `<p>` tags for each line
5. **Status indicators** — Use text indicators (Success, Error, etc.) not emojis
6. **Bold text** — Use `<strong>` for emphasis
7. **Attachments** — Indicate with text like "[Attachment: filename.pdf]"

### Complete Example

```html
<div class="wa-chat">
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>Hello! How can I help you today?</p>
      <div class="wa-time">10:30</div>
    </div>
  </div>
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>I want to enroll in computer science</p>
      <div class="wa-time">10:31</div>
    </div>
  </div>
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>I'll help you enroll! What's your name?</p>
      <div class="wa-time">10:31</div>
    </div>
  </div>
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>Sarah Chen</p>
      <div class="wa-time">10:31</div>
    </div>
  </div>
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p><strong>Success:</strong> Welcome to Computer Science, Sarah!</p>
      <p>Your enrollment ID is: ENR-2025-0142</p>
      <div class="wa-time">10:31</div>
    </div>
  </div>
</div>
```

### When to Use Each Format

| Content Type | Format |
|--------------|--------|
| Interface screenshots | SVG wireframe |
| System architecture | SVG diagram |
| Data flow diagrams | SVG diagram |
| Bot conversations | WhatsApp HTML |
| API examples | Code blocks |
| Configuration | Code blocks |

The WhatsApp chat styling is defined in `src/whatsapp-chat.css` and automatically included in the book build.
