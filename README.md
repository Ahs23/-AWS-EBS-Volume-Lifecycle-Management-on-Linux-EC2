🚀 AWS EBS Volume Lifecycle Management on Linux EC2
📌 Executive Summary

This project demonstrates production-level handling of Amazon Elastic Block Store (EBS) with a Linux-based EC2 instance.
It focuses on manual storage provisioning, Linux disk management, and AWS infrastructure fundamentals, which are essential skills for Cloud Engineers, CloudOps, and DevOps roles.

The implementation mirrors real-world scenarios where applications require separate, scalable, and persistent storage beyond the root volume.

🧠 Problem Statement

By default, EC2 instances launch with a single root EBS volume.
In real production environments, additional storage is required for:

Application data

Logs

Databases

Backups

This project solves that problem by:

Creating an independent EBS volume

Attaching it to a running EC2 instance

Preparing and mounting it using Linux

🧩 Architecture Overview

Compute: Linux EC2 instance

Storage:

Root EBS Volume → 8 GiB (default)

Data EBS Volume → 2 GiB (gp3)

Filesystem: EXT4

Mount Point: /dir1

⚙️ Implementation Workflow
1️⃣ Provision Infrastructure

Launched a Linux EC2 instance

Default root volume automatically attached

2️⃣ Create Independent EBS Volume

Created a gp3 EBS volume

Availability Zone matched with EC2

Volume initially in Available state

3️⃣ Attach Volume to EC2

Attached as /dev/sdb via AWS Console

Linux internally mapped the device as:

/dev/nvme1n1


✔️ Demonstrates understanding of AWS vs Linux device name mapping

4️⃣ Disk Detection & Validation
lsblk


Verified block device availability at OS level.

5️⃣ Filesystem Creation
mkfs.ext4 /dev/nvme1n1


Prepared disk for Linux usage.

6️⃣ Mount Configuration
mkdir /dir1
mount /dev/nvme1n1 /dir1

7️⃣ Verification
df -h


Confirmed successful mount:

/dev/nvme1n1   2.0G   24K   1.8G   1%   /dir1

📊 Outcome

Extra EBS volume successfully attached and mounted

Storage now available independently of root volume

Demonstrates persistent storage architecture

🔐 Key Technical Insights

EBS is network-attached block storage

Filesystem creation is mandatory before mounting

AWS device names ≠ Linux device names

Mounted volumes require /etc/fstab for persistence across reboots

📈 Future Enhancements

Persistent mount using /etc/fstab

EBS snapshot & restore

Online volume resizing

Terraform-based automation

CloudWatch monitoring integration

🎯 Industry Relevance

This project aligns with real-world cloud use cases such as:

Application storage separation

Scalable data volumes

CloudOps infrastructure setup

Production Linux server management

👨‍💻 Author

Arman Shaikh
Aspiring AWS Cloud & Infrastructure Engineer
📌 Hands-on project built to demonstrate real AWS operational skills
