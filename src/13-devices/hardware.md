# Supported Hardware

## Single Board Computers (SBCs)

### Recommended Boards

| Board | CPU | RAM | Best For | Price |
|-------|-----|-----|----------|-------|
| **Orange Pi 5** | RK3588S | 4-16GB | Full LLM, NPU accel | $89-149 |
| **Raspberry Pi 5** | BCM2712 | 4-8GB | General purpose | $60-80 |
| **Orange Pi Zero 3** | H618 | 1-4GB | Minimal deployments | $20-35 |
| **Raspberry Pi 4** | BCM2711 | 2-8GB | Established ecosystem | $45-75 |
| **Raspberry Pi Zero 2W** | RP3A0 | 512MB | Ultra-compact | $15 |
| **Rock Pi 4** | RK3399 | 4GB | NPU available | $75 |
| **NVIDIA Jetson Nano** | Tegra X1 | 4GB | GPU inference | $149 |
| **BeagleBone Black** | AM3358 | 512MB | Industrial | $55 |
| **LattePanda 3 Delta** | N100 | 8GB | x86 compatibility | $269 |
| **ODROID-N2+** | S922X | 4GB | High performance | $79 |

### Minimum Requirements

**For UI only (connect to remote botserver):**
- Any ARM/x86 Linux board
- 256MB RAM
- Network connection
- Display output

**For local botserver:**
- ARM64 or x86_64
- 1GB RAM minimum
- 4GB storage

**For local LLM (llama.cpp):**
- ARM64 or x86_64
- 2GB+ RAM (4GB recommended)
- 2GB+ storage for model

### Orange Pi 5 (Recommended for LLM)

The Orange Pi 5 with RK3588S is ideal for embedded LLM:

<img src="../assets/chapter-13/orange-pi-5-specs.svg" alt="Orange Pi 5 Specifications" style="max-width: 100%; height: auto;">

## Displays

### Character LCDs (Minimal)

For text-only interfaces:

| Display | Resolution | Interface | Use Case |
|---------|------------|-----------|----------|
| HD44780 16x2 | 16 chars × 2 lines | I2C/GPIO | Status, simple Q&A |
| HD44780 20x4 | 20 chars × 4 lines | I2C/GPIO | More context |
| LCD2004 | 20 chars × 4 lines | I2C | Industrial |

**Example output on 16x2:** Simple text display showing user prompt and bot status.

### OLED Displays

For graphical monochrome interfaces:

| Display | Resolution | Interface | Size |
|---------|------------|-----------|------|
| SSD1306 | 128×64 | I2C/SPI | 0.96" |
| SSD1309 | 128×64 | I2C/SPI | 2.42" |
| SH1106 | 128×64 | I2C/SPI | 1.3" |
| SSD1322 | 256×64 | SPI | 3.12" |

### TFT/IPS Color Displays

For full graphical interface:

| Display | Resolution | Interface | Notes |
|---------|------------|-----------|-------|
| ILI9341 | 320×240 | SPI | Common, cheap |
| ST7789 | 240×320 | SPI | Fast refresh |
| ILI9488 | 480×320 | SPI | Larger |
| Waveshare 5" | 800×480 | HDMI | Touch optional |
| Waveshare 7" | 1024×600 | HDMI | Touch, IPS |
| Official Pi 7" | 800×480 | DSI | Best for Pi |

### E-Ink/E-Paper

For low-power, readable in sunlight:

| Display | Resolution | Colors | Refresh |
|---------|------------|--------|---------|
| Waveshare 2.13" | 250×122 | B/W | 2s |
| Waveshare 4.2" | 400×300 | B/W | 4s |
| Waveshare 7.5" | 800×480 | B/W | 5s |
| Good Display 9.7" | 1200×825 | B/W | 6s |

**Best for:** Menu displays, signs, low-update applications

### Industrial Displays

| Display | Resolution | Features |
|---------|------------|----------|
| Advantech | Various | Wide temp, sunlight |
| Winstar | Various | Industrial grade |
| Newhaven | Various | Long availability |

## Input Devices

### Keyboards

- **USB Keyboard** - Standard, any USB keyboard works
- **PS/2 Keyboard** - Via adapter, lower latency
- **Matrix Keypad** - 4x4 or 3x4, GPIO connected
- **I2C Keypad** - Fewer GPIO pins needed

### Touch Input

- **Capacitive Touch** - Better response, needs driver
- **Resistive Touch** - Works with gloves, pressure-based
- **IR Touch Frame** - Large displays, vandal-resistant

### Buttons & GPIO

<img src="../assets/chapter-13/gpio-button-interface.svg" alt="GPIO Button Interface" style="max-width: 100%; height: auto;">

## Enclosures

### Commercial Options

- **Hammond Manufacturing** - Industrial metal enclosures
- **Polycase** - Plastic, IP65 rated
- **Bud Industries** - Various sizes
- **Pi-specific cases** - Argon, Flirc, etc.

### DIY Options

- **3D Printed** - Custom fit, PLA/PETG
- **Laser Cut** - Acrylic, wood
- **Metal Fabrication** - Professional look

## Power

### Power Requirements

| Configuration | Power | Recommended PSU |
|---------------|-------|-----------------|
| Pi Zero + LCD | 1-2W | 5V 1A |
| Pi 4 + Display | 5-10W | 5V 3A |
| Orange Pi 5 | 8-15W | 5V 4A or 12V 2A |
| With NVMe SSD | +2-3W | Add 1A headroom |

### Power Options

- **USB-C PD** - Modern, efficient
- **PoE HAT** - Power over Ethernet
- **12V Barrel** - Industrial standard
- **Battery** - UPS, solar applications

### UPS Solutions

- **PiJuice** - Pi-specific UPS HAT
- **UPS PIco** - Small form factor
- **Powerboost** - Adafruit, lithium battery
