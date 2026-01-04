# Minikube Commands

## Installation and Setup

### Windows Installation
```bash
# Install Minikube on Windows
winget install Kubernetes.minikube
```

### Cluster Management
```bash
# Start Minikube cluster
minikube start

# Stop Minikube cluster
minikube stop

# Delete Minikube cluster
minikube delete

# SSH into Minikube node
minikube ssh

# Open Minikube dashboard (useful for IP conflicts)
minikube dashboard
```

## Cluster Information

### Basic Commands
```bash
# Get cluster information
kubectl cluster-info

# Get current context
kubectl config current-context

# Get nodes
kubectl get nodes

# Get nodes with IP addresses
kubectl get nodes -o wide

# Get pods with IP addresses
kubectl get pods -o wide

# Get endpoints
kubectl get endpoints

# Get all resources
kubectl get all
```

## Common Issues

### IP Conflicts
If you encounter IP conflicts with Minikube:
```bash
# Check dashboard status
minikube dashboard

# Reference: https://github.com/kubernetes/minikube/issues/12315
```

## Addons

### Enable Common Addons
```bash
# Enable ingress addon
minikube addons enable ingress

# List all available addons
minikube addons list

# Enable dashboard
minikube addons enable dashboard
```
