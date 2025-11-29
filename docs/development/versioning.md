# Versioning Guide

Semantic Versioning (SemVer) specification for the HaloSense project.

## Overview

HaloSense follows [Semantic Versioning 2.0.0](https://semver.org/) to provide predictable version numbers that convey meaning about the underlying changes.

Combined with [Conventional Commits](CONVENTIONAL_COMMITS.md), version numbers are automatically determined based on commit messages.

---

## Version Format

```
MAJOR.MINOR.PATCH[-PRERELEASE][+BUILD]
```

**Example:** `1.4.2-beta.1+20231128`

- **MAJOR** version: Incompatible API/hardware changes
- **MINOR** version: Backwards-compatible new features
- **PATCH** version: Backwards-compatible bug fixes
- **PRERELEASE** (optional): Pre-release version identifier
- **BUILD** (optional): Build metadata

---

## Version Components

### MAJOR Version (X.0.0)

Increment when making **incompatible changes**:

**Hardware (PCB/Schematic):**
- Pin assignment changes that break compatibility
- Component changes requiring new firmware
- PCB footprint incompatible with previous enclosure
- Power requirements change (voltage, PoE standard)
- Connector type changes (USB-C to different connector)

**Firmware:**
- Breaking ESPHome configuration changes
- Sensor protocol changes requiring re-configuration
- Network protocol changes
- Home Assistant integration breaks

**Enclosure:**
- Dimensions change incompatible with previous PCB
- Mounting mechanism fundamentally changes
- Sensor window placement changes

**Examples:**
```
1.0.0 → 2.0.0: USB-C replaced with different connector
1.2.3 → 2.0.0: ESP32 GPIO assignments changed, firmware incompatible
1.5.0 → 2.0.0: Enclosure redesigned, not compatible with v1.x PCB
```

### MINOR Version (0.X.0)

Increment when adding **backwards-compatible functionality**:

**Hardware:**
- New optional sensor added
- Additional GPIO broken out
- New optional features (e.g., external antenna connector)
- Power optimization (lower consumption)

**Firmware:**
- New sensor support added
- New configuration options
- New Home Assistant entities
- Performance improvements
- New optional features

**Enclosure:**
- New mounting bracket option added
- Additional cable routing options
- Ventilation improvements

**Examples:**
```
1.0.0 → 1.1.0: Added optional temperature sensor
1.2.0 → 1.3.0: Added MQTT support alongside existing HA API
1.4.0 → 1.5.0: New desk mounting bracket added
```

### PATCH Version (0.0.X)

Increment when making **backwards-compatible bug fixes**:

**Hardware:**
- Silkscreen corrections
- Footprint optimizations (same component, better placement)
- BOM cost reductions (compatible alternatives)
- Manufacturing improvements

**Firmware:**
- Bug fixes
- Documentation corrections
- Minor optimizations
- Security patches

**Enclosure:**
- Print quality improvements
- Minor dimensional tweaks (within tolerance)
- Surface finish improvements

**Examples:**
```
1.0.0 → 1.0.1: Fixed incorrect resistor value on PCB
1.2.3 → 1.2.4: Fixed UART timeout bug in firmware
1.4.0 → 1.4.1: Fixed 3D print bridging issue in enclosure
```

---

## Pre-release Versions

Format: `MAJOR.MINOR.PATCH-PRERELEASE`

### Pre-release Identifiers

**alpha** - Early testing, unstable
```
1.0.0-alpha.1
1.0.0-alpha.2
```

**beta** - Feature complete, testing for bugs
```
1.0.0-beta.1
1.0.0-beta.2
```

**rc** (Release Candidate) - Potentially final, final testing
```
1.0.0-rc.1
1.0.0-rc.2
```

### Pre-release Progression

```
Development → Alpha → Beta → RC → Release

0.1.0-alpha.1    First alpha
0.1.0-alpha.2    Second alpha (fixes)
0.1.0-beta.1     First beta
0.1.0-beta.2     Second beta (fixes)
0.1.0-rc.1       Release candidate 1
0.1.0-rc.2       Release candidate 2 (final fixes)
0.1.0            Official release
```

---

## Version 0.x.x (Initial Development)

**Status:** Project is in initial development

During initial development (version 0.x.x):
- Public API should not be considered stable
- Breaking changes may occur in MINOR versions
- Version 0.x.x indicates the project is not yet production-ready

**Current Phase:** 0.1.0-alpha (Early development)

**Progression to 1.0.0:**
```
0.1.0-alpha.1    Initial hardware design
0.1.0-alpha.2    Firmware development begins
0.2.0-alpha.1    Enclosure design added
0.3.0-beta.1     All components integrated, testing
0.3.0-beta.2     Bug fixes from testing
0.3.0-rc.1       Release candidate
1.0.0            First stable release
```

---

## Commit Type to Version Mapping

When using [Conventional Commits](CONVENTIONAL_COMMITS.md):

| Commit Type | Version Increment | Example |
|-------------|-------------------|---------|
| `feat` | MINOR (0.X.0) | 1.2.0 → 1.3.0 |
| `fix` | PATCH (0.0.X) | 1.2.3 → 1.2.4 |
| `perf` | PATCH (0.0.X) | 1.2.3 → 1.2.4 |
| `docs` | No version change | - |
| `style` | No version change | - |
| `refactor` | No version change | - |
| `test` | No version change | - |
| `build` | No version change | - |
| `ci` | No version change | - |
| `chore` | No version change | - |
| **BREAKING CHANGE** | MAJOR (X.0.0) | 1.2.3 → 2.0.0 |

**Note:** `BREAKING CHANGE` in commit footer triggers MAJOR version bump regardless of type.

---

## Component Versioning

HaloSense has three main components, each with independent versions:

### Hardware Version

**Format:** `HW-MAJOR.MINOR.PATCH`

**Examples:**
- `HW-1.0.0` - First production hardware
- `HW-1.1.0` - Added optional temperature sensor
- `HW-1.1.1` - Fixed silkscreen error
- `HW-2.0.0` - Changed USB connector (breaking)

**Marked on:**
- PCB silkscreen
- Schematic title block
- BOM header

### Firmware Version

**Format:** `FW-MAJOR.MINOR.PATCH`

**Examples:**
- `FW-1.0.0` - Initial stable firmware
- `FW-1.1.0` - Added MQTT support
- `FW-1.1.1` - Fixed sensor timeout
- `FW-2.0.0` - New config format (breaking)

**Stored in:**
- `firmware/halosense.yaml` substitutions
- ESPHome device info
- OTA update metadata

### Enclosure Version

**Format:** `EN-MAJOR.MINOR.PATCH`

**Examples:**
- `EN-1.0.0` - First 3D printable enclosure
- `EN-1.1.0` - Added cable management clips
- `EN-1.0.1` - Fixed print bridging issue
- `EN-2.0.0` - New mounting system (breaking)

**Marked in:**
- STL file metadata
- STEP file annotations
- Printed on enclosure base

### Full Product Version

**Format:** `vMAJOR.MINOR.PATCH`

Overall project version tracking all components together:

**Example:** `v1.2.0`
- Hardware: HW-1.1.0
- Firmware: FW-1.2.3
- Enclosure: EN-1.1.1

---

## Release Process

### 1. Development

Make changes following [Conventional Commits](CONVENTIONAL_COMMITS.md):

```bash
git add .
git commit -m "feat(sensor): add temperature sensor support"
```

### 2. Version Bump (Automated)

Use `standard-version` or `semantic-release`:

```bash
# Determine next version based on commits
npx standard-version

# Or for pre-release
npx standard-version --prerelease alpha
```

This will:
1. Analyze commits since last release
2. Determine version bump (MAJOR/MINOR/PATCH)
3. Update version in files
4. Generate/update CHANGELOG.md
5. Create version commit and tag

### 3. Manual Version Bump

If not using automation:

```bash
# Update version in:
# - firmware/halosense.yaml (substitutions)
# - hardware/schematics/*.kicad_sch (title block)
# - enclosure files metadata

# Commit version bump
git add .
git commit -m "chore(release): bump version to 1.2.0"

# Create tag
git tag -a v1.2.0 -m "Release v1.2.0"
```

### 4. Release

```bash
# Push commits and tags
git push origin main
git push origin v1.2.0
```

---

## Changelog Generation

### Automated (Recommended)

Using `standard-version`:

```bash
npx standard-version
```

Generates `CHANGELOG.md` with sections:

```markdown
# Changelog

## [1.2.0](https://github.com/Soriarty/HaloSense/compare/v1.1.0...v1.2.0) (2024-11-28)

### Features

* **sensor:** add temperature sensor support ([abc1234](https://github.com/Soriarty/HaloSense/commit/abc1234))
* **firmware:** add MQTT integration ([def5678](https://github.com/Soriarty/HaloSense/commit/def5678))

### Bug Fixes

* **esphome:** correct UART timeout ([789abcd](https://github.com/Soriarty/HaloSense/commit/789abcd))
```

### Manual

Update `CHANGELOG.md` following [Keep a Changelog](https://keepachangelog.com/):

```markdown
# Changelog

## [1.2.0] - 2024-11-28

### Added
- Temperature sensor support (optional)
- MQTT integration alongside Home Assistant API
- New desk mounting bracket option

### Fixed
- UART timeout issue with C4001 sensor
- Incorrect voltage regulator on PCB

### Changed
- Improved enclosure ventilation
- Optimized power consumption

### Breaking Changes
None
```

---

## Version Compatibility Matrix

Track compatibility between component versions:

| Project | Hardware | Firmware | Enclosure | Notes |
|---------|----------|----------|-----------|-------|
| v1.0.0 | HW-1.0.0 | FW-1.0.0 | EN-1.0.0 | Initial release |
| v1.1.0 | HW-1.1.0 | FW-1.1.0 | EN-1.0.0 | Added temp sensor |
| v1.2.0 | HW-1.1.0 | FW-1.2.0 | EN-1.1.0 | MQTT + new bracket |
| v2.0.0 | HW-2.0.0 | FW-2.0.0 | EN-2.0.0 | Complete redesign |

**Compatibility Notes:**
- Firmware FW-1.2.x works with Hardware HW-1.1.0 and HW-1.0.0
- Enclosure EN-1.1.0 fits Hardware HW-1.1.0 and HW-1.0.0
- Firmware FW-2.x.x ONLY works with Hardware HW-2.0.0+

---

## Tags and Branches

### Git Tags

**Format:** `vMAJOR.MINOR.PATCH[-PRERELEASE]`

```bash
# Release tags
v1.0.0
v1.1.0
v1.2.0

# Pre-release tags
v1.0.0-alpha.1
v1.0.0-beta.1
v1.0.0-rc.1

# Component-specific tags (optional)
hw-1.0.0
fw-1.2.0
en-1.1.0
```

### Branches

```
main              # Stable releases only
develop           # Development branch
feature/*         # New features
fix/*             # Bug fixes
release/v1.2.0    # Release preparation
hotfix/v1.1.1     # Emergency fixes
```

---

## Tools and Automation

### standard-version

**Install:**
```bash
npm install --save-dev standard-version
```

**Usage:**
```bash
# Regular release
npx standard-version

# Pre-release
npx standard-version --prerelease alpha

# First release
npx standard-version --first-release

# Specific version
npx standard-version --release-as 2.0.0
```

### semantic-release

For fully automated releases on CI/CD:

**Install:**
```bash
npm install --save-dev semantic-release
```

**Configuration (.releaserc.json):**
```json
{
  "branches": ["main"],
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator",
    "@semantic-release/changelog",
    "@semantic-release/github",
    "@semantic-release/git"
  ]
}
```

### Version Scripts (package.json)

```json
{
  "scripts": {
    "release": "standard-version",
    "release:minor": "standard-version --release-as minor",
    "release:major": "standard-version --release-as major",
    "release:alpha": "standard-version --prerelease alpha",
    "release:beta": "standard-version --prerelease beta",
    "release:rc": "standard-version --prerelease rc"
  }
}
```

---

## Examples

### Feature Addition (MINOR bump)

```bash
# Make changes
git add firmware/halosense.yaml
git commit -m "feat(sensor): add BH1750 light sensor support

Add support for BH1750 ambient light sensor with I2C interface.
Includes ESPHome configuration and calibration settings.

Closes #67"

# Bump version (1.1.0 → 1.2.0)
npx standard-version

# Push
git push --follow-tags origin main
```

### Bug Fix (PATCH bump)

```bash
# Fix bug
git add firmware/halosense.yaml
git commit -m "fix(esphome): correct sensor update interval

Change update interval from 30s to 60s to prevent sensor overload.

Fixes #72"

# Bump version (1.2.0 → 1.2.1)
npx standard-version

# Push
git push --follow-tags origin main
```

### Breaking Change (MAJOR bump)

```bash
# Make breaking change
git add hardware/schematics/
git commit -m "feat(pcb): replace USB-C with USB-B connector

Switch to USB-B connector for increased durability in industrial
environments.

BREAKING CHANGE: USB-C connector replaced with USB-B. Existing cables
and enclosures with USB-C cutouts are not compatible. Update enclosure
design and inform users to use USB-B cables.

Closes #85"

# Bump version (1.2.1 → 2.0.0)
npx standard-version

# Push
git push --follow-tags origin main
```

---

## Version History

### Planned Releases

- `0.1.0-alpha.1` - Initial hardware design (Current)
- `0.2.0-alpha.1` - Firmware development complete
- `0.3.0-beta.1` - Full integration testing
- `1.0.0` - First stable release

### Release Targets

- **v1.0.0:** Full production-ready design (Hardware + Firmware + Enclosure)
- **v1.1.0:** Additional sensor support (temperature, humidity)
- **v1.2.0:** Advanced features (multi-zone detection, MQTT)
- **v2.0.0:** Next-generation hardware (ESP32-S3, WiFi 6)

---

## References

- [Semantic Versioning 2.0.0](https://semver.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [standard-version](https://github.com/conventional-changelog/standard-version)
- [semantic-release](https://semantic-release.gitbook.io/)

---

## Questions?

For versioning questions:
1. Check this guide and examples
2. Review [Conventional Commits Guide](CONVENTIONAL_COMMITS.md)
3. Ask in [Discussions](https://github.com/Soriarty/HaloSense/discussions)
4. See [CONTRIBUTING.md](../CONTRIBUTING.md)

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28
