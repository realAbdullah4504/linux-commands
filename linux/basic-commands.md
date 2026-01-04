# Basic Linux Commands

## Directory Navigation (CD Commands)

### Basic Navigation

```bash
cd /                    # Go to root directory
cd                      # Go to home directory
cd /path/to/directory    # Navigate using absolute path
cd ..                   # Go back one level
cd ../..                # Go back two levels
cd -                    # Go to previous directory (same as echo $OLDPWD)
```

### Tab Completion

```bash
cd ho => cd home        # Tab to autocomplete
cd ho[TAB][TAB]        # Double tab to show options
```

### Clear Screen

```bash
clear                   # Clear screen
Ctrl + l                # Clear screen shortcut
```

## File Listing (LS Commands)

### Basic Listing

```bash
ls                      # Simple list
ls -l                   # Long format
ls -a                   # Show hidden files
ls -la                  # Long format with hidden files
ls -lh                  # Human readable sizes
ls -lah                 # All options combined
```

### Common Aliases

```bash
ll                      # Usually aliased to 'ls -l'
la                      # Usually aliased to 'ls -la'
```

## Command History

### Search Command History

```bash
Ctrl + r                # Reverse search command history
history                  # Show command history
!!                      # Repeat last command
!n                      # Repeat command number n from history
```

### History Management

```bash
history | grep "command" # Search history for specific command
Ctrl + p                # Previous command
Ctrl + n                # Next command
```

## Terminal Shortcuts

### Cursor Movement

```bash
Ctrl + a                # Move cursor to start of line
Ctrl + e                # Move cursor to end of line
Ctrl + f                # Move cursor forward one character
Ctrl + b                # Move cursor backward one character
Alt + f                 # Move cursor forward one word
Alt + b                 # Move cursor backward one word
```

### Text Manipulation

```bash
Ctrl + u                # Delete everything before cursor
Ctrl + k                # Delete everything after cursor
Ctrl + w                # Delete word before cursor
Ctrl + y                # Paste (yank) deleted text
Alt + backspace          # Delete word backwards (fast)
Ctrl + d                # Delete character under cursor
```

### Process Control

```bash
Ctrl + c                # Kill current process
Ctrl + z                # Suspend current process
Ctrl + s                # Stop output to screen
Ctrl + q                # Resume output to screen
```

### Command Editing

```bash
Ctrl + x + e            # Open current command in editor
Ctrl + t                # Swap current character with previous
Alt + t                 # Swap current word with previous
```

## Custom Commands and Aliases

### Temporary Aliases

```bash
alias ll="ls -la"        # Create temporary alias
alias gs="git status"    # Git status alias
alias myip="curl ifconfig.me"  # Get public IP
```

### Permanent Aliases

```bash
nano ~/.bashrc          # Edit bashrc file
```

Add these lines:

```bash
alias ll='ls -lah'
alias gs='git status'
alias myip='curl ifconfig.me'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
```

### Reload Bash Configuration

```bash
source ~/.bashrc         # Reload bashrc
. ~/.bashrc            # Alternative reload method
```

### Custom Functions

```bash
# Create directory and cd into it
echo 'mkcd () { mkdir -p "$1" && cd "$1"; }' >> ~/.bashrc && source ~/.bashrc

# Extract any archive
extract () {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar x $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)           echo "'$1' cannot be extracted via extract()" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}
```

## File and Directory Operations

### Create Directories

```bash
mkdir dirname            # Create single directory
mkdir -p path/to/dir    # Create parent directories as needed
mkdir dir1 dir2 dir3    # Create multiple directories
```

### Remove Files and Directories

```bash
rm filename             # Remove file
rm -r dirname          # Remove directory and contents
rm -f filename         # Force remove file
rm -rf dirname         # Force remove directory and contents
```

### Copy and Move

```bash
cp source dest          # Copy file
cp -r source dest      # Copy directory
mv source dest          # Move/rename file or directory
```

## File Content Viewing

### View File Content

```bash
cat filename            # Display entire file
less filename          # View file with pagination
head filename          # Show first 10 lines
tail filename          # Show last 10 lines
tail -f filename      # Follow file in real-time
```

### Search in Files

```bash
grep pattern filename   # Search for pattern in file
grep -r pattern dir   # Recursive search in directory
```

## System Information

### Current Working Directory

```bash
pwd                    # Print working directory
echo $PWD              # Alternative method
```

### User Information

```bash
whoami                 # Current user
id                     # User and group IDs
groups                  # Groups current user belongs to
```

### System Information

```bash
uname -a               # System information
date                   # Current date and time
uptime                 # System uptime
```

## Process Management

### View Processes

```bash
ps                     # Current user processes
ps aux                  # All processes
top                     # Interactive process viewer
htop                    # Enhanced process viewer
```

### Kill Processes

```bash
kill PID                # Kill process by PID
killall processname     # Kill process by name
Ctrl + c                # Kill foreground process
```

## Help and Documentation

### Getting Help

```bash
man command             # Manual page for command
command --help          # Help for specific command
whatis command          # Brief description of command
whereis command         # Location of command
which command          # Which command will be executed
```

## Environment Variables

### View Environment

```bash
env                    # All environment variables
printenv               # Alternative method
echo $VAR_NAME         # Show specific variable
```

### Set Environment Variables

```bash
export VAR_NAME="value" # Set for current session
VAR_NAME="value"        # Set for current command only
```

## File Permissions Quick Reference

### Symbolic to Numeric

```bash
rwx = 7 (4+2+1)
rw- = 6 (4+2)
r-x = 5 (4+1)
r-- = 4
-wx = 3 (2+1)
-w- = 2
--x = 1
--- = 0
```

### Common Permissions

```bash
chmod 755 file         # rwxr-xr-x (owner: rwx, group: r-x, others: r-x)
chmod 644 file         # rw-r--r-- (owner: rw-, group: r--, others: r--)
chmod 600 file         # rw------- (owner only)
chmod 777 file         # rwxrwxrwx (everyone)
```
