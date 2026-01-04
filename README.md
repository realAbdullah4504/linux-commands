# Linux Commands Reference

A comprehensive collection of Linux commands and Kubernetes setup guides organized for quick reference and efficient workflow.

## 📚 Quick Navigation

### 🐧 Linux Commands

**Directory:** [`linux/`](./linux/)

#### 🚀 Essentials

- **[Basic Commands](./linux/basic-commands.md)** - CD, LS, aliases, terminal shortcuts
- **[File Operations](./linux/file-operations.md)** - Find, copy, move, permissions, compression
- **[Text Editing](./linux/text-editing.md)** - Nano, sed, file writing methods

#### 👤 System Administration

- **[User Management](./linux/user-management.md)** - Users, groups, sudo, SSH keys
- **[System Monitoring](./linux/system-monitoring.md)** - Memory, disk, processes, ports
- **[Logs & Debugging](./linux/logs-debugging.md)** - Log viewing, troubleshooting, journalctl

#### 🌐 Advanced Topics

- **[Networking & Transfer](./linux/networking-transfer.md)** - SSH, SCP, port forwarding
- **[Volume Management](./linux/volume-mounting.md)** - Disk mounting, fstab, bind mounts

### 🐙 Git & GitHub

**Directory:** [`github/`](./github/)

#### 📋 Git Essentials

- **[Setup](./github/setup.md)** - SSH setup and initial configuration
- **[Basic Commands](./github/basic-commands.md)** - Essential Git commands for daily use
- **[Branching](./github/branching.md)** - Branch management and strategies

#### 🔧 Advanced Git

- **[Advanced Operations](./github/advanced.md)** - Advanced Git operations and workflows
- **[Troubleshooting](./github/troubleshooting.md)** - Common issues and solutions

### 🐳 Docker

**Directory:** [`docker/`](./docker/)

#### 🚀 Docker Basics

- **[Installation](./docker/install.md)** - Docker installation and setup
- **[Basic Commands](./docker/basic-commands.md)** - Container management essentials
- **[Docker Compose](./docker/docker-compose.md)** - Multi-container applications

#### 🔧 Docker Advanced

- **[Networking](./docker/networking.md)** - Docker networking configuration
- **[Volumes](./docker/volumes.md)** - Data persistence and volumes
- **[Advanced Operations](./docker/advanced.md)** - Advanced Docker techniques

### ☸️ Kubernetes

**Directory:** [`kubernetes/`](./kubernetes/)

#### 🚀 Kubernetes Basics

- **[Basic Commands](./kubernetes/basic-commands.md)** - Essential kubectl commands
- **[Core Concepts](./kubernetes/core-concepts.md)** - Pods, services, deployments explained
- **[Configuration](./kubernetes/configuration.md)** - ConfigMaps, secrets, and settings

#### 🔧 Kubernetes Advanced

- **[Advanced Operations](./kubernetes/advanced.md)** - Advanced kubectl and cluster management
- **[Helm](./kubernetes/helm.md)** - Helm package manager
- **[Namespaces](./kubernetes/namespaces.md)** - Namespace management
- **[Volumes](./kubernetes/volumes.md)** - Storage and persistent volumes
- **[Ingress](./kubernetes/ingress.md)** - Ingress controllers and routing
- **[Debugging](./kubernetes/debugging.md)** - Troubleshooting and monitoring
- **[Minikube](./kubernetes/minikube.md)** - Local Kubernetes development

### ☸️ Kubernetes on EC2

**Directory:** [`kubernetes-ec2/`](./kubernetes-ec2/)

#### ⚙️ Setup & Installation

- **[Setup Prerequisites](./kubernetes-ec2/setup-prerequisites.md)** - SSH connections, basic setup
- **[Installation](./kubernetes-ec2/installation.md)** - Docker, Kubernetes components
- **[Cluster Initialization](./kubernetes-ec2/cluster-initialization.md)** - Control plane, worker nodes

#### 📦 Infrastructure

- **[Storage & Volumes](./kubernetes-ec2/storage-volumes.md)** - PV, PVC, EBS, storage management
- **[Networking](./kubernetes-ec2/networking.md)** - DNS, AWS CNI, network config
- **[Ingress & Load Balancer](./kubernetes-ec2/ingress-loadbalancer.md)** - NGINX Ingress, AWS LB

#### 🔧 Operations

- **[Troubleshooting](./kubernetes-ec2/troubleshooting.md)** - Reset, debugging, cleanup

## 🎯 Quick Reference Commands

### Linux Essentials

```bash
# Navigation
cd /path/to/directory    # Change directory
cd ..                   # Go back
cd -                    # Previous directory
ls -la                  # List all files

# File Operations
find . -name "*.sh" -exec chmod +x {} \;  # Make scripts executable
grep -r "pattern" /path  # Recursive search
tar -czf backup.tar.gz folder/  # Create archive

# System Info
df -h                   # Disk usage
free -h                  # Memory usage
ps aux | grep process    # Find processes
```

### Git Essentials

```bash
# Repository Setup
git init                 # Initialize repository
git clone <url>          # Clone repository
git remote add origin <url> # Add remote

# Daily Workflow
git add .                # Stage all changes
git commit -m "message"  # Commit changes
git push origin main      # Push to remote
git pull origin main      # Pull from remote

# Branch Management
git branch               # List branches
git checkout -b new     # Create and switch branch
git merge feature        # Merge branch
```

### Docker Essentials

```bash
# Container Management
docker run -d nginx                   # Run container
docker ps                              # List containers
docker stop <container>                # Stop container
docker rm <container>                  # Remove container

# Image Management
docker pull ubuntu                      # Pull image
docker images                          # List images
docker build -t app .                  # Build image

# Docker Compose
docker-compose up -d                   # Start services
docker-compose down                     # Stop services
docker-compose logs -f                  # Follow logs
```

### Kubernetes Essentials

```bash
# Cluster Management
kubectl get nodes        # Check nodes
kubectl get pods -A      # All pods
kubectl describe pod name # Pod details

# Application Management
kubectl apply -f file.yaml    # Deploy
kubectl delete -f file.yaml   # Remove
kubectl logs pod-name         # View logs
kubectl port-forward svc/name 8080:80  # Forward port
```

## 🔍 Search Commands

### Find Commands Fast

```bash
# By category
grep -r "ssh" ./linux/                    # Find SSH-related commands
grep -r "mount" ./linux/volume-mounting.md  # Mount commands
grep -r "ingress" ./kubernetes-ec2/       # Ingress setup
grep -r "commit" ./github/               # Git commit commands
grep -r "docker run" ./docker/           # Docker run commands
grep -r "kubectl" ./kubernetes/         # Kubernetes commands
```

### By Use Case

```bash
# File operations
find . -name "*.md" -exec grep "chmod" {} \;

# Git workflows
grep -r "branch\|merge\|rebase" ./github/

# Docker troubleshooting
grep -r "error\|debug\|logs" ./docker/

# Kubernetes troubleshooting
grep -r "error\|debug\|reset" ./kubernetes-ec2/troubleshooting.md

# Kubernetes operations
grep -r "deployment\|service\|pod" ./kubernetes/
```

## 📖 Usage Tips

### For Beginners

1. Start with [`linux/basic-commands.md`](./linux/basic-commands.md) for fundamentals
2. Learn file operations with [`linux/file-operations.md`](./linux/file-operations.md)
3. Practice user management with [`linux/user-management.md`](./linux/user-management.md)
4. Get started with Git using [`github/setup.md`](./github/setup.md) and [`github/basic-commands.md`](./github/basic-commands.md)
5. Learn Docker basics with [`docker/install.md`](./docker/install.md) and [`docker/basic-commands.md`](./docker/basic-commands.md)

### For System Administrators

1. Master system monitoring with [`linux/system-monitoring.md`](./linux/system-monitoring.md)
2. Learn networking with [`linux/networking-transfer.md`](./linux/networking-transfer.md)
3. Study volume management with [`linux/volume-mounting.md`](./linux/volume-mounting.md)
4. Advance Git skills with [`github/advanced.md`](./github/advanced.md) and [`github/branching.md`](./github/branching.md)
5. Master Docker with [`docker/networking.md`](./docker/networking.md) and [`docker/volumes.md`](./docker/volumes.md)

### For DevOps Engineers

1. Set up Kubernetes with [`kubernetes-ec2/setup-prerequisites.md`](./kubernetes-ec2/setup-prerequisites.md)
2. Configure storage with [`kubernetes-ec2/storage-volumes.md`](./kubernetes-ec2/storage-volumes.md)
3. Set up ingress with [`kubernetes-ec2/ingress-loadbalancer.md`](./kubernetes-ec2/ingress-loadbalancer.md)
4. Combine Git and Docker workflows using [`github/advanced.md`](./github/advanced.md) and [`docker/docker-compose.md`](./docker/docker-compose.md)

## 🛠️ Common Workflows

### Server Setup Workflow

```bash
# 1. Connect and setup user
ssh -i key.pem user@server
sudo useradd -m -s /bin/bash newuser
sudo usermod -aG sudo newuser

# 2. Install essentials
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io kubeadm kubelet kubectl

# 3. Configure system
sudo systemctl enable docker
sudo systemctl enable kubelet
```

### Kubernetes Deployment Workflow

```bash
# 1. Initialize cluster
sudo kubeadm init --pod-network-cidr=192.168.0.0/16

# 2. Configure kubectl
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# 3. Deploy applications
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
```

## 📚 Additional Resources

### Documentation

- [Linux Command Line Basics](https://www.linuxcommand.org/)
- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [AWS EKS Documentation](https://docs.aws.amazon.com/eks/)

### Tools Reference

- [Docker CLI Reference](https://docs.docker.com/engine/reference/commandline/cli/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## 🤝 Contributing

This is a living reference guide. Feel free to:

- Add new commands and examples
- Update existing documentation
- Fix any errors or typos
- Suggest improvements

---

**💡 Pro Tip:** Use `Ctrl + F` in your browser/editor to quickly search for specific commands or topics within this repository.

**🔖 Bookmark this page** for quick access to essential Linux and Kubernetes commands!
