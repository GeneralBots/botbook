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