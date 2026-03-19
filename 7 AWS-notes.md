# 🚀 AWS EFS with EC2 — Practical Guide 

### 📌 Goal

Connect **multiple EC2 instances** to a **shared storage (EFS)** and verify data sharing.

---

# 🟢 Phase 1: Infrastructure Setup

## 🔹 Step 1: Launch EC2 Instances

* Login to Amazon Web Services
* Go to **EC2 Dashboard**
* Launch **2 Linux instances**

### Important:

* Choose **Ubuntu / Amazon Linux AMI**
* Place instances in **different Availability Zones**

  * Example: `ap-south-1a` and `ap-south-1b`

👉 This ensures high availability (real-world concept)

---

# 🟡 Phase 2: Create EFS (Elastic File System)

## 🔹 Step 2: Create File System

* Search **EFS** in AWS
* Click **Create File System**
* Give name: `shared-efs`

### Configuration:

* VPC → Default VPC
* Storage Type → **Regional (Important)**
* Enable only required AZs (same as EC2)

---

## 🔹 Step 3: Security Group Setup (VERY IMPORTANT)

Make sure:

* Port **2049 (NFS)** is allowed
* Source → EC2 Security Group

👉 Without this, mounting will fail ❌

---

# 🔵 Phase 3: Prepare EC2 Instances

## 🔹 Step 4: Connect to Instances (SSH)

Connect using:

```bash
ssh -i key.pem ubuntu@<public-ip>
```

---

## 🔹 Step 5: Install Required Packages

### For Ubuntu:

```bash
sudo apt update -y
sudo apt install nfs-common -y
```

### For Amazon Linux:

```bash
sudo yum install nfs-utils -y
```

---

# 🟣 Phase 4: Mount EFS

## 🔹 Step 6: Create Mount Directory

Run on **both instances**:

```bash
sudo mkdir /efs
```

---

## 🔹 Step 7: Mount the EFS

* Go to EFS → **Attach**
* Copy mount command

Example:

```bash
sudo mount -t nfs4 -o nfsvers=4.1 <EFS-DNS>:/ /efs
```

👉 Use correct **AZ-specific endpoint** if needed

---

# 🟥 Phase 5: Verification (Important)

## 🔹 Step 8: Test on Instance 1

```bash
cd /efs
sudo touch file{1..5}
ls
```

---

## 🔹 Step 9: Check on Instance 2

```bash
cd /efs
ls
```

✅ If files appear → **EFS is working correctly**

---

# ⚙️ Phase 6: Auto-Mount (Production Setup)

To mount automatically after reboot:

```bash
sudo nano /etc/fstab
```

Add:

```text
<EFS-DNS>:/ /efs nfs4 defaults,_netdev 0 0
```

Then run:

```bash
sudo mount -a
```

---

# 💡 Real DevOps Use Case

* Shared storage for:

  * Multiple app servers
  * CI/CD pipelines
  * Logs and uploads

Example:

* Web server 1 uploads file
* Web server 2 instantly accesses same file

---

# ⚠️ Common Mistakes (Very Important)

* ❌ Forgot port 2049 in security group
* ❌ Wrong AZ mount target
* ❌ Missing `nfs-common` package
* ❌ Wrong mount path

---

# 🎯 Interview Quick Points

* EFS = **Managed NFS storage**
* Supports **multi-AZ access**
* Used for **shared file systems**
* Works with **EC2 instances**

---

