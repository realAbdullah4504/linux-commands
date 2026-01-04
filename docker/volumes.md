# Docker Volumes

## Volume Management

### Create and Use Volumes
```bash
# Create a volume
docker volume create my_volume

# Run container with volume
docker run -d --name my_container -v my_volume:/app myimage
```

### Volume Operations
```bash
# List all volumes
docker volume ls

# Inspect volume
docker volume inspect my_volume1

# Delete volumes
docker volume rm <volume_name_or_id>
docker volume prune
```

## Volume Backup and Restore

### Copy Volume to Another Volume
```bash
# Copy one docker volume to another
docker run --rm \
  -v n8n_data:/from \
  -v ai_n8n_data:/to \
  alpine sh -c "cp -a /from/. /to/"
```

### Backup Volume Data
```bash
# Create backup of volume
docker run --rm \
  -v acunetix-data:/volume \
  -v $(pwd):/backup \
  alpine \
  tar -czvf /backup/acunetix-backup-$(date +%F).tar.gz -C /volume .
```

### Restore Volume Data
```bash
# Create new volume
docker volume create jenkins_home

# Restore from backup
docker run --rm -v jenkins-data:/data -v $(pwd):/backup alpine tar xvf /backup/volume_name.tar -C /data
```

## Database Container Examples

### MongoDB Container with Volume
```bash
docker run --name mongodb-container -d -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=yourUsername \
  -e MONGO_INITDB_ROOT_PASSWORD=yourPassword \
  -v mongodb-data:/data/db mongo
```

## Volume Inspection

### Check Container Mounts
```bash
# Inspect container volume mounts
docker inspect <container_name_or_id>

# Check specific mount points
docker inspect <container-name> --format '{{ range .Mounts }}{{ .Name }}:{{ .Destination }} {{ end }}'
```
