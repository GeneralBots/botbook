# Quick Start - Deploy in 5 Minutes

Get General Bots running on your embedded device with local AI in just a few commands.

## Prerequisites

- An SBC (Raspberry Pi, Orange Pi, etc.) with Armbian/Raspbian
- SSH access to the device
- Internet connection (for initial setup only)

## One-Line Deploy

From your development machine:

```bash
# Clone and run the deployment script
git clone https://github.com/GeneralBots/botserver.git
cd botserver

# Deploy to Orange Pi (replace with your device IP)
./scripts/deploy-embedded.sh orangepi@192.168.1.100 --with-ui --with-llama
```

That's it! After ~10-15 minutes:
- botserver runs on port 8088
- llama.cpp runs on port 8080 with TinyLlama
- Embedded UI available at `http://your-device:8088/embedded/`

## Step-by-Step Guide

### Step 1: Prepare Your Device

Flash your SBC with a compatible OS:

**Raspberry Pi:**
```bash
# Download Raspberry Pi Imager
# Select: Raspberry Pi OS Lite (64-bit)
# Enable SSH in settings
```

**Orange Pi:**
```bash
# Download Armbian from armbian.com
# Flash with balenaEtcher
```

### Step 2: First Boot Configuration

```bash
# SSH into your device
ssh pi@raspberrypi.local  # or orangepi@orangepi.local

# Update system
sudo apt update && sudo apt upgrade -y

# Set timezone
sudo timedatectl set-timezone America/Sao_Paulo

# Enable I2C/SPI if using GPIO displays
sudo raspi-config  # or armbian-config
```

### Step 3: Run Deployment Script

From your development PC:

```bash
# Basic deployment (botserver only)
./scripts/deploy-embedded.sh pi@raspberrypi.local

# With embedded UI
./scripts/deploy-embedded.sh pi@raspberrypi.local --with-ui

# With local LLM (requires 4GB+ RAM)
./scripts/deploy-embedded.sh pi@raspberrypi.local --with-ui --with-llama

# Specify a different model
./scripts/deploy-embedded.sh pi@raspberrypi.local --with-llama --model phi-2-Q4_K_M.gguf
```

### Step 4: Verify Installation

```bash
# Check services
ssh pi@raspberrypi.local 'sudo systemctl status botserver'
ssh pi@raspberrypi.local 'sudo systemctl status llama-server'

# Test botserver
curl http://raspberrypi.local:8088/health

# Test llama.cpp
curl http://raspberrypi.local:8080/v1/models
```

### Step 5: Access the Interface

Open in your browser:
```
http://raspberrypi.local:8088/embedded/
```

Or set up kiosk mode (auto-starts on boot):
```bash
# Already configured if you used --with-ui
# Just reboot:
ssh pi@raspberrypi.local 'sudo reboot'
```

## Local Installation (On the Device)

If you prefer to install directly on the device:

```bash
# SSH into the device
ssh pi@raspberrypi.local

# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env

# Clone and build
git clone https://github.com/GeneralBots/botserver.git
cd botserver

# Run local deployment
./scripts/deploy-embedded.sh --local --with-ui --with-llama
```

⚠️ **Note:** Building on ARM devices is slow (1-2 hours). Cross-compilation is faster.

## Configuration

After deployment, edit the config file:

```bash
ssh pi@raspberrypi.local
sudo nano /opt/botserver/.env
```

Key settings:
```env
# Server
HOST=0.0.0.0
PORT=8088

# Local LLM
LLM_PROVIDER=llamacpp
LLM_API_URL=http://127.0.0.1:8080
LLM_MODEL=tinyllama

# Memory limits for small devices
MAX_CONTEXT_TOKENS=2048
MAX_RESPONSE_TOKENS=512
```

Restart after changes:
```bash
sudo systemctl restart botserver
```

## Troubleshooting

### Out of Memory

```bash
# Check memory usage
free -h

# Reduce llama.cpp context
sudo nano /etc/systemd/system/llama-server.service
# Change -c 2048 to -c 1024

# Or use a smaller model
# TinyLlama uses ~700MB, Phi-2 uses ~1.6GB
```

### Service Won't Start

```bash
# Check logs
sudo journalctl -u botserver -f
sudo journalctl -u llama-server -f

# Common issues:
# - Port already in use
# - Missing model file
# - Database permissions
```

### Display Not Working

```bash
# Check if display is detected
ls /dev/fb*       # HDMI/DSI
ls /dev/i2c*      # I2C displays
ls /dev/spidev*   # SPI displays

# For HDMI, check config
sudo nano /boot/config.txt  # Raspberry Pi
sudo nano /boot/armbianEnv.txt  # Orange Pi
```

## Next Steps

- [Embedded UI Guide](./embedded-ui.md) - Customize the interface
- [Local LLM Configuration](./local-llm.md) - Optimize AI performance
- [Kiosk Mode](./kiosk-mode.md) - Production deployment
- [Offline Operation](./offline.md) - Disconnected environments
