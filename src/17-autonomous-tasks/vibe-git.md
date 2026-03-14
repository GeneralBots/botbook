# Vibe Git

Git operations integrated with Forgejo ALM.

![Vibe Git](./assets/vibe/git.png)

---

## Overview

Vibe Git provides visual Git operations for version control of your generated applications. Connect to Forgejo for remote operations.

---

## Features

### Local Operations
- Initialize repository
- Stage/unstage files
- Commit changes
- View diff
- Branch management

### Remote Operations
- Push to Forgejo
- Pull from remote
- Fetch updates
- Create pull requests

### History
- Commit log viewer
- Author and date display
- Message search
- File change history

---

## Interface

### Changes Panel
```
Changes:
 M  index.html
 A  styles.css
 D  old-file.js

Staged (2):
 + styles.css
 M index.html
```

### Commit History
```
abc1234 (main) Add user authentication - John, 2h ago
def5678 Fix login validation      - Jane, 5h ago
ghi9012 Initial commit            - John, 1d ago
```

---

## Quick Start

### 1. Initialize Repository
```bash
git init
```

### 2. Add Files
```bash
git add .
```

### 3. Commit
```bash
git commit -m "Initial commit"
```

### 4. Connect to Remote
```bash
git remote add origin https://forgejo.example/user/repo.git
git push -u origin main
```

---

## Git Commands

### Status
```bash
git status
```

### Add Files
```bash
# Add specific file
git add file.txt

# Add all changes
git add -A
```

### Commit
```bash
git commit -m "Your message"
```

### Push
```bash
git push origin main
```

### Pull
```bash
git pull origin main
```

### Branch
```bash
# List branches
git branch

# Create branch
git branch feature-name

# Switch branch
git checkout feature-name

# Create and switch
git checkout -b feature-name
```

### Merge
```bash
git merge feature-name
```

---

## Forgejo Integration

### Configure Remote
```
Remote URL: https://forgejo.example/owner/repo.git
Username:   Your Forgejo username
Token:      Your API token
```

### Create Pull Request
1. Push branch to Forgejo
2. Click "Create PR" button
3. Fill title and description
4. Submit

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+S` | Stage current file |
| `Ctrl+Shift+S` | Stage all |
| `Ctrl+C` | Commit |
| `Ctrl+P` | Push |
| `Ctrl+U` | Pull |

---

## Troubleshooting

### Push Failed
- Check remote URL is correct
- Verify Forgejo credentials
- Check network connectivity

### Merge Conflicts
- View conflicting files
- Edit to resolve
- Stage and commit

### Empty History
- Repository may be new
- Check correct directory
- Verify .git exists
