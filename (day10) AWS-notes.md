# 📂 NFS & Amazon EFS — DevOps Practical Guide

> Beginner → Advanced | Hands-on + Interview Ready
> Ideal for GitHub portfolio and real-world understanding

---

# 📚 1️⃣ NFS (Network File System) — Basics

## 🔹 What is NFS?

NFS allows one machine to **share its directory over a network**, so other machines can access it like local storage.

👉 Works using **client–server model**

---

## 🔹 How It Works

* Server → shares directory
* Client → mounts it
* Communication → happens over network (TCP)
* 
```
NFS Server (/data)
        ↓  (Port 2049)
NFS Client (/mnt)
```

---

## 🔹 Key Points

* Protocol: NFS
* Default Port: **2049**
* Versions:

  * NFSv3 → basic
  * NFSv4 → secure + better

---

## 🔹 Real DevOps Use Cases

* Shared uploads (web apps)
* Central logs storage
* Dev/Test shared environment
* Config file sharing

---

## 🔹 Limitations (Important for Interviews)

* Depends on network
* Can be slow (latency)
* Not suitable for heavy databases

---

## 🔐 Security Tips

* Restrict access by IP
* Use firewall rules
* Prefer NFSv4
* Encrypt traffic if possible

---

# ☁️ 2️⃣ Amazon EFS (Managed NFS)

## 🔹 What is EFS?

Amazon Web Services EFS is a **managed file storage service** based on NFS.

👉 No server setup required
👉 Auto scaling storage

---

## 🔹 Key Features

* Works with Linux systems
* Multi-AZ access
* Fully managed
* Scales automatically

---

## 🔹 How It Works

* EFS is regional
* Mount targets created in each AZ
* EC2 connects via NFS

---

## 🔹 Performance Modes

| Mode            | Use Case                  |
| --------------- | ------------------------- |
| General Purpose | Low latency apps          |
| Max I/O         | High throughput workloads |

---

## 🔹 Throughput Modes

* Bursting → based on size
* Provisioned → fixed
* Elastic → auto scaling

---

## 🔐 Security in EFS

* Security Groups (port 2049)
* IAM permissions
* Encryption (KMS)
* TLS (in transit)

---

# ⚙️ 3️⃣ Hands-On Practical (Important Section)

---

## 🔹 Step 1: Launch EC2

* Launch 2 EC2 instances
* Same VPC
* Different AZ (recommended)

---

## 🔹 Step 2: Create EFS

* Go to EFS → Create
* Select VPC
* Create mount targets

---

## 🔹 Step 3: Security Group

Allow:

```id="5ikd5a"
Port: 2049 (NFS)
Source: EC2 Security Group
```

---

## 🔹 Step 4: Install NFS Tools

### Amazon Linux:

```bash id="qdy9xk"
sudo yum install -y amazon-efs-utils
```

### Ubuntu:

```bash id="btce5c"
sudo apt install -y nfs-common
```

---

## 🔹 Step 5: Mount EFS

```bash id="f6g4kq"
sudo mkdir /mnt/efs
sudo mount -t nfs4 fs-xxxx:/ /mnt/efs
```

---

## 🔹 Step 6: Auto-Mount

```bash id="4ys3l1"
sudo nano /etc/fstab
```

Add:

```id="ldrmz6"
fs-xxxx:/ /mnt/efs nfs4 defaults,_netdev 0 0
```

---

## 🔹 Step 7: Testing

Instance 1:

```bash id="l0tnpf"
echo "Hello from server1" > /mnt/efs/test.txt
```

Instance 2:

```bash id="h7a27q"
cat /mnt/efs/test.txt
```

✅ If visible → working correctly

---

# 🛠 Troubleshooting

| Issue            | Fix                          |
| ---------------- | ---------------------------- |
| Mount timeout    | Check port 2049              |
| Permission error | Check IAM / file permissions |
| Slow speed       | Check throughput mode        |

---

# 🚀 4️⃣ Real DevOps Use Cases

* WordPress (shared uploads)
* Jenkins shared workspace
* Kubernetes (EKS persistent storage)
* Centralized logging

---

# 🏆 5️⃣ Best Practices (Important for Interviews)

* Create mount targets in all AZs
* Enable lifecycle policy
* Use encryption
* Monitor using CloudWatch
* Avoid hardcoding values

---

# 🎯 6️⃣ Interview Quick Revision

## 🔹 Must-Know Points

* EFS uses **NFS (v4.1)**
* Supports **multi-instance access**
* Works across **multiple AZs**

---

## 🔹 Common Questions

* EFS vs EBS
* Why EFS for auto scaling apps?
* Why not use EFS for databases?

---

## 🔹 Smart Answer Structure

👉 Definition → Architecture → Use Case → Limitation

Example:

> "EFS is a managed file storage service that allows multiple EC2 instances to share data across AZs. It is useful for scalable web apps but not ideal for high-performance databases."

---
