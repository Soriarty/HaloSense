# HaloSense Technical Documentation

This directory contains all technical and developer documentation for the HaloSense project.

## 📚 Documentation Structure

### 🔧 [Hardware Documentation](hardware/README.md)

Hardware design specifications and analysis:

- **[Power Budget Analysis](hardware/power-budget.md)** - Complete power consumption breakdown
  - Component-by-component analysis
  - PoE budget verification (1.3W typical / 15.4W available)
  - USB-C power scenarios
  - MSL rating vs power trade-off analysis

- **[IP Rating Guide](hardware/ip-rating.md)** - IP54 enclosure design specifications
  - IEC 60529 standard explained
  - IP54 target requirements (dust protected + splash water)
  - Enclosure design checklist
  - MSL rating correlation for component selection
  - DIY testing procedures

### 📡 [Sensor Documentation](sensors/README.md)

Complete technical specifications for all sensors:

- **[DFRobot C4001](sensors/dfrobot-c4001/README.md)** - 24GHz mmWave radar sensor
  - UART protocol specification
  - ESPHome integration examples
  - Detection range: 1.2-25m

- **[Panasonic EKMC1604111](sensors/panasonic-ekmc1604111/README.md)** - PIR motion sensor
  - Digital GPIO interface
  - Three-step lens detection zones
  - <0.1s response time

- **[ROHM BH1750FVI](sensors/rohm-bh1750/README.md)** - Ambient light sensor
  - I2C interface (0x23/0x5C)
  - 1-65,535 lx range
  - ESPHome native support

### 🛠️ [Development Workflows](development/README.md)

Developer guides, standards, and best practices:

- **[Git Flow Workflow](development/git-flow.md)** - Branching strategy and PR process
- **[Conventional Commits](development/conventional-commits.md)** - Commit message format standards
- **[Semantic Versioning](development/versioning.md)** - Version numbering strategy
- **[Branch Protection](development/branch-protection.md)** - GitHub protection rules
- **[GitHub Wiki Strategy](development/github-wiki.md)** - Wiki management workflow

## 📖 User Documentation

**User-facing documentation (assembly, installation, troubleshooting) is available on the GitHub Wiki:**

👉 **[HaloSense Wiki](https://github.com/Soriarty/HaloSense/wiki)**

The Wiki includes:
- Getting Started guide
- Bill of Materials
- Assembly instructions
- Installation guide
- ESPHome configuration examples
- Home Assistant integration
- FAQ and troubleshooting

## 🗂️ Documentation Philosophy

**Two-tier documentation system:**

| Documentation Type | Location | Audience | Content |
|-------------------|----------|----------|---------|
| **User Documentation** | [GitHub Wiki](https://github.com/Soriarty/HaloSense/wiki) | End users, builders | How to build, configure, install, troubleshoot |
| **Technical Documentation** | `docs/` (this directory) | Developers, contributors | Technical specs, workflows, design analysis |

This separation ensures:
- **Wiki:** Beginner-friendly, practical, step-by-step guides
- **docs/:** Technical depth, engineering specifications, development standards

## 🔗 Quick Links

- **[Main Project README](../README.md)** - Project overview and features
- **[Contributing Guidelines](../CONTRIBUTING.md)** - How to contribute
- **[Firmware Guide](../firmware/FIRMWARE_GUIDE.md)** - ESPHome configuration reference
- **[GitHub Wiki](https://github.com/Soriarty/HaloSense/wiki)** - User documentation

---

**Last Updated:** 2025-11-29
