# Kubernetes on EC2

This directory contains comprehensive documentation for setting up and managing a Kubernetes cluster on AWS EC2 instances.

## Overview

This guide covers the complete setup of a self-provisioned Kubernetes cluster with:
- 1 control-plane node
- 2 worker nodes

## Documentation Structure

### 🚀 Setup and Installation

- **[setup-prerequisites.md](./setup-prerequisites.md)** - SSH connections, basic prerequisites, and cluster overview
- **[installation.md](./installation.md)** - Docker and Kubernetes components installation

### ⚙️ Cluster Management

- **[cluster-initialization.md](./cluster-initialization.md)** - Control plane setup, worker node joining, and cluster management

### 📦 Storage and Networking

- **[storage-volumes.md](./storage-volumes.md)** - PersistentVolumes, PVCs, EBS CSI driver, and storage management
- **[networking.md](./networking.md)** - DNS resolution, AWS CNI, and network configuration

### 🌐 Ingress and Load Balancing

- **[ingress-loadbalancer.md](./ingress-loadbalancer.md)** - NGINX Ingress Controller, AWS Load Balancer Controller, and traffic management

### 🔧 Troubleshooting

- **[troubleshooting.md](./troubleshooting.md)** - Common issues, debugging commands, and cleanup procedures

## Quick Start

1. **Prerequisites**: Start with [setup-prerequisites.md](./setup-prerequisites.md) to establish SSH connections and prepare your environment
2. **Installation**: Follow [installation.md](./installation.md) to install Docker and Kubernetes components
3. **Cluster Setup**: Use [cluster-initialization.md](./cluster-initialization.md) to initialize the cluster and join worker nodes
4. **Storage & Networking**: Configure storage and networking with [storage-volumes.md](./storage-volumes.md) and [networking.md](./networking.md)
5. **Ingress**: Set up external access with [ingress-loadbalancer.md](./ingress-loadbalancer.md)

## Useful Resources

- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [AWS EKS Documentation](https://docs.aws.amazon.com/eks/)
- [Kubeadm Installation Guide](https://v1-30.docs.kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

## Cluster Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Control Plane │    │   Worker Node 1 │    │   Worker Node 2 │
│                 │    │                 │    │                 │
│  - API Server   │    │  - Kubelet      │    │  - Kubelet      │
│  - Scheduler    │    │  - Kube-proxy   │    │  - Kube-proxy   │
│  - Controller   │    │  - Container    │    │  - Container    │
│  - etcd         │    │    Runtime      │    │    Runtime      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │   AWS VPC       │
                    │                 │
                    │  - Subnets      │
                    │  - Security     │
                    │    Groups       │
                    │  - IAM Roles    │
                    └─────────────────┘
```

## Support

For troubleshooting and common issues, refer to the [troubleshooting.md](./troubleshooting.md) file.
