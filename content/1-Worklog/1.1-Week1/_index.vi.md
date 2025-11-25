---
title: "Nhật ký công việc Tuần 1"
date: 2025-09-14
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Hiểu **Điện Toán Đám Mây** là gì và lợi ích của AWS.
* Tìm hiểu về **Hạ Tầng Toàn Cầu AWS**: Regions, Availability Zones, Edge Locations.
* Làm quen với **Công Cụ Quản Lý AWS**: Console, CLI, SDK, CloudFormation.
* Thực hành tạo tài khoản AWS, thiết lập MFA và quản lý IAM user.
* Học về **Tối Ưu Hóa Chi Phí AWS** và các gói AWS Support.
* Hoàn thành các bài lab về thiết lập tài khoản, budgets và support requests.

---

### Công việc thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | **Module 01-01 đến 01-02:**<br>- Tìm hiểu Điện Toán Đám Mây là gì và lợi ích<br>- Học điều gì tạo nên sự khác biệt của AWS so với các nhà cung cấp khác<br>- Hiểu giá trị và các trường hợp sử dụng AWS | 2025/09/08 | 2025/09/08 | [What is Cloud Computing?](https://aws.amazon.com/what-is-cloud-computing/), [AWS Overview](https://aws.amazon.com/what-is-aws/) |
| 2 | **Module 01-03 đến 01-04:**<br>- Học cách bắt đầu hành trình lên mây với AWS<br>- Tìm hiểu Hạ Tầng Toàn Cầu AWS: Regions, AZs, Edge Locations<br>- Hiểu cơ bản về AWS Well-Architected Framework | 2025/09/09 | 2025/09/09 | [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/), [Getting Started](https://aws.amazon.com/getting-started/) |
| 3 | **Module 01-05 & Lab01:**<br>- Học Công Cụ Quản Lý AWS: Console, CLI, SDK, CloudFormation<br>- **Lab01-01:** Tạo tài khoản AWS Free Tier<br>- **Lab01-02:** Thiết lập Virtual MFA Device cho root account<br>- **Lab01-03:** Tạo admin group và admin user<br>- **Lab01-04:** Cấu hình account authentication support | 2025/09/10 | 2025/09/10 | [AWS Management Console](https://aws.amazon.com/console/), [AWS CLI](https://aws.amazon.com/cli/), [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 4 | **Module 01-06 & Lab07 (Phần 1):**<br>- Học chiến lược Tối Ưu Hóa Chi Phí AWS<br>- Tìm hiểu về AWS Budgets và Cost Explorer<br>- **Lab07-01:** Create Budget by Template<br>- **Lab07-02:** Create Cost Budget Tutorial | 2025/09/11 | 2025/09/11 | [AWS Cost Management](https://aws.amazon.com/aws-cost-management/), [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/) |
| 5 | **Lab07 (Phần 2):**<br>- **Lab07-03:** Creating a Usage Budget in AWS<br>- **Lab07-04:** Creating a Reservation Instance (RI) Budget<br>- **Lab07-05:** Creating a Savings Plans Budget<br>- **Lab07-06:** Clean Up Budgets | 2025/09/12 | 2025/09/12 | [AWS Budgets User Guide](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html), [Savings Plans](https://aws.amazon.com/savingsplans/) |
| 6 | **Module 01-07 & Lab09 (Phần 1):**<br>- Học về các gói AWS Support và tùy chọn<br>- **Lab09-01:** Tìm hiểu AWS Support Packages (Basic, Developer, Business, Enterprise)<br>- **Lab09-02:** Hiểu các loại support requests | 2025/09/13 | 2025/09/13 | [AWS Support Plans](https://aws.amazon.com/premiumsupport/plans/), [AWS Support](https://aws.amazon.com/premiumsupport/) |
| 7 | **Lab09 (Phần 2) & Ôn tập:**<br>- **Lab09-03:** Change support package (thực hành)<br>- **Lab09-04:** Manage support requests<br>- Ôn tập tất cả khái niệm và labs của Module 01<br>- Thực hành bài tập bổ sung | 2025/09/14 | 2025/09/14 | [AWS Support Center](https://console.aws.amazon.com/support/), [AWS Documentation](https://docs.aws.amazon.com/) |

---

### Kết quả đạt được trong tuần:

* Hiểu rõ các khái niệm cơ bản về **Điện Toán Đám Mây** và tại sao AWS là nhà cung cấp đám mây hàng đầu.
* Nắm được về **Hạ Tầng Toàn Cầu AWS**:
  * **Regions**: Các vị trí địa lý với nhiều Availability Zones.
  * **Availability Zones (AZs)**: Các trung tâm dữ liệu độc lập cho tính khả dụng cao.
  * **Edge Locations**: Các điểm CDN cho CloudFront và phân phối nội dung.
* Hiểu về **Công Cụ Quản Lý AWS**:
  * **AWS Console**: Giao diện web để quản lý dịch vụ.
  * **AWS CLI**: Công cụ dòng lệnh cho tự động hóa.
  * **AWS SDK**: Thư viện lập trình để tích hợp ứng dụng.
  * **AWS CloudFormation**: Dịch vụ Infrastructure as Code (IaC).
* Hoàn thành thành công **Lab01** - Thiết lập tài khoản:
  * Tạo tài khoản AWS Free Tier với email và thanh toán phù hợp.
  * Cấu hình Virtual MFA Device để tăng cường bảo mật.
  * Tạo IAM admin group và admin user theo best practices.
  * Thiết lập account authentication support.
* Hoàn thành **Lab07** - AWS Budgets:
  * Tạo các loại budget khác nhau: Cost, Usage, RI và Savings Plans.
  * Học cách thiết lập cảnh báo và thông báo để kiểm soát chi phí.
  * Thực hành dọn dẹp budgets để tránh cảnh báo không cần thiết.
* Hoàn thành **Lab09** - AWS Support:
  * Hiểu các gói AWS Support khác nhau và lợi ích của chúng.
  * Học cách tạo và quản lý support requests.
  * Khám phá các tính năng của AWS Support Center.
* Nắm được các chiến lược và best practices về **Tối Ưu Hóa Chi Phí AWS**.

---

### Tóm tắt tuần 1:

Trong tuần 1, em tập trung vào **các kiến thức nền tảng về AWS và thiết lập tài khoản**. Việc hiểu Điện Toán Đám Mây là gì và cách AWS cung cấp các giải pháp có khả năng mở rộng, đáng tin cậy và tiết kiệm chi phí là nền tảng cho hành trình học tập của em.

Tìm hiểu về **Hạ Tầng Toàn Cầu AWS** giúp em hiểu cách AWS đạt được tính khả dụng cao và độ trễ thấp thông qua kiến trúc phân tán. Khái niệm về Regions, Availability Zones và Edge Locations rất quan trọng để thiết kế các ứng dụng có khả năng phục hồi.

Các bài lab thực hành cực kỳ hữu ích. Thông qua **Lab01**, em học được tầm quan trọng của các best practices về bảo mật như bật MFA và sử dụng IAM users thay vì root account. **Lab07** dạy em cách giám sát và kiểm soát chi phí AWS bằng Budgets, điều này rất quan trọng để tránh các khoản phí bất ngờ. **Lab09** giới thiệu cho em các tùy chọn AWS Support và cách nhận trợ giúp khi cần.

Hiểu về **Công Cụ Quản Lý AWS** cho em nhiều cách để tương tác với các dịch vụ AWS, từ Console thân thiện với người dùng đến CLI mạnh mẽ cho tự động hóa.

Kiến thức của tuần này tạo thành **nền tảng thiết yếu** để làm việc với AWS và chuẩn bị cho em thành công trong việc học các dịch vụ nâng cao hơn trong những tuần tới.

---

### Tài Liệu Tham Khảo:

**Điện Toán Đám Mây & AWS Cơ Bản:**
* [What is Cloud Computing?](https://aws.amazon.com/what-is-cloud-computing/)
* [What is AWS?](https://aws.amazon.com/what-is-aws/)
* [AWS Overview](https://aws.amazon.com/about-aws/)
* [Benefits of AWS](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)

**Hạ Tầng Toàn Cầu AWS:**
* [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)
* [Regions and Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)
* [AWS Edge Locations](https://aws.amazon.com/cloudfront/features/)

**Công Cụ Quản Lý AWS:**
* [AWS Management Console](https://aws.amazon.com/console/)
* [AWS CLI Documentation](https://aws.amazon.com/cli/)
* [AWS SDKs](https://aws.amazon.com/tools/)
* [AWS CloudFormation](https://aws.amazon.com/cloudformation/)

**Lab01 - Thiết Lập Tài Khoản:**
* [Create AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
* [Enable MFA for Root User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html)
* [IAM Users and Groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
* [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

**Lab07 - AWS Budgets:**
* [AWS Cost Management](https://aws.amazon.com/aws-cost-management/)
* [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/)
* [Create a Budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html)
* [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/)
* [AWS Savings Plans](https://aws.amazon.com/savingsplans/)

**Lab09 - AWS Support:**
* [AWS Support Plans](https://aws.amazon.com/premiumsupport/plans/)
* [AWS Support](https://aws.amazon.com/premiumsupport/)
* [AWS Support Center](https://console.aws.amazon.com/support/)
* [Create Support Cases](https://docs.aws.amazon.com/awssupport/latest/user/case-management.html)
