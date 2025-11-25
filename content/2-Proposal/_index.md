---
title: "Proposal"
date: 2025-09-15
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Blood Donation Support System (BDSS)

## 1. Executive Summary

**Blood Donation Support System (BDSS)** is a web platform that supports the management and connection of blood donors with medical facilities. The project was developed by a group of students in Ho Chi Minh City to optimize the blood donation process, reduce the burden of finding donors, and improve healthcare communication effectiveness.

The system is built on **AWS Cloud architecture**, using **Amazon EC2**, **Amazon RDS**, **API Gateway**, **Cognito**, and **CI/CD Pipeline (GitLab + CodePipeline)** for automated deployment. BDSS supports four user groups (Guest, Member, Staff, Admin), providing features for searching, registering blood donations, managing blood inventory, tracking donation processes, and visual reporting.

---

## 2. Problem Statement

### Current Problem:
Medical facilities are currently managing the blood donation process manually or through disparate tools. Finding suitable blood donors by blood type or region is difficult, especially in emergency situations. Additionally, the data storage system is not synchronized, making it difficult to analyze, report, and optimize blood donation campaigns.

### Proposed Solution:
Develop a **comprehensive blood donation support platform on AWS Cloud**, with functions for managing blood donations, searching for donors and recipients by blood type or geographic location, integrating user authentication via Amazon Cognito, and data management on Amazon RDS.

Frontend is deployed via **Route 53 + CloudFront**, backend through **API Gateway – EC2**, MySQL database on **Amazon RDS**, and automated CI/CD pipeline using **GitLab – CodePipeline**.

### Benefits and ROI:
- Reduce 60–70% of time searching for suitable blood donors.
- Increase accuracy of blood type and location information.
- Optimize operating costs with flexible cloud architecture, pay-as-you-go pricing.
- Improve response capability in emergency blood situations.

---

## 3. Solution Architecture

### Overall Architecture:
![AWS Blood Donation Architecture](AWS%20architecture%20diagrams%20blood%20donation%20support%20systems.png)

The system is designed with a **3-tier architecture on AWS Cloud** with the following main components:

### 1. Frontend & Content Delivery Layer:
- **Users**: Users access the system via web browser or mobile.
- **Route 53**: DNS service managing domain name and routing traffic to CloudFront.
- **CloudFront**: CDN distributing static content with low latency, cached at edge locations.
- **Amazon S3**: Stores static assets (HTML, CSS, JS, images) for frontend application.

### 2. Application & Compute Layer:
- **API Gateway**: REST API endpoint, handling request/response between frontend and backend.
- **VPC (Virtual Private Cloud)**: Isolated virtual private network with configuration:
  - **Internet Gateway**: Allows public subnet to connect to Internet.
  - **Public Subnet**: Contains EC2 instances processing business logic.
  - **Private Subnet**: Contains RDS database, no direct Internet access.
  - **NAT Gateway**: Allows private subnet to access Internet one-way (outbound).
- **Amazon EC2**: Compute instances running backend API (Node.js/Express).
- **Amazon RDS (MySQL)**: Relational database storing blood donor data, blood types, donation history.

### 3. CI/CD & DevOps Pipeline:
- **GitLab**: Source code repository and version control.
- **AWS CodePipeline**: Orchestrate automated CI/CD workflow.
- **AWS CodeBuild**: Build and test code before deployment.
- **Automated Deployment**: Automatically deploy to EC2 when code changes.

### 4. Monitoring, Security & Management Layer:
- **Amazon Cognito**: User authentication and authorization (Guest, Member, Staff, Admin roles).
- **AWS IAM**: Manage access permissions for users and services.
- **AWS Secrets Manager**: Securely store database credentials and API keys.
- **Amazon CloudWatch**: Monitor metrics, logs, and create alarms.
- **AWS CloudTrail**: Audit logs for all API calls and user activities.
- **Amazon Athena**: Query and analyze logs from S3.
- **Amazon SNS**: Send notifications (email/SMS) for important events (emergency blood, suitable donors).

### System Workflow:
1. **User Access**: Users → Route 53 → CloudFront → S3 (Frontend)
2. **API Requests**: Frontend → API Gateway → EC2 (Backend) → RDS (Database)
3. **Data Flow**: EC2 instances in public subnet connect to RDS in private subnet
4. **Outbound Traffic**: Private subnet → NAT Gateway → Internet Gateway
5. **CI/CD Flow**: GitLab → CodePipeline → CodeBuild → EC2 deployment
6. **Monitoring**: CloudWatch collects metrics → SNS sends alerts → Athena analyzes logs

---

## 4. Technical Implementation

### Implementation Phases:

#### 1. Analysis & Design (Month 1)
- Gather requirements, identify use cases, design ERD and AWS architecture.

#### 2. Infrastructure & Pipeline Setup (Month 2)
- Configure Route 53, CloudFront, EC2, RDS and CI/CD on AWS.

#### 3. Development & Testing (Months 3–4)
- Build main modules: blood donation registration, search, blood inventory management.
- Integrate Cognito and SNS alert system.

#### 4. Deployment & Operations (Month 5)
- Deploy production system and monitor with CloudWatch.

### Main Technical Requirements:
- **Frontend:** React/Next.js or Angular (deploy via S3/CloudFront).
- **Backend:** Node.js/Express on EC2, communicate via REST API Gateway.
- **Database:** Amazon RDS MySQL, optimize queries and periodic backups.
- **CI/CD:** GitLab → CodeBuild → CodePipeline → EC2.
- **Auth:** Cognito (4 roles: Guest, Member, Staff, Admin).
- **Alert & Logs:** SNS + CloudWatch + CloudTrail.

---

## 5. Timeline & Milestones

| Timeline      | Phase                        | Main Results                                     |
| ------------- | ---------------------------- | ------------------------------------------------ |
| **Month 1**   | Requirements analysis & design | AWS architecture + use case diagram             |
| **Month 2**   | Infrastructure & pipeline setup | EC2, RDS, API Gateway operational              |
| **Month 3–4** | Development & testing        | Complete main modules                            |
| **Month 5**   | Production deployment        | System running stably with Dashboard reporting   |

---

## 6. Budget Estimation

| Service                         | Estimated cost/month (USD) | Notes                |
| ------------------------------- | -------------------------- | -------------------- |
| EC2 (t2.micro)                  | 3.50                       | Backend REST API     |
| Amazon RDS (MySQL)              | 2.80                       | 20 GB storage        |
| API Gateway                     | 0.50                       | 5,000 requests       |
| CloudFront + S3                 | 0.80                       | Website + CDN        |
| Route 53                        | 0.50                       | Domain & DNS         |
| Cognito                         | 0.10                       | <100 users           |
| CloudWatch + Logs               | 0.30                       | Monitoring & alerts  |
| CI/CD (CodePipeline, CodeBuild) | 0.40                       | Automated deployment |
| **Total**                       | **8.9 USD/month**          | ~106.8 USD/year      |

> All costs can be adjusted based on AWS Free Tier or using spot instances.

---

## 7. Risk Assessment

| Risk                       | Impact     | Probability | Mitigation Measures               |
| -------------------------- | ---------- | ----------- | --------------------------------- |
| Internet connection loss   | Medium     | Medium      | Backup on EC2                     |
| DDoS attack                | High       | Low         | AWS WAF + CloudFront              |
| User data error            | High       | Low         | RDS backup + IAM access control   |
| Budget overrun             | Medium     | Low         | AWS budget alerts                 |
| CI/CD deployment disruption| Low        | Medium      | Test pipeline before merge        |

---

## 8. Expected Outcomes

- **Technical:** Cloud-native system, automated CI/CD, multi-user support and high security.
- **Application:** Helps medical facilities manage blood donations effectively, minimizes manual processes.
- **Expansion:** Can be scaled to many other hospitals, integrate AI to analyze blood type demand or predict upcoming donation waves.
