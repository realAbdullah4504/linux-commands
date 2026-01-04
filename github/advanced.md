# Advanced Git Operations

## Rebase and Interactive Rebase

### Basic Rebase
```bash
# Rebase current branch onto main
git rebase main

# Rebase with specific upstream
git rebase upstream/main

# Continue rebase after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort

# Skip current commit during rebase
git rebase --skip
```

### Interactive Rebase
```bash
# Interactive rebase of last 5 commits
git rebase -i HEAD~5

# Interactive rebase from specific commit
git rebase -i <commit-hash>

# Common interactive rebase commands:
# pick = use commit
# reword = edit commit message
# edit = stop for amending
# squash = merge with previous commit
# fixup = merge with previous (discard message)
# drop = remove commit
```

## Rewriting History

### Squashing Commits
```bash
# Interactive rebase for squashing
git rebase -i HEAD~n

# Soft reset to combine commits
git reset --soft <commit-hash>
git commit -m "Combined commit message"
```

### Filter Branch
```bash
# Filter branch to specific directory
git filter-branch --subdirectory-filter path/to/dir HEAD

# Remove file from history
git filter-branch --tree-filter 'rm -f filename' HEAD

# Change author information
git filter-branch --env-filter '
  if [ "$GIT_AUTHOR_NAME" = "Old Name" ]; then
    export GIT_AUTHOR_NAME="New Name"
    export GIT_AUTHOR_EMAIL="new.email@example.com"
  fi
' HEAD
```

## Tag Management

### Tag Operations
```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Version 1.0.0"

# Create tag with specific commit
git tag v1.0.0 <commit-hash>

# List all tags
git tag

# List tags with details
git tag -l -n1

# Push specific tag
git push origin v1.0.0

# Push all tags
git push --tags

# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0
```

## Submodules

### Submodule Management
```bash
# Add submodule
git submodule add https://github.com/user/repo.git path/to/submodule

# Clone repository with submodules
git clone --recursive https://github.com/user/repo.git

# Initialize and update submodules
git submodule update --init --recursive

# Update all submodules to latest
git submodule update --remote --merge

# Remove submodule
git submodule deinit path/to/submodule
git rm path/to/submodule
git commit -m "Remove submodule"
```

## Worktrees

### Multiple Working Directories
```bash
# Create new worktree
git worktree add ../feature-branch feature-branch

# List worktrees
git worktree list

# Remove worktree
git worktree remove ../feature-branch

# Prune worktrees
git worktree prune
```

## Bisect and Blame

### Finding Bugs
```bash
# Start bisect
git bisect start

# Mark current commit as bad
git bisect bad

# Mark known good commit
git bisect good <commit-hash>

# Automatic bisect
git bisect run ./test-script.sh

# End bisect
git bisect reset
```

### File History
```bash
# Show who changed what and when
git blame filename.txt

# Show blame with specific commit range
git blame <commit-hash>~..<commit-hash> filename.txt

# Ignore whitespace changes in blame
git blame -w filename.txt
```

## Maintenance and Optimization

### Repository Cleanup
```bash
# Clean unnecessary files
git clean -fd

# Garbage collection
git gc

# Aggressive garbage collection
git gc --aggressive

# Prune unreachable objects
git prune

# Pack loose objects
git repack -a -d

# Verify repository integrity
git fsck
```

## Advanced Merge Strategies

### Merge Strategies
```bash
# Specify merge strategy
git merge -s recursive -X theirs feature-branch

# Octopus merge (multiple branches)
git merge branch1 branch2 branch3

# Ours strategy (always choose ours)
git merge -s ours feature-branch
```

### Resolve Merge Conflicts
```bash
# Check conflict markers
git diff --name-only --diff-filter=U

# Use our version
git checkout --ours filename.txt

# Use their version
git checkout --theirs filename.txt

# Mark conflicts as resolved
git add filename.txt
```
