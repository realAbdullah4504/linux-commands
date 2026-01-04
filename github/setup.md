# Git Setup and Configuration

## SSH Setup

### Generate SSH Key
```bash
# Generate new SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Display public key
cat ~/.ssh/id_ed25519.pub

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
cat ~/.ssh/id_ed25519.pub
```

### Initial Git Configuration
```bash
# Set global user name
git config --global user.name "Your Name"

# Set global email
git config --global user.email "your_email@example.com"

# List all configuration
git config --global --list

# Set default branch name
git config --global init.defaultBranch main
```

## Repository Setup

### Initialize New Repository
```bash
# Initialize repository
git init

# Add all files
git add .

# Make initial commit
git commit -m "Initial commit"

# Add remote origin
git remote add origin <repository_url>

# Push to remote
git push -u origin main
```

### Clone Existing Repository
```bash
# Clone via HTTPS
git clone https://github.com/username/repository.git

# Clone via SSH
git clone git@github.com:username/repository.git

# Clone specific branch
git clone -b branch-name https://github.com/username/repository.git
```

## Remote Management

### Remote Operations
```bash
# List remotes
git remote -v

# Add remote
git remote add origin <repository_url>

# Remove remote
git remote remove origin

# Update remote URL
git remote set-url origin <new_repository_url>

# Fetch from remote
git fetch origin

# Pull with rebase
git pull --rebase origin main
```

## Line Ending Issues

### Windows CRLF Configuration
```bash
# Configure line endings for Windows
git config --global core.autocrlf input

# Reference: https://betterstack.com/community/questions/git-replacing-lf-with-crlf/
```

## File Permissions

### Make Files Executable
```bash
# Make shell scripts executable
git update-index --chmod=+x scripts/*

# Check file permissions
git ls-files --stage
```
