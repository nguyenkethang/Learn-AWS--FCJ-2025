---
title: "Week 5 Worklog"
date: 2025-10-12
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Understand the **Shared Responsibility Model** and the division of security responsibilities between **AWS** and the **customer**.  
* Learn about **AWS Identity and Access Management (IAM)**: user, group, and role management, and permission mechanisms.  
* Gain knowledge of **Amazon Cognito**: User Pool, Identity Pool, and authentication/authorization mechanisms for accessing AWS services.  
* Get an overview of other security and access management services: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS Key Management Service (KMS)**, and **AWS Security Hub**.
* Practice hands-on labs on IAM, Security Hub, KMS, and resource management with Tags.

---

### Tasks Performed During the Week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the **Shared Responsibility Model** and analyze the security responsibility boundaries between AWS and the customer. | 2025/10/06 | 2025/10/06 | [AWS Shared Responsibility Model Documentation](https://aws.amazon.com/compliance/shared-responsibility-model/) |
| 2 | - Research **IAM**: Root account, User, Group, Role, Federated User, and **STS** (Security Token Service). | 2025/10/07 | 2025/10/07 | [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html), [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 3 | - Study **IAM Policies**: JSON structure, identity-based and resource-based policies, and the **Explicit Deny** rule precedence. | 2025/10/08 | 2025/10/08 | [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html), [Policy Evaluation Logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) |
| 4 | - Learn about **Amazon Cognito**: User Pool (authentication), Identity Pool (authorization), and integration with third-party logins such as Facebook/Google/Amazon. | 2025/10/09 | 2025/10/09 | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/), [Cognito User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html) |
| 5 | - Explore advanced access and security management services: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS KMS**, and **AWS Security Hub**. | 2025/10/10 | 2025/10/10 | [AWS Security Hub Docs](https://docs.aws.amazon.com/securityhub/), [AWS KMS Docs](https://docs.aws.amazon.com/kms/), [AWS Identity Center Docs](https://docs.aws.amazon.com/singlesignon/), [AWS Organizations Docs](https://docs.aws.amazon.com/organizations/) |
| 6 | - Practice **Lab 18, 22, 27**: Security Hub, Lambda automation, Resource Tagging. | 2025/10/11 | 2025/10/11 | [AWS Tagging Strategies](https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html), [Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html) |
| 7 | - Practice **Lab 28, 30, 33, 44, 48**: IAM Policies, KMS encryption, CloudTrail logging. | 2025/10/12 | 2025/10/12 | [CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/), [KMS Best Practices](https://docs.aws.amazon.com/kms/latest/developerguide/best-practices.html), [Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/what-is.html) |

---

### Module List:

#### **Theory:**
- Module 05-01: Share Responsibility Model
- Module 05-02: Amazon Identity and Access Management
- Module 05-03: Amazon Cognito
- Module 05-04: AWS Organization
- Module 05-05: AWS Identity Center
- Module 05-06: Amazon Key Management Service
- Module 05-07: AWS Security Hub
- Module 05-08: Hands-on and Additional research

#### **Hands-on Labs:**

**Lab 18 - Security Hub:**
- Module 05-Lab18-02: Enable Security Hub
- Module 05-Lab18-03: Score for each set of criteria
- Module 05-Lab18-04: Clean up resources

**Lab 22 - Lambda Automation with Slack:**
- Module 05-Lab22-2.1: Create VPC
- Module 05-Lab22-2.2: Create Security Group
- Module 05-Lab22-2.3: Create EC2 instance
- Module 05-Lab22-2.4: Incoming Web-hooks slack
- Module 05-Lab22-3: Create Tag for Instance
- Module 05-Lab22-4: Create Role for Lambda
- Module 05-Lab22-5.1: Function stop instance
- Module 05-Lab22-5.2: Function start instance
- Module 05-Lab22-6: Check Result
- Module 05-Lab22-7: Clean up resources

**Lab 27 - Resource Tagging:**
- Module 05-Lab27-2.1.1: Create EC2 Instance with tag
- Module 05-Lab27-2.1.2: Managing Tags in AWS Resources
- Module 05-Lab27-2.1.3: Filter resources by tag
- Module 05-Lab27-2.2: Using tags with CLI
- Module 05-Lab27-3: Create a Resource Group
- Module 05-Lab27-4: Clean up resources

**Lab 28 - IAM Policy and Role:**
- Module 05-Lab28-2.1: Create IAM user
- Module 05-Lab28-3: Create IAM Policy
- Module 05-Lab28-4: Create IAM Role
- Module 05-Lab28-5.1: Switch Roles
- Module 05-Lab28-5.2.1: Initiating access to EC2 console in AWS Region - Tokyo
- Module 05-Lab28-5.2.2: Initiating access to EC2 console in AWS Region - North Virginia
- Module 05-Lab28-5.2.3: Proceed to create EC2 instance when there are no and qualified Tags
- Module 05-Lab28-5.2.4: Edit Resource Tag on EC2 Instance
- Module 05-Lab28-5.2.5: Policy Check
- Module 05-Lab28-6: Clean up resources

**Lab 30 - IAM User Restrictions:**
- Module 05-Lab30-3: Create Restriction Policy
- Module 05-Lab30-4: Create IAM Limited User
- Module 05-Lab30-5: Test IAM User Limits
- Module 05-Lab30-6: Clean up resources

**Lab 33 - KMS and CloudTrail:**
- Module 05-Lab33-2.1: Create Policy and Role
- Module 05-Lab33-2.2: Create Group and User
- Module 05-Lab33-3: Create Key Management Service
- Module 05-Lab33-4.1: Create Bucket
- Module 05-Lab33-4.2: Upload data to S3
- Module 05-Lab33-5.1: Create CloudTrail
- Module 05-Lab33-5.2: Logging to CloudTrail
- Module 05-Lab33-5.3: Create Amazon Athena
- Module 05-Lab33-5.4: Retrieve data with Athena
- Module 05-Lab33-6: Test and share encrypted data on S3
- Module 05-Lab33-7: Resource cleanup

**Lab 44 - IAM Group and Switch Role:**
- Module 05-Lab44-2: Create IAM Group
- Module 05-Lab44-3.1: Create IAM Users
- Module 05-Lab44-3.2: Check permissions
- Module 05-Lab44-4.1: Create Admin IAM Role
- Module 05-Lab44-4.2: Configure Switch role
- Module 05-Lab44-4.3.1: Limit switch role by IP
- Module 05-Lab44-4.3.2: Limit switch role by Time
- Module 05-Lab44-5: Clean up resources

**Lab 48 - IAM Role for EC2:**
- Module 05-Lab48-1.1: Create EC2 Instance
- Module 05-Lab48-1.2: Create S3 bucket
- Module 05-Lab48-2.1: Generate IAM user and access key
- Module 05-Lab48-2.2: Use access key
- Module 05-Lab48-3.1: Create IAM role
- Module 05-Lab48-3.2: Using IAM role
- Module 05-Lab48-4: Clean up resources

---

### Weekly Achievements:

* Gained a clear understanding of the **Shared Responsibility Model** – AWS is responsible for securing the infrastructure, while customers are responsible for securing their data, applications, and configurations.  
* Learned the main components of **IAM**:
  * **Root account** has full permissions but should not be used frequently.  
  * **IAM User** has no permissions by default – permissions must be granted via **IAM Policies**.  
  * **IAM Group** helps manage multiple users with shared permissions.  
  * **IAM Role** grants temporary access through **Security Token Service (STS)**.  
* Understood the **IAM Policy** mechanism (JSON format), distinguishing between **Identity-based** and **Resource-based Policies**, and the rule **Explicit Deny > Allow**.  
* Acquired knowledge of **Amazon Cognito**:
  * **User Pool** is used for authentication and user account management.  
  * **Identity Pool** allows authenticated users to access AWS services directly.  
  * Cognito integrates with **IAM** for detailed access control and enhanced security.  
* Gained an overview of advanced security-related AWS services:
  * **AWS Organizations**: manage multiple AWS accounts under Organizational Units (OUs) and enforce **Service Control Policies (SCPs)** for maximum permission boundaries.  
  * **AWS Identity Center (SSO)**: centralized login and access management for multiple accounts and applications.  
  * **AWS KMS**: create, store, and manage encryption keys to protect data.  
  * **AWS Security Hub**: assess and aggregate security posture based on industry standards and best practices.
* Completed hands-on lab exercises:
  * **Lab 18**: Enabled and used Security Hub for security assessment.
  * **Lab 22**: Created Lambda functions to automatically start/stop EC2 instances with Slack webhooks.
  * **Lab 27**: Managed AWS resources using Tags and Resource Groups.
  * **Lab 28**: Created and tested IAM Policies, Roles, and Switch Role across regions.
  * **Lab 30**: Created IAM users with restricted permissions and tested limitations.
  * **Lab 33**: Encrypted S3 data with KMS, logging with CloudTrail, and querying with Athena.
  * **Lab 44**: Managed IAM Groups, Switch Role with IP and time restrictions.
  * **Lab 48**: Used IAM Role for EC2 instances instead of access keys.

---

### Week 5 Summary:

In Week 5, I shifted focus from using basic AWS services to **understanding and managing security on the AWS platform**.  
Studying the Shared Responsibility Model helped me clearly identify which security aspects are managed by AWS and which must be handled by the customer.  

Through **IAM** and **Amazon Cognito**, I learned how to manage identities, permissions, and user authentication in applications.  
In addition, exploring **AWS Organizations**, **Identity Center**, **KMS**, and **Security Hub** provided a broader perspective on access control, data encryption, and system-level security monitoring.  

Notably, this week I completed **8 hands-on labs** covering Security Hub, Lambda automation, Resource Tagging, IAM Policies, KMS encryption, and CloudTrail logging. These labs helped me apply theoretical knowledge to practice, understand proper security implementation, and avoid common mistakes such as using access keys instead of IAM Roles.

The knowledge gained this week forms a crucial foundation for implementing **secure, compliant, and AWS best-practice-aligned systems**.
