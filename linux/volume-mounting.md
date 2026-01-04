# Volume Management and Mounting

## Disk and Volume Information

### Check Attached Volumes

```bash
lsblk
```

### Check Block Device Information

```bash
blkid /dev/xvdf
ls -la /dev/sd*
fdisk -l
```

### Check Disk Usage

```bash
df -h
du -sh /path/to/directory
```

## Volume Mounting

### Basic Mounting

```bash
sudo mount /dev/xvdf /mnt/mongodb
```

### Mount with Filesystem Type

```bash
sudo mount -t ext4 /dev/xvdf /mnt/mongodb
```

### Mount with Options

```bash
sudo mount -o defaults,noatime /dev/xvdf /mnt/mongodb
```

## Automated Volume Mounting Script

### Wait and Mount Script

```bash
#!/bin/bash

# Device and Mount Point
DEVICE="/dev/xvdf"
MOUNT_POINT="/mnt/mongodb"

# Wait for device to appear
while [ ! -e $DEVICE ]; do 
    echo "Waiting for device $DEVICE to appear..."
    sleep 1; 
done

# Check if device is formatted as ext4
if ! blkid $DEVICE | grep -q "TYPE=\"ext4\""; then
    echo "Formatting $DEVICE as ext4..."
    # Ensure device is not mounted before formatting
    sudo umount $DEVICE || true
    sudo mkfs.ext4 $DEVICE
fi

# Create mount point if it doesn't exist
sudo mkdir -p $MOUNT_POINT

# Mount device
echo "Mounting $DEVICE to $MOUNT_POINT..."
sudo mount $DEVICE $MOUNT_POINT

# Update /etc/fstab to ensure persistence
if ! grep -qs "$DEVICE" /etc/fstab; then
    echo "$DEVICE $MOUNT_POINT ext4 defaults,nofail 0 2" | sudo tee -a /etc/fstab
fi
```

## Filesystem Formatting

### Format as ext4

```bash
sudo mkfs.ext4 /dev/xvdf
```

### Format with Label

```bash
sudo mkfs.ext4 -L "data" /dev/xvdf
```

### Format as NTFS (for Windows compatibility)

```bash
sudo mkfs.ntfs /dev/xvdf
```

### Format as XFS

```bash
sudo mkfs.xfs /dev/xvdf
```

## fstab Configuration

### Edit fstab

```bash
sudo nano /etc/fstab
```

### fstab Entry Format

```
<device> <mount_point> <filesystem> <options> <dump> <pass>
```

### Common fstab Entries

```bash
# Standard ext4 mount
/dev/xvdf /mnt/data ext4 defaults,nofail 0 2

# NFS mount
server:/path/to/share /mnt/nfs nfs defaults 0 0

# Bind mount
/mnt/source /mnt/destination none bind 0 0
```

### fstab Options

- `defaults` - Default options (rw, suid, dev, exec, auto, nouser, async)
- `nofail` - Don't boot if device doesn't exist
- `noatime` - Don't update access time
- `ro` - Read-only
- `rw` - Read-write
- `user` - Allow any user to mount
- `users` - Allow any user to mount/unmount

## Bind Mounts

### Create Bind Mount

```bash
sudo mount --bind /mnt/external_drive/docker_volumes /var/lib/docker/volumes
```

### Persistent Bind Mount in fstab

```bash
sudo nano /etc/fstab
```

Add this line:

```
/mnt/external_drive/docker_volumes /var/lib/docker/volumes none bind 0 0
```

### Test fstab Mounts

```bash
sudo mount -a  # Mount all entries in fstab
```

## Mount Management

### Unmount Volumes

```bash
sudo umount /mnt/mongodb
sudo umount /dev/xvdf
```

### Force Unmount

```bash
sudo umount -l /mnt/mongodb  # Lazy unmount
sudo umount -f /mnt/mongodb  # Force unmount
```

### Remount with Options

```bash
sudo mount -o remount,ro /mnt/mongodb  # Remount as read-only
sudo mount -o remount,rw /mnt/mongodb  # Remount as read-write
```

## LVM (Logical Volume Manager)

### Create Physical Volume

```bash
sudo pvcreate /dev/xvdf
```

### Create Volume Group

```bash
sudo vgcreate datavg /dev/xvdf
```

### Create Logical Volume

```bash
sudo lvcreate -n datalv -l 100%FREE datavg
```

### Format Logical Volume

```bash
sudo mkfs.ext4 /dev/datavg/datalv
```

### Mount Logical Volume

```bash
sudo mount /dev/datavg/datalv /mnt/data
```

## Swap Management

### Create Swap File

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

### Add to fstab

```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

### Check Swap Usage

```bash
swapon --show
free -h
```

## Disk Health and Maintenance

### Check Disk Health

```bash
sudo fsck /dev/xvdf
sudo e2fsck -f /dev/xvdf
```

### Resize Filesystem

```bash
sudo resize2fs /dev/xvdf
```

### Defragment ext4

```bash
sudo e4defrag /dev/xvdf
```

## Monitoring Disk I/O

### Monitor Disk Usage

```bash
iotop
sudo iotop
```

### Disk Statistics

```bash
iostat -x 1
vmstat 1
```

## Troubleshooting

### Check Mounted Filesystems

```bash
mount | column -t
findmnt
```

### Check Available Space

```bash
df -h
df -i  # Check inodes
```

### Fix Corrupted Filesystem

```bash
sudo fsck -y /dev/xvdf
```

### Recover Lost Files

```bash
sudo photorec /dev/xvdf
```

## Advanced Mounting

### Mount ISO Image

```bash
sudo mount -o loop image.iso /mnt/iso
```

### Mount NFS Share

```bash
sudo mount -t nfs server:/path/to/share /mnt/nfs
```

### Mount Samba Share

```bash
sudo mount -t cifs //server/share /mnt/smb -o username=user,password=pass
```

### Mount tmpfs (RAM Disk)

```bash
sudo mount -t tmpfs -o size=1G tmpfs /mnt/ramdisk
```
