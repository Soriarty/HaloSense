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
- **PIR Motion Sensor** - Traditional motion detection backup
- **Ambient Light Sensor** - Lux measurement for smart lighting automation

### Flexible Connectivity
- **PoE Mode** - Single cable for power + data (IEEE 802.3af)
- **Ethernet + USB-C** - Standard network connection with USB power
- **WiFi + USB-C** - Wireless connectivity for flexible placement

### Complete Design Package
- **Hardware** - KiCad PCB design files (circular form factor)
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

🚧 **Work in Progress** 🚧

This project is in active development. Check back for updates!

### Roadmap
- [ ] Hardware design (KiCad)
  - [ ] ESP32-POE base modification
  - [ ] Circular PCB layout
  - [ ] Sensor integration
  - [ ] USB-C + Ethernet rear panel
- [ ] Firmware (ESPHome)
  - [x] mmWave sensor selection (DFRobot C4001)
  - [ ] mmWave sensor ESPHome configuration
  - [ ] PIR sensor selection and integration
  - [ ] Lux sensor selection and setup
  - [ ] Multi-mode power management
- [ ] Enclosure (3D Models)
  - [ ] Main housing design
  - [ ] Mounting brackets
  - [ ] Sensor windows/covers
- [x] Documentation
  - [x] mmWave sensor documentation ([DFRobot C4001](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md))
  - [ ] PIR sensor documentation
  - [ ] Light sensor documentation
  - [ ] Bill of Materials (BOM)
  - [ ] Assembly guide
  - [ ] Installation instructions
  - [ ] ESPHome configuration examples

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
├── docs/                  # Documentation
│   ├── sensors/           # Sensor technical documentation ✓
│   │   ├── SENSORS_INDEX.md
│   │   └── dfrobot-c4001/
│   │       ├── C4001_TECHNICAL_GUIDE.md
│   │       └── datasheets/
│   │           └── DATASHEETS_INDEX.md
│   ├── bom.md
│   ├── assembly.md
│   └── installation.md
├── CONTRIBUTING.md        # Contribution guidelines ✓
├── LICENSE.md             # Project license ✓
└── README.md              # This file
```

---

## Getting Started

### Prerequisites

- **Hardware:**
  - [DFRobot C4001 mmWave sensor](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md) (SEN0609)
  - PIR sensor (TBD)
  - Ambient light sensor (TBD)
  - Supporting components (see BOM - coming soon)

- **Software:**
  - [KiCad 8.0+](https://www.kicad.org/) (for PCB modifications)
  - [ESPHome](https://esphome.io/) (for firmware)
  - [Home Assistant](https://www.home-assistant.io/) (optional, recommended)

### Sensor Documentation

Detailed technical documentation for selected sensors:
- **[DFRobot C4001 mmWave Radar](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md)** - Complete UART protocol, pinouts, ESPHome integration

### Build Instructions

*Coming soon - Hardware and firmware in development*

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
- **PIR:** TBD (model selection in progress)
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

- **Issues:** [GitHub Issues](https://github.com/Soriarty/HaloSense/issues) - Bug reports and feature requests
- **Discussions:** [GitHub Discussions](https://github.com/Soriarty/HaloSense/discussions) - General questions and community
- **Contributing:** [Contribution Guidelines](CONTRIBUTING.md) - How to contribute
- **Documentation:**
  - [Sensor Documentation Index](https://github.com/Soriarty/HaloSense/blob/main/docs/sensors/SENSORS_INDEX.md)
  - [Git Flow Workflow](https://github.com/Soriarty/HaloSense/blob/main/docs/GITFLOW.md)
  - [Conventional Commits Guide](https://github.com/Soriarty/HaloSense/blob/main/docs/CONVENTIONAL_COMMITS.md)
  - [Versioning Guide](https://github.com/Soriarty/HaloSense/blob/main/docs/VERSIONING.md)
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
