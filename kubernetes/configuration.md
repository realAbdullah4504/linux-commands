# Kubernetes Configuration Management

## ConfigMaps and Secrets

### Secrets Management
```bash
# Create secret from base64 encoded value
echo -n "admin" | base64

# Apply secret configuration
kubectl apply -f mongo-secret.yaml

# Get secrets
kubectl get secret

# Create secret generic
kubectl create secret generic basic-auth-secret --from-file=auth=./authfile

# Get secret details
kubectl get secret <secret-name> -o yaml

# Decode secret value
echo <encoded-value> | base64 --decode
```

### ConfigMaps
```bash
# Create configmap from literal
kubectl create configmap app-config --from-literal=KEY=VALUE

# Create configmap from file
kubectl create configmap app-config --from-file=config.properties

# Create configmap from directory
kubectl create configmap app-config --from-file=./config-dir/

# Get configmaps
kubectl get configmap

# Get configmap details
kubectl describe configmap <configmap-name>
```

## Configuration Files

### File Structure
Configuration files have 3 parts:
1. **Metadata**: Name, namespace, labels
2. **Specification**: Desired state
3. **Status**: Current state (automatic)

### Applying Configurations
```bash
# Apply configuration
kubectl apply -f <deployment-or-service>.yaml

# Apply multiple files
kubectl apply -f deployment.yaml -f service.yaml

# Apply all files in directory
kubectl apply -f ./configs/

# Delete using configuration file
kubectl delete -f <deployment-or-service>.yaml

# Get deployment as YAML
kubectl get deployment <deployment-name> -o yaml > deployment-result.yaml

# Validate configuration without applying
kubectl apply --dry-run=client -f config.yaml
```

### Configuration Best Practices
- Use descriptive names and labels
- Separate configurations by environment
- Use namespaces for isolation
- Store sensitive data in Secrets, not ConfigMaps
- Use version control for configuration files
