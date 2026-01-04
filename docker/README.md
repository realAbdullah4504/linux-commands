# Docker Commands

This directory contains comprehensive Docker commands and documentation organized by topic for container management and orchestration.

## 📚 Quick Navigation

### 🚀 Docker Basics
- **[install.md](./install.md)** - Docker installation and setup
- **[basic-commands.md](./basic-commands.md)** - Container management essentials
- **[docker-compose.md](./docker-compose.md)** - Multi-container applications

### 🔧 Docker Advanced
- **[networking.md](./networking.md)** - Docker networking configuration
- **[volumes.md](./volumes.md)** - Data persistence and volumes
- **[advanced.md](./advanced.md)** - Advanced Docker techniques

## 🎯 Quick Reference Commands

### Container Management
```bash
# Run container
docker run -d nginx                   # Run in detached mode
docker run -it ubuntu /bin/bash     # Interactive mode
docker run --name mycontainer nginx  # Named container

# List containers
docker ps                               # Running containers
docker ps -a                            # All containers
docker ps -q                            # Container IDs only

# Stop/Remove containers
docker stop <container_id>                # Stop container
docker rm <container_id>                  # Remove container
docker kill <container_id>                 # Force stop
```

### Image Management
```bash
# Pull images
docker pull ubuntu                      # Pull latest image
docker pull ubuntu:20.04               # Pull specific version

# List images
docker images                          # List all images
docker images -q                       # Image IDs only

# Build images
docker build -t app:latest .            # Build with tag
docker build -f Dockerfile .             # Specify Dockerfile

# Remove images
docker rmi <image_id>                   # Remove image
docker rmi -f $(docker images -q)        # Remove all images
```

### Docker Compose
```bash
# Start services
docker-compose up -d                   # Detached mode
docker-compose up --build               # Build and start

# Stop services
docker-compose down                     # Stop and remove
docker-compose stop                    # Stop only

# View logs
docker-compose logs -f                  # Follow logs
docker-compose logs web                 # Specific service
```

### Volume Management
```bash
# Create volume
docker volume create myvolume           # Named volume

# List volumes
docker volume ls                       # List volumes
docker volume inspect myvolume          # Volume details

# Mount volume
docker run -v myvolume:/data ubuntu   # Mount when running

# Backup and restore volumes
docker run --rm -v source:/data -v backup:/backup alpine tar -czf /backup/data.tar.gz -C /data
docker run --rm -v target:/data -v backup:/backup alpine tar -xzf /backup/data.tar.gz -C /data
```

### Network Management
```bash
# Create network
docker network create mynetwork          # Bridge network
docker network create --driver overlay mynet  # Overlay network

# List networks
docker network ls                     # List networks

# Connect container to network
docker network connect mynetwork container
```

## 🔍 Search Commands

### Find Docker Commands
```bash
# By category
grep -r "docker run" ./docker/           # Run commands
grep -r "docker build" ./docker/         # Build commands
grep -r "volume" ./docker/volumes.md       # Volume commands
grep -r "network" ./docker/networking.md    # Network commands
```

### By Use Case
```bash
# Container operations
grep -r "run\|ps\|stop\|rm" ./docker/basic-commands.md

# Image management
grep -r "pull\|images\|build\|rmi" ./docker/basic-commands.md ./docker/advanced.md

# Docker Compose
grep -r "up\|down\|logs" ./docker/docker-compose.md

# Troubleshooting
grep -r "error\|debug\|fix" ./docker/advanced.md
```

## 📖 Usage Tips

### For Beginners
1. Start with [install.md](./install.md) to set up Docker
2. Learn basic commands with [basic-commands.md](./basic-commands.md)
3. Practice with [docker-compose.md](./docker-compose.md) for multi-container apps

### For Advanced Users
1. Master networking with [networking.md](./networking.md)
2. Learn volume management with [volumes.md](./volumes.md)
3. Study advanced techniques with [advanced.md](./advanced.md)

## 🛠️ Common Workflows

### Web Application Deployment
```bash
# 1. Build and run
docker build -t myapp .
docker run -d -p 8080:80 --name myapp myapp

# 2. With volume
docker run -d -p 8080:80 -v ./data:/app/data myapp

# 3. With environment variables
docker run -d -p 8080:80 -e NODE_ENV=production myapp
```

### Development Environment
```bash
# 1. Start development stack
docker-compose up -d

# 2. View logs
docker-compose logs -f web

# 3. Execute commands in container
docker exec -it web_container bash

# 4. Stop all services
docker-compose down
```

### Production Deployment
```bash
# 1. Pull latest images
docker pull myapp:latest
docker pull postgres:13

# 2. Run with production settings
docker run -d --name prod_db \
  -e POSTGRES_PASSWORD=securepass \
  -v pgdata:/var/lib/postgresql/data \
  postgres:13

# 3. Backup data
docker exec prod_db pg_dump -U postgres mydb > backup.sql
```

## 📚 Additional Resources

### Documentation
- [Docker Official Docs](https://docs.docker.com/)
- [Docker Compose Reference](https://docs.docker.com/compose/)
- [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

### Tools
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Portainer](https://www.portainer.io/)
- [Docker Swarm](https://docs.docker.com/engine/swarm/)

### Registries
- [Docker Hub](https://hub.docker.com/)
- [GitHub Container Registry](https://ghcr.io/)
- [Amazon ECR](https://aws.amazon.com/ecr/)

---

**💡 Pro Tip:** Use `docker --help` or `docker-compose --help` to get detailed help for any command.

**🔖 Bookmark this page** for quick access to essential Docker commands!
