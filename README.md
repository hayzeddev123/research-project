# AWS Research Project – Critical Thinking

**Author:** Adeniyi Abdulazeez (`hayzeddev123`)  
**Date:** August 2026  
**Topic:** Cloud Storage, Amazon S3, Security Strategy & Disaster Recovery

---

## 1. Cloud Storage and Amazon S3

### a) Types of Cloud Storage

* **Block storage**: Stores data in blocks and is commonly used for virtual machines and databases.  
  **Example:** Amazon EBS.

* **File storage**: Stores data as files in folders.  
  **Example:** Amazon EFS.

* **Object storage**: Stores data as objects with metadata.  
  **Example:** Amazon S3.

Amazon S3 is an **object storage** service.

### b) Key Features of Amazon S3

* **Durability**: Designed to prevent data loss (11 nines of durability).
* **Availability**: Data can be accessed when needed.
* **Scalability**: Can store very large amounts of data without capacity planning.
* **Security**: Supports encryption, IAM, bucket policies, and access controls.

### c) S3 vs Google Cloud Storage and Azure Blob Storage

Amazon S3, Google Cloud Storage, and Azure Blob Storage are all object storage services.  
Their main differences are:

* The cloud provider ecosystem
* Pricing models
* Available features and storage classes
* Integration with their respective cloud services

### d) Benefits of Amazon S3

* Cost-effective
* Highly scalable
* Easy to use
* Flexible storage classes and lifecycle options
* Integrates with many AWS services

### e) S3 Integration with AWS Services

* **IAM**: Controls who can access S3 resources.
* **Bucket policies**: Define fine-grained access to buckets and objects.
* **EC2**: Applications running on EC2 can store and retrieve files from S3.
* **CloudFront**: Delivers S3 content faster to users through a global CDN.
* **Lambda**: Can automatically perform actions when objects are uploaded or changed (event-driven).

### f) S3 Best Practices

* Enable encryption (SSE-S3, SSE-KMS, or client-side).
* Use IAM and bucket policies to control access.
* Avoid making sensitive buckets public.
* Enable versioning where appropriate.
* Use lifecycle rules to move or delete old data automatically.
* Monitor access and activity using CloudTrail and S3 access logs.

---

## 2. Storage Solution for a Large E-Commerce Website

**Recommendation:** Amazon S3 combined with Amazon CloudFront.

### Why this combination?

* **Scalability**: S3 can handle large amounts of images, videos, and other website assets without capacity limits.
* **Performance**: CloudFront caches assets closer to users, reducing loading time and improving user experience.
* **Cost**: S3 is generally cheaper than storing large static assets directly on application servers.
* **Management**: S3 is fully managed, so there is no need to maintain storage servers.

### Architecture

```
Users → CloudFront (CDN) → Amazon S3 → Website Assets
```

This architecture separates large static files from the application server and significantly improves website performance and scalability.

---

## 3. Security Strategy for 30 Internal Videos

I would use a **private S3 bucket** with the following security measures:

### Encryption
* Enable S3 server-side encryption (SSE-S3 or SSE-KMS).
* Encrypt sensitive data both at rest and in transit (HTTPS).

### Access Control
* Keep the bucket private (Block Public Access enabled).
* Use IAM roles and policies to give only authorized employees access.
* Follow the **Principle of Least Privilege**.
* Use temporary access methods such as **presigned URLs** when appropriate.

### Monitoring
* Enable logging and monitoring.
* Use **AWS CloudTrail** to track API activity.
* Monitor unusual access attempts.
* Review permissions regularly.

### Backup & Protection
* Enable **S3 Versioning** to protect against accidental deletion or overwrite.
* Use appropriate backup or cross-region replication options for important videos.

This strategy helps prevent unauthorized access, accidental deletion, and data loss.

---

## 4. Disaster Recovery Plan

A cloud application should have a plan that allows it to recover after a major failure.

### 1. Backup
* Regularly back up databases and important files.
* Store backups separately from the main environment (preferably in another region or account).
* Test backups regularly to ensure they can be restored.

### 2. Redundancy
* Deploy applications across multiple **Availability Zones**.
* Use redundant databases (Multi-AZ) and storage.
* Avoid having a single server as the only point of failure.

### 3. Failover
Use services such as:
* **Elastic Load Balancer** to distribute traffic and detect unhealthy instances.
* **Auto Scaling** to automatically replace failed servers.
* **Route 53** for DNS-based failover and health checks.

### 4. Recovery Steps
When a disaster occurs:

1. Detect the failure (monitoring & alarms).
2. Redirect users to healthy infrastructure.
3. Restore data from backups if necessary.
4. Verify the application is working correctly.
5. Monitor the recovered environment.

### 5. Testing
Regularly perform disaster recovery tests (tabletop exercises and actual recovery drills) to make sure backups, failover, and recovery procedures actually work.

**Main Goal:** Minimize downtime and data loss while getting the application back online as quickly as possible.

---

**End of Report**
