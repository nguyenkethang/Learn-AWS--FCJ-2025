---
title: "Week 9 Worklog"
date: 2025-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Deploy complete AWS infrastructure using CloudFormation (Infrastructure as Code)
* Configure and deploy Spring Boot backend application to EC2
* Implement automated deployment pipeline with systemd service
* Establish database connectivity and verify application health

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Study CloudFormation template structure and syntax <br> - Review VPC architecture design (public/private subnets) <br> - Understand Auto Scaling Group and Load Balancer configuration <br> - Prepare deployment parameters (KeyPair, AMI ID, region) | 2025/11/03 | 2025/11/03 | AWS CloudFormation User Guide <br> <https://docs.aws.amazon.com/cloudformation/> <br> AWS VPC Best Practices <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-best-practices.html> <br> CloudFormation Template Reference <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html> |
| 2   | - Validate CloudFormation template syntax <br> - Deploy infrastructure stack (VPC, EC2, RDS, ALB, S3, CloudFront) <br> - Monitor stack creation progress and troubleshoot errors <br> - Verify all resources created successfully | 2025/11/04 | 2025/11/04 | AWS CloudFormation Stack Creation <br> <https://docs.aws.amazon.com/cloudformation/latest/userguide/cfn-console-create-stack.html> <br> Troubleshooting CloudFormation <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/troubleshooting.html> |
| 3   | - Extract CloudFormation outputs (RDS endpoint, ALB DNS, S3 bucket names) <br> - Configure Spring Boot application.properties with RDS connection <br> - Build backend JAR file using Maven <br> - Upload JAR to S3 backend artifacts bucket | 2025/11/05 | 2025/11/05 | Spring Boot Configuration Properties <br> <https://docs.spring.io/spring-boot/reference/features/external-config.html> <br> Maven Build Lifecycle <br> <https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html> <br> AWS S3 CLI Reference <br> <https://docs.aws.amazon.com/cli/latest/reference/s3/> |
| 4   | - Connect to EC2 instance via AWS Systems Manager Session Manager <br> - Download JAR from S3 to EC2 instance <br> - Configure application properties on EC2 <br> - Start Spring Boot application and verify health endpoint | 2025/11/06 | 2025/11/06 | AWS Systems Manager Session Manager <br> <https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html> <br> Spring Boot Actuator Health Endpoint <br> <https://docs.spring.io/spring-boot/reference/actuator/endpoints.html> |
| 5   | - Create systemd service unit file for auto-start <br> - Configure application logging to CloudWatch <br> - Test application via Load Balancer and API Gateway <br> - Verify database connectivity and data persistence <br> - Document deployment process and troubleshooting steps | 2025/11/07 | 2025/11/09 | Systemd Service Management <br> <https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html> <br> AWS CloudWatch Logs Agent <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_GettingStarted.html> <br> Spring Boot Production Best Practices <br> <https://docs.spring.io/spring-boot/reference/deployment/installing.html> |

### Week 9 Achievements:

**1. Infrastructure Deployment with CloudFormation:**
* Successfully deployed complete AWS infrastructure stack including:
  * **VPC Architecture**: Created VPC with CIDR 10.0.0.0/16, 2 public subnets (10.0.1.0/24, 10.0.2.0/24), 2 private subnets (10.0.3.0/24, 10.0.4.0/24) across 2 availability zones
  * **Networking Components**: Internet Gateway, NAT Gateway, Route Tables with proper routing configuration
  * **Compute Resources**: EC2 Auto Scaling Group with t3.nano instances, Application Load Balancer with health checks
  * **Database**: RDS MySQL db.t3.micro instance in private subnet with automated backups
  * **Storage & CDN**: S3 buckets for frontend/backend, CloudFront distribution for global content delivery
  * **Security**: Security Groups with least-privilege access, IAM roles for EC2 and services
  * **API Management**: API Gateway REST API with VPC Link integration to ALB

* Deployment completed in approximately 18 minutes with all resources in healthy state

**2. CloudFormation Template Validation:**
* Validated template syntax using AWS CLI before deployment
* Identified and resolved parameter issues (KeyPair name, AMI ID for region)
* Implemented proper resource dependencies and DependsOn attributes
* Used CloudFormation outputs for easy access to resource identifiers

**3. Backend Application Configuration:**
* Configured Spring Boot application.properties with:
  * RDS MySQL connection string with SSL enabled
  * HikariCP connection pool (max 10, min 5 connections)
  * JPA Hibernate auto-update for schema management
  * JWT authentication with secure signing key
  * CORS configuration for frontend integration
  * CloudWatch logging configuration

* Built production-ready JAR file (workshop-0.0.1-SNAPSHOT.jar, ~65MB)
* Uploaded JAR to S3 backend artifacts bucket for version control

**4. EC2 Deployment and Configuration:**
* Connected to EC2 instance using AWS Systems Manager Session Manager (no SSH key required)
* Downloaded application JAR from S3 to /opt/workshop directory
* Created application.properties with environment-specific configuration
* Started Spring Boot application successfully on port 8080
* Verified health endpoint returned `{"status":"UP"}`

**5. Systemd Service Implementation:**
* Created systemd service unit file (/etc/systemd/system/workshop.service)
* Configured automatic restart on failure with 10-second delay
* Enabled service to start on system boot
* Implemented proper logging to /opt/workshop/application.log
* Tested service start/stop/restart operations

**6. Application Verification:**
* **Local Testing**: Verified application responds on localhost:8080
* **Load Balancer Testing**: Confirmed ALB health checks passing, traffic routing correctly
* **API Gateway Testing**: Validated API Gateway integration with backend
* **Database Connectivity**: Confirmed RDS connection successful, queries executing properly
* **CloudWatch Logs**: Verified application logs streaming to CloudWatch Logs group

**7. Cost Optimization Insights:**
* Identified NAT Gateway as highest cost component (~$32/month)
* Researched VPC Endpoints as alternative to reduce NAT Gateway usage
* Planned implementation of S3, CloudWatch, and SSM VPC Endpoints for Week 10
* Estimated potential savings of $20-25/month with VPC Endpoints

### Week 9 Results & Outcomes:

**Deliverables Completed:**
* ✅ Complete AWS infrastructure deployed via CloudFormation
* ✅ Spring Boot backend application running on EC2
* ✅ RDS MySQL database configured and connected
* ✅ Application Load Balancer routing traffic to backend
* ✅ API Gateway exposing secure REST API
* ✅ Systemd service for automatic application management
* ✅ CloudWatch logging and monitoring configured
* ✅ Deployment documentation and troubleshooting guide

**Key Metrics:**
* **Infrastructure Deployment Time**: 18 minutes
* **Backend Application Startup Time**: 12 seconds
* **Health Check Success Rate**: 100%
* **API Response Time**: <200ms average
* **Database Connection Pool**: 5 active, 10 max connections
* **Monthly Cost Estimate**: $8.90 (excluding NAT Gateway optimization)

**Technical Stack Deployed:**
* **Frontend**: S3 + CloudFront (prepared for Week 10)
* **Backend**: Spring Boot 3.x on EC2 t3.nano
* **Database**: RDS MySQL 8.0 db.t3.micro
* **Load Balancer**: Application Load Balancer
* **API Gateway**: REST API with VPC Link
* **Monitoring**: CloudWatch Logs and Metrics
* **IaC**: CloudFormation YAML template

### Lessons Learned:

**1. Infrastructure as Code Benefits:**
* **Lesson**: CloudFormation enables repeatable, version-controlled infrastructure deployment
* **Application**: Single template deployed entire stack in 18 minutes vs hours of manual configuration
* **Takeaway**: IaC is essential for production environments - enables disaster recovery, environment replication, and audit trails

**2. VPC Subnet Design:**
* **Lesson**: Proper public/private subnet isolation is critical for security
* **Application**: Placed RDS in private subnet with no internet access, only accessible via EC2 in public subnet
* **Takeaway**: Never expose databases directly to internet - use bastion hosts or application servers as intermediaries

**3. CloudFormation Dependencies:**
* **Lesson**: Resource creation order matters - must use DependsOn for proper sequencing
* **Application**: NAT Gateway must exist before private subnet route table, RDS must wait for subnet group
* **Takeaway**: Always map resource dependencies in CloudFormation to avoid creation failures

**4. Spring Boot Configuration Management:**
* **Lesson**: Externalize configuration from JAR for environment-specific settings
* **Application**: Used --spring.config.location to load properties from /opt/workshop/application.properties
* **Takeaway**: Never hardcode environment-specific values in application code or JAR files

**5. Systemd Service Management:**
* **Lesson**: Systemd provides robust process management with automatic restart and logging
* **Application**: Configured Restart=always with RestartSec=10 for high availability
* **Takeaway**: Always use process managers (systemd, supervisord) for production applications, never run manually

**6. AWS Systems Manager Session Manager:**
* **Lesson**: Session Manager eliminates need for SSH keys and bastion hosts
* **Application**: Connected to EC2 instances securely without opening port 22 or managing key pairs
* **Takeaway**: Session Manager is more secure than SSH - provides audit logs, no key management, works with private subnets

**7. Health Check Configuration:**
* **Lesson**: Proper health check endpoints are essential for load balancer traffic routing
* **Application**: Used Spring Boot Actuator /actuator/health endpoint for ALB health checks
* **Takeaway**: Always implement health check endpoints that verify database connectivity and critical dependencies

**8. Cost Awareness:**
* **Lesson**: NAT Gateway is expensive (~$32/month) for small workloads
* **Application**: Identified VPC Endpoints as cost-effective alternative for AWS service access
* **Takeaway**: Always review AWS Cost Explorer and identify optimization opportunities - VPC Endpoints can save 60-70% on NAT costs

**9. Troubleshooting Methodology:**
* **Lesson**: Systematic troubleshooting saves time - check logs, verify connectivity, test endpoints
* **Application**: Used CloudWatch Logs, systemd journalctl, and curl commands to diagnose issues
* **Takeaway**: Establish troubleshooting runbooks and use structured debugging approaches

**10. Documentation Importance:**
* **Lesson**: Clear deployment documentation accelerates future deployments and team onboarding
* **Application**: Documented every step with commands, expected outputs, and troubleshooting tips
* **Takeaway**: Time invested in documentation pays dividends during incident response and knowledge transfer
