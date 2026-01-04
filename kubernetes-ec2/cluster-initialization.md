# Cluster Initialization

## Control Plane Setup

### Initialize the Cluster

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --ignore-preflight-errors=all
```

### Configure kubectl Access

For the current user:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

For root user:

```bash
sudo mkdir -p /root/.kube 
sudo cp /etc/kubernetes/admin.conf /root/.kube/config 
sudo chown root:root /root/.kube/config
```

### Generate Join Command

```bash
sudo kubeadm token create --print-join-command
```

## Worker Node Setup

### Join Worker Node to Cluster

Use the join command generated from the control plane:

```bash
sudo kubeadm join <control-plane-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### Configure kubectl on Worker Node

```bash
sudo mkdir -p /root/.kube 
sudo cp /etc/kubernetes/kubelet.conf /root/.kube/config
```

## Cluster Management Commands

### Node Information

```bash
kubectl describe node <control-plane-node-name>
```

### Delete All Pods

```bash
kubectl delete pod --force --grace-period=0 --all
```

### Context Management

```bash
kubectl config current-context
kubectl config get-contexts
```

## DaemonSet Information

DaemonSet ensures that a pod runs on all cluster nodes that meet certain criteria. When a new node is added to the cluster, the pod is automatically added to it. When a node is removed, the pod is removed.

## Auto Scaling

Configure cluster auto-scaling based on workload requirements.
