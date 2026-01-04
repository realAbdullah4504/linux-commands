# Git Troubleshooting

## Common Issues and Solutions

### Undo Changes

### Undo Last Commit
```bash
# If you want to keep your changes staged for committing again:
git reset --soft <commit-hash>

# If you want to revert to database connection fixes as a new commit:
git revert <commit-hash>

# First copy backup and then again apply backup:
git reset --hard dev-backup
```

### Reset to Previous State
```bash
# Reset to specific commit (keep changes)
git reset <commit-hash>

# Reset to specific commit (discard changes)
git reset --hard <commit-hash>

# Reset to specific commit (keep staged)
git reset --soft <commit-hash>
```

### Revert Merge Commits
```bash
# Revert merge commit (specify parent)
git revert -m 1 <merge-commit-hash>

# Revert specific commit
git revert <commit-hash>
```

## Merge Conflicts

### Resolve Conflicts
```bash
# Check which files have conflicts
git status

# View conflict markers
git diff

# Use our version
git checkout --ours filename.txt

# Use their version
git checkout --theirs filename.txt

# Mark as resolved
git add filename.txt
git commit
```

### Prevent Conflicts
```bash
# Pull with rebase to avoid merge commits
git pull --rebase origin main

# Stash before pull
git stash
git pull
git stash pop
```

## Remote Issues

### Force Push
```bash
# Force push (use with caution)
git push --force origin main

# Force push with lease (safer)
git push --force-with-lease origin main
```

### Remote Sync Issues
```bash
# Update remote references
git remote update origin

# Prune stale remote branches
git remote prune origin

# Fetch all branches
git fetch --all
```

## File Issues

### Line Ending Problems
```bash
# Configure for Windows
git config --global core.autocrlf input

# Configure for Linux/Mac
git config --global core.autocrlf output

# Check current setting
git config --global core.autocrlf

# Reference: https://betterstack.com/community/questions/git-replacing-lf-with-crlf/
```

### File Permissions
```bash
# Make files executable in Git
git update-index --chmod=+x scripts/*

# Ignore file mode changes
git config core.fileMode false

# Check file permissions
git ls-files --stage
```

## Repository Corruption

### Check Repository Health
```bash
# Check repository integrity
git fsck

# Check for dangling objects
git fsck --unreachable

# Check for lost commits
git fsck --lost-found
```

### Recover Lost Commits
```bash
# Find lost commits
git fsck --lost-found

# Show lost commits
git log --reflog

# Recover lost commit
git merge <lost-commit-hash>
```

## Performance Issues

### Large Repository
```bash
# Garbage collection
git gc

# Aggressive garbage collection
git gc --aggressive

# Repack objects
git repack -a -d

# Prune loose objects
git prune
```

### Shallow Clone
```bash
# Clone with limited history
git clone --depth 1 https://github.com/user/repo.git

# Clone with specific depth
git clone --depth 50 https://github.com/user/repo.git

# Unshallow repository
git fetch --unshallow
```

## Authentication Issues

### SSH Key Problems
```bash
# Generate new SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Add SSH key to agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Test SSH connection
ssh -T git@github.com
```

### Credential Issues
```bash
# Configure credential helper
git config --global credential.helper manager

# Remove stored credentials
git config --global --unset credential.helper

# Cache credentials temporarily
git config --global credential.helper 'cache --timeout=3600'
```

## Branch Issues

### Orphaned Branches
```bash
# Find orphaned branches
git branch -a

# Delete remote branch
git push origin --delete branch-name

# Delete local branch
git branch -d branch-name

# Force delete local branch
git branch -D branch-name
```

### Detached HEAD
```bash
# Check if in detached HEAD
git status

# Create branch from detached HEAD
git checkout -b new-branch-name

# Return to previous branch
git checkout -
```

## Useful Debug Commands

### Debug Information
```bash
# Show all configuration
git config --list

# Show remote URLs
git remote -v

# Show reflog
git reflog

# Show commit graph
git log --graph --oneline --all

# Show unreachable commits
git log --reflog
```
