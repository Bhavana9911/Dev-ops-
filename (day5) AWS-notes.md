# 🚀 AWS EC2 Deep Dive --- Dashboard, Instance Types, AMI, Status Checks & Launch Templates
------------------------------------------------------------------------

# 📑 Table of Contents

-   Complete EC2 Dashboard Overview
-   Instance Types Explained
-   Status Checks & AMI (Types, Create, Copy)
-   Launch Templates
-   EC2 Purchasing Options
-   DevOps Architecture Notes
-   Interview Preparation

------------------------------------------------------------------------

# 🧭 1️⃣ Complete Dashboard of EC2

![EC2 Dashboard Overview](images/ec2-dashboard-overview.png)

## 🔹 What is EC2 Dashboard?

The EC2 Dashboard is the central control panel to manage virtual
machines in AWS.

You can:

-   Launch instances
-   Monitor health
-   Manage networking
-   Configure storage

------------------------------------------------------------------------

## 🔹 Main Sections in EC2 Dashboard

### 🖥️ Instances

View running or stopped servers.

### 🧾 AMIs

Templates used to launch instances.

### 💽 Volumes

EBS storage attached to instances.

### 🌐 Security Groups

Firewall rules for instances.

### 🔑 Key Pairs

Used for SSH/RDP authentication.

### ⚡ Elastic IP

Static public IP address.

------------------------------------------------------------------------

## 🔹 Real DevOps Usage

DevOps engineers use EC2 Dashboard to:

-   Deploy applications
-   Create staging environments
-   Monitor infrastructure health

------------------------------------------------------------------------

# ⚙️ 2️⃣ Instance Types Explained

![EC2 Instance Types Architecture](images/ec2-instance-types.png)

Instance types define hardware resources like CPU, RAM, and network
speed.

------------------------------------------------------------------------

## 🔹 Instance Families

  Family              Purpose             Example
  ------------------- ------------------- ---------
  General Purpose     Balanced workload   t3, t2
  Compute Optimized   High CPU apps       c5
  Memory Optimized    Databases           r5
  Storage Optimized   Big data            i3
  GPU Instances       AI/ML workloads     p3

------------------------------------------------------------------------

## 🔹 Real-Time Use Cases

-   t2.micro → Learning & Free Tier
-   c5.large → CI/CD build servers
-   r5.large → Database servers

------------------------------------------------------------------------

# 🩺 3️⃣ Status Check & AMI (Types, Create, Copy)

![EC2 Status Check Diagram](images/ec2-status-checks.png)

## 🔹 EC2 Status Checks

AWS performs automatic health checks.

### Types of Status Checks

  Check Type              Meaning
  ----------------------- ---------------------------
  System Status Check     AWS hardware issue
  Instance Status Check   OS or configuration issue

When you see:

    2/2 Status Checks Passed

👉 Instance is healthy.

------------------------------------------------------------------------

## 🔹 What is AMI?

AMI (Amazon Machine Image) is a template containing:

-   Operating system
-   Software configuration
-   Security settings

------------------------------------------------------------------------

## 🔹 Types of AMI

  Type              Description
  ----------------- -----------------
  Public AMI        Shared by AWS
  Private AMI       Created by user
  Marketplace AMI   Paid images

------------------------------------------------------------------------

## 🔹 Create Custom AMI

Steps:

1.  Select Instance
2.  Actions → Image → Create Image
3.  Provide name & description
4.  AWS creates reusable template

------------------------------------------------------------------------

## 🔹 Copy AMI (Cross Region)

Used for:

-   Disaster recovery
-   Multi-region deployment

Process:

    AMI → Actions → Copy AMI → Select Region

------------------------------------------------------------------------

# 🧱 4️⃣ Launch Template

![EC2 Launch Template Architecture](images/ec2-launch-template.png)

## 🔹 What is Launch Template?

Reusable configuration for launching instances.

Includes:

-   AMI
-   Instance Type
-   Security Groups
-   Storage
-   User Data

------------------------------------------------------------------------

## 🔹 Why DevOps Teams Use Launch Templates?

✔ Auto Scaling deployments\
✔ Standardized infrastructure\
✔ Faster provisioning

------------------------------------------------------------------------

## 🔹 Real DevOps Example

    Auto Scaling Group → Launch Template → EC2 Instances

Ensures identical server configuration.

------------------------------------------------------------------------

# 💰 5️⃣ EC2 Purchasing Options

![EC2 Pricing Models](images/ec2-purchasing-options.png)

AWS provides multiple pricing models.

------------------------------------------------------------------------

## 🔹 On-Demand Instances

-   Pay per hour/second
-   No long-term commitment

Best for:

-   Testing
-   Short-term workloads

------------------------------------------------------------------------

## 🔹 Reserved Instances

-   Long-term commitment (1--3 years)
-   Cheaper pricing

Best for:

-   Production systems

------------------------------------------------------------------------

## 🔹 Spot Instances

-   Lowest cost
-   Can terminate anytime

Best for:

-   Batch jobs
-   CI pipelines

------------------------------------------------------------------------

## 🔹 Savings Plans

Flexible pricing with commitment.

------------------------------------------------------------------------

# 🧠 DevOps Architecture Insight

Typical scalable design:

    Load Balancer
          ↓
    Auto Scaling Group
          ↓
    Launch Template
          ↓
    EC2 Instances

Benefits:

✔ Automation\
✔ High Availability\
✔ Consistency

------------------------------------------------------------------------

