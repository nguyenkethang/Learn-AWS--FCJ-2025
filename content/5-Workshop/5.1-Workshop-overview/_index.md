---
title: "Workshop Overview"
date: 2025-12-08
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

## Introduction

This workshop guides you through deploying a full-stack DNA Analysis application on AWS. The application allows users to analyze DNA sequences, manage results, and visualize biological data.

## Application Architecture

### Frontend (React + Vite)
- **Framework**: React 18 with TypeScript
- **UI Libraries**: Material-UI, TailwindCSS, Recharts
- **State Management**: React Context API
- **Routing**: React Router v6
- **Form Handling**: React Hook Form with Zod validation
- **HTTP Client**: Axios
- **Hosting**: S3 + CloudFront CDN

### Backend (Spring Boot)
- **Framework**: Spring Boot 3.x
- **Language**: Java 17
- **Database**: MySQL 8.0 with Spring Data JPA
- **Security**: Spring Security with JWT authentication
- **API**: RESTful API with proper error handling
- **Hosting**: EC2 instances with Auto Scaling

### Database (RDS MySQL)
- **Engine**: MySQL 8.0.40
- **Instance**: db.t3.micro (scalable)
- **Storage**: 20GB gp3 with encryption
- **Backup**: Automated backups with 3-7 days retention
- **High Availability**: Multi-AZ deployment (optional)

## AWS Architecture

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

## Key Features

### 1. User Authentication
- User registration and login
- JWT token-based authentication
- AWS Cognito integration (optional)
- Session management

### 2. DNA Analysis
- Upload and analyze DNA sequences
- Support multiple file formats
- Batch processing capability
- Store analysis results

### 3. Data Visualization
- DNA analysis charts
- Dashboard with metrics
- Export results in multiple formats

### 4. User Management
- User profile management
- Analysis history
- Role-based access control

## Infrastructure as Code

### CloudFormation Template
The `infrastructure.yaml` template includes:

**Networking (Lines 1-400)**
- VPC with DNS support
- 2 Public Subnets (Multi-AZ)
- 2 Private Subnets (Multi-AZ)
- Internet Gateway
- NAT Gateway (can be disabled for cost savings)
- Route Tables
- VPC Endpoints (S3, CloudWatch, SSM, Cognito)

**Compute (Lines 400-700)**
- Launch Template with User Data script
- Auto Scaling Group (1-4 instances)
- Application Load Balancer
- Target Group with health checks
- Scaling Policies (CPU-based)

**Storage & CDN (Lines 700-900)**
- S3 Bucket for Frontend
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
- SNS Topic for alerts
- API Gateway with CORS

## Cost Optimization

### 1. VPC Endpoints instead of NAT Gateway
**Savings**: ~$20-25/month
- S3 Gateway Endpoint: FREE
- Interface Endpoints: $7.20/endpoint/month
- Total: ~$28/month vs NAT Gateway $32/month + data transfer

### 2. Instance Sizing
**Development**: t3.micro ($7-10/month)
**Production**: t3.small or t3.medium

### 3. RDS Optimization
- Single-AZ for development
- Multi-AZ for production
- Automated backups with appropriate retention

### 4. CloudFront Caching
- Reduce requests to S3
- Lower latency for users
- Free tier: 1TB data transfer/month

## Best Practices Applied

### 1. Security
✅ Private subnets for EC2 and RDS
✅ Security Groups with least privilege
✅ IAM Roles instead of hardcoded credentials
✅ Encryption at rest and in transit
✅ VPC Endpoints for private connectivity
✅ CloudTrail for audit logging (optional)

### 2. High Availability
✅ Multi-AZ deployment
✅ Auto Scaling Group
✅ Application Load Balancer
✅ RDS automated backups
✅ CloudFront global CDN

### 3. Monitoring & Logging
✅ CloudWatch Logs for application logs
✅ CloudWatch Alarms for metrics
✅ SNS notifications
✅ Health checks on ALB and ASG

### 4. Automation
✅ Infrastructure as Code with CloudFormation
✅ User Data scripts for EC2 initialization
✅ Systemd service for application management
✅ Automated deployments with scripts

## Deployment Steps

1. **Preparation** (10 minutes)
   - Install AWS CLI
   - Create EC2 Key Pair
   - Configure parameters

2. **Deploy Infrastructure** (15-20 minutes)
   - Validate CloudFormation template
   - Create stack
   - Wait for resources to be created

3. **Deploy Backend** (20-30 minutes)
   - Build JAR file
   - Upload to S3
   - Deploy to EC2
   - Configure database connection

4. **Deploy Frontend** (10-15 minutes)
   - Build React application
   - Upload to S3
   - Invalidate CloudFront cache

5. **Testing** (15-30 minutes)
   - Test authentication
   - Test DNA analysis features
   - Verify monitoring

6. **Cleanup** (5-10 minutes)
   - Delete CloudFormation stack
   - Verify all resources deleted

## Expected Outcomes

After completing this workshop, you will have:

✅ A working full-stack application on AWS
✅ Deep understanding of AWS networking and security
✅ Experience with Infrastructure as Code
✅ Knowledge of cost optimization
✅ Best practices for production deployment

## Reference Resources

- [AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/)
- [AWS VPC Best Practices](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Spring Boot on AWS](https://spring.io/guides/gs/spring-boot-aws/)
- [React Deployment Best Practices](https://create-react-app.dev/docs/deployment/)

