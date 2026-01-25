# botbook Development Guide

**Version:** 6.2.0  
**Purpose:** Documentation for General Bots (mdBook)

---

## 📚 CRITICAL: Keyword Naming Rules

**Keywords NEVER use underscores. Always use spaces.**

### ✅ Correct Syntax
```basic
SEND MAIL to, subject, body, attachments
GENERATE PDF template, data, output
MERGE PDF files, output
DELETE "url"
ON ERROR RESUME NEXT
SET BOT MEMORY key, value
KB STATISTICS
```

### ❌ WRONG - Never Use Underscores
```basic
SEND_MAIL          ' WRONG!
GENERATE_PDF       ' WRONG!
DELETE_HTTP        ' WRONG!
```

### Keyword Mappings
| Write This | NOT This |
|------------|----------|
| `SEND MAIL` | `SEND_MAIL` |
| `GENERATE PDF` | `GENERATE_PDF` |
| `MERGE PDF` | `MERGE_PDF` |
| `DELETE` | `DELETE_HTTP` |
| `SET HEADER` | `SET_HEADER` |
| `FOR EACH` | `FOR_EACH` |

---

## 🎨 OFFICIAL ICONS - MANDATORY

**NEVER generate icons with LLM. Use official SVG icons from `botui/ui/suite/assets/icons/`**

### Usage in Documentation

```markdown
<!-- Reference icons in docs -->
![Chat](../assets/icons/gb-chat.svg)

<!-- With HTML for sizing -->
<img src="../assets/icons/gb-analytics.svg" alt="Analytics" width="24">
```

---

## 📁 STRUCTURE

```
botbook/
├── book.toml          # mdBook configuration
├── src/
│   ├── SUMMARY.md     # Table of contents
│   ├── README.md      # Introduction
│   ├── 01-introduction/   # Quick Start
│   ├── 02-templates/      # Package System
│   ├── 03-knowledge-base/ # Knowledge Base
│   ├── 06-gbdialog/       # BASIC Dialogs
│   ├── 08-config/         # Configuration
│   ├── 10-rest/           # REST API
│   └── assets/            # Images, diagrams
├── i18n/              # Translations
└── book/              # Generated output
```

---

## 📖 DOCUMENTATION RULES

```
- All documentation MUST match actual source code
- Extract real keywords from botserver/src/basic/keywords/
- Use actual examples from botserver/templates/
- Version numbers must be 6.2.0
- No placeholder content - only verified features
```

---

## 🚫 NO ASCII DIAGRAMS — MANDATORY

**NEVER use ASCII art diagrams. ALL diagrams must be SVG.**

### ❌ Prohibited ASCII Patterns
```
┌─────────┐    ╔═══════╗    +-------+
│  Box    │    ║ Box   ║    | Box   |
└─────────┘    ╚═══════╝    +-------+
```

### ✅ What to Use Instead

| Instead of... | Use... |
|---------------|--------|
| ASCII box diagrams | SVG diagrams in `assets/` |
| ASCII flow charts | SVG with arrows and boxes |
| ASCII directory trees | Markdown tables |

---

## 🎨 SVG DIAGRAM GUIDELINES

All SVGs must support light/dark modes:

```xml
<style>
  .title-text { fill: #1E1B4B; }
  .main-text { fill: #334155; }
  
  @media (prefers-color-scheme: dark) {
    .title-text { fill: #F1F5F9; }
    .main-text { fill: #E2E8F0; }
  }
</style>
```

---

## 💬 CONVERSATION EXAMPLES

Use WhatsApp-style HTML format for bot interactions:

```html
<div class="wa-chat">
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>Hello! How can I help?</p>
      <div class="wa-time">10:30</div>
    </div>
  </div>
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>I want to enroll</p>
      <div class="wa-time">10:31</div>
    </div>
  </div>
</div>
```

---

## 📋 SOURCE CODE REFERENCES

| Topic | Source Location |
|-------|-----------------|
| BASIC Keywords | `botserver/src/basic/keywords/` |
| Database Models | `botserver/src/shared/models.rs` |
| API Routes | `botserver/src/core/urls.rs` |
| Configuration | `botserver/src/core/config/` |
| Templates | `botserver/templates/` |

---

## 🔧 BUILDING DOCUMENTATION

```bash
# Install mdBook
cargo install mdbook

# Build documentation
cd botbook && mdbook build

# Serve locally with hot reload
mdbook serve --open
```

---

## 🔑 REMEMBER

- **Accuracy** - Must match botserver source code
- **Completeness** - No placeholder sections
- **Clarity** - Accessible to BASIC enthusiasts
- **Keywords** - NEVER use underscores - always spaces
- **NO ASCII art** - Use SVG diagrams only
- **Version 6.2.0** - Always reference 6.2.0
- **GIT WORKFLOW** - ALWAYS push to ALL repositories (github, pragmatismo)
