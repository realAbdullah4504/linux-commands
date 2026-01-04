# Networking and File Transfer

## SSH Connections

### Basic SSH Connection

```bash
ssh -i /path/to/key.pem user@hostname
ssh -i /c/Users/YourUsername/.ssh/ec2-key.pem ec2-user@your-ec2-public-ip
```

### SSH with Port Forwarding

#### Local Port Forwarding

```bash
ssh -i "keypair.pem" -L 27018:localhost:27018 abdullah@3.110.84.40
```

#### Remote Port Forwarding

```bash
ssh -i key.pem -R 8080:localhost:80 user@hostname
```

#### Dynamic Port Forwarding (SOCKS Proxy)

```bash
ssh -D 8080 user@hostname
```

### SSH Configuration

#### Create SSH Config

```bash
nano ~/.ssh/config
```

Example config:

```
Host myserver
    HostName example.com
    User username
    IdentityFile ~/.ssh/key.pem
    Port 22
```

### SSH Key Management

#### Generate SSH Key

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

#### Copy SSH Key to Server

```bash
ssh-copy-id -i ~/.ssh/key.pem user@hostname
```

#### Manage Known Hosts

```bash
# Remove specific host from known_hosts
ssh-keygen -f "/home/abdullah/.ssh/known_hosts" -R "72.60.7.166"

# Remove host key for any IP
ssh-keygen -f ~/.ssh/known_hosts -R hostname

# Remove all host keys
ssh-keygen -f ~/.ssh/known_hosts -R
```

## SCP File Transfer

### Copy File from Remote to Local

```bash
scp -i carlos_server.pem -r root@212.85.17.223:/root/rengine_backup /mnt/e/
```

### Copy File from Local to Remote

```bash
scp -i "keypair.pem" ./article-db.articles.json ec2-user@ec2-3-7-69-212.ap-south-1.compute.amazonaws.com:/home/ec2-user/
```

### Copy Directory Recursively

```bash
scp -r -i key.pem /local/path user@hostname:/remote/path
```

### Copy with Port Specification

```bash
scp -P 2222 -i key.pem file.txt user@hostname:/path/
```

## Rsync for Synchronization

### Basic Rsync

```bash
rsync -avz /source/ user@hostname:/destination/
```

### Rsync with SSH Key

```bash
rsync -avz -e "ssh -i key.pem" /source/ user@hostname:/destination/
```

### Rsync with Progress

```bash
rsync -avz --progress /source/ user@hostname:/destination/
```

### Rsync with Delete

```bash
rsync -avz --delete /source/ user@hostname:/destination/
```

## Network Diagnostics

### Check Network Connectivity

```bash
ping hostname
ping -c 4 hostname  # Send 4 packets
```

### Trace Route

```bash
traceroute hostname
tracepath hostname
```

### DNS Lookup

```bash
nslookup hostname
dig hostname
host hostname
```

### Check Open Ports

```bash
sudo ss -tuln
sudo netstat -tuln
nmap -sT -O localhost
```

### Network Interface Information

```bash
ifconfig
ip addr show
ip link show
```

### Network Statistics

```bash
ip -s link show
cat /proc/net/dev
```

## Network Configuration

### Check IP Address

```bash
ip addr show
hostname -I
curl ifconfig.me  # Public IP
```

### Set Static IP (Temporary)

```bash
ip addr add 192.168.1.100/24 dev eth0
```

### Check Routing Table

```bash
ip route show
route -n
```

### Check ARP Table

```bash
arp -a
ip neigh show
```

## Network Services

### Check Listening Services

```bash
sudo netstat -tulpn
sudo ss -tulpn
lsof -i -P -n | grep LISTEN
```

### Check Network Connections

```bash
netstat -an
ss -an
```

### Monitor Network Traffic

```bash
iftop
nethogs
sudo tcpdump -i eth0
```

## Firewall Management

### UFW (Ubuntu)

```bash
sudo ufw enable
sudo ufw status
sudo ufw allow 22/tcp
sudo ufw deny 80/tcp
sudo ufw reload
```

### iptables

```bash
sudo iptables -L
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables-save > /etc/iptables/rules.v4
```

## SSH Tunneling Examples

### Database Tunnel

```bash
ssh -i key.pem -L 3306:localhost:3306 user@db-server
```

### Web Server Tunnel

```bash
ssh -i key.pem -L 8080:localhost:80 user@web-server
```

### SSH Through Gateway

```bash
ssh -i key.pem -J gateway-user@gateway-host target-user@target-host
```

## Network Performance Testing

### Bandwidth Test

```bash
iperf3 -s  # Server mode
iperf3 -c server_ip  # Client mode
```

### Download Speed Test

```bash
wget -O /dev/null http://speedtest.net/10mb.zip
curl -o /dev/null http://speedtest.net/10mb.zip
```

## Network Troubleshooting

### Check DNS Resolution

```bash
nslookup google.com
dig google.com
host google.com
```

### Test Port Connectivity

```bash
telnet hostname port
nc -zv hostname port
```

### Check Network Latency

```bash
ping -c 10 hostname
mtr hostname  # Continuous traceroute
```

### Monitor Network Connections

```bash
watch -n 1 'ss -tuln'
watch -n 1 'netstat -tuln'
```

## Advanced Networking

### Create Network Interface Alias

```bash
sudo ip addr add 192.168.1.101/24 dev eth0:1
```

### Bridge Configuration

```bash
sudo brctl addbr br0
sudo brctl addif br0 eth0
```

### VLAN Configuration

```bash
sudo ip link add link eth0 name eth0.100 type vlan id 100
sudo ip addr add 192.168.100.1/24 dev eth0.100
```

## Network Security

### SSH Hardening

```bash
# Edit /etc/ssh/sshd_config
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

### Check for Failed Login Attempts

```bash
sudo grep "Failed password" /var/log/auth.log
sudo journalctl -u sshd | grep "Failed"
```
