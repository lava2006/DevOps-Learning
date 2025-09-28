
# 🚀 Deep Dive: Amazon S3 Features and Storage Classes

## Overview

Amazon Simple Storage Service (S3) is a cloud-native, fully managed object storage service designed for storing and retrieving any amount of data from anywhere. It offers industry-leading durability, scalability, and security with:

- 11 nines (99.999999999%) durability via data replication across multiple Availability Zones (AZs).
- Encryption options at rest and in transit.
- Virtually unlimited storage capacity.
- Easy access through AWS SDKs, CLI, REST APIs, and the AWS Management Console.

---

## Amazon S3 Storage Classes

| Storage Class                  | Use Case & Access Patterns                                                       | Durability           | Availability        | Latency              | Cost                   |
|-------------------------------|---------------------------------------------------------------------------------|----------------------|---------------------|----------------------|------------------------|
| **S3 Standard**                | Frequently accessed data such as websites and applications                       | 99.999999999%        | 99.99%              | Millisecond          | Highest                |
| **S3 Intelligent-Tiering**    | Data with unknown or changing access patterns, auto tiering                      | 99.999999999%        | 99.9%               | Millisecond          | Lower with monitoring   |
| **S3 One Zone-IA**            | Infrequently accessed, re-creatable data stored in a single AZ                   | 99.999999999%        | 99.5%               | Millisecond          | Lowest per tier         |
| **S3 Standard-IA**            | Less frequently accessed data but needs rapid access                             | 99.999999999%        | 99.9%               | Millisecond          | Lower than standard     |
| **S3 Glacier Instant Retrieval** | Long-lived archive with instant retrieval                                     | 99.999999999%        | 99.9%               | Millisecond          | Very low                |
| **S3 Glacier Flexible Retrieval** | Archive data with minutes to hours retrieval                                  | 99.999999999%        | 99.99%              | Minutes to hours     | Very low                |
| **S3 Glacier Deep Archive**   | Deep archival storage rarely accessed                                            | 99.999999999%        | 99.99%              | Hours                | Lowest cost             |

---

## Use Cases Aligned to Storage Classes

| Use Case                           | Recommended Storage Class                      |
|-----------------------------------|-----------------------------------------------|
| Hosting frequently accessed assets| S3 Standard                                   |
| Data lakes with unpredictable access patterns | S3 Intelligent-Tiering                 |
| Backup with rapid access needs    | S3 Standard-IA or Glacier Instant Retrieval   |
| Long-term archival                | Glacier Flexible Retrieval or Deep Archive    |
| Live data requiring very low latency | S3 Express One Zone                          |

---

## Project Example: Hosting a Static Website on Amazon S3

Amazon S3 can host a **fully static website** with no servers required, ideal for portfolio sites, documentation, or simple landing pages.

### Steps to host a static website on S3

1. **Create an S3 bucket**


aws s3 mb s3://my-static-website-bucket


2. **Enable static website hosting**


aws s3 website s3://my-static-website-bucket/ --index-document index.html --error-document error.html


3. **Set bucket policy to allow public read access**


{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::my-static-website-bucket/*"]
    }
  ]
}


Apply it via AWS CLI:


aws s3api put-bucket-policy --bucket my-static-website-bucket --policy file://bucket-policy.json


4. **Upload your static website files**


aws s3 cp ./website/ s3://my-static-website-bucket/ --recursive


5. **Access your website**

Visit: `http://my-static-website-bucket.s3-website.<region>.amazonaws.com`

---

## Summary

Amazon S3 is a powerful and versatile storage service with a wide range of storage classes tailored for different needs. Hosting a static website is a popular, cost-effective use case that leverages S3’s global availability and durability.

---

## References

- [AWS S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/)  
- [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)  
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-website.html)  

---

Would you like a similar project or example scripts for other AWS storage services like EBS, EFS, or FSx?


This README section helps demonstrate practical knowledge and can be expanded with your website project details. Would you like assistance creating a full sample static site project repository structure?
