# Chapter 20: Embedded & Offline Deployment

Deploy General Bots to any device - from Raspberry Pi to industrial kiosks - with local LLM inference for fully offline AI capabilities.

## Overview

General Bots can run on minimal hardware with displays as small as 16x2 character LCDs, enabling AI-powered interactions anywhere:

- **Kiosks** - Self-service terminals in stores, airports, hospitals
- **Industrial IoT** - Factory floor assistants, machine interfaces
- **Smart Home** - Wall panels, kitchen displays, door intercoms
- **Retail** - Point-of-sale systems, product information terminals
- **Education** - Classroom assistants, lab equipment interfaces
- **Healthcare** - Patient check-in, medication reminders

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         Embedded GB Architecture                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│    ┌──────────────┐     ┌──────────────┐     ┌──────────────┐              │
│    │   Display    │     │  botserver   │     │  llama.cpp   │              │
│    │  LCD/OLED    │────▶│   (Rust)     │────▶│   (Local)    │              │
│    │   TFT/HDMI   │     │  Port 8088   │     │  Port 8080   │              │
│    └──────────────┘     └──────────────┘     └──────────────┘              │
│           │                    │                    │                       │
│           │                    │                    │                       │
│    ┌──────▼──────┐     ┌──────▼──────┐     ┌──────▼──────┐              │
│    │  Keyboard   │     │   SQLite    │     │  TinyLlama  │              │
│    │  Buttons    │     │   (Data)    │     │    GGUF     │              │
│    │  Touch      │     │             │     │   (~700MB)  │              │
│    └─────────────┘     └─────────────┘     └─────────────┘              │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

## What's in This Chapter

- [Supported Hardware](./hardware.md) - Boards, displays, and peripherals
- [Quick Start](./quick-start.md) - Deploy in 5 minutes
- [Embedded UI](./embedded-ui.md) - Interface for small displays
- [Local LLM](./local-llm.md) - Offline AI with llama.cpp
- [Display Modes](./display-modes.md) - LCD, OLED, TFT, E-ink configurations
- [Kiosk Mode](./kiosk-mode.md) - Locked-down production deployments
- [Performance Tuning](./performance.md) - Optimize for limited resources
- [Offline Operation](./offline.md) - No internet required
- [Use Cases](./use-cases.md) - Real-world deployment examples
