# Git Flow Workflow

Git Flow branching strategy for the HaloSense project.

## Overview

HaloSense uses the **Git Flow** workflow, a popular branching model designed by Vincent Driessen. This provides a robust framework for managing releases, features, and hotfixes.

**Reference:** [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)

---

## Branch Structure

### Main Branches

#### `main` (Production)
- **Purpose:** Production-ready code only
- **Protection:** Fully protected, no direct commits
- **Updates:** Only via merge from `release/*` or `hotfix/*`
- **Tags:** All releases tagged here (v1.0.0, v1.1.0, etc.)
- **Deployment:** Automatic deployment to production (future)

#### `develop` (Integration)
- **Purpose:** Integration branch for ongoing development
- **Protection:** Protected, requires PR reviews
- **Updates:** Via merge from `feature/*`, `bugfix/*`, `release/*`, `hotfix/*`
- **Testing:** Continuous integration tests run here
- **State:** Always reflects latest delivered development changes

---

## Supporting Branches

### Feature Branches

**Format:** `feature/<description>` or `feature/<issue-number>-<description>`

**Examples:**
```
feature/temperature-sensor
feature/mqtt-integration
feature/23-add-pir-sensor
```

**Purpose:** Develop new features for upcoming releases

**Branch from:** `develop`
**Merge into:** `develop`
**Lifetime:** Until feature is complete and merged

**Workflow:**
```bash
# Create feature branch
git checkout develop
git pull origin develop
git checkout -b feature/temperature-sensor

# Work on feature (multiple commits)
git add .
git commit -m "feat(sensor): add temperature sensor support"
git commit -m "test(sensor): add temperature sensor tests"

# Keep feature updated with develop
git checkout develop
git pull origin develop
git checkout feature/temperature-sensor
git merge develop

# Create pull request to develop
git push origin feature/temperature-sensor
# Open PR: feature/temperature-sensor → develop
```

### Release Branches

**Format:** `release/<version>`

**Examples:**
```
release/1.0.0
release/1.1.0-rc.1
release/2.0.0-beta.1
```

**Purpose:** Prepare for a new production release

**Branch from:** `develop`
**Merge into:** `main` AND `develop`
**Lifetime:** Until release is deployed

**Workflow:**
```bash
# Create release branch
git checkout develop
git pull origin develop
git checkout -b release/1.0.0

# Version bump and prepare release
npm run release  # or manual version updates

# Bug fixes only (no new features!)
git commit -m "fix(build): correct production build script"

# Final testing and QA
# Update CHANGELOG.md if needed

# Merge to main (creates release)
git checkout main
git pull origin main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main --follow-tags

# Merge back to develop
git checkout develop
git pull origin develop
git merge --no-ff release/1.0.0
git push origin develop

# Delete release branch
git branch -d release/1.0.0
git push origin --delete release/1.0.0
```

### Hotfix Branches

**Format:** `hotfix/<version>` or `hotfix/<issue-number>-<description>`

**Examples:**
```
hotfix/1.0.1
hotfix/42-critical-uart-bug
```

**Purpose:** Emergency fixes for production

**Branch from:** `main`
**Merge into:** `main` AND `develop`
**Lifetime:** Until fix is deployed

**Workflow:**
```bash
# Create hotfix branch from main
git checkout main
git pull origin main
git checkout -b hotfix/1.0.1

# Fix the critical bug
git commit -m "fix(esphome): correct critical UART timeout issue

This is a critical fix for production issue #42 where UART
communication would timeout under high load conditions.

Fixes #42"

# Version bump (PATCH)
npm run release:patch

# Merge to main (emergency release)
git checkout main
git pull origin main
git merge --no-ff hotfix/1.0.1
git tag -a v1.0.1 -m "Hotfix v1.0.1"
git push origin main --follow-tags

# Merge back to develop
git checkout develop
git pull origin develop
git merge --no-ff hotfix/1.0.1
git push origin develop

# If release branch exists, merge there too
git checkout release/1.1.0
git merge --no-ff hotfix/1.0.1

# Delete hotfix branch
git branch -d hotfix/1.0.1
git push origin --delete hotfix/1.0.1
```

### Bugfix Branches

**Format:** `bugfix/<description>` or `bugfix/<issue-number>-<description>`

**Examples:**
```
bugfix/sensor-calibration
bugfix/78-pcb-silkscreen-error
```

**Purpose:** Fix bugs in develop branch (not production emergencies)

**Branch from:** `develop`
**Merge into:** `develop`
**Lifetime:** Until bug is fixed

**Workflow:**
```bash
# Create bugfix branch
git checkout develop
git pull origin develop
git checkout -b bugfix/sensor-calibration

# Fix the bug
git commit -m "fix(sensor): correct calibration algorithm"

# Create pull request to develop
git push origin bugfix/sensor-calibration
# Open PR: bugfix/sensor-calibration → develop
```

---

## Branch Naming Conventions

### Format Rules

**Feature:**
- `feature/short-description`
- `feature/issue-number-description`
- Use lowercase with hyphens
- Keep concise (max 50 characters)

**Release:**
- `release/version`
- Follow semantic versioning: `release/1.0.0`
- Pre-release: `release/1.0.0-beta.1`

**Hotfix:**
- `hotfix/version` for version-based
- `hotfix/issue-number-description` for issue-based

**Bugfix:**
- `bugfix/short-description`
- `bugfix/issue-number-description`

### Examples

**Good:**
```
feature/mqtt-support
feature/45-temperature-sensor
release/1.2.0
hotfix/1.1.1
bugfix/uart-timeout
```

**Bad:**
```
Feature/MQTT-Support          ❌ (uppercase)
new_feature                   ❌ (no prefix)
fix-bug                       ❌ (ambiguous)
feature/add-new-temperature-sensor-with-i2c  ❌ (too long)
```

---

## Workflow Scenarios

### Scenario 1: New Feature Development

**Goal:** Add PIR motion sensor support

```bash
# 1. Start from develop
git checkout develop
git pull origin develop

# 2. Create feature branch
git checkout -b feature/pir-sensor

# 3. Develop feature (multiple commits)
git commit -m "feat(sensor): add PIR sensor hardware definitions"
git commit -m "feat(sensor): implement PIR sensor ESPHome config"
git commit -m "docs(sensor): add PIR sensor documentation"
git commit -m "test(sensor): add PIR sensor integration tests"

# 4. Keep branch updated
git checkout develop
git pull origin develop
git checkout feature/pir-sensor
git merge develop

# 5. Push and create PR
git push origin feature/pir-sensor
# GitHub: Create PR feature/pir-sensor → develop

# 6. After review and approval, merge via GitHub
# (Squash merge or merge commit, depending on team preference)

# 7. Clean up
git checkout develop
git pull origin develop
git branch -d feature/pir-sensor
```

### Scenario 2: Release Preparation

**Goal:** Prepare version 1.0.0 release

```bash
# 1. Create release branch from develop
git checkout develop
git pull origin develop
git checkout -b release/1.0.0

# 2. Version bump
npm run release

# 3. Update version in other files
# - firmware/halosense.yaml (substitutions)
# - hardware/schematics/*.kicad_sch (title block)
# - Update CHANGELOG.md

# 4. Commit version changes
git add .
git commit -m "chore(release): prepare v1.0.0 release"

# 5. Bug fixes only (no new features!)
# If bugs found during QA:
git commit -m "fix(esphome): correct sensor initialization"

# 6. Final testing
# - Run all tests
# - Build hardware documentation
# - Verify firmware compilation

# 7. Merge to main
git checkout main
git pull origin main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Release v1.0.0: First stable release

Major features:
- DFRobot C4001 mmWave sensor support
- Complete documentation
- Hardware design v1.0.0
- Firmware v1.0.0"

git push origin main --follow-tags

# 8. Merge back to develop
git checkout develop
git pull origin develop
git merge --no-ff release/1.0.0
git push origin develop

# 9. Clean up
git branch -d release/1.0.0
git push origin --delete release/1.0.0
```

### Scenario 3: Critical Production Fix

**Goal:** Fix critical UART bug in production

```bash
# 1. Create hotfix from main
git checkout main
git pull origin main
git checkout -b hotfix/1.0.1

# 2. Fix the bug
git commit -m "fix(esphome): resolve UART timeout under load

Critical fix for issue #42. UART communication would timeout
when sensor data rate exceeded 100Hz. Increased buffer size
and adjusted timeout values.

Fixes #42"

# 3. Version bump
npm run release:patch

# 4. Test thoroughly
# - Verify fix works
# - Ensure no regressions

# 5. Merge to main (emergency release)
git checkout main
git merge --no-ff hotfix/1.0.1
git tag -a v1.0.1 -m "Hotfix v1.0.1: Critical UART fix"
git push origin main --follow-tags

# 6. Merge to develop
git checkout develop
git merge --no-ff hotfix/1.0.1
git push origin develop

# 7. If active release branch exists
git checkout release/1.1.0  # if exists
git merge --no-ff hotfix/1.0.1

# 8. Clean up
git branch -d hotfix/1.0.1
git push origin --delete hotfix/1.0.1
```

---

## Pull Request Guidelines

### Feature/Bugfix → Develop

**Title Format:**
```
feat(sensor): add PIR motion sensor support
fix(esphome): correct UART configuration
```

**PR Template:**
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] New feature
- [ ] Bug fix
- [ ] Documentation
- [ ] Refactoring

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed
- [ ] Hardware tested (if applicable)

## Checklist
- [ ] Follows conventional commits
- [ ] Documentation updated
- [ ] No breaking changes (or documented)
- [ ] Branch up to date with develop

Closes #123
```

### Release → Main

**Title Format:**
```
Release v1.0.0
```

**PR Template:**
```markdown
## Release Version
v1.0.0

## Changes
Link to CHANGELOG.md section

## Pre-Release Checklist
- [ ] Version bumped in all files
- [ ] CHANGELOG.md updated
- [ ] All tests passing
- [ ] Documentation reviewed
- [ ] Hardware validated (if applicable)
- [ ] Firmware compiled successfully

## Release Notes
Brief summary of major changes
```

---

## Branch Protection Rules

### `main` Branch

**Required:**
- ✅ Require pull request reviews (1 minimum)
- ✅ Require status checks to pass
- ✅ Require branches to be up to date
- ✅ Require conversation resolution
- ✅ No force pushes
- ✅ No deletions
- ✅ Require signed commits (recommended)

**Allowed to merge:**
- Release branches (`release/*`)
- Hotfix branches (`hotfix/*`)
- Repository administrators (emergency only)

### `develop` Branch

**Required:**
- ✅ Require pull request reviews (1 minimum)
- ✅ Require status checks to pass
- ✅ No force pushes
- ✅ Require conversation resolution

**Allowed to merge:**
- Feature branches (`feature/*`)
- Bugfix branches (`bugfix/*`)
- Release branches (`release/*`)
- Hotfix branches (`hotfix/*`)

---

## Version Management

### Semantic Versioning with Git Flow

**MAJOR (X.0.0):**
- Breaking hardware changes
- Breaking firmware API changes
- Incompatible component versions
- Triggered by: `BREAKING CHANGE:` in commits

**MINOR (0.X.0):**
- New features (backwards-compatible)
- New sensor support
- New optional functionality
- Triggered by: `feat:` commits

**PATCH (0.0.X):**
- Bug fixes
- Documentation updates
- Minor improvements
- Triggered by: `fix:` commits

### Version Workflow

**Development:**
```
develop: 1.1.0-dev
feature/temp-sensor: 1.1.0-dev
```

**Release Preparation:**
```
release/1.1.0: 1.1.0-rc.1 → 1.1.0-rc.2 → 1.1.0
```

**Production:**
```
main: 1.1.0 (tagged)
```

**Hotfix:**
```
hotfix/1.1.1: 1.1.0 → 1.1.1
main: 1.1.1 (tagged)
```

---

## CI/CD Integration

### Automated Workflows (Future)

**On `develop` push:**
- Run all tests
- Build documentation
- Deploy to staging environment
- Notify team in Slack/Discord

**On `release/*` creation:**
- Run full test suite
- Build release artifacts
- Generate release notes draft
- Create pre-release on GitHub

**On `main` tag:**
- Create GitHub release
- Build final artifacts
- Deploy to production
- Generate changelog
- Notify community

---

## Common Commands

### Daily Development

```bash
# Start new feature
git checkout develop
git pull origin develop
git checkout -b feature/my-feature

# Update feature with latest develop
git checkout develop
git pull origin develop
git checkout feature/my-feature
git merge develop

# Finish feature
git push origin feature/my-feature
# Create PR on GitHub
```

### Release Management

```bash
# Start release
git checkout -b release/1.2.0 develop
npm run release

# Finish release
git checkout main
git merge --no-ff release/1.2.0
git tag -a v1.2.0
git push origin main --follow-tags

git checkout develop
git merge --no-ff release/1.2.0
git push origin develop
```

### Emergency Hotfix

```bash
# Start hotfix
git checkout -b hotfix/1.1.1 main
# Fix bug
git commit -m "fix: critical bug"
npm run release:patch

# Finish hotfix
git checkout main
git merge --no-ff hotfix/1.1.1
git tag -a v1.1.1
git push origin main --follow-tags

git checkout develop
git merge --no-ff hotfix/1.1.1
git push origin develop
```

---

## Git Flow Tools

### git-flow Extension (Optional)

Install git-flow for simplified commands:

**Installation:**
```bash
# macOS
brew install git-flow

# Ubuntu/Debian
sudo apt-get install git-flow

# Fedora
sudo dnf install gitflow
```

**Initialization:**
```bash
git flow init

# Use defaults:
# Production branch: main
# Development branch: develop
# Feature prefix: feature/
# Release prefix: release/
# Hotfix prefix: hotfix/
# Support prefix: support/
```

**Usage:**
```bash
# Feature
git flow feature start my-feature
git flow feature finish my-feature

# Release
git flow release start 1.0.0
git flow release finish 1.0.0

# Hotfix
git flow hotfix start 1.0.1
git flow hotfix finish 1.0.1
```

**Note:** git-flow is optional. Manual Git commands work equally well.

---

## Best Practices

### DO ✅

- Always branch from `develop` for features
- Keep feature branches short-lived (days, not weeks)
- Merge `develop` into feature branches regularly
- Use descriptive branch names
- Follow conventional commits
- Write meaningful PR descriptions
- Review code before merging
- Tag all releases on `main`
- Document breaking changes
- Keep `main` always deployable

### DON'T ❌

- Never commit directly to `main` or `develop`
- Don't create long-lived feature branches
- Don't add new features in release branches
- Don't skip code reviews
- Don't force push to protected branches
- Don't merge without resolving conflicts
- Don't leave stale branches
- Don't forget to update version numbers
- Don't skip tests before merging

---

## Troubleshooting

### Merge Conflicts

```bash
# If conflict occurs during merge
git status  # See conflicted files

# Resolve conflicts manually in editor
# Look for <<<<<<< ======= >>>>>>> markers

# After resolving
git add <resolved-files>
git commit
```

### Wrong Branch

```bash
# If committed to wrong branch
git log  # Find commit hash

# Switch to correct branch
git checkout correct-branch
git cherry-pick <commit-hash>

# Remove from wrong branch
git checkout wrong-branch
git reset --hard HEAD~1
```

### Revert Release

```bash
# If release needs to be reverted
git checkout main
git revert -m 1 <merge-commit-hash>
git push origin main

# Also revert in develop
git checkout develop
git revert -m 1 <merge-commit-hash>
git push origin develop
```

---

## Migration to Git Flow

### Initial Setup

```bash
# 1. Create develop branch from current main
git checkout main
git pull origin main
git checkout -b develop
git push origin develop

# 2. Set develop as default branch on GitHub
# Settings → Branches → Default branch → develop

# 3. Set up branch protection rules
# Settings → Branches → Add rule
```

### Existing Branches

```bash
# Rename existing feature branches
git branch -m old-feature-name feature/new-name

# Update remote
git push origin :old-feature-name
git push origin feature/new-name
```

---

## Resources

- **Original Article:** [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- **git-flow cheatsheet:** [https://danielkummer.github.io/git-flow-cheatsheet/](https://danielkummer.github.io/git-flow-cheatsheet/)
- **Git Flow Tutorial:** [Atlassian Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- **Semantic Versioning:** [semver.org](https://semver.org/)
- **Conventional Commits:** [conventionalcommits.org](https://conventionalcommits.org/)

---

## Questions?

For Git Flow questions:
1. Check this guide and examples
2. Review [CONTRIBUTING.md](../CONTRIBUTING.md)
3. See [VERSIONING.md](VERSIONING.md)
4. Ask in [Discussions](https://github.com/Soriarty/HaloSense/discussions)

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28
