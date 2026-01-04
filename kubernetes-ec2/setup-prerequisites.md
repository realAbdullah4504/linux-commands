# Setup Prerequisites

## SSH Connections

### Control Plane
```bash
ssh -i "keypair.pem" ubuntu@ec2-65-0-71-60.ap-south-1.compute.amazonaws.com
```

### Worker Node 1
```bash
ssh -i "keypair.pem" ubuntu@ec2-13-232-57-227.ap-south-1.compute.amazonaws.com
```

## Useful Resources

- Script Resources: https://github.com/piyushsachdeva/CKA-2024/tree/main/Resources/Day27
- Additional Examples: https://github.com/saiyam1814
- Kubernetes Examples: https://github.com/LearningLightInCloud/k8s/tree/main

## AppArmor Configuration

To check AppArmor logs and potentially disable if causing issues:

```bash
sudo systemctl stop apparmor && sudo systemctl disable apparmor
sudo dmesg | grep apparmor
```

## Cluster Overview

Self-provisioned cluster with:
- 1 control-plane node
- 2 worker nodes
