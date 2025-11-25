---
title: "Week 3 Worklog"
date: 2025-09-28
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---


### Week 3 Objectives:

* Understand **Amazon EC2** (Elastic Compute Cloud) fundamentals: Instance Types, AMI, Key Pair, EBS, Instance Store.
* Master the use of **User Data** and **Metadata** to automate EC2 configuration during initialization.
* Learn how **EC2 Auto Scaling** works to automatically add or remove instances based on demand.
* Practice Labs on **AWS Backup**, **Storage Gateway**, and **S3 Static Website** with CloudFront.

---

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                           | Start Date | Completion Date | Reference Material     |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ---------------------- |
| 1   | - Study Module 03-01: Compute VM on AWS <br>&emsp; + Module 03-01-01: Amazon EC2 - Instance Type <br>&emsp; + Module 03-01-02: Amazon EC2 - AMI / Backup / Key Pair <br>&emsp; + Module 03-01-03: Amazon EC2 - Elastic Block Store <br>&emsp; + Module 03-01-04: Amazon EC2 - Instance Store |  2025/09/22 |  2025/09/22      | https://docs.aws.amazon.com/ec2/ |
| 2   | - Study Module 03-01 (continued) <br>&emsp; + Module 03-01-05: Amazon EC2 - User Data <br>&emsp; + Module 03-01-06: Amazon EC2 - Meta Data <br>&emsp; + Module 03-01-07: Amazon EC2 - EC2 Auto Scaling <br> - Study Module 03-02: EC2 Autoscaling - EFS/FSx - Lightsail - MGN |  2025/09/23 |  2025/09/23      | https://docs.aws.amazon.com/autoscaling/ |
| 3   | - **Lab 13 - Part 1:** Deploy AWS Backup <br>&emsp; + Module 03-Lab13-01: Introduction <br>&emsp; + Module 03-Lab13-02.2: Deploy Infrastructure <br>&emsp; + Module 03-Lab13-03: Create Backup Plan |  2025/09/24 |  2025/09/24      | https://000013.awsstudygroup.com/ |
| 4   | - **Lab 13 - Part 2:** Test and Clean up <br>&emsp; + Module 03-Lab13-05: Test Restore <br>&emsp; + Module 03-Lab13-06: Clean up Resources <br> - **Lab 24 - Part 1:** Storage Gateway <br>&emsp; + Module 03-Lab24-01.1: Create S3 Bucket <br>&emsp; + Module 03-Lab24-01.2: Create EC2 for Storage Gateway |  2025/09/25 |  2025/09/25      | https://000024.awsstudygroup.com/ |
| 5   | - **Lab 24 - Part 2:** Configure Storage Gateway <br>&emsp; + Module 03-Lab24-02.1: Create Storage Gateway <br>&emsp; + Module 03-Lab24-02.2: Create File Shares <br> - **Lab 57 - Part 1:** S3 Static Website <br>&emsp; + Module 03-Lab57-02.1: Create S3 Bucket <br>&emsp; + Module 03-Lab57-02.2: Load Data <br>&emsp; + Module 03-Lab57-03: Enable Static Website Feature |  2025/09/26 |  2025/09/26      | https://000057.awsstudygroup.com/ |
| 6   | - **Lab 57 - Part 2:** Public Access and CloudFront <br>&emsp; + Module 03-Lab57-04: Configuring Public Access Block <br>&emsp; + Module 03-Lab57-05: Configuring Public Objects <br>&emsp; + Module 03-Lab57-06: Test Website <br>&emsp; + Module 03-Lab57-07.1: Block All Public Access <br>&emsp; + Module 03-Lab57-07.2: Config Amazon CloudFront <br>&emsp; + Module 03-Lab57-07.3: Test Amazon CloudFront |  2025/09/27 |  2025/09/27      | https://000057.awsstudygroup.com/ |
| 7   | - **Lab 57 - Part 3:** Versioning and Replication <br>&emsp; + Module 03-Lab57-08: Bucket Versioning <br>&emsp; + Module 03-Lab57-09: Move Objects <br>&emsp; + Module 03-Lab57-10: Replication Object Multi Region <br>&emsp; + Module 03-Lab57-11: Clean up Resources <br> - Write weekly report and review all learned content |  2025/09/28 |  2025/09/28      | https://000057.awsstudygroup.com/ |


---

### Week 3 Achievements:

* **Understanding AWS EC2 Concepts**:  
  * EC2 Instance Types and how to choose the right type for workloads.
  * AMI for instance initialization, Backup/Snapshot for data protection, Key Pair for secure access.
  * EBS (persistent block storage) and Instance Store (high-performance ephemeral storage).
  * User Data to automatically run scripts during initialization, Metadata to retrieve instance information.
  * EC2 Auto Scaling to automatically adjust the number of instances based on demand.

* **Exploring Storage and Compute Services**:  
  * EFS (Elastic File System) for Linux, FSx for Windows.
  * Amazon Lightsail for simple workloads with fixed pricing.
  * AWS MGN (Application Migration Service) to migrate on-premise servers to AWS.

* **Practical Skills Achieved**:  
  * **Lab 13 - AWS Backup:** Deployed infrastructure, created Backup Plan for EC2 and EBS, tested data recovery from backup.
  * **Lab 24 - Storage Gateway:** Created S3 Bucket, deployed EC2 for Storage Gateway, configured Storage Gateway and File Shares to connect on-premise storage with AWS.
  * **Lab 57 - S3 Static Website:** Created S3 Bucket, uploaded data, enabled Static Website feature, configured public access, integrated CloudFront for content acceleration, enabled Versioning and multi-region Replication.

---

### Week 3 Summary:

This week focused on AWS EC2 compute fundamentals and storage solutions. Started with understanding EC2 Instance Types, AMI, Key Pairs, and storage options like EBS and Instance Store. Learned about User Data to automate instance configuration and Metadata to retrieve instance information.

Studied EC2 Auto Scaling to automatically adjust capacity based on demand, helping optimize costs and ensure high availability. Explored complementary services like EFS, FSx, Lightsail, and MGN.

Key hands-on experience included deploying AWS Backup to automatically backup and restore EC2/EBS resources (Lab 13), configuring Storage Gateway to connect hybrid storage between on-premises and S3 (Lab 24), and creating S3 Static Website with CloudFront distribution, versioning, and multi-region replication (Lab 57).

This week provided essential knowledge of AWS compute and storage services, preparing for building scalable, resilient, and cost-effective cloud applications.

---

### Reference Materials:

**Workshop Labs:**
* **Lab 13 - Deploy AWS Backup:**  
  https://000013.awsstudygroup.com/

* **Lab 24 - Storage Gateway:**  
  https://000024.awsstudygroup.com/

* **Lab 57 - S3 Static Website with CloudFront:**  
  https://000057.awsstudygroup.com/

**AWS Official Documentation:**
* **Amazon EC2 User Guide:**  
  https://docs.aws.amazon.com/ec2/

* **EC2 Instance Types:**  
  https://aws.amazon.com/ec2/instance-types/

* **Amazon EBS Documentation:**  
  https://docs.aws.amazon.com/ebs/

* **EC2 Auto Scaling:**  
  https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html

* **AWS Backup:**  
  https://docs.aws.amazon.com/aws-backup/

* **AWS Storage Gateway:**  
  https://docs.aws.amazon.com/storagegateway/

* **Amazon S3 Static Website Hosting:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html

* **Amazon CloudFront:**  
  https://docs.aws.amazon.com/cloudfront/

* **Amazon EFS:**  
  https://docs.aws.amazon.com/efs/

* **Amazon FSx:**  
  https://docs.aws.amazon.com/fsx/

**Video Tutorials:**
* **AWS EC2 Complete Tutorial:**  
  https://www.youtube.com/watch?v=iHX-jtKIVNA

* **EC2 Auto Scaling Explained:**  
  https://www.youtube.com/watch?v=4EOaAkY4pNE

* **AWS Storage Services Overview:**  
  https://www.youtube.com/watch?v=6vNC_BCqFmI

* **S3 Static Website with CloudFront:**  
  https://www.youtube.com/watch?v=mls8tiiI3uc

**Additional Resources:**
* **EC2 Pricing Calculator:**  
  https://calculator.aws/

* **AWS Well-Architected Framework:**  
  https://aws.amazon.com/architecture/well-architected/

* **AWS Skill Builder - EC2 Course:**  
  https://explore.skillbuilder.aws/learn

* **EC2 Best Practices:**  
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html
