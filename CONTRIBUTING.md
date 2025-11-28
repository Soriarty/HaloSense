# Contributing to HaloSense

First off, thank you for considering contributing to HaloSense! It's people like you that make HaloSense such a great project for the DIY smart home community.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
  - [Hardware Design](#hardware-design)
  - [Firmware Development](#firmware-development)
  - [Enclosure Design](#enclosure-design)
  - [Documentation](#documentation)
  - [Bug Reports](#bug-reports)
  - [Feature Requests](#feature-requests)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Style Guidelines](#style-guidelines)
  - [Git Commit Messages](#git-commit-messages)
  - [Versioning](#versioning)
- [Community](#community)

---

## Code of Conduct

This project and everyone participating in it is governed by basic principles of respect and collaboration:

- **Be respectful** - Treat everyone with respect. Healthy debate is encouraged, personal attacks are not.
- **Be constructive** - Provide helpful feedback. If you disagree, explain why and suggest alternatives.
- **Be inclusive** - Welcome newcomers and help them learn. We all started somewhere.
- **Be patient** - This is a volunteer project. Maintainers respond as time permits.

By participating, you are expected to uphold these principles.

---

## How Can I Contribute?

### Hardware Design

**Areas for contribution:**
- PCB layout improvements
- Component selection and optimization
- Power management enhancements
- Signal integrity improvements
- Cost reduction suggestions

**Requirements:**
- All hardware changes must include:
  - Updated KiCad schematics (`.kicad_sch`)
  - Updated PCB layout (`.kicad_pcb`)
  - Updated Bill of Materials (BOM)
  - Clear explanation of changes and rationale
  - Photos/renders of physical prototypes (if available)

**Before starting major hardware changes:**
- Open an issue to discuss your proposed changes
- Check if someone is already working on similar improvements
- Consider backward compatibility with existing builds

**Testing requirements:**
- Prototype and test your changes
- Document test results (power consumption, signal quality, etc.)
- Verify compatibility with all supported power modes (PoE, USB-C, hybrid)

### Firmware Development

**Areas for contribution:**
- ESPHome configuration improvements
- Sensor integration and calibration
- Power management optimization
- Home Assistant automation examples
- Bug fixes

**Requirements:**
- All firmware changes must:
  - Be tested on actual hardware (or clearly marked as untested)
  - Include comments explaining logic
  - Follow ESPHome best practices
  - Work with the latest stable ESPHome release
  - Be documented in configuration comments

**Testing requirements:**
- Test all affected sensor modes
- Verify power consumption hasn't increased significantly
- Test both PoE and USB-C power modes
- Verify Home Assistant integration still works
- Document any breaking changes

### Enclosure Design

**Areas for contribution:**
- Printability improvements
- Aesthetic enhancements
- Alternative mounting options
- Assembly simplification
- Support for different printer types

**Requirements:**
- All enclosure changes must include:
  - Updated STL files (for printing)
  - Updated STEP files (for editing)
  - Print settings recommendations
  - Assembly instructions
  - Photos of printed parts

**Design considerations:**
- Must be printable without supports (preferred)
- Should work on common FDM printers (220x220x250mm build volume)
- Must provide adequate ventilation for ESP32
- Must accommodate sensor beam angles
- Should be mechanically robust

### Documentation

**Areas for contribution:**
- Sensor documentation for additional components
- Assembly guides with photos
- Installation tutorials
- Troubleshooting guides
- ESPHome configuration examples
- Translations (future)

**Documentation standards:**
- Use clear, concise language
- Include images/diagrams where helpful
- Follow existing documentation structure
- Use Markdown formatting
- Check spelling and grammar
- Test all code examples

**Sensor documentation template:**
When adding documentation for new sensors, follow this structure:
```
docs/sensors/sensor-name/
├── SENSOR_NAME_TECHNICAL_GUIDE.md
└── datasheets/
    ├── DATASHEETS_INDEX.md
    └── *.pdf
```

See [docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md](docs/sensors/dfrobot-c4001/C4001_TECHNICAL_GUIDE.md) as a reference.

### Bug Reports

**Before submitting a bug report:**
- Check existing issues to avoid duplicates
- Update to the latest firmware/hardware revision
- Gather relevant information (see below)

**Bug report should include:**
- Clear description of the problem
- Steps to reproduce
- Expected behavior
- Actual behavior
- Hardware revision (if applicable)
- Firmware configuration (ESPHome YAML)
- Logs/error messages
- Photos/videos if visual issue

**Use this template:**
```markdown
**Describe the bug:**
A clear description of what the bug is.

**To Reproduce:**
1. Step 1
2. Step 2
3. See error

**Expected behavior:**
What you expected to happen.

**Actual behavior:**
What actually happened.

**Environment:**
- Hardware revision: [e.g., v1.0]
- Firmware: [ESPHome version]
- Power mode: [PoE/USB-C/Hybrid]
- Sensors: [list installed sensors]

**Logs:**
```
[Paste relevant logs here]
```

**Additional context:**
Any other relevant information.
```

### Feature Requests

**Before submitting a feature request:**
- Check if it's already been requested
- Consider if it fits the project's scope
- Think about implementation complexity

**Feature request should include:**
- Clear description of the feature
- Use case / problem it solves
- Proposed implementation (if you have ideas)
- Alternatives considered
- Impact on existing functionality

---

## Development Setup

### Hardware Development

**Required software:**
- [KiCad 8.0+](https://www.kicad.org/)
- [OLIMEX ESP32-POE reference design](https://github.com/OLIMEX/ESP32-POE) (for reference)

**Recommended:**
- Git for version control
- KiCad library management tool

### Firmware Development

**Required software:**
- [ESPHome](https://esphome.io/)
- [Home Assistant](https://www.home-assistant.io/) (for testing)
- Python 3.8+ (for ESPHome)

**Development workflow:**
```bash
# Clone the repository
git clone https://github.com/Soriarty/HaloSense.git
cd HaloSense

# Install ESPHome
pip install esphome

# Validate configuration
esphome config firmware/halosense.yaml

# Compile
esphome compile firmware/halosense.yaml

# Upload to device
esphome upload firmware/halosense.yaml
```

### Enclosure Development

**Required software:**
- CAD software supporting STEP format (FreeCAD, Fusion 360, etc.)
- 3D slicer (Cura, PrusaSlicer, etc.)

**Testing:**
- Print prototypes before submitting
- Test fit with actual PCB
- Verify sensor windows don't obstruct beams

---

## Pull Request Process

### Before Creating a PR

1. **Fork the repository** to your GitHub account
2. **Create a feature branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```
   Or for bug fixes:
   ```bash
   git checkout -b fix/bug-description
   ```

3. **Make your changes** following the style guidelines

4. **Test thoroughly** according to the requirements for your change type

5. **Commit your changes** following [Conventional Commits](docs/CONVENTIONAL_COMMITS.md):
   ```bash
   git commit -m "feat(sensor): add DFRobot C4001 documentation"
   ```

   Good commit message examples:
   - `docs(sensor): add DFRobot C4001 technical guide`
   - `fix(esphome): correct UART baud rate configuration`
   - `feat(enclosure): improve wall thickness for better strength`
   - `docs(bom): add alternative component sources`

6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

### Creating the Pull Request

1. **Open a Pull Request** from your fork to the main repository

2. **Fill out the PR template** with:
   - Description of changes
   - Related issue (if applicable)
   - Type of change (hardware/firmware/enclosure/docs)
   - Testing performed
   - Screenshots/photos (if applicable)

3. **PR title format:**
   - Hardware: `[Hardware] Brief description`
   - Firmware: `[Firmware] Brief description`
   - Enclosure: `[Enclosure] Brief description`
   - Docs: `[Docs] Brief description`
   - Multiple: `[Hardware/Firmware] Brief description`

### PR Review Process

1. **Maintainer review** - A project maintainer will review your PR
2. **Feedback** - Address any requested changes
3. **Testing** - Changes may be tested by maintainers or community
4. **Approval** - Once approved, your PR will be merged
5. **Credit** - You'll be credited in the commit and release notes

### After Your PR is Merged

- Delete your feature branch (optional)
- Pull the latest changes from main
- Your contribution is now part of HaloSense! 🎉

---

## Style Guidelines

### Git Commit Messages

**HaloSense follows [Conventional Commits](docs/CONVENTIONAL_COMMITS.md) specification.**

**Format:**
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Quick Reference:**
- **Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`
- **Scopes:** `pcb`, `schematic`, `bom`, `esphome`, `sensor`, `network`, `3d-model`, `mounting`, `docs`, etc.
- **Subject:** Imperative mood, lowercase, no period, max 72 characters
- **Footer:** `Closes #123`, `Fixes #456`, `BREAKING CHANGE: description`

**Examples:**
```bash
feat(sensor): add DFRobot C4001 mmWave radar support
fix(esphome): correct UART baud rate for C4001
docs: update installation guide with PoE setup
```

**Setup commit template:**
```bash
git config commit.template .github/COMMIT_TEMPLATE.md
```

**Detailed guide:** See [docs/CONVENTIONAL_COMMITS.md](docs/CONVENTIONAL_COMMITS.md)

### Versioning

**HaloSense follows [Semantic Versioning 2.0.0](docs/VERSIONING.md).**

**Version Format:** `MAJOR.MINOR.PATCH[-PRERELEASE]`

**Version Bumps:**
- **MAJOR (X.0.0):** Breaking changes (incompatible hardware/firmware)
- **MINOR (0.X.0):** New features (backwards-compatible)
- **PATCH (0.0.X):** Bug fixes (backwards-compatible)

**Examples:**
- `feat(sensor)` → MINOR bump (1.2.0 → 1.3.0)
- `fix(esphome)` → PATCH bump (1.2.3 → 1.2.4)
- `feat` with `BREAKING CHANGE:` → MAJOR bump (1.2.3 → 2.0.0)

**Component Versions:**
- Hardware: `HW-1.0.0` (marked on PCB silkscreen)
- Firmware: `FW-1.0.0` (in halosense.yaml)
- Enclosure: `EN-1.0.0` (in STL metadata)

**Automated Versioning:**
```bash
# Install standard-version
npm install --save-dev standard-version

# Bump version based on commits
npx standard-version

# Pre-release
npx standard-version --prerelease alpha
```

**Detailed guide:** See [docs/VERSIONING.md](docs/VERSIONING.md)

### KiCad Design Files

- Use consistent grid settings (5mil for PCB routing)
- Follow KiCad design rule conventions
- Include reference designators (R1, C1, etc.)
- Use meaningful net names
- Group related components logically
- Include version number in schematic title block

### ESPHome Configuration

- Use consistent indentation (2 spaces)
- Add comments explaining non-obvious configurations
- Group related settings together
- Use meaningful entity names
- Include units in sensor names where applicable
- Format example:
  ```yaml
  sensor:
    - platform: dfrobot_c4001
      uart_id: uart_radar
      presence:
        name: "Living Room Presence"  # Clear, descriptive name
        id: presence_sensor
      update_interval: 1s  # Include units
  ```

### Markdown Documentation

- Use ATX-style headers (`#` not underlines)
- One sentence per line (makes diffs clearer)
- Use fenced code blocks with language tags
- Include alt text for images
- Use relative links for internal documentation
- Check links aren't broken

### 3D Model Files

- Use standard units (millimeters)
- Name parts descriptively
- Include assembly relationships in STEP files
- Center parts at origin when possible
- Use consistent orientation (Z-up preferred)

---

## Community

### Communication Channels

- **GitHub Issues** - Bug reports, feature requests, technical discussions
- **GitHub Discussions** - General questions, ideas, showcasing builds
- **Pull Requests** - Code/design reviews and collaboration

### Getting Help

If you're stuck or need help:

1. Check existing documentation
2. Search closed issues for similar problems
3. Ask in GitHub Discussions
4. Open an issue with a clear description of your problem

### Recognition

Contributors will be:
- Credited in commit messages and release notes
- Listed in project acknowledgments
- Welcomed as valued community members

Significant contributors may be offered maintainer status.

---

## License

By contributing to HaloSense, you agree that your contributions will be licensed under the same [CC BY-NC-SA 4.0](LICENSE.md) license that covers the project.

For commercial licensing discussions, contact [@Soriarty](https://github.com/Soriarty).

---

## Questions?

If you have questions about contributing:

- Open a [GitHub Discussion](https://github.com/Soriarty/HaloSense/discussions)
- Check the [main README](README.md)
- Review existing PRs to see examples

---

**Thank you for contributing to HaloSense!**

Every contribution, no matter how small, helps make this project better for the entire DIY smart home community.

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense
