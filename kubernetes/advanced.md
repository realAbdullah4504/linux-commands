# Kubernetes Advanced Topics

## Headless Services

### What are Headless Services?
Headless services are used for direct pod discovery without load balancing. They're useful for stateful applications and service discovery.

### Creating Headless Services
```yaml
apiVersion: v1
kind: Service
metadata:
  name: headless-service
spec:
  clusterIP: None  # This makes it headless
  selector:
    app: my-app
  ports:
  - port: 80
    targetPort: 8080
```

### Use Cases
- Stateful applications (databases, message queues)
- Peer-to-peer communication
- Service discovery without load balancing
- Custom load balancing algorithms

## Distributed Tracing

### Overview
Tools like Jaeger or Zipkin can be used for distributed tracing, allowing you to visualize the flow of requests through various services, making it easier to identify bottlenecks or failures.

### Jaeger Installation
```bash
# Install Jaeger operator
kubectl create namespace observability
kubectl apply -f https://github.com/jaegertracing/jaeger-operator/releases/download/v1.49.0/jaeger-operator.yaml

# Create Jaeger instance
kubectl apply -f - <<EOF
apiVersion: jaegertracing.io/v1
kind: Jaeger
metadata:
  name: simplest
EOF
```

### Application Integration
```yaml
# Add tracing to your application deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: traced-app
spec:
  template:
    spec:
      containers:
      - name: app
        image: my-app
        env:
        - name: JAEGER_AGENT_HOST
          value: simplest-agent.observability.svc.cluster.local
        - name: JAEGER_SAMPLER_TYPE
          value: const
        - name: JAEGER_SAMPLER_PARAM
          value: "1"
```

## Service Mesh

### Istio Installation
```bash
# Download Istio
curl -L https://istio.io/downloadIstio | sh -
cd istio-*

# Install Istio
istioctl install --set profile=default -y

# Enable automatic sidecar injection
kubectl label namespace default istio-injection=enabled
```

### Traffic Management
```yaml
# Virtual service for traffic routing
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: reviews
spec:
  http:
  - match:
    - headers:
        end-user:
          exact: jason
    fault:
      delay:
        percentage:
          value: 100
        fixedDelay: 5s
    route:
    - destination:
        host: reviews
        subset: v2
  - route:
    - destination:
        host: reviews
        subset: v1
```

## Advanced Networking

### Network Policies
```yaml
# Deny all traffic by default
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

### Custom Resource Definitions (CRDs)
```bash
# List CRDs
kubectl get crd

# Describe CRD
kubectl describe crd <crd-name>

# Get custom resources
kubectl get <custom-resource-name>
```

## Performance Optimization

### Resource Limits and Requests
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: optimized-pod
spec:
  containers:
  - name: app
    image: nginx
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

### Horizontal Pod Autoscaling
```bash
# Create HPA
kubectl autoscale deployment <deployment-name> --cpu-percent=50 --min=1 --max=10

# Get HPA status
kubectl get hpa

# Describe HPA
kubectl describe hpa <hpa-name>
```

## Security Best Practices

### Pod Security Policies
```yaml
# Restrictive pod security policy
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restricted
spec:
  privileged: false
  allowPrivilegeEscalation: false
  requiredDropCapabilities:
    - ALL
  volumes:
    - 'configMap'
    - 'emptyDir'
    - 'projected'
    - 'secret'
    - 'downwardAPI'
    - 'persistentVolumeClaim'
  runAsUser:
    rule: 'MustRunAsNonRoot'
  seLinux:
    rule: 'RunAsAny'
  fsGroup:
    rule: 'RunAsAny'
```

### RBAC Configuration
```bash
# Create role
kubectl create role pod-reader --verb=get,list,watch --resource=pods

# Create role binding
kubectl create rolebinding pod-reader-binding --role=pod-reader --user=<username>

# Create cluster role
kubectl create cluster role cluster-admin --verb=* --resource=*
```

## MongoDB Connection Examples

### Direct Connection
```bash
# Direct connection string example
mongodb://username:password@hostname:27017/database?directConnection=true
```

### Kubernetes Service Discovery
```bash
# Service discovery format
busybox-deployment-1.busybox-service.default.svc.cluster.local

# MongoDB StatefulSet connection
mongodb-0.mongodb-service.mongodb-namespace.svc.cluster.local
mongodb-1.mongodb-service.mongodb-namespace.svc.cluster.local
```

## Useful Links

- Kubernetes Networking: https://chatgpt.com/share/673ed029-4c74-8001-b274-9f95d82f72cc
- General Kubernetes Guide: https://chatgpt.com/share/67263470-2e98-8001-a9e1-8564c9a215cd
- Headless Services: https://stackoverflow.com/questions/52707840/what-is-a-headless-service-what-does-it-do-accomplish-and-what-are-some-legiti
- Minikube IP Conflicts: https://github.com/kubernetes/minikube/issues/12315
- Helm Installation: https://helm.sh/docs/intro/install/
