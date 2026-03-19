# 🔐 AWS Security Groups, Windows EC2 & Remote Access Guide
------------------------------------------------------------------------

# 📑 Table of Contents

-   Security Group (SSH & RDP Ports)
-   Create Windows EC2 Instance
-   Remote Access (Linux & Windows)
-   DevOps Best Practices
-   Interview Preparation

------------------------------------------------------------------------

# 🔥 1️⃣ Security Group --- SSH and RDP Ports

![AWS Security Group
Architecture](images/aws-security-group-diagram.png)

## 🔹 What is a Security Group?

A Security Group acts as a **virtual firewall** for EC2 instances.

It controls:

-   Inbound Traffic (Incoming)
-   Outbound Traffic (Outgoing)

Security Groups are **stateful**, meaning responses to allowed traffic
are automatically allowed.

------------------------------------------------------------------------

## 🔹 Common Ports Used in DevOps

  Port   Protocol   Purpose
  ------ ---------- --------------------------
  22     SSH        Remote access to Linux
  3389   RDP        Remote access to Windows
  80     HTTP       Web traffic
  443    HTTPS      Secure web traffic

------------------------------------------------------------------------

## 🔹 SSH Rule Example

    Type: SSH
    Port: 22
    Source: My IP (Recommended)

✔ Used for Ubuntu / Amazon Linux instances.

------------------------------------------------------------------------

## 🔹 RDP Rule Example

    Type: RDP
    Port: 3389
    Source: My IP (Recommended)

✔ Used for Windows Server instances.

⚠️ Never allow 0.0.0.0/0 in production for SSH or RDP.

------------------------------------------------------------------------

# 🪟 2️⃣ Create Instance of Windows

![Windows EC2 Launch](images/aws-windows-ec2-launch.png)

## 🔹 Step-by-Step

### Step 1 --- Open EC2 Console

AWS Console → EC2 → Launch Instance

------------------------------------------------------------------------

### Step 2 --- Name Instance

    windows-devops-server

------------------------------------------------------------------------

### Step 3 --- Choose AMI

Select:

👉 Windows Server 2019 / 2022 Base

------------------------------------------------------------------------

### Step 4 --- Choose Instance Type

    t3.micro or t2.micro

------------------------------------------------------------------------

### Step 5 --- Create Key Pair

    Key Name: windows-key
    Format: .pem

AWS uses this key to decrypt Windows password.

------------------------------------------------------------------------

### Step 6 --- Configure Security Group

Allow:

-   RDP (3389)
-   HTTP (Optional)
-   HTTPS (Optional)

------------------------------------------------------------------------

### Step 7 --- Launch Instance

Wait until:

    Running
    2/2 Status Checks Passed

------------------------------------------------------------------------

# 💻 3️⃣ Remote Access of Linux and Windows Machines

![Remote Access Architecture](images/aws-remote-access-diagram.png)

------------------------------------------------------------------------

## 🐧 Remote Access to Linux (SSH)

### Requirements

-   Public IP
-   Key Pair (.pem)
-   Port 22 Open

### Command

``` bash
chmod 400 mykey.pem
ssh -i mykey.pem ubuntu@<Public-IP>
```

Default Users:

-   Ubuntu AMI → ubuntu
-   Amazon Linux → ec2-user

------------------------------------------------------------------------

## 🪟 Remote Access to Windows (RDP)

### Steps

1.  Go to EC2 → Connect
2.  Select **RDP Client**
3.  Download RDP File
4.  Get Password using Key Pair

------------------------------------------------------------------------

### Windows Login Process

    Public IP → Open Remote Desktop → Enter Username & Password

Default Username:

    Administrator

------------------------------------------------------------------------

## 🔹 DevOps Real-Time Use Case

### Linux EC2

-   Deploy Docker containers
-   Run Jenkins agents
-   Host Nginx web servers

### Windows EC2

-   .NET application hosting
-   IIS web server deployment
-   Active Directory testing

------------------------------------------------------------------------

# 🧠 DevOps Security Best Practices

    ✔ Restrict SSH/RDP to My IP
    ✔ Use IAM roles instead of access keys
    ✔ Rotate key pairs regularly
    ✔ Enable CloudWatch monitoring
    ✔ Disable password login for Linux

------------------------------------------------------------------------

