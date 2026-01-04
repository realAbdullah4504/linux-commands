# Kubernetes Namespaces

## Namespace Management

### Creating and Managing Namespaces
```bash
# Create namespace
kubectl create namespace <namespace-name>

# Get all namespaces
kubectl get namespaces

# Get namespaces with abbreviated output
kubectl get ns

# Describe namespace
kubectl describe namespace <namespace-name>

# Delete namespace (deletes all resources in it)
kubectl delete namespace <namespace-name>
```

### Working with Namespaces
```bash
# Set current namespace for context
kubectl config set-context --current --namespace=<namespace-name>

# Get current namespace
kubectl config view --minify | grep namespace

# Get resources in specific namespace
kubectl get pods -n <namespace-name>
kubectl get services -n <namespace-name>

# Get all resources in namespace
kubectl get all -n <namespace-name>

# Apply configuration to specific namespace
kubectl apply -f config.yaml -n <namespace-name>
```

### Context Switching Tools

#### Using kubectx (Recommended)
```bash
# Install kubectx for Windows using scoop
scoop install kubectx

# Switch namespace
kubens <namespace-name>

# List available namespaces
kubens

# Switch back to previous namespace
kubens -
```

#### Manual Context Management
```bash
# Create context with namespace
kubectl config set-context <context-name> --cluster=<cluster-name> --user=<user-name> --namespace=<namespace-name>

# Switch to context
kubectl config use-context <context-name>

# List contexts
kubectl config get-contexts

# Get current context
kubectl config current-context
```

## Namespace Best Practices

### Organization
- Use separate namespaces for different environments (dev, staging, prod)
- Use namespaces for team isolation
- Create namespaces for different applications or microservices

### Resource Quotas
```bash
# Create resource quota for namespace
kubectl create quota <quota-name> --hard=cpu=1,memory=1G,pods=10 -n <namespace-name>

# Get resource quotas
kubectl get resourcequota -n <namespace-name>

# Describe resource quota
kubectl describe resourcequota <quota-name> -n <namespace-name>
```

### Network Policies
```bash
# Create network policy for namespace isolation
kubectl apply -f network-policy.yaml -n <namespace-name>

# Get network policies
kubectl get networkpolicy -n <namespace-name>
```
