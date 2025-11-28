# Conventional Commits Guide

Conventional Commits specification for the HaloSense project.

## Overview

HaloSense follows the [Conventional Commits](https://www.conventionalcommits.org/) specification to maintain a clear, structured commit history that enables automated versioning and changelog generation.

## Commit Message Format

Each commit message consists of a **header**, **body**, and **footer**:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Header (Required)

The header has a special format that includes a **type**, **scope**, and **subject**:

```
<type>(<scope>): <subject>
```

**Rules:**
- Maximum 72 characters
- Lowercase type and scope
- Subject in imperative mood ("add" not "added" or "adds")
- No period at the end

### Type (Required)

Must be one of the following:

- **feat**: New feature for the user
- **fix**: Bug fix for the user
- **docs**: Documentation only changes
- **style**: Changes that don't affect code meaning (white-space, formatting, etc.)
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **build**: Changes that affect the build system or external dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files
- **revert**: Reverts a previous commit

### Scope (Optional)

The scope provides additional context and should be a noun describing a section of the codebase:

**Hardware:**
- `pcb` - PCB design changes
- `schematic` - Schematic changes
- `bom` - Bill of materials updates

**Firmware:**
- `esphome` - ESPHome configuration
- `sensor` - Sensor integration
- `network` - Network configuration
- `power` - Power management

**Enclosure:**
- `3d-model` - 3D model changes
- `mounting` - Mounting bracket changes

**Documentation:**
- `docs` - General documentation
- `readme` - README updates
- `guide` - Guide updates

**Project:**
- `deps` - Dependency updates
- `config` - Configuration changes
- `release` - Release-related changes

### Subject (Required)

Brief description of the change:

- Use imperative, present tense: "change" not "changed" nor "changes"
- Don't capitalize first letter
- No period (.) at the end
- Maximum 50 characters

### Body (Optional)

Detailed description of the change:

- Use imperative, present tense
- Include motivation for the change
- Contrast with previous behavior
- Wrap at 72 characters

### Footer (Optional)

The footer should contain:

**Breaking Changes:**
```
BREAKING CHANGE: <description>
```

**Issue References:**
```
Closes #123
Fixes #456
Relates to #789
```

**Co-authors:**
```
Co-authored-by: Name <email@example.com>
```

---

## Examples

### Feature Addition

```
feat(sensor): add DFRobot C4001 mmWave radar integration

Implement complete UART protocol support for C4001 sensor including:
- Presence detection mode
- Distance/velocity measurement mode
- Configuration commands (setRange, setSensitivity)
- Data parsing for both output formats

Closes #15
```

### Bug Fix

```
fix(esphome): correct UART baud rate for C4001

Change default baud rate from 9600 to 115200 to match C4001
specifications. Previous rate caused communication errors.

Fixes #23
```

### Documentation Update

```
docs(sensor): update C4001 technical guide with UART protocol

Add complete UART command reference extracted from official
communication protocol PDF. Includes all configuration commands
and data format specifications.
```

### Breaking Change

```
feat(pcb): change USB connector from Micro-USB to USB-C

BREAKING CHANGE: USB-C connector replaces Micro-USB. Existing
enclosures and cables will not be compatible. Update enclosure
design and BOM accordingly.

Closes #42
```

### Hardware Change

```
feat(pcb): add PoE module footprint to mainboard

Add footprint for IEEE 802.3af PoE module on PCB. Includes
isolation transformer, rectifier, and regulation circuitry.
Power budget increased to 5W typical, 8W peak.

Relates to #18
```

### Enclosure Update

```
feat(3d-model): add wall mounting bracket

Create wall mounting bracket with cable management features.
Includes keyhole slots for easy installation and cable routing
channels for clean appearance.

Closes #31
```

### Firmware Refactoring

```
refactor(esphome): restructure sensor configuration

Move sensor definitions into separate YAML packages for better
organization. No functional changes.
```

### Dependency Update

```
chore(deps): update ESPHome to 2024.11.0

Update ESPHome dependency for bug fixes and new features.
Tested with existing configuration, no breaking changes.
```

### Revert

```
revert: feat(pcb): add PoE module footprint

This reverts commit abc1234def5678. PoE module footprint conflicts
with planned sensor placement. Will redesign layout before
reintroducing.

Relates to #18
```

---

## Commit Message Template

Use this template for your commits (available in `.github/COMMIT_TEMPLATE.md`):

```
# <type>(<scope>): <subject>
# |<----  Using a Maximum Of 72 Characters  ---->|

# Explain why this change is being made
# |<----   Try To Limit Each Line to a Maximum Of 72 Characters   ---->|

# Provide links or keys to any relevant tickets, articles or other resources
# Example: Closes #23

# --- COMMIT END ---
# Type can be
#    feat     (new feature)
#    fix      (bug fix)
#    refactor (refactoring code)
#    style    (formatting, missing semi colons, etc; no code change)
#    docs     (changes to documentation)
#    test     (adding or refactoring tests; no production code change)
#    chore    (updating grunt tasks etc; no production code change)
#    perf     (performance improvements)
#    build    (build system changes)
#    ci       (CI configuration changes)
#    revert   (revert a previous commit)
# --------------------
# Scope is optional and can be anything specifying place of the commit change
# Subject should use imperative tone and say what the commit does
# Body should explain why the change is being made
# --------------------
# Remember to:
#   - Use the imperative mood in the subject line
#   - Do not end the subject line with a period
#   - Capitalize the subject line and each paragraph
#   - Separate subject from body with a blank line
#   - Use the body to explain what and why vs. how
#   - Can use multiple lines with "-" or "*" for bullet points in body
# --------------------
# Breaking changes:
#   - Add "BREAKING CHANGE:" in the footer
#   - Describe what breaks and migration path
# --------------------
```

---

## Setup Git Commit Template

Configure your local repository to use the commit template:

```bash
cd /path/to/HaloSense
git config commit.template .github/COMMIT_TEMPLATE.md
```

Or globally for all repositories:

```bash
git config --global commit.template ~/.gitmessage
cp .github/COMMIT_TEMPLATE.md ~/.gitmessage
```

---

## Validation

### Pre-commit Hook (Optional)

You can use [commitlint](https://commitlint.js.org/) to automatically validate commit messages:

**Install:**
```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional
```

**Configure (.commitlintrc.json):**
```json
{
  "extends": ["@commitlint/config-conventional"],
  "rules": {
    "type-enum": [
      2,
      "always",
      [
        "feat",
        "fix",
        "docs",
        "style",
        "refactor",
        "perf",
        "test",
        "build",
        "ci",
        "chore",
        "revert"
      ]
    ],
    "scope-enum": [
      2,
      "always",
      [
        "pcb",
        "schematic",
        "bom",
        "esphome",
        "sensor",
        "network",
        "power",
        "3d-model",
        "mounting",
        "docs",
        "readme",
        "guide",
        "deps",
        "config",
        "release"
      ]
    ],
    "subject-max-length": [2, "always", 72],
    "header-max-length": [2, "always", 72]
  }
}
```

---

## Automated Changelog Generation

Conventional commits enable automated changelog generation using tools like:

### standard-version

```bash
npm install --save-dev standard-version
```

**Generate changelog and bump version:**
```bash
npx standard-version
```

### semantic-release

For fully automated releases:

```bash
npm install --save-dev semantic-release
```

See [VERSIONING.md](VERSIONING.md) for version management details.

---

## Benefits

**For Developers:**
- ✅ Clear commit history
- ✅ Easy to understand changes
- ✅ Better code reviews
- ✅ Faster onboarding for new contributors

**For Project:**
- ✅ Automated version bumping
- ✅ Automated changelog generation
- ✅ Better release notes
- ✅ Easier to track breaking changes

**For Users:**
- ✅ Clear release notes
- ✅ Understanding what changed between versions
- ✅ Knowing when breaking changes occur

---

## References

- [Conventional Commits Specification](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)
- [commitlint](https://commitlint.js.org/)
- [standard-version](https://github.com/conventional-changelog/standard-version)
- [semantic-release](https://semantic-release.gitbook.io/)

---

## Common Mistakes

### ❌ Wrong

```
Added new sensor support
```
- Not using conventional format
- Past tense instead of imperative

```
feat: Added DFRobot C4001 sensor.
```
- Past tense instead of imperative
- Period at end of subject

```
FEAT(SENSOR): ADD MMWAVE RADAR
```
- Type and scope should be lowercase
- Subject should not be all caps

```
feat(sensor): this commit adds support for the new DFRobot C4001 mmWave radar sensor that we want to use
```
- Subject too long (>72 characters)

### ✅ Correct

```
feat(sensor): add DFRobot C4001 mmWave radar support
```

```
fix(esphome): correct UART configuration for C4001

Change baud rate from 9600 to 115200 to match sensor specifications.
Resolves communication timeout errors.

Fixes #23
```

```
docs: update installation guide with PoE setup

Add detailed instructions for PoE installation including:
- Required equipment list
- Step-by-step installation
- Troubleshooting common issues

Closes #45
```

---

## Questions?

If you're unsure about commit message format:
1. Check this guide and examples
2. Look at recent commit history for reference
3. Ask in [Discussions](https://github.com/Soriarty/HaloSense/discussions)
4. See [CONTRIBUTING.md](../CONTRIBUTING.md) for general guidelines

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28
