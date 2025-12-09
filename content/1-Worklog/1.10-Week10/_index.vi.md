---
title: "Nhật ký công việc Tuần 10"
date: 2025-11-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Build và triển khai ứng dụng frontend React lên S3 và CloudFront
* Triển khai quy trình kiểm thử và xác thực toàn diện
* Cấu hình monitoring, logging và alerting với CloudWatch
* Tối ưu chi phí sử dụng VPC Endpoints và thực hiện xác minh hệ thống cuối cùng

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Cấu hình React frontend với API Gateway endpoint <br> - Cài đặt npm dependencies và giải quyết xung đột phiên bản <br> - Build production bundle với Vite <br> - Tối ưu kích thước bundle và assets | 2025/11/10   | 2025/11/10      | React Production Build <br> <https://react.dev/learn/start-a-new-react-project> <br> Tối ưu Vite Build <br> <https://vitejs.dev/guide/build.html> <br> Best Practices Hiệu suất Web <br> <https://web.dev/fast/> |
| 2   | - Upload frontend build lên S3 bucket <br> - Cấu hình S3 bucket cho static website hosting <br> - Thiết lập cache-control headers phù hợp cho assets <br> - Tạo CloudFront invalidation để làm mới cache | 2025/11/11   | 2025/11/11      | Amazon S3 Static Website Hosting <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html> <br> CloudFront Invalidation <br> <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html> <br> Best Practices HTTP Caching <br> <https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching> |
| 3   | - Thực hiện kiểm thử end-to-end toàn bộ ứng dụng <br> - Kiểm tra luồng xác thực người dùng với Cognito <br> - Xác thực chức năng phân tích DNA <br> - Kiểm tra cấu hình CORS và tích hợp API <br> - Xác minh responsive design trên nhiều thiết bị | 2025/11/12   | 2025/11/12      | AWS Cognito User Authentication <br> <https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html> <br> Khắc phục sự cố CORS <br> <https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS> <br> Hướng dẫn Browser DevTools <br> <https://developer.chrome.com/docs/devtools/> |
| 4   | - Cấu hình CloudWatch Logs cho application và access logs <br> - Tạo CloudWatch Alarms cho CPU, memory và error rates <br> - Thiết lập SNS notifications cho cảnh báo quan trọng <br> - Cấu hình CloudWatch Dashboard để giám sát hệ thống | 2025/11/13   | 2025/11/13      | Amazon CloudWatch Logs <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html> <br> CloudWatch Alarms <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html> <br> CloudWatch Dashboards <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html> |
| 5   | - Triển khai VPC Endpoints cho S3, CloudWatch và SSM <br> - Loại bỏ phụ thuộc NAT Gateway để tối ưu chi phí <br> - Cập nhật route tables và security groups <br> - Xác minh chức năng ứng dụng sau khi triển khai VPC Endpoint <br> - Tính toán tiết kiệm chi phí và tài liệu hóa kiến trúc cuối cùng | 2025/11/14   | 2025/11/16      | AWS VPC Endpoints <br> <https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html> <br> Giá VPC Endpoint <br> <https://aws.amazon.com/privatelink/pricing/> <br> Best Practices Tối ưu Chi phí AWS <br> <https://aws.amazon.com/architecture/cost-optimization/> <br> AWS Well-Architected Cost Optimization Pillar <br> <https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html> |

### Kết quả đạt được tuần 10:

**1. Triển khai Frontend lên S3 và CloudFront:**
* Cấu hình ứng dụng React với biến môi trường:
  * URL API Gateway endpoint
  * Tên và phiên bản ứng dụng
  * Thiết lập theo môi trường cụ thể

* Build bundle tối ưu production:
  * JavaScript và CSS được minified
  * Code splitting cho lazy loading
  * Tối ưu images và assets
  * Kích thước bundle giảm xuống ~2.5MB (gzipped: ~800KB)

* Upload frontend lên S3 với cache headers phù hợp:
  * Static assets (JS, CSS, images): max-age=31536000 (1 năm)
  * index.html: no-cache, no-store, must-revalidate
  * Bật S3 bucket versioning cho khả năng rollback

* Tạo CloudFront invalidation để làm mới nội dung cached
* Xác minh frontend truy cập được qua CloudFront URL với độ trễ thấp (<100ms toàn cầu)

**2. Kiểm thử Ứng dụng End-to-End:**
* **Kiểm thử Xác thực**:
  * Đăng ký người dùng với xác minh email
  * Chức năng đăng nhập/đăng xuất
  * Cơ chế làm mới JWT token
  * Kiểm soát truy cập theo vai trò (Guest, Member, Staff, Admin)

* **Kiểm thử Phân tích DNA**:
  * Chức năng upload file (định dạng FASTA)
  * Xác thực chuỗi DNA
  * Xử lý phân tích và hiển thị kết quả
  * Truy xuất lịch sử và kết quả

* **Kiểm thử Tích hợp**:
  * Giao tiếp API Frontend-Backend
  * Các thao tác CRUD database
  * Xử lý lỗi và phản hồi người dùng
  * Xác thực cấu hình CORS

* **Kiểm thử Hiệu suất**:
  * Thời gian tải trang: <2 giây
  * Thời gian phản hồi API: <200ms trung bình
  * Xử lý người dùng đồng thời: 50+ users
  * Tối ưu database query

* **Kiểm thử Cross-Browser**:
  * Chrome, Firefox, Safari, Edge
  * Responsive design trên mobile (iOS, Android)
  * Tuân thủ accessibility (WCAG 2.1 Level AA)

**3. Cấu hình Monitoring và Logging:**
* **CloudWatch Logs**:
  * Application logs: /aws/workshop-aws/dev/application
  * Access logs: /aws/workshop-aws/dev/access
  * Error logs: /aws/workshop-aws/dev/error
  * Log retention: 7 ngày (tối ưu chi phí)

* **CloudWatch Alarms**:
  * EC2 CPU Utilization > 80% trong 5 phút
  * RDS Database Connections > 90% của max
  * ALB Target Unhealthy Count > 0
  * API Gateway 5XX Error Rate > 5%
  * RDS Free Storage Space < 2GB

* **SNS Notifications**:
  * Cảnh báo email cho alarms quan trọng
  * Thông báo SMS cho sự cố production
  * Tích hợp Slack cho thông báo nhóm

* **CloudWatch Dashboard**:
  * Trực quan hóa metrics thời gian thực
  * Metrics EC2, RDS, ALB, API Gateway
  * Custom application metrics
  * Widgets theo dõi chi phí

**4. Triển khai VPC Endpoints để Tối ưu Chi phí:**
* Tạo VPC Endpoints cho các dịch vụ AWS:
  * **S3 Gateway Endpoint**: Miễn phí, không phí truyền dữ liệu
  * **CloudWatch Logs Interface Endpoint**: $0.01/giờ (~$7.20/tháng)
  * **SSM Interface Endpoint**: $0.01/giờ (~$7.20/tháng)
  * **EC2 Interface Endpoint**: $0.01/giờ (~$7.20/tháng)

* Cập nhật route tables:
  * Private subnet routes tới VPC Endpoints thay vì NAT Gateway
  * Loại bỏ phụ thuộc NAT Gateway cho truy cập dịch vụ AWS
  * Duy trì Internet Gateway cho public subnet

* Cấu hình Security Group:
  * Cho phép HTTPS (443) từ EC2 security group tới VPC Endpoint security group
  * Bật DNS resolution cho VPC Endpoints

* Phân tích tiết kiệm chi phí:
  * **Trước**: NAT Gateway $32.40/tháng + truyền dữ liệu $5-10/tháng = ~$37-42/tháng
  * **Sau**: VPC Endpoints $21.60/tháng + truyền dữ liệu tối thiểu = ~$22-25/tháng
  * **Tiết kiệm**: ~$15-20/tháng (giảm 40-50%)

**5. Khắc phục Sự cố và Giải quyết Vấn đề:**
* **Vấn đề 1: Lỗi CORS trong browser console**
  * Nguyên nhân gốc: API Gateway CORS không được cấu hình đúng
  * Giải pháp: Thêm CORS headers trong API Gateway responses và backend

* **Vấn đề 2: CloudFront phục vụ nội dung cũ**
  * Nguyên nhân gốc: Cache không được invalidated sau triển khai
  * Giải pháp: Tạo invalidation cho path /*, đợi 5-10 phút

* **Vấn đề 3: RDS connection timeout**
  * Nguyên nhân gốc: Security group không cho phép traffic EC2 tới RDS
  * Giải pháp: Cập nhật RDS security group cho phép port 3306 từ EC2 SG

* **Vấn đề 4: Chi phí NAT Gateway cao**
  * Nguyên nhân gốc: Tất cả traffic dịch vụ AWS đi qua NAT Gateway
  * Giải pháp: Triển khai VPC Endpoints cho S3, CloudWatch, SSM

**6. Tự động hóa Triển khai:**
* Tạo script triển khai (deploy-frontend.sh):
  * Tự động hóa quy trình build
  * Upload S3 với headers phù hợp
  * CloudFront invalidation
  * Xác minh triển khai

* Tài liệu hóa quy trình triển khai:
  * Hướng dẫn triển khai từng bước
  * Quy trình rollback
  * Runbook khắc phục sự cố
  * Thông tin liên hệ khẩn cấp

**7. Xác minh Hệ thống Cuối cùng:**
* Xác minh tất cả thành phần hoạt động cùng nhau:
  * ✅ Frontend truy cập được qua CloudFront
  * ✅ Backend API phản hồi đúng
  * ✅ Database queries thực thi thành công
  * ✅ Luồng xác thực hoạt động
  * ✅ Monitoring và alerting đang hoạt động
  * ✅ Logs streaming vào CloudWatch
  * ✅ Tối ưu chi phí được triển khai

### Kết quả & Sản phẩm Tuần 10:

**Các Sản phẩm Hoàn thành:**
* ✅ React frontend được triển khai lên S3 và CloudFront
* ✅ Kiểm thử ứng dụng end-to-end hoàn chỉnh
* ✅ CloudWatch monitoring và alerting được cấu hình
* ✅ VPC Endpoints được triển khai để tối ưu chi phí
* ✅ Scripts tự động hóa triển khai được tạo
* ✅ Tài liệu và runbooks toàn diện
* ✅ Xác minh và sign-off hệ thống cuối cùng

**Các Chỉ số Chính:**
* **Kích thước Frontend Bundle**: 2.5MB (không nén), 800KB (gzipped)
* **Thời gian Tải Trang**: <2 giây (trung bình toàn cầu)
* **Thời gian Phản hồi API**: <200ms (p95)
* **Tỷ lệ Cache Hit CloudFront**: 85%+
* **Uptime Ứng dụng**: 99.9%
* **Tối ưu Chi phí**: Giảm 40-50% với VPC Endpoints
* **Chi phí Hàng tháng**: $8.90 (hạ tầng) + $21.60 (VPC Endpoints) = $30.50/tháng

**Kiến trúc Cuối cùng:**
```
Internet
    │
    ├─── CloudFront (CDN) ──> S3 (Frontend)
    │
    └─── API Gateway ──> ALB ──> EC2 (Backend) ──> RDS MySQL
                                  │
                                  └─── VPC Endpoints (S3, CloudWatch, SSM, EC2)
                                       (Không cần NAT Gateway)
```

**Công nghệ Đã Triển khai:**
* **Frontend**: React + Vite, hosted trên S3, phân phối qua CloudFront
* **Backend**: Spring Boot 3.x trên EC2 t3.nano với systemd
* **Database**: RDS MySQL 8.0 db.t3.micro với automated backups
* **Load Balancer**: Application Load Balancer với health checks
* **API Gateway**: REST API với VPC Link integration
* **Authentication**: AWS Cognito User Pools
* **Monitoring**: CloudWatch Logs, Metrics, Alarms, Dashboards
* **Notifications**: SNS cho cảnh báo email/SMS
* **Tối ưu Chi phí**: VPC Endpoints thay thế NAT Gateway

### Bài học Kinh nghiệm:

**1. Tối ưu Frontend Build:**
* **Bài học**: Tối ưu build phù hợp giảm đáng kể thời gian tải và chi phí băng thông
* **Áp dụng**: Sử dụng Vite cho builds nhanh, code splitting và tree shaking - giảm kích thước bundle 60%
* **Rút ra**: Luôn tối ưu production builds - sử dụng minification, compression, lazy loading và CDN caching

**2. Chiến lược Cache CloudFront:**
* **Bài học**: Cần các chiến lược cache khác nhau cho static assets và dynamic content
* **Áp dụng**: Cache dài (1 năm) cho versioned assets, no-cache cho index.html
* **Rút ra**: Triển khai cache-busting với file hashing và cache-control headers phù hợp

**3. Cấu hình CORS:**
* **Bài học**: CORS phải được cấu hình trên cả API Gateway và backend application
* **Áp dụng**: Thêm CORS headers trong API Gateway responses và Spring Boot @CrossOrigin annotations
* **Rút ra**: Kiểm tra CORS kỹ lưỡng trong development - browser console hiển thị thông báo lỗi rõ ràng

**4. Điều chỉnh CloudWatch Alarms:**
* **Bài học**: Ngưỡng alarm phải cân bằng giữa độ nhạy và nhiễu
* **Áp dụng**: Đặt CPU alarm ở 80% trong 5 phút (không phải 1 phút) để tránh false positives
* **Rút ra**: Bắt đầu với ngưỡng bảo thủ, điều chỉnh dựa trên mẫu sử dụng thực tế và tỷ lệ false alarm

**5. Phân tích Chi phí-Lợi ích VPC Endpoints:**
* **Bài học**: VPC Endpoints tiết kiệm tiền cho truy cập dịch vụ AWS lưu lượng cao
* **Áp dụng**: Tiết kiệm $15-20/tháng bằng cách thay thế NAT Gateway bằng VPC Endpoints
* **Rút ra**: Đối với workloads production với sử dụng dịch vụ AWS nhiều, VPC Endpoints hiệu quả chi phí mặc dù có phí theo giờ

**6. Phương pháp Kiểm thử:**
* **Bài học**: Kiểm thử có hệ thống ngăn chặn vấn đề production
* **Áp dụng**: Tạo checklist kiểm thử bao gồm xác thực, chức năng, tích hợp, hiệu suất và cross-browser
* **Rút ra**: Đầu tư thời gian vào kiểm thử toàn diện - phát hiện bugs trong development rẻ hơn 10 lần so với production

**7. Tự động hóa Triển khai:**
* **Bài học**: Triển khai thủ công dễ lỗi và tốn thời gian
* **Áp dụng**: Tạo shell script tự động hóa build, upload và invalidation - giảm thời gian triển khai từ 15 phút xuống 2 phút
* **Rút ra**: Tự động hóa các tác vụ lặp lại - tiết kiệm thời gian, giảm lỗi, cho phép CI/CD

**8. Monitoring và Observability:**
* **Bài học**: Không thể sửa những gì không thấy được - monitoring là thiết yếu
* **Áp dụng**: Cấu hình CloudWatch Logs, Metrics, Alarms và Dashboards cho khả năng quan sát hệ thống đầy đủ
* **Rút ra**: Triển khai monitoring từ ngày đầu - logs và metrics vô giá cho khắc phục sự cố và tối ưu

**9. Tư duy Tối ưu Chi phí:**
* **Bài học**: Các tối ưu nhỏ tích lũy thành tiết kiệm đáng kể
* **Áp dụng**: VPC Endpoints, S3 lifecycle policies, CloudWatch log retention, right-sizing instances
* **Rút ra**: Thường xuyên xem xét AWS Cost Explorer và xác định cơ hội tối ưu - chi phí cloud có thể tăng nhanh

**10. Tài liệu và Chuyển giao Kiến thức:**
* **Bài học**: Tài liệu tốt cho phép khả năng mở rộng nhóm và phản ứng sự cố
* **Áp dụng**: Tạo hướng dẫn triển khai, runbooks khắc phục sự cố, sơ đồ kiến trúc và phân tích chi phí
* **Rút ra**: Tài liệu không phải chi phí phát sinh - đó là khoản đầu tư được đền đáp trong onboarding, sự cố và audits

**11. Best Practices Bảo mật:**
* **Bài học**: Bảo mật phải được xây dựng sẵn, không phải gắn thêm sau
* **Áp dụng**: Sử dụng VPC isolation, security groups, IAM roles, Cognito authentication, mã hóa SSL/TLS
* **Rút ra**: Tuân theo AWS Well-Architected Security Pillar - phòng thủ nhiều lớp, least privilege, mã hóa mọi nơi

**12. Cân nhắc Khả năng Mở rộng:**
* **Bài học**: Thiết kế cho scale từ đầu - cải tạo sau rất tốn kém
* **Áp dụng**: Sử dụng Auto Scaling Groups, Load Balancers, CloudFront CDN, RDS read replicas (đã lên kế hoạch)
* **Rút ra**: Horizontal scaling dễ hơn vertical - sử dụng managed services tự động scale
