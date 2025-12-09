---
title: "Tổng quan Workshop"
date: 2025-12-08
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

## Giới thiệu

Workshop này hướng dẫn bạn triển khai một ứng dụng phân tích DNA full-stack trên AWS. Ứng dụng cho phép người dùng phân tích chuỗi DNA, quản lý kết quả, và trực quan hóa dữ liệu sinh học.

## Kiến trúc Ứng dụng

### Frontend (React + Vite)
- **Framework**: React 18 với TypeScript
- **UI Libraries**: Material-UI, TailwindCSS, Recharts
- **State Management**: React Context API
- **Routing**: React Router v6
- **Form Handling**: React Hook Form với Zod validation
- **HTTP Client**: Axios
- **Hosting**: S3 + CloudFront CDN

### Backend (Spring Boot)
- **Framework**: Spring Boot 3.x
- **Language**: Java 17
- **Database**: MySQL 8.0 với Spring Data JPA
- **Security**: Spring Security với JWT authentication
- **API**: RESTful API với proper error handling
- **Hosting**: EC2 instances với Auto Scaling

### Database (RDS MySQL)
- **Engine**: MySQL 8.0.40
- **Instance**: db.t3.micro (có thể scale up)
- **Storage**: 20GB gp3 với encryption
- **Backup**: Automated backups với 3-7 days retention
- **High Availability**: Multi-AZ deployment (optional)

## Kiến trúc AWS

### Network Layer
```
VPC (10.0.0.0/16)
├── Public Subnets (10.0.1.0/24, 10.0.3.0/24)
│   ├── Internet Gateway
│   ├── NAT Gateway
│   └── Application Load Balancer
│
└── Private Subnets (10.0.2.0/24, 10.0.4.0/24)
    ├── EC2 Instances (Auto Scaling Group)
    ├── RDS MySQL (Multi-AZ)
    └── VPC Endpoints (S3, CloudWatch, SSM, Cognito)
```

### Application Flow
```
User Browser
    │
    ├─── HTTPS ──> CloudFront ──> S3 (Static Frontend)
    │
    └─── HTTPS ──> API Gateway ──> ALB ──> EC2 (Backend API)
                                            │
                                            └──> RDS MySQL
```

### Security Architecture
```
Internet
    │
    ├─── CloudFront (HTTPS only)
    │    └─── S3 Bucket Policy (CloudFront OAI)
    │
    └─── API Gateway (Resource Policy)
         └─── ALB Security Group (Port 80/443)
              └─── EC2 Security Group (Port 8080 from ALB only)
                   └─── RDS Security Group (Port 3306 from EC2 only)
```

## Các Tính năng Chính

### 1. User Authentication
- Đăng ký và đăng nhập người dùng
- JWT token-based authentication
- AWS Cognito integration (optional)
- Session management

### 2. DNA Analysis
- Upload và phân tích chuỗi DNA
- Hỗ trợ nhiều định dạng file
- Xử lý batch processing
- Lưu trữ kết quả phân tích

### 3. Data Visualization
- Biểu đồ phân tích DNA
- Dashboard với metrics
- Export kết quả dưới nhiều định dạng

### 4. User Management
- Quản lý profile người dùng
- Lịch sử phân tích
- Role-based access control

## Infrastructure as Code

### CloudFormation Template
Template `infrastructure.yaml` bao gồm:

**Networking (Lines 1-400)**
- VPC với DNS support
- 2 Public Subnets (Multi-AZ)
- 2 Private Subnets (Multi-AZ)
- Internet Gateway
- NAT Gateway (có thể tắt để tiết kiệm chi phí)
- Route Tables
- VPC Endpoints (S3, CloudWatch, SSM, Cognito)

**Compute (Lines 400-700)**
- Launch Template với User Data script
- Auto Scaling Group (1-4 instances)
- Application Load Balancer
- Target Group với health checks
- Scaling Policies (CPU-based)

**Storage & CDN (Lines 700-900)**
- S3 Bucket cho Frontend
- S3 Bucket Policy
- CloudFront Distribution
- CloudFront Origin Access Identity

**Database (Lines 900-1000)**
- RDS MySQL Instance
- DB Subnet Group
- Automated Backups
- Encryption at rest

**Security (Lines 1000-1200)**
- Security Groups (ALB, EC2, RDS, VPC Endpoints)
- IAM Roles (EC2, CloudWatch, S3)
- IAM Instance Profile
- Cognito User Pool (optional)
- Secrets Manager (optional)

**Monitoring (Lines 1200-1393)**
- CloudWatch Log Groups
- CloudWatch Alarms (CPU, Memory)
- SNS Topic cho alerts
- API Gateway với CORS

## Tối ưu Chi phí

### 1. VPC Endpoints thay vì NAT Gateway
**Tiết kiệm**: ~$20-25/tháng
- S3 Gateway Endpoint: FREE
- Interface Endpoints: $7.20/endpoint/tháng
- Tổng: ~$28/tháng vs NAT Gateway $32/tháng + data transfer

### 2. Instance Sizing
**Development**: t3.micro ($7-10/tháng)
**Production**: t3.small hoặc t3.medium

### 3. RDS Optimization
- Single-AZ cho development
- Multi-AZ cho production
- Automated backups với retention phù hợp

### 4. CloudFront Caching
- Giảm requests đến S3
- Giảm latency cho users
- Free tier: 1TB data transfer/tháng

## Best Practices được áp dụng

### 1. Security
✅ Private subnets cho EC2 và RDS
✅ Security Groups với least privilege
✅ IAM Roles thay vì hardcoded credentials
✅ Encryption at rest và in transit
✅ VPC Endpoints cho private connectivity
✅ CloudTrail cho audit logging (optional)

### 2. High Availability
✅ Multi-AZ deployment
✅ Auto Scaling Group
✅ Application Load Balancer
✅ RDS automated backups
✅ CloudFront global CDN

### 3. Monitoring & Logging
✅ CloudWatch Logs cho application logs
✅ CloudWatch Alarms cho metrics
✅ SNS notifications
✅ Health checks trên ALB và ASG

### 4. Automation
✅ Infrastructure as Code với CloudFormation
✅ User Data scripts cho EC2 initialization
✅ Systemd service cho application management
✅ Automated deployments với scripts

## Các Bước Triển khai

1. **Chuẩn bị** (10 phút)
   - Cài đặt AWS CLI
   - Tạo EC2 Key Pair
   - Cấu hình parameters

2. **Deploy Infrastructure** (15-20 phút)
   - Validate CloudFormation template
   - Create stack
   - Đợi resources được tạo

3. **Deploy Backend** (20-30 phút)
   - Build JAR file
   - Upload lên S3
   - Deploy lên EC2
   - Cấu hình database connection

4. **Deploy Frontend** (10-15 phút)
   - Build React application
   - Upload lên S3
   - Invalidate CloudFront cache

5. **Testing** (15-30 phút)
   - Test authentication
   - Test DNA analysis features
   - Verify monitoring

6. **Cleanup** (5-10 phút)
   - Delete CloudFormation stack
   - Verify all resources deleted

## Kết quả Mong đợi

Sau khi hoàn thành workshop, bạn sẽ có:

✅ Một ứng dụng full-stack hoạt động trên AWS
✅ Hiểu biết sâu về AWS networking và security
✅ Kinh nghiệm với Infrastructure as Code
✅ Kiến thức về cost optimization
✅ Best practices cho production deployment

## Tài nguyên Tham khảo

- [AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/)
- [AWS VPC Best Practices](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Spring Boot on AWS](https://spring.io/guides/gs/spring-boot-aws/)
- [React Deployment Best Practices](https://create-react-app.dev/docs/deployment/)

