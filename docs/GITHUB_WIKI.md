# GitHub Wiki Strategy

Complete guide for using GitHub Wiki professionally with HaloSense.

## Overview

GitHub Wiki provides a dedicated space for project documentation separate from the code repository, offering easier editing and better discoverability.

**Wiki URL:** `https://github.com/Soriarty/HaloSense/wiki`

---

## Wiki vs Docs Directory

### Current Setup

HaloSense has **both** Wiki and `docs/` directory:

```
GitHub Wiki (User-facing documentation)
├── Home (Project overview)
├── Getting Started
├── User Guides
└── FAQ

Repository docs/ (Technical documentation)
├── API references
├── Development guides
├── Architecture docs
└── Contributing guides
```

### When to Use Wiki

**✅ Use Wiki for:**
- 📘 User-facing documentation
- 🚀 Getting started guides
- 📝 How-to articles
- ❓ FAQs
- 🎓 Tutorials
- 📰 Release notes
- 🔍 Troubleshooting
- 🌐 Community content

**Why Wiki is Better for These:**
- Easy web-based editing
- No pull requests needed for docs updates
- Better for community contributions
- Search-optimized
- Discoverable on GitHub
- Version history built-in

### When to Use docs/ Directory

**✅ Use docs/ for:**
- 🔧 Technical specifications
- 💻 API references
- 🏗️ Architecture documents
- 🔬 Development workflows
- 📋 Code-adjacent documentation
- 🔐 Internal processes
- 🧪 Testing procedures

**Why docs/ is Better for These:**
- Version controlled with code
- Lives alongside implementation
- Part of PR review process
- Can reference specific code
- Consistent with codebase versions
- Offline accessible

---

## Recommended Hybrid Architecture

### High-Level Structure

```
┌─────────────────────────────────────────┐
│         GitHub Wiki                     │
│  (User Documentation Portal)            │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │ Home                              │  │
│  │  • Project Overview               │  │
│  │  • Quick Start                    │  │
│  │  • Navigation Hub                 │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │ User Guides                       │  │
│  │  • Installation                   │  │
│  │  • Configuration                  │  │
│  │  • Usage Examples                 │  │
│  │  • Troubleshooting                │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │ Hardware                          │  │
│  │  • Assembly Guide                 │  │
│  │  • BOM                            │  │
│  │  • Ordering Parts                 │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │ Links to Technical Docs           │  │
│  │  → docs/ (for developers)         │  │
│  └──────────────────────────────────┘  │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│      Repository docs/                   │
│  (Developer Documentation)              │
│                                         │
│  • Git Flow Workflow                    │
│  • Conventional Commits                 │
│  • API Specifications                   │
│  • Contributing Guidelines              │
│  • Sensor Technical Details             │
│  • Development Setup                    │
└─────────────────────────────────────────┘
```

### Content Mapping

**Wiki Pages → Source:**
- Home → Brief overview + links
- Getting Started → Simplified from docs/installation.md
- Assembly Guide → User-friendly version of docs/assembly.md
- BOM → Simplified from docs/bom.md with shopping links
- Configuration → ESPHome setup guide
- Troubleshooting → FAQ-style
- Release Notes → Generated from CHANGELOG.md

**Keep in docs/:**
- GITFLOW.md
- CONVENTIONAL_COMMITS.md
- VERSIONING.md
- BRANCH_PROTECTION.md
- CONTRIBUTING.md
- Sensor technical specs

---

## Wiki Structure Design

### Recommended Page Hierarchy

```
Home
├── Getting-Started
│   ├── Quick-Start-Guide
│   ├── Requirements
│   └── First-Time-Setup
│
├── Hardware
│   ├── Assembly-Guide
│   ├── Bill-of-Materials
│   ├── Where-to-Buy
│   ├── PCB-Ordering
│   └── 3D-Printing-Guide
│
├── Firmware
│   ├── ESPHome-Setup
│   ├── Configuration-Examples
│   ├── OTA-Updates
│   └── Troubleshooting-Firmware
│
├── Home-Assistant
│   ├── Integration-Setup
│   ├── Automations
│   ├── Dashboard-Cards
│   └── Example-Configurations
│
├── Troubleshooting
│   ├── Common-Issues
│   ├── FAQ
│   ├── Hardware-Problems
│   ├── Firmware-Problems
│   └── Network-Issues
│
├── Community
│   ├── Showcase
│   ├── User-Builds
│   ├── Tips-and-Tricks
│   └── Custom-Modifications
│
└── Development
    ├── Contributing → Link to CONTRIBUTING.md
    ├── Git-Flow → Link to docs/GITFLOW.md
    ├── Technical-Docs → Link to docs/
    └── API-Reference
```

---

## Professional Wiki Setup

### 1. Home Page Design

**Template for Home.md:**

````markdown
# 🌟 HaloSense Wiki

> **Professional-grade presence detection for your smart home**

[![GitHub](https://img.shields.io/github/stars/Soriarty/HaloSense?style=social)](https://github.com/Soriarty/HaloSense)
[![License](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

---

## 📖 Welcome

HaloSense is an open-source smart home presence sensor combining mmWave radar, PIR motion, and ambient light sensing with multiple connectivity options (PoE, Ethernet+USB-C, WiFi+USB-C).

**This Wiki provides user-focused documentation. For technical/development docs, see the [docs/](https://github.com/Soriarty/HaloSense/tree/main/docs) directory.**

---

## 🚀 Quick Navigation

### New to HaloSense?
👉 **[Getting Started Guide](Getting-Started)** - Start here!

### Ready to Build?
🔧 **[Assembly Guide](Assembly-Guide)** - Step-by-step instructions
🛒 **[Bill of Materials](Bill-of-Materials)** - What you need to buy
📦 **[Where to Buy](Where-to-Buy)** - Sourcing components

### Configure Your Device
⚙️ **[ESPHome Setup](ESPHome-Setup)** - Firmware configuration
🏠 **[Home Assistant Integration](Home-Assistant-Integration)** - Connect to HA
🎨 **[Configuration Examples](Configuration-Examples)** - Copy-paste configs

### Need Help?
❓ **[FAQ](FAQ)** - Frequently asked questions
🐛 **[Troubleshooting](Troubleshooting)** - Common issues and solutions
💬 **[Discussions](https://github.com/Soriarty/HaloSense/discussions)** - Ask the community

### For Developers
💻 **[Contributing](https://github.com/Soriarty/HaloSense/blob/main/CONTRIBUTING.md)** - How to contribute
🔀 **[Git Flow](https://github.com/Soriarty/HaloSense/blob/main/docs/GITFLOW.md)** - Development workflow
📚 **[Technical Docs](https://github.com/Soriarty/HaloSense/tree/main/docs)** - Deep technical details

---

## ✨ Features

### 🎯 Multi-Sensor Detection
- **mmWave Radar** - Accurate presence detection (even stationary people)
- **PIR Motion** - Traditional motion detection backup
- **Ambient Light** - Lux measurement for smart lighting

### 🔌 Flexible Connectivity
- **PoE** - Single cable for power + data
- **Ethernet + USB-C** - Standard network with USB power
- **WiFi + USB-C** - Wireless connectivity

### 🏗️ Complete Design Package
- **Hardware** - KiCad PCB design (circular form factor)
- **Firmware** - ESPHome configuration
- **Enclosure** - 3D-printable housing

---

## 📊 Project Status

🚧 **Work in Progress** - Active development

**Completed:**
- ✅ Project structure and documentation
- ✅ mmWave sensor selection (DFRobot C4001)
- ✅ Development workflow (Git Flow, Conventional Commits)

**In Progress:**
- 🔨 Hardware design (KiCad)
- 🔨 Firmware development (ESPHome)
- 🔨 Component selection (PIR, light sensors)

**Planned:**
- 📋 Enclosure design (3D models)
- 📋 Prototyping and testing
- 📋 First stable release (v1.0.0)

---

## 🤝 Community

- **💬 [GitHub Discussions](https://github.com/Soriarty/HaloSense/discussions)** - Questions, ideas, showcase
- **🐛 [Issue Tracker](https://github.com/Soriarty/HaloSense/issues)** - Bug reports and feature requests
- **👥 [Contributors](https://github.com/Soriarty/HaloSense/graphs/contributors)** - Thank you!

---

## 📜 License

This project is licensed under **CC BY-NC-SA 4.0** for personal/DIY use.
Commercial use requires separate licensing. [Learn more →](https://github.com/Soriarty/HaloSense/blob/main/LICENSE.md)

---

## 🔗 Quick Links

| Resource | Link |
|----------|------|
| 📦 Repository | https://github.com/Soriarty/HaloSense |
| 📖 Technical Docs | [/docs](https://github.com/Soriarty/HaloSense/tree/main/docs) |
| 🚀 Getting Started | [Start Here](Getting-Started) |
| 🛠️ Contributing | [CONTRIBUTING.md](https://github.com/Soriarty/HaloSense/blob/main/CONTRIBUTING.md) |
| 💬 Discussions | [GitHub Discussions](https://github.com/Soriarty/HaloSense/discussions) |
| 📄 License | [LICENSE.md](https://github.com/Soriarty/HaloSense/blob/main/LICENSE.md) |

---

**Maintained by:** [@Soriarty](https://github.com/Soriarty)
**Last Updated:** 2025-11-28

---

_Star ⭐ the repository if you find this project useful!_
````

### 2. Sidebar Navigation

**Create _Sidebar.md:**

````markdown
## 📖 HaloSense Wiki

**[🏠 Home](Home)**

---

### 🚀 Getting Started
- [Quick Start](Quick-Start-Guide)
- [Requirements](Requirements)
- [First Setup](First-Time-Setup)

### 🔧 Hardware
- [Assembly Guide](Assembly-Guide)
- [Bill of Materials](Bill-of-Materials)
- [Where to Buy](Where-to-Buy)
- [PCB Ordering](PCB-Ordering)
- [3D Printing](3D-Printing-Guide)

### 💻 Firmware
- [ESPHome Setup](ESPHome-Setup)
- [Configuration](Configuration-Examples)
- [OTA Updates](OTA-Updates)
- [Troubleshooting](Troubleshooting-Firmware)

### 🏠 Home Assistant
- [Integration](Home-Assistant-Integration)
- [Automations](Automations)
- [Dashboard Cards](Dashboard-Cards)
- [Examples](Example-Configurations)

### ❓ Help
- [FAQ](FAQ)
- [Common Issues](Common-Issues)
- [Hardware Problems](Hardware-Problems)
- [Network Issues](Network-Issues)

### 👥 Community
- [Showcase](Showcase)
- [User Builds](User-Builds)
- [Tips & Tricks](Tips-and-Tricks)

### 💻 Development
- [Contributing](https://github.com/Soriarty/HaloSense/blob/main/CONTRIBUTING.md)
- [Technical Docs](https://github.com/Soriarty/HaloSense/tree/main/docs)
- [Git Flow](https://github.com/Soriarty/HaloSense/blob/main/docs/GITFLOW.md)

---

**[💬 Discussions](https://github.com/Soriarty/HaloSense/discussions)** | **[🐛 Issues](https://github.com/Soriarty/HaloSense/issues)**
````

### 3. Footer Template

**Create _Footer.md:**

````markdown
---

📦 **Repository:** [Soriarty/HaloSense](https://github.com/Soriarty/HaloSense) | 📄 **License:** [CC BY-NC-SA 4.0](https://github.com/Soriarty/HaloSense/blob/main/LICENSE.md) | 👤 **Maintainer:** [@Soriarty](https://github.com/Soriarty)

_Last updated: 2025-11-28 | [Edit this page](https://github.com/Soriarty/HaloSense/wiki/_edit)_
````

---

## Wiki Best Practices

### Content Guidelines

**DO ✅:**
- Write for users, not developers
- Use clear, simple language
- Include screenshots and diagrams
- Provide copy-paste examples
- Link to related pages
- Keep pages focused (one topic)
- Update regularly
- Add timestamps
- Include troubleshooting
- Cross-reference docs/

**DON'T ❌:**
- Duplicate technical docs
- Write overly long pages
- Use jargon without explanation
- Include code implementation details
- Forget to update outdated content
- Create orphaned pages
- Use broken links
- Skip images for complex steps

### Page Naming Conventions

**Format:** `Title-With-Hyphens` (GitHub auto-generates)

**Good:**
```
Getting-Started
Assembly-Guide
Bill-of-Materials
ESPHome-Setup
Troubleshooting-Network-Issues
```

**Bad:**
```
getting_started        ❌ (underscores)
assembly               ❌ (too vague)
BOM                    ❌ (unclear abbreviation)
esphome-setup          ❌ (inconsistent casing)
```

### Image Management

**Where to Store Images:**

**Option 1: Wiki Repository (Recommended)**
```bash
# Clone wiki
git clone https://github.com/Soriarty/HaloSense.wiki.git
cd HaloSense.wiki

# Add images directory
mkdir images
cp ~/my-image.png images/

# Commit and push
git add images/
git commit -m "Add assembly guide images"
git push
```

**Reference in Wiki:**
```markdown
![Assembly Step 1](images/assembly-step-1.png)
```

**Option 2: Main Repository**
```markdown
![PCB Diagram](https://raw.githubusercontent.com/Soriarty/HaloSense/main/docs/images/pcb-diagram.png)
```

**Option 3: External (Not Recommended)**
```markdown
![Imgur](https://i.imgur.com/xyz.png)
```

---

## Wiki Automation

### Sync from docs/ to Wiki

**Script: scripts/sync-wiki.sh**

```bash
#!/bin/bash
# Sync documentation from docs/ to Wiki

# Clone wiki
git clone https://github.com/Soriarty/HaloSense.wiki.git /tmp/wiki
cd /tmp/wiki

# Copy and convert user-facing docs
# (Create simplified versions)

# Example: Convert assembly.md to Wiki format
cat > Assembly-Guide.md <<'EOF'
# Assembly Guide

> Simplified user guide. [Full technical guide →](https://github.com/Soriarty/HaloSense/blob/main/docs/assembly.md)

## Overview

Step-by-step instructions for building your HaloSense...

[Content from docs/assembly.md, simplified]

EOF

# Commit and push
git add .
git commit -m "docs: sync from main repository"
git push

# Cleanup
cd -
rm -rf /tmp/wiki
```

### GitHub Actions (Future)

**`.github/workflows/sync-wiki.yml`:**

```yaml
name: Sync Wiki

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'
      - 'README.md'

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Sync to Wiki
        run: |
          # Clone wiki
          git clone https://${{ secrets.GITHUB_TOKEN }}@github.com/Soriarty/HaloSense.wiki.git

          # Sync content
          ./scripts/sync-wiki.sh

          # Push changes
          cd HaloSense.wiki
          git config user.name "GitHub Actions"
          git config user.email "actions@github.com"
          git add .
          git commit -m "docs: auto-sync from main repo" || exit 0
          git push
```

---

## Wiki Management

### Editing Workflow

**Web Interface (Easy):**
1. Go to Wiki page
2. Click "Edit"
3. Make changes
4. Click "Save Page"

**Git Clone (Power Users):**
```bash
# Clone wiki
git clone https://github.com/Soriarty/HaloSense.wiki.git
cd HaloSense.wiki

# Create branch
git checkout -b update-assembly-guide

# Edit files
vim Assembly-Guide.md

# Commit
git add .
git commit -m "docs(wiki): update assembly guide with photos"

# Push
git push origin update-assembly-guide

# (Optional: Create PR via gh CLI)
```

### Access Control

**Who Can Edit:**
- Repository owners: ✅ Full access
- Collaborators: ✅ Can edit
- Public: ❌ Cannot edit (by default)

**Enable Public Editing (Not Recommended for HaloSense):**
- Settings → Features → Wikis
- "Restrict editing to collaborators only" → Uncheck

**Recommendation:** Keep editing restricted, accept contributions via PR to docs/

### Version History

**View History:**
- Click "Page History" on any Wiki page
- See all revisions and authors
- Compare versions
- Revert if needed

**Via Git:**
```bash
git clone https://github.com/Soriarty/HaloSense.wiki.git
cd HaloSense.wiki
git log
git diff HEAD~1 Assembly-Guide.md
```

---

## Migration Plan

### Phase 1: Setup (Week 1)

**Tasks:**
1. Enable Wiki on GitHub
2. Create Home page
3. Create _Sidebar
4. Create _Footer
5. Add Getting Started page

### Phase 2: Content (Week 2-3)

**Migrate User-Facing Content:**
1. Assembly Guide (simplified from docs/assembly.md)
2. BOM (shopping-focused from docs/bom.md)
3. Installation (user-friendly from docs/installation.md)
4. ESPHome Setup (beginner guide)
5. Home Assistant Integration
6. FAQ / Troubleshooting

### Phase 3: Polish (Week 4)

**Enhancements:**
1. Add images and diagrams
2. Create video tutorials (links)
3. Add user showcase page
4. Implement sidebar navigation
5. Add footer with links
6. Review all cross-references

### Phase 4: Automation (Future)

**Optional:**
1. Auto-sync script from docs/
2. GitHub Actions integration
3. Automated image optimization
4. Link checker

---

## Wiki Examples from Popular Projects

### Excellent Wiki Examples

**Home Assistant:**
- https://github.com/home-assistant/core/wiki
- Clean navigation
- Comprehensive developer docs
- Good use of sidebar

**ESPHome:**
- https://esphome.io/ (separate site, but wiki-like)
- Excellent component docs
- Search functionality
- Code examples

**Prusa3D:**
- https://github.com/prusa3d/PrusaSlicer/wiki
- Good troubleshooting section
- Hardware assembly guides
- User contributions

### What Makes Them Great

✅ Clear homepage with navigation
✅ Logical page hierarchy
✅ Consistent formatting
✅ Rich with images
✅ Updated regularly
✅ Community contributions
✅ Search-friendly titles
✅ Cross-references

---

## Wiki vs Docs Decision Matrix

| Content Type | Wiki | docs/ | Reason |
|--------------|------|-------|--------|
| Getting Started | ✅ | ❌ | User-focused |
| Assembly Guide | ✅ | ✅ | Both (simplified vs detailed) |
| BOM | ✅ | ✅ | Both (shopping vs technical) |
| Installation | ✅ | ✅ | Both (beginner vs advanced) |
| ESPHome Config | ✅ | ❌ | User examples |
| Home Assistant | ✅ | ❌ | User automations |
| FAQ | ✅ | ❌ | User questions |
| Troubleshooting | ✅ | ❌ | User issues |
| Git Flow | ❌ | ✅ | Developer workflow |
| Conventional Commits | ❌ | ✅ | Developer standards |
| API Reference | ❌ | ✅ | Technical specs |
| Contributing | ❌ | ✅ | Developer guide |
| Sensor Specs | ❌ | ✅ | Technical details |
| Architecture | ❌ | ✅ | Internal design |

---

## Checklist

### Initial Setup
- [ ] Enable Wiki on GitHub
- [ ] Create Home page with template
- [ ] Create _Sidebar navigation
- [ ] Create _Footer
- [ ] Add Getting Started page
- [ ] Test all internal links

### Content Migration
- [ ] Simplify and migrate Assembly Guide
- [ ] Create user-friendly BOM with links
- [ ] Write beginner Installation guide
- [ ] Create ESPHome setup tutorial
- [ ] Write Home Assistant integration guide
- [ ] Create FAQ page
- [ ] Add Troubleshooting page

### Polish
- [ ] Add images to key pages
- [ ] Cross-reference all pages
- [ ] Verify all external links
- [ ] Add search keywords to pages
- [ ] Review consistency
- [ ] Update timestamps

### Maintenance
- [ ] Set up Wiki update reminders
- [ ] Document Wiki workflow in CONTRIBUTING.md
- [ ] Consider automation (optional)
- [ ] Monitor community feedback

---

## Questions?

For Wiki strategy questions:
1. Check this guide
2. Review [CONTRIBUTING.md](../CONTRIBUTING.md)
3. Ask in [Discussions](https://github.com/Soriarty/HaloSense/discussions)

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28
