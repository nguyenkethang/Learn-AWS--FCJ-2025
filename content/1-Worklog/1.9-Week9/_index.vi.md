---
title: "Nhật ký công việc Tuần 9"
date: 2025-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Triển khai hạ tầng AWS hoàn chỉnh sử dụng CloudFormation (Infrastructure as Code)
* Cấu hình và triển khai ứng dụng backend Spring Boot lên EC2
* Triển khai pipeline tự động với systemd service
* Thiết lập kết nối cơ sở dữ liệu và xác minh tình trạng ứng dụng

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Nghiên cứu cấu trúc và cú pháp CloudFormation template <br> - Xem xét thiết kế kiến trúc VPC (public/private subnets) <br> - Hiểu cấu hình Auto Scaling Group và Load Balancer <br> - Chuẩn bị tham số triển khai (KeyPair, AMI ID, region) | 2025/11/03   | 2025/11/03      | Hướng dẫn Người dùng AWS CloudFormation <br> <https://docs.aws.amazon.com/cloudformation/> <br> Best Practices AWS VPC <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-best-practices.html> <br> Tài liệu Tham khảo CloudFormation Template <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html> |
| 2   | - Xác thực cú pháp CloudFormation template <br> - Triển khai infrastructure stack (VPC, EC2, RDS, ALB, S3, CloudFront) <br> - Giám sát tiến trình tạo stack và khắc phục lỗi <br> - Xác minh tất cả tài nguyên được tạo thành công | 2025/11/04   | 2025/11/04      | Tạo Stack AWS CloudFormation <br> <https://docs.aws.amazon.com/cloudformation/latest/userguide/cfn-console-create-stack.html> <br> Khắc phục sự cố CloudFormation <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/troubleshooting.html> |
| 3   | - Trích xuất outputs CloudFormation (RDS endpoint, ALB DNS, tên S3 bucket) <br> - Cấu hình Spring Boot application.properties với kết nối RDS <br> - Build file JAR backend sử dụng Maven <br> - Upload JAR lên S3 backend artifacts bucket | 2025/11/05   | 2025/11/05      | Spring Boot Configuration Properties <br> <https://docs.spring.io/spring-boot/reference/features/external-config.html> <br> Maven Build Lifecycle <br> <https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html> <br> Tài liệu AWS S3 CLI <br> <https://docs.aws.amazon.com/cli/latest/reference/s3/> |
| 4   | - Kết nối EC2 instance qua AWS Systems Manager Session Manager <br> - Tải JAR từ S3 xuống EC2 instance <br> - Cấu hình application properties trên EC2 <br> - Khởi động ứng dụng Spring Boot và xác minh health endpoint | 2025/11/06   | 2025/11/06      | AWS Systems Manager Session Manager <br> <https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html> <br> Spring Boot Actuator Health Endpoint <br> <https://docs.spring.io/spring-boot/reference/actuator/endpoints.html> |
| 5   | - Tạo file systemd service unit để tự động khởi động <br> - Cấu hình logging ứng dụng vào CloudWatch <br> - Kiểm tra ứng dụng qua Load Balancer và API Gateway <br> - Xác minh kết nối database và lưu trữ dữ liệu <br> - Tài liệu hóa quy trình triển khai và các bước khắc phục sự cố | 2025/11/07   | 2025/11/09      | Quản lý Systemd Service <br> <https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html> <br> AWS CloudWatch Logs Agent <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_GettingStarted.html> <br> Best Practices Spring Boot Production <br> <https://docs.spring.io/spring-boot/reference/deployment/installing.html> |

### Kết quả đạt được tuần 9:

**1. Triển khai Hạ tầng với CloudFormation:**
* Triển khai thành công infrastructure stack AWS hoàn chỉnh bao gồm:
  * **Kiến trúc VPC**: Tạo VPC với CIDR 10.0.0.0/16, 2 public subnets (10.0.1.0/24, 10.0.2.0/24), 2 private subnets (10.0.3.0/24, 10.0.4.0/24) trên 2 availability zones
  * **Thành phần Mạng**: Internet Gateway, NAT Gateway, Route Tables với cấu hình routing phù hợp
  * **Tài nguyên Tính toán**: EC2 Auto Scaling Group với t3.nano instances, Application Load Balancer với health checks
  * **Cơ sở dữ liệu**: RDS MySQL db.t3.micro instance trong private subnet với automated backups
  * **Lưu trữ & CDN**: S3 buckets cho frontend/backend, CloudFront distribution để phân phối nội dung toàn cầu
  * **Bảo mật**: Security Groups với quyền truy cập tối thiểu, IAM roles cho EC2 và các dịch vụ
  * **Quản lý API**: API Gateway REST API với VPC Link integration tới ALB

* Triển khai hoàn tất trong khoảng 18 phút với tất cả tài nguyên ở trạng thái khỏe mạnh

**2. Xác thực CloudFormation Template:**
* Xác thực cú pháp template sử dụng AWS CLI trước khi triển khai
* Xác định và giải quyết các vấn đề về tham số (tên KeyPair, AMI ID cho region)
* Triển khai các phụ thuộc tài nguyên phù hợp và thuộc tính DependsOn
* Sử dụng CloudFormation outputs để dễ dàng truy cập các định danh tài nguyên

**3. Cấu hình Ứng dụng Backend:**
* Cấu hình Spring Boot application.properties với:
  * Chuỗi kết nối RDS MySQL với SSL được bật
  * HikariCP connection pool (max 10, min 5 connections)
  * JPA Hibernate auto-update cho quản lý schema
  * Xác thực JWT với signing key bảo mật
  * Cấu hình CORS cho tích hợp frontend
  * Cấu hình logging CloudWatch

* Build file JAR production-ready (workshop-0.0.1-SNAPSHOT.jar, ~65MB)
* Upload JAR lên S3 backend artifacts bucket để kiểm soát phiên bản

**4. Triển khai và Cấu hình EC2:**
* Kết nối EC2 instance sử dụng AWS Systems Manager Session Manager (không cần SSH key)
* Tải ứng dụng JAR từ S3 về thư mục /opt/workshop
* Tạo application.properties với cấu hình theo môi trường cụ thể
* Khởi động ứng dụng Spring Boot thành công trên port 8080
* Xác minh health endpoint trả về `{"status":"UP"}`

**5. Triển khai Systemd Service:**
* Tạo file systemd service unit (/etc/systemd/system/workshop.service)
* Cấu hình tự động khởi động lại khi lỗi với độ trễ 10 giây
* Bật service để khởi động cùng hệ thống
* Triển khai logging phù hợp vào /opt/workshop/application.log
* Kiểm tra các thao tác start/stop/restart service

**6. Xác minh Ứng dụng:**
* **Kiểm tra Local**: Xác minh ứng dụng phản hồi trên localhost:8080
* **Kiểm tra Load Balancer**: Xác nhận ALB health checks đạt, traffic routing đúng
* **Kiểm tra API Gateway**: Xác thực tích hợp API Gateway với backend
* **Kết nối Database**: Xác nhận kết nối RDS thành công, queries thực thi đúng
* **CloudWatch Logs**: Xác minh logs ứng dụng streaming vào CloudWatch Logs group

**7. Thông tin Chi tiết Tối ưu Chi phí:**
* Xác định NAT Gateway là thành phần chi phí cao nhất (~$32/tháng)
* Nghiên cứu VPC Endpoints như giải pháp thay thế để giảm sử dụng NAT Gateway
* Lập kế hoạch triển khai S3, CloudWatch và SSM VPC Endpoints cho Tuần 10
* Ước tính tiết kiệm tiềm năng $20-25/tháng với VPC Endpoints

### Kết quả & Sản phẩm Tuần 9:

**Các Sản phẩm Hoàn thành:**
* ✅ Hạ tầng AWS hoàn chỉnh được triển khai qua CloudFormation
* ✅ Ứng dụng backend Spring Boot chạy trên EC2
* ✅ Cơ sở dữ liệu RDS MySQL được cấu hình và kết nối
* ✅ Application Load Balancer routing traffic tới backend
* ✅ API Gateway expose REST API bảo mật
* ✅ Systemd service để quản lý ứng dụng tự động
* ✅ CloudWatch logging và monitoring được cấu hình
* ✅ Tài liệu triển khai và hướng dẫn khắc phục sự cố

**Các Chỉ số Chính:**
* **Thời gian Triển khai Hạ tầng**: 18 phút
* **Thời gian Khởi động Ứng dụng Backend**: 12 giây
* **Tỷ lệ Thành công Health Check**: 100%
* **Thời gian Phản hồi API**: <200ms trung bình
* **Database Connection Pool**: 5 active, 10 max connections
* **Ước tính Chi phí Hàng tháng**: $8.90 (chưa tối ưu NAT Gateway)

**Công nghệ Đã Triển khai:**
* **Frontend**: S3 + CloudFront (chuẩn bị cho Tuần 10)
* **Backend**: Spring Boot 3.x trên EC2 t3.nano
* **Database**: RDS MySQL 8.0 db.t3.micro
* **Load Balancer**: Application Load Balancer
* **API Gateway**: REST API với VPC Link
* **Monitoring**: CloudWatch Logs và Metrics
* **IaC**: CloudFormation YAML template

### Bài học Kinh nghiệm:

**1. Lợi ích Infrastructure as Code:**
* **Bài học**: CloudFormation cho phép triển khai hạ tầng có thể lặp lại, được kiểm soát phiên bản
* **Áp dụng**: Template duy nhất triển khai toàn bộ stack trong 18 phút so với hàng giờ cấu hình thủ công
* **Rút ra**: IaC là thiết yếu cho môi trường production - cho phép khôi phục thảm họa, sao chép môi trường và audit trails

**2. Thiết kế Subnet VPC:**
* **Bài học**: Cách ly subnet public/private phù hợp rất quan trọng cho bảo mật
* **Áp dụng**: Đặt RDS trong private subnet không có truy cập internet, chỉ truy cập qua EC2 trong public subnet
* **Rút ra**: Không bao giờ expose database trực tiếp ra internet - sử dụng bastion hosts hoặc application servers làm trung gian

**3. Phụ thuộc CloudFormation:**
* **Bài học**: Thứ tự tạo tài nguyên quan trọng - phải sử dụng DependsOn để sắp xếp đúng
* **Áp dụng**: NAT Gateway phải tồn tại trước private subnet route table, RDS phải đợi subnet group
* **Rút ra**: Luôn ánh xạ các phụ thuộc tài nguyên trong CloudFormation để tránh lỗi tạo

**4. Quản lý Cấu hình Spring Boot:**
* **Bài học**: Tách cấu hình ra khỏi JAR cho các thiết lập theo môi trường
* **Áp dụng**: Sử dụng --spring.config.location để load properties từ /opt/workshop/application.properties
* **Rút ra**: Không bao giờ hardcode các giá trị theo môi trường trong code hoặc file JAR

**5. Quản lý Systemd Service:**
* **Bài học**: Systemd cung cấp quản lý process mạnh mẽ với tự động khởi động lại và logging
* **Áp dụng**: Cấu hình Restart=always với RestartSec=10 cho high availability
* **Rút ra**: Luôn sử dụng process managers (systemd, supervisord) cho ứng dụng production, không chạy thủ công

**6. AWS Systems Manager Session Manager:**
* **Bài học**: Session Manager loại bỏ nhu cầu SSH keys và bastion hosts
* **Áp dụng**: Kết nối EC2 instances an toàn mà không mở port 22 hoặc quản lý key pairs
* **Rút ra**: Session Manager an toàn hơn SSH - cung cấp audit logs, không quản lý key, hoạt động với private subnets

**7. Cấu hình Health Check:**
* **Bài học**: Endpoints health check phù hợp là thiết yếu cho routing traffic của load balancer
* **Áp dụng**: Sử dụng Spring Boot Actuator /actuator/health endpoint cho ALB health checks
* **Rút ra**: Luôn triển khai health check endpoints xác minh kết nối database và các phụ thuộc quan trọng

**8. Nhận thức Chi phí:**
* **Bài học**: NAT Gateway đắt (~$32/tháng) cho workloads nhỏ
* **Áp dụng**: Xác định VPC Endpoints là giải pháp thay thế hiệu quả chi phí cho truy cập dịch vụ AWS
* **Rút ra**: Luôn xem xét AWS Cost Explorer và xác định cơ hội tối ưu - VPC Endpoints có thể tiết kiệm 60-70% chi phí NAT

**9. Phương pháp Khắc phục Sự cố:**
* **Bài học**: Khắc phục sự cố có hệ thống tiết kiệm thời gian - kiểm tra logs, xác minh kết nối, test endpoints
* **Áp dụng**: Sử dụng CloudWatch Logs, systemd journalctl và lệnh curl để chẩn đoán vấn đề
* **Rút ra**: Thiết lập runbooks khắc phục sự cố và sử dụng phương pháp debugging có cấu trúc

**10. Tầm quan trọng Tài liệu:**
* **Bài học**: Tài liệu triển khai rõ ràng tăng tốc các lần triển khai tương lai và onboarding nhóm
* **Áp dụng**: Tài liệu hóa mọi bước với lệnh, outputs mong đợi và mẹo khắc phục sự cố
* **Rút ra**: Thời gian đầu tư vào tài liệu được đền đáp trong phản ứng sự cố và chuyển giao kiến thức
