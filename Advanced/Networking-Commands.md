## **🔍 Why Networking Knowledge Matters in DevOps?**
- Debug connectivity issues
- Configure cloud infrastructure
- Secure applications
- Monitor traffic
- Optimize performance

---

## **📡 Basic Connectivity Commands**

### **1. Check IP Address**
```bash
ip a       # Show all interfaces
ifconfig   # Older alternative (deprecated on some systems)
```

### **2. Test Network Connectivity**
```bash
ping google.com          # Basic ping test
ping -c 4 8.8.8.8       # Ping 4 times to Google DNS
```

### **3. Trace Network Path**
```bash
traceroute google.com    # Show route path
tracepath google.com     # Alternative
mtr google.com           # Real-time traceroute + ping
```

---

## **🔌 Port and Socket Management**

### **1. Check Open Ports**
```bash
ss -tulnp               # Modern replacement for netstat
netstat -tulnp          # Show listening ports (older)
lsof -i :80             # Find processes using port 80
```

### **2. Test Port Connectivity**
```bash
telnet example.com 80    # Basic port test
nc -zv example.com 443  # Netcat port test
curl -I http://example.com # HTTP header check
```

---

## **📊 Network Performance**

### **1. Check Bandwidth Usage**
```bash
nload                   # Real-time bandwidth monitor
iftop                   # Show bandwidth by connection
vnstat -l               # Interface traffic statistics
```

### **2. Measure Download Speed**
```bash
curl -o /dev/null http://speedtest.example.com/test.bin
wget -O /dev/null http://speedtest.example.com/test.bin
```

---

## **🛡️ Network Security**

### **1. Firewall Management (UFW)**
```bash
sudo ufw status          # Check firewall status
sudo ufw allow 22/tcp    # Allow SSH
sudo ufw enable          # Enable firewall
```

### **2. Check SSL Certificate**
```bash
openssl s_client -connect example.com:443 | openssl x509 -noout -text
```

### **3. Scan Network (Nmap)**
```bash
nmap -sV example.com    # Service version detection
nmap -p 1-1000 192.168.1.1  # Port range scan
```

---

## **☁️ Cloud-Specific Networking**

### **1. AWS CLI Networking**
```bash
aws ec2 describe-security-groups
aws ec2 describe-subnets
```

### **2. Check Route Tables**
```bash
ip route show           # Local routing table
route -n                # Alternative
```

### **3. DNS Troubleshooting**
```bash
dig example.com         # Detailed DNS lookup
nslookup example.com    # Basic DNS query
host example.com        # Simple DNS check
```

---

## **🔧 Advanced DevOps Networking**

### **1. Persistent Connections**
```bash
ssh -NfL 8080:localhost:80 user@gateway  # Local port forwarding
ssh -NfR 9000:localhost:3000 user@gateway # Remote port forwarding
```

### **2. Network Namespaces (Container Networking)**
```bash
ip netns list           # List network namespaces
ip netns exec ns1 ping 8.8.8.8  # Execute command in namespace
```

### **3. TCP Dump (Packet Capture)**
```bash
sudo tcpdump -i eth0 port 80 -w capture.pcap  # Capture HTTP traffic
sudo tcpdump -i any 'port 5432'  # Monitor PostgreSQL traffic
```

---

## **📚 Networking Cheat Sheet**

| Task | Command |
|------|---------|
| Check IP | `ip a` |
| Test connection | `ping -c 4 8.8.8.8` |
| Check open ports | `ss -tulnp` |
| Test HTTP | `curl -I http://example.com` |
| Monitor traffic | `sudo iftop -i eth0` |
| DNS check | `dig +short example.com` |
| Route tracing | `mtr google.com` |
| Firewall | `sudo ufw status` |

---

## **🚀 Pro Tips**
1. **Always use `ss` instead of `netstat`** (faster, more reliable)
2. **Learn CIDR notation** for cloud security groups (e.g., `10.0.0.0/16`)
3. **Master `tcpdump`** for debugging microservices
4. **Understand OSI model** (especially Layers 4 and 7)
5. **Bookmark these commands** - you'll use them daily!

🐧 **Happy Networking!** 🌐
