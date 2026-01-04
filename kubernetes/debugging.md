# Kubernetes Debugging and Monitoring

## Debugging Commands

### Pod and Container Debugging
```bash
# Get pod logs
kubectl logs <podname>

# Get logs with follow (tail -f equivalent)
kubectl logs <podname> -f

# Get logs from previous container instance
kubectl logs <podname> --previous

# Describe pod
kubectl describe pod <podname>

# Describe service
kubectl describe service <service-name>

# Describe deployment
kubectl describe deployment <deployment-name>

# Execute command in pod
kubectl exec [POD] -- [COMMAND]

# Get interactive shell in pod
kubectl exec -it <podname> -- /bin/bash

# Copy files from pod
kubectl cp <podname>:/path/to/file ./local-file

# Copy files to pod
kubectl cp ./local-file <podname>:/path/to/file
```

### Node and Cluster Debugging
```bash
# Describe nodes
kubectl describe nodes

# Get node resource usage
kubectl top nodes

# Get pod resource usage
kubectl top pods

# Get pod resource usage in namespace
kubectl top pods -n kube-system | grep ebs-csi-controller

# View kubelet logs
sudo journalctl -u kubelet -f

# Get cluster events
kubectl get events --sort-by=.metadata.creationTimestamp

# Get events in specific namespace
kubectl get events -n <namespace>
```

## Testing and Troubleshooting

### Test Pod Commands
```bash
# Run test pod
kubectl run test-pod --rm -i --tty --image=busybox -- /bin/sh

# Run temporary pod for debugging
kubectl run debug-pod --image=busybox --rm -it --restart=Never -- sh

# Port forward to local port for testing
kubectl port-forward service/<service-name> 8080:80

# Test network connectivity
kubectl run test-pod --image=busybox --rm -it -- wget -qO- http://service-name
```

## Metrics and Monitoring

### Metrics Server
```bash
# Install metrics server
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.1/components.yaml

# Check metrics server status
kubectl get pods -n kube-system | grep metrics-server

# Get resource usage metrics
kubectl top nodes
kubectl top pods
```

## Common Debugging Scenarios

### Pod Not Starting
```bash
# Check pod status and events
kubectl describe pod <podname>

# Check resource constraints
kubectl describe pod <podname> | grep -A 10 "Limits\|Requests"

# Check image pull issues
kubectl describe pod <podname> | grep -A 5 "Events"
```

### Service Not Accessible
```bash
# Check service endpoints
kubectl get endpoints <service-name>

# Check service configuration
kubectl describe service <service-name>

# Test service connectivity
kubectl run test-pod --image=busybox --rm -it -- nslookup <service-name>
```

### Network Issues
```bash
# Check network policies
kubectl get networkpolicies

# Test DNS resolution
kubectl run test-pod --image=busybox --rm -it -- nslookup kubernetes.default

# Check ingress status
kubectl get ingress
kubectl describe ingress <ingress-name>
```
