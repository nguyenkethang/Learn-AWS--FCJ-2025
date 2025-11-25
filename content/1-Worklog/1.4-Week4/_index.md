---
title: "Week 4 Worklog"
date: 2025-10-05
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
* Master key AWS Storage Services including **Amazon S3**, **Glacier**, **Snow Family**, **Storage Gateway**, **AWS Backup**, and **Amazon FSx**.  
* Understand **RTO/RPO** concepts and **Disaster Recovery** strategies on AWS.  
* Complete hands-on labs for S3 Bucket, Backup Plan, Storage Gateway, VM Migration, and FSx for Windows File Server.
* Master advanced S3 features: Access Point, Storage Class, CORS, Versioning, Replication.

---

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ----- | ---------- | --------------- | ------------------ |
| 1 | - **Module 04-01:** AWS Storage Services Overview <br> - **Module 04-02:** Amazon S3 - Access Point - Storage Class <br>&emsp; + Object Storage concepts, Buckets and Objects <br>&emsp; + S3 Access Point for access management <br>&emsp; + Storage Classes: Standard, IA, Intelligent-Tiering, Glacier <br> - **Lab 13-02.1:** Create S3 Bucket | 2025/09/29 | 2025/09/29 | https://000013.awsstudygroup.com/ |
| 2 | - **Module 04-03:** S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier <br>&emsp; + Static Website Hosting <br>&emsp; + CORS Configuration <br>&emsp; + Bucket Policy, ACL, IAM Policy <br>&emsp; + Object Key Optimization <br>&emsp; + Glacier Retrieval Options <br> - **Lab 13-02.2:** Deploy Infrastructure <br> - **Lab 13-03:** Create Backup Plan | 2025/09/30 | 2025/09/30 | https://000013.awsstudygroup.com/ |
| 3 | - **Module 04-04:** Snow Family - Storage Gateway - Backup <br>&emsp; + Snowball, Snowball Edge, Snowmobile <br>&emsp; + File Gateway, Volume Gateway, Tape Gateway <br>&emsp; + AWS Backup Service <br>&emsp; + RTO/RPO and Disaster Recovery Strategies <br> - **Lab 13-04:** Set up notifications <br> - **Lab 13-05:** Test Restore <br> - **Lab 13-06:** Clean up resources | 2025/10/01 | 2025/10/01 | https://000013.awsstudygroup.com/ |
| 4 | - **Lab 14-01:** VMWare Workstation Setup <br> - **Lab 14-02.1:** Export Virtual Machine from On-premises <br> - **Lab 14-02.2:** Upload virtual machine to AWS <br> - **Lab 14-02.3:** Import virtual machine to AWS <br> - **Lab 14-02.4:** Deploy Instance from AMI | 2025/10/02 | 2025/10/02 | https://000014.awsstudygroup.com/ |
| 5 | - **Lab 14-03.1:** Setting up S3 bucket ACL <br> - **Lab 14-03.2:** Export virtual machine from Instance <br> - **Lab 14-05:** Resource Cleanup on AWS Cloud <br> - **Lab 24-2.1:** Create Storage Gateway <br> - **Lab 24-2.2:** Create File Shares | 2025/10/03 | 2025/10/03 | https://000024.awsstudygroup.com/ |
| 6 | - **Lab 24-2.3:** Mount File shares on On-premises machine <br> - **Lab 24-3:** Clean up resources <br> - **Lab 25-2.2:** Create an SSD Multi-AZ file system <br> - **Lab 25-2.3:** Create an HDD Multi-AZ file system <br> - **Lab 25-3:** Create new file shares | 2025/10/04 | 2025/10/04 | https://000025.awsstudygroup.com/ |
| 7 | - **Lab 25-4:** Test Performance <br> - **Lab 25-5:** Monitor Performance <br> - **Lab 25-6:** Enable data deduplication <br> - **Lab 25-7:** Enable shadow copies <br> - **Lab 25-8:** Manage user sessions and open files <br> - **Lab 25-9:** Enable user storage quotas <br> - **Lab 25-11:** Scale throughput capacity <br> - **Lab 25-12:** Scale storage capacity <br> - **Lab 25-13:** Delete environment <br> - Write weekly report and review all learned content | 2025/10/05 | 2025/10/05 | https://000025.awsstudygroup.com/ |

---

### Week 4 Achievements:

#### Amazon Simple Storage Service (S3)
This week, I learned in detail about **Amazon S3** – an Object Storage service on AWS.  
Data in S3 is stored as **objects** in **buckets**, with 99.999999999% durability and 99.99% availability.  
Each object can be up to **5TB**, and data is **replicated across 3 Availability Zones (AZ)** within the same Region for safety.  

Amazon S3 supports useful features like **Multipart Upload** (uploading large files in parts), **Trigger Events** (triggering actions on upload or delete events), and access via **REST API (HTTP)**.  
S3 is particularly suitable for **Write Once Read Many (WORM)** data types.

#### Amazon S3 Storage Classes

Amazon S3 is divided into multiple **Storage Classes** to optimize cost and performance:  
- **S3 Standard:** For frequently accessed data.  
- **S3 Standard-IA:** For infrequently accessed data.  
- **S3 Intelligent-Tiering:** Automatically moves data between tiers based on access frequency.  
- **S3 One Zone-IA:** Infrequent access data, stored in only 1 AZ, lower cost.  
- **S3 Glacier / Deep Archive:** Long-term storage, extremely low cost.  

Users can set up **Object Lifecycle Management** to automatically transition data between classes over time.

#### Access Control, Endpoint & Versioning

Amazon S3 supports 2 main permission mechanisms:  
- **Access Control List (ACL)** – grants permissions directly at the object or bucket level.  
- **Bucket Policy / IAM Policy** – allows detailed permission definition through Resources.  

Additionally, **Versioning** can be enabled to recover old data when overwritten or deleted, and **S3 Endpoint** can be used for secure access within AWS internal networks.

#### Static Website Hosting & CORS

Amazon S3 allows **hosting static websites (HTML, CSS, JS)**, very suitable for SPA (Single Page Application).  
The service supports **CORS (Cross-Origin Resource Sharing)**, allowing resources like scripts, images, or fonts to be accessed from different domains.

#### Performance Optimization

In S3, each object is assigned a unique **Object Key**, with no true hierarchical directory structure.  
To optimize retrieval performance, **random prefixes** can be used to distribute data evenly across multiple partitions.

#### Amazon S3 Glacier

**S3 Glacier** is a low-cost storage class for long-term data that is rarely accessed.  
There are three data retrieval methods:  
- **Expedited:** 1–5 minutes.  
- **Standard:** 3–5 hours.  
- **Bulk:** 5–12 hours.  

#### AWS Snow Family

The **Snow Family** product line includes:  
- **Snowball:** Device for migrating on-premise data to AWS, maximum capacity 80TB.  
- **Snowball Edge:** Supports on-site compute processing, 100TB capacity.  
- **Snowmobile:** Solution for extremely large data transport, up to 100PB, using specialized containers.

#### AWS Storage Gateway

**AWS Storage Gateway** service helps connect **on-premise environments with AWS Cloud**, providing hybrid storage solutions.  
Includes three main types:  
- **File Gateway:** File sharing (NFS/SMB) → S3 storage.  
- **Volume Gateway:** Provides block storage (iSCSI) → saves snapshots to S3/EBS.  
- **Tape Gateway:** Virtual tape backup solution (VTL) → stores on S3/Glacier.

#### AWS Backup & Disaster Recovery

**AWS Backup** is a centralized backup management service for AWS resources (EBS, EC2, RDS, DynamoDB, EFS, Storage Gateway).  
Two important concepts:  
- **RTO (Recovery Time Objective):** Time needed to restore the system.  
- **RPO (Recovery Point Objective):** Maximum amount of data that can be lost.  

Four common disaster recovery strategies:  
1. **Backup & Restore**  
2. **Pilot Light (Active–Standby)**  
3. **Low Capacity Active–Active**  
4. **Full Capacity Active–Active**

#### VM Migration to AWS

Through **Lab 14**, I learned how to migrate virtual machines from on-premises to AWS using **VM Import/Export**:
- Export VM from VMware Workstation
- Upload VM image to S3
- Import VM to create AMI
- Deploy EC2 instances from AMI
- Export instances back to VM format

#### Amazon FSx for Windows File Server

Through **Lab 25**, I gained hands-on experience with **Amazon FSx for Windows File Server**:
- Create Multi-AZ file systems (both SSD and HDD)
- Test and monitor performance
- Enable advanced features: data deduplication, shadow copies
- Manage user sessions and storage quotas
- Scale throughput and storage capacity dynamically

---

### Week 4 Summary:

This week I completed comprehensive learning and hands-on practice of AWS Storage Services including Amazon S3, Glacier, Snow Family, Storage Gateway, AWS Backup, and Amazon FSx for Windows File Server.

Through 4 theory modules and 4 hands-on lab series (Lab 13, 14, 24, 25), I mastered how to classify data by access needs, configure detailed permissions, deploy automated backups, and establish effective disaster recovery policies.

In particular, I practiced important skills:
- Create and manage S3 Buckets with different Storage Classes
- Deploy AWS Backup Plan for EC2 and EBS with notifications and restore testing
- Configure Storage Gateway for hybrid cloud connectivity and mount file shares
- Migrate VMs from on-premises to AWS through VM Import/Export
- Deploy and optimize Amazon FSx for Windows File Server with full features: deduplication, shadow copies, storage quotas, and scaling

This knowledge helps me understand the mechanisms of Object Storage, Access Control, Versioning, Lifecycle in S3, as well as hybrid storage solutions and file systems on AWS, enabling flexible, secure, and cost-effective data management.

---

### Reference Materials:

**Lab Workshops:**
* **Lab 13 - Deploy AWS Backup:**  
  https://000013.awsstudygroup.com/

* **Lab 14 - VM Import/Export:**  
  https://000014.awsstudygroup.com/

* **Lab 24 - Storage Gateway:**  
  https://000024.awsstudygroup.com/

* **Lab 25 - Amazon FSx for Windows File Server:**  
  https://000025.awsstudygroup.com/

**Official AWS Documentation:**
* **Amazon S3 User Guide:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/

* **S3 Storage Classes:**  
  https://aws.amazon.com/s3/storage-classes/

* **S3 Access Points:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points.html

* **S3 Static Website Hosting:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html

* **S3 CORS Configuration:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html

* **S3 Versioning:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html

* **S3 Replication:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html

* **S3 Lifecycle Management:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html

* **S3 Performance Optimization:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/optimizing-performance.html

* **Amazon S3 Glacier:**  
  https://docs.aws.amazon.com/amazonglacier/latest/dev/

* **AWS Snow Family:**  
  https://aws.amazon.com/snow/

* **AWS Snowball:**  
  https://docs.aws.amazon.com/snowball/

* **AWS Storage Gateway:**  
  https://docs.aws.amazon.com/storagegateway/

* **AWS Backup:**  
  https://docs.aws.amazon.com/aws-backup/

* **AWS Backup Best Practices:**  
  https://docs.aws.amazon.com/aws-backup/latest/devguide/best-practices.html

* **Amazon FSx for Windows File Server:**  
  https://docs.aws.amazon.com/fsx/latest/WindowsGuide/

* **VM Import/Export:**  
  https://docs.aws.amazon.com/vm-import/latest/userguide/

* **Amazon CloudFront:**  
  https://docs.aws.amazon.com/cloudfront/

* **Disaster Recovery on AWS:**  
  https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/

**Video Tutorials:**
* **Amazon S3 Tutorial:**  
  https://www.youtube.com/watch?v=_yunukwcAwc

* **S3 Storage Classes Explained:**  
  https://www.youtube.com/watch?v=BYW-HCr3Qbc

* **AWS Storage Gateway Deep Dive:**  
  https://www.youtube.com/watch?v=9wgaV70FeaM

* **AWS Snow Family Overview:**  
  https://www.youtube.com/watch?v=YXn8Q_Hpsu4

* **AWS Backup Tutorial:**  
  https://www.youtube.com/watch?v=dCy7ixko3tE

* **Amazon FSx for Windows File Server:**  
  https://www.youtube.com/watch?v=CW2hz-Uy7Gg

* **S3 Static Website with CloudFront:**  
  https://www.youtube.com/watch?v=mls8tiiI3uc

* **VM Migration to AWS:**  
  https://www.youtube.com/watch?v=afSJaFJsfXw

* **S3 Versioning and Replication:**  
  https://www.youtube.com/watch?v=4EOaAkY4pNE

* **AWS Storage Services Overview:**  
  https://www.youtube.com/watch?v=6vNC_BCqFmI

**Training Courses:**
* **AWS Skill Builder - S3 Primer:**  
  https://explore.skillbuilder.aws/learn/course/external/view/elearning/50/amazon-s3-primer

* **AWS Skill Builder - Storage Learning Plan:**  
  https://explore.skillbuilder.aws/learn/learning_plan/view/51/storage-learning-plan

* **AWS Training - Storage Fundamentals:**  
  https://aws.amazon.com/training/learn-about/storage/

* **Coursera - AWS Fundamentals: Migrating to the Cloud:**  
  https://www.coursera.org/learn/aws-fundamentals-migrating-to-the-cloud

* **A Cloud Guru - AWS Certified Solutions Architect:**  
  https://acloudguru.com/course/aws-certified-solutions-architect-associate-saa-c03

**Blog Posts and Articles:**
* **AWS Storage Blog:**  
  https://aws.amazon.com/blogs/storage/

* **S3 Best Practices:**  
  https://aws.amazon.com/blogs/storage/best-practices-for-amazon-s3/

* **Optimizing S3 Performance:**  
  https://aws.amazon.com/blogs/storage/optimizing-amazon-s3-performance/

* **S3 Security Best Practices:**  
  https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/

* **Hybrid Cloud Storage with Storage Gateway:**  
  https://aws.amazon.com/blogs/storage/hybrid-cloud-storage-with-aws-storage-gateway/

* **Data Migration Strategies:**  
  https://aws.amazon.com/blogs/storage/aws-data-migration-strategies/

* **Disaster Recovery Strategies:**  
  https://aws.amazon.com/blogs/publicsector/rapidly-recover-mission-critical-systems-in-a-disaster/

**Whitepapers:**
* **AWS Storage Services Overview:**  
  https://docs.aws.amazon.com/whitepapers/latest/aws-storage-services-overview/

* **Cost Optimization for Storage:**  
  https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-storage-optimization/

* **Backup and Recovery Approaches Using AWS:**  
  https://docs.aws.amazon.com/whitepapers/latest/backup-recovery-approaches-using-aws/

* **Hybrid Cloud Storage Architecture:**  
  https://docs.aws.amazon.com/whitepapers/latest/hybrid-cloud-with-aws/storage.html

**Tools and Calculators:**
* **AWS Pricing Calculator:**  
  https://calculator.aws/

* **S3 Storage Lens:**  
  https://aws.amazon.com/s3/storage-lens/

* **AWS Total Cost of Ownership (TCO) Calculator:**  
  https://aws.amazon.com/tco-calculator/

**Community Resources:**
* **AWS re:Post (Community Forum):**  
  https://repost.aws/

* **AWS Samples GitHub:**  
  https://github.com/aws-samples

* **Reddit - r/aws:**  
  https://www.reddit.com/r/aws/

* **Stack Overflow - AWS Tags:**  
  https://stackoverflow.com/questions/tagged/amazon-web-services

**Best Practices Guides:**
* **S3 Security Best Practices:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html

* **AWS Well-Architected Framework - Storage:**  
  https://docs.aws.amazon.com/wellarchitected/latest/framework/storage.html

* **Data Protection in S3:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html

* **AWS Backup Best Practices:**  
  https://docs.aws.amazon.com/prescriptive-guidance/latest/backup-recovery/backup.html

**Hands-on Labs and Workshops:**
* **AWS Workshops - Storage:**  
  https://workshops.aws/categories/Storage

* **AWS Hands-on Tutorials:**  
  https://aws.amazon.com/getting-started/hands-on/

* **QwikLabs - AWS Storage:**  
  https://www.qwiklabs.com/catalog?keywords=aws+storage

**Certification Resources:**
* **AWS Certified Solutions Architect - Associate Exam Guide:**  
  https://aws.amazon.com/certification/certified-solutions-architect-associate/

* **AWS Certification Practice Questions:**  
  https://explore.skillbuilder.aws/learn/course/external/view/elearning/13266/aws-certified-solutions-architect-associate-official-practice-question-set

**Additional Resources:**
* **AWS Architecture Center:**  
  https://aws.amazon.com/architecture/

* **AWS Reference Architectures:**  
  https://aws.amazon.com/architecture/reference-architecture-diagrams/

* **AWS Quick Starts:**  
  https://aws.amazon.com/quickstart/

* **AWS Solutions Library:**  
  https://aws.amazon.com/solutions/
