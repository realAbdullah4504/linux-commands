# Installation

## Docker Installation

### For Ubuntu/Debian

```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker ubuntu
newgrp docker
```

### For CentOS/RHEL

```bash
sudo yum install -y docker
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker ubuntu
newgrp docker
```

## Kubernetes Installation

Reference: <https://v1-30.docs.kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/>

### Prerequisites

```bash
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```

### Add Kubernetes Repository

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

### Install Kubernetes Components

```bash
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Enable Kubelet

```bash
sudo systemctl enable --now kubelet
```

### Install Additional Tools

```bash
sudo apt install kubectx
```

## Containerd Management

List containers in the k8s.io namespace:

```bash
sudo ctr -n k8s.io containers list
```
