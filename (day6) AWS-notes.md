# 💽 AWS EBS Volumes --- Types, Attach Volume, Partition & Mount (DevOps Practical Guide)
------------------------------------------------------------------------

# 📑 Table of Contents

-   Introduction to EBS Volumes
-   EBS Volume Types
-   Attach Volume to EC2
-   Create Partition
-   Format and Mount Volume
-   Auto Mount using fstab
-   DevOps Best Practices
-   Interview Preparation

------------------------------------------------------------------------

# 💽 1️⃣ Introduction to EBS Volumes

![AWS EBS Architecture](images/aws-ebs-architecture.png)

## 🔹 What is EBS?

EBS (Elastic Block Store) is persistent block storage used with EC2
instances.

Think of it like:

    Hard Disk of your Cloud Server

Key Features:

✔ Persistent storage\
✔ High availability within AZ\
✔ Detachable & reusable\
✔ Snapshot support

------------------------------------------------------------------------

# 🧱 2️⃣ EBS Volume Types

![EBS Volume Types](images/aws-ebs-types.png)

AWS provides different EBS types based on performance needs.

  Volume Type   Description            Use Case
  ------------- ---------------------- ---------------------
  gp3           General Purpose SSD    Web servers
  gp2           Previous Gen SSD       Legacy workloads
  io1/io2       Provisioned IOPS SSD   High-performance DB
  st1           Throughput HDD         Big data
  sc1           Cold HDD               Archival storage

------------------------------------------------------------------------

## 🔹 Real DevOps Use Cases

-   gp3 → NGINX web servers
-   io2 → Production databases
-   st1 → Log processing pipelines

------------------------------------------------------------------------

# 🔗 3️⃣ Attach Volume to EC2 Instance

![Attach EBS Volume](images/aws-ebs-attach.png)

## 🔹 Steps

1.  Go to EC2 → Volumes
2.  Click **Create Volume**
3.  Select:

```{=html}
<!-- -->
```
    Type: gp3
    Size: 10 GB
    AZ: Same as Instance

4.  Create Volume
5.  Select Volume → Actions → Attach
6.  Choose Instance

Device Example:

    /dev/xvdf

------------------------------------------------------------------------

# 🧩 4️⃣ Create Partition

After attaching volume, login to EC2:

``` bash
lsblk
```

You will see new disk (example: xvdf).

------------------------------------------------------------------------

## 🔹 Create Partition using fdisk

``` bash
sudo fdisk /dev/xvdf
```

Steps inside fdisk:

    n → new partition
    p → primary
    w → write changes

Check partition:

``` bash
lsblk
```

Example output:

    xvdf1

------------------------------------------------------------------------

# 🧾 5️⃣ Format and Mount Volume

## 🔹 Format Disk

``` bash
sudo mkfs.ext4 /dev/xvdf1
```

------------------------------------------------------------------------

## 🔹 Create Mount Directory

``` bash
sudo mkdir /data
```

------------------------------------------------------------------------

## 🔹 Mount Volume

``` bash
sudo mount /dev/xvdf1 /data
```

Verify:

``` bash
df -h
```

------------------------------------------------------------------------

# 🔄 6️⃣ Auto Mount using fstab

To make mount permanent after reboot:

``` bash
sudo nano /etc/fstab
```

Add:

    /dev/xvdf1  /data  ext4  defaults,nofail  0  2

Test configuration:

``` bash
sudo mount -a
```

------------------------------------------------------------------------

# 🧠 DevOps Real-Time Example

Production Architecture:

    EC2 Instance
       ├── Root Volume (OS)
       └── EBS Volume (/data)
            └── Application Logs

Benefits:

✔ Separate storage for logs\
✔ Easy backup using snapshots\
✔ Scalable storage

------------------------------------------------------------------------

# 🔐 DevOps Best Practices

    ✔ Use gp3 instead of gp2
    ✔ Take snapshots before deleting volume
    ✔ Use separate EBS for application data
    ✔ Avoid storing critical data on root volume
    ✔ Monitor IOPS using CloudWatch

------------------------------------------------------------------------


