# Networking

## DNS Resolution

### DNS Configuration

Check network source stop option for DNS resolution issues.

Reference: <https://chatgpt.com/share/67407b8e-fa78-8001-921c-54ad46cb5e34>

### Fix DNS Resolution

To fix DNS resolution issues, you may need to update the resolv.conf configuration:

```bash
sudo rm /etc/resolv.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

### DNS Testing

Deploy DNS utilities for testing:

```bash
kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml
```

Test DNS resolution:

```bash
kubectl exec -i -t dnsutils -n default -- nslookup mongodb-service
kubectl exec -i -t dnsutils -- nslookup kubernetes.default
```

## AWS CNI

### AWS VPC CNI Plugin

Reference: <https://docs.aws.amazon.com/eks/latest/userguide/vpc-add-on-self-managed-update.html>
GitHub: <https://github.com/aws/amazon-vpc-cni-k8s>

### ECR Authentication

Authenticate with Amazon ECR:

```bash
aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 602401143452.dkr.ecr.us-west-2.amazonaws.com
```

### Create ECR Secret

Create a Kubernetes secret for ECR access:

```bash
kubectl create secret generic ecr-secret \
  --from-file=.dockerconfigjson=/home/ubuntu/.docker/config.json \
  --type=kubernetes.io/dockerconfigjson \
  --namespace=kube-system
```

### Update AWS Node DaemonSet

Edit the AWS node DaemonSet to use the ECR secret:

```bash
kubectl edit daemonset aws-node -n kube-system
```

Add the following configuration:

```yaml
spec:
  template:
    spec:
      imagePullSecrets:
      - name: ecr-secret
```

## Network Configuration

### DNS Configuration for Pods

When configuring DNS for pods, consider using the `--resolv-conf` option to specify custom DNS configuration.

### Network Policies

Implement network policies to control traffic flow between pods and namespaces for enhanced security.
