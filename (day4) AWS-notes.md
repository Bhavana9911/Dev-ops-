# 🔐 SSH Authentication, User Management & NGINX Deployment --- DevOps Practical Guide
------------------------------------------------------------------------

# 📑 Table of Contents

-   SSH Service (Key-Based Authentication)
-   Practical: Create Another Login User
-   Deploy Web Server using NGINX
-   DevOps Best Practices
-   Interview Preparation

------------------------------------------------------------------------

# 🔑 1️⃣ SSH Service --- Key Based Authentication

![SSH Key Authentication
Architecture](images/ssh-key-authentication.png)

## 🔹 What is SSH?

SSH (Secure Shell) is used to remotely access Linux servers securely.

Instead of passwords, AWS recommends **Key-Based Authentication**.

### Why Key-Based Authentication?

✔ More secure than passwords\
✔ Prevents brute force attacks\
✔ Industry DevOps standard

------------------------------------------------------------------------

## 🔹 How SSH Key Authentication Works

    Local Machine (Private Key)
              ↓
          Encrypted Login
              ↓
    EC2 Instance (Public Key stored)

-   `.pem` file = Private Key (Keep Secret)
-   Public key stored inside `~/.ssh/authorized_keys`

------------------------------------------------------------------------

## 🔹 Connect Using SSH

``` bash
chmod 400 mykey.pem
ssh -i mykey.pem ubuntu@<Public-IP>
```

Default Users:

-   Ubuntu → ubuntu
-   Amazon Linux → ec2-user

------------------------------------------------------------------------

# 👤 2️⃣ Practical --- Create Another Login User

![Linux User Creation Diagram](images/linux-user-management.png)

## 🔹 Why Create New Users?

DevOps teams avoid using default users.

Reasons:

-   Security
-   Access control
-   Team collaboration

------------------------------------------------------------------------

## 🔹 Step 1 --- Create User

``` bash
sudo adduser devopsuser
```

System will ask for password and details.

------------------------------------------------------------------------

## 🔹 Step 2 --- Grant Sudo Access

``` bash
sudo usermod -aG sudo devopsuser
```

Now the user has admin privileges.

------------------------------------------------------------------------

## 🔹 Step 3 --- Setup SSH Access for New User

Create SSH directory:

``` bash
sudo mkdir /home/devopsuser/.ssh
```

Copy authorized keys:

``` bash
sudo cp ~/.ssh/authorized_keys /home/devopsuser/.ssh/
```

Set permissions:

``` bash
sudo chown -R devopsuser:devopsuser /home/devopsuser/.ssh
sudo chmod 700 /home/devopsuser/.ssh
sudo chmod 600 /home/devopsuser/.ssh/authorized_keys
```

------------------------------------------------------------------------

## 🔹 Step 4 --- Login with New User

``` bash
ssh -i mykey.pem devopsuser@<Public-IP>
```

------------------------------------------------------------------------

# 🌐 3️⃣ Deploy Web Server using NGINX

![NGINX Deployment Architecture](images/nginx-deployment.png)

## 🔹 What is NGINX?

NGINX is a high-performance web server used for:

-   Hosting websites
-   Reverse proxy
-   Load balancing

------------------------------------------------------------------------

## 🔹 Install NGINX

``` bash
sudo apt update -y
sudo apt install nginx -y
```

------------------------------------------------------------------------

## 🔹 Start and Enable Service

``` bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

Check status:

``` bash
sudo systemctl status nginx
```

------------------------------------------------------------------------

## 🔹 Allow HTTP Traffic in Security Group

Add Rule:

    Port: 80
    Type: HTTP
    Source: 0.0.0.0/0 (for demo)

------------------------------------------------------------------------

## 🔹 Verify Web Server

Open browser:

    http://<Public-IP>

You should see:

    Welcome to nginx!

------------------------------------------------------------------------

## 🔹 Deploy Custom Web Page

``` bash
sudo nano /var/www/html/index.html
```

Example HTML:

``` html
<h1>DevOps NGINX Deployment Successful 🚀</h1>
```

Save and refresh browser.

------------------------------------------------------------------------

# 🧠 DevOps Best Practices

    ✔ Disable password authentication
    ✔ Use IAM roles where possible
    ✔ Restrict SSH to My IP
    ✔ Rotate SSH keys regularly
    ✔ Monitor with CloudWatch

------------------------------------------------------------------------




