# Troubleshooting

## Kubernetes Cluster Reset

### Drain Node

Before resetting a node, drain it to evict all pods:

```bash
kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data
```

### Remove Node from Cluster

```bash
kubectl delete node <node-name>
```

### Reset Kubernetes Components

```bash
sudo systemctl stop kubelet
sudo kubeadm reset
```

## Container Debugging

### List Containers

List containers in the k8s.io namespace:

```bash
sudo ctr -n k8s.io containers list
```

## Storage Issues

### PersistentVolume Stuck in Terminating

If a PersistentVolume is stuck in terminating state:

```bash
kubectl patch pv <pv-name> -p '{"metadata":{"finalizers":null}}'
```

Example:

```bash
kubectl patch pv ebs-pv -p '{"metadata":{"finalizers":null}}'
```

## Network Issues

### DNS Resolution Problems

If experiencing DNS resolution issues, try:

1. Check DNS configuration:

```bash
kubectl exec -i -t dnsutils -n default -- nslookup kubernetes.default
```

2. Fix resolv.conf if needed:

```bash
sudo rm /etc/resolv.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

3. Flush local DNS cache:

```bash
ipconfig /flushdns
```

## Ingress Issues

### Validation Errors

If encountering validation webhook errors:

```bash
kubectl delete validatingwebhookconfiguration ingress-nginx-admission
```

### Force Delete Ingress Service

```bash
kubectl patch svc ingress-nginx-controller -n ingress-nginx -p '{"metadata":{"finalizers":null}}' --type=merge
```

## General Debugging Commands

### Check Node Status

```bash
kubectl describe node <node-name>
```

### Check All Resources in Namespace

```bash
kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -n <namespace>
```

### Delete All Pods

```bash
kubectl delete pod --force --grace-period=0 --all
```

## System Issues

### Check Block Devices

```bash
lsblk
```

### Check System Logs

```bash
sudo dmesg | grep apparmor
```

## Cleanup Commands

### Remove Ingress Controller

```bash
helm uninstall -n ingress-nginx ingress-nginx
```

### Remove AWS Load Balancer Controller

```bash
helm uninstall -n kube-system aws-load-balancer-controller
```
