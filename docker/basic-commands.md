# Docker Basic Commands

## Container Management

### Run Container
```bash
# Pull and run nginx container
sudo docker pull nginx
sudo docker run -d -p 80:80 nginx

# Run with interactive mode
docker run -it <image> /bin/bash

# Run in host network mode
sudo docker run --name my_nginx --network host -d nginx
```

### Container Operations
```bash
# List all containers
docker ps -a

# Stop container
docker stop <container_name_or_id>

# Enter interactive container shell
docker exec -it <container_name_or_id> /bin/bash

# Execute command in container
docker exec -it wordpress /bin/bash

# Restart service without restarting container
docker exec <container_id_or_name> nginx -s reload

# Delete containers
docker rm <container>
docker container prune
```

### Image Management
```bash
# List all images
docker images

# Push image to registry
docker push myusername/my-app:latest

# Delete images
docker rmi <images>
```

### System Information
```bash
# Display container storage information
docker system df

# Monitor container stats
docker stats

# Check what's running on port 80
sudo lsof -i :80

# Docker storage location
# The docker store in local /var/lib/docker
```

### Copy Files
```bash
# Copy from host to container
docker cp /path/to/volume_name.tar <container_id>:/var/jenkins_home/
```

## Container Run Options

### Common Flags
- `-it`: Instructs docker to allocate pseudo-tty connected to the container
- `-d`: Detach mode (run in background)
- `-p`: Port mapping (host:container)
- `-v`: Volume mounting
- `-e`: Environment variables
- `--name`: Container name
- `--network`: Network mode
