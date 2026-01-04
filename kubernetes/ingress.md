# Kubernetes Ingress

## Ingress Setup

### Minikube Ingress
```bash
# Enable ingress addon in Minikube
minikube addons enable ingress
```

### NGINX Ingress Controller
```bash
# Install NGINX ingress controller
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml

# Get ingress controller pods
kubectl get pods -n ingress-nginx

# Get pods in kube-system namespace
kubectl get pods --namespace=kube-system

# Get ingress controller service
kubectl get service -n ingress-nginx
```

### Ingress Management
```bash
# Get ingress resources
kubectl get ingress --all-namespaces

# Get ingress in specific namespace
kubectl get ingress -n <namespace>

# Describe ingress
kubectl describe ingress <ingress-name>

# Apply ingress configuration
kubectl apply -f dashboard-ingress.yaml

# Delete ingress
kubectl delete ingress <ingress-name>
```

## Ingress Configuration

### Basic Ingress Example
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: example-service
            port:
              number: 80
```

## Authentication

### Basic Authentication
```bash
# Create htpasswd file
htpasswd -c auth admin

# Create secret for authentication
kubectl create secret generic basic-auth-secret --from-file=auth=./authfile

# Apply ingress with basic auth
kubectl apply -f ingress-with-auth.yaml
```

### TLS/SSL Configuration
```bash
# Create TLS secret
kubectl create secret tls tls-secret --key=tls.key --cert=tls.crt

# Apply ingress with TLS
kubectl apply -f ingress-with-tls.yaml
```

## Troubleshooting

### Ingress Issues
```bash
# View ingress controller logs
kubectl logs <nginx-ingress-controller-pod-name> -n ingress-nginx

# Check ingress controller events
kubectl get events -n ingress-nginx

# Test ingress connectivity
curl -H "Host: example.com" http://<ingress-ip>

# Check ingress status
kubectl describe ingress <ingress-name>
```

### Common Problems
- Ensure ingress controller is running
- Check DNS resolution for hostnames
- Verify service endpoints exist
- Check firewall rules and security groups
- Validate TLS certificates
