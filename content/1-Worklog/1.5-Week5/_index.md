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

---

### Tasks Performed During the Week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Study the **Shared Responsibility Model** and analyze the security responsibility boundaries between AWS and the customer. | 2025/10/06 | 2025/10/06 | [AWS Shared Responsibility Model Documentation](https://aws.amazon.com/compliance/shared-responsibility-model/) |
| 2 | - Research **IAM**: Root account, User, Group, Role, Federated User, and **STS** (Security Token Service). | 2025/10/07 | 2025/10/07 | [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| 3 | - Study **IAM Policies**: JSON structure, identity-based and resource-based policies, and the **Explicit Deny** rule precedence. | 2025/10/08 | 2025/10/08 | [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) |
| 4 | - Learn about **Amazon Cognito**: User Pool (authentication), Identity Pool (authorization), and integration with third-party logins such as Facebook/Google/Amazon. | 2025/10/09 | 2025/10/09 | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/) |
| 5 | - Explore advanced access and security management services: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS KMS**, and **AWS Security Hub**. | 2025/10/11 | 2025/10/11 | [AWS Security Hub Docs](https://docs.aws.amazon.com/securityhub/), [AWS KMS Docs](https://docs.aws.amazon.com/kms/), [AWS Identity Center Docs](https://docs.aws.amazon.com/singlesignon/), [AWS Organizations Docs](https://docs.aws.amazon.com/organizations/) |

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

---

### Week 5 Summary:

In Week 5, I shifted focus from using basic AWS services to **understanding and managing security on the AWS platform**.  
Studying the Shared Responsibility Model helped me clearly identify which security aspects are managed by AWS and which must be handled by the customer.  

Through **IAM** and **Amazon Cognito**, I learned how to manage identities, permissions, and user authentication in applications.  
In addition, exploring **AWS Organizations**, **Identity Center**, **KMS**, and **Security Hub** provided a broader perspective on access control, data encryption, and system-level security monitoring.  

The knowledge gained this week forms a crucial foundation for implementing **secure, compliant, and AWS best-practice-aligned systems**.
