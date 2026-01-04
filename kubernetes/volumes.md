# Kubernetes Volumes and Storage

## Volume Debugging

### DNS and Network Debugging
```bash
# DNS lookup for service
nslookup mongodb-1.mongodb-service.my-namespace.svc.cluster.local

# Install DNS utilities
apt-get update
apt-get install -y dnsutils
apt-get install -y iputils-ping

# Test connectivity from pod
kubectl exec -it <pod-name> -- nslookup kubernetes.default
```

### Volume Troubleshooting
```bash
# Check volume mounts in pod
kubectl describe pod <pod-name> | grep -A 10 "Mounts\|Volumes"

# Check persistent volumes
kubectl get pv

# Check persistent volume claims
kubectl get pvc

# Describe persistent volume
kubectl describe pv <pv-name>

# Describe persistent volume claim
kubectl describe pvc <pvc-name>

# Check storage classes
kubectl get storageclass

# Describe storage class
kubectl describe storageclass <storage-class-name>
```

## NFS Setup

### Server Configuration
```bash
# Install NFS server
sudo apt install nfs-kernel-server

# Add export to /etc/exports
echo "/mnt/win_share *(rw,sync,no_subtree_check,no_root_squash)" | sudo tee -a /etc/exports

# Create and set permissions for share directory
sudo mkdir /mnt/win_share
sudo chmod 777 /mnt/win_share

# Start NFS service
sudo systemctl start nfs-kernel-server
sudo systemctl enable nfs-kernel-server

# Show NFS exports
sudo exportfs -v
```

### Kubernetes NFS Configuration
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteMany
  nfs:
    server: nfs-server-ip
    path: /mnt/win_share
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
```

## Volume Types

### Common Volume Types
- **emptyDir**: Empty directory for pod lifetime
- **hostPath**: Directory from host node
- **nfs**: Network File System
- **configMap**: Configuration data
- **secret**: Sensitive data
- **persistentVolumeClaim**: Persistent storage

### Volume Mount Examples
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-pod
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - name: data-volume
      mountPath: /data
    - name: config-volume
      mountPath: /config
  volumes:
  - name: data-volume
    persistentVolumeClaim:
      claimName: nfs-pvc
  - name: config-volume
    configMap:
      name: app-config
```

## Storage Management

### Storage Classes
```bash
# Get storage classes
kubectl get storageclass

# Create storage class
kubectl apply -f storage-class.yaml

# Set default storage class
kubectl patch storageclass <storage-class-name> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

### Volume Snapshots
```bash
# Create volume snapshot
kubectl apply -f snapshot.yaml

# Get volume snapshots
kubectl get volumesnapshot

# Restore from snapshot
kubectl apply -f restore.yaml
```
