
# 🚀 Deep Dive into AWS Storage Services

A friendly guide and hands-on learning log for **DevOps beginners** on AWS’s core storage offerings: **S3, EBS, EFS, FSx, and Storage Gateway**.

---

## 🌟 Overview

AWS offers a toolkit of storage services: whether files, VM drives, big data, or hybrid cloud setups, there’s a managed service for every need.  
This guide explores what each service does, why DevOps teams use them, and how to get started with real command-line examples.

---

## 1️⃣ Amazon S3 (Simple Storage Service)

**For:** Uploading, storing, and sharing files like documents, backups, images, videos — almost anything.

- **Durable:** Keeps data safe with 99.999999999% durability.  
- **Flexible:** Multiple storage classes to save money.  
- **Secure:** Encrypts data, lets you fine-tune who can see or change your stuff.  

**Common Use-Cases:**
- Backing up important files  
- Hosting a static website  
- Storing build artifacts, logs  
- Data lakes for analytics  

**Scripts to Try:**
```bash
# Make a new S3 bucket
aws s3 mb s3://my-first-s3-bucket

# Upload a file
aws s3 cp ./photo.jpg s3://my-first-s3-bucket/

# List bucket contents
aws s3 ls s3://my-first-s3-bucket/
````

---

## 2️⃣ Amazon EBS (Elastic Block Store)

**For:** Attaching “virtual hard drives” to EC2 cloud servers, perfect for things like databases or application storage.

* **Blocks:** Like a regular disk — good for databases and fast-changing data.
* **Different types:** Fast SSD or big capacity HDD, pick what fits.
* **Easy backup:** Snapshots let you save your data at any point for safety.

**Common Use-Cases:**

* Store files needed by an app server
* Database data and logs
* Daily/weekly automatic backups

**Scripts to Try:**

```bash
# Make a 20GB volume
aws ec2 create-volume --size 20 --availability-zone us-east-1a --volume-type gp3

# Attach the volume to an EC2 server
aws ec2 attach-volume --volume-id vol-xxxxxxxx --instance-id i-xxxxxxxx --device /dev/xvdf

# Make a backup snapshot
aws ec2 create-snapshot --volume-id vol-xxxxxxxx --description "Backup 28-09-2025"
```

---

## 3️⃣ Amazon EFS (Elastic File System)

**For:** Shared file storage that lots of servers can access at once, just like a network drive.

* **Network file system:** Perfect for apps and tools needing to read/write at the same time.
* **Grows/shrinks automatically:** Only pay for what you use!
* **Works with containers:** Great for microservices.

**Common Use-Cases:**

* Shared file storage for web apps
* Processing big data together
* Multiple servers using the same data

**Scripts to Try:**

```bash
# Create an EFS file system
aws efs create-file-system --creation-token myfirst-efs

# Make it accessible in your subnet
aws efs create-mount-target --file-system-id fs-xxxxxxxx --subnet-id subnet-xxxxxxxx

# On EC2, mount and use it (Linux example)
sudo mkdir /mnt/efs
sudo mount -t nfs4 -o nfsvers=4.1 fs-xxxxxxxx.efs.us-east-1.amazonaws.com:/ /mnt/efs
```

---

## 4️⃣ Amazon FSx (Specialized File Storage)

**For:** High-performance shared drives tailored for Windows, HPC workloads, or enterprise NAS.

* **Options:** File shares for Windows (SMB), super-fast Lustre for big data, and NetApp ONTAP for enterprise features.
* **Fully managed:** AWS handles hardware, scaling, and backups.
* **Integrates with S3:** FSx Lustre can sync with S3 for analytics workflows.

**Common Use-Cases:**

* Windows file servers in the cloud
* Running simulations or machine learning models
* Large shared storage for teams

**Scripts to Try:**

```bash
# Create FSx for Windows
aws fsx create-file-system --file-system-type WINDOWS --storage-capacity 300 --subnet-ids subnet-xxxxxxxx --windows-configuration DeploymentType=SINGLE_AZ_1

# Create FSx for Lustre
aws fsx create-file-system --file-system-type LUSTRE --storage-capacity 1200 --subnet-ids subnet-xxxxxxxx
```

---

## 5️⃣ AWS Storage Gateway

**For:** Connecting on-premises environments (office, data center) to AWS cloud storage.

* **Hybrid storage:** Access cloud data locally, backup files/tapes offsite easily.
* **Protocols:** File (NFS/SMB), block (iSCSI), or virtual tape library.
* **Good for:** Backup, disaster recovery, and migration to cloud.

**Common Use-Cases:**

* Local file servers with cloud backup
* Tape replacement with cloud storage
* Seamless migration to AWS

**Scripts to Try:**

```bash
# Create a file gateway template (requires activation key from AWS Console)
aws storagegateway create-gateway --gateway-name MyFirstGateway --gateway-type FILE_S3 --activation-key ABCDEFGHIJ --gateway-region us-east-1

# Make an NFS file share (example only, customize as needed)
aws storagegateway create-nfs-file-share --client-list 0.0.0.0/0 --gateway-arn arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-xxxxxxxx --location-arn arn:aws:s3:::my-first-s3-bucket --role arn:aws:iam::123456789012:role/StorageGatewayRole
```

---

## 🔒 DevOps Fit and Security

* Use AWS CLI or Infrastructure-as-Code for automating storage set-up and tear-down.
* Store build artifacts and logs in S3, backups on EBS, and shared code/config on EFS.
* Always enable encryption and control permissions with IAM.
* Monitor usage and costs with the AWS console or AWS Budgets.

---

## 📚 Beginner Resources

* [AWS Free Tier – Try AWS services for free](https://aws.amazon.com/free/)
* [AWS S3 Getting Started Docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
* [Simple AWS CLI Tutorial](https://docs.aws.amazon.com/cli/latest/userguide/getting-started.html)
* [AWS EBS User Guide for Beginners](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
* [AWS EFS Documentation](https://docs.aws.amazon.com/efs/)
* [Amazon FSx Types Explained](https://aws.amazon.com/fsx/)
* [AWS Storage Gateway Beginner Guide](https://docs.aws.amazon.com/storagegateway/latest/userguide/WhatIsStorageGateway.html)
* [AWS Training & Certification Portal](https://explore.skillbuilder.aws/learn)

```
