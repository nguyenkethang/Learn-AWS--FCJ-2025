---
title: "Workshop"
date: 2025-12-08
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploy DNA Analysis Application on AWS

#### Overview

In this workshop, you will learn how to deploy a production-ready full-stack DNA Analysis application on AWS using Infrastructure as Code (IaC) with CloudFormation. The application consists of a React frontend, Spring Boot backend, and MySQL database, all deployed with AWS best practices for security, scalability, and cost optimization.

**AWS Services Used:**
- **VPC & Networking**: VPC, Subnets, Internet Gateway, NAT Gateway, VPC Endpoints
- **Compute**: EC2 Auto Scaling Group, Application Load Balancer
- **Storage & CDN**: S3 for frontend hosting, CloudFront for global content delivery
- **Database**: RDS MySQL for data persistence with automated backups
- **Security**: Security Groups, IAM Roles, AWS Cognito for user authentication
- **Monitoring**: CloudWatch Logs, Alarms, and SNS notifications
- **API Management**: API Gateway for secure backend API exposure

#### What You Will Learn

1. **Infrastructure as Code**: Deploy complete AWS infrastructure using CloudFormation templates
2. **VPC Design**: Create a secure VPC with public and private subnets across multiple availability zones
3. **Cost Optimization**: Use VPC Endpoints to reduce NAT Gateway costs (~$20-25/month savings)
4. **Auto Scaling**: Configure EC2 Auto Scaling based on CPU metrics for high availability
5. **Database Management**: Deploy and configure RDS MySQL with security best practices
6. **Frontend Deployment**: Host static React website on S3 with CloudFront CDN
7. **Backend Deployment**: Deploy Spring Boot application on EC2 with systemd service
8. **Security Best Practices**: Implement security groups, IAM roles, and Cognito authentication
9. **Monitoring & Logging**: Set up CloudWatch for application monitoring and alerting

#### Architecture Diagram

```
Internet
    │
    ├─── CloudFront (CDN) ──> S3 (Frontend)
    │
    └─── API Gateway ──> ALB ──> EC2 (Backend) ──> RDS MySQL
                                  │
                                  └─── VPC Endpoints (S3, CloudWatch, SSM)
```

#### Prerequisites

- AWS Account with appropriate permissions (Administrator or equivalent)
- AWS CLI installed and configured (`aws configure`)
- EC2 Key Pair created in your AWS region (ap-southeast-1)
- Basic understanding of AWS services and command line interface
- Familiarity with CloudFormation concepts

#### Estimated Cost

Running this workshop infrastructure will cost approximately **$8.90/month** (if running 24/7):

| Service | Instance Type | Cost/month (USD) |
|---------|---------------|------------------|
| EC2 | t3.nano | $3.50 |
| RDS MySQL | db.t3.micro | $2.80 |
| API Gateway | - | $0.50 |
| S3 + CloudFront | - | $0.80 |
| Route 53 | - | $0.50 |
| Cognito | - | $0.10 |
| CloudWatch | - | $0.30 |
| CI/CD (CodePipeline) | - | $0.40 |
| **Total** | | **$8.90** |

**For workshop (2-3 hours):** ~$0.50-1.00

**💡 Cost Saving Tips:**
- Delete the stack immediately after workshop completion
- Use AWS Free Tier for eligible services
- Disable NAT Gateway when not in use (saves ~$32/month)
- Use VPC Endpoints instead of NAT Gateway for production

#### Workshop Duration

- **Total Time**: 2-3 hours
- **Infrastructure Deployment**: 15-20 minutes
- **Application Configuration**: 30-45 minutes
- **Testing & Validation**: 15-30 minutes
- **Cleanup**: 5-10 minutes

#### Content

1. [Workshop Overview](5.1-workshop-overview/)
2. [Prerequisites & Preparation](5.2-prerequisite/)
3. [Deploy Infrastructure with CloudFormation](5.3-deploy-infrastructure/)
4. [Configure and Deploy Backend Application](5.4-deploy-backend/)
5. [Deploy Frontend to S3 and CloudFront](5.5-deploy-frontend/)
6. [Testing and Validation](5.6-testing/)
7. [Monitoring and Troubleshooting](5.7-monitoring/)
8. [CI/CD Pipeline Setup](5.8-cicd-pipeline/)
9. [Clean Up Resources](5.9-cleanup/)

