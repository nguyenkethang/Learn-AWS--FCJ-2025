---
title: "Week 11 Work Log"
date: 2025-11-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Research and plan detailed DNA analysis application deployment project on AWS
* Analyze system architecture and required AWS services
* Design Infrastructure as Code with CloudFormation
* Prepare development environment and necessary tools
* Build deployment roadmap for 2 weeks

### Tasks to be implemented this week:

| Day | Tasks                                                                                                                                                                                   | Start Date | Completion Date | Documentation Sources                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Research full-stack application architecture on AWS <br> - Analyze suitable AWS services (VPC, EC2, RDS, S3, CloudFront) <br> - Learn about Infrastructure as Code with CloudFormation <br> - Read AWS Well-Architected Framework documentation | 2025/11/17   | 2025/11/17      | AWS Well-Architected Framework <br> <https://aws.amazon.com/architecture/well-architected/> <br> AWS CloudFormation Best Practices <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html> <br> Building Modern Applications on AWS <br> <https://aws.amazon.com/modern-apps/> |
| 2   | - Design VPC architecture with public and private subnets <br> - Plan Multi-AZ deployment configuration <br> - Research VPC Endpoints for cost optimization <br> - Draw detailed system architecture diagrams | 2025/11/18   | 2025/11/18      | Amazon VPC Design Best Practices <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-design.html> <br> VPC Endpoints Cost Optimization <br> <https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/> <br> Multi-AZ Deployments <br> <https://docs.aws.amazon.com/whitepapers/latest/real-time-communication-on-aws/high-availability-and-scalability-on-aws.html> |
| 3   | - Research Spring Boot deployment on EC2 <br> - Learn about Auto Scaling Groups and Load Balancers <br> - Learn how to configure systemd service for Java applications <br> - Research RDS MySQL best practices | 2025/11/19   | 2025/11/19      | Deploying Spring Boot Applications <br> <https://docs.spring.io/spring-boot/reference/deployment/installing.html> <br> EC2 Auto Scaling Best Practices <br> <https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-best-practices.html> <br> Amazon RDS Best Practices <br> <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.html> |
| 4   | - Research React deployment with S3 and CloudFront <br> - Learn about CloudFront caching strategies <br> - Learn how to optimize frontend build with Vite <br> - Research CORS configuration for API Gateway | 2025/11/20   | 2025/11/20      | Hosting Static Website on S3 <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html> <br> CloudFront Performance Optimization <br> <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/ConfiguringCaching.html> <br> Vite Build Optimization <br> <https://vitejs.dev/guide/build.html> <br> API Gateway CORS Configuration <br> <https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html> |
| 5   | - Build detailed CloudFormation template <br> - Configure parameters and outputs <br> - Validate template syntax <br> - Prepare AWS environment (IAM roles, Key Pairs) <br> - Create detailed deployment roadmap for week 12 | 2025/11/21   | 2025/11/23      | CloudFormation Template Anatomy <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html> <br> CloudFormation Parameters <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html> <br> IAM Best Practices <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html> |

### Week 11 Achievements:

**1. System Architecture Analysis:**
* Completed detailed architecture analysis for DNA Analysis application:
  * **Frontend Layer**: React 18 + TypeScript with Material-UI and TailwindCSS
  * **Backend Layer**: Spring Boot 3.x with Java 17, Spring Security and JWT authentication
  * **Database Layer**: RDS MySQL 8.0 with automated backups and encryption
  * **CDN Layer**: CloudFront distribution for global content delivery
  * **API Layer**: API Gateway with VPC Link integration

* Identified non-functional requirements:
  * **Performance**: Response time < 200ms, page load < 2s
  * **Scalability**: Auto scaling from 1-4 instances based on CPU metrics
  * **Availability**: Multi-AZ deployment with 99.9% uptime target
  * **Security**: Encryption at rest and in transit, least privilege access
  * **Cost**: Target ~$30-40/month for production workload

**2. VPC Architecture Design:**
* Designed complete VPC architecture:
  * **VPC CIDR**: 10.0.0.0/16 (65,536 IP addresses)
  * **Public Subnets**: 
    - 10.0.1.0/24 (AZ-1) - 256 IPs for ALB, NAT Gateway
    - 10.0.3.0/24 (AZ-2) - 256 IPs for high availability
  * **Private Subnets**:
    - 10.0.2.0/24 (AZ-1) - 256 IPs for EC2 instances
    - 10.0.4.0/24 (AZ-2) - 256 IPs for RDS and EC2 backup

* Planned network components:
  * Internet Gateway for public internet access
  * NAT Gateway in public subnet (can be replaced with VPC Endpoints)
  * Separate Route Tables for public and private subnets
  * VPC Endpoints for S3, CloudWatch, SSM, EC2 (saves ~$20-25/month)

**3. Cost Optimization Research:**
* Analyzed projected costs:
  * **EC2 t3.nano**: $3.50/month (development), t3.micro $7/month (production)
  * **RDS db.t3.micro**: $2.80/month (Single-AZ), $5.60/month (Multi-AZ)
  * **NAT Gateway**: $32.40/month + data transfer $5-10/month
  * **VPC Endpoints**: $7.20/endpoint/month (~$21.60 for 3 endpoints)
  * **S3 + CloudFront**: $0.80/month (with Free Tier)
  * **API Gateway**: $0.50/month
  * **CloudWatch**: $0.30/month

* Identified optimization strategy:
  * Use VPC Endpoints instead of NAT Gateway: saves ~$15-20/month
  * S3 Gateway Endpoint: FREE (no charges)
  * Interface Endpoints for CloudWatch, SSM, EC2: $21.60/month
  * Total projected cost: $30-35/month (optimized)

**4. CloudFormation Template Development:**
* Completed CloudFormation template with 1,393 lines of code:
  * **Parameters Section** (50 lines): Environment, KeyName, InstanceType, DBPassword
  * **Networking Resources** (400 lines): VPC, Subnets, IGW, NAT, Route Tables, VPC Endpoints
  * **Compute Resources** (300 lines): Launch Template, ASG, ALB, Target Group, Scaling Policies
  * **Storage Resources** (200 lines): S3 Buckets, CloudFront Distribution, OAI
  * **Database Resources** (100 lines): RDS Instance, Subnet Group, Parameter Group
  * **Security Resources** (200 lines): Security Groups, IAM Roles, Instance Profile
  * **Monitoring Resources** (143 lines): CloudWatch Logs, Alarms, SNS Topic, API Gateway

* Successfully validated template syntax:
  ```bash
  aws cloudformation validate-template --template-body file://infrastructure.yaml
  ```

**5. Development Environment Preparation:**
* Installed and configured tools:
  * **AWS CLI v2**: Configured with credentials and default region (ap-southeast-1)
  * **Java 17 JDK**: For Spring Boot development
  * **Maven 3.9+**: For building backend JAR files
  * **Node.js 18+ & npm**: For React frontend development
  * **Git**: For version control
  * **VS Code**: With extensions for Java, React, CloudFormation

* Created EC2 Key Pair:
  * Key name: `workshop-keypair`
  * Region: ap-southeast-1 (Singapore)
  * Downloaded and securely stored private key

* Configured IAM User:
  * Created IAM user with programmatic access
  * Attached policies: AdministratorAccess (for workshop)
  * Configured AWS CLI credentials
  * Enabled MFA for security

**6. Deployment Roadmap:**
* **Week 12 - Day 1 (24/11)**: Deploy Infrastructure
  * Deploy CloudFormation stack
  * Verify all resources created successfully
  * Check VPC, Subnets, Security Groups

* **Week 12 - Day 2 (25/11)**: Deploy Backend
  * Build Spring Boot JAR file
  * Upload to S3 backend bucket
  * Deploy to EC2 instances
  * Configure database connection

* **Week 12 - Day 3 (26/11)**: Deploy Frontend
  * Build React production bundle
  * Upload to S3 frontend bucket
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


**7. Best Practices Research:**
* **Security Best Practices**:
  * Principle of least privilege for IAM roles
  * Encryption at rest (RDS, S3) and in transit (HTTPS, SSL/TLS)
  * Private subnets for sensitive resources (EC2, RDS)
  * Security Groups with specific port ranges
  * No hardcoded credentials - use IAM roles and Secrets Manager

* **High Availability Best Practices**:
  * Multi-AZ deployment for critical components
  * Auto Scaling Groups with health checks
  * Application Load Balancer with multiple targets
  * RDS automated backups with 7-day retention
  * CloudFront global edge locations

* **Performance Best Practices**:
  * CloudFront caching with appropriate TTL
  * Database connection pooling (HikariCP)
  * Lazy loading and code splitting for frontend
  * Gzip compression for static assets
  * CDN for static content delivery

* **Cost Optimization Best Practices**:
  * Right-sizing instances (t3.nano/micro for development)
  * VPC Endpoints instead of NAT Gateway
  * S3 lifecycle policies for old data
  * CloudWatch log retention policies
  * Reserved Instances for production (long-term)

**8. Technical Documentation:**
* Created detailed documentation:
  * **Architecture Diagram**: System architecture with all components
  * **Network Diagram**: VPC layout with subnets and routing
  * **Security Diagram**: Security groups and IAM roles
  * **Deployment Guide**: Step-by-step deployment instructions
  * **Cost Analysis**: Cost breakdown by service
  * **Troubleshooting Guide**: Common issues and solutions

### Week 11 Results & Deliverables:

**Completed Deliverables:**
* ✅ Complete CloudFormation template (1,393 lines)
* ✅ Detailed system architecture diagrams
* ✅ Cost analysis and optimization plan
* ✅ Deployment roadmap for Week 12
* ✅ Configured development environment
* ✅ Technical documentation and best practices
* ✅ IAM roles and security policies
* ✅ EC2 Key Pair and AWS credentials

**Planning Metrics:**
* **Total AWS Services**: 15+ services
* **CloudFormation Resources**: 50+ resources
* **Estimated Cost**: $30-35/month (production)
* **Expected Deployment Time**: 5 days (Week 12)
* **Target Performance**: <200ms API response, <2s page load
* **Target Availability**: 99.9% uptime

**Designed Architecture:**
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

**Technology Stack:**
* **Frontend**: React 18, TypeScript, Vite, Material-UI, TailwindCSS
* **Backend**: Spring Boot 3.x, Java 17, Spring Security, JWT
* **Database**: MySQL 8.0, Spring Data JPA, HikariCP
* **Infrastructure**: CloudFormation, VPC, EC2, RDS, S3, CloudFront
* **Monitoring**: CloudWatch Logs, Metrics, Alarms, SNS
* **Security**: IAM, Security Groups, Encryption, HTTPS

### Lessons Learned:

**1. Importance of Planning:**
* **Lesson**: Detailed planning before deployment helps avoid rework and saves time
* **Application**: Spent entire week researching, designing and preparing instead of rushing into implementation
* **Takeaway**: "Measure twice, cut once" - time invested in planning pays off in execution phase

**2. Infrastructure as Code Benefits:**
* **Lesson**: CloudFormation enables version control, repeatability and automation
* **Application**: 1,393-line template can deploy entire infrastructure in 15-20 minutes
* **Takeaway**: IaC is essential for modern cloud applications - enables disaster recovery, environment replication and audit trails

**3. Cost Optimization from Start:**
* **Lesson**: Cost optimization should be considered in design phase, not after deployment
* **Application**: VPC Endpoints save $15-20/month compared to NAT Gateway for this workload
* **Takeaway**: Always analyze cost-benefit of architectural decisions - small optimizations add up

**4. Security by Design:**
* **Lesson**: Security must be built-in from the start, not bolted-on later
* **Application**: Private subnets, Security Groups, IAM roles, encryption - all designed into architecture
* **Takeaway**: Follow AWS Well-Architected Security Pillar - defense in depth, least privilege, encryption everywhere

**5. Multi-AZ for High Availability:**
* **Lesson**: Multi-AZ deployment is critical for production applications
* **Application**: Designed 2 AZs with subnets, ALB and ASG spanning multiple zones
* **Takeaway**: Single point of failure is unacceptable for production - always design for redundancy

**6. Scalability Considerations:**
* **Lesson**: Design for scale from the start - vertical scaling has limits, horizontal scaling is key
* **Application**: Auto Scaling Groups allow scaling from 1-4 instances based on demand
* **Takeaway**: Use managed services (RDS, ALB) and stateless applications for easy scaling

**7. Monitoring and Observability:**
* **Lesson**: Cannot manage what you cannot measure
* **Application**: CloudWatch Logs, Metrics, Alarms designed into architecture from start
* **Takeaway**: Implement comprehensive monitoring - logs, metrics, traces and alerts

**8. Documentation Importance:**
* **Lesson**: Good documentation accelerates development and troubleshooting
* **Application**: Created architecture diagrams, deployment guides and troubleshooting runbooks
* **Takeaway**: Time invested in documentation pays off in team onboarding, incident response and knowledge transfer

**9. AWS Service Selection:**
* **Lesson**: Choosing right AWS services for use case is critical
* **Application**: S3+CloudFront for static content, EC2+ASG for backend, RDS for database
* **Takeaway**: Understand service capabilities and limitations - managed services reduce operational overhead

**10. Template Validation:**
* **Lesson**: Validate CloudFormation templates before deployment to catch errors early
* **Application**: Used `aws cloudformation validate-template` and cfn-lint
* **Takeaway**: Syntax errors in templates can cause deployment failures - validate early and often

**11. Environment Preparation:**
* **Lesson**: Proper environment setup prevents deployment issues
* **Application**: AWS CLI, IAM credentials, Key Pairs, development tools - all prepared beforehand
* **Takeaway**: Checklist approach for environment setup ensures nothing is missed

**12. Roadmap and Timeline:**
* **Lesson**: Clear roadmap with milestones helps track progress and manage expectations
* **Application**: 5-day deployment plan with specific tasks for each day
* **Takeaway**: Break down complex projects into manageable tasks with clear deliverables

### References and Learning Resources:

**AWS Official Documentation:**
* AWS Well-Architected Framework: <https://aws.amazon.com/architecture/well-architected/>
* CloudFormation User Guide: <https://docs.aws.amazon.com/cloudformation/>
* VPC User Guide: <https://docs.aws.amazon.com/vpc/>
* EC2 Auto Scaling: <https://docs.aws.amazon.com/autoscaling/ec2/>
* RDS Best Practices: <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.html>

**AWS Blogs and Whitepapers:**
* Cost Optimization with VPC Endpoints: <https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/>
* Building Modern Applications: <https://aws.amazon.com/modern-apps/>
* Security Best Practices: <https://docs.aws.amazon.com/security/>

**Spring Boot Resources:**
* Spring Boot Documentation: <https://docs.spring.io/spring-boot/>
* Deploying Spring Boot: <https://docs.spring.io/spring-boot/reference/deployment/>
* Spring Security: <https://docs.spring.io/spring-security/>

**React and Frontend:**
* React Documentation: <https://react.dev/>
* Vite Guide: <https://vitejs.dev/guide/>
* Web Performance: <https://web.dev/fast/>

**DevOps and Best Practices:**
* The Twelve-Factor App: <https://12factor.net/>
* AWS Architecture Center: <https://aws.amazon.com/architecture/>
* Cloud Design Patterns: <https://docs.microsoft.com/en-us/azure/architecture/patterns/>

