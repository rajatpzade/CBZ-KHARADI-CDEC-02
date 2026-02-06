# Day-18

---

## Basic Networking in Linux

Welcome to Day 18! Today, we'll dive into the fundamentals of networking in Linux. Understanding networking is essential for system administration, troubleshooting connectivity issues, and managing network configurations. We'll cover basic concepts, commands, and practical configuration steps.

---

### Overview of Networking Fundamentals

**What is Networking?**
Networking in Linux involves connecting computers and devices to share resources, communicate, and access services. It enables data transfer between systems over various media (wired, wireless, etc.).

**Key Networking Concepts:**
- **IP Address:** Unique identifier for devices on a network (e.g., 192.168.1.100)
- **Subnet Mask:** Defines network boundaries (e.g., 255.255.255.0)
- **Gateway/Default Route:** Router that connects to other networks (e.g., 192.168.1.1)
- **DNS:** Translates domain names to IP addresses (e.g., google.com → 8.8.8.8)
- **MAC Address:** Hardware address of network interface (e.g., 00:1B:44:11:3A:B7)

**Network Layers (Simplified):**
1. **Physical Layer:** Cables, wireless signals
2. **Data Link Layer:** MAC addresses, Ethernet
3. **Network Layer:** IP addresses, routing (IP protocol)
4. **Transport Layer:** TCP/UDP ports
5. **Application Layer:** HTTP, FTP, SSH

**Why Networking Matters in Linux:**
- Remote access via SSH
- File sharing (NFS, Samba)
- Web services (Apache, Nginx)
- System updates and package downloads
- Multi-system administration

---

### Network Types and Protocols

#### Network Types:
1. **Local Area Network (LAN):** Small network, same building (e.g., home/office)
2. **Wide Area Network (WAN):** Large network, multiple locations (e.g., internet)
3. **Wireless LAN (WLAN):** Wi-Fi networks
4. **Virtual Private Network (VPN):** Secure connection over public network

#### Common Protocols:
- **TCP (Transmission Control Protocol):** Reliable, connection-oriented (e.g., HTTP, SSH)
- **UDP (User Datagram Protocol):** Fast, connectionless (e.g., DNS, video streaming)
- **IP (Internet Protocol):** Routing and addressing
- **ICMP (Internet Control Message Protocol):** Network diagnostics (ping)
- **ARP (Address Resolution Protocol):** Maps IP to MAC addresses

#### Port Numbers:
- **Well-known Ports:** 0-1023 (e.g., 22=SSH, 80=HTTP, 443=HTTPS)
- **Registered Ports:** 1024-49151
- **Dynamic Ports:** 49152-65535

**Example Services and Ports:**
- SSH: 22
- HTTP: 80
- HTTPS: 443
- FTP: 21
- DNS: 53

---

### Using ifconfig and ip Commands

These are essential commands for viewing and managing network interfaces.

#### ifconfig Command (Deprecated but still used):
**Purpose:** Configure and display network interface information

**Basic Usage:**
```bash
# Show all interfaces
ifconfig

# Show specific interface
ifconfig eth0

# Bring interface up/down
sudo ifconfig eth0 up
sudo ifconfig eth0 down

# Set IP address temporarily
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0
```

**Sample Output:**
```bash
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::a00:27ff:fe4e:66a1  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:4e:66:a1  txqueuelen 1000  (Ethernet)
        RX packets 12345  bytes 1234567 (1.2 MB)
        TX packets 6789  bytes 987654 (987.6 KB)
```

#### ip Command (Modern replacement for ifconfig):
**Purpose:** Show and manipulate routing, devices, policy routing, and tunnels

**Basic Usage:**
```bash
# Show all interfaces
ip addr show
ip a  # Short form

# Show specific interface
ip addr show eth0

# Show routing table
ip route show
ip r  # Short form

# Bring interface up/down
sudo ip link set eth0 up
sudo ip link set eth0 down

# Set IP address temporarily
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip addr del 192.168.1.100/24 dev eth0
```

**Sample Output:**
```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:4e:66:a1 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 86399sec preferred_lft 86399sec
```

**Key Differences:**
- `ifconfig`: Older, simpler, being phased out
- `ip`: Modern, more powerful, part of iproute2 suite

---

### Basic Network Configuration Steps

#### 1. Identify Network Interfaces:
```bash
ip a
# or
ifconfig
```

#### 2. Check Current Configuration:
```bash
# IP address, subnet, gateway
ip addr show

# Routing table
ip route show

# DNS servers
cat /etc/resolv.conf
```

#### 3. Test Connectivity:
```bash
# Ping local gateway
ping -c 4 192.168.1.1

# Ping external host
ping -c 4 google.com

# Test DNS resolution
nslookup google.com
```

#### 4. Configure Network (Temporary):
```bash
# Set IP address
sudo ip addr add 192.168.1.100/24 dev eth0

# Set default gateway
sudo ip route add default via 192.168.1.1

# Set DNS
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

#### 5. Make Changes Permanent:
Use NetworkManager (nmcli/nmtui) or edit configuration files directly.

---

### Configuring Static IP with nmtui and nmcli

NetworkManager provides user-friendly tools for network configuration.

#### Using nmtui (Text-based UI):
**nmtui** provides a simple text interface for network configuration.

```bash
# Launch nmtui
sudo nmtui

# Navigate with arrow keys and Enter
# 1. Select "Edit a connection"
# 2. Choose your network interface (e.g., eth0)
# 3. Select "Edit"
# 4. Change IPv4 Configuration to "Manual"
# 5. Enter IP Address, Netmask, Gateway
# 6. Enter DNS servers
# 7. Select "OK" and "Back"
# 8. Select "Activate a connection" if needed
# 9. Quit
```

#### Using nmcli (Command Line):
**nmcli** is the command-line tool for NetworkManager.

**Basic Commands:**
```bash
# List connections
nmcli connection show

# Show device status
nmcli device status

# Modify connection (replace 'eth0' with your interface)
sudo nmcli connection modify eth0 ipv4.method manual
sudo nmcli connection modify eth0 ipv4.addresses 192.168.1.100/24
sudo nmcli connection modify eth0 ipv4.gateway 192.168.1.1
sudo nmcli connection modify eth0 ipv4.dns "8.8.8.8 8.8.4.4"

# Bring connection down and up to apply changes
sudo nmcli connection down eth0
sudo nmcli connection up eth0
```

**View Configuration:**
```bash
# Show connection details
nmcli connection show eth0
```

---

### Example: Configuring a Static IP Address and Verifying Network Connectivity

#### Scenario:
Configure eth0 with static IP 192.168.1.100, subnet 255.255.255.0, gateway 192.168.1.1, DNS 8.8.8.8

#### Step-by-Step Configuration:

1. **Check Current Configuration:**
   ```bash
   ip addr show eth0
   ip route show
   cat /etc/resolv.conf
   ```

2. **Configure with nmcli:**
   ```bash
   sudo nmcli connection modify eth0 ipv4.method manual
   sudo nmcli connection modify eth0 ipv4.addresses 192.168.1.100/24
   sudo nmcli connection modify eth0 ipv4.gateway 192.168.1.1
   sudo nmcli connection modify eth0 ipv4.dns "8.8.8.8"
   ```

3. **Apply Changes:**
   ```bash
   sudo nmcli connection down eth0
   sudo nmcli connection up eth0
   ```

4. **Verify Configuration:**
   ```bash
   # Check IP address
   ip addr show eth0
   
   # Check routing
   ip route show
   
   # Check DNS
   cat /etc/resolv.conf
   ```

5. **Test Connectivity:**
   ```bash
   # Ping gateway
   ping -c 4 192.168.1.1
   
   # Ping external host
   ping -c 4 google.com
   
   # Test DNS
   nslookup google.com
   
   # Test internet connectivity
   curl -I https://www.google.com
   ```

6. **Troubleshooting if Issues Occur:**
   ```bash
   # Check NetworkManager status
   systemctl status NetworkManager
   
   # Restart NetworkManager
   sudo systemctl restart NetworkManager
   
   # Check logs
   journalctl -u NetworkManager -n 20
   ```

#### Alternative: Using nmtui:
```bash
sudo nmtui
# Follow the menu to set static IP as described earlier
```

---

## Hands-On Exercises for Students

1. **Explore Network Interfaces:**
   ```bash
   # List all interfaces
   ip a
   
   # Show routing table
   ip route show
   
   # Check DNS configuration
   cat /etc/resolv.conf
   ```

2. **Test Connectivity:**
   ```bash
   # Ping local gateway (find gateway first with ip route)
   ping -c 4 [gateway-ip]
   
   # Ping external host
   ping -c 4 google.com
   
   # Test DNS resolution
   host google.com
   ```

3. **Configure Static IP with nmcli:**
   ```bash
   # Backup current connection
   sudo nmcli connection show
   
   # Modify connection (use your interface name)
   sudo nmcli connection modify [interface] ipv4.method manual
   sudo nmcli connection modify [interface] ipv4.addresses 192.168.1.200/24
   sudo nmcli connection modify [interface] ipv4.gateway 192.168.1.1
   sudo nmcli connection modify [interface] ipv4.dns "8.8.8.8"
   
   # Apply changes
   sudo nmcli connection down [interface]
   sudo nmcli connection up [interface]
   
   # Verify
   ip addr show [interface]
   ping -c 4 google.com
   ```

4. **Use nmtui for Configuration:**
   ```bash
   sudo nmtui
   # Follow the interface to set static IP
   # Test connectivity after
   ```

5. **Network Troubleshooting:**
   ```bash
   # Check interface status
   nmcli device status
   
   # Check connection status
   nmcli connection show
   
   # Restart networking
   sudo systemctl restart NetworkManager
   
   # Test with different tools
   traceroute google.com
   dig google.com
   ```

---

## Quick Reference Cheat-Sheet

### Network Commands:
- `ip addr show` — Show IP addresses
- `ip route show` — Show routing table
- `ping host` — Test connectivity
- `nslookup host` — DNS lookup
- `traceroute host` — Trace network path

### NetworkManager Commands:
- `nmcli connection show` — List connections
- `nmcli device status` — Show device status
- `sudo nmtui` — Text UI for configuration
- `nmcli connection modify` — Modify connection

### Configuration Files:
- `/etc/resolv.conf` — DNS servers
- `/etc/hosts` — Local hostname resolution
- `/etc/network/interfaces` — Static config (older systems)

### Common Issues:
- No internet: Check gateway and DNS
- IP conflict: Use different IP address
- DNS issues: Check /etc/resolv.conf

---

## Key Takeaways for Students

- Networking fundamentals include IP addresses, subnets, gateways, and DNS.
- Use `ip` command for modern network management; `ifconfig` is legacy.
- NetworkManager tools (nmcli, nmtui) simplify configuration.
- Always test connectivity after configuration changes.
- Static IP configuration requires IP, subnet mask, gateway, and DNS.

Remember, networking is crucial for Linux administration. Practice these commands in a safe environment before applying to production systems!

--- 