---
title: "Week 3 Worklog"
date: 2025-09-28
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Understand the concept of **Amazon EC2** as a virtual/physical server in the cloud with fast provisioning, elasticity, and ability to handle various workloads such as web hosting, applications, and databases.  

* Learn about **EC2 Instance Types**, how CPU, memory, storage, and network configurations are defined, and how to choose appropriate types for different workloads. 

* Explore **AMI (Amazon Machine Image)**, **Key Pairs**, and backup with **Snapshots** for secure provisioning and management of EC2 instances.  

* Gain knowledge of EC2 storage options:  
  - **EBS (Elastic Block Store):** persistent, high-availability block storage.  
  - **Instance Store:** high-speed ephemeral NVMe disks for temporary data.
  - **EFS & FSx:** shared storage solutions for Linux and Windows environments. 

* Practice using **User Data** and **Metadata** to automate instance initialization and retrieve instance information.

* Learn how **EC2 Auto Scaling** works to dynamically add or remove instances based on demand, integrate with Elastic Load Balancer, and optimize costs. 

* Understand **EC2 Pricing Models** (On-Demand, Reserved, Savings Plans, Spot) and their use cases, along with additional compute services such as **Amazon Lightsail** and **AWS Application Migration Service (MGN)**. 

---

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                               | Start Date | Completion Date | Reference Material |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 1   | - Get familiar with the concept of **Amazon EC2**: compare with physical servers, advantages of fast provisioning, high elasticity, and typical workloads such as web hosting, databases, authentication services | 2025/09/22 | 2025/09/22     | <https://000027.awsstudygroup.com/> |
| 2   | - Learn about **Instance Types**: configuration of CPU (Intel/AMD/ARM/Graviton/GPU), Memory, Network, Storage <br> - Study **AMI** and how to launch multiple instances from one AMI | 2025/09/23 | 2025/09/23      | <https://000008.awsstudygroup.com/> |
| 3   | - Study **EBS (Elastic Block Store)**: block storage, replication in AZ, incremental snapshots, multi-attach with Nitro Hypervisor <br> - Compare EBS with **Instance Store**: high performance but data lost when instance is stopped | 09/24/2025 | 09/24/2025      | <https://000006.awsstudygroup.com/> |
| 4   | - Learn about **EC2 User Data**: scripts executed during provisioning, using bash for Linux and PowerShell for Windows <br> - Explore **EC2 Metadata**: private IP, hostname, security groups, etc. |  2025/09/25 |  2025/09/26      | <https://000004.awsstudygroup.com/> |
| 5   | - Study **EC2 Auto Scaling**: scale out when load increases, scale in when load decreases to save costs <br> - Learn how Auto Scaling integrates with Elastic Load Balancer and works across multiple AZs |  2025/09/26 |  2025/09/27      | <https://000045.awsstudygroup.com/> |
| 6   | - Explore **Pricing Options**: On-Demand, Reserved, Savings Plans, Spot Instances, and how to combine them in Auto Scaling <br> - Learn about **EFS** (network file system for Linux), **FSx** (SMB for Windows/Linux), and **Lightsail** for lightweight workloads |  2025/09/27 |  2025/09/28      | <https://000046.awsstudygroup.com/> |


---

### Week 3 Achievements:

* **Understood AWS EC2 concepts**:  
  * EC2 is comparable to virtual or physical servers but offers faster provisioning, elasticity, and high scalability:contentReference[oaicite:0]{index=0}.  
  * EC2 instances are defined by **Instance Types** (CPU, memory, storage, network capacity) and optimized for specific workloads such as compute-intensive, memory-intensive, or storage-heavy tasks:contentReference[oaicite:1]{index=1}.  
  * Learned about **AMI** for provisioning instances, backup with **snapshots**, and secure access with **Key Pairs**:contentReference[oaicite:2]{index=2}.  

* **Explored EC2 Storage options**:  
  * **EBS (Elastic Block Store):** persistent block storage, replicated within an Availability Zone, with snapshots stored in S3:contentReference[oaicite:3]{index=3}.  
  * **Instance Store:** high-speed ephemeral NVMe storage suited for caching, swap, or logs; data lost when the instance stops:contentReference[oaicite:4]{index=4}.  
  * **EFS (Elastic File System):** scalable shared storage for Linux instances.  
  * **FSx:** managed Windows NTFS file systems accessible over SMB:contentReference[oaicite:5]{index=5}.  

* **Learned EC2 Auto Scaling:**  
  * Auto Scaling dynamically adjusts instance counts based on demand (scale-out when load increases, scale-in to save costs when load decreases):contentReference[oaicite:6]{index=6}.  
  * Auto Scaling integrates with **Elastic Load Balancer (ELB)** and works across multiple Availability Zones:contentReference[oaicite:7]{index=7}.  

* **Explored EC2 Pricing Models**:contentReference[oaicite:8]{index=8}:  
  * **On-Demand:** pay-as-you-go, most flexible but costly.  
  * **Reserved Instances:** discounted long-term contracts (1–3 years).  
  * **Savings Plans:** flexible alternative with discounts not tied strictly to instance families.  
  * **Spot Instances:** lowest-cost option using spare capacity, but can be terminated with short notice.  

* **Hands-on skills achieved:**  
  * Created and configured AWS Free Tier account.  
  * Installed and configured AWS CLI (Access Key, Secret Key, Default Region).  
  * Used AWS CLI for operations:  
    - Check account & config info  
    - Retrieve AWS regions list  
    - Launch & monitor EC2 instances  
    - Manage key pairs and EBS volumes  
  * Practiced connecting to EC2 via SSH and attaching additional EBS volumes.  

* **Other Services Learned:**  
  * **Amazon Lightsail:** simplified compute option for lightweight workloads, predictable monthly pricing:contentReference[oaicite:9]{index=9}.  
  * **AWS Application Migration Service (MGN):** replicates on-prem servers to AWS EC2 for DR and migration:contentReference[oaicite:10]{index=10}.  

---

### Key Takeaways:

* EC2 is the backbone of AWS Compute services, providing flexibility in deployment and scaling.  
* Proper understanding of storage choices (EBS, Instance Store, EFS, FSx) is crucial for balancing cost, performance, and persistence.  
* Auto Scaling ensures high availability while optimizing cost efficiency.  
* Combining AWS Console (GUI) and AWS CLI (command-line) gives flexibility and automation power for managing resources.  
