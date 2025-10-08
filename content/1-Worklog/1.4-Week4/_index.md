---
title: "Week 4 Worklog"
date: 2025-10-05
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
* Understand key AWS Storage Services including Amazon S3, S3 Glacier, AWS Snow Family, AWS Storage Gateway, and AWS Backup.  
* Learn the concepts of RTO/RPO and disaster recovery strategies on AWS.  

---

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ----- | ---------- | --------------- | ------------------ |
| 1 | - Study an overview of Amazon Simple Storage Service (S3): <br>&emsp; + Object storage concept <br>&emsp; + Buckets and objects <br>&emsp; + Data durability and availability <br>&emsp; + Multipart upload, trigger events, REST API | 2025/09/29 | 2025/09/29 |[Amazon Simple Storage Service ( S3 )](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=104) |
| 2 | - Learn about S3 Storage Classes: <br>&emsp; + Standard, Standard-IA, Intelligent Tiering, One Zone-IA, Glacier / Deep Archive <br>&emsp; + Configure Object Lifecycle Management for automated data transitions | 2025/09/30 | 2025/09/30 |[Amazon Simple Storage Service ( S3 )](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=104) |
| 3 | - Study S3 access control: <br>&emsp; + Access Control List (ACL) <br>&emsp; + Bucket Policy & IAM Policy <br>&emsp; + S3 Access Point <br>&emsp; + Endpoint & Versioning | 2025/10/01 | 2025/10/01 | [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) |
| 4 | - Explore Static Website Hosting and CORS on S3 <br>&emsp; + Understand Cross-Origin Resource Sharing (CORS) mechanism <br>&emsp; + Configure CORS policy for domain-based access | 2025/10/02 | 2025/10/02 | [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) |
| 5 | - Study S3 Glacier and retrieval options: Expedited, Standard, Bulk <br> - Learn about S3 Object Keys and performance optimization using prefixes and partitions | 2025/10/03 | 2025/10/03 | [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) |
| 6 | - Learn about AWS Snow Family: <br>&emsp; + Snowball (80 TB) <br>&emsp; + Snowball Edge (100 TB with compute) <br>&emsp; + Snowmobile (100 PB) <br> - Study AWS Storage Gateway types (File / Volume / Tape) <br> - Understand AWS Backup and Disaster Recovery concepts: RTO, RPO, and 4 recovery strategies | 2025/10/04 | 2025/10/05 | [AWS Snow Family Video](http://youtube.com/watch?v=YXn8Q_Hpsu4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=106) |

---

### Week 4 Achievements:

#### Amazon Simple Storage Service (S3)

· Amazon S3 is an object-based storage service, meaning if you want to modify part of a file, you must re-upload the entire file.  
· Suitable for **Write Once, Read Many (WORM)** data.  
· There is no limit on total storage capacity, but each object can be up to **5 TB**.  
· Data is replicated across **3 Availability Zones** by default for high durability and availability (99.999999999% durability and 99.99% availability).  
· Supports **multipart uploads**, **event triggers**, and **REST API** access.  

#### Amazon S3 Storage Classes

· S3 offers multiple storage classes to optimize cost:  
  - **S3 Standard** – frequently accessed data.  
  - **S3 Standard-IA** – infrequently accessed data.  
  - **S3 Intelligent-Tiering** – automatically moves objects between classes based on access frequency.  
  - **S3 One Zone-IA** – infrequent access, single AZ.  
  - **S3 Glacier / Deep Archive** – long-term, low-cost archival storage.  

· **Object Lifecycle Management** can automatically transition data between storage classes.  

#### Access Control in S3

· Two main access control mechanisms:  
  - **S3 Access Control List (ACL)** – older method granting specific access to accounts or groups.  
  - **Bucket Policy & IAM Policy** – define fine-grained access at the resource level.  

#### S3 Endpoint & Versioning

· **S3 Endpoint** allows access to buckets through AWS private networks.  
· **Versioning** enables recovery of previous object versions after deletion or overwrite.  

#### Static Website Hosting & CORS

· S3 supports hosting static websites (HTML, CSS, JS, media).  
· **CORS (Cross-Origin Resource Sharing)** allows resources (fonts, scripts, etc.) to be accessed from other domains.  

#### Object Key & Performance

· Each object in S3 is flat (non-hierarchical) and identified by a unique key.  
· For optimal performance, random prefixes can be used to distribute load across multiple partitions.  

#### Amazon S3 Glacier

· Low-cost storage for long-term data retention with delayed access.  
· Three retrieval options:  
  - **Expedited:** 1–5 minutes  
  - **Standard:** 3–5 hours  
  - **Bulk:** 5–12 hours  

#### AWS Snow Family

· **Snowball:** Data migration device up to 80 TB.  
· **Snowball Edge:** 100 TB capacity with local compute capability.  
· **Snowmobile:** Large-scale migration up to 100 PB (Exabyte-level).  

#### AWS Storage Gateway

· Hybrid storage solution connecting on-premises environments with AWS Cloud.  
· Supports three types:  
  - **File Gateway (NFS/SMB → S3)**  
  - **Volume Gateway (iSCSI → S3 / EBS Snapshot)**  
  - **Tape Gateway (VTL → S3 / Glacier)**  

#### AWS Backup & Disaster Recovery

· Centralized backup management service for AWS resources (EBS, EC2, RDS, DynamoDB, EFS, Storage Gateway).  
· **RTO (Recovery Time Objective):** Time required to restore services.  
· **RPO (Recovery Point Objective):** Maximum acceptable data loss window.  
· Four disaster recovery strategies:  
  1. Backup & Restore  
  2. Pilot Light (Active–Standby)  
  3. Low-Capacity Active–Active  
  4. Full-Capacity Active–Active  

---

### Week 4 Summary:
During this week, I learned in detail about AWS Storage Services including Amazon S3, S3 Glacier, AWS Snow Family, Storage Gateway, and AWS Backup.  
I understood the storage classes, access control methods, lifecycle policies, versioning, and CORS configurations in S3.  
Additionally, I explored data migration tools, hybrid storage solutions, and disaster recovery mechanisms using RTO/RPO strategies.
