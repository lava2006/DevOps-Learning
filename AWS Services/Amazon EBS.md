
# Amazon Elastic Block Store (EBS) - Comprehensive Guide and DevOps Learning Log

## Overview  
Amazon Elastic Block Store (EBS) provides high-performance block-level storage volumes that can be attached to Amazon EC2 instances, functioning like traditional hard drives or SSDs. It is ideal for workloads requiring low-latency access to raw storage, such as databases, file systems, and enterprise applications.

***

## Introduction

EBS volumes provide persistent block storage for EC2 instances with a range of volume types to accommodate different performance and cost requirements, from general-purpose SSDs to provisioned IOPS for high throughput workloads.

***

## Core Concepts

- *Volumes:* Virtual hard disks attached to EC2 instances.  
- *Snapshots:* Point-in-time, incremental backups stored in S3 for durability.  
- *IOPS:* Input/output operations per second, representing volume performance.  
- *Throughput:* Data transfer rate to/from the volume.  
- *Elasticity:* Volumes can be resized or changed dynamically.

***

## Volume Types

| Volume Type             | Description                                      | Use Case                                 | Performance                              |
|------------------------|------------------------------------------------|-----------------------------------------|-----------------------------------------|
| General Purpose SSD (gp3, gp2) | Balanced price/performance for most workloads | Web servers, dev/test, boot volumes    | Max 16,000 IOPS, 1000 MB/s throughput   |
| Provisioned IOPS SSD (io2, io1) | High-performance for mission-critical apps     | Databases, latency-sensitive workloads | Max 256,000 IOPS, 4000 MB/s throughput  |
| Throughput Optimized HDD (st1) | Low-cost, high throughput magnetic             | Big data, log processing, streaming    | Max 500 MB/s throughput                  |
| Cold HDD (sc1)          | Lowest cost magnetic, for infrequent access     | Backup, rarely accessed data            | Up to 250 MB/s throughput                |

***

## Snapshots and Backup

- Snapshots are incremental, capturing only changed blocks, reducing cost and time.  
- Can be used to create new volumes or replicate data across regions.  
- Snapshots are stored durably in S3 with 99.999999999% durability.

***

## Performance and Throughput

- EBS volumes deliver consistent, low-latency performance.  
- Supports bursting on gp2 volumes for short spikes.  
- io2 and io2 Block Express volumes support higher IOPS for critical workloads.

***

## Security and Encryption

- Supports encryption at rest using AWS-managed or customer-managed keys via AWS KMS.  
- Encrypts data in transit between EC2 and EBS.  
- Snapshot encryption propagates to new volumes created from snapshots.

***

## Use Cases

- Backend databases (MySQL, PostgreSQL, MongoDB) requiring low-latency disk access.  
- Boot volumes and application file systems.  
- High-throughput workloads like big data analytics and streaming logs.

***

## Best Practices

- Select volume type based on IOPS and throughput needs to balance cost.  
- Regularly snapshot critical volumes for disaster recovery.  
- Use encryption for sensitive data.  
- Monitor performance and adjust volume size/type accordingly.  
- Use RAID configurations for higher throughput or redundancy when needed.

***

## Practical Examples

bash
## Create a new gp3 volume of 100 GiB in us-east-1a
aws ec2 create-volume --availability-zone us-east-1a --size 100 --volume-type gp3

## Attach volume to an EC2 instance
aws ec2 attach-volume --volume-id vol-0123456789abcdef0 --instance-id i-0123456789abcdef0 --device /dev/xvdf

## Create a snapshot of the volume
aws ec2 create-snapshot --volume-id vol-0123456789abcdef0 --description "Daily backup snapshot"

## Create a new volume from snapshot
aws ec2 create-volume --snapshot-id snap-0123456789abcdef0 --availability-zone us-east-1a


***

## Further Reading

- [Amazon EBS Documentation](https://docs.aws.amazon.com/ebs/)  
- [EBS Volume Types and Performance](https://aws.amazon.com/ebs/volume-types/)  
- [Using Amazon EBS Snapshots](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSSnapshots.html)
