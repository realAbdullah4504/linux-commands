# Basic Git Commands

## Daily Workflow Commands

### Status and Information
```bash
# Check repository status
git status

# View commit history
git log

# View commit history (one line)
git log --oneline

# Show commit details
git show <commit-hash>

# Show file changes
git diff

# Show staged changes
git diff --staged
```

### Staging and Committing
```bash
# Add specific file
git add filename.txt

# Add all files
git add .

# Add all files with message
git add -A

# Commit with message
git commit -m "Your commit message"

# Commit all staged files
git commit

# Amend last commit
git commit --amend
```

### Pushing and Pulling
```bash
# Push to remote
git push origin main

# Push and set upstream
git push -u origin main

# Pull latest changes
git pull origin main

# Pull with rebase
git pull --rebase origin main

# Fetch without merging
git fetch origin
```

## File Management

### Restoring Files
```bash
# Restore file to last commit
git restore filename.txt

# Restore all files
git restore .

# Unstage file
git restore --staged filename.txt
```

### Cleaning
```bash
# Remove untracked files
git clean

# Remove untracked files and directories
git clean -fd

# Remove untracked files interactively
git clean -i
```

## History and Navigation

### Moving Through History
```bash
# Reset to specific commit (keep changes)
git reset <commit-hash>

# Reset to specific commit (discard changes)
git reset --hard <commit-hash>

# Reset to specific commit (keep staged)
git reset --soft <commit-hash>

# Reset to specific commit (keep working directory)
git reset --mixed <commit-hash>
```

### Stashing
```bash
# Stash current changes
git stash

# Stash with message
git stash save "Work in progress"

# List stashes
git stash list

# Apply stash
git stash apply

# Apply and remove stash
git stash pop

# Drop specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```
