## **🌐 What is NGINX?**  
**NGINX** (pronounced "engine-x") is a **web server** and **reverse proxy** that helps:  
✔ Host websites & web apps  
✔ Load balance traffic  
✔ Cache content for speed  
✔ Secure applications with SSL  

---

## **🚀 How to Install NGINX**  

### **1. Install NGINX (Ubuntu/Debian)**
```bash
sudo apt update
sudo apt install nginx -y
```

### **2. Start & Enable NGINX**
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### **3. Check Status**
```bash
sudo systemctl status nginx  # Should show "active (running)"
```

### **4. Verify NGINX is Working**  
Open browser → Visit:  
👉 **`http://<your-server-ip>`**  
You should see the **"Welcome to NGINX"** page!  

---

## **📂 NGINX File Structure**  

| **Path** | **Purpose** |
|----------|------------|
| `/etc/nginx/` | Main config directory |
| `/etc/nginx/nginx.conf` | Global NGINX config |
| `/etc/nginx/sites-available/` | Stores website configs |
| `/etc/nginx/sites-enabled/` | Active websites (symlinks) |
| `/var/www/html/` | Default web files location |
| `/var/log/nginx/` | Logs (`access.log`, `error.log`) |

---

## **⚙️ Setting Up a Simple Website**  

### **1. Create Website Directory**
```bash
sudo mkdir -p /var/www/myapp
sudo chown -R $USER:$USER /var/www/myapp
```

### **2. Create a Test HTML Page**
```bash
echo "<h1>Hello from MyApp! 🚀</h1>" > /var/www/myapp/index.html
```

### **3. Create NGINX Config**  
Edit a new config file:  
```bash
sudo nano /etc/nginx/sites-available/myapp
```  

Paste this (**replace `your_domain_or_ip`**):  
```nginx
server {
    listen 80;
    server_name your_domain_or_ip;

    root /var/www/myapp;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

### **4. Enable the Site**
```bash
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
sudo nginx -t  # Test config
sudo systemctl restart nginx
```

### **5. Visit Your Website!**  
Open browser → **`http://<your-server-ip>`**  
You should see **"Hello from MyApp! 🚀"**  

---

## **🔧 Key NGINX Commands**  

| **Command** | **Description** |
|------------|----------------|
| `sudo systemctl start nginx` | Start NGINX |
| `sudo systemctl stop nginx` | Stop NGINX |
| `sudo systemctl restart nginx` | Restart NGINX |
| `sudo nginx -t` | Test config file |
| `sudo tail -f /var/log/nginx/error.log` | Check errors |

---

## **📜 NGINX Configuration Basics**  

### **1. Basic Server Block (Virtual Host)**
```nginx
server {
    listen 80;
    server_name example.com;

    root /var/www/example;
    index index.html;
}
```

### **2. Reverse Proxy (For Node.js, Python Apps)**
```nginx
server {
    listen 80;
    server_name api.example.com;

    location / {
        proxy_pass http://localhost:3000;  # Your app runs here
        proxy_set_header Host $host;
    }
}
```

### **3. Load Balancing**
```nginx
upstream backend {
    server 10.0.0.1;
    server 10.0.0.2;
}

server {
    listen 80;
    server_name app.example.com;

    location / {
        proxy_pass http://backend;
    }
}
```

---

## **📊 NGINX Architecture (Diagram)**  

```
          🌐 Internet
            │
            ▼
      ┌───────────┐
      │ NGINX     │  ← Reverse Proxy / Load Balancer
      └───────────┘
            │
   ┌───────┴───────┐
   ▼               ▼
┌─────┐         ┌─────┐
│App 1│         │App 2│  ← Your Applications
└─────┘         └─────┘
```


## **📚 Free Resources**  
🔗 [NGINX Official Docs](https://nginx.org/en/docs/)  
🔗 [DigitalOcean NGINX Guide](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)  

🐧 **Happy Hosting!** 🚀
