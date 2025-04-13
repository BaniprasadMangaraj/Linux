## **🔍 Why This Matters for DevOps?**
- Secure server access for team members
- Control file permissions for deployments
- Isolate processes (Docker, CI/CD)
- Manage service accounts

---

## **🛠️ User Management Basics**

### **1. Add a New User**
```bash
sudo useradd -m devuser  # -m creates home directory
sudo passwd devuser      # Set password
```

### **2. Modify a User**
```bash
sudo usermod -aG sudo devuser  # Add to sudo group
sudo usermod -s /bin/bash devuser  # Change shell
```

### **3. Delete a User**
```bash
sudo userdel -r devuser  # -r removes home dir
```

---

## **👥 Group Management**

### **1. Create a Group**
```bash
sudo groupadd devops-team
```

### **2. Add User to Group**
```bash
sudo usermod -aG devops-team devuser
```

### **3. Verify Group Membership**
```bash
groups devuser  # Shows all groups user belongs to
```

---

## **🔐 Permission Management**

### **1. Change File Owner**
```bash
sudo chown devuser:devops-team /opt/app
```

### **2. Change Permissions**
```bash
chmod 750 /opt/app  # Owner:rwx, Group:r-x, Others:---
```

### **3. Set Default Permissions (umask)**
```bash
umask 0027  # New files get 640, dirs get 750
```

---

## **💼 DevOps-Specific Use Cases**

### **1. Service Accounts (for CI/CD)**
```bash
sudo useradd -r -s /usr/sbin/nologin ci-bot
```

### **2. Docker Group (Avoid Sudo)**
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

### **3. SSH Key-Based Access**
```bash
sudo mkdir /home/devuser/.ssh
sudo cp id_rsa.pub /home/devuser/.ssh/authorized_keys
sudo chown -R devuser:devuser /home/devuser/.ssh
sudo chmod 700 /home/devuser/.ssh
sudo chmod 600 /home/devuser/.ssh/authorized_keys
```

---

## **📋 User/Group Info Files**

| File | Purpose | Example |
|------|---------|---------|
| `/etc/passwd` | User accounts | `devuser:x:1001:1001::/home/devuser:/bin/bash` |
| `/etc/group` | Group definitions | `devops-team:x:1002:devuser` |
| `/etc/shadow` | Encrypted passwords | `devuser:$6$...:19182:0:99999:7:::` |
| `/etc/sudoers` | Sudo permissions | `devuser ALL=(ALL) NOPASSWD: ALL` |

---

## **🚀 Pro Tips for DevOps**

1. **Least Privilege Principle**: Only give necessary permissions
2. **Use Groups**: Manage permissions via groups, not individual users
3. **Service Accounts**: Always create dedicated users for services
4. **Audit Regularly**: `sudo lastlog` to check user access
5. **SSH Restrictions**: `AllowGroups ssh-users` in `/etc/ssh/sshd_config`

---

## **📚 Learning Resources**
🔗 [Linux Documentation Project](https://tldp.org/LDP/lame/LAME/linux-admin-made-easy/user-account-management.html)  
🔗 [DigitalOcean User Management](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-ubuntu-20-04)

🐧 **Practice these commands on a test server before production!**
