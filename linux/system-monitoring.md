# System Monitoring

## Memory Monitoring

### Check Memory Usage

```bash
free -h
```

### Real-time Memory Monitoring

```bash
top
htop  # More graphical interface (requires installation)
```

### Install htop

```bash
sudo apt install htop
```

## Disk Usage Monitoring

### Check Disk Space Usage

```bash
df -h
```

### Check Directory Size

```bash
du -sh /path/to/directory
```

### Check Specific User Directory Size

```bash
du -sh /home/username
```

### Find Large Files

```bash
find / -type f -size +100M 2>/dev/null
find /home -type f -size +50M 2>/dev/null
```

## Process Monitoring

### View Running Processes

```bash
ps aux
ps aux | grep "nginx"
ps -ef
```

### Process Tree View

```bash
pstree
```

### Systemctl Service Management

```bash
systemctl status servicename
systemctl start servicename
systemctl stop servicename
systemctl restart servicename
systemctl enable servicename
systemctl disable servicename
```

### Journal Logs for Processes

```bash
journalctl -u servicename
journalctl -f  # Follow logs in real-time
journalctl -u servicename -f  # Follow specific service logs
```

## Network Monitoring

### Check Open Ports

```bash
sudo ss -tuln
sudo netstat -tuln
```

### Network Connections

```bash
ss -tuln
netstat -an
```

### Network Interface Statistics

```bash
ifconfig
ip addr show
ip link show
```

### Network Traffic Monitoring

```bash
iftop  # Real-time network usage (requires installation)
sudo apt install iftop
```

## System Resource Monitoring

### CPU Usage

```bash
top
htop
mpstat  # CPU statistics (requires sysstat package)
```

### Install System Monitoring Tools

```bash
sudo apt install sysstat
sudo apt install iotop  # I/O monitoring
```

### I/O Monitoring

```bash
iotop
iostat
```

## System Information

### System Information

```bash
uname -a
lsb_release -a
cat /etc/os-release
```

### Hardware Information

```bash
lscpu  # CPU information
lsblk  # Block device information
lspci  # PCI devices
lsusb  # USB devices
```

### Memory Information

```bash
cat /proc/meminfo
vmstat
```

## Resource Limits

### View System Limits

```bash
ulimit -a
```

### Check File Descriptor Usage

```bash
lsof | wc -l
```

### Check Open Files per User

```bash
lsof -u username | wc -l
```

## Performance Monitoring

### System Load

```bash
uptime
w
```

### Process Resource Usage

```bash
ps aux --sort=-%cpu | head -10  # Top 10 CPU processes
ps aux --sort=-%mem | head -10  # Top 10 memory processes
```

### Real-time System Monitoring

```bash
watch -n 1 'free -h'           # Monitor memory every second
watch -n 1 'df -h'             # Monitor disk space
watch -n 1 'ps aux | head -20'  # Monitor processes
```

## Temperature Monitoring

### CPU Temperature

```bash
sensors  # Requires lm-sensors package
sudo apt install lm-sensors
sudo sensors-detect
```

## Package Management Monitoring

### Check Installed Packages

```bash
dpkg -l
apt list --installed
```

### Search for Specific Packages

```bash
yum list installed | grep mysql  # For CentOS/RHEL
dpkg -l | grep mysql          # For Debian/Ubuntu
```

### Remove Packages

```bash
sudo yum remove mysql80-community-release -y
sudo yum erase mongodb-org*
sudo apt remove package_name
sudo apt purge package_name
```

## System Health Checks

### Check System Logs

```bash
dmesg
dmesg | grep error
journalctl -p err
```

### Check Failed Services

```bash
systemctl --failed
```

### Check Disk Health

```bash
sudo smartctl -a /dev/sda  # Requires smartmontools
sudo apt install smartmontools
```
