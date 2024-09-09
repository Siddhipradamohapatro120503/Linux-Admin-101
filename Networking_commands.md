# Linux Networking and Troubleshooting Commands Cheat Sheet

This cheat sheet provides an overview of essential Linux networking and troubleshooting commands that every software developer, system administrator, or DevOps engineer should know.

## 1. ifconfig / ip

`ifconfig` is used to display and configure network interfaces. However, it's being phased out in favor of the `ip` command.

```bash
# Display network devices and configuration
ip addr

# Get details of a specific interface
ip a show eth0

# List routing tables
ip route
```

## 2. traceroute / tracepath

`traceroute` is used for troubleshooting network connectivity and determining the path to a destination.

```bash
# Trace route to a destination
traceroute google.com

# Use ICMP instead of UDP
traceroute -I google.com

# Avoid reverse DNS lookup
traceroute -n google.com
```

`tracepath` is similar to `traceroute` but doesn't require root privileges.

```bash
tracepath google.com
```

## 3. ping

`ping` is used to check network connectivity and measure round-trip time.

```bash
# Basic ping
ping google.com

# Limit the number of packets
ping -c 4 google.com
```

## 4. netstat / ss

`netstat` provides network statistics. `ss` is a more modern replacement for `netstat`.

```bash
# List all connections
ss

# List all TCP listening ports
ss -lt

# List all established connections
ss -t -r state established
```

## 5. curl

`curl` is a versatile tool for data transfer and network troubleshooting.

```bash
# Download a webpage
curl https://www.example.com

# Check web server headers
curl -I https://www.example.com

# Test connectivity to a specific port
curl -v telnet://192.168.1.1:22
```

## 6. wget

`wget` is used for downloading files and can also help with network troubleshooting.

```bash
# Download a file
wget https://example.com/file.zip

# Download through a proxy
wget -e use_proxy=yes -e http_proxy=proxy.example.com:8080 https://example.com/file
```

## 7. hostname

`hostname` is used to view or set the system's hostname.

```bash
# View current hostname
hostname

# Set a new hostname (temporary)
sudo hostname new-hostname
```

## 8. ssh

`ssh` is used for secure remote login and command execution.

```bash
# Connect to a remote server
ssh username@remote_host

# Use a specific private key
ssh -i ~/path/to/private_key.pem username@remote_host
```

## 9. scp

`scp` is used for secure file transfer between hosts.

```bash
# Copy a file to a remote host
scp /path/to/local/file.txt username@remote_host:/path/to/remote/directory/

# Copy a file from a remote host
scp username@remote_host:/path/to/remote/file.txt /path/to/local/directory/
```

## 10. dig

`dig` is used for DNS lookups and troubleshooting.

```bash
# Perform a basic DNS lookup
dig example.com

# Get specific DNS record types
dig example.com A +short
dig example.com MX +short

# Perform a reverse DNS lookup
dig -x 8.8.8.8
```

## 11. arp

`arp` is used to view and manage the ARP cache.

```bash
# View the ARP cache
arp
```

## 12. mtr

`mtr` combines the functionality of `ping` and `traceroute`.

```bash
# Run an mtr report
mtr -n --report google.com
```

## 13. nc (netcat)

`nc` is a versatile networking utility for reading from and writing to network connections.

```bash
# Check if a port is open
nc -v -n 192.168.1.1 22
```

## 14. lsof

`lsof` lists open files and can be used to find processes using specific ports.

```bash
# Find process using a specific port
lsof -i :8080
```

Remember to consult the man pages (`man command_name`) for more detailed information on each command and its options.
