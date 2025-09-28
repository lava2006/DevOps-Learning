
# Amazon Elastic File System (EFS) - Comprehensive Guide and DevOps Learning Log

## Overview  
Amazon EFS is a fully managed, scalable, elastic NFS file system designed for Linux-based workloads. It provides scalable file storage that can be concurrently accessed by multiple EC2 instances, containers, and on-premises servers.


## Introduction

EFS supports shared storage needs with a standard file system interface and file system semantics. It is ideal for workloads needing distributed access to data such as web serving, content management, big data analytics, and container storage.

***

## Core Concepts

- *File System:* A network file system accessible via the NFS protocol.  
- *Elasticity:* Automatically scales storage capacity as files are added and removed without provisioning or managing storage.  
- *Access Control:* Integrates with AWS IAM and POSIX permissions to manage user and process access.  
- *Availability & Durability:* Data is stored redundantly across multiple AZs within a region.  

***

## Performance Modes

| Mode              | Description                                                               | Use Case                             |
|-------------------|---------------------------------------------------------------------------|-------------------------------------|
| General Purpose   | Default; low latency and high throughput for broad workloads              | Web servers, CMS, home directories   |
| Max I/O            | Higher throughput and IOPS for highly parallelized and latency-tolerant workloads | Big data analytics, media processing |

***

## Throughput Modes

| Mode           | Description                                                       | Use Case                            |
|----------------|-------------------------------------------------------------------|------------------------------------|
| Bursting       | Throughput scales automatically with stored data size           | Typical workloads with variable demand |
| Provisioned    | Manually set throughput independent of stored data size          | Performance-sensitive, constant workloads |

***

## Security Features

- Supports encryption of data at rest and in transit.  
- Integrates with AWS KMS for key management.  
- Access controlled by security groups, network ACLs, and IAM policies.  
- Supports POSIX permissions and user/group ownership to enforce file-level security.  

***

## Use Cases

- Shared storage for containerized applications (ECS, EKS).  
- Big data and analytics workloads requiring concurrent access.  
- Content management and media workflows.  
- Lift-and-shift migration of legacy applications needing shared storage.

***

## Best Practices

- Select performance and throughput modes based on workload needs.  
- Use lifecycle management to archive inactive files to cost-effective storage options.  
- Monitor metrics via CloudWatch for performance and throughput optimization.  
- Use IAM and POSIX permissions together for fine-grained security.

***

## Practical Examples

bash
### Create an EFS file system
aws efs create-file-system --creation-token my-efs-token --performance-mode generalPurpose

### Create a mount target in a VPC subnet
aws efs create-mount-target --file-system-id fs-0123456789abcdef0 --subnet-id subnet-12345678 --security-groups sg-12345678

### Mount EFS on EC2 instance (Linux)
sudo yum install -y nfs-utils
sudo mkdir /mnt/efs
sudo mount -t nfs4 -o nfsvers=4.1 fs-0123456789abcdef0.efs.us-east-1.amazonaws.com:/ /mnt/efs

### View mounted file system info
df -h /mnt/efs


***

## Further Reading

- [Amazon EFS Documentation](https://docs.aws.amazon.com/efs/)  
- [Amazon EFS Performance](https://aws.amazon.com/efs/features/performance/)  
- [Amazon EFS Security](https://docs.aws.amazon.com/efs/latest/ug/security.html)  

***
