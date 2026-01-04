# Git Branching Strategies

## Branch Management

### Basic Branch Operations
```bash
# List all branches
git branch

# List all branches (including remote)
git branch -a

# Create new branch
git branch feature/new-feature

# Switch to branch
git checkout feature/new-feature

# Create and switch to branch
git checkout -b feature/new-feature

# Rename branch
git branch -m old-name new-name

# Delete local branch
git branch -d branch-name

# Delete remote branch
git push origin --delete branch-name
```

## Branching Strategy

### Recommended Branch Naming Convention

#### Feature Branches
```bash
feature/login-page
feature/add-logout
feature/user-profile
```

#### Bug Fix Branches
```bash
bugfix/fix-404-error
bugfix/fix-login-issue
bugfix/memory-leak-fix
```

#### Hotfix Branches
```bash
hotfix/critical-security-patch
hotfix/payment-gateway-fix
hotfix/database-connection-fix
```

#### Release Branches
```bash
release/1.2.0
release/v2.0.0
release/beta-release
```

#### Chore Branches
```bash
chore/update-readme
chore/refactor-code
chore/update-dependencies
```

### Advantages of Structured Branching

#### 1. Improved Organization
- Clear purpose for each branch
- Easy to identify branch type at a glance
- Consistent naming across team

#### 2. Easier Collaboration in Teams
- Teams can use prefixes like `feature/`, `bugfix/`, `hotfix/` to clearly indicate type of work
- Eliminates guesswork when looking at branch names in repository
- Better code review organization

#### 3. Better Tool Support
- Git GUI tools handle nested names well
- Command-line tab completion works efficiently
- Example: `git checkout feature/<tab>`

#### 4. Easier Automation
- GitHub Actions can filter by branch patterns
- CI/CD pipelines can have different rules per branch type

Example GitHub Actions configuration:
```yaml
on:
  push:
    branches:
      - feature/*
      - hotfix/*
      - release/*
```

## Merging Strategies

### Merge vs Rebase
```bash
# Merge branch (creates merge commit)
git merge feature/new-feature

# Rebase branch (linear history)
git rebase main

# Pull with rebase
git pull --rebase origin main
```

### Cherry-Picking
```bash
# Cherry-pick specific commit
git cherry-pick <commit-hash>

# Cherry-pick with signed commit
git cherry-pick -s <commit-hash>

# Cherry-pick from merge commit (specify parent)
git cherry-pick -m 1 <merge-commit-hash>
```

## Branch Protection

### GitHub Branch Protection Rules
- Require pull request reviews
- Require status checks to pass
- Include administrators
- Limit who can push to branch

### Local Branch Protection
```bash
# Prevent force push to main
git config branch.main.pushRemote origin
git config branch.main.pushMergeOptions "--no-ff"
```
