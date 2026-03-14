# Vibe Terminal

Full-featured terminal with isolated LXC containers for each session.

![Vibe Terminal](./assets/vibe/terminal.png)

---

## Overview

The Vibe terminal provides an isolated Ubuntu 22.04 container for each session. Your commands run in a secure, sandboxed environment that is automatically created on connect and destroyed on disconnect.

---

## Quick Start

1. Click **Terminal** icon on desktop or in Vibe window
2. Terminal connects to a new LXC container
3. Type commands as normal bash shell

```bash
$ pwd
/root
$ whoami
root
$ uname -a
Linux term-abc123 5.15.0 #1 SMP x86_64 GNU/Linux
```

---

## Features

### Isolated Containers
- Each terminal session gets its own Ubuntu 22.04 container
- Containers are ephemeral - destroyed on disconnect
- Full root access within container

### 256-Color Support
- Full xterm-256color support
- Works with vim, tmux, htop, etc.

### WebSocket Protocol
- Connects via WebSocket for real-time I/O
- Automatic reconnection on disconnect
- Session persistence during network issues

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `WS` | `/api/terminal/ws?session_id=xxx` | Terminal WebSocket |
| `GET` | `/api/terminal/list` | List active terminals |
| `POST` | `/api/terminal/create` | Create new terminal |
| `POST` | `/api/terminal/kill` | Kill terminal session |

### WebSocket Commands

Send text to execute commands:
```
ls -la
```

Special commands:
- `resize COLS ROWS` - Resize terminal
- `exit` - Close terminal session

---

## Configuration

### Container Settings

The terminal uses these LXC commands:
- `lxc launch ubuntu:22.04 {name}` - Create container
- `lxc exec {name} -- bash` - Execute shell
- `lxc stop {name} -f` - Stop container
- `lxc delete {name} -f` - Delete container

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `TERM` | `xterm-256color` | Terminal type |

---

## Troubleshooting

### Connection Failed
- Check that LXC is installed and running
- Verify network connectivity
- Check botserver logs for errors

### Container Won't Start
- Ensure LXC daemon is running: `systemctl status lxc`
- Check LXC configuration: `lxc list`
- Review container logs: `lxc info {name}`

### Commands Not Working
- Container may have been destroyed - reconnect
- Check WebSocket connection status

---

## Security

- Container names are sanitized (alphanumeric + dash only)
- Containers are isolated from host network by default
- Sessions are cleaned up on disconnect
- No persistent storage between sessions
