---
title: "Nhật ký công việc Tuần 5"
date: 2025-10-12
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Hiểu rõ mô hình **Trách nhiệm chia sẻ (Shared Responsibility Model)** và sự phân chia trách nhiệm bảo mật giữa **AWS** và **khách hàng**.  
* Tìm hiểu **AWS Identity and Access Management (IAM)**: quản lý người dùng, nhóm, vai trò (role) và cơ chế cấp quyền.  
* Nắm được kiến thức về **Amazon Cognito**: User Pool, Identity Pool và cơ chế xác thực / cấp quyền truy cập dịch vụ AWS.  
* Tổng quan các dịch vụ quản lý bảo mật và truy cập khác: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS Key Management Service (KMS)**, **AWS Security Hub**.
* Thực hành các bài lab về IAM, Security Hub, KMS, và quản lý tài nguyên với Tags.

---

### Công việc thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Tìm hiểu mô hình **Trách nhiệm chia sẻ (Shared Responsibility Model)** và phân tích ranh giới trách nhiệm giữa AWS và khách hàng. | 2025/10/06 | 2025/10/06 | [AWS Shared Responsibility Model Documentation](https://aws.amazon.com/compliance/shared-responsibility-model/) |
| 2 | - Nghiên cứu **IAM**: Tài khoản Root, người dùng (User), nhóm (Group), vai trò (Role), người dùng liên kết (Federated User) và dịch vụ **STS**. | 2025/10/07 | 2025/10/07 | [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html), [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 3 | - Tìm hiểu **Chính sách IAM (IAM Policy)**: cấu trúc JSON, chính sách dựa trên danh tính và tài nguyên, quy tắc ưu tiên **Explicit Deny**. | 2025/10/08 | 2025/10/08 | [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html), [Policy Evaluation Logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) |
| 4 | - Học về **Amazon Cognito**: User Pool (xác thực), Identity Pool (cấp quyền truy cập), đăng nhập qua Facebook/Google/Amazon. | 2025/10/09 | 2025/10/09 | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/), [Cognito User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html) |
| 5 | - Tìm hiểu các dịch vụ quản lý bảo mật nâng cao: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS KMS**, **AWS Security Hub**. | 2025/10/10 | 2025/10/10 | [AWS Security Hub Docs](https://docs.aws.amazon.com/securityhub/), [AWS KMS Docs](https://docs.aws.amazon.com/kms/), [AWS Identity Center Docs](https://docs.aws.amazon.com/singlesignon/), [AWS Organizations Docs](https://docs.aws.amazon.com/organizations/) |
| 6 | - Thực hành **Lab 18, 22, 27**: Security Hub, Lambda automation, Resource Tagging. | 2025/10/11 | 2025/10/11 | [AWS Tagging Strategies](https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html), [Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html) |
| 7 | - Thực hành **Lab 28, 30, 33, 44, 48**: IAM Policies, KMS encryption, CloudTrail logging. | 2025/10/12 | 2025/10/12 | [CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/), [KMS Best Practices](https://docs.aws.amazon.com/kms/latest/developerguide/best-practices.html), [Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/what-is.html) |

---

### Danh sách Module học tập:

#### **Lý thuyết:**
- Module 05-01: Share Responsibility Model
- Module 05-02: Amazon Identity and Access Management
- Module 05-03: Amazon Cognito
- Module 05-04: AWS Organization
- Module 05-05: AWS Identity Center
- Module 05-06: Amazon Key Management Service
- Module 05-07: AWS Security Hub
- Module 05-08: Hands-on and Additional research

#### **Thực hành:**

**Lab 18 - Security Hub:**
- Module 05-Lab18-02: Enable Security Hub
- Module 05-Lab18-03: Score for each set of criteria
- Module 05-Lab18-04: Clean up resources

**Lab 22 - Lambda Automation với Slack:**
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

**Lab 28 - IAM Policy và Role:**
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

**Lab 33 - KMS và CloudTrail:**
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

**Lab 44 - IAM Group và Switch Role:**
- Module 05-Lab44-2: Create IAM Group
- Module 05-Lab44-3.1: Create IAM Users
- Module 05-Lab44-3.2: Check permissions
- Module 05-Lab44-4.1: Create Admin IAM Role
- Module 05-Lab44-4.2: Configure Switch role
- Module 05-Lab44-4.3.1: Limit switch role by IP
- Module 05-Lab44-4.3.2: Limit switch role by Time
- Module 05-Lab44-5: Clean up resources

**Lab 48 - IAM Role cho EC2:**
- Module 05-Lab48-1.1: Create EC2 Instance
- Module 05-Lab48-1.2: Create S3 bucket
- Module 05-Lab48-2.1: Generate IAM user and access key
- Module 05-Lab48-2.2: Use access key
- Module 05-Lab48-3.1: Create IAM role
- Module 05-Lab48-3.2: Using IAM role
- Module 05-Lab48-4: Clean up resources

---

### Kết quả đạt được trong tuần:

* Hiểu rõ mô hình **Trách nhiệm chia sẻ (Shared Responsibility Model)** – AWS chịu trách nhiệm bảo vệ hạ tầng, còn khách hàng chịu trách nhiệm bảo mật dữ liệu, ứng dụng và cấu hình của mình.  
* Nắm được các thành phần chính của **IAM**:
  * **Root account** có toàn quyền nhưng không nên sử dụng thường xuyên.  
  * **IAM User** mặc định không có quyền – cần gán quyền qua **IAM Policy**.  
  * **IAM Group** giúp quản lý nhiều người dùng với cùng nhóm quyền.  
  * **IAM Role** cho phép cấp quyền truy cập tạm thời thông qua **Security Token Service (STS)**.  
* Hiểu cơ chế **IAM Policy** (dạng JSON), phân biệt giữa **Identity-based** và **Resource-based Policy**, đồng thời nắm quy tắc ưu tiên **Explicit Deny > Allow**.  
* Nắm được **Amazon Cognito**:
  * **User Pool** phục vụ xác thực và quản lý tài khoản người dùng.  
  * **Identity Pool** cho phép truy cập trực tiếp các dịch vụ AWS dựa trên danh tính đã xác thực.  
  * Cognito có thể kết hợp với **IAM** để quản lý quyền truy cập chi tiết và tăng cường bảo mật.  
* Hiểu tổng quan các dịch vụ bảo mật mở rộng:
  * **AWS Organizations**: quản lý nhiều tài khoản AWS theo đơn vị (OU) và áp dụng **Service Control Policy (SCP)** để giới hạn quyền tối đa.  
  * **AWS Identity Center (SSO)**: quản lý đăng nhập và phân quyền truy cập tập trung.  
  * **AWS KMS**: tạo, lưu trữ và quản lý khóa mã hóa bảo vệ dữ liệu.  
  * **AWS Security Hub**: đánh giá và tổng hợp tình trạng bảo mật theo tiêu chuẩn và best practices.
* Hoàn thành các bài lab thực hành:
  * **Lab 18**: Kích hoạt và sử dụng Security Hub để đánh giá bảo mật.
  * **Lab 22**: Tạo Lambda function tự động start/stop EC2 instance với Slack webhook.
  * **Lab 27**: Quản lý tài nguyên AWS bằng Tags và Resource Groups.
  * **Lab 28**: Tạo và kiểm tra IAM Policy, Role, và Switch Role giữa các region.
  * **Lab 30**: Tạo IAM user với quyền hạn chế và kiểm tra giới hạn.
  * **Lab 33**: Mã hóa dữ liệu S3 với KMS, logging với CloudTrail, và truy vấn với Athena.
  * **Lab 44**: Quản lý IAM Group, Switch Role với giới hạn IP và thời gian.
  * **Lab 48**: Sử dụng IAM Role cho EC2 instance thay vì access key.  

---

### Tóm tắt tuần 5:

Trong tuần 5, em đã chuyển trọng tâm từ việc sử dụng các dịch vụ cơ bản sang việc **hiểu và quản lý bảo mật trên nền tảng AWS**.  
Việc nghiên cứu mô hình chia sẻ trách nhiệm giúp em xác định rõ phạm vi bảo mật mà AWS đảm bảo và phần người dùng cần chủ động cấu hình.  

Thông qua **IAM** và **Amazon Cognito**, em đã hiểu rõ cách quản lý danh tính, phân quyền và xác thực người dùng trong ứng dụng.  
Ngoài ra, việc tìm hiểu **AWS Organizations**, **Identity Center**, **KMS** và **Security Hub** giúp em có cái nhìn tổng thể về việc kiểm soát truy cập, mã hóa dữ liệu và giám sát an ninh hệ thống.  

Đặc biệt, tuần này em đã hoàn thành **8 bài lab thực hành** bao gồm Security Hub, Lambda automation, Resource Tagging, IAM Policies, KMS encryption, và CloudTrail logging. Các bài lab này giúp em áp dụng kiến thức lý thuyết vào thực tế, hiểu rõ cách triển khai bảo mật đúng cách và tránh các lỗi phổ biến như sử dụng access key thay vì IAM Role.

Kiến thức của tuần này là nền tảng quan trọng cho việc triển khai hệ thống **an toàn, tuân thủ và theo chuẩn bảo mật AWS Best Practices**.
