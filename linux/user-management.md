# User Management

## User Operations

### List All Users

```bash
cat /etc/passwd
```

### Create New User

```bash
sudo useradd -m -s /bin/bash abdullah
sudo passwd abdullah
sudo usermod -aG wheel abdullah
```

### Change User Shell

```bash
sudo usermod --shell /bin/bash username
```

### Change Username

```bash
sudo usermod -l newname previousname
```

### Switch User

```bash
su - username
```

### Delete User

```bash
sudo userdel username
```

### Delete User from Group

```bash
sudo deluser username groupname
```

## Password Management

### Change User Password

```bash
sudo passwd username
```

## Group Management

### Create Group

```bash
sudo groupadd groupname
```

### List All Groups

```bash
cat /etc/group
```

### Show Groups for Current User

```bash
groups
```

### Show Groups for Specific User

```bash
groups username
```

### Add User to Group

```bash
sudo usermod -aG groupname username
```

### Remove User from Group

```bash
sudo gpasswd -d username groupname
```

### Delete Group

```bash
sudo groupdel groupname
```

### Apply Group Changes

```bash
newgrp groupname
```

## Sudo Configuration

### Edit Sudoers File

```bash
sudo visudo
```

### Sudoers File Syntax

```bash
<user_or_group> <host> = (<run_as>) <commands>
```

- `%` in sudoers file means group

### Grant Specific Command Access

```bash
abdullah ALL=(ALL) NOPASSWD: /bin/systemctl restart nginx
```

### Execute Remote Command with Sudo

```bash
ssh -i ./id_ubuntu abdullah@172.27.142.51 'sudo systemctl restart nginx'
```

### Check User Privileges

```bash
sudo -l
```

### Check Sudo Permissions

```bash
visudo -c
```

## SSH Key Management

### Create SSH Directory for User

```bash
sudo mkdir -p /home/username/.ssh
```

### Copy SSH Keys

```bash
sudo cp /home/ec2-user/.ssh/authorized_keys /home/username/.ssh/authorized_keys
```

### Set SSH Directory Permissions

```bash
sudo chown -R username:username /home/username/.ssh
sudo chmod 700 /home/username/.ssh
sudo chmod 600 /home/username/.ssh/authorized_keys
```

## User Session Management

### Repeat Last Command with Sudo

```bash
sudo !!
```

### Check Current User

```bash
whoami
sudo whoami
```

### Check User ID

```bash
id
id username
```

## User Environment

### Set User Shell Environment

```bash
chsh -s /bin/bash username
```

### View User Login Information

```bash
finger username
```

### Check Last Login

```bash
last username
lastlog
```

## User Resource Limits

### View User Limits

```bash
ulimit -a
```

### Set User Limits

```bash
ulimit -n 4096  # Increase file descriptor limit
```

## User Process Management

### Show User Processes

```bash
ps -u username
ps aux | grep username
```

### Kill User Processes

```bash
pkill -u username
killall -u username
```

## User Home Directory Management

### Create User Home Directory

```bash
sudo mkdir -p /home/username
sudo chown username:username /home/username
```

### Copy Skeleton Files

```bash
sudo cp -r /etc/skel/* /home/username/
sudo chown -R username:username /home/username/
```

## User Backup and Restore

### Backup User Home Directory

```bash
sudo tar -czf username_backup.tar.gz /home/username
```

### Restore User Home Directory

```bash
sudo tar -xzf username_backup.tar.gz -C /
```
