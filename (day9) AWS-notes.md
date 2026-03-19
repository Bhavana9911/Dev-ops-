# 🌐 Deploy NGINX on EC2 (Ubuntu) — Step-by-Step Guide

## 📌 Objective

Launch an EC2 instance and deploy a basic web server using NGINX.

---

# 🟢 Step 1: Launch EC2 Instance

Go to Amazon Web Services → EC2 → **Launch Instance**

### Configuration:

* **AMI** → Ubuntu Server 24.04 LTS
* **Instance Type** → t2.micro (Free tier)
* **Key Pair** → Download `.pem` file

### 🔐 Security Group (Important)

Allow:

* SSH → Port 22 (your IP)
* HTTP → Port 80 (0.0.0.0/0)

📌 Copy the **Public IP** after launching

---

# 🔵 Step 2: Connect via SSH

```bash
ssh -i ~/Downloads/your-key.pem ubuntu@<PUBLIC-IP>
```

✅ You are now inside your EC2 server

---

# 🟡 Step 3: Update System

```bash
sudo apt update -y
sudo apt upgrade -y
```

👉 Always update before installing anything

---

# 🟠 Step 4: Install NGINX

```bash
sudo apt install nginx -y
```

Enable and start service:

```bash
sudo systemctl enable --now nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

# 🟣 Step 5: Configure Firewall

```bash
sudo ufw allow 'Nginx HTTP'
sudo ufw enable
sudo ufw status
```

👉 Ensures web traffic is allowed

---

# 🔴 Step 6: Verify Installation

### Browser:

```
http://<PUBLIC-IP>
```

✅ You should see **NGINX default page**

---

### Terminal test:

```bash
curl http://localhost
```

---

# 🟤 Step 7: Deploy Your Own Web Page

Edit default file:

```bash
sudo nano /var/www/html/index.html
```

Example content:

```html
<h1>🚀 My NGINX Server is Live</h1>
<p>Deployed on EC2 using Ubuntu</p>
```

---

## 🔄 Apply Changes

```bash
sudo nginx -t
sudo systemctl reload nginx
```

👉 Refresh browser to see changes

---

# ⚙️ Useful NGINX Commands

| Action      | Command                        |
| ----------- | ------------------------------ |
| Start       | `sudo systemctl start nginx`   |
| Stop        | `sudo systemctl stop nginx`    |
| Restart     | `sudo systemctl restart nginx` |
| Reload      | `sudo systemctl reload nginx`  |
| Status      | `sudo systemctl status nginx`  |
| Test Config | `sudo nginx -t`                |

---

# 🔍 Logs & Debugging

```bash
sudo tail -f /var/log/nginx/access.log
sudo journalctl -u nginx -f
```

---

# ⚠️ Common Issues

* ❌ Site not loading → Check **Security Group (port 80)**
* ❌ NGINX not running → Restart service
* ❌ Permission issues → Check file ownership

---

# 🚀 Next Step (Optional)

Enable HTTPS using:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

---

# 💡 DevOps Use Case

* Host static websites
* Use as reverse proxy
* Serve frontend applications

---

# 📂 GitHub Structure Suggestion

```bash
aws-projects/
└── nginx-ec2-deployment/
    └── README.md
```

---

# 🎯 Final Note

Now your portfolio has:

* ✅ EFS (shared storage)
* ✅ EBS (storage + backup)
* ✅ NGINX (web server deployment)



