# Docker Compose

## Installation

### Linux Installation
```bash
# Download Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.11.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Make executable
sudo chmod +x /usr/local/bin/docker-compose
```

## Basic Commands

### Container Lifecycle
```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v

# Build services
docker-compose build

# Build without cache
docker-compose build --no-cache

# Push images
docker-compose push

# Remove all images
docker-compose down --rmi all
```

### Monitoring and Logs
```bash
# Follow logs
docker-compose logs -f

# Monitor with docker compose
docker-compose logs -f
```

## Advanced Usage

### Multiple Compose Files
```bash
# Use multiple compose files from different folders
docker-compose -f main/docker-compose.yml -f service-b/docker-compose-b.yml -f service-c/docker-compose-c.yml up
```

### Backup Compose Configuration
```bash
# Save compose file configuration to backup
docker-compose -f ./handyman-docker-compose.yml config > ./backups/backup_$timestamp.yml
```

## Development Workflow

### Development, Staging, Production
Docker Compose can be used for different environments:
- Development: Local development with hot reload
- Staging: Pre-production testing
- Production: Production deployment

### Immutable Infrastructure
Consistent environments across all stages using Docker Compose.

## Useful Resources
- Docker Scout for security scanning
- Multi-stage Docker builds
- BuildKit for improved builds: https://docs.docker.com/build/buildkit/
- Reference: https://chatgpt.com/share/6720d72b-84c4-8001-a5e2-83be7556be84
