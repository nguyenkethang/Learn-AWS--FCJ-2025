---
title: "Week 6 Worklog"
date: 2025-10-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Understand basic **database concepts** and the differences between relational and non-relational databases.
* Learn about **Amazon RDS** (Relational Database Service) and **Amazon Aurora** for managed database solutions.
* Explore **Amazon Redshift** for data warehousing and **Amazon ElastiCache** for in-memory caching.
* Practice creating and configuring RDS instances with VPC, security groups, and subnet groups.
* Deploy a simple application connecting to RDS and perform backup/restore operations.

---

### Tasks Performed During the Week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study **Database Concepts**: relational vs non-relational databases, ACID properties, and database use cases.<br>- Read documentation about different database types and when to use each. | 2025/10/13 | 2025/10/13 | [AWS Database Services Overview](https://aws.amazon.com/products/databases/) |
| 2 | - Learn about **Amazon RDS & Amazon Aurora**: features, benefits, Multi-AZ deployments, and read replicas.<br>- Watch tutorial videos about RDS setup and configuration. | 2025/10/14 | 2025/10/14 | [Amazon RDS User Guide](https://docs.aws.amazon.com/rds/), [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/) |
| 3 | - Explore **Amazon Redshift** for data warehousing and **Amazon ElastiCache** for caching with Redis/Memcached.<br>- Compare use cases for different database services. | 2025/10/15 | 2025/10/15 | [Amazon Redshift Documentation](https://docs.aws.amazon.com/redshift/), [Amazon ElastiCache Documentation](https://docs.aws.amazon.com/elasticache/) |
| 4 | **Lab05 - Part 1 (Lab05-2.1 to Lab05-2.4):**<br>- Lab05-2.1: Create VPC with CIDR 10.0.0.0/16<br>- Lab05-2.2: Create EC2 Security Group (allow SSH port 22, HTTP port 80)<br>- Lab05-2.3: Create RDS Security Group (allow MySQL port 3306 from EC2 SG)<br>- Lab05-2.4: Create DB Subnet Group with 2 subnets in different AZs | 2025/10/16 | 2025/10/16 | [Lab05-2.1 Create VPC](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html), [Lab05-2.2 EC2 Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html), [Lab05-2.3 RDS Security Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html), [Lab05-2.4 DB Subnet Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Subnets) |
| 5 | **Lab05 - Part 2 (Lab05-3 to Lab05-5):**<br>- Lab05-3: Create EC2 instance (Amazon Linux 2) in public subnet<br>- Lab05-4: Create RDS MySQL database instance (db.t3.micro)<br>- Lab05-5: Application Deployment - SSH to EC2, install MySQL client, deploy app and test RDS connection | 2025/10/17 | 2025/10/17 | [Lab05-3 Create EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html), [Lab05-4 Create RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MySQL.html), [Lab05-5 Deploy App](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html) |
| 6 | **Lab05 - Part 3 (Lab05-6 to Lab05-7):**<br>- Lab05-6: Backup and Restore - Create manual snapshot, modify automated backup retention, practice restore from snapshot<br>- Lab05-7: Clean up resources - Delete RDS instances, EC2, DB Subnet Group, Security Groups, VPC | 2025/10/18 | 2025/10/18 | [Lab05-6 Backup & Restore](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html), [Lab05-7 Clean Up](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_DeleteInstance.html) |
| 7 | - Review database migration concepts: DMS (Database Migration Service), Schema Conversion Tool, and migration best practices.<br>- Study migration scenarios: homogeneous vs heterogeneous migrations. | 2025/10/19 | 2025/10/19 | [AWS Database Migration Service](https://docs.aws.amazon.com/dms/), [AWS Schema Conversion Tool](https://docs.aws.amazon.com/SchemaConversionTool/) |

---

### Weekly Achievements:

* Understood the fundamental differences between **relational databases** (SQL) and **non-relational databases** (NoSQL), and when to use each type.
* Learned about **Amazon RDS** features:
  * Managed database service supporting MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server.
  * **Multi-AZ deployment** for high availability and automatic failover.
  * **Read replicas** for scaling read operations and improving performance.
* Gained knowledge of **Amazon Aurora**:
  * MySQL and PostgreSQL-compatible database with up to 5x performance improvement.
  * Automatic storage scaling and distributed architecture for high availability.
* Explored **Amazon Redshift** for data warehousing and analytics workloads, and **Amazon ElastiCache** for improving application performance with in-memory caching.
* Successfully completed hands-on labs:
  * Created VPC with proper network configuration for RDS deployment.
  * Configured security groups to control access between EC2 and RDS instances.
  * Deployed RDS database instance and connected it to an application running on EC2.
  * Performed backup and restore operations to protect database data.
* Gained overview of database migration tools and strategies for migrating databases to AWS.

---

### Week 6 Summary:

In Week 6, I focused on **database services on AWS**, particularly **Amazon RDS** and related managed database solutions.

Understanding the differences between relational and non-relational databases helped me choose the right database type for different application requirements. Through **Amazon RDS**, I learned how AWS simplifies database management by handling backups, patching, and high availability automatically.

The hands-on labs were particularly valuable, as I practiced creating a complete database environment with VPC, security groups, and RDS instances. Deploying an application and connecting it to RDS gave me practical experience with real-world database scenarios.

Learning about **Amazon Aurora**, **Redshift**, and **ElastiCache** expanded my understanding of specialized database services for different use cases – from high-performance transactional databases to data warehousing and caching solutions.

This week's knowledge is essential for building **scalable, reliable, and well-architected database solutions on AWS**.

---

### Reference Materials:

**Theory & Concepts:**
* [AWS Database Services Overview](https://aws.amazon.com/products/databases/)
* [Amazon RDS User Guide](https://docs.aws.amazon.com/rds/)
* [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/)
* [Amazon Redshift Documentation](https://docs.aws.amazon.com/redshift/)
* [Amazon ElastiCache Documentation](https://docs.aws.amazon.com/elasticache/)

**Lab05 - RDS Hands-on Practice:**
* [Lab05-2.1: Create VPC](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html)
* [Lab05-2.2: Create EC2 Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
* [Lab05-2.3: Create RDS Security Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html)
* [Lab05-2.4: Create DB Subnet Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Subnets)
* [Lab05-3: Launch EC2 Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
* [Lab05-4: Create RDS MySQL Database](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MySQL.html)
* [Lab05-5: Connect to RDS from EC2](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html)
* [Lab05-6: Backup and Restore RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html)
* [Lab05-7: Delete RDS Resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_DeleteInstance.html)

**Database Migration (Lab43 - Overview):**
* [AWS Database Migration Service (DMS)](https://docs.aws.amazon.com/dms/)
* [AWS Schema Conversion Tool (SCT)](https://docs.aws.amazon.com/SchemaConversionTool/)
* [DMS Best Practices](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_BestPractices.html)
