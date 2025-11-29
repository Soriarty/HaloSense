# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial project structure and documentation
- Complete sensor documentation for DFRobot C4001 mmWave radar
- Complete sensor documentation for Panasonic EKMC1604111 PIR sensor
- Complete sensor documentation for ROHM BH1750FVI light sensor
- Power budget analysis document (comprehensive system power consumption)
- IP rating guide (IP54 enclosure design specifications)
- Conventional Commits specification and guide
- Semantic Versioning guide
- Contribution guidelines
- Git Flow workflow documentation
- Branch protection configuration guide
- GitHub Wiki as Git submodule
- Comprehensive Wiki with 15 user-facing pages
- Hardware design framework (placeholders)
- Firmware structure (ESPHome configuration)
- Enclosure design framework (placeholders)

### Documentation
- **Developer Documentation (docs/):**
  - Comprehensive technical guide for DFRobot C4001 mmWave sensor (UART protocol, ESPHome)
  - Comprehensive technical guide for Panasonic EKMC1604111 PIR sensor (GPIO, detection zones)
  - Comprehensive technical guide for ROHM BH1750FVI light sensor (I2C protocol, ESPHome)
  - Power budget analysis (1.3W typical, 10× PoE margin, component-by-component breakdown)
  - IP rating guide (IP54 target, enclosure design checklist, MSL correlation)
  - SENSORS_INDEX.md with complete GPIO allocation and power summary
  - Git Flow workflow guide
  - Conventional Commits guide
  - Semantic Versioning guide
  - Branch Protection configuration
  - GitHub Wiki strategy and architecture
- **User Documentation (Wiki):**
  - Professional Home page with navigation
  - Getting Started guide
  - Bill of Materials with sourcing info
  - Assembly guide with step-by-step instructions
  - Installation guide for setup and configuration
  - FAQ with 50+ questions and answers
  - Troubleshooting guide with detailed solutions
  - Placeholder pages for future content

### Changed
- Migrated user-facing documentation from docs/ to Wiki
- Converted docs/assembly.md, docs/bom.md, docs/installation.md to Wiki redirects
- Reorganized documentation: Wiki (users) vs docs/ (developers)

### Infrastructure
- Set up Git Flow branching strategy (main, develop, feature/*, release/*, hotfix/*)
- Configured branch protection for main and develop branches
- Added Wiki repository as Git submodule at docs/wiki/
- Enabled commitlint validation for Conventional Commits
- Configured standard-version for automated versioning

## [0.1.0-alpha.1] - 2025-11-28

### Added
- Initial repository setup
- Project README with specifications
- License (CC BY-NC-SA 4.0)
- Basic project structure
- Documentation framework

### Project Status
**Current Phase:** Early development - Documentation and planning

**Completed:**
- ✅ Project structure and repository organization
- ✅ Sensor selection and documentation (all 3 sensors complete)
  - ✅ mmWave radar: DFRobot C4001 (SEN0609)
  - ✅ PIR motion: Panasonic EKMC1604111
  - ✅ Ambient light: ROHM BH1750FVI (MSL 3 uniformity)
- ✅ Power budget analysis (1.3W typical, excellent PoE margin)
- ✅ IP rating specifications (IP54 target for kitchen/bathroom)
- ✅ Contribution guidelines
- ✅ Conventional Commits implementation with validation
- ✅ Semantic Versioning strategy
- ✅ Git Flow workflow with branch protection
- ✅ GitHub Wiki with comprehensive user documentation
- ✅ Developer documentation (technical specs, workflows)

**In Progress:**
- 🔨 Hardware design planning (KiCad schematic/PCB)
- 🔨 Firmware development planning (ESPHome YAML)

**Planned:**
- 📋 Hardware design (KiCad PCB)
- 📋 Firmware implementation (ESPHome)
- 📋 Enclosure design (3D models)
- 📋 Prototyping and testing
- 📋 First stable release (v1.0.0)

---

**Project:** HaloSense
**Repository:** https://github.com/Soriarty/HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)

[Unreleased]: https://github.com/Soriarty/HaloSense/compare/v0.1.0-alpha.1...HEAD
[0.1.0-alpha.1]: https://github.com/Soriarty/HaloSense/releases/tag/v0.1.0-alpha.1
