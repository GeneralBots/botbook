# Documentation Style Standards

All interface layouts in this documentation use SVG-based wireframe representations for screenshots and diagrams. Conversation examples use the WhatsApp-style HTML format for consistent, visually appealing rendering.

---

## Interface Wireframes (SVG)

All interface screenshots and layouts should use SVG wireframes located in `/assets/`.

### Directory Structure

```
assets/
├── suite/
│   ├── chat-screen.svg
│   ├── drive-screen.svg
│   ├── calendar-screen.svg
│   ├── mail-screen.svg
│   ├── tasks-screen.svg
│   ├── meet-screen.svg
│   ├── live-monitoring-organism.svg
│   └── ...
├── chapter-01/
│   ├── bootstrap-process.svg
│   └── session-states.svg
└── chapter-04/
    └── analytics-interface.svg
```

### Referencing SVG Wireframes

Use standard HTML image syntax with responsive styling:

```html
<img src="../assets/suite/chat-screen.svg" alt="Chat Interface" style="max-width: 100%; height: auto;">
```

---

## SVG Theme Transparency Guidelines

All SVGs MUST be theme-agnostic and work with light/dark modes. Follow these requirements:

### Required CSS Media Query

Every SVG must include a `<style>` block with `prefers-color-scheme` support:

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

### Background Transparency

- Use `fill="#FAFBFC"` for light backgrounds (subtle, not pure white)
- Add dot pattern overlay for texture: `fill="url(#dots)"` with low opacity
- Cards use `fill="#FFFFFF"` with border strokes for definition
- **NEVER** use pure black (`#000000`) backgrounds

### Color Palette (Theme-Safe)

| Purpose | Light Mode | Dark Mode Adaptation |
|---------|------------|---------------------|
| Title text | `#1E1B4B` | `#F1F5F9` (via CSS) |
| Main text | `#334155` | `#E2E8F0` (via CSS) |
| Secondary text | `#64748B` | `#94A3B8` (via CSS) |
| Mono/code text | `#475569` | `#CBD5E1` (via CSS) |
| Card backgrounds | `#FFFFFF` | Keep white (contrast) |
| Borders | `#E2E8F0` | Keep (works both) |

### Standard Gradients

Use these gradient IDs consistently across all SVGs:

```xml
<defs>
  <linearGradient id="primaryGrad" x1="0%" y1="0%" x2="100%" y2="100%">
    <stop offset="0%" style="stop-color:#6366F1;stop-opacity:1" />
    <stop offset="100%" style="stop-color:#8B5CF6;stop-opacity:1" />
  </linearGradient>

  <linearGradient id="cyanGrad" x1="0%" y1="0%" x2="100%" y2="100%">
    <stop offset="0%" style="stop-color:#06B6D4;stop-opacity:1" />
    <stop offset="100%" style="stop-color:#0EA5E9;stop-opacity:1" />
  </linearGradient>

  <linearGradient id="greenGrad" x1="0%" y1="0%" x2="100%" y2="100%">
    <stop offset="0%" style="stop-color:#10B981;stop-opacity:1" />
    <stop offset="100%" style="stop-color:#34D399;stop-opacity:1" />
  </linearGradient>

  <linearGradient id="orangeGrad" x1="0%" y1="0%" x2="100%" y2="100%">
    <stop offset="0%" style="stop-color:#F59E0B;stop-opacity:1" />
    <stop offset="100%" style="stop-color:#FBBF24;stop-opacity:1" />
  </linearGradient>

  <filter id="cardShadow" x="-10%" y="-10%" width="120%" height="130%">
    <feDropShadow dx="0" dy="4" stdDeviation="8" flood-color="#6366F1" flood-opacity="0.15"/>
  </filter>

  <pattern id="dots" patternUnits="userSpaceOnUse" width="20" height="20">
    <circle cx="10" cy="10" r="1" fill="#6366F1" opacity="0.08"/>
  </pattern>
</defs>
```

### DO NOT

- ❌ Hardcode text colors without CSS class
- ❌ Use pure black (`#000000`) or pure white (`#FFFFFF`) for text
- ❌ Forget the `@media (prefers-color-scheme: dark)` block
- ❌ Use opaque backgrounds that don't adapt
- ❌ Create new gradient IDs when standard ones exist

### DO

- ✅ Use CSS classes for all text elements
- ✅ Include dark mode media query in every SVG
- ✅ Use standard gradient IDs from the palette
- ✅ Test SVGs in both light and dark browser modes
- ✅ Use subtle shadows with low opacity (`0.15`)
- ✅ Keep white cards for contrast in both modes

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
      <p>✅ Welcome to Computer Science, Sarah!</p>
      <p>Your enrollment ID is: ENR-2025-0142</p>
      <div class="wa-time">10:31</div>
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
5. **Emojis** — Use sparingly for status indicators (✅, ❌, 📧, 📅, 📁)
6. **Bold text** — Use `<strong>` for emphasis
7. **Attachments** — Indicate with 📎 emoji and filename

### File Attachments Example

```html
<div class="wa-chat">
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>Upload the quarterly report</p>
      <p>📎 Q4-Report.pdf</p>
      <div class="wa-time">10:30</div>
    </div>
  </div>
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>✅ File uploaded successfully!</p>
      <p>📄 Q4-Report.pdf (2.4 MB)</p>
      <p>📁 Saved to: My Drive</p>
      <div class="wa-time">10:30</div>
    </div>
  </div>
</div>
```

---

## CSS Styling

The WhatsApp chat styling is defined in `whatsapp-chat.css` and automatically included in the book build. The styles provide:

- Familiar messaging app appearance
- Proper alignment (user right, bot left)
- Bubble styling with shadows
- Responsive layout
- Timestamp formatting

---

## When to Use Each Format

| Content Type | Format |
|--------------|--------|
| Interface screenshots | SVG wireframe |
| System architecture | SVG diagram |
| Data flow diagrams | SVG diagram |
| Bot conversations | WhatsApp HTML |
| API examples | Code blocks |
| Configuration | Code blocks |

---

## Global Conversation Style Reference

For all conversation examples throughout the book, follow the format established in:

**[BASIC vs Automation Tools](../chapter-06-gbdialog/basic-vs-automation-tools.md)**

This document serves as the canonical reference for:

- Conversation formatting
- Multi-channel message representation
- Bot response styling
- User input examples

---

## See Also

- [Conversation Examples](./conversation-examples.md) — Example patterns
- [BASIC vs Automation Tools](../chapter-06-gbdialog/basic-vs-automation-tools.md) — Canonical conversation style
- [Chapter 04 Apps](../chapter-04-gbui/apps/README.md) — Interface documentation