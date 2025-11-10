---
title: "Nhật ký công việc Tuần 5"
date: 2025-10-12
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Hiểu rõ mô hình **Trách nhiệm chia sẻ (Shared Responsibility Model)** và sự phân chia trách nhiệm bảo mật giữa **AWS** và **khách hàng**.  
* Tìm hiểu **AWS Identity and Access Management (IAM)**: quản lý người dùng, nhóm, vai trò (role) và cơ chế cấp quyền.  
* Nắm được kiến thức về **Amazon Cognito**: User Pool, Identity Pool và cơ chế xác thực / cấp quyền truy cập dịch vụ AWS.  
* Tổng quan các dịch vụ quản lý bảo mật và truy cập khác: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS Key Management Service (KMS)**, **AWS Security Hub**.  

---

### Công việc thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Tìm hiểu mô hình **Trách nhiệm chia sẻ (Shared Responsibility Model)** và phân tích ranh giới trách nhiệm giữa AWS và khách hàng. | 2025/10/06 | 2025/10/06 | [AWS Shared Responsibility Model Documentation](https://aws.amazon.com/compliance/shared-responsibility-model/) |
| 2 | - Nghiên cứu **IAM**: Tài khoản Root, người dùng (User), nhóm (Group), vai trò (Role), người dùng liên kết (Federated User) và dịch vụ **STS**. | 2025/10/07 | 2025/10/07 | [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| 3 | - Tìm hiểu **Chính sách IAM (IAM Policy)**: cấu trúc JSON, chính sách dựa trên danh tính và tài nguyên, quy tắc ưu tiên **Explicit Deny**. | 2025/10/08 | 2025/10/08 | [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) |
| 4 | - Học về **Amazon Cognito**: User Pool (xác thực), Identity Pool (cấp quyền truy cập), đăng nhập qua Facebook/Google/Amazon. | 2025/10/10 | 2025/10/10 | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/) |
| 5 | - Tìm hiểu các dịch vụ quản lý bảo mật nâng cao: **AWS Organizations**, **AWS Identity Center (SSO)**, **AWS KMS**, **AWS Security Hub**. | 2025/10/11 | 2025/10/11 | [AWS Security Hub Docs](https://docs.aws.amazon.com/securityhub/), [AWS KMS Docs](https://docs.aws.amazon.com/kms/), [AWS Identity Center Docs](https://docs.aws.amazon.com/singlesignon/), [AWS Organizations Docs](https://docs.aws.amazon.com/organizations/) |

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

---

### Tóm tắt tuần 5:

Trong tuần 5, em đã chuyển trọng tâm từ việc sử dụng các dịch vụ cơ bản sang việc **hiểu và quản lý bảo mật trên nền tảng AWS**.  
Việc nghiên cứu mô hình chia sẻ trách nhiệm giúp em xác định rõ phạm vi bảo mật mà AWS đảm bảo và phần người dùng cần chủ động cấu hình.  

Thông qua **IAM** và **Amazon Cognito**, em đã hiểu rõ cách quản lý danh tính, phân quyền và xác thực người dùng trong ứng dụng.  
Ngoài ra, việc tìm hiểu **AWS Organizations**, **Identity Center**, **KMS** và **Security Hub** giúp em có cái nhìn tổng thể về việc kiểm soát truy cập, mã hóa dữ liệu và giám sát an ninh hệ thống.  

Kiến thức của tuần này là nền tảng quan trọng cho việc triển khai hệ thống **an toàn, tuân thủ và theo chuẩn bảo mật AWS Best Practices**.
