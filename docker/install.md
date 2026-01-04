# Docker Installation on Ubuntu

## Prerequisites
- Ubuntu 20.04 LTS or later
- User with sudo privileges
- Internet connection

## Installation Steps

### 1. Update System Packages
```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Install Required Packages
```bash
sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release
```

### 3. Add Docker's Official GPG Key
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### 4. Add Docker Repository
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 5. Update Package Index
```bash
sudo apt update
```

### 6. Install Docker Engine
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 7. Start and Enable Docker Service
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 8. Add User to Docker Group (Optional)
```bash
sudo usermod -aG docker $USER
```
**Note:** You'll need to log out and log back in for this to take effect.

### 9. Verify Installation
```bash
docker --version
docker run hello-world
```

## Post-Installation Configuration

### Configure Docker to Start on Boot
```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

### Configure Docker Daemon (Optional)
Create or edit `/etc/docker/daemon.json`:
```bash
sudo nano /etc/docker/daemon.json
```

Example configuration:
```json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
```

Restart Docker after configuration:
```bash
sudo systemctl restart docker
```

## Troubleshooting

### Docker Command Requires Sudo
If you didn't add your user to the docker group, you'll need to use sudo:
```bash
sudo docker ps
```

### Docker Service Not Running
```bash
sudo systemctl status docker
sudo systemctl start docker
```

### Permission Denied Issues
```bash
sudo chown $USER:$USER /var/run/docker.sock
```

### Remove Docker (If Needed)
```bash
sudo apt purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo apt autoremove
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

## Next Steps
- [Docker Basic Commands](./basic-commands.md)
- [Docker Compose Guide](./docker-compose.md)
- [Docker Best Practices](./best-practices.md)