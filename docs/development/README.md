# Development Workflow Documentation

This directory contains developer workflow guides, standards, and best practices for contributing to the HaloSense project.

## 📄 Documents

### Version Control & Git

- **[git-flow.md](git-flow.md)** - Git Flow branching strategy
  - Branch types: main, develop, feature/*, release/*, hotfix/*
  - Complete workflow examples
  - Pull request process
  - Branch protection rules

- **[branch-protection.md](branch-protection.md)** - Branch protection configuration
  - main branch protection rules
  - develop branch protection rules
  - GitHub settings reference

### Code Standards

- **[conventional-commits.md](conventional-commits.md)** - Commit message format
  - Conventional Commits specification
  - Type and scope reference
  - Examples and validation
  - Commitlint configuration

- **[versioning.md](versioning.md)** - Semantic versioning strategy
  - Version numbering (MAJOR.MINOR.PATCH)
  - Pre-release versions (alpha, beta, rc)
  - Version tagging workflow
  - CHANGELOG management

### Documentation

- **[github-wiki.md](github-wiki.md)** - Wiki strategy and architecture
  - Wiki as Git submodule
  - User vs developer documentation separation
  - Wiki update workflow
  - Content organization

## 🔗 Related Documentation

- **[Sensor Documentation](../sensors/README.md)** - All sensors technical specs
- **[Hardware Documentation](../hardware/README.md)** - Power budget, IP rating, design specs
- **[Project Documentation](../../README.md)** - Main project README
- **[Contributing Guidelines](../../CONTRIBUTING.md)** - How to contribute

## 🛠️ Quick Links

- **Git Flow Workflow:** Start here for branching strategy
- **Conventional Commits:** Required for all commits (validated by commitlint)
- **Pull Requests:** Must target `develop` branch (except hotfixes)
- **Versioning:** Semantic versioning with standard-version automation

---

**Last Updated:** 2025-11-29
