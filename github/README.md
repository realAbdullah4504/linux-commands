# Git and GitHub Commands

This directory contains comprehensive Git and GitHub commands and documentation organized by topic.

## 📚 Quick Navigation

### 📋 Git Essentials
- **[setup.md](./setup.md)** - SSH setup and initial configuration
- **[basic-commands.md](./basic-commands.md)** - Essential Git commands for daily use
- **[branching.md](./branching.md)** - Branch management and strategies

### 🔧 Advanced Git
- **[advanced.md](./advanced.md)** - Advanced Git operations and workflows
- **[troubleshooting.md](./troubleshooting.md)** - Common issues and solutions

## 🎯 Quick Reference Commands

### Repository Setup
```bash
git init                 # Initialize repository
git clone <url>          # Clone repository
git remote add origin <url> # Add remote
```

### Daily Workflow
```bash
git add .                # Stage all changes
git commit -m "message"  # Commit changes
git push origin main      # Push to remote
git pull origin main      # Pull from remote
```

### Branch Management
```bash
git branch               # List branches
git checkout -b new     # Create and switch branch
git merge feature        # Merge branch
git branch -d feature    # Delete branch
```

### History and Inspection
```bash
git log                 # Show commit history
git log --oneline       # Compact log view
git status              # Show working directory status
git diff                # Show unstaged changes
```

### Undo Operations
```bash
git checkout -- <file>  # Discard changes to file
git reset HEAD~1        # Reset to previous commit
git revert <commit>     # Create new commit to undo changes
```

## 🔍 Search Commands

### Find Git Commands
```bash
# By category
grep -r "clone" ./github/           # Clone-related commands
grep -r "branch" ./github/          # Branch management
grep -r "merge" ./github/           # Merge operations
```

### By Use Case
```bash
# Repository initialization
grep -r "init\|clone\|remote" ./github/setup.md ./github/basic-commands.md

# Branch operations
grep -r "checkout\|merge\|rebase" ./github/branching.md ./github/advanced.md

# Troubleshooting
grep -r "error\|fix\|resolve" ./github/troubleshooting.md
```

## 📖 Usage Tips

### For Beginners
1. Start with [setup.md](./setup.md) to configure Git
2. Learn daily commands with [basic-commands.md](./basic-commands.md)
3. Practice branching with [branching.md](./branching.md)

### For Advanced Users
1. Master advanced workflows with [advanced.md](./advanced.md)
2. Learn troubleshooting with [troubleshooting.md](./troubleshooting.md)

## 🛠️ Common Workflows

### Feature Branch Workflow
```bash
# 1. Create feature branch
git checkout -b feature/new-feature

# 2. Make changes and commit
git add .
git commit -m "Add new feature"

# 3. Push and create pull request
git push origin feature/new-feature
```

### Hotfix Workflow
```bash
# 1. Create hotfix branch from main
git checkout -b hotfix/critical-bug

# 2. Fix and commit
git add .
git commit -m "Fix critical bug"

# 3. Merge and push
git checkout main
git merge hotfix/critical-bug
git push origin main
```

## 📚 Additional Resources

### Documentation
- [Pro Git Book](https://git-scm.com/book)
- [GitHub Docs](https://docs.github.com/)
- [Git Reference](https://git-scm.com/docs)

### Tools
- [GitHub CLI](https://cli.github.com/)
- [Git LFS](https://git-lfs.github.com/)
- [SourceTree](https://www.sourcetreeapp.com/)

---

**💡 Pro Tip:** Use `git help <command>` to get detailed help for any Git command.

**🔖 Bookmark this page** for quick access to essential Git commands!
