---
title: "Nhật ký công việc Tuần 11"
date: 2025-11-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Nghiên cứu và lập kế hoạch chi tiết cho project triển khai ứng dụng phân tích DNA trên AWS
* Phân tích kiến trúc hệ thống và các dịch vụ AWS cần thiết
* Thiết kế Infrastructure as Code với CloudFormation
* Chuẩn bị môi trường phát triển và các công cụ cần thiết
* Xây dựng roadmap triển khai cho 2 tuần

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Nghiên cứu kiến trúc ứng dụng full-stack trên AWS <br> - Phân tích các dịch vụ AWS phù hợp (VPC, EC2, RDS, S3, CloudFront) <br> - Tìm hiểu về Infrastructure as Code với CloudFormation <br> - Đọc tài liệu AWS Well-Architected Framework | 2025/11/17   | 2025/11/17      | AWS Well-Architected Framework <br> <https://aws.amazon.com/architecture/well-architected/> <br> AWS CloudFormation Best Practices <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html> <br> Building Modern Applications on AWS <br> <https://aws.amazon.com/modern-apps/> |
| 2   | - Thiết kế kiến trúc VPC với public và private subnets <br> - Lập kế hoạch cấu hình Multi-AZ deployment <br> - Nghiên cứu về VPC Endpoints để tối ưu chi phí <br> - Vẽ sơ đồ kiến trúc hệ thống chi tiết | 2025/11/18   | 2025/11/18      | Amazon VPC Design Best Practices <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-design.html> <br> VPC Endpoints Cost Optimization <br> <https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/> <br> Multi-AZ Deployments <br> <https://docs.aws.amazon.com/whitepapers/latest/real-time-communication-on-aws/high-availability-and-scalability-on-aws.html> |
| 3   | - Nghiên cứu Spring Boot deployment trên EC2 <br> - Tìm hiểu về Auto Scaling Groups và Load Balancers <br> - Học cách cấu hình systemd service cho Java applications <br> - Nghiên cứu RDS MySQL best practices | 2025/11/19   | 2025/11/19      | Deploying Spring Boot Applications <br> <https://docs.spring.io/spring-boot/reference/deployment/installing.html> <br> EC2 Auto Scaling Best Practices <br> <https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-best-practices.html> <br> Amazon RDS Best Practices <br> <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.html> |
| 4   | - Nghiên cứu React deployment với S3 và CloudFront <br> - Tìm hiểu về CloudFront caching strategies <br> - Học cách tối ưu frontend build với Vite <br> - Nghiên cứu CORS configuration cho API Gateway | 2025/11/20   | 2025/11/20      | Hosting Static Website on S3 <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html> <br> CloudFront Performance Optimization <br> <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/ConfiguringCaching.html> <br> Vite Build Optimization <br> <https://vitejs.dev/guide/build.html> <br> API Gateway CORS Configuration <br> <https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html> |
| 5   | - Xây dựng CloudFormation template chi tiết <br> - Cấu hình parameters và outputs <br> - Validate template syntax <br> - Chuẩn bị môi trường AWS (IAM roles, Key Pairs) <br> - Tạo roadmap triển khai chi tiết cho tuần 12 | 2025/11/21   | 2025/11/23      | CloudFormation Template Anatomy <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html> <br> CloudFormation Parameters <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html> <br> IAM Best Practices <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html> |

### Kết quả đạt được tuần 11:

**1. Phân tích Kiến trúc Hệ thống:**
* Hoàn thành phân tích chi tiết kiến trúc ứng dụng DNA Analysis:
  * **Frontend Layer**: React 18 + TypeScript với Material-UI và TailwindCSS
  * **Backend Layer**: Spring Boot 3.x với Java 17, Spring Security và JWT authentication
  * **Database Layer**: RDS MySQL 8.0 với automated backups và encryption
  * **CDN Layer**: CloudFront distribution cho global content delivery
  * **API Layer**: API Gateway với VPC Link integration

* Xác định các yêu cầu phi chức năng:
  * **Performance**: Response time < 200ms, page load < 2s
  * **Scalability**: Auto scaling từ 1-4 instances dựa trên CPU metrics
  * **Availability**: Multi-AZ deployment với 99.9% uptime target
  * **Security**: Encryption at rest và in transit, least privilege access
  * **Cost**: Target ~$30-40/tháng cho production workload

**2. Thiết kế Kiến trúc VPC:**
* Thiết kế VPC architecture hoàn chỉnh:
  * **VPC CIDR**: 10.0.0.0/16 (65,536 IP addresses)
  * **Public Subnets**: 
    - 10.0.1.0/24 (AZ-1) - 256 IPs cho ALB, NAT Gateway
    - 10.0.3.0/24 (AZ-2) - 256 IPs cho high availability
  * **Private Subnets**:
    - 10.0.2.0/24 (AZ-1) - 256 IPs cho EC2 instances
    - 10.0.4.0/24 (AZ-2) - 256 IPs cho RDS và EC2 backup

* Lập kế hoạch network components:
  * Internet Gateway cho public internet access
  * NAT Gateway trong public subnet (có thể thay thế bằng VPC Endpoints)
  * Route Tables riêng biệt cho public và private subnets
  * VPC Endpoints cho S3, CloudWatch, SSM, EC2 (tiết kiệm ~$20-25/tháng)

**3. Nghiên cứu Tối ưu Chi phí:**
* Phân tích chi phí dự kiến:
  * **EC2 t3.nano**: $3.50/tháng (development), t3.micro $7/tháng (production)
  * **RDS db.t3.micro**: $2.80/tháng (Single-AZ), $5.60/tháng (Multi-AZ)
  * **NAT Gateway**: $32.40/tháng + data transfer $5-10/tháng
  * **VPC Endpoints**: $7.20/endpoint/tháng (~$21.60 cho 3 endpoints)
  * **S3 + CloudFront**: $0.80/tháng (với Free Tier)
  * **API Gateway**: $0.50/tháng
  * **CloudWatch**: $0.30/tháng

* Xác định chiến lược tối ưu:
  * Sử dụng VPC Endpoints thay vì NAT Gateway: tiết kiệm ~$15-20/tháng
  * S3 Gateway Endpoint: FREE (không tính phí)
  * Interface Endpoints cho CloudWatch, SSM, EC2: $21.60/tháng
  * Tổng chi phí dự kiến: $30-35/tháng (đã tối ưu)

**4. Xây dựng CloudFormation Template:**
* Hoàn thành CloudFormation template với 1,393 dòng code:
  * **Parameters Section** (50 dòng): Environment, KeyName, InstanceType, DBPassword
  * **Networking Resources** (400 dòng): VPC, Subnets, IGW, NAT, Route Tables, VPC Endpoints
  * **Compute Resources** (300 dòng): Launch Template, ASG, ALB, Target Group, Scaling Policies
  * **Storage Resources** (200 dòng): S3 Buckets, CloudFront Distribution, OAI
  * **Database Resources** (100 dòng): RDS Instance, Subnet Group, Parameter Group
  * **Security Resources** (200 dòng): Security Groups, IAM Roles, Instance Profile
  * **Monitoring Resources** (143 dòng): CloudWatch Logs, Alarms, SNS Topic, API Gateway

* Validate template syntax thành công:
  ```bash
  aws cloudformation validate-template --template-body file://infrastructure.yaml
  ```

**5. Chuẩn bị Môi trường Phát triển:**
* Cài đặt và cấu hình công cụ:
  * **AWS CLI v2**: Cấu hình với credentials và default region (ap-southeast-1)
  * **Java 17 JDK**: Cho Spring Boot development
  * **Maven 3.9+**: Cho build backend JAR files
  * **Node.js 18+ & npm**: Cho React frontend development
  * **Git**: Cho version control
  * **VS Code**: Với extensions cho Java, React, CloudFormation

* Tạo EC2 Key Pair:
  * Key name: `workshop-keypair`
  * Region: ap-southeast-1 (Singapore)
  * Downloaded và lưu trữ an toàn private key

* Cấu hình IAM User:
  * Tạo IAM user với programmatic access
  * Attach policies: AdministratorAccess (cho workshop)
  * Cấu hình AWS CLI credentials
  * Enable MFA cho security

**6. Xây dựng Roadmap Triển khai:**
* **Week 12 - Day 1 (24/11)**: Deploy Infrastructure
  * Triển khai CloudFormation stack
  * Xác minh tất cả resources được tạo thành công
  * Kiểm tra VPC, Subnets, Security Groups

* **Week 12 - Day 2 (25/11)**: Deploy Backend
  * Build Spring Boot JAR file
  * Upload lên S3 backend bucket
  * Deploy lên EC2 instances
  * Cấu hình database connection

* **Week 12 - Day 3 (26/11)**: Deploy Frontend
  * Build React production bundle
  * Upload lên S3 frontend bucket
  * Configure CloudFront distribution
  * Test end-to-end application flow

* **Week 12 - Day 4 (27/11)**: Testing & Monitoring
  * Comprehensive testing (authentication, DNA analysis)
  * Configure CloudWatch monitoring
  * Set up alarms and notifications
  * Performance testing

* **Week 12 - Day 5 (28-30/11)**: Optimization & Documentation
  * Implement VPC Endpoints
  * Cost optimization verification
  * Complete documentation
  * Final system validation

**7. Nghiên cứu Best Practices:**
* **Security Best Practices**:
  * Principle of least privilege cho IAM roles
  * Encryption at rest (RDS, S3) và in transit (HTTPS, SSL/TLS)
  * Private subnets cho sensitive resources (EC2, RDS)
  * Security Groups với specific port ranges
  * No hardcoded credentials - sử dụng IAM roles và Secrets Manager

* **High Availability Best Practices**:
  * Multi-AZ deployment cho critical components
  * Auto Scaling Groups với health checks
  * Application Load Balancer với multiple targets
  * RDS automated backups với 7-day retention
  * CloudFront global edge locations

* **Performance Best Practices**:
  * CloudFront caching với appropriate TTL
  * Database connection pooling (HikariCP)
  * Lazy loading và code splitting cho frontend
  * Gzip compression cho static assets
  * CDN cho static content delivery

* **Cost Optimization Best Practices**:
  * Right-sizing instances (t3.nano/micro cho development)
  * VPC Endpoints thay vì NAT Gateway
  * S3 lifecycle policies cho old data
  * CloudWatch log retention policies
  * Reserved Instances cho production (long-term)

**8. Tài liệu Kỹ thuật:**
* Tạo các tài liệu chi tiết:
  * **Architecture Diagram**: Sơ đồ kiến trúc với tất cả components
  * **Network Diagram**: VPC layout với subnets và routing
  * **Security Diagram**: Security groups và IAM roles
  * **Deployment Guide**: Hướng dẫn triển khai từng bước
  * **Cost Analysis**: Breakdown chi phí theo dịch vụ
  * **Troubleshooting Guide**: Common issues và solutions

### Kết quả & Sản phẩm Tuần 11:

**Các Sản phẩm Hoàn thành:**
* ✅ CloudFormation template hoàn chỉnh (1,393 dòng)
* ✅ Sơ đồ kiến trúc hệ thống chi tiết
* ✅ Phân tích chi phí và tối ưu hóa
* ✅ Roadmap triển khai cho Week 12
* ✅ Môi trường phát triển đã cấu hình
* ✅ Tài liệu kỹ thuật và best practices
* ✅ IAM roles và security policies
* ✅ EC2 Key Pair và AWS credentials

**Các Chỉ số Kế hoạch:**
* **Tổng số dịch vụ AWS**: 15+ services
* **CloudFormation Resources**: 50+ resources
* **Ước tính Chi phí**: $30-35/tháng (production)
* **Thời gian Triển khai dự kiến**: 5 ngày (Week 12)
* **Target Performance**: <200ms API response, <2s page load
* **Target Availability**: 99.9% uptime

**Kiến trúc Đã Thiết kế:**
```
Internet
    │
    ├─── CloudFront (CDN) ──> S3 (Frontend React App)
    │                          └─── Static Assets (JS, CSS, Images)
    │
    └─── API Gateway ──> Application Load Balancer
                         └─── EC2 Auto Scaling Group (1-4 instances)
                              └─── Spring Boot Backend (Port 8080)
                                   └─── RDS MySQL (Private Subnet)
                                        └─── Automated Backups
         
         VPC Endpoints (Cost Optimization):
         ├─── S3 Gateway Endpoint (FREE)
         ├─── CloudWatch Interface Endpoint
         ├─── SSM Interface Endpoint
         └─── EC2 Interface Endpoint
```

**Công nghệ Stack:**
* **Frontend**: React 18, TypeScript, Vite, Material-UI, TailwindCSS
* **Backend**: Spring Boot 3.x, Java 17, Spring Security, JWT
* **Database**: MySQL 8.0, Spring Data JPA, HikariCP
* **Infrastructure**: CloudFormation, VPC, EC2, RDS, S3, CloudFront
* **Monitoring**: CloudWatch Logs, Metrics, Alarms, SNS
* **Security**: IAM, Security Groups, Encryption, HTTPS

### Bài học Kinh nghiệm:

**1. Tầm quan trọng của Planning:**
* **Bài học**: Lập kế hoạch chi tiết trước khi triển khai giúp tránh rework và tiết kiệm thời gian
* **Áp dụng**: Dành cả tuần để nghiên cứu, thiết kế và chuẩn bị thay vì rush vào implementation
* **Rút ra**: "Measure twice, cut once" - đầu tư thời gian vào planning sẽ được đền đáp trong execution phase

**2. Infrastructure as Code Benefits:**
* **Bài học**: CloudFormation cho phép version control, repeatability và automation
* **Áp dụng**: Template 1,393 dòng có thể deploy toàn bộ infrastructure trong 15-20 phút
* **Rút ra**: IaC là essential cho modern cloud applications - cho phép disaster recovery, environment replication và audit trails

**3. Cost Optimization từ Đầu:**
* **Bài học**: Tối ưu chi phí nên được xem xét trong giai đoạn thiết kế, không phải sau khi deploy
* **Áp dụng**: VPC Endpoints tiết kiệm $15-20/tháng so với NAT Gateway cho workload này
* **Rút ra**: Luôn phân tích cost-benefit của các architectural decisions - small optimizations add up

**4. Security by Design:**
* **Bài học**: Security phải được built-in từ đầu, không phải bolt-on sau
* **Áp dụng**: Private subnets, Security Groups, IAM roles, encryption - tất cả được thiết kế trong architecture
* **Rút ra**: Follow AWS Well-Architected Security Pillar - defense in depth, least privilege, encryption everywhere

**5. Multi-AZ cho High Availability:**
* **Bài học**: Multi-AZ deployment là critical cho production applications
* **Áp dụng**: Thiết kế 2 AZs với subnets, ALB và ASG spanning multiple zones
* **Rút ra**: Single point of failure là unacceptable cho production - luôn design cho redundancy

**6. Scalability Considerations:**
* **Bài học**: Design cho scale từ đầu - vertical scaling có limits, horizontal scaling is key
* **Áp dụng**: Auto Scaling Groups cho phép scale từ 1-4 instances dựa trên demand
* **Rút ra**: Use managed services (RDS, ALB) và stateless applications cho easy scaling

**7. Monitoring và Observability:**
* **Bài học**: Không thể manage những gì không measure được
* **Áp dụng**: CloudWatch Logs, Metrics, Alarms được thiết kế vào architecture từ đầu
* **Rút ra**: Implement comprehensive monitoring - logs, metrics, traces và alerts

**8. Documentation Importance:**
* **Bài học**: Good documentation accelerates development và troubleshooting
* **Áp dụng**: Tạo architecture diagrams, deployment guides và troubleshooting runbooks
* **Rút ra**: Time invested in documentation pays off in team onboarding, incident response và knowledge transfer

**9. AWS Service Selection:**
* **Bài học**: Chọn đúng AWS services cho use case là critical
* **Áp dụng**: S3+CloudFront cho static content, EC2+ASG cho backend, RDS cho database
* **Rút ra**: Understand service capabilities và limitations - managed services reduce operational overhead

**10. Template Validation:**
* **Bài học**: Validate CloudFormation templates trước khi deploy để catch errors early
* **Áp dụng**: Sử dụng `aws cloudformation validate-template` và cfn-lint
* **Rút ra**: Syntax errors trong templates có thể cause deployment failures - validate early và often

**11. Environment Preparation:**
* **Bài học**: Proper environment setup prevents deployment issues
* **Áp dụng**: AWS CLI, IAM credentials, Key Pairs, development tools - tất cả được chuẩn bị trước
* **Rút ra**: Checklist approach cho environment setup ensures nothing is missed

**12. Roadmap và Timeline:**
* **Bài học**: Clear roadmap với milestones giúp track progress và manage expectations
* **Áp dụng**: 5-day deployment plan với specific tasks cho mỗi ngày
* **Rút ra**: Break down complex projects into manageable tasks với clear deliverables

### References và Tài nguyên Học tập:

**AWS Official Documentation:**
* AWS Well-Architected Framework: <https://aws.amazon.com/architecture/well-architected/>
* CloudFormation User Guide: <https://docs.aws.amazon.com/cloudformation/>
* VPC User Guide: <https://docs.aws.amazon.com/vpc/>
* EC2 Auto Scaling: <https://docs.aws.amazon.com/autoscaling/ec2/>
* RDS Best Practices: <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.html>

**AWS Blogs và Whitepapers:**
* Cost Optimization with VPC Endpoints: <https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/>
* Building Modern Applications: <https://aws.amazon.com/modern-apps/>
* Security Best Practices: <https://docs.aws.amazon.com/security/>

**Spring Boot Resources:**
* Spring Boot Documentation: <https://docs.spring.io/spring-boot/>
* Deploying Spring Boot: <https://docs.spring.io/spring-boot/reference/deployment/>
* Spring Security: <https://docs.spring.io/spring-security/>

**React và Frontend:**
* React Documentation: <https://react.dev/>
* Vite Guide: <https://vitejs.dev/guide/>
* Web Performance: <https://web.dev/fast/>

**DevOps và Best Practices:**
* The Twelve-Factor App: <https://12factor.net/>
* AWS Architecture Center: <https://aws.amazon.com/architecture/>
* Cloud Design Patterns: <https://docs.microsoft.com/en-us/azure/architecture/patterns/>

