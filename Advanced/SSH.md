
### *Secure Shell (SSH) *

---

## **🔐 Why SSH Matters in DevOps?**
- Secure remote server access
- Automated deployments (CI/CD pipelines)
- Server-to-server communication
- File transfers (SCP/SFTP)
- Port forwarding & tunneling

---

## **🛠️ Basic SSH Setup**

### **1. Install SSH (Ubuntu/Debian)**
```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable --now ssh
```

### **2. Check SSH Status**
```bash
sudo systemctl status ssh  # Should show "active (running)"
```

---

## **🔑 SSH Key Authentication (More Secure Than Passwords)**

### **1. Generate SSH Key Pair (On Your Local Machine)**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
# -OR- for older systems:
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
*Files created:*
- `~/.ssh/id_ed25519` (Private key - **NEVER SHARE**)
- `~/.ssh/id_ed25519.pub` (Public key)

### **2. Copy Public Key to Server**
```bash
ssh-copy-id username@server_ip
# -OR- manually:
cat ~/.ssh/id_ed25519.pub | ssh username@server_ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

### **3. Test Key-Based Login**
```bash
ssh username@server_ip  # Should login without password
```

---

## **🚀 Advanced SSH Configurations**

### **1. SSH Config File (Local Machine)**
Edit `~/.ssh/config` for easy access:
```bash
Host myserver
    HostName server_ip_or_domain
    User username
    Port 22
    IdentityFile ~/.ssh/id_ed25519
```
Now just use: `ssh myserver`

### **2. Disable Password Authentication (After Setting Up Keys)**
Edit `/etc/ssh/sshd_config` on server:
```bash
PasswordAuthentication no
ChallengeResponseAuthentication no
```
Then restart SSH:
```bash
sudo systemctl restart ssh
```

---

## **🔄 Server-to-Server SSH (For Automation)**

### **1. Generate Key Pair on Server**
```bash
ssh-keygen -t ed25519
```

### **2. Copy Key Between Servers**
```bash
ssh-copy-id user@other_server
```

### **3. Test Connection**
```bash
ssh user@other_server
```

---

## **🔧 Common SSH Commands for DevOps**

| Command | Description |
|---------|-------------|
| `ssh user@host` | Basic SSH connection |
| `ssh -p 2222 user@host` | Connect to non-standard port |
| `scp file.txt user@host:/path` | Secure file copy |
| `rsync -avz -e ssh /local user@host:/remote` | Sync files over SSH |
| `ssh -L 8080:localhost:80 user@host` | Local port forwarding |
| `ssh -R 8080:localhost:80 user@host` | Remote port forwarding |
| `ssh -D 1080 user@host` | SOCKS proxy |

---

## **🛡️ SSH Security Best Practices**

1. **Change Default SSH Port** (Edit `Port 2222` in `/etc/ssh/sshd_config`)
2. **Use Fail2Ban** to block brute force attacks:
   ```bash
   sudo apt install fail2ban
   ```
3. **Disable Root Login**:
   ```bash
   PermitRootLogin no
   ```
4. **Use SSH Agent Forwarding Carefully** (Only when needed)
5. **Regularly Rotate Keys** (At least every 6 months)

---

## **🚨 Troubleshooting SSH Issues**

1. **Permission Denied?**
   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```
2. **Connection Refused?**
   ```bash
   sudo ufw allow ssh  # Open firewall
   ```
3. **Check SSH Logs**:
   ```bash
   sudo tail -f /var/log/auth.log
   ```

---

## **📚 Recommended Resources**
🔗 [OpenSSH Manual](https://www.openssh.com/manual.html)  
🔗 [SSH Essentials eBook](https://www.digitalocean.com/community/books/ssh-essentials)
