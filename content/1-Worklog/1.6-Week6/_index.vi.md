---
title: "Nhật ký công việc Tuần 6"
date: 2025-10-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hiểu các khái niệm cơ bản về **cơ sở dữ liệu** và sự khác biệt giữa cơ sở dữ liệu quan hệ và phi quan hệ.
* Tìm hiểu về **Amazon RDS** (Relational Database Service) và **Amazon Aurora** cho giải pháp cơ sở dữ liệu được quản lý.
* Khám phá **Amazon Redshift** cho kho dữ liệu và **Amazon ElastiCache** cho bộ nhớ đệm.
* Thực hành tạo và cấu hình RDS instance với VPC, security groups và subnet groups.
* Triển khai ứng dụng đơn giản kết nối với RDS và thực hiện sao lưu/khôi phục dữ liệu.

---

### Công việc thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Tìm hiểu **Khái niệm cơ sở dữ liệu**: cơ sở dữ liệu quan hệ và phi quan hệ, thuộc tính ACID, và các trường hợp sử dụng.<br>- Đọc tài liệu về các loại database khác nhau và khi nào nên dùng. | 2025/10/13 | 2025/10/13 | [AWS Database Services Overview](https://aws.amazon.com/products/databases/) |
| 2 | - Học về **Amazon RDS & Amazon Aurora**: tính năng, lợi ích, triển khai Multi-AZ và read replicas.<br>- Xem video hướng dẫn về cách thiết lập và cấu hình RDS. | 2025/10/14 | 2025/10/14 | [Amazon RDS User Guide](https://docs.aws.amazon.com/rds/), [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/) |
| 3 | - Khám phá **Amazon Redshift** cho kho dữ liệu và **Amazon ElastiCache** cho bộ nhớ đệm với Redis/Memcached.<br>- So sánh các trường hợp sử dụng cho các dịch vụ database khác nhau. | 2025/10/15 | 2025/10/15 | [Amazon Redshift Documentation](https://docs.aws.amazon.com/redshift/), [Amazon ElastiCache Documentation](https://docs.aws.amazon.com/elasticache/) |
| 4 | **Lab05 - Phần 1 (Lab05-2.1 đến Lab05-2.4):**<br>- Lab05-2.1: Tạo VPC với CIDR 10.0.0.0/16<br>- Lab05-2.2: Tạo EC2 Security Group (cho phép SSH port 22, HTTP port 80)<br>- Lab05-2.3: Tạo RDS Security Group (cho phép MySQL port 3306 từ EC2 SG)<br>- Lab05-2.4: Tạo DB Subnet Group với 2 subnet ở 2 AZ khác nhau | 2025/10/16 | 2025/10/16 | [Lab05-2.1 Create VPC](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html), [Lab05-2.2 EC2 Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html), [Lab05-2.3 RDS Security Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html), [Lab05-2.4 DB Subnet Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Subnets) |
| 5 | **Lab05 - Phần 2 (Lab05-3 đến Lab05-5):**<br>- Lab05-3: Tạo EC2 instance (Amazon Linux 2) trong public subnet<br>- Lab05-4: Tạo RDS MySQL database instance (db.t3.micro)<br>- Lab05-5: Application Deployment - SSH vào EC2, cài MySQL client, deploy ứng dụng và test kết nối đến RDS | 2025/10/17 | 2025/10/17 | [Lab05-3 Create EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html), [Lab05-4 Create RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MySQL.html), [Lab05-5 Deploy App](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html) |
| 6 | **Lab05 - Phần 3 (Lab05-6 đến Lab05-7):**<br>- Lab05-6: Backup and Restore - Tạo manual snapshot, thay đổi automated backup retention, thực hành restore từ snapshot<br>- Lab05-7: Clean up resources - Xóa RDS instances, EC2, DB Subnet Group, Security Groups, VPC | 2025/10/18 | 2025/10/18 | [Lab05-6 Backup & Restore](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html), [Lab05-7 Clean Up](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_DeleteInstance.html) |
| 7 | - Ôn tập các khái niệm di chuyển cơ sở dữ liệu: DMS (Database Migration Service), Schema Conversion Tool và best practices.<br>- Nghiên cứu các kịch bản migration: homogeneous và heterogeneous migrations. | 2025/10/19 | 2025/10/19 | [AWS Database Migration Service](https://docs.aws.amazon.com/dms/), [AWS Schema Conversion Tool](https://docs.aws.amazon.com/SchemaConversionTool/) |

---

### Kết quả đạt được trong tuần:

* Hiểu rõ sự khác biệt cơ bản giữa **cơ sở dữ liệu quan hệ** (SQL) và **cơ sở dữ liệu phi quan hệ** (NoSQL), và khi nào nên sử dụng từng loại.
* Nắm được các tính năng của **Amazon RDS**:
  * Dịch vụ cơ sở dữ liệu được quản lý hỗ trợ MySQL, PostgreSQL, MariaDB, Oracle và SQL Server.
  * **Triển khai Multi-AZ** cho tính khả dụng cao và tự động chuyển đổi dự phòng.
  * **Read replicas** để mở rộng khả năng đọc và cải thiện hiệu suất.
* Hiểu về **Amazon Aurora**:
  * Cơ sở dữ liệu tương thích MySQL và PostgreSQL với hiệu suất cao hơn tới 5 lần.
  * Tự động mở rộng dung lượng lưu trữ và kiến trúc phân tán cho tính khả dụng cao.
* Khám phá **Amazon Redshift** cho kho dữ liệu và phân tích, và **Amazon ElastiCache** để cải thiện hiệu suất ứng dụng với bộ nhớ đệm.
* Hoàn thành thành công các bài lab thực hành:
  * Tạo VPC với cấu hình mạng phù hợp cho triển khai RDS.
  * Cấu hình security groups để kiểm soát truy cập giữa EC2 và RDS instances.
  * Triển khai RDS database instance và kết nối với ứng dụng chạy trên EC2.
  * Thực hiện các thao tác sao lưu và khôi phục để bảo vệ dữ liệu.
* Nắm được tổng quan về các công cụ và chiến lược di chuyển cơ sở dữ liệu lên AWS.

---

### Tóm tắt tuần 6:

Trong tuần 6, em tập trung vào **các dịch vụ cơ sở dữ liệu trên AWS**, đặc biệt là **Amazon RDS** và các giải pháp cơ sở dữ liệu được quản lý.

Việc hiểu sự khác biệt giữa cơ sở dữ liệu quan hệ và phi quan hệ giúp em lựa chọn đúng loại cơ sở dữ liệu cho các yêu cầu ứng dụng khác nhau. Thông qua **Amazon RDS**, em đã học được cách AWS đơn giản hóa việc quản lý cơ sở dữ liệu bằng cách tự động xử lý sao lưu, vá lỗi và tính khả dụng cao.

Các bài lab thực hành đặc biệt hữu ích, khi em thực hành tạo một môi trường cơ sở dữ liệu hoàn chỉnh với VPC, security groups và RDS instances. Việc triển khai ứng dụng và kết nối với RDS giúp em có kinh nghiệm thực tế với các tình huống cơ sở dữ liệu thực tế.

Tìm hiểu về **Amazon Aurora**, **Redshift** và **ElastiCache** mở rộng hiểu biết của em về các dịch vụ cơ sở dữ liệu chuyên biệt cho các trường hợp sử dụng khác nhau – từ cơ sở dữ liệu giao dịch hiệu suất cao đến kho dữ liệu và giải pháp bộ nhớ đệm.

Kiến thức của tuần này rất quan trọng để xây dựng **các giải pháp cơ sở dữ liệu có khả năng mở rộng, đáng tin cậy và tuân theo kiến trúc tốt trên AWS**.

---

### Tài Liệu Tham Khảo:

**Lý thuyết & Khái niệm:**
* [AWS Database Services Overview](https://aws.amazon.com/products/databases/)
* [Amazon RDS User Guide](https://docs.aws.amazon.com/rds/)
* [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/)
* [Amazon Redshift Documentation](https://docs.aws.amazon.com/redshift/)
* [Amazon ElastiCache Documentation](https://docs.aws.amazon.com/elasticache/)

**Lab05 - Thực hành RDS:**
* [Lab05-2.1: Tạo VPC](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html)
* [Lab05-2.2: Tạo EC2 Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
* [Lab05-2.3: Tạo RDS Security Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html)
* [Lab05-2.4: Tạo DB Subnet Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Subnets)
* [Lab05-3: Khởi chạy EC2 Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
* [Lab05-4: Tạo RDS MySQL Database](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MySQL.html)
* [Lab05-5: Kết nối RDS từ EC2](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html)
* [Lab05-6: Sao lưu và Khôi phục RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html)
* [Lab05-7: Xóa tài nguyên RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_DeleteInstance.html)

**Database Migration (Lab43 - Tổng quan):**
* [AWS Database Migration Service (DMS)](https://docs.aws.amazon.com/dms/)
* [AWS Schema Conversion Tool (SCT)](https://docs.aws.amazon.com/SchemaConversionTool/)
* [DMS Best Practices](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_BestPractices.html)
