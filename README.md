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

🚧 **Current Phase:** Phase 1 - Component Selection & Planning (~70% complete)

This is a hobby project in active development with a realistic timeline. Check back for updates!

### Development Roadmap

| Phase | Milestone | Focus Area | Status | Target |
|-------|-----------|------------|--------|--------|
| **Phase 1** | v0.1 | Component Selection & Planning | 🔨 **In Progress** (70%) | 2026 Q1 |
| **Phase 2** | v0.2 | Hardware Design (Schematic, PCB, BOM) | 📋 Planned | 2026 Q3 |
| **Phase 3** | v0.3 | Firmware Development (ESPHome) | 📋 Planned | 2026 Q4 |
| **Phase 4** | v0.4 | Enclosure Design (3D Models, FreeCAD) | 📋 Planned | 2027 Q1 |
| **Phase 5** | v0.5 | Prototype & Testing | 📋 Planned | 2027 Q2 |
| **Phase 6** | v1.0 | Documentation & Public Release | 📋 Planned | 2027 Q3 |

#### Phase 1 Progress (Current)
- ✅ Project setup, Git Flow workflow, Wiki (15+ pages)
- ✅ mmWave sensor selected (DFRobot C4001) with full documentation
- ✅ PIR sensor selected (Panasonic EKMC1604111) with full documentation
- 🔨 Light sensor selection in progress

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
│   └── HARDWARE_DESIGN.md
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
│   ├── sensors/           # Sensor technical specs ✓
│   │   ├── SENSORS_INDEX.md
│   │   └── dfrobot-c4001/
│   │       ├── C4001_TECHNICAL_GUIDE.md
│   │       └── datasheets/
│   ├── GITFLOW.md         # Git Flow workflow ✓
│   ├── CONVENTIONAL_COMMITS.md  # Commit standards ✓
│   ├── VERSIONING.md      # Semantic versioning ✓
│   ├── BRANCH_PROTECTION.md  # Branch rules ✓
│   ├── GITHUB_WIKI.md     # Wiki strategy ✓
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

- **[DFRobot C4001 mmWave Technical Guide](https://github.com/Soriarty/HaloSense/blob/develop/docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)** - Complete UART protocol, pinouts, ESPHome integration
- **[Git Flow Workflow](https://github.com/Soriarty/HaloSense/blob/develop/docs/GITFLOW.md)** - Development workflow
- **[Conventional Commits](https://github.com/Soriarty/HaloSense/blob/develop/docs/CONVENTIONAL_COMMITS.md)** - Commit message format
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

### Sensors
- **mmWave:** [DFRobot C4001 (SEN0609)](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)
  - 24GHz FMCW radar, UART interface
  - Presence: 16m, Motion: 25m, 100° × 40° beam
- **PIR:** [Panasonic EKMC1604111](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/panasonic-ekmc1604111/EKMC1604111_TECHNICAL_GUIDE.md) (wall installation type)
  - Three-step lens (12m/6m/3m zones), Digital output
  - Coverage: 105° × 40° (asymmetric vertical), 68 detection zones
  - Response: <0.1s instant trigger, 170μA low power
  - Mainboard-integrated (through-hole mounting)
- **Light Sensor:** TBD (model selection in progress)

### Physical
- **Form Factor:** Circular PCB
- **Diameter:** TBD
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
  - [Sensor Documentation Index](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/SENSORS_INDEX.md)
  - [Git Flow Workflow](https://github.com/Soriarty/HaloSense/blob/main/docs/GITFLOW.md)
  - [Conventional Commits Guide](https://github.com/Soriarty/HaloSense/blob/main/docs/CONVENTIONAL_COMMITS.md)
  - [Versioning Guide](https://github.com/Soriarty/HaloSense/blob/main/docs/VERSIONING.md)
  - [GitHub Wiki Strategy](https://github.com/Soriarty/HaloSense/blob/main/docs/GITHUB_WIKI.md)
- **Author:** [@Soriarty](https://github.com/Soriarty)
- **Home Assistant Community:** [Coming soon]

---

## Acknowledgments

- **OLIMEX** - ESP32-POE board design foundation
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
