# Storage and Volumes

## Volume Types

### Local Volumes

Local PersistentVolumes are node-specific resources tied to a specific node where the storage exists.

```bash
kubectl port-forward svc/mongodb-service 27017:27017
```

**Important Note**: When mounted to local volumes, multiple pods on the same server can access the storage, but there's no file locking mechanism.

### Dynamic Volumes

When using dynamic volume provisioning, the storage class must be specified in the PVC configuration.

### Existing EBS Volumes

For existing EBS volumes, no storage class needs to be mentioned in the configuration.

## PVC Claims vs PVC Claim Templates

- **PVC Template**: Creates separate PVCs for individual StatefulSet pods, resulting in separate volumes for each pod.
- **PVC YAML**: Connects one volume to multiple non-StatefulSet pods.

## AWS EBS CSI Driver

### Installation

```bash
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.37"
```

Reference: <https://github.com/kubernetes-sigs/aws-ebs-csi-driver/blob/master/docs/install.md>

### Monitor CSI Driver

```bash
kubectl get pods -n kube-system -l app.kubernetes.io/name=aws-ebs-csi-driver --watch
```

### Check Deployment Configuration

```bash
kubectl describe deployment <name> -n kube-system
```

Example environment variable configuration:

```yaml
env:
  - name: AWS_REGION
    value: "us-west-2"
```

## Storage Troubleshooting

### Stuck PersistentVolume

If a PV is stuck in terminating state:

```bash
kubectl patch pv ebs-pv -p '{"metadata":{"finalizers":null}}'
```

### Check Block Devices

```bash
lsblk
```

## Snapshots and Backup

Snapshot and backup configurations are pending implementation.
