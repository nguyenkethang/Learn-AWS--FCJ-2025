---
title: "Event 5"
date: 2025-11-29
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

## AWS WELL-ARCHITECTED SECURITY PILLAR WORKSHOP – MORNING SESSION

### 📍 Location & Time
- **Date:** November 29, 2025 (Morning Only)  
- **Time:** 08:30 AM – 12:00 PM  
- **Venue:** 26th Floor, Bitexco Financial Tower, 2 Hai Trieu Street, Ben Nghe Ward, District 1, Ho Chi Minh City

---

### 🎯 Workshop Objectives
- Deep dive into the AWS Well-Architected Framework – Security Pillar
- Explore best practices for securing cloud infrastructure across five key domains
- Learn from real-world scenarios and common pitfalls in Vietnamese enterprise environments
- Discover the roadmap for AWS security learning and certifications

---

## 🛡️ Session Breakdown

### 🔹 8:30 – 8:50 AM | Opening & Security Foundation
- Role of the Security Pillar in the Well-Architected Framework  
- Core principles: Least Privilege – Zero Trust – Defense in Depth  
- Shared Responsibility Model  
- Top cloud threats in Vietnam

---

### ⭐ Pillar 1 — Identity & Access Management (IAM)
**🕗 8:50 – 9:30 AM | Modern IAM Architecture**

**Speakers:**
- **Le Vu Xuan An** - AWS Cloud Club Captain HCMUTE, First Cloud AI Journey
- **Tran Duc Anh** - AWS Cloud Club Captain SGU, First Cloud AI Journey
- **Tran Doan Cong Ly** - AWS Cloud Club Captain PTIT, First Cloud AI Journey
- **Danh Hoang Hieu Nghi** - AWS Cloud Club Captain HUFLIT, First Cloud AI Journey

**Topics Covered:**
- IAM: Users, Roles, Policies – avoid long-term credentials  
- IAM Identity Center: SSO, permission sets  
- SCP & permission boundaries for multi-account setups  
- MFA, credential rotation, Access Analyzer  
- Mini Demo: Validate IAM Policy + simulate access

---

### ⭐ Pillar 2 — Detection
**🕘 9:30 – 9:55 AM | Detection & Continuous Monitoring**

**Speakers:**
- **Huynh Hoang Long** - AWS Community Builders
- **Dinh Le Hoang Anh** - AWS Community Builders

**Topics Covered:**
- CloudTrail (org-level), GuardDuty, Security Hub  
- Logging at all layers: VPC Flow Logs, ALB/S3 logs  
- Alerting & automation with EventBridge  
- Detection-as-Code (infrastructure + rules)

---

### ☕ 9:55 – 10:10 AM | Coffee Break

---

### ⭐ Pillar 3 — Infrastructure Protection
**🕙 10:10 – 10:40 AM | Network & Workload Security**

**Speakers:**
- **Tran Duc Anh** - AWS Cloud Club Captain SGU, Cloud Security Engineer Trainee, First Cloud AI Journey
- **Nguyen Tuan Thinh** - Cloud Engineer Trainee, First Cloud AI Journey
- **Nguyen Do Thanh Dat** - Cloud Engineer Trainee, First Cloud AI Journey

**Topics Covered:**
- VPC segmentation, private vs public placement  
- Security Groups vs NACLs: application models  
- WAF + Shield + Network Firewall  
- Workload protection: EC2, ECS/EKS security basics

---

### ⭐ Pillar 4 — Data Protection
**🕥 10:40 – 11:10 AM | Encryption, Keys & Secrets**

**Speakers:**
- **Thinh Lam** - FCJer
- **Viet Nguyen** - FCJer

**Topics Covered:**
- KMS: key policies, grants, rotation  
- Encryption at-rest & in-transit: S3, EBS, RDS, DynamoDB  
- Secrets Manager & Parameter Store — rotation patterns  
- Data classification & access guardrails

---

### ⭐ Pillar 5 — Incident Response
**🕚 11:10 – 11:40 AM | IR Playbook & Automation**

**Speaker:**
- **Mendel Grabski** - Secure by Design | Azure | Blockchain | Data Security

**Topics Covered:**
- IR lifecycle with AWS  
- Playbook scenarios:
  - Compromised IAM key  
  - S3 public exposure  
  - EC2 malware detection  
- Snapshot, isolation, evidence collection  
- Auto-response using Lambda/Step Functions

---

### 🔚 11:40 – 12:00 PM | Wrap-Up & Q&A
- Summary of the 5 pillars  
- Common pitfalls & enterprise realities in Vietnam  
- Roadmap for security learning (Security Specialty, SA Pro)

---

## 💡 Key Takeaways
- Strengthened understanding of AWS security architecture and operational best practices
- Learned how to apply layered defense strategies and automate detection and response
- Gained insights into IAM, logging, encryption, and incident response in real-world cloud environments
- Discovered practical tools and services to secure workloads and data across AWS
- Clarified learning paths and certifications to advance in cloud security

---

## 🧱 Advanced DNS & Network Security

### 🛡️ Route 53 Resolver DNS Firewall

#### Key Features
- **Block malicious domain access**: Based on deny/allow lists to prevent access to dangerous domains
- **Protect DNS queries**: Control DNS traffic from VPC, prevent DNS tunneling and exfiltration
- **Security Hub integration**: Send alerts when abnormal access is detected

#### Essential Knowledge
DNS queries from instances are sent to the resolver (VPC CIDR + 2 or 169.254.169.253).

The resolver categorizes queries:
- **Private DNS**: Internal queries within hosted zone
- **VPC DNS**: Queries to AWS resources (e.g., EC2)
- **Public DNS**: Queries to the internet

---

### 🔥 AWS Network Firewall

#### Primary Use Cases

**1. Egress Filtering**
- Block outbound access to malicious domains (FQDN, ccTLDs, TLS fingerprint)
- Validate legitimate ports/protocols
- Prevent direct communication to suspicious IPs

**2. Environment Segmentation**
- Isolate traffic between VPCs and dev/prod environments
- Control connectivity between on-premises and cloud

**3. Intrusion Prevention**
- Use rules from AWS or third parties to detect and block attacks
- Automatically block brute force IPs from GuardDuty

---

### 🌐 DNS Resolver Deployment Models

#### 🏢 Hybrid Network Deployment
- Connect enterprise network to AWS via Direct Connect
- DNS query flow: client → DNS resolver → AWS Route 53 resolver
- Support for Private DNS, Amazon Domains, and Public DNS
- Use inbound endpoint to receive queries from on-premises

#### ☁️ Cloud-Only Deployment
- Entire system resides in AWS Cloud
- Each Availability Zone has its own resolver
- DNS Firewall controls DNS queries from instances
- Support for internal and public domain resolution

---

### 🧩 Centralized Alerting & Normalization
- Security Hub CSPM normalizes data from GuardDuty, Inspector, etc. using ASFF (AWS Security Finding Format)
- Simplifies data analysis and filtering
- Supports centralized management across multiple accounts and regions

---

## 🧠 Advanced Detection & Practical Automation

### 🔍 GuardDuty – Three Pillars of Detection

| **Data Source**       | **What It Monitors**                          | **Real-World Scenario**                                  |
|-----------------------|-----------------------------------------------|----------------------------------------------------------|
| CloudTrail Events     | IAM actions, permission changes, API calls    | Hacker disables logging to hide tracks                   |
| VPC Flow Logs         | Network traffic to/from resources             | EC2 sends data to botnet C&C server                      |
| DNS Logs              | DNS queries from infrastructure               | Infected instance queries cryptocurrency mining pool     |

---

### 🛠️ Runtime Monitoring – "The All-Seeing Eye" in the OS

**GuardDuty Agent**: Lightweight software installed on EC2/EKS/ECS Fargate

**Deep Monitoring:**
- Which processes are running, who initiated them
- File access: who, when, which files
- System calls & permission changes
- Detect reverse shells, privilege escalation

---

### ⚡ EventBridge – Security Response Automation

#### 🔔 Real-time Findings
- GuardDuty detects threats → sends findings immediately to EventBridge

#### 🤖 Automated Remediation
Lambda automatically:
- Isolates infected EC2 instances
- Revokes IAM credentials
- Preserves evidence (snapshots, logs)

#### 🔄 Cross-account Routing
- Central security account receives findings from all member accounts

#### � Integratioon & Workflows
- Integrate with SNS, Slack, SQS to alert security teams

---

### 🧱 Detection-as-Code – DevSecOps Integration

- **IaC with CloudFormation/Terraform**: Deploy GuardDuty organization-wide
- **Custom Detection Rules**: Suppression rules, IP whitelisting to reduce false positives
- **Version-Controlled Logic**: Store rules in Git, integrate CI/CD for testing & deployment
- **Protection Plan Rollout**: Automate activation of protection layers like S3/EKS

---

### 🛡️ AWS Security Hub CSPM – Security Posture Management

#### Key Features
- **Automated Checks**: Automatically audit entire AWS environment
- **Consolidated Findings**: Aggregate findings from GuardDuty, Inspector, Macie, etc.
- **Prioritized Alerts**: Classify alerts by severity level
- **EventBridge Integration**: Send findings to ticketing/chat/email systems or automate remediation

---

### 🔐 Advanced Protection Plans

| **Feature**                 | **Details**                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| S3 Protection               | Detect abnormal access, scan malware on upload                              |
| EKS Protection              | Monitor Kubernetes audit logs, integrate with S3 for attack path analysis   |
| Extended Threat Detection   | Correlate discrete events into logical attack chains                        |

---

## 🧱 Incident Controls – Proactive Security Foundation

### 🔐 Core Components

#### AWS Organizations + SCPs
- Establish organization-wide guardrails
- Prevent privilege escalation from IAM policies

#### CloudTrail
- Log all API calls
- Enable in all regions to capture every event

#### AWS Config
- Continuous compliance monitoring
- Detect drift from standard configurations

#### GuardDuty
- ML-powered threat detection
- One-click activation across the organization

#### Security Hub
- Aggregate alerts from multiple security services
- Standardize compliance with CIS, PCI DSS, etc.

---

## 🛡️ Prevention – No Time for Incidents!

### � C5 Golden Rules

**1. Kill long-lived credentials**
- Use OIDC, IAM roles, temporary tokens
- Secrets in `.env` or Slack = high risk

**2. Never expose S3 directly**
- Use CloudFront, API Gateway, pre-signed URLs
- Public buckets = data breaches in the news

**3. No public IPs for sensitive resources**
- Redis, RDP, DB must be in private subnets
- The internet will find them faster than you think!

**4. Everything through IaC**
- No ClickOps
- Terraform/CDK + version control = better control

**5. Double-gate for dangerous changes**
- SCPs + PR approval + pipeline deploy
- No one has direct console write access to production

---

## 🧪 Hands-on Labs – Learning Through Practice

| **Lab Name**              | **Objective**                                      | **Key Techniques**                                   |
|----------------------------|---------------------------------------------------|------------------------------------------------------|
| EC2 IAM & Passwordless     | Eliminate SSH keys and DB passwords                | Session Manager, RDS IAM Auth, AssumeRole            |
| S3 Exposed & Remediation   | Detect and auto-remediate public S3 buckets        | EventBridge, Lambda, CloudFront OAC, SCPs            |
| EC2 Isolation              | Automatically isolate suspected infected EC2       | GuardDuty, Forensics, Network Isolation              |
| OIDC GitHub Federation     | Deploy from GitHub Actions without static AWS keys | OIDC, IAM Trust Policies, Least Privilege            |

🔗 **GitHub Labs**: [https://github.com/grabskimm/aws-labs](https://github.com/grabskimm/aws-labs)

---

## 🧩 CloudTrail & Multi-Layer Visibility

### 🔍 CloudTrail Organization-Level

- **Centralized Logging**: Log all API actions from all accounts in the AWS organization
- **Enterprise Scale Monitoring**: Detect abnormal behavior, comprehensive auditing, and post-incident forensics
- **EventBridge & Security Hub Integration**: Automate alerting and response

---

### � Multi-Layesr Security Visibility

| **Monitoring Layer**       | **Details**                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| Management Events          | Record API calls and console actions across all accounts                    |
| Data Events                | S3 object access, Lambda execution – track data at application layer        |
| Network Activity Events    | VPC Flow Logs – monitor network traffic, detect anomalies                   |
| Organization Coverage      | Unified logging across all regions and accounts – enhanced detection        |

---

## 🔐 Access Management & Identity Security

### 🔁 Credential Rotation – Secret Lifecycle Management

**AWS Secrets Manager** automates credential rotation (IAM, DB, API keys).

#### Rotation Process in 5 Steps:
1. `createSecret` – Create new secret
2. `setSecret` – Assign new secret to application
3. `testSecret` – Test new secret
4. `finishSecret` – Complete rotation process
5. `deletePreviousSecret` – Delete old secret after grace period

➡️ **EventBridge + Lambda**: Automate deletion of old secrets after rotation completion

---

### 🔐 Multi-Factor Authentication (MFA)

| **Method** | **Characteristics**                                                                 |
|------------|------------------------------------------------------------------------------------|
| **TOTP**   | Free, flexible backup, manual 6-digit code entry, uses shared secret               |
| **FIDO2**  | Uses public-key cryptography, touch or biometric authentication, high security, cannot recover if device is lost |

**Recommendations:**
- Use **FIDO2** for root accounts and administrators
- Use **TOTP** for regular users

---

### 🕵️ IAM Access Analyzer – Detect Risky Policies

- Detect policies containing `Principal: *` → Alert as potentially public
- Even with `Condition: SourceIP` → May still be considered public if constraints are insufficient

#### Integration with EventBridge + Lambda + SNS:
- Automatically add deny statement to IAM Role
- Send email alerts to security team

---

### 🎬 Demo & Practical Automation

**Presenters:**
- **Tran Duc Anh** – Cloud Security Engineer Trainee
- **Nguyen Tuan Thinh** – Cloud Engineer Trainee
- **Nguyen Do Thanh Dat** – Cloud Engineer Trainee

**Demo Content:**
- Integrate CloudTrail, GuardDuty, Security Hub
- Automate response using EventBridge → Lambda → SNS
- Analyze logs, detect abnormal behavior, send real-time alerts

---

## 📸 Workshop Highlights

![Security Workshop - Opening Session](images/image1.jpg?width=1500)
*Opening session at Bitexco Financial Tower*

---

![Security Workshop - IAM Presentation](images/image2.jpg?width=1500)
*Deep dive into Identity & Access Management*

---

![Security Workshop - Detection & Monitoring](images/image3.jpg?width=1500)
*Exploring GuardDuty and Security Hub*

---

![Security Workshop - Infrastructure Protection](images/image4.jpg?width=1500)
*Network security and workload protection discussion*

---

![Security Workshop - Hands-on Labs](images/image5.jpg?width=1500)
*Participants engaged in practical security labs*

---

![Security Workshop - Group Photo](images/image6.jpg?width=1500)
*AWS Well-Architected Security Pillar Workshop participants*

---

## 🎓 What You've Learned

Throughout this intensive morning session, you've gained comprehensive knowledge across the five pillars of AWS security:

**Identity & Access Management**
- Modern IAM architecture with temporary credentials and SSO
- Multi-account security with SCPs and permission boundaries
- MFA implementation and credential rotation strategies

**Detection & Monitoring**
- Organization-level CloudTrail for comprehensive API logging
- GuardDuty's ML-powered threat detection across multiple data sources
- Security Hub for centralized security posture management

**Infrastructure Protection**
- Network segmentation with VPCs, Security Groups, and NACLs
- DNS-layer security with Route 53 Resolver Firewall
- Advanced protection with AWS Network Firewall and WAF

**Data Protection**
- Encryption at-rest and in-transit across AWS services
- KMS key management and rotation policies
- Secrets Manager for automated credential lifecycle management

**Incident Response**
- Automated response workflows with EventBridge and Lambda
- Forensics and evidence collection techniques
- Isolation and remediation strategies for compromised resources

---

## 🚀 Your Journey Ahead

### Immediate Next Steps
1. **Practice the Labs**: Revisit the hands-on exercises at [github.com/grabskimm/aws-labs](https://github.com/grabskimm/aws-labs)
2. **Implement in Your Environment**: Start with quick wins like enabling GuardDuty and Security Hub
3. **Build Your Playbooks**: Create incident response runbooks for your organization

### Certification Path
- **AWS Certified Security – Specialty**: Deep dive into security best practices
- **AWS Certified Solutions Architect – Professional**: Comprehensive architectural knowledge including security

### Continuous Learning
- Join AWS Security community forums and user groups
- Follow AWS Security Blog for latest updates and best practices
- Participate in AWS Cloud Clubs and community events
- Contribute to open-source security tools and share your knowledge

### Real-World Application
- Audit your current AWS environment against Well-Architected Framework
- Implement Detection-as-Code in your CI/CD pipelines
- Establish security champions program in your organization
- Conduct regular security reviews and tabletop exercises

---

## 💬 Final Message

Security in the cloud is not a destination—it's a continuous journey of learning, adapting, and improving. The AWS Well-Architected Security Pillar provides a solid foundation, but the real value comes from applying these principles in your unique context.

**Remember:**
- Start small, but start today
- Automate everything you can
- Share knowledge with your team
- Stay curious and keep learning

The Vietnamese cloud community is growing stronger every day. By implementing these security practices, you're not just protecting your organization—you're contributing to a more secure cloud ecosystem for everyone.

**Thank you for your participation and dedication to cloud security excellence!**

---

> This workshop was a powerful reminder that security is not just a feature—it's a mindset and a continuous practice in cloud architecture.
