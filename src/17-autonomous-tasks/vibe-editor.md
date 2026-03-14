# Vibe Editor

Monaco-powered code editor with full IDE features.

![Vibe Editor](./assets/vibe/editor.png)

---

## Overview

The Vibe Editor is based on Monaco (the same editor that powers VS Code). It provides a full IDE experience with syntax highlighting, IntelliSense, multi-file editing, and more.

---

## Features

### Syntax Highlighting
Supports 70+ languages including:
- JavaScript/TypeScript
- Python
- Rust
- Go
- HTML/CSS
- SQL
- JSON/YAML
- And many more

### IntelliSense
- Auto-completion
- Parameter hints
- Signature help
- Quick fixes

### Multi-Cursor Editing
- `Ctrl+D` - Select next occurrence
- `Alt+Click` - Add cursor
- `Ctrl+Alt+Down` - Add line below

### Search & Replace
- `Ctrl+F` - Find
- `Ctrl+H` - Replace
- `Ctrl+Shift+F` - Find in files
- Regex support enabled

### Minimap
- Code overview on right side
- Click to navigate
- Draggable viewport

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+S` | Save file |
| `Ctrl+P` | Quick open file |
| `Ctrl+Shift+P` | Command palette |
| `Ctrl+F` | Find |
| `Ctrl+H` | Replace |
| `Ctrl+Shift+F` | Find in files |
| `Ctrl+D` | Select next occurrence |
| `Alt+Up/Down` | Move line up/down |
| `Ctrl+/` | Toggle comment |
| `Ctrl+Shift+K` | Delete line |
| `Ctrl+Enter` | Insert line below |
| `Ctrl+Shift+Enter` | Insert line above |
| `F12` | Go to definition |
| `Ctrl+Space` | Trigger IntelliSense |

---

## File Operations

### Opening Files
- Click file in file tree
- `Ctrl+P` for quick open
- Drag and drop files

### Saving Files
- `Ctrl+S` to save
- Auto-save on focus loss
- Shows unsaved indicator (dot on tab)

### Creating Files
- Right-click in file tree
- New file button in toolbar

---

## Workspace

### File Tree
Located on the left side:
- Expand/collapse folders
- File icons by type
- Right-click context menu

### Supported File Types
| Icon | Type |
|------|------|
| 📄 | Generic file |
| 📜 | Script (js, ts, py) |
| 🎨 | Style (css, scss) |
| 📦 | Config (json, yaml, toml) |
| 🔷 | Component (vue, svelte) |

---

## Configuration

### Theme
- Dark (default)
- Light
- High contrast

### Font
- Fira Code (with ligatures)
- Customizable size
- Line height control

### Editor Settings
```json
{
  "editor.fontSize": 14,
  "editor.fontFamily": "Fira Code",
  "editor.tabSize": 4,
  "editor.minimap.enabled": true,
  "editor.formatOnSave": true
}
```

---

## Integration

### With Vibe Pipeline
The editor integrates with the Vibe AI pipeline:
1. AI generates code in editor
2. Review agent checks code
3. You can edit manually
4. Changes tracked in Git

### With Terminal
- `Ctrl+`` - Toggle terminal panel
- Run code directly from editor
- See output in terminal
