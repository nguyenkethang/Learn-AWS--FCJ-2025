---
title: "Workshop"
date: 2025-12-08
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai Ứng dụng Phân tích DNA trên AWS

#### Tổng quan

Trong workshop này, bạn sẽ học cách triển khai một ứng dụng phân tích DNA full-stack sẵn sàng cho production trên AWS sử dụng Infrastructure as Code (IaC) với CloudFormation. Ứng dụng bao gồm frontend React, backend Spring Boot, và cơ sở dữ liệu MySQL, tất cả được triển khai theo các best practices của AWS về bảo mật, khả năng mở rộng và tối ưu chi phí.

**Các dịch vụ AWS được sử dụng:**
- **VPC & Networking**: VPC, Subnets, Internet Gateway, NAT Gateway, VPC Endpoints
- **Compute**: EC2 Auto Scaling Group, Application Load Balancer
- **Storage & CDN**: S3 để lưu trữ frontend, CloudFront để phân phối nội dung toàn cầu
- **Database**: RDS MySQL để lưu trữ dữ liệu với sao lưu tự động
- **Security**: Security Groups, IAM Roles, AWS Cognito cho xác thực người dùng
- **Monitoring**: CloudWatch Logs, Alarms, và thông báo SNS
- **API Management**: API Gateway để expose backend API một cách an toàn

#### Bạn sẽ học được gì

1. **Infrastructure as Code**: Triển khai toàn bộ hạ tầng AWS bằng CloudFormation templates
2. **Thiết kế VPC**: Tạo VPC an toàn với public và private subnets trên nhiều availability zones
3. **Tối ưu chi phí**: Sử dụng VPC Endpoints để giảm chi phí NAT Gateway (~$20-25/tháng)
4. **Auto Scaling**: Cấu hình EC2 Auto Scaling dựa trên CPU metrics để đảm bảo high availability
5. **Quản lý Database**: Triển khai và cấu hình RDS MySQL với các best practices về bảo mật
6. **Triển khai Frontend**: Host static React website trên S3 với CloudFront CDN
7. **Triển khai Backend**: Deploy ứng dụng Spring Boot trên EC2 với systemd service
8. **Best Practices về Security**: Triển khai security groups, IAM roles, và Cognito authentication
9. **Monitoring & Logging**: Thiết lập CloudWatch để giám sát và cảnh báo ứng dụng

#### Sơ đồ Kiến trúc

```
Internet
    │
    ├─── CloudFront (CDN) ──> S3 (Frontend)
    │
    └─── API Gateway ──> ALB ──> EC2 (Backend) ──> RDS MySQL
                                  │
                                  └─── VPC Endpoints (S3, CloudWatch, SSM)
```

#### Yêu cầu trước khi bắt đầu

- Tài khoản AWS với quyền phù hợp (Administrator hoặc tương đương)
- AWS CLI đã cài đặt và cấu hình (`aws configure`)
- EC2 Key Pair đã được tạo trong AWS region của bạn (ap-southeast-1)
- Hiểu biết cơ bản về các dịch vụ AWS và command line interface
- Quen thuộc với các khái niệm CloudFormation

#### Chi phí ước tính

Chạy hạ tầng workshop này sẽ tốn khoảng **$8.90/tháng** (nếu chạy 24/7):

| Dịch vụ | Instance Type | Chi phí/tháng (USD) |
|---------|---------------|---------------------|
| EC2 | t3.nano | $3.50 |
| RDS MySQL | db.t3.micro | $2.80 |
| API Gateway | - | $0.50 |
| S3 + CloudFront | - | $0.80 |
| Route 53 | - | $0.50 |
| Cognito | - | $0.10 |
| CloudWatch | - | $0.30 |
| CI/CD (CodePipeline) | - | $0.40 |
| **Tổng** | | **$8.90** |

**Cho workshop (2-3 giờ):** ~$0.50-1.00

**💡 Mẹo tiết kiệm chi phí:**
- Xóa stack ngay sau khi hoàn thành workshop
- Sử dụng Free Tier cho các dịch vụ đủ điều kiện
- Tắt NAT Gateway khi không sử dụng (tiết kiệm ~$32/tháng)
- Sử dụng VPC Endpoints thay vì NAT Gateway cho production

#### Thời gian Workshop

- **Tổng thời gian**: 2-3 giờ
- **Triển khai Infrastructure**: 15-20 phút
- **Cấu hình Application**: 30-45 phút
- **Testing & Validation**: 15-30 phút
- **Cleanup**: 5-10 phút

#### Nội dung

1. [Tổng quan Workshop](5.1-workshop-overview/)
2. [Chuẩn bị & Yêu cầu](5.2-prerequisite/)
3. [Triển khai Infrastructure với CloudFormation](5.3-deploy-infrastructure/)
4. [Cấu hình và Triển khai Backend Application](5.4-deploy-backend/)
5. [Triển khai Frontend lên S3 và CloudFront](5.5-deploy-frontend/)
6. [Kiểm tra và Xác thực](5.6-testing/)
7. [Giám sát và Xử lý sự cố](5.7-monitoring/)
8. [Thiết lập CI/CD Pipeline](5.8-cicd-pipeline/)
9. [Dọn dẹp tài nguyên](5.9-cleanup/)

