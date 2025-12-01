# HaloSense

> **Professional-grade presence detection for your smart home**

[![GitHub](https://img.shields.io/badge/GitHub-Soriarty%2FHaloSense-blue?logo=github)](https://github.com/Soriarty/HaloSense)
[![License](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Maintainer](https://img.shields.io/badge/Maintainer-Soriarty-orange?logo=github)](https://github.com/Soriarty)

Open-source smart home presence sensor with complete design files included. Custom ESP32 circular PCB (KiCad), mmWave+PIR+lux sensors, 3D-printable enclosure, and mounting solutions. Deploy via PoE, Ethernet+USB-C, or WiFi+USB-C. ESPHome-ready for Home Assistant integration.

Fork it, build it, customize it. Professional results, maker-friendly.

🔗 **Repository:** [https://github.com/Soriarty/HaloSense](https://github.com/Soriarty/HaloSense)

---

## Features

### Multi-Sensor Detection
- **mmWave Radar** - Accurate presence detection (even stationary people)
- **PIR Motion Sensor** - Fast motion detection for instant room entry trigger
- **Ambient Light Sensor** - Lux measurement for smart lighting automation

**Why Both mmWave + PIR?**
- **PIR:** Instant detection (<0.1s) when entering room - immediate automation trigger
- **mmWave:** Continuous presence monitoring - detects even stationary people
- **Combined:** Best of both worlds - instant response + accurate presence tracking

### Flexible Connectivity
- **PoE Mode** - Single cable for power + data (IEEE 802.3af)
- **Ethernet + USB-C** - Standard network connection with USB power
- **WiFi + USB-C** - Wireless connectivity for flexible placement

### Complete Design Package
- **Hardware** - Single mainboard design (circular form factor)
  - Top-side: ESP32 + sensor module connectors
  - Bottom-side: PoE circuit + vertical Ethernet + vertical USB-C
- **Firmware** - ESPHome configuration for Home Assistant
- **Enclosure** - 3D-printable housing (STL files)
- **Mounting** - Various mounting options (wall, ceiling, desk)

---

## Why HaloSense?

Inspired by devices like the Aqara FP2, but addressing key limitations:

- ✅ **Wired networking** - No WiFi congestion, rock-solid reliability
- ✅ **PoE support** - Single cable installation
- ✅ **Open source** - Full control, no cloud dependencies
- ✅ **ESPHome integration** - Seamless Home Assistant compatibility
- ✅ **Flexible deployment** - Multiple power/connectivity options
- ✅ **DIY-friendly** - Build it yourself, customize to your needs

---

## Project Status

🚧 **Current Phase:** Phase 1 - Component Selection & Planning (**100% complete** ✅)

This is a hobby project in active development with a realistic timeline. Check back for updates!

### Development Roadmap

| Phase | Milestone | Focus Area | Status | Target |
|-------|-----------|------------|--------|--------|
| **Phase 1** | v0.1 | Component Selection & Planning | ✅ **Complete** (100%) | 2026 Q1 |
| **Phase 2** | v0.2 | Hardware Design (Schematic, PCB, BOM) | 📋 Planned | 2026 Q3 |
| **Phase 3** | v0.3 | Firmware Development (ESPHome) | 📋 Planned | 2026 Q4 |
| **Phase 4** | v0.4 | Enclosure Design (3D Models, FreeCAD) | 📋 Planned | 2027 Q1 |
| **Phase 5** | v0.5 | Prototype & Testing | 📋 Planned | 2027 Q2 |
| **Phase 6** | v1.0 | Documentation & Public Release | 📋 Planned | 2027 Q3 |

#### Phase 1 Completed ✅
- ✅ Project setup, Git Flow workflow, Wiki (15+ pages)
- ✅ Sensors selected with full documentation (mmWave, PIR, Light)
- ✅ ESP32 modules documented (WROOM-32E recommended, WROVER-E alternative)
- ✅ Hardware components documented (Ethernet PHY, PoE, Power ICs, USB)
- ✅ GPIO allocation finalized (all conflicts resolved)
- ✅ OLIMEX ESP32-POE reference design analyzed

**📊 Track detailed progress:**
- **[GitHub Project Board](https://github.com/Soriarty/HaloSense/projects)** - Kanban view with all tasks
- **[Milestones](https://github.com/Soriarty/HaloSense/milestones)** - Phase tracking with due dates
- **[Open Issues](https://github.com/Soriarty/HaloSense/issues)** - Current work items
- **[Closed Issues](https://github.com/Soriarty/HaloSense/issues?q=is%3Aissue+is%3Aclosed)** - Completed work

---

## Repository Structure

```
HaloSense/
├── hardware/              # KiCad PCB design files (planned)
│   ├── schematics/
│   ├── pcb/
│   ├── gerbers/
│   ├── reference/         # Reference designs (submodules)
│   │   └── esp32-poe/     # OLIMEX ESP32-POE reference ✓
│   └── README.md
├── firmware/              # ESPHome configuration (planned)
│   ├── halosense.yaml
│   └── FIRMWARE_GUIDE.md
├── enclosure/             # 3D printable models (planned)
│   ├── stl/
│   ├── step/
│   └── ENCLOSURE_DESIGN.md
├── docs/                  # Technical documentation (for developers)
│   ├── wiki/              # Wiki submodule (user documentation) ✓
│   │   ├── Home.md
│   │   ├── Getting-Started.md
│   │   ├── Assembly-Guide.md
│   │   ├── FAQ.md
│   │   └── ... (15 Wiki pages)
│   ├── hardware/          # Hardware component documentation ✓
│   │   ├── components/    # All hardware components (sensors + ICs)
│   │   │   ├── dfrobot-c4001/              # mmWave radar sensor
│   │   │   ├── panasonic-ekmc1604111/      # PIR motion sensor
│   │   │   ├── rohm-bh1750/                # Ambient light sensor
│   │   │   ├── espressif-esp32-wroom-32e/  # ESP32 MCU (recommended)
│   │   │   ├── espressif-esp32-wrover-e/   # ESP32 with PSRAM
│   │   │   ├── microchip-lan8720a/         # Ethernet PHY
│   │   │   ├── ti-tps2378/                 # PoE controller
│   │   │   ├── ti-tps62a02a/               # 3.3V buck converter
│   │   │   ├── silergy-tx4138/             # 5V buck converter
│   │   │   ├── tp-tp4054/                  # Battery charger
│   │   │   └── wch-ch340x/                 # USB-UART bridge
│   │   ├── power-budget.md     # Power consumption analysis
│   │   └── ip-rating.md        # IP54 enclosure design
│   ├── development/       # Developer workflow docs ✓
│   │   ├── git-flow.md
│   │   ├── conventional-commits.md
│   │   ├── versioning.md
│   │   ├── branch-protection.md
│   │   └── github-wiki.md
│   ├── assembly.md        # → Redirects to Wiki
│   ├── bom.md             # → Redirects to Wiki
│   └── installation.md    # → Redirects to Wiki
├── CONTRIBUTING.md        # Contribution guidelines ✓
├── LICENSE.md             # Project license ✓
├── CHANGELOG.md           # Version history ✓
└── README.md              # This file
```

---

## Getting Started

### 📖 User Documentation

**For building and using HaloSense, visit the [Wiki](https://github.com/Soriarty/HaloSense/wiki):**

- **[Getting Started Guide](https://github.com/Soriarty/HaloSense/wiki/Getting-Started)** - Start here!
- **[Bill of Materials](https://github.com/Soriarty/HaloSense/wiki/Bill-of-Materials)** - What to buy
- **[Assembly Guide](https://github.com/Soriarty/HaloSense/wiki/Assembly-Guide)** - How to build
- **[Installation Guide](https://github.com/Soriarty/HaloSense/wiki/Installation-Guide)** - Setup and config
- **[FAQ](https://github.com/Soriarty/HaloSense/wiki/FAQ)** - Common questions
- **[Troubleshooting](https://github.com/Soriarty/HaloSense/wiki/Troubleshooting)** - Problem solving

### 🔧 Technical Documentation

**For developers and technical details, see the [docs/](https://github.com/Soriarty/HaloSense/tree/develop/docs) directory:**

**Hardware Components (Sensors + ICs):**
- **[All Components Overview & GPIO Allocation](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/README.md)** - Complete documentation, power budget
- **[DFRobot C4001 mmWave Radar](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/dfrobot-c4001/README.md)** - UART protocol, ESPHome integration
- **[Panasonic EKMC1604111 PIR Sensor](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/panasonic-ekmc1604111/README.md)** - Motion detection specs
- **[ROHM BH1750FVI Light Sensor](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/rohm-bh1750/README.md)** - I2C ambient light sensor
- **[ESP32-WROOM-32E Module](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/espressif-esp32-wroom-32e/README.md)** - Main MCU

**Development Workflow:**
- **[Git Flow Workflow](https://github.com/Soriarty/HaloSense/blob/develop/docs/development/git-flow.md)** - Branching strategy
- **[Conventional Commits](https://github.com/Soriarty/HaloSense/blob/develop/docs/development/conventional-commits.md)** - Commit standards
- **[Contributing Guidelines](https://github.com/Soriarty/HaloSense/blob/develop/CONTRIBUTING.md)** - How to contribute

### Prerequisites

- **Hardware:** [See Bill of Materials on Wiki](https://github.com/Soriarty/HaloSense/wiki/Bill-of-Materials)
- **Software:**
  - [KiCad 9.0+](https://www.kicad.org/) - PCB design
  - [FreeCAD 1.0+](https://www.freecad.org/) - 3D enclosure design
  - [ESPHome](https://esphome.io/) - Firmware
  - [Home Assistant](https://www.home-assistant.io/) - Integration (optional)

---

## Technical Specifications

### Power Options
- **PoE (802.3af):** 15.4W available, ~5W typical consumption
- **USB-C:** 5V/2A minimum
- **Ethernet + USB-C:** Standard networking + external power

### Connectivity
- **Ethernet:** 10/100 Mbps
- **WiFi:** 802.11 b/g/n (2.4GHz)
- **Protocol:** MQTT, Home Assistant API

### Sensors & GPIO Allocation
- **mmWave Radar:** [DFRobot C4001 (SEN0609)](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/dfrobot-c4001/README.md)
  - 24GHz FMCW radar, UART interface (115200 baud)
  - **GPIO:** GPIO16 (RX), GPIO9 (TX) - Software UART
  - Presence: 16m, Motion: 25m, 100° × 40° beam
  - ESPHome compatible, ASCII command protocol

- **PIR Motion:** [Panasonic EKMC1604111](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/panasonic-ekmc1604111/README.md)
  - Three-step lens (12m/6m/3m zones), Digital output
  - **GPIO:** GPI35 (input-only, 33kΩ pull-down resistor)
  - Coverage: 105° × 40° (asymmetric vertical), 68 beams
  - Response: <0.1s instant trigger, 170μA low power
  - Mainboard-integrated (through-hole mounting)

- **Light Sensor:** [ROHM BH1750FVI](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/rohm-bh1750/README.md)
  - Digital 16-bit I2C ambient light sensor
  - **GPIO:** GPIO32 (SDA), GPIO33 (SCL) - Hardware I2C
  - Range: 1-65,535 lx (extendable to 0.11-100,000 lx)
  - Resolution: 0.5-4 lx, Address: 0x23 or 0x5C
  - Power: 120μA active, 0.01μA standby (0.4mW typical)
  - ESPHome native support, JLCPCB available (C78960)

**All GPIO conflicts resolved** - No interference with Ethernet RMII or boot strapping pins.

### Hardware Components
- **MCU:** [ESP32-WROOM-32E](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/espressif-esp32-wroom-32e/README.md)
  - Dual-core Xtensa LX6 @ 240 MHz, 520KB SRAM, 4/8/16MB Flash
  - Wi-Fi 802.11 b/g/n + Bluetooth 4.2 BR/EDR/BLE
  - All 38 GPIOs available (including GPIO16/GPIO17)

- **Ethernet PHY:** Microchip LAN8720A (10/100 Mbps RMII)
- **PoE Controller:** TI TPS2378 (IEEE 802.3af/at, up to 25.5W)
- **Power ICs:**
  - Silergy TX4138 (48V → 5V buck converter)
  - TI TPS62A02A (5V → 3.3V buck converter for LAN PHY)
  - TP4054 (Li-Po battery charger, optional backup)
- **USB Bridge:** WCH CH340X (USB-to-UART for programming)

See [Hardware Components Documentation](https://github.com/Soriarty/HaloSense/blob/develop/docs/hardware/components/README.md) for complete specifications.

### Physical
- **Form Factor:** Circular PCB (based on OLIMEX ESP32-POE reference)
- **Diameter:** TBD (Phase 2 design)
- **Mounting:** Wall, ceiling, or desk options

---

## License & Usage

### For Individual/DIY Use (Free)

This project is licensed under **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)**.

You are free to:
- ✅ **Build** - Manufacture units for personal use
- ✅ **Modify** - Adapt the design to your needs
- ✅ **Share** - Distribute your modifications (under same license)
- ✅ **Non-commercial** - Use in your home, share with friends

### For Commercial Use

Commercial use requires a separate licensing agreement.

**Commercial use includes:**
- Manufacturing for sale or profit
- Integration into commercial products or services
- Providing as part of paid installation/support services

📧 **Contact:** [@Soriarty](https://github.com/Soriarty) or [open an issue](https://github.com/Soriarty/HaloSense/issues) for commercial licensing inquiries.

---

## Contributing

Contributions are welcome! Whether it's hardware improvements, firmware enhancements, documentation, or bug reports - all help is appreciated.

**Please read our [Contribution Guidelines](CONTRIBUTING.md)** for detailed information on:
- How to contribute (hardware, firmware, enclosure, documentation)
- Development setup
- Pull request process
- Style guidelines
- Testing requirements

### Quick Start

1. Fork the repository
2. Create a feature branch from `develop`:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/amazing-improvement
   ```
3. Make your changes following the [guidelines](CONTRIBUTING.md)
4. Test thoroughly
5. Commit using [Conventional Commits](docs/CONVENTIONAL_COMMITS.md) format:
   ```bash
   git commit -m "feat(sensor): add new sensor support"
   ```
6. Push to your fork and create PR to `develop`

**Workflow:** We use [Git Flow](docs/GITFLOW.md) branching strategy with [Conventional Commits](docs/CONVENTIONAL_COMMITS.md) and [Semantic Versioning](docs/VERSIONING.md).

**First time contributing?** Check out our [detailed guide](CONTRIBUTING.md) or ask in [Discussions](https://github.com/Soriarty/HaloSense/discussions)!

---

## Community & Support

- **📖 Wiki:** [User Documentation](https://github.com/Soriarty/HaloSense/wiki) - Getting started, guides, tutorials
- **Issues:** [GitHub Issues](https://github.com/Soriarty/HaloSense/issues) - Bug reports and feature requests
- **Discussions:** [GitHub Discussions](https://github.com/Soriarty/HaloSense/discussions) - General questions and community
- **Contributing:** [Contribution Guidelines](CONTRIBUTING.md) - How to contribute
- **Technical Documentation:**
  - [Sensor Documentation Index](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/README.md)
  - [Git Flow Workflow](https://github.com/Soriarty/HaloSense/blob/main/docs/development/git-flow.md)
  - [Conventional Commits Guide](https://github.com/Soriarty/HaloSense/blob/main/docs/development/conventional-commits.md)
  - [Versioning Guide](https://github.com/Soriarty/HaloSense/blob/main/docs/development/versioning.md)
  - [GitHub Wiki Strategy](https://github.com/Soriarty/HaloSense/blob/main/docs/development/github-wiki.md)
- **Author:** [@Soriarty](https://github.com/Soriarty)
- **Home Assistant Community:** [Coming soon]

---

## Acknowledgments

- **OLIMEX** - [ESP32-POE board](https://github.com/OLIMEX/ESP32-POE) design foundation (included as git submodule in `hardware/reference/esp32-poe/`)
- **ESPHome** - Making ESP32 integration seamless
- **Home Assistant** - Open-source smart home platform
- Inspired by **Aqara FP2** presence sensor design

---

## Author

**Soriarty** - [@Soriarty](https://github.com/Soriarty)

*HaloSense was created to address the need for reliable, wired presence detection in professional smart home installations while remaining accessible to the DIY community.*

---

## Disclaimer

This is a DIY electronics project. Build at your own risk. Always follow proper safety procedures when working with electronics and mains power (especially with PoE).

The authors are not responsible for any damage, injury, or issues arising from building or using this design.

---

## Project Inspiration

This project was born from a simple need: reliable, wired presence detection for smart homes. While there are excellent wireless options available, the lack of PoE-capable, multi-sensor presence detectors led to the creation of HaloSense.

Built during a home renovation with smart home integration in mind, HaloSense aims to provide the flexibility and reliability that professional installations demand, while remaining accessible to the DIY community.

---

**Star ⭐ this repo if you find it useful!**

---

License: CC BY-NC-SA 4.0 | Created by [@Soriarty](https://github.com/Soriarty) | Made with ❤️ for the smart home community
