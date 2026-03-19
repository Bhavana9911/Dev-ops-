# 💾 AWS EBS — Partitions, Mounting & Snapshot Automation 

---

# 📌 Objective

Learn how to:

* Create partitions in Linux
* Mount EBS volume (temporary + permanent)
* Take backups using snapshots
* Automate backups using policies

---

# 🧩 1️⃣ Linux Disk Partitioning

## 🔹 What is a Partition?

A partition is a **logical division of a disk**.

### Example:

```
Disk → /dev/xvdf  
Partition → /dev/xvdf1
```

### Why partitions?

* Better organization
* Separate application data
* Easier management & security

---

## 🔹 Check Available Disks

```bash
lsblk
```

👉 Shows all disks and partitions attached to the system

---

## 🔹 Create Partition

```bash
sudo fdisk /dev/xvdf
```

Inside fdisk:

```
n → create new partition  
p → primary partition  
w → save changes  
```

Verify:

```bash
lsblk
```

---

# 📌 2️⃣ Mounting EBS Volume

## 🔹 Temporary vs Permanent Mount

| Type      | Behavior               |
| --------- | ---------------------- |
| Temporary | Lost after reboot      |
| Permanent | Auto mounts on startup |

---

## 🔹 Format the Partition

```bash
sudo mkfs.ext4 /dev/xvdf1
```

---

## 🔹 Create Mount Directory

```bash
sudo mkdir /data
```

---

## 🔹 Mount Volume (Temporary)

```bash
sudo mount /dev/xvdf1 /data
```

Check:

```bash
df -h
```

---

## 🔹 Permanent Mount using fstab

Edit file:

```bash
sudo nano /etc/fstab
```

Add:

```
/dev/xvdf1  /data  ext4  defaults,nofail  0  2
```

Apply:

```bash
sudo mount -a
```

---

# 📸 3️⃣ EBS Snapshot (Backup)

## 🔹 What is Snapshot?

A snapshot is a **backup of an EBS volume**, stored by Amazon Web Services.

### Why use snapshots?

* Point-in-time backup
* Disaster recovery
* Easy rollback

---

## 🔹 Manual Snapshot Creation

Steps:

1. Go to EC2 → Volumes
2. Select volume
3. Click **Actions → Create Snapshot**
4. Add description and create

---

## 🔹 Real DevOps Use Case

Before deployment:

```
Take Snapshot → Deploy Changes → Rollback if needed
```

---

# ⚙️ 4️⃣ Automating Snapshots

## 🔹 What is Snapshot Policy?

AWS provides automation using **Data Lifecycle Manager (DLM)**.

👉 Automatically creates and deletes snapshots

---

## 🔹 Example Policy

* Backup: Daily
* Time: 2 AM
* Retention: 7 days

---

## 🔹 Steps to Create Policy

1. Go to EC2 → Lifecycle Manager
2. Click **Create Lifecycle Policy**
3. Select:

   * Resource → EBS Volume
   * Schedule → Daily
   * Retention → 7 snapshots
4. Apply using **tags**

---

## 🔹 Automation Flow

```
Tagged Volume  
     ↓  
Lifecycle Policy  
     ↓  
Automatic Snapshots
```

---

# 🧠 DevOps Best Practices

* Use **UUID instead of device name** in fstab
* Always test using:

  ```bash
  sudo mount -a
  ```
* Take snapshot before:

  * Resizing volume
  * Major deployments
* Use tags for automation
* Never rely on manual backups

---

# 💼 🎯 Interview Preparation

## ✅ Basic Questions

* What is a partition?
* What does `lsblk` do?
* What is fstab?
* What is EBS snapshot?
* Why backups are important?

---

## ⚙️ Intermediate Questions

* Difference between temporary and permanent mount
* Snapshot vs AMI
* What is lifecycle policy?
* Why use UUID in fstab?

---

## 🚀 Scenario-Based Questions

* Volume not mounted after reboot
  👉 Missing fstab entry

* Need automatic backups
  👉 Use lifecycle policy

* Deployment failed
  👉 Restore from snapshot

---


