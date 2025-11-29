# Branch Protection Configuration

GitHub branch protection settings for the HaloSense project.

## Overview

HaloSense uses **Classic Branch Protection Rules** to protect critical branches from accidental or unauthorized changes.

**Configuration Date:** 2025-11-28

---

## Protected Branches

### Main Branch (`main`)

**Purpose:** Production-ready code only

**Protection Rules:**

✅ **Require Pull Request Before Merging**
- Require approvals: **1**
- Dismiss stale pull request approvals when new commits are pushed: **Yes**
- Require review from Code Owners: **Optional**

✅ **Require Conversation Resolution Before Merging**
- All review comments must be resolved before merge

✅ **Require Signed Commits** (Optional but Recommended)
- All commits must be signed with GPG/SSH key

✅ **Do Not Allow Force Pushes**
- Force pushes are blocked to prevent history rewriting

✅ **Do Not Allow Deletions**
- Branch cannot be deleted

✅ **Restrict Who Can Push**
- Only maintainers can push (or nobody if strict PR-only workflow)
- Currently configured: **[@Soriarty](https://github.com/Soriarty)**

**Bypass Settings:**
- Do not allow bypassing the above settings: **Yes**

---

### Develop Branch (`develop`)

**Purpose:** Integration branch for ongoing development

**Protection Rules:**

✅ **Require Pull Request Before Merging**
- Require approvals: **1**
- Dismiss stale approvals: **Optional** (more lenient for development)

✅ **Require Conversation Resolution Before Merging**
- All review comments must be resolved

✅ **Do Not Allow Force Pushes**
- Force pushes are blocked

**Less Strict Than Main:**
- Signed commits: Optional
- Branch deletion: Allowed (though unlikely to be needed)
- Status checks: Optional (unless CI/CD configured)

---

## Why These Settings?

### Main Branch Protection

**Strict protection ensures:**
- ✅ Production code is always reviewed
- ✅ No accidental direct commits
- ✅ No history rewriting (force push blocked)
- ✅ Branch cannot be deleted
- ✅ All conversations resolved before merge
- ✅ Maintains clean, traceable history

**Perfect for:**
- Tagged releases
- Production deployments
- Stable version history
- Customer-facing code

### Develop Branch Protection

**Moderate protection allows:**
- ✅ Faster feature integration
- ✅ Easier collaboration
- ✅ Quick bug fixes
- ✅ Less overhead for development

**Still protected from:**
- ❌ Force pushes (history stays intact)
- ❌ Direct commits (all via PR)
- ❌ Unresolved review comments

---

## Git Flow Integration

### Feature Branches → Develop

```bash
# Create feature
git checkout develop
git checkout -b feature/my-feature

# Work and commit
git commit -m "feat(sensor): add feature"

# Push and create PR to develop
git push origin feature/my-feature
```

**Protection Applies:**
- ✅ PR required to merge into `develop`
- ✅ 1 approval needed
- ✅ Cannot force push to `develop`

### Release Branches → Main

```bash
# Create release
git checkout develop
git checkout -b release/1.0.0

# Prepare release
npm run release

# Create PR to main
git push origin release/1.0.0
```

**Protection Applies:**
- ✅ PR required to merge into `main`
- ✅ 1 approval needed
- ✅ All conversations must be resolved
- ✅ Cannot force push to `main`
- ✅ Cannot delete `main`

### Hotfix Branches → Main

```bash
# Create hotfix from main
git checkout main
git checkout -b hotfix/1.0.1

# Fix bug
git commit -m "fix: critical bug"

# Create PR to main
git push origin hotfix/1.0.1
```

**Protection Applies:**
- Same as release branches
- Emergency fixes still require PR + review

---

## Override/Bypass Scenarios

### When Can Protection Be Bypassed?

**Main Branch:**
- **Never** - Protection cannot be bypassed
- Even repository admins must follow PR process

**Develop Branch:**
- **Emergency only** - Repository admins only
- Should be documented when used

### Emergency Override Process

If absolutely necessary (e.g., security vulnerability):

1. **Document the reason** in issue tracker
2. **Notify team** via communication channels
3. **Create emergency PR** with clear description
4. **Fast-track review** with available maintainer
5. **Post-merge review** if pushed without review

**Log emergency overrides in:** `docs/EMERGENCY_CHANGES.md`

---

## Testing Branch Protection

### Test 1: Direct Push to Main (Should Fail)

```bash
# Try to push directly to main
git checkout main
echo "test" >> test.txt
git add test.txt
git commit -m "test: direct commit"
git push origin main

# Expected result:
# remote: error: GH006: Protected branch update failed
# To https://github.com/Soriarty/HaloSense.git
#  ! [remote rejected] main -> main (protected branch hook declined)
# error: failed to push some refs
```

### Test 2: Force Push to Develop (Should Fail)

```bash
# Try to force push to develop
git push -f origin develop

# Expected result:
# remote: error: GH006: Protected branch update failed
# To https://github.com/Soriarty/HaloSense.git
#  ! [remote rejected] develop -> develop (protected branch hook declined)
# error: failed to push some refs
```

### Test 3: Valid PR Workflow (Should Succeed)

```bash
# Create feature branch
git checkout develop
git checkout -b feature/test-protection

# Make changes
echo "test" >> test.txt
git add test.txt
git commit -m "feat(test): test branch protection"

# Push feature branch
git push origin feature/test-protection

# Create PR on GitHub: feature/test-protection → develop
# Request review → Get approval → Merge
# ✅ Should succeed
```

---

## Updating Protection Rules

### When to Update

**Consider updating when:**
- Team size changes
- Contribution volume increases
- CI/CD pipeline added
- Security requirements change
- Community guidelines evolve

### How to Update

1. **GitHub → Settings → Branches**
2. **Find rule** (e.g., `main` or `develop`)
3. **Click Edit**
4. **Modify settings**
5. **Save changes**
6. **Update this documentation**
7. **Notify team** of changes

### Recommended Updates for Future

**When CI/CD is added:**
- Enable "Require status checks to pass before merging"
- Add required checks: `build`, `test`, `lint`

**When team grows:**
- Increase required approvals to 2
- Enable "Require review from Code Owners"
- Add CODEOWNERS file

**When security is critical:**
- Enable "Require signed commits" (mandatory)
- Enable "Require deployment to succeed"
- Add security scanning checks

---

## Branch Protection Matrix

| Feature | Main | Develop | Feature/* | Release/* | Hotfix/* |
|---------|------|---------|-----------|-----------|----------|
| **Protected** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Require PR** | ✅ | ✅ | - | - | - |
| **Require Approvals** | 1 | 1 | - | - | - |
| **Block Force Push** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Block Deletion** | ✅ | ⚠️ | ❌ | ❌ | ❌ |
| **Signed Commits** | ⚠️ | ⚠️ | ❌ | ❌ | ❌ |
| **Status Checks** | ⚠️ | ⚠️ | - | - | - |
| **Conversation Resolution** | ✅ | ✅ | - | - | - |

**Legend:**
- ✅ Enabled
- ⚠️ Optional/Recommended
- ❌ Not enabled/Not protected
- `-` Not applicable

---

## CODEOWNERS File (Future)

When team grows, create `.github/CODEOWNERS`:

```
# HaloSense Code Owners

# Default owners for everything
* @Soriarty

# Hardware design
/hardware/ @Soriarty @hardware-team

# Firmware
/firmware/ @Soriarty @firmware-team

# Documentation
/docs/ @Soriarty @docs-team

# Enclosure design
/enclosure/ @Soriarty @mechanical-team
```

**Benefits:**
- Automatic reviewer assignment
- Required reviews from domain experts
- Clear ownership structure

---

## Status Checks (Future)

When CI/CD is implemented, enable required checks:

**Main Branch:**
```yaml
Required checks:
  - build-hardware-docs
  - compile-firmware
  - run-tests
  - lint-commits
  - security-scan
```

**Develop Branch:**
```yaml
Required checks:
  - build
  - test
  - lint
```

**Configuration:**
- Settings → Branches → Edit rule
- "Require status checks to pass before merging"
- Select required checks from list

---

## Common Issues

### Issue: Can't Push to Main

**Symptom:**
```
error: GH006: Protected branch update failed
```

**Solution:**
✅ This is expected behavior!
- Create PR instead of direct push
- Follow Git Flow workflow
- Push to feature/release/hotfix branch first

### Issue: PR Can't Merge (Requires Approval)

**Symptom:**
"Merging is blocked" - Requires 1 approval

**Solution:**
- Request review from team member
- Wait for approval
- If solo developer, you may need to adjust settings

### Issue: Force Push Needed

**Symptom:**
Need to rewrite history but blocked

**Solution:**
- ❌ Don't force push to main/develop!
- ✅ Create new branch and PR
- ✅ Revert commits if needed
- ✅ Fix forward, not backward

---

## Best Practices

### DO ✅

- Always work in feature branches
- Create PR for all changes to main/develop
- Request reviews before merging
- Resolve all conversations
- Test locally before pushing
- Write clear PR descriptions
- Link PRs to issues
- Follow conventional commits

### DON'T ❌

- Never try to force push to protected branches
- Don't bypass protection rules
- Don't commit directly to main/develop
- Don't merge without approval
- Don't delete protected branches
- Don't ignore review comments
- Don't rewrite history on shared branches

---

## Monitoring

### Regular Checks

**Weekly:**
- Review protection settings still appropriate
- Check for any bypass attempts (GitHub audit log)
- Verify team members have correct permissions

**Monthly:**
- Review PR approval patterns
- Assess if rules too strict/lenient
- Update documentation if rules changed

**Quarterly:**
- Full security review
- Update protection rules based on team growth
- Review and update CODEOWNERS

---

## References

- [GitHub Branch Protection Docs](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [Git Flow Workflow](GITFLOW.md)
- [Contributing Guidelines](../CONTRIBUTING.md)
- [Conventional Commits](CONVENTIONAL_COMMITS.md)

---

## Change Log

### 2025-11-28: Initial Setup

**Main Branch:**
- ✅ Require PR with 1 approval
- ✅ Block force push
- ✅ Block deletion
- ✅ Require conversation resolution
- ⚠️ Signed commits (optional)

**Develop Branch:**
- ✅ Require PR with 1 approval
- ✅ Block force push
- ✅ Require conversation resolution

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense

**Last Updated:** 2025-11-28
