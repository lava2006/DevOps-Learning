# 🔐 Deep Dive into AWS IAM

A friendly **beginner-to-intermediate learning guide and hands-on log** for **AWS Identity and Access Management (IAM)**.

AWS IAM helps control **who can access AWS resources, what they can do, and how access is managed securely**.

---

## 🌟 Overview

AWS IAM is one of the most important AWS services to understand when learning **Cloud and DevOps**.

Instead of giving everyone full access to an AWS account, IAM allows us to provide only the permissions required for a particular task.

This guide starts with the basics and gradually moves into practical IAM concepts used in real AWS and DevOps environments.

---

# 1️⃣ What is AWS IAM?

**IAM stands for Identity and Access Management.**

It is used to control access to AWS resources.

```text
User / Application
       |
       v
      IAM
       |
       v
Permissions
       |
       v
AWS Resources
```

### IAM helps answer two questions:

> **Who are you?**

> **What are you allowed to do?**

---

# 2️⃣ Authentication vs Authorization

These are two fundamental IAM concepts.

## Authentication

Authentication answers:

> **Who are you?**

```text
User
  |
  v
Sign In
  |
  v
Identity Verified
```

## Authorization

Authorization answers:

> **What are you allowed to do?**

```text
Verified User
      |
      v
IAM Permissions
      |
      +---- S3 Read → Allowed
      +---- EC2 Start → Allowed
      +---- IAM User Delete → Not Allowed
```

### Simple Difference

| Concept        | Meaning                |
| -------------- | ---------------------- |
| Authentication | Verifies identity      |
| Authorization  | Determines permissions |

---

# 3️⃣ IAM Users

**For:** Representing an individual identity that needs to interact with AWS.

An IAM user can have credentials and permissions that determine which AWS actions they can perform.

### Common Use-Cases

* Individual AWS users
* Development environments
* Testing environments
* Users requiring AWS Console or programmatic access

### Commands to Try

```bash
# List IAM users
aws iam list-users

# Get information about a user
aws iam get-user --user-name my-user

# List policies attached to a user
aws iam list-attached-user-policies --user-name my-user
```

> Avoid creating unnecessary IAM users just for practice.

---

# 4️⃣ IAM Groups

**For:** Managing multiple IAM users with similar responsibilities.

Instead of assigning the same permissions to every user individually, users can be placed into a group.

```text
Developers Group
       |
       +---- User 1
       +---- User 2
       +---- User 3
       |
       v
Common Permissions
```

### Common Use-Cases

* Development teams
* Testing teams
* Operations teams
* Users with similar responsibilities

### Commands to Try

```bash
# List groups
aws iam list-groups

# List users in a group
aws iam get-group --group-name Developers

# List policies attached to a group
aws iam list-attached-group-policies --group-name Developers
```

---

# 5️⃣ IAM Roles

**For:** Providing permissions to trusted entities that can assume the role.

IAM roles are very important in AWS and DevOps because AWS services and applications can use roles instead of storing long-term credentials.

```text
EC2 Instance
      |
      v
   IAM Role
      |
      v
IAM Permissions
      |
      v
S3 Bucket
```

### Common Use-Cases

* EC2 accessing S3
* Lambda accessing DynamoDB
* Applications accessing AWS services
* CI/CD pipelines
* Temporary access

### Commands to Try

```bash
# List roles
aws iam list-roles

# Get role information
aws iam get-role --role-name MyApplicationRole

# List policies attached to a role
aws iam list-attached-role-policies --role-name MyApplicationRole
```

---

# 6️⃣ IAM Policies

**For:** Defining what actions are allowed or denied.

IAM policies are JSON documents.

A policy commonly contains:

| Element   | Meaning            |
| --------- | ------------------ |
| Effect    | Allow or Deny      |
| Action    | AWS operation      |
| Resource  | AWS resource       |
| Condition | Optional condition |

### Example Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
```

### What Does This Mean?

```text
Effect
  ↓
Allow

Action
  ↓
s3:GetObject

Resource
  ↓
Objects inside example-bucket
```

The policy allows the specified identity to read objects from the specified S3 bucket.

---

# 7️⃣ IAM Policy Types

There are different ways IAM policies can be managed.

### AWS Managed Policies

Policies created and maintained by AWS.

Example:

```text
ReadOnlyAccess
```

### Customer Managed Policies

Policies created and managed by you.

Useful when you need customized permissions.

### Inline Policies

Policies directly embedded into an IAM identity.

### Simple Comparison

| Type             | Managed By             | Use                         |
| ---------------- | ---------------------- | --------------------------- |
| AWS Managed      | AWS                    | Common permissions          |
| Customer Managed | You                    | Custom reusable permissions |
| Inline           | Directly with identity | Specific use case           |

---

# 8️⃣ IAM Permissions

Permissions determine exactly what an identity can do.

For example:

```text
Developer
    |
    v
IAM Policy
    |
    +---- EC2 Start → Allowed
    +---- EC2 Stop → Allowed
    +---- S3 Read → Allowed
    +---- IAM User Delete → Not Allowed
```

Permissions can control access to:

* S3
* EC2
* Lambda
* DynamoDB
* RDS
* CloudWatch
* ECR
* ECS

---

# 9️⃣ Principle of Least Privilege

**Least Privilege means giving only the permissions required to complete a task.**

### Too Much Access

```text
Application
     |
     v
AdministratorAccess
     |
     v
Entire AWS Account
```

### Limited Access

```text
Application
     |
     v
Required Permission
     |
     v
S3 Object Read
```

If an application only needs to read S3 objects, it should not automatically receive administrator permissions.

### Why It Matters

Least privilege helps reduce unnecessary access and limits the potential impact of compromised credentials or workloads.

---

# 🔟 IAM Access Keys

Access keys are credentials used for programmatic access to AWS.

They consist of:

```text
Access Key ID
+
Secret Access Key
```

AWS CLI can use these credentials for authentication.

### Check Your Current AWS Identity

```bash
aws sts get-caller-identity
```

### Configure AWS CLI

```bash
aws configure
```

> Never upload AWS access keys to GitHub or place them directly inside source code.

For AWS workloads, IAM roles are generally preferred over long-term credentials.

---

# 1️⃣1️⃣ IAM Roles vs Access Keys

This is an important DevOps concept.

### Using Long-Term Credentials

```text
Application
     |
     v
Access Key
     |
     v
AWS Service
```

### Using an IAM Role

```text
Application
     |
     v
IAM Role
     |
     v
Temporary Credentials
     |
     v
AWS Service
```

### Simple Rule

```text
AWS Workload
     ↓
Prefer IAM Role
```

Roles help avoid storing long-term AWS credentials inside applications.

---

# 1️⃣2️⃣ Multi-Factor Authentication — MFA

**MFA adds an additional authentication factor.**

Instead of relying only on a password:

```text
Password
   +
MFA
   |
   v
Authentication
```

MFA provides an additional layer of protection for AWS identities.

### Good Practice

Use appropriate MFA protection for important AWS identities and accounts.

---

# 1️⃣3️⃣ IAM Policy Evaluation

When an AWS request is made, AWS evaluates applicable permissions to determine whether the request is allowed.

Simplified flow:

```text
AWS Request
     |
     v
Authentication
     |
     v
Policy Evaluation
     |
     +---- Explicit Deny
     |         |
     |         v
     |       DENIED
     |
     +---- Allow
     |       |
     |       v
     |     ALLOWED
     |
     +---- No Allow
             |
             v
           DENIED
```

### Important Rule

> **An explicit Deny overrides an Allow.**

This is very useful when troubleshooting permission problems.

---

# 1️⃣4️⃣ Resource-Based Policies

Some AWS resources can have their own policies.

For example, an S3 bucket can have a **bucket policy**.

### Identity-Based Policy

```text
IAM User / Role
       |
       v
IAM Policy
       |
       v
S3 Bucket
```

### Resource-Based Policy

```text
IAM User / Role
       |
       v
S3 Bucket
       |
       v
Bucket Policy
```

This is an important concept when understanding how AWS resources control access.

---

# 1️⃣5️⃣ IAM Roles for AWS Services

AWS services can use IAM roles to access other AWS services.

### EC2 Example

```text
EC2
 |
 v
IAM Role
 |
 v
S3
```

### Lambda Example

```text
Lambda
   |
   v
Execution Role
   |
   v
DynamoDB
```

### Common Examples

| AWS Service    | IAM Role                   |
| -------------- | -------------------------- |
| EC2            | Instance Role              |
| Lambda         | Execution Role             |
| ECS            | Task Role / Execution Role |
| CloudFormation | Service Role               |

---

# 1️⃣6️⃣ Cross-Account IAM Roles

Organizations may use multiple AWS accounts.

For example:

```text
Development Account
        |
        | Assume Role
        v
Production Account
        |
        v
Production Role
        |
        v
AWS Resources
```

Cross-account roles allow a trusted identity from one AWS account to access resources in another account according to the configured policies.

### Important Concepts

* Trust policy
* Permissions policy
* AssumeRole
* Temporary credentials

---

# 1️⃣7️⃣ Trust Policy vs Permissions Policy

These two policies are easy to confuse.

## Trust Policy

Answers:

> **Who can assume this role?**

```text
Who?
 |
 v
Trust Policy
 |
 v
Can assume role?
```

## Permissions Policy

Answers:

> **What can the role do?**

```text
Role
 |
 v
Permissions Policy
 |
 v
AWS Resources
```

### Easy Way to Remember

```text
Trust Policy
    ↓
WHO can assume?

Permissions Policy
    ↓
WHAT can they do?
```

---

# 🔧 Hands-On Practice

## Explore IAM in AWS Console

Open:

```text
AWS Console
    |
    v
IAM
    |
    +---- Users
    +---- Groups
    +---- Roles
    +---- Policies
```

Explore each section and understand how they are connected.

---

## Check Your Current Identity

```bash
aws sts get-caller-identity
```

Your output will depend on the AWS identity configured in your environment.

---

## List IAM Users

```bash
aws iam list-users
```

---

## List IAM Groups

```bash
aws iam list-groups
```

---

## List IAM Roles

```bash
aws iam list-roles
```

---

## List IAM Policies

```bash
aws iam list-policies
```

---

## Inspect a Role

```bash
aws iam get-role --role-name MyApplicationRole
```

Replace `MyApplicationRole` with a role that exists in your AWS account.

---

# 🧪 Progressive Hands-On Labs

## 🟢 Beginner Lab

Understand:

```text
User
 ↓
Group
 ↓
Policy
```

### Goal

Understand how IAM identities receive permissions.

---

## 🟡 Beginner → Intermediate Lab

Explore an IAM policy and identify:

```text
Effect:
Action:
Resource:
Condition:
```

Then explain what the policy allows or denies in your own words.

---

## 🔵 Intermediate Lab

Understand:

```text
EC2
 ↓
IAM Role
 ↓
S3
```

### Goal

Understand how an AWS workload can access another AWS service using an IAM role.

---

## 🟣 DevOps Lab

Understand:

```text
CI/CD Pipeline
      |
      v
IAM Role
      |
      v
AWS Deployment
```

### Goal

Understand why IAM roles are useful for automated AWS deployments.

---

# 🌍 Real-World DevOps Example

Imagine a company running an application on AWS.

Different users and applications need different permissions.

```text
AWS Account
     |
     +---- Developers
     |
     +---- Testers
     |
     +---- Operations
     |
     +---- Applications
```

A developer may need access to EC2 and CloudWatch.

An application running on EC2 may need access to an S3 bucket.

A CI/CD pipeline may need permission to deploy an application.

IAM allows these permissions to be managed separately.

---

# 🔒 IAM Security Practices

* Follow the principle of least privilege.
* Enable MFA where appropriate.
* Never share AWS credentials.
* Never upload AWS access keys to GitHub.
* Avoid hard-coding credentials in source code.
* Prefer IAM roles for AWS workloads.
* Review permissions regularly.
* Remove unused credentials.
* Avoid using the root user for everyday AWS operations.
* Use temporary credentials where appropriate.

---

# ⚠️ Common Mistakes

### Giving Everyone AdministratorAccess

Not every user or application needs complete AWS access.

### Sharing AWS Credentials

Each identity should use its own appropriate authentication method.

### Hard-Coding Access Keys

Never put AWS credentials directly into application code.

### Confusing Users and Roles

```text
User
 ↓
Identity

Role
 ↓
Assumable identity with permissions
```

### Ignoring Least Privilege

Giving excessive permissions creates unnecessary access.

### Forgetting Explicit Deny

Remember:

```text
Explicit Deny
     ↓
Overrides Allow
```

---

# 💡 Key Takeaways

* IAM stands for **Identity and Access Management**.
* IAM controls access to AWS resources.
* Authentication verifies identity.
* Authorization determines permissions.
* IAM Users represent identities.
* IAM Groups organize users with common permissions.
* IAM Roles provide permissions to trusted entities.
* IAM Policies define permissions.
* Least privilege means giving only required access.
* Access keys provide programmatic authentication.
* IAM roles are important for AWS workloads.
* Resource-based policies can control access from the resource side.
* Explicit Deny overrides Allow.
* IAM is an important part of AWS security and DevOps.

---

# 🚀 Mini Challenges

## Challenge 1

Explain the difference between:

```text
IAM User
IAM Group
IAM Role
IAM Policy
```

---

## Challenge 2

An EC2 instance needs to read files from an S3 bucket.

Which approach is more appropriate?

```text
A. Store an AWS access key inside the application

B. Use an IAM Role with the required S3 permissions
```

Explain why.

---

## Challenge 3

Look at an IAM policy and identify:

```text
Effect:
Action:
Resource:
Condition:
```

---

## Challenge 4

Explain the difference between:

```text
Authentication
Authorization
```

in your own words.

---

## Challenge 5

Draw this architecture:

```text
EC2
 ↓
IAM Role
 ↓
IAM Policy
 ↓
S3
```

---

# 📝 My Learning Notes

```text
What I learned:

IAM means:

Authentication means:

Authorization means:

IAM User means:

IAM Group means:

IAM Role means:

IAM Policy means:

Least Privilege means:

Trust Policy means:

Permissions Policy means:

What I practiced:

What I observed:

What I found difficult:

What I want to learn next:
```

---



# 📚 Beginner-Friendly Resources

* [AWS Free Tier](https://aws.amazon.com/free/)
* [AWS IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
* [IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
* [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
* [AWS CLI Getting Started](https://docs.aws.amazon.com/cli/latest/userguide/getting-started.html)
* [AWS Skill Builder](https://skillbuilder.aws/)

---

# 📌 GitHub Update

### Commit Message

```text
Learned AWS IAM from beginner to intermediate
```

### Learning Summary

```text
Learned the fundamentals of AWS IAM, including
Users, Groups, Roles, Policies, Authentication,
Authorization, Least Privilege, MFA, Access Keys,
Policy Evaluation, Resource-Based Policies, and
Cross-Account Roles.

Also practiced exploring IAM using the AWS Console
and AWS CLI and understood how IAM is used in
real-world AWS and DevOps environments.
```
