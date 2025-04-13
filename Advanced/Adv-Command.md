
## **👥 User Management Deep Dive**

### **1. Create User with Home Directory**
```bash
sudo useradd -m dholu  # Creates user 'dholu' with home folder
```
*Output:* No output on success (verify with `id dholu`)

### **2. Delete User Completely**
```bash
sudo userdel -r dholu  # Removes user and home directory
```
*Output:* No output on success (verify with `id dholu` → "no such user")

---

## **👥 Group Management**

### **1. Create New Group**
```bash
sudo groupadd devops
sudo groupadd tester
```
*Check:* `cat /etc/group | grep -E 'devops|tester'`  
*Output:*  
```
devops:x:1001:
tester:x:1002:
```

### **2. Add Multiple Users to Group**
```bash
sudo gpasswd -M tappu,bhide devops
sudo gpasswd -M ubuntu,babitaji tester
```
*Check:* `cat /etc/group`  
*Output:*  
```
devops:x:1001:tappu,bhide
tester:x:1002:ubuntu,babitaji
```

### **3. Add Single User to Group**
```bash
sudo usermod -aG devops aiyer
```
*Check:* `groups aiyer`  
*Output:*  
```
aiyer : aiyer devops
```

---

## **🔐 File Permissions (DevOps Critical!)**

### **1. Change File Permissions**
```bash
chmod 400 commands.txt  # Owner read-only
chmod 666 demo-file.txt # All read+write
ls -l  # Verify changes
```
*Output:*
```
-r-------- 1 aiyer aiyer  0 Jul 12 15:30 commands.txt
-rw-rw-rw- 1 aiyer aiyer 12 Jul 12 15:31 demo-file.txt
```

### **2. Change File Ownership**
```bash
sudo chown aiyer commands.txt  # Change owner
sudo chgrp aiyer commands.txt  # Change group
ls -l commands.txt
```
*Output:*
```
-r-------- 1 aiyer aiyer 0 Jul 12 15:30 commands.txt
```

---

## **📊 Log Analysis (Essential for DevOps)**

### **1. Basic Grep Filtering**
```bash
grep -i "authentication failure" app.log | head -n 5
```
*Sample Output:*
```
Jul 11 03:45:22 server sshd[1234]: Authentication failure for user root
Jul 11 05:12:33 server sshd[5678]: Authentication failure for invalid user admin
```

### **2. Advanced AWK Filtering**
```bash
awk '/authentication failure/ {print $1,$2,$3,$13,$14,$15}' app.log > auth_failures.txt
```
*Sample Output (auth_failures.txt):*
```
Jul 11 03:45:22 for user root
Jul 11 05:12:33 for invalid user admin
```

### **3. Date-Specific Filtering**
```bash
awk '/authentication failure/ {if ($1=="Jul" && $2=="11") print $13,$14,$15}' app.log
```
*Output:*
```
for user
root from
192.168.1.100
```

---

## **🔧 Key Commands Cheat Sheet**

| Task | Command | Example Output |
|------|---------|----------------|
| Create user | `sudo useradd -m username` | (silent) |
| Delete user | `sudo userdel -r username` | (silent) |
| Create group | `sudo groupadd groupname` | (silent) |
| Add users to group | `sudo gpasswd -M user1,user2 group` | (silent) |
| Check groups | `cat /etc/group` | `groupname:x:1001:user1,user2` |
| Change owner | `sudo chown user:group file` | (silent) |
| Search logs | `grep -i "error" /var/log/syslog` | Error messages |

---

## **💡 Pro DevOps Tips**
1. **Always use `-m` with `useradd`** to create home directories
2. **Prefer `gpasswd -M`** for bulk user additions to groups
3. **Secure permissions**:
   - `400` for config files
   - `750` for scripts
   - `600` for SSH keys
4. **Log analysis patterns**:
   ```bash
   # Count authentication failures
   grep -i "authentication failure" /var/log/auth.log | wc -l
   
   # Extract IPs from logs
   awk '/Failed password/ {print $11}' /var/log/auth.log | sort | uniq -c
   ```

5. **Bookmark these commands** - you'll use them daily in:
   - User management for CI/CD
   - Log analysis for debugging
   - Permission fixing for deployments

🐧 **Master these to become a Linux/DevOps power user!**
