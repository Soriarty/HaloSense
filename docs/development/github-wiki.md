# GitHub Wiki Strategy

Complete guide for using GitHub Wiki professionally with HaloSense.

## Overview

GitHub Wiki provides a dedicated space for project documentation separate from the code repository, offering easier editing and better discoverability.

**Wiki URL:** `https://github.com/Soriarty/HaloSense/wiki`

---

## Wiki as Git Submodule (Recommended Strategy)

### Overview

GitHub Wiki is actually a **separate Git repository** that lives alongside your main repository. The best way to manage it professionally is to treat it as a **Git submodule** in your main repo.

**Why this is powerful:**
- ✅ Wiki content becomes part of your main repo structure
- ✅ Branch protection applies to Wiki changes (via PR process)
- ✅ Wiki updates can be reviewed like code
- ✅ Conventional Commits work for Wiki content
- ✅ Version control between code and docs is synchronized
- ✅ Clone main repo → Wiki comes along (optional)

### How GitHub Wiki Works

**Separate Repository:**
```bash
# Main repository
https://github.com/Soriarty/HaloSense.git

# Wiki repository (automatically created by GitHub)
https://github.com/Soriarty/HaloSense.wiki.git
```

**Important characteristics:**
- Wiki is a complete Git repository (`.git/` directory)
- Contains Markdown files (`Home.md`, `Getting-Started.md`, etc.)
- No branch protection by default
- Direct web editing or Git clone workflow

### Setup Wiki as Submodule

**Step 1: Enable Wiki on GitHub**
1. Go to repository Settings
2. Features → Check "Wikis"
3. Create first page (Home) via web interface
4. This initializes the `.wiki.git` repository

**Step 2: Add Wiki as Submodule**

```bash
# Navigate to your main repository
cd ~/Git/HaloSense

# Add Wiki as submodule in docs/wiki/
git submodule add https://github.com/Soriarty/HaloSense.wiki.git docs/wiki

# This creates:
# - docs/wiki/ directory containing Wiki files
# - .gitmodules file tracking the submodule

# Commit the submodule addition
git add .gitmodules docs/wiki
git commit -m "docs(wiki): add Wiki repository as submodule"
git push origin develop
```

**Result:**
```
HaloSense/
├── docs/
│   ├── wiki/                    # ← Wiki submodule
│   │   ├── Home.md
│   │   ├── Getting-Started.md
│   │   └── _Sidebar.md
│   ├── GITFLOW.md               # Technical docs
│   ├── CONVENTIONAL_COMMITS.md
│   └── ...
├── hardware/
├── firmware/
└── ...
```

### Workflow with Submodule

**For Contributors:**

```bash
# Clone main repo with submodules
git clone --recursive https://github.com/Soriarty/HaloSense.git

# Or if already cloned, initialize submodules
git submodule init
git submodule update

# Navigate to Wiki submodule
cd docs/wiki

# Create feature branch (in Wiki repo)
git checkout -b update-assembly-guide

# Edit Wiki pages
vim Assembly-Guide.md

# Commit in Wiki repo
git add Assembly-Guide.md
git commit -m "docs(wiki): update assembly guide with photos"

# Push Wiki changes
git push origin update-assembly-guide

# Go back to main repo
cd ../..

# The submodule reference has changed
git add docs/wiki
git commit -m "docs(wiki): update Wiki reference"

# Create PR to main repo (includes Wiki changes)
git push origin feature/update-docs
```

**For Reviewers:**

When someone creates a PR that includes Wiki changes:
1. PR shows submodule commit hash changed
2. Reviewer can click submodule link to see Wiki diff
3. Review Wiki content before approving PR
4. Branch protection enforces review process

**For Maintainers:**

```bash
# Pull latest changes including submodule updates
git pull origin develop
git submodule update --remote

# Or update all submodules at once
git submodule update --init --recursive
```

### Advantages of Submodule Strategy

| Feature | Without Submodule | With Submodule |
|---------|-------------------|----------------|
| **Branch Protection** | ❌ No (direct Wiki push) | ✅ Yes (via main repo PR) |
| **Code Review** | ❌ No review process | ✅ PR review required |
| **Conventional Commits** | ⚠️ Optional | ✅ Enforced via commitlint |
| **Version Sync** | ❌ Manual | ✅ Submodule commit tracks version |
| **Offline Access** | ❌ Must clone separately | ✅ Included in recursive clone |
| **CI/CD Integration** | ⚠️ Difficult | ✅ Easy (part of main repo) |
| **Atomic Updates** | ❌ Wiki and code separate | ✅ Single PR updates both |

### Branch Protection Integration

**How it works:**

1. **Direct Wiki Push:** Blocked by requiring Wiki changes via main repo PR
2. **Feature Branch Workflow:**
   ```
   feature/new-sensor
   ├── hardware/sensor.kicad_sch    (new hardware)
   ├── firmware/sensor.yaml          (new firmware)
   └── docs/wiki/Sensor-Guide.md    (updated Wiki)
   ```
3. **PR Review:** All changes reviewed together
4. **Merge:** Wiki submodule updated atomically with code

**Configuration:**

```bash
# In main repo, enforce that Wiki changes go through PR
# (no special config needed - main repo branch protection applies)

# Optional: Remind contributors in CONTRIBUTING.md
cat >> CONTRIBUTING.md <<'EOF'

### Updating Wiki

Wiki content is managed as a Git submodule at `docs/wiki/`.

To update Wiki pages:
1. Navigate to `docs/wiki/`
2. Create branch and edit pages
3. Commit Wiki changes
4. Return to main repo root
5. Commit submodule reference update
6. Create PR to main repo (includes Wiki changes)

EOF
```

### Alternative: Two-Way Sync Strategy

If you want to allow **both** direct Wiki editing (via web) **and** submodule workflow:

**Setup bidirectional sync:**

```bash
# Script: scripts/sync-wiki.sh
#!/bin/bash

# Pull latest Wiki changes into submodule
cd docs/wiki
git pull origin main

# Update submodule reference in main repo
cd ../..
git add docs/wiki
git commit -m "docs(wiki): sync latest Wiki changes" || true
```

**Run periodically:**
```bash
# Manual sync
./scripts/sync-wiki.sh

# Or via cron/GitHub Actions
# (runs daily to pull web-edited Wiki changes)
```

**Trade-offs:**
- ✅ Allows quick web edits (no PR)
- ❌ Bypasses branch protection
- ⚠️ Two sources of truth (can conflict)

**Recommendation:** Choose **one** workflow:
- **Strict:** All Wiki changes via submodule PR (recommended for HaloSense)
- **Flexible:** Allow web edits + periodic sync (for community wikis)

### Submodule Commands Reference

```bash
# Add submodule
git submodule add <url> <path>

# Clone repo with submodules
git clone --recursive <repo-url>

# Initialize submodules (if not cloned with --recursive)
git submodule init
git submodule update

# Update submodule to latest
cd docs/wiki
git pull origin main
cd ../..
git add docs/wiki
git commit -m "docs(wiki): update to latest"

# Update all submodules
git submodule update --remote

# Remove submodule
git submodule deinit docs/wiki
git rm docs/wiki
rm -rf .git/modules/docs/wiki
```

### .gitmodules File

After adding submodule, `.gitmodules` contains:

```ini
[submodule "docs/wiki"]
	path = docs/wiki
	url = https://github.com/Soriarty/HaloSense.wiki.git
	branch = main
```

**Optional: Track specific branch:**
```bash
# Make submodule track 'develop' branch instead of 'main'
git config -f .gitmodules submodule.docs/wiki.branch develop
```

### Troubleshooting Submodules

**Issue: Submodule not initialized**
```bash
# Solution
git submodule init
git submodule update
```

**Issue: Submodule detached HEAD**
```bash
# Solution: check out main branch in submodule
cd docs/wiki
git checkout main
```

**Issue: Submodule conflicts**
```bash
# Solution: resolve in submodule first, then main repo
cd docs/wiki
git pull
# Resolve conflicts
git add .
git commit
cd ../..
git add docs/wiki
git commit
```

**Issue: Forgot to push submodule changes**
```bash
# Main repo references commit that doesn't exist in Wiki
# Solution: push Wiki changes first
cd docs/wiki
git push origin main
cd ../..
git push origin develop
```

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
