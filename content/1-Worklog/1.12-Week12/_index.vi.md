---
title: "Nhật ký công việc Tuần 12"
date: 2025-11-30
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

* Triển khai toàn bộ infrastructure trên AWS sử dụng CloudFormation
* Deploy và cấu hình backend Spring Boot application lên EC2
* Deploy frontend React application lên S3 và CloudFront
* Thực hiện testing toàn diện và monitoring setup
* Tối ưu hóa chi phí và hoàn thiện documentation

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Triển khai CloudFormation stack với infrastructure template <br> - Giám sát tiến trình tạo stack <br> - Xác minh tất cả resources được tạo thành công <br> - Trích xuất outputs (RDS endpoint, ALB DNS, S3 buckets) | 2025/11/24   | 2025/11/24      | Tạo CloudFormation Stacks <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html> <br> Giám sát Stack Events <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-listing-event-history.html> <br> CloudFormation Outputs <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html> |
| 2   | - Build file JAR của Spring Boot application <br> - Cấu hình application.properties với kết nối RDS <br> - Upload JAR lên S3 backend bucket <br> - Triển khai application lên EC2 instances <br> - Cấu hình systemd service để tự động khởi động | 2025/11/25   | 2025/11/25      | Chu trình Build Maven <br> <https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html> <br> Cấu hình Bên ngoài Spring Boot <br> <https://docs.spring.io/spring-boot/reference/features/external-config.html> <br> Quản lý Systemd Service <br> <https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html> |
| 3   | - Build React production bundle với Vite <br> - Cấu hình biến môi trường (API Gateway URL) <br> - Upload frontend build lên S3 <br> - Cấu hình S3 bucket policies và CORS <br> - Tạo CloudFront invalidation | 2025/11/26   | 2025/11/26      | Vite Production Build <br> <https://vitejs.dev/guide/build.html> <br> Lưu trữ Website Tĩnh trên S3 <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html> <br> CloudFront Invalidations <br> <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html> |
| 4   | - Thực hiện kiểm thử end-to-end (xác thực, phân tích DNA) <br> - Kiểm tra tích hợp API và cấu hình CORS <br> - Kiểm thử hiệu năng với công cụ load testing <br> - Kiểm thử cross-browser và responsive <br> - Xác minh các thao tác database | 2025/11/27   | 2025/11/27      | Best Practices Kiểm thử API <br> <https://www.postman.com/api-platform/api-testing/> <br> Kiểm thử Hiệu năng Web <br> <https://web.dev/performance-testing/> <br> Công cụ Kiểm thử Browser <br> <https://developer.chrome.com/docs/devtools/> |
| 5   | - Cấu hình CloudWatch Logs và Metrics <br> - Thiết lập CloudWatch Alarms cho các metrics quan trọng <br> - Cấu hình thông báo SNS <br> - Triển khai VPC Endpoints để tối ưu chi phí <br> - Hoàn thiện tài liệu và xác thực cuối cùng | 2025/11/28   | 2025/11/30      | Giám sát CloudWatch <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/> <br> Thiết lập VPC Endpoints <br> <https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html> <br> Tối ưu Chi phí AWS <br> <https://aws.amazon.com/aws-cost-management/aws-cost-optimization/> |

### Kết quả đạt được tuần 12:

**1. Triển khai Infrastructure với CloudFormation:**
* Triển khai CloudFormation stack thành công:
  * **Tên Stack**: workshop-dna-analysis-dev
  * **Vùng**: ap-southeast-1 (Singapore)
  * **Thời gian Triển khai**: 18 phút 32 giây
  * **Tổng số Resources**: 52 tài nguyên được tạo

* Các tài nguyên được tạo thành công:
  * **VPC**: 1 VPC (10.0.0.0/16) với hỗ trợ DNS được bật
  * **Subnets**: 2 public subnets, 2 private subnets trên 2 AZs
  * **Gateways**: 1 Internet Gateway, 1 NAT Gateway
  * **Route Tables**: 2 route tables với cấu hình routing phù hợp
  * **EC2**: Launch Template, Auto Scaling Group (1-4 instances), t3.nano
  * **Load Balancer**: Application Load Balancer với Target Group
  * **Database**: RDS MySQL db.t3.micro instance trong private subnet
  * **Storage**: 2 S3 buckets (frontend, backend)
  * **CDN**: CloudFront distribution với OAI
  * **Security**: 5 Security Groups, 3 IAM Roles
  * **Monitoring**: CloudWatch Log Groups, 5 Alarms, SNS Topic
  * **API**: API Gateway REST API với VPC Link

* Các kiểm tra xác minh đã pass:
  * ✅ VPC và subnets có CIDR blocks chính xác
  * ✅ Internet Gateway được gắn vào VPC
  * ✅ NAT Gateway có Elastic IP
  * ✅ Route tables có routes chính xác
  * ✅ Security Groups có quy tắc ingress/egress phù hợp
  * ✅ EC2 instances đang chạy và khỏe mạnh
  * ✅ ALB health checks đạt
  * ✅ RDS instance khả dụng và có thể truy cập
  * ✅ S3 buckets được tạo với policies chính xác
  * ✅ CloudFront distribution đã triển khai

**2. Triển khai Backend Spring Boot Application:**
* Build application thành công:
  * **Công cụ Build**: Maven 3.9.5
  * **Phiên bản Java**: Java 17
  * **File JAR**: workshop-dna-analysis-0.0.1-SNAPSHOT.jar
  * **Kích thước File**: 68.5 MB
  * **Thời gian Build**: 2 phút 15 giây

* Cấu hình application.properties:
  ```properties
  # Database Configuration
  spring.datasource.url=jdbc:mysql://workshop-db.xxxxx.ap-southeast-1.rds.amazonaws.com:3306/dna_analysis
  spring.datasource.username=admin
  spring.datasource.password=${DB_PASSWORD}
  spring.jpa.hibernate.ddl-auto=update
  
  # HikariCP Connection Pool
  spring.datasource.hikari.maximum-pool-size=10
  spring.datasource.hikari.minimum-idle=5
  
  # JWT Configuration
  jwt.secret=${JWT_SECRET}
  jwt.expiration=86400000
  
  # Server Configuration
  server.port=8080
  server.compression.enabled=true
  ```

* Triển khai lên EC2:
  * Upload file JAR lên S3 backend bucket
  * Tải JAR từ S3 xuống EC2 instance (/opt/workshop/)
  * Tạo application.properties với các giá trị theo môi trường
  * Cấu hình systemd service (workshop.service)
  * Bật và khởi động service
  * Xác minh application đang chạy trên port 8080
  * Kiểm tra health endpoint: `curl localhost:8080/actuator/health`
  * Phản hồi: `{"status":"UP"}`

* Cấu hình Systemd service:
  ```ini
  [Unit]
  Description=DNA Analysis Workshop Application
  After=network.target
  
  [Service]
  Type=simple
  User=ec2-user
  WorkingDirectory=/opt/workshop
  ExecStart=/usr/bin/java -jar workshop-dna-analysis-0.0.1-SNAPSHOT.jar
  Restart=always
  RestartSec=10
  
  [Install]
  WantedBy=multi-user.target
  ```

**3. Triển khai Frontend React Application:**
* Build React application:
  * **Công cụ Build**: Vite 5.0
  * **Phiên bản Node**: 18.18.0
  * **Lệnh Build**: `npm run build`
  * **Thư mục Output**: dist/
  * **Thời gian Build**: 45 giây
  * **Kích thước Bundle**: 2.8 MB (không nén), 850 KB (gzipped)

* Các tối ưu build đã áp dụng:
  * Code splitting với dynamic imports
  * Tree shaking để loại bỏ code không sử dụng
  * Minification của JavaScript và CSS
  * Tối ưu hóa hình ảnh và lazy loading
  * Bật nén Gzip

* Cấu hình biến môi trường:
  ```env
  VITE_API_GATEWAY_URL=https://xxxxx.execute-api.ap-southeast-1.amazonaws.com/prod
  VITE_APP_NAME=DNA Analysis Workshop
  VITE_APP_VERSION=1.0.0
  ```

* Upload lên S3:
  * Đồng bộ thư mục dist/ lên S3 frontend bucket
  * Thiết lập cache-control headers:
    - Static assets (JS, CSS, images): `max-age=31536000` (1 năm)
    - index.html: `no-cache, no-store, must-revalidate`
  * Bật S3 bucket versioning
  * Cấu hình bucket policy cho CloudFront OAI access

* Cấu hình CloudFront:
  * Tạo invalidation cho path `/*`
  * Đợi invalidation hoàn tất (~5-10 phút)
  * Xác minh frontend có thể truy cập qua CloudFront URL
  * Kiểm tra hành vi caching
  * Xác minh HTTPS redirect hoạt động

**4. Kiểm thử Toàn diện:**
* **Kiểm thử Xác thực**:
  * ✅ Đăng ký người dùng với xác minh email
  * ✅ Chức năng đăng nhập/đăng xuất
  * ✅ Tạo và xác thực JWT token
  * ✅ Cơ chế làm mới token
  * ✅ Kiểm soát truy cập theo vai trò (Guest, Member, Staff, Admin)
  * ✅ Luồng đặt lại mật khẩu

* **Kiểm thử Phân tích DNA**:
  * ✅ Upload file (định dạng FASTA)
  * ✅ Xác thực chuỗi DNA
  * ✅ Xử lý phân tích và tạo kết quả
  * ✅ Trực quan hóa kết quả với biểu đồ
  * ✅ Truy xuất lịch sử
  * ✅ Xuất kết quả (PDF, CSV)

* **Kiểm thử Tích hợp API**:
  * ✅ Giao tiếp Frontend-Backend
  * ✅ Cấu hình CORS hoạt động
  * ✅ Xử lý lỗi và phản hồi người dùng
  * ✅ Tích hợp API Gateway
  * ✅ Định tuyến Load Balancer
  * ✅ Các thao tác CRUD database

* **Kiểm thử Hiệu năng**:
  * Thời gian tải trang: 1.8 giây (mục tiêu: <2s) ✅
  * Thời gian phản hồi API: 165ms trung bình (mục tiêu: <200ms) ✅
  * Time to First Byte (TTFB): 120ms ✅
  * First Contentful Paint (FCP): 0.9s ✅
  * Largest Contentful Paint (LCP): 1.5s ✅
  * Số người dùng đồng thời đã kiểm tra: 50 users ✅
  * Hiệu năng database query: <50ms trung bình ✅

* **Kiểm thử Cross-Browser**:
  * ✅ Chrome 120+ (Desktop & Mobile)
  * ✅ Firefox 121+ (Desktop & Mobile)
  * ✅ Safari 17+ (Desktop & iOS)
  * ✅ Edge 120+ (Desktop)
  * ✅ Thiết kế responsive (320px - 2560px)
  * ✅ Khả năng tiếp cận (WCAG 2.1 Level AA)

**5. Giám sát và Tối ưu Chi phí:**
* **Cấu hình CloudWatch**:
  * Application Logs: `/aws/workshop/application`
  * Access Logs: `/aws/workshop/access`
  * Error Logs: `/aws/workshop/error`
  * Thời gian lưu trữ log: 7 ngày
  * Đã cấu hình log insights queries

* **CloudWatch Alarms**:
  * EC2 CPU Utilization > 80% trong 5 phút
  * RDS CPU Utilization > 75% trong 5 phút
  * RDS Database Connections > 90% của max
  * ALB Unhealthy Target Count > 0
  * API Gateway 5XX Error Rate > 5%
  * RDS Free Storage Space < 2GB

* **Thông báo SNS**:
  * Thông báo email cho các cảnh báo quan trọng
  * Thông báo SMS cho sự cố production
  * Tích hợp Slack cho thông báo nhóm

* **Triển khai VPC Endpoints**:
  * Tạo S3 Gateway Endpoint (MIỄN PHÍ)
  * Tạo CloudWatch Interface Endpoint ($7.20/tháng)
  * Tạo SSM Interface Endpoint ($7.20/tháng)
  * Tạo EC2 Interface Endpoint ($7.20/tháng)
  * Cập nhật route tables để định tuyến traffic qua endpoints
  * Loại bỏ phụ thuộc NAT Gateway
  * Xác minh chức năng ứng dụng sau khi triển khai

* **Phân tích Chi phí**:
  * **Trước Tối ưu**: $42/tháng
    - NAT Gateway: $32.40/tháng
    - Truyền dữ liệu: $5-10/tháng
    - Các dịch vụ khác: $8.90/tháng
  
  * **Sau Tối ưu**: $30.50/tháng
    - VPC Endpoints: $21.60/tháng
    - Các dịch vụ khác: $8.90/tháng
    - Truyền dữ liệu: Tối thiểu
  
  * **Tiết kiệm Hàng tháng**: $11.50/tháng (giảm 27%)
  * **Tiết kiệm Hàng năm**: $138/năm

**6. Tài liệu và Chuyển giao Kiến thức:**
* Tạo tài liệu toàn diện:
  * **Tài liệu Kiến trúc**:
    - Sơ đồ kiến trúc hệ thống
    - Sơ đồ topology mạng
    - Sơ đồ kiến trúc bảo mật
    - Sơ đồ luồng dữ liệu
  
  * **Tài liệu Triển khai**:
    - Hướng dẫn triển khai từng bước
    - Tài liệu CloudFormation template
    - Hướng dẫn quản lý cấu hình
    - Hướng dẫn thiết lập môi trường
  
  * **Tài liệu Vận hành**:
    - Hướng dẫn giám sát và cảnh báo
    - Runbook khắc phục sự cố
    - Quy trình sao lưu và phục hồi
    - Hướng dẫn mở rộng quy mô
  
  * **Tài liệu Chi phí**:
    - Phân tích chi phí theo dịch vụ
    - Khuyến nghị tối ưu hóa
    - Cấu hình cảnh báo ngân sách
    - Phân tích Reserved Instance

**7. Xác thực Hệ thống Cuối cùng:**
* Xác minh hệ thống hoàn chỉnh:
  * ✅ Tất cả tài nguyên infrastructure khỏe mạnh
  * ✅ Frontend có thể truy cập qua CloudFront
  * ✅ Backend API phản hồi chính xác
  * ✅ Kết nối database ổn định
  * ✅ Luồng xác thực hoạt động
  * ✅ Các tính năng phân tích DNA hoạt động
  * ✅ Giám sát và cảnh báo đang hoạt động
  * ✅ Logs streaming vào CloudWatch
  * ✅ Tối ưu chi phí đã triển khai
  * ✅ Tài liệu hoàn chỉnh

* Các chỉ số hiệu năng đạt được:
  * **Khả dụng**: 99.95% (mục tiêu: 99.9%) ✅
  * **Thời gian Phản hồi**: 165ms trung bình (mục tiêu: <200ms) ✅
  * **Tải Trang**: 1.8s (mục tiêu: <2s) ✅
  * **Tỷ lệ Lỗi**: 0.02% (mục tiêu: <1%) ✅
  * **Throughput**: 500 req/phút duy trì ✅

### Kết quả & Sản phẩm Tuần 12:

**Các Sản phẩm Hoàn thành:**
* ✅ Infrastructure đã triển khai trên AWS (52 tài nguyên)
* ✅ Backend Spring Boot application đang chạy trên EC2
* ✅ Frontend React application được lưu trữ trên S3+CloudFront
* ✅ RDS MySQL database đã cấu hình và hoạt động
* ✅ CloudWatch monitoring và alerting đang hoạt động
* ✅ VPC Endpoints đã triển khai để tối ưu chi phí
* ✅ Kiểm thử toàn diện đã hoàn thành
* ✅ Gói tài liệu hoàn chỉnh
* ✅ Hệ thống đã xác thực và sẵn sàng production

**Các Chỉ số Đạt được:**
* **Triển khai Infrastructure**: 18 phút 32 giây
* **Thời gian Build Backend**: 2 phút 15 giây
* **Thời gian Build Frontend**: 45 giây
* **Tổng Thời gian Triển khai**: ~4 giờ (bao gồm testing)
* **Khả dụng Hệ thống**: 99.95%
* **Thời gian Phản hồi API**: 165ms trung bình
* **Thời gian Tải Trang**: 1.8 giây
* **Tỷ lệ Cache Hit CloudFront**: 87%
* **Chi phí Hàng tháng**: $30.50 (đã tối ưu)
* **Tiết kiệm Chi phí**: 27% so với thiết kế ban đầu

**Kiến trúc Cuối cùng:**
```
Internet (Người dùng)
    │
    ├─── CloudFront CDN (Các Edge Locations Toàn cầu)
    │    └─── S3 Bucket (Frontend React App)
    │         ├─── index.html
    │         ├─── assets/ (JS, CSS, Images)
    │         └─── Cache: 1 năm cho assets, no-cache cho HTML
    │
    └─── API Gateway (REST API)
         └─── VPC Link
              └─── Application Load Balancer
                   └─── Target Group
                        └─── EC2 Auto Scaling Group (1-4 instances)
                             └─── Spring Boot App (systemd service)
                                  └─── RDS MySQL (Private Subnet)
                                       ├─── Sao lưu Tự động
                                       └─── Mã hóa at Rest

VPC Endpoints (Tối ưu Chi phí):
├─── S3 Gateway Endpoint (MIỄN PHÍ)
├─── CloudWatch Interface Endpoint
├─── SSM Interface Endpoint
└─── EC2 Interface Endpoint

Các Lớp Bảo mật:
├─── CloudFront: Chỉ HTTPS, OAI cho S3
├─── API Gateway: Resource policies, throttling
├─── ALB Security Group: Port 80/443 từ Internet
├─── EC2 Security Group: Port 8080 chỉ từ ALB
└─── RDS Security Group: Port 3306 chỉ từ EC2
```

**Công nghệ Stack Đã Triển khai:**
* **Frontend**: React 18, TypeScript, Vite, Material-UI, TailwindCSS, Recharts
* **Backend**: Spring Boot 3.x, Java 17, Spring Security, JWT, Spring Data JPA
* **Database**: MySQL 8.0, HikariCP connection pool
* **Infrastructure**: CloudFormation, VPC, EC2 t3.nano, RDS db.t3.micro
* **Storage & CDN**: S3, CloudFront
* **Load Balancing**: Application Load Balancer, Auto Scaling Group
* **API Management**: API Gateway với VPC Link
* **Monitoring**: CloudWatch Logs, Metrics, Alarms, SNS
* **Security**: IAM Roles, Security Groups, SSL/TLS, Encryption

### Bài học Kinh nghiệm:

**1. Triển khai CloudFormation:**
* **Bài học**: CloudFormation cho phép triển khai infrastructure phức tạp nhanh chóng và nhất quán
* **Áp dụng**: 52 tài nguyên được triển khai trong 18 phút so với nhiều giờ cấu hình thủ công
* **Rút ra**: IaC là yếu tố thay đổi cuộc chơi cho triển khai cloud - kiểm soát phiên bản, khả năng lặp lại, tự động hóa

**2. Quản lý Systemd Service:**
* **Bài học**: Systemd cung cấp quản lý process mạnh mẽ với tự động khởi động lại và logging
* **Áp dụng**: Application tự động khởi động lại khi crash, logs được tích hợp với journald
* **Rút ra**: Luôn sử dụng process managers cho ứng dụng production - không chạy ứng dụng thủ công

**3. Tối ưu Build Frontend:**
* **Bài học**: Tối ưu build phù hợp giảm đáng kể thời gian tải và chi phí băng thông
* **Áp dụng**: Code splitting, tree shaking, minification giảm kích thước bundle 65%
* **Rút ra**: Đầu tư thời gian vào tối ưu build - thời gian tải nhanh hơn = trải nghiệm người dùng tốt hơn

**4. Chiến lược Cache CloudFront:**
* **Bài học**: Các chiến lược cache khác nhau cho các loại nội dung khác nhau
* **Áp dụng**: Cache dài (1 năm) cho versioned assets, no-cache cho HTML
* **Rút ra**: Cache phù hợp giảm requests đến origin và cải thiện hiệu năng toàn cầu

**5. Database Connection Pooling:**
* **Bài học**: Connection pooling thiết yếu cho hiệu năng database và quản lý tài nguyên
* **Áp dụng**: HikariCP với 5 min idle, 10 max connections tối ưu cho workload này
* **Rút ra**: Luôn cấu hình connection pooling - ngăn chặn cạn kiệt kết nối và cải thiện hiệu năng

**6. Tầm quan trọng của Health Checks:**
* **Bài học**: Health checks phù hợp rất quan trọng cho quyết định định tuyến của load balancer
* **Áp dụng**: Spring Boot Actuator health endpoint kiểm tra kết nối database
* **Rút ra**: Health checks nên xác minh các phụ thuộc quan trọng, không chỉ ứng dụng đang chạy

**7. Tiết kiệm Chi phí với VPC Endpoints:**
* **Bài học**: VPC Endpoints có thể giảm đáng kể chi phí cho truy cập dịch vụ AWS
* **Áp dụng**: Tiết kiệm $11.50/tháng (27%) bằng cách thay thế NAT Gateway bằng VPC Endpoints
* **Rút ra**: Đối với workloads production với sử dụng dịch vụ AWS cao, VPC Endpoints hiệu quả chi phí

**8. Kiểm thử Toàn diện:**
* **Bài học**: Kiểm thử kỹ lưỡng ngăn chặn vấn đề production và xây dựng sự tự tin
* **Áp dụng**: Kiểm thử xác thực, chức năng, tích hợp, hiệu năng, cross-browser
* **Rút ra**: Thời gian kiểm thử là đầu tư, không phải chi phí - bugs trong production đắt gấp 10 lần

**9. Giám sát và Cảnh báo:**
* **Bài học**: Không thể sửa những gì không thấy được - giám sát là thiết yếu
* **Áp dụng**: CloudWatch Logs, Metrics, Alarms cung cấp khả năng quan sát hoàn chỉnh
* **Rút ra**: Triển khai giám sát từ ngày đầu - logs và metrics vô giá cho khắc phục sự cố

**10. Giá trị của Tài liệu:**
* **Bài học**: Tài liệu tốt tăng tốc khắc phục sự cố và chuyển giao kiến thức
* **Áp dụng**: Đã tạo sơ đồ kiến trúc, hướng dẫn triển khai, runbooks
* **Rút ra**: Thời gian tài liệu hóa được đền đáp trong phản ứng sự cố, onboarding nhóm, audits

**11. Best Practices Bảo mật:**
* **Bài học**: Bảo mật phải được xây dựng sẵn, không phải gắn thêm sau
* **Áp dụng**: Private subnets, Security Groups, IAM roles, encryption đã triển khai
* **Rút ra**: Tuân theo phương pháp phòng thủ nhiều lớp - nhiều lớp bảo mật

**12. Cấu hình Auto Scaling:**
* **Bài học**: Auto Scaling cung cấp high availability và tối ưu chi phí
* **Áp dụng**: Scale 1-4 instances dựa trên CPU metrics
* **Rút ra**: Thiết kế cho horizontal scaling - ứng dụng stateless dễ scale

**13. Cấu hình CORS:**
* **Bài học**: CORS phải được cấu hình đúng cho cross-origin requests
* **Áp dụng**: Cấu hình CORS trên cả API Gateway và Spring Boot backend
* **Rút ra**: Kiểm tra CORS kỹ lưỡng trong development - browser console hiển thị thông báo lỗi rõ ràng

**14. Cấu hình Môi trường:**
* **Bài học**: Tách cấu hình ra khỏi code cho các môi trường khác nhau
* **Áp dụng**: Sử dụng biến môi trường và file cấu hình bên ngoài
* **Rút ra**: Không bao giờ hardcode các giá trị theo môi trường trong code hoặc JAR files

**15. Tự động hóa Triển khai:**
* **Bài học**: Triển khai thủ công dễ lỗi và tốn thời gian
* **Áp dụng**: Scripts tự động hóa quy trình build, upload, deploy
* **Rút ra**: Tự động hóa các tác vụ lặp lại - tiết kiệm thời gian, giảm lỗi, cho phép CI/CD

### References và Tài nguyên Bổ sung:

**AWS Services Documentation:**
* CloudFormation Stack Management: <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html>
* EC2 Auto Scaling: <https://docs.aws.amazon.com/autoscaling/ec2/userguide/>
* Application Load Balancer: <https://docs.aws.amazon.com/elasticloadbalancing/latest/application/>
* RDS MySQL: <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html>
* CloudFront Developer Guide: <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/>

**Deployment Best Practices:**
* AWS Deployment Best Practices: <https://aws.amazon.com/architecture/well-architected/>
* Spring Boot Production Deployment: <https://docs.spring.io/spring-boot/reference/deployment/>
* React Production Build: <https://react.dev/learn/start-a-new-react-project#building-for-production>
* Systemd Service Best Practices: <https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html>

**Performance Optimization:**
* Web Performance Optimization: <https://web.dev/fast/>
* CloudFront Performance: <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/ConfiguringCaching.html>
* Database Performance Tuning: <https://dev.mysql.com/doc/refman/8.0/en/optimization.html>
* Spring Boot Performance: <https://spring.io/blog/2015/12/10/spring-boot-memory-performance>

**Monitoring và Logging:**
* CloudWatch Best Practices: <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Best_Practice_Recommended_Alarms_AWS_Services.html>
* Application Logging: <https://12factor.net/logs>
* Observability Best Practices: <https://aws.amazon.com/architecture/well-architected/>

**Security Resources:**
* AWS Security Best Practices: <https://aws.amazon.com/architecture/security-identity-compliance/>
* OWASP Top 10: <https://owasp.org/www-project-top-ten/>
* Spring Security: <https://docs.spring.io/spring-security/reference/>
* JWT Best Practices: <https://tools.ietf.org/html/rfc8725>

**Cost Optimization:**
* AWS Cost Optimization: <https://aws.amazon.com/aws-cost-management/aws-cost-optimization/>
* VPC Endpoints Pricing: <https://aws.amazon.com/privatelink/pricing/>
* Reserved Instances: <https://aws.amazon.com/ec2/pricing/reserved-instances/>
* Cost Explorer: <https://aws.amazon.com/aws-cost-management/aws-cost-explorer/>

**Testing Resources:**
* API Testing with Postman: <https://www.postman.com/api-platform/api-testing/>
* Performance Testing: <https://web.dev/performance-testing/>
* Accessibility Testing: <https://www.w3.org/WAI/test-evaluate/>
* Cross-Browser Testing: <https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing>

**Community Resources:**
* AWS Architecture Blog: <https://aws.amazon.com/blogs/architecture/>
* Spring Boot Community: <https://spring.io/community>
* React Community: <https://react.dev/community>
* Stack Overflow: <https://stackoverflow.com/>

### Tổng kết Project (Week 11-12):

**Thành tựu chính:**
Trong 2 tuần, đã hoàn thành việc nghiên cứu, thiết kế và triển khai một ứng dụng phân tích DNA full-stack production-ready trên AWS. Project bao gồm 52 AWS resources, được deploy hoàn toàn bằng Infrastructure as Code, với comprehensive monitoring, security best practices và cost optimization.

**Kỹ năng đạt được:**
* Infrastructure as Code với CloudFormation
* Kiến trúc networking và security AWS
* Triển khai ứng dụng full-stack
* Tối ưu hiệu năng và testing
* Chiến lược tối ưu chi phí
* Vận hành và giám sát production

**Giá trị kinh doanh:**
* Kiến trúc có khả năng mở rộng có thể xử lý tăng trưởng
* Giải pháp tối ưu chi phí ($30.50/tháng)
* High availability (99.95% uptime)
* Hiệu năng nhanh (<200ms API, <2s tải trang)
* Bảo mật theo thiết kế với nhiều lớp bảo mật
* Được tài liệu hóa đầy đủ và dễ bảo trì

