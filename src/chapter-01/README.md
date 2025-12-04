# Chapter 01: Run and Talk

> **⚡ In a hurry?** Jump straight to [Quick Start](./quick-start.md) — you'll be chatting with your bot in 5 minutes.

Get General Bots running and have your first conversation.

---

## What You'll Achieve

By the end of this chapter, you will:

- ✅ Have General Bots running on your machine
- ✅ Understand what happens during bootstrap
- ✅ Complete your first conversation with a bot
- ✅ Know how sessions and channels work

---

## Choose Your Path

| If You Want To... | Go To |
|-------------------|-------|
| Get running immediately | [Quick Start](./quick-start.md) |
| Understand the architecture first | [Overview](./overview.md) |
| See all installation options | [Installation](./installation.md) |
| Learn about conversations | [First Conversation](./first-conversation.md) |
| Understand session management | [Sessions and Channels](./sessions.md) |

---

## The 30-Second Version

```bash
./botserver
```

Open `http://localhost:8080`. Start chatting. That's it.

Everything installs automatically on first run—PostgreSQL, storage, cache, and your first bot.

---

## How It Works

<div class="wa-chat">
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>How do I get started with General Bots?</p>
      <div class="wa-time">09:00</div>
    </div>
  </div>
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>Just three steps:</p>
      <p>1️⃣ Download <code>botserver</code></p>
      <p>2️⃣ Run <code>./botserver</code></p>
      <p>3️⃣ Open your browser to localhost:8080</p>
      <p>The bootstrap process handles everything else automatically!</p>
      <div class="wa-time">09:00</div>
    </div>
  </div>
  <div class="wa-message user">
    <div class="wa-bubble">
      <p>What gets installed?</p>
      <div class="wa-time">09:01</div>
    </div>
  </div>
  <div class="wa-message bot">
    <div class="wa-bubble">
      <p>📦 PostgreSQL (database)</p>
      <p>📦 MinIO (file storage)</p>
      <p>📦 Cache (Redis-compatible)</p>
      <p>📦 Default bot templates</p>
      <p>All in <code>botserver-stack/</code> — no system-wide installation!</p>
      <div class="wa-time">09:01</div>
    </div>
  </div>
</div>

---

## Topics in This Chapter

### [Overview](./overview.md)
What General Bots does and how it fits together.

### [Quick Start](./quick-start.md)
The fastest path from zero to running bot.

### [Installation](./installation.md)
Detailed setup options including LXC containers and production deployment.

### [First Conversation](./first-conversation.md)
Understanding how the bot responds and learns.

### [Sessions and Channels](./sessions.md)
How conversations are managed across WhatsApp, Web, Telegram, and more.

---

## Coming From Executive Vision?

If you just read the [Executive Vision](../executive-vision.md), here's what to know:

1. **Everything in that feature table?** It's all included in the single `botserver` binary
2. **No configuration needed** — Bootstrap detects your system and sets everything up
3. **Start simple** — Run it, chat with it, then customize

The philosophy is: **get running first, understand later**.

---

## Prerequisites

- **Operating System**: Linux, macOS, or Windows (WSL2 recommended)
- **Disk Space**: ~2GB for botserver-stack
- **RAM**: 4GB minimum, 8GB recommended
- **Ports**: 8080 (web), 5432 (database), 9000 (storage)

No Docker required. No cloud accounts. No API keys to start.

---

## Next Step

**[Quick Start →](./quick-start.md)**

---

<div align="center">
  <img src="https://pragmatismo.com.br/icons/general-bots-text.svg" alt="General Bots" width="200">
</div>