# 🤝 Contributing Guide

[![Branching Strategy](https://img.shields.io/badge/Branching-Cascade_Flow-blue)](CONTRIBUTING.md)
[![Workflows](https://img.shields.io/badge/GitHub_Actions-Automated-green)](../../actions)

> 🌐 **¿Prefieres Español?** [Ver versión en español](CONTRIBUTING.es.md)

Thank you for your interest in contributing to **Danger From The Deep - Godot Edition**. This document describes the workflow, conventions, and best practices for collaborating on this project.

---

## 📋 Table of Contents

- [Branch Workflow](#-branch-workflow)
- [Branch Structure](#-branch-structure)
- [Merge Rules](#-merge-rules)
- [How to Contribute](#-how-to-contribute)
- [Automated Workflows](#-automated-workflows)
- [Conflict Resolution](#-conflict-resolution)
- [Best Practices](#-best-practices)

---

## 🌳 Branch Workflow

This project uses a **cascade flow** with 6 main branches representing different development stages:

```
pre-alpha → alpha → beta → rc → rtm → main
```

### Cascade Order

Changes must flow sequentially through the branches:

1. **pre-alpha** - Active and experimental development
2. **alpha** - Internal testing and stabilization
3. **beta** - External testing and community feedback
4. **rc** - Release Candidate
5. **rtm** - Release To Manufacturing (production-ready)
6. **main** - Stable production version

---

## 🔧 Branch Structure

### Protected Branches (Cannot be deleted)

| Branch | Purpose | Stability | Direct Commits | PRs |
|--------|---------|-----------|----------------|-----|
| `pre-alpha` | Active development, experimental features | Unstable | ✅ Allowed | ✅ Validated |
| `alpha` | Internal testing, complete features | Low | ✅ Allowed | ✅ Validated |
| `beta` | Public testing, bug fixes | Medium | ✅ Allowed | ✅ Validated |
| `rc` | Release candidate, final testing | High | ✅ Allowed | ✅ Validated |
| `rtm` | Release to manufacturing | Very High | ✅ Allowed | ✅ Validated |
| `main` | Production code | Stable | ❌ **Blocked** | ✅ **PRs Only** |

> ⚠️ **Important:** The `main` branch **does NOT accept direct commits**. All changes must be made through approved Pull Requests.

### Temporary Branches

You can create temporary branches for features, fixes, or experiments:

**Recommended naming:**

```bash
feature/descriptive-name         # New functionality
fix/bug-description              # Bug fixes
hotfix/critical-issue            # Urgent fixes
refactor/code-improvement        # Refactoring
docs/documentation-update        # Documentation
test/new-tests                   # Tests
experiment/new-idea              # Experimentation
```

**Examples:**
```bash
feature/submarine-torpedos
fix/collision-detection-bug
hotfix/memory-leak-critical
docs/update-api-documentation
```

---

## ⚙️ Merge Rules

### ✅ Allowed

1. **Feature branches → pre-alpha**
   ```bash
   feature/new-functionality → pre-alpha ✅
   ```
   - All new features must go to `pre-alpha` first

2. **Sequential cascade between protected branches**
   ```bash
   pre-alpha → alpha ✅
   alpha → beta ✅
   beta → rc ✅
   rc → rtm ✅
   rtm → main ✅ (via PR only)
   ```

3. **Direct commits to development branches**
   ```bash
   git checkout alpha
   git commit -m "fix: minor correction"
   git push origin alpha ✅
   ```
   - You can make direct commits to: `pre-alpha`, `alpha`, `beta`, `rc`, `rtm`
   - ⚠️ **Exception**: `main` only accepts changes through Pull Requests

### ❌ Blocked

1. **Feature branches to other branches (not pre-alpha)**
   ```bash
   feature/new → alpha ❌
   feature/new → main ❌
   ```

2. **Skipping levels in cascade**
   ```bash
   pre-alpha → beta ❌  (skips alpha)
   alpha → rc ❌        (skips beta)
   beta → main ❌       (skips rc and rtm)
   ```

3. **Reverse merge**
   ```bash
   main → rtm ❌
   beta → alpha ❌
   ```

4. **Direct commits to main**
   ```bash
   git checkout main
   git commit -m "fix"
   git push origin main ❌
   ```
   - `main` is a **protected branch** that only accepts changes through approved Pull Requests
   - GitHub will automatically block any direct commit attempts

5. **Delete protected branches**
   ```bash
   git push origin --delete main ❌
   git push origin --delete pre-alpha ❌
   ```

---

## 🚀 How to Contribute

### Step 1: Fork and Clone

```bash
# Fork the repository on GitHub (click "Fork" button)

# Clone your fork
git clone https://github.com/YOUR_USERNAME/dftdg.git
cd dftdg

# Add upstream
git remote add upstream https://github.com/NippurElErrante/dftdg.git
```

### Step 2: Create Feature Branch

```bash
# Update pre-alpha
git checkout pre-alpha
git pull upstream pre-alpha

# Create your branch
git checkout -b feature/my-new-feature
```

### Step 3: Develop

```bash
# Make changes
# ... edit files ...

# Frequent commits
git add .
git commit -m "feat: add new feature X"

# Push to your fork
git push origin feature/my-new-feature
```

### Step 4: Create Pull Request

1. Go to GitHub on your fork
2. Click **"Compare & pull request"**
3. **Base**: `pre-alpha` (from original repo)
4. **Compare**: `feature/my-new-feature` (from your fork)
5. Add detailed description
6. Click **"Create pull request"**

### Step 5: Automatic Validation

The system will automatically run:

- ✅ **Validate Cascade Order** - Verifies the PR follows cascade rules
- ✅ Automated tests (if configured)

**If check passes:** ✅ Your PR can be merged  
**If check fails:** ❌ Review the error and fix the PR target

### Step 6: Review and Merge

- A maintainer will review your code
- May request changes
- Once approved, it will be merged to `pre-alpha`
- Cascade to other branches will be done manually when appropriate

---

## 🤖 Automated Workflows

### 1. Validate Cascade Order

**Runs:** Automatically on every Pull Request

**Function:** Validates that the PR follows the correct cascade order

**Results:**
- ✅ **Pass** - Correct PR, can be merged
- ❌ **Fail** - Incorrect PR, merge button blocked

**Example error:**
```
ERROR: Cannot skip levels. pre-alpha must go to next level first
Expected target: alpha
```

### 2. Cascade Merge (Manual)

**Runs:** Manually from GitHub Actions

**Function:** Create cascade PRs or direct merge between branches

**How to use:**

1. Go to **Actions** → **Cascade Merge**
2. Click **"Run workflow"**
3. Configure:
   - **source_branch**: Where to start (e.g., `pre-alpha`)
   - **target_branch**: Where to end (empty = to `main`)
   - **mode**: 
     - `create-prs` - Creates PRs for manual review (recommended)
     - `direct-merge` - Direct merge without PRs (emergencies only)
4. Click **"Run workflow"**

**Usage example:**

To propagate changes from `pre-alpha` to all other branches:

```
source_branch: pre-alpha
target_branch: (empty)
mode: create-prs
```

This will automatically create:
- PR #1: pre-alpha → alpha
- PR #2: alpha → beta
- PR #3: beta → rc
- PR #4: rc → rtm
- PR #5: rtm → main

Then you can review and merge each PR manually.

---

## 🔧 Conflict Resolution

### During Development

Keep your branch updated with `pre-alpha`:

```bash
git checkout feature/my-feature
git fetch upstream
git merge upstream/pre-alpha
# Resolve conflicts if any
git push origin feature/my-feature
```

### During Cascade

If there are conflicts during cascade, the automatic workflow:

1. **Detects the conflict**
2. **Creates a PR** instead of direct merge
3. **You resolve** conflicts manually
4. **Merge** the PR after resolving

---

## ✨ Best Practices

### Commits

✅ **Use descriptive messages**
```bash
# Good
git commit -m "feat: add torpedo system to submarine"
git commit -m "fix: correct iceberg collision"
git commit -m "docs: update installation guide"

# Bad
git commit -m "changes"
git commit -m "fix"
git commit -m "update"
```

✅ **Commit convention** (recommended):
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `style:` - Formatting, missing semicolons, etc.
- `refactor:` - Code refactoring
- `test:` - Adding tests
- `chore:` - Maintenance tasks

### Pull Requests

✅ **Small, focused PRs**
- One PR = One feature or fix
- Easier to review
- Faster to merge

✅ **Clear description**
```markdown
## Description
Implements torpedo system for U-Boot submarine.

## Changes
- Add `Torpedo` class with realistic physics
- Implement UI for torpedo launch
- Add sound and visual effects

## Tests
- [x] Unit tests for Torpedo class
- [x] Integration tests with combat system
- [x] Manual testing in battle scenario

## Screenshots
![torpedo-ui](link-to-image)
```

### Branches

✅ **Descriptive names**
```bash
# Good
feature/submarine-damage-system
fix/sonar-display-rendering-bug

# Bad
feature/stuff
fix/bug
my-branch
```

✅ **Delete branches after merge**
```bash
# After your PR is merged
git checkout pre-alpha
git pull upstream pre-alpha
git branch -d feature/my-feature
git push origin --delete feature/my-feature
```

### Testing

✅ **Test before creating PR**
- Compile the project
- Run existing tests
- Manually test functionality
- Verify you didn't break existing code

---

## 📊 Complete Example Flow

```bash
# 1. Update pre-alpha
git checkout pre-alpha
git pull upstream pre-alpha

# 2. Create feature branch
git checkout -b feature/new-sonar-display

# 3. Develop
# ... make changes ...
git add .
git commit -m "feat: implement new sonar display with better graphics"

# 4. Push
git push origin feature/new-sonar-display

# 5. Create PR on GitHub
#    Base: pre-alpha
#    Compare: feature/new-sonar-display

# 6. Wait for review and merge

# 7. (Optional) A maintainer runs Cascade Merge
#    This propagates changes from pre-alpha → alpha → beta → rc → rtm → main

# 8. Clean up your local branch
git checkout pre-alpha
git pull upstream pre-alpha
git branch -d feature/new-sonar-display
git push origin --delete feature/new-sonar-display
```

---

## 🔐 Branch Protections

### Current Configuration

| Protection | Affected Branches | Description |
|------------|-------------------|-------------|
| **No deletion** | All (pre-alpha → main) | Cannot delete the 6 main branches |
| **Cascade validation** | All (pre-alpha → main) | PRs must follow sequential order |
| **PRs only** | **main** only | Direct commits blocked, approved PRs only |

### Active Rulesets

1. **protected-branches-no-delete**: Prevents deletion of main branches
2. **require-cascade-checks**: Validates order in Pull Requests
3. **main-require-pull-requests**: Blocks direct commits to main

---

## 🆘 Need Help?

- 💬 **Issues**: [Create an issue](../../issues/new)
- 📖 **Documentation**: See [README](README.md)
- 🐛 **Report bug**: [Bug report template](../../issues/new?template=bug_report.md)
- 💡 **Suggest feature**: [Feature request template](../../issues/new?template=feature_request.md)

---

## 📜 License

By contributing to this project, you agree that your contributions will be published under the **GNU General Public License v3.0 (GPLv3)**.

See [LICENSE](LICENSE) for more details.

---

## 🙏 Acknowledgments

Thank you for contributing to **Danger From The Deep - Godot Edition**! Your contribution helps keep this classic submarine simulator alive.

**Set sail with us on this exciting mission! ⚓🌊**
