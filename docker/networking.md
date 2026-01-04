# Docker Networking

## Network Management

### List Networks
```bash
# List all docker networks
docker network ls

# Show IP addresses
ip address show
bridge link
ip route

# Check container IP
hostname -I
```

### Container Network Inspection
```bash
# Get container IP address
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' my_nginx_container

# See IP addresses of all containers
docker ps -q | xargs -n 1 docker inspect --format '{{.Name}}: {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```

### Network Operations
```bash
# Connect container to network
docker network connect my-network node-app

# Disconnect container from network
docker network disconnect <network_name> <container_name_or_id>
```

## Network Types

### Macvlan Network
```bash
# Create macvlan network
docker network create -d macvlan --subnet 172.31.0.0/20 --gateway 172.31.13.161 -o parent=enX0 newasgard
```

### Host Network
```bash
# Run container in host network mode
sudo docker run --name my_nginx --network host -d nginx
```

## Network Debugging

### Install Ping in Containers
```bash
# For Alpine containers
apk add --no-cache iputils

# For Debian/Ubuntu containers
apt-get update
apt-get install -y iputils-ping
```

### Check Volume Mount Points
```bash
# Inspect container mounts
docker inspect <container-name> --format '{{ range .Mounts }}{{ .Name }}:{{ .Destination }} {{ end }}'
```
