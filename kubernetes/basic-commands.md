# Basic Kubernetes Commands

## Deployments

### Creating and Managing Deployments
```bash
# Create deployment
kubectl create deployment nginx-deployment --image=nginx

# Get deployments
kubectl get deployment

# Get replica sets
kubectl get replicaset

# Edit deployment
kubectl edit deployment <deployment-name>

# Apply configuration from file
kubectl apply -f config-file.yml

# Delete deployment
kubectl delete deployment <deployment-name>

# Delete all deployments in namespace
kubectl delete deployments --all -n my-namespace

# Delete resources by label
kubectl delete pods,services,deployments -l app=myapp

# Restart deployment
kubectl rollout restart deployment news-app-backend

# Restart deployment in specific namespace
kubectl rollout restart deployment -n kube-system
```

## Services and Networking

### Service Management
```bash
# Get services
kubectl get services

# Get services in specific namespace
minikube service nginx-service -n kubernetes-dashboard

# Start service locally
minikube service mongo-express-service

# Port forward service
kubectl port-forward service/hello-minikube 7080:8080

# Get ingress resources
kubectl get ingress --all-namespaces
```

## General Resource Management

### Viewing Resources
```bash
# Get all resources in current namespace
kubectl get all

# Get pods
kubectl get pods

# Get pods with wide output (shows IPs and nodes)
kubectl get pods -o wide

# Get nodes
kubectl get nodes

# Get endpoints
kubectl get endpoints
```

### Resource Status
```bash
# Get detailed information about resources
kubectl get deployment <deployment-name> -o yaml

# Watch resources for changes
kubectl get pods --watch

# Get resource events
kubectl get events
```
