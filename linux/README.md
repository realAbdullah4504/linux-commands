# Linux Commands Reference

This directory contains comprehensive Linux commands and utilities organized by category for easy reference and learning.

## Overview

A collection of essential Linux commands and terminal hacks to help you work faster and more efficiently.

## Documentation Structure

### 📁 File Operations

- **[file-operations.md](./file-operations.md)** - File manipulation, find commands, removal, and permissions

### 👤 User Management

- **[user-management.md](./user-management.md)** - User creation, groups, sudo configuration, and SSH keys

### 📊 System Monitoring

- **[system-monitoring.md](./system-monitoring.md)** - Memory, disk usage, processes, and port monitoring

### ✏️ Text Editing

- **[text-editing.md](./text-editing.md)** - Nano editor, sed commands, and file writing methods

### 🌐 Networking & Transfer

- **[networking-transfer.md](./networking-transfer.md)** - SSH, SCP, port forwarding, and network utilities

### 💾 Volume Management

- **[volume-mounting.md](./volume-mounting.md)** - Disk mounting, fstab configuration, and bind mounts

### 🚀 Basic Commands

- **[basic-commands.md](./basic-commands.md)** - CD, LS, aliases, and terminal shortcuts

### 📝 Logs & Debugging

- **[logs-debugging.md](./logs-debugging.md)** - Log viewing, debugging techniques, and journalctl

## Quick Start

1. **Beginners**: Start with [basic-commands.md](./basic-commands.md) for fundamental navigation and file operations
2. **System Admin**: Use [system-monitoring.md](./system-monitoring.md) and [user-management.md](./user-management.md) for administration tasks
3. **Development**: Refer to [text-editing.md](./text-editing.md) and [networking-transfer.md](./networking-transfer.md) for development workflows
4. **Advanced**: Explore [volume-mounting.md](./volume-mounting.md) and [logs-debugging.md](./logs-debugging.md) for advanced system management

## Essential Commands Cheat Sheet

### Navigation
```bash
cd /path/to/directory    # Change directory
cd ..                   # Go back one level
cd -                    # Go to previous directory
ls -la                  # List all files with details
```

### File Operations
```bash
find . -name "*.sh" -exec chmod +x {} \;  # Make all .sh files executable
rm -rf /path/to/directory/*                # Remove directory contents
chmod 755 file.txt                         # Set file permissions
```

### System Info
```bash
df -h              # Disk usage
free -h            # Memory usage
ps aux | grep nginx # Find processes
sudo ss -tuln      # Check open ports
```

## Resources

- [Linux Command Line Basics](https://www.linuxcommand.org/)
- [Advanced Linux Commands](https://www.gnu.org/software/coreutils/manual/)
- [Shell Scripting Guide](https://www.shellscript.sh/)

## Tips

- Use `Ctrl + R` to search command history
- Use tab completion for faster navigation
- Create aliases for frequently used commands
- Use `!!` to repeat the last command with sudo
