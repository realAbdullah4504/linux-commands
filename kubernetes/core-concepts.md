# Kubernetes Core Concepts

## Architecture Components

### Node
Simple server that runs containers

### Pod
Container wrapper - smallest deployable unit

### Service
Permanent IP address for each pod (lifecycle of service and pod are not connected)

### Ingress
Load balancer that routes to services

### Volumes
Persistent storage

### Deployment
Manages replicas of pods

### Stateful Sets
For stateful applications like databases (can't deploy databases with regular pods due to state)

## Master Node (Control Plane)

- **API Server**: Central management point
- **Scheduler**: Determines where to place pods
- **Controller Manager**: Requests scheduler to restart pods when needed
- **Etcd**: Key-value store for cluster changes

## Deployment Flow
```text
Deployment → ReplicaSet → Pod → Container (Automatic)
```

## Key Relationships

- **Pods** are scheduled on **Nodes**
- **Services** provide stable networking to **Pods**
- **Deployments** manage **ReplicaSets** which manage **Pods**
- **Ingress** routes external traffic to **Services**
- **Volumes** provide persistent storage to **Pods**
