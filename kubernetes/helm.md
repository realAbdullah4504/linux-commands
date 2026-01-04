# Helm Package Manager

## Installation

### Linux/macOS Installation
```bash
# Download Helm installation script
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

# Make script executable
chmod 700 get_helm.sh

# Run installation script
./get_helm.sh
```

### Windows Installation
```bash
# Install using Chocolatey
choco install kubernetes-helm

# Or using Scoop
scoop install helm
```

### Verify Installation
```bash
# Check Helm version
helm version

# List available commands
helm help
```

## Basic Helm Commands

### Repository Management
```bash
# Add repository
helm repo add <repo-name> <repo-url>

# List repositories
helm repo list

# Update repositories
helm repo update

# Remove repository
helm repo remove <repo-name>

# Search for charts
helm search repo <chart-name>
```

### Chart Operations
```bash
# Install chart
helm install <release-name> <chart-name>

# Install chart from specific repo
helm install <release-name> <repo-name>/<chart-name>

# Install chart with values file
helm install <release-name> <chart-name> -f values.yaml

# Install chart with set values
helm install <release-name> <chart-name> --set key=value

# List releases
helm list

# List releases in all namespaces
helm list --all-namespaces

# Get release status
helm status <release-name>

# Upgrade release
helm upgrade <release-name> <chart-name>

# Rollback release
helm rollback <release-name> <revision>

# Uninstall release
helm uninstall <release-name>
```

## Chart Development

### Create Chart
```bash
# Create new chart
helm create <chart-name>

# Package chart
helm package <chart-path>

# Lint chart
helm lint <chart-path>

# Template rendering (dry run)
helm template <release-name> <chart-path>

# Install dependencies
helm dependency update <chart-path>
```

### Chart Structure
```
chart-name/
├── Chart.yaml          # Chart metadata
├── values.yaml         # Default configuration values
├── templates/          # Template files
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ...
├── charts/            # Dependency charts
└── .helmignore        # Files to ignore
```

## Configuration Management

### Values Files
```bash
# Show default values
helm show values <chart-name>

# Override values with file
helm install <release-name> <chart-name> -f custom-values.yaml

# Override multiple values files
helm install <release-name> <chart-name> -f values.yaml -f prod-values.yaml

# Set values from command line
helm install <release-name> <chart-name> --set image.tag=v1.2.3 --set replicas=3
```

### Environment-Specific Configurations
```bash
# Development
helm install app-dev ./app -f values-dev.yaml

# Staging
helm install app-staging ./app -f values-staging.yaml

# Production
helm install app-prod ./app -f values-prod.yaml
```

## Troubleshooting

### Debug Helm Commands
```bash
# Enable verbose output
helm install <release-name> <chart-name> --debug --dry-run

# Check chart dependencies
helm dependency list <chart-path>

# Validate chart
helm lint <chart-path>

# Show manifest without installing
helm template <release-name> <chart-path>
```

### Common Issues
- Ensure Kubernetes cluster is accessible
- Check Helm version compatibility
- Verify chart dependencies are satisfied
- Check for conflicting values in multiple files
