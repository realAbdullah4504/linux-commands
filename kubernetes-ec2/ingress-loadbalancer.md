# Ingress and Load Balancer

## NGINX Ingress Controller

### Installation

Reference: <https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-3-nginx-ingress-controller/>

#### Method 1: Static Manifest

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

#### Method 2: Helm Installation

```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace
```

#### Method 3: Helm with AWS Load Balancer

```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.type=LoadBalancer \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-type"="nlb" \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-scheme"="internet-facing" \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-nlb-target-type"="instance"
```

## Ingress Management

### Validation Error Fix

If encountering validation errors:

```bash
kubectl delete validatingwebhookconfiguration ingress-nginx-admission
```

### DNS Flush

```bash
ipconfig /flushdns
```

### Scaling Ingress

```bash
kubectl scale deployment ingress-nginx-controller --replicas=2 -n ingress-nginx
```

### Export Ingress Configuration

```bash
kubectl get svc ingress-nginx-controller -n ingress-nginx -o yaml > ingress-nginx-controller.yaml
```

## Ingress Troubleshooting

### Force Delete Ingress

```bash
kubectl patch svc ingress-nginx-controller -n ingress-nginx -p '{"metadata":{"finalizers":null}}' --type=merge
```

### Check Resources

```bash
kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -n ingress-nginx
```

## Ingress Configuration Updates

### Update Ingress Specifications

```bash
helm upgrade ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx \
  --set controller.config.use-proxy-protocol="true" \
  --set controller.config.real-ip-header="proxy_protocol" \
  --set controller.service.annotations."service.beta.kubernetes.io/aws-load-balancer-proxy-protocol"="*" \
  --reuse-values
```

### Patch Service Annotations

```bash
kubectl patch svc ingress-nginx-controller -n ingress-nginx --patch '{"metadata": {"annotations": {"service.beta.kubernetes.io/aws-load-balancer-proxy-protocol": "*"}}}'

kubectl patch svc ingress-nginx-controller -n ingress-nginx --type='json' -p='[{"op": "add", "path": "/metadata/annotations/service.beta.kubernetes.io~1aws-load-balancer-type", "value": "nlb"}]'
```

**Important**: Subnet tags are required for proper load balancer configuration.

## AWS Load Balancer Controller

### Installation

Reference: <https://docs.aws.amazon.com/eks/latest/userguide/lbc-manifest.html>
<https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.3/deploy/installation/>

**Important**: Subnets should be properly tagged.

#### Add EKS Chart Repository

```bash
helm repo add eks https://aws.github.io/eks-charts
helm repo update
```

#### Install AWS Load Balancer Controller

```bash
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  --set clusterName=kubernetes \
  --set serviceAccount.create=true \
  --set region=ap-south-1 \
  --namespace kube-system
```

## Cleanup

### Remove Ingress Controller

```bash
helm uninstall -n ingress-nginx ingress-nginx
```

### Remove AWS Load Balancer Controller

```bash
helm uninstall -n kube-system aws-load-balancer-controller
```
