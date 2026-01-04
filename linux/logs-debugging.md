# Logs and Debugging

## System Logs

### Authentication Logs

```bash
sudo tail -f /var/log/auth.log          # Real-time auth logs (Ubuntu/Debian)
sudo tail -f /var/log/secure           # Real-time auth logs (CentOS/RHEL)
```

### System Logs

```bash
sudo tail -f /var/log/syslog           # System logs (Ubuntu/Debian)
sudo tail -f /var/log/messages         # System logs (CentOS/RHEL)
```

### Kernel Messages

```bash
sudo dmesg                             # Kernel ring buffer
sudo dmesg | grep error                # Filter for errors
sudo dmesg -T                         # Human readable timestamps
```

## Log Viewing Commands

### Basic Log Viewing

```bash
cat /path/to/log                       # View entire log
less /path/to/log                      # Interactive log viewer
tail /path/to/log                      # Last 10 lines
tail -n 50 /path/to/log               # Last 50 lines
tail -f /path/to/log                  # Follow log in real-time
```

### Log Navigation in less

```bash
G                    # Go to end of file
g                    # Go to beginning of file
/search_term         # Search forward
?search_term         # Search backward
n                    # Next search result
N                    # Previous search result
q                    # Quit less
```

## Journalctl (Systemd Logs)

### Basic Journalctl Usage

```bash
journalctl                           # Show all logs
journalctl -f                        # Follow logs in real-time
journalctl -u servicename            # Logs for specific service
journalctl -u servicename -f         # Follow specific service logs
```

### Time-based Filtering

```bash
journalctl --since "2024-01-01"     # Logs since specific date
journalctl --since "1 hour ago"      # Logs from last hour
journalctl --since yesterday           # Logs from yesterday
journalctl --until "2024-01-02"     # Logs until specific date
```

### Priority Filtering

```bash
journalctl -p err                     # Error messages only
journalctl -p warning                # Warning messages only
journalctl -p err..alert             # Error to alert messages
```

### Boot-related Logs

```bash
journalctl -b                        # Current boot logs
journalctl -b -1                     # Previous boot logs
journalctl -b -p err                # Errors from current boot
```

## Application Logs

### Web Server Logs

```bash
# Apache/Nginx access logs
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/apache2/access.log

# Apache/Nginx error logs
sudo tail -f /var/log/nginx/error.log
sudo tail -f /var/log/apache2/error.log
```

### Database Logs

```bash
# MySQL logs
sudo tail -f /var/log/mysql/error.log
sudo tail -f /var/log/mysql/mysql.log

# PostgreSQL logs
sudo tail -f /var/log/postgresql/postgresql-*.log

# MongoDB logs
sudo tail -f /var/log/mongodb/mongod.log
```

### Application-specific Logs

```bash
# Docker logs
docker logs container_name
docker logs -f container_name          # Follow logs
docker logs --tail 100 container_name  # Last 100 lines

# Kubernetes pod logs
kubectl logs pod_name
kubectl logs -f pod_name             # Follow logs
kubectl logs --tail 50 pod_name      # Last 50 lines
```

## Log Rotation and Management

### Check Log Rotation Configuration

```bash
cat /etc/logrotate.conf               # Global logrotate config
cat /etc/logrotate.d/*               # Application-specific configs
```

### Force Log Rotation

```bash
sudo logrotate -f /etc/logrotate.conf  # Force rotation
```

### Compress Old Logs

```bash
sudo gzip /var/log/app.log.1          # Compress log file
```

## Debugging Techniques

### Script Debugging

```bash
# Debug shell scripts
bash -x script.sh                    # Enable debug mode
bash -v script.sh                    # Verbose mode
bash -xv script.sh                   # Both debug and verbose

# Debug with output capture
./myscript.sh | tee debug.log         # Save and display output
./myscript.sh 2>&1 | tee error.log  # Capture stderr and stdout
```

### View and Save Logs Simultaneously

```bash
tail -f /var/log/syslog | tee log_copy.txt
```

### Filter Logs with Grep

```bash
grep "error" /var/log/syslog          # Find error messages
grep -i "failed" /var/log/auth.log   # Case insensitive search
grep -n "pattern" /path/to/log      # Show line numbers
grep -C 3 "pattern" /path/to/log   # Show 3 lines before/after
```

### Real-time Log Filtering

```bash
tail -f /var/log/syslog | grep "error"
tail -f /var/log/auth.log | grep -i "failed"
```

## Performance Debugging

### System Performance Logs

```bash
# System resource usage
vmstat 1                              # Virtual memory statistics
iostat 1                               # I/O statistics
sar 1                                   # System activity reporter

# Process monitoring
top -b -n 1 > process_snapshot.txt     # Save top output to file
ps aux --sort=-%cpu | head -10         # Top 10 CPU processes
ps aux --sort=-%mem | head -10         # Top 10 memory processes
```

### Network Debugging

```bash
# Network connections
ss -tuln                               # Show listening ports
netstat -tuln                          # Alternative command
tcpdump -i eth0                        # Capture network traffic

# DNS debugging
nslookup domain.com                     # DNS lookup
dig domain.com                          # Detailed DNS info
host domain.com                         # Simple DNS lookup
```

## Log Analysis Tools

### Log Analysis with awk

```bash
# Count occurrences of patterns
grep "error" /var/log/syslog | wc -l
awk '/error/ {count++} END {print count}' /var/log/syslog

# Extract specific fields
awk '{print $1, $7}' /var/log/nginx/access.log

# Time-based analysis
awk '$4 >= "[01/Jan/2024:10:00:00" && $4 <= "[01/Jan/2024:11:00:00"' /var/log/nginx/access.log
```

### Log Analysis with sed

```bash
# Extract lines matching pattern
sed -n '/error/p' /var/log/syslog

# Remove lines matching pattern
sed '/debug/d' /var/log/syslog

# Replace text in logs
sed 's/old_ip/new_ip/g' /var/log/access.log
```

## Troubleshooting Common Issues

### Check System Status

```bash
# Failed services
systemctl --failed

# Boot issues
journalctl -b -p err

# Disk space issues
df -h
du -sh /var/log/*

# Memory issues
free -h
dmesg | grep -i memory
```

### Network Issues

```bash
# Check network connectivity
ping -c 4 google.com
traceroute google.com

# Check DNS resolution
nslookup google.com
dig google.com

# Check listening ports
sudo ss -tuln
```

### Service Issues

```bash
# Check service status
systemctl status servicename

# Restart service
sudo systemctl restart servicename

# Check service logs
journalctl -u servicename -f
```

## Log Monitoring and Alerting

### Monitor Logs for Specific Patterns

```bash
# Continuous monitoring
tail -f /var/log/syslog | grep --line-buffered "error" | while read line; do
    echo "Error detected: $line"
    # Add alert logic here
done
```

### Log File Size Monitoring

```bash
# Check log file sizes
find /var/log -name "*.log" -exec ls -lh {} \;

# Monitor log growth
watch -n 60 'du -sh /var/log/syslog'
```

## Advanced Debugging

### Strace for System Call Tracing

```bash
strace -p PID                        # Trace running process
strace -f command                     # Trace command and children
strace -o output.txt command          # Save trace to file
```

### GDB for Application Debugging

```bash
gdb -p PID                           # Debug running process
gdb executable                       # Debug executable
```

### Core Dump Analysis

```bash
# Enable core dumps
ulimit -c unlimited
echo "/tmp/core.%e.%p" > /proc/sys/kernel/core_pattern

# Analyze core dump
gdb executable core_file
```
