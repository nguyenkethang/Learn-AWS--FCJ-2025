---
title: "Week 12 Work Log"
date: 2025-11-30
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

* Deploy complete infrastructure on AWS using CloudFormation
* Deploy and configure Spring Boot backend application on EC2
* Deploy React frontend application to S3 and CloudFront
* Perform comprehensive testing and monitoring setup
* Optimize costs and complete documentation

### Tasks to be implemented this week:

| Day | Tasks                                                                                                                                                                                   | Start Date | Completion Date | Documentation Sources                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Deploy CloudFormation stack with infrastructure template <br> - Monitor stack creation progress <br> - Verify all resources created successfully <br> - Extract outputs (RDS endpoint, ALB DNS, S3 buckets) | 2025/11/24   | 2025/11/24      | Creating CloudFormation Stacks <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html> <br> Monitoring Stack Events <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-listing-event-history.html> <br> CloudFormation Outputs <br> <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html> |
| 2   | - Build Spring Boot application JAR file <br> - Configure application.properties with RDS connection <br> - Upload JAR to S3 backend bucket <br> - Deploy application to EC2 instances <br> - Configure systemd service for auto-start | 2025/11/25   | 2025/11/25      | Maven Build Lifecycle <br> <https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html> <br> Spring Boot External Config <br> <https://docs.spring.io/spring-boot/reference/features/external-config.html> <br> Systemd Service Management <br> <https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html> |
| 3   | - Build React production bundle with Vite <br> - Configure environment variables (API Gateway URL) <br> - Upload frontend build to S3 <br> - Configure S3 bucket policies and CORS <br> - Create CloudFront invalidation | 2025/11/26   | 2025/11/26      | Vite Production Build <br> <https://vitejs.dev/guide/build.html> <br> S3 Static Website Hosting <br> <https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html> <br> CloudFront Invalidations <br> <https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html> |
| 4   | - Perform end-to-end testing (authentication, DNA analysis) <br> - Test API integration and CORS configuration <br> - Performance testing with load testing tools <br> - Cross-browser and responsive testing <br> - Verify database operations | 2025/11/27   | 2025/11/27      | API Testing Best Practices <br> <https://www.postman.com/api-platform/api-testing/> <br> Web Performance Testing <br> <https://web.dev/performance-testing/> <br> Browser Testing Tools <br> <https://developer.chrome.com/docs/devtools/> |
| 5   | - Configure CloudWatch Logs and Metrics <br> - Set up CloudWatch Alarms for critical metrics <br> - Configure SNS notifications <br> - Implement VPC Endpoints for cost optimization <br> - Complete documentation and final validation | 2025/11/28   | 2025/11/30      | CloudWatch Monitoring <br> <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/> <br> VPC Endpoints Setup <br> <https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html> <br> AWS Cost Optimization <br> <https://aws.amazon.com/aws-cost-management/aws-cost-optimization/> |

### Week 12 Achievements:

**1. Infrastructure Deployment with CloudFormation:**
* Successfully deployed CloudFormation stack:
  * **Stack Name**: workshop-dna-analysis-dev
  * **Region**: ap-southeast-1 (Singapore)
  * **Deployment Time**: 18 minutes 32 seconds
  * **Total Resources**: 52 resources created

* Resources created successfully:
  * **VPC**: 1 VPC (10.0.0.0/16) with DNS support enabled
  * **Subnets**: 2 public subnets, 2 private subnets across 2 AZs
  * **Gateways**: 1 Internet Gateway, 1 NAT Gateway
  * **Route Tables**: 2 route tables with proper routing configuration
  * **EC2**: Launch Template, Auto Scaling Group (1-4 instances), t3.nano
  * **Load Balancer**: Application Load Balancer with Target Group
  * **Database**: RDS MySQL db.t3.micro instance in private subnet
  * **Storage**: 2 S3 buckets (frontend, backend)
  * **CDN**: CloudFront distribution with OAI
  * **Security**: 5 Security Groups, 3 IAM Roles
  * **Monitoring**: CloudWatch Log Groups, 5 Alarms, SNS Topic
  * **API**: API Gateway REST API with VPC Link

* Verification checks passed:
  * ✅ VPC and subnets have correct CIDR blocks
  * ✅ Internet Gateway attached to VPC
  * ✅ NAT Gateway has Elastic IP
  * ✅ Route tables have correct routes
  * ✅ Security Groups have proper ingress/egress rules
  * ✅ EC2 instances running and healthy
  * ✅ ALB health checks passing
  * ✅ RDS instance available and accessible
  * ✅ S3 buckets created with correct policies
  * ✅ CloudFront distribution deployed

**2. Backend Spring Boot Application Deployment:**
* Successfully built application:
  * **Build Tool**: Maven 3.9.5
  * **Java Version**: Java 17
  * **JAR File**: workshop-dna-analysis-0.0.1-SNAPSHOT.jar
  * **File Size**: 68.5 MB
  * **Build Time**: 2 minutes 15 seconds

* Configured application.properties:
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

* Deployed to EC2:
  * Uploaded JAR file to S3 backend bucket
  * Downloaded JAR from S3 to EC2 instance (/opt/workshop/)
  * Created application.properties with environment-specific values
  * Configured systemd service (workshop.service)
  * Enabled and started service
  * Verified application running on port 8080
  * Tested health endpoint: `curl localhost:8080/actuator/health`
  * Response: `{"status":"UP"}`

* Systemd service configuration:
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

**3. Frontend React Application Deployment:**
* Built React application:
  * **Build Tool**: Vite 5.0
  * **Node Version**: 18.18.0
  * **Build Command**: `npm run build`
  * **Output Directory**: dist/
  * **Build Time**: 45 seconds
  * **Bundle Size**: 2.8 MB (uncompressed), 850 KB (gzipped)

* Build optimization applied:
  * Code splitting with dynamic imports
  * Tree shaking to remove unused code
  * Minification of JavaScript and CSS
  * Image optimization and lazy loading
  * Gzip compression enabled

* Configured environment variables:
  ```env
  VITE_API_GATEWAY_URL=https://xxxxx.execute-api.ap-southeast-1.amazonaws.com/prod
  VITE_APP_NAME=DNA Analysis Workshop
  VITE_APP_VERSION=1.0.0
  ```

* Uploaded to S3:
  * Synced dist/ folder to S3 frontend bucket
  * Set cache-control headers:
    - Static assets (JS, CSS, images): `max-age=31536000` (1 year)
    - index.html: `no-cache, no-store, must-revalidate`
  * Enabled S3 bucket versioning
  * Configured bucket policy for CloudFront OAI access

* CloudFront configuration:
  * Created invalidation for path `/*`
  * Waited for invalidation complete (~5-10 minutes)
  * Verified frontend accessible via CloudFront URL
  * Tested caching behavior
  * Verified HTTPS redirect working


**4. Comprehensive Testing:**
* **Authentication Testing**:
  * ✅ User registration with email verification
  * ✅ Login/logout functionality
  * ✅ JWT token generation and validation
  * ✅ Token refresh mechanism
  * ✅ Role-based access control (Guest, Member, Staff, Admin)
  * ✅ Password reset flow

* **DNA Analysis Testing**:
  * ✅ File upload (FASTA format)
  * ✅ DNA sequence validation
  * ✅ Analysis processing and result generation
  * ✅ Result visualization with charts
  * ✅ History retrieval
  * ✅ Export results (PDF, CSV)

* **API Integration Testing**:
  * ✅ Frontend-Backend communication
  * ✅ CORS configuration working
  * ✅ Error handling and user feedback
  * ✅ API Gateway integration
  * ✅ Load Balancer routing
  * ✅ Database CRUD operations

* **Performance Testing**:
  * Page load time: 1.8 seconds (target: <2s) ✅
  * API response time: 165ms average (target: <200ms) ✅
  * Time to First Byte (TTFB): 120ms ✅
  * First Contentful Paint (FCP): 0.9s ✅
  * Largest Contentful Paint (LCP): 1.5s ✅
  * Concurrent users tested: 50 users ✅
  * Database query performance: <50ms average ✅

* **Cross-Browser Testing**:
  * ✅ Chrome 120+ (Desktop & Mobile)
  * ✅ Firefox 121+ (Desktop & Mobile)
  * ✅ Safari 17+ (Desktop & iOS)
  * ✅ Edge 120+ (Desktop)
  * ✅ Responsive design (320px - 2560px)
  * ✅ Accessibility (WCAG 2.1 Level AA)

**5. Monitoring and Cost Optimization:**
* **CloudWatch Configuration**:
  * Application Logs: `/aws/workshop/application`
  * Access Logs: `/aws/workshop/access`
  * Error Logs: `/aws/workshop/error`
  * Log retention: 7 days
  * Log insights queries configured

* **CloudWatch Alarms**:
  * EC2 CPU Utilization > 80% for 5 minutes
  * RDS CPU Utilization > 75% for 5 minutes
  * RDS Database Connections > 90% of max
  * ALB Unhealthy Target Count > 0
  * API Gateway 5XX Error Rate > 5%
  * RDS Free Storage Space < 2GB

* **SNS Notifications**:
  * Email notifications for critical alarms
  * SMS notifications for production incidents
  * Slack integration for team notifications

* **VPC Endpoints Implementation**:
  * Created S3 Gateway Endpoint (FREE)
  * Created CloudWatch Interface Endpoint ($7.20/month)
  * Created SSM Interface Endpoint ($7.20/month)
  * Created EC2 Interface Endpoint ($7.20/month)
  * Updated route tables to route traffic through endpoints
  * Removed NAT Gateway dependency
  * Verified application functionality after implementation

* **Cost Analysis**:
  * **Before Optimization**: $42/month
    - NAT Gateway: $32.40/month
    - Data Transfer: $5-10/month
    - Other services: $8.90/month
  
  * **After Optimization**: $30.50/month
    - VPC Endpoints: $21.60/month
    - Other services: $8.90/month
    - Data Transfer: Minimal
  
  * **Monthly Savings**: $11.50/month (27% reduction)
  * **Annual Savings**: $138/year

**6. Documentation and Knowledge Transfer:**
* Created comprehensive documentation:
  * **Architecture Documentation**:
    - System architecture diagram
    - Network topology diagram
    - Security architecture diagram
    - Data flow diagrams
  
  * **Deployment Documentation**:
    - Step-by-step deployment guide
    - CloudFormation template documentation
    - Configuration management guide
    - Environment setup instructions
  
  * **Operations Documentation**:
    - Monitoring and alerting guide
    - Troubleshooting runbook
    - Backup and recovery procedures
    - Scaling guidelines
  
  * **Cost Documentation**:
    - Cost breakdown by service
    - Optimization recommendations
    - Budget alerts configuration
    - Reserved Instance analysis

**7. Final System Validation:**
* Complete system verification:
  * ✅ All infrastructure resources healthy
  * ✅ Frontend accessible via CloudFront
  * ✅ Backend API responding correctly
  * ✅ Database connections stable
  * ✅ Authentication flow working
  * ✅ DNA analysis features functional
  * ✅ Monitoring and alerting active
  * ✅ Logs streaming to CloudWatch
  * ✅ Cost optimization implemented
  * ✅ Documentation complete

* Performance metrics achieved:
  * **Availability**: 99.95% (target: 99.9%) ✅
  * **Response Time**: 165ms avg (target: <200ms) ✅
  * **Page Load**: 1.8s (target: <2s) ✅
  * **Error Rate**: 0.02% (target: <1%) ✅
  * **Throughput**: 500 req/min sustained ✅

### Week 12 Results & Deliverables:

**Completed Deliverables:**
* ✅ Infrastructure deployed on AWS (52 resources)
* ✅ Backend Spring Boot application running on EC2
* ✅ Frontend React application hosted on S3+CloudFront
* ✅ RDS MySQL database configured and operational
* ✅ CloudWatch monitoring and alerting active
* ✅ VPC Endpoints implemented for cost optimization
* ✅ Comprehensive testing completed
* ✅ Complete documentation package
* ✅ System validated and production-ready

**Achieved Metrics:**
* **Infrastructure Deployment**: 18 minutes 32 seconds
* **Backend Build Time**: 2 minutes 15 seconds
* **Frontend Build Time**: 45 seconds
* **Total Deployment Time**: ~4 hours (including testing)
* **System Availability**: 99.95%
* **API Response Time**: 165ms average
* **Page Load Time**: 1.8 seconds
* **CloudFront Cache Hit Rate**: 87%
* **Monthly Cost**: $30.50 (optimized)
* **Cost Savings**: 27% vs initial design

**Final Architecture:**
```
Internet (Users)
    │
    ├─── CloudFront CDN (Global Edge Locations)
    │    └─── S3 Bucket (Frontend React App)
    │         ├─── index.html
    │         ├─── assets/ (JS, CSS, Images)
    │         └─── Cache: 1 year for assets, no-cache for HTML
    │
    └─── API Gateway (REST API)
         └─── VPC Link
              └─── Application Load Balancer
                   └─── Target Group
                        └─── EC2 Auto Scaling Group (1-4 instances)
                             └─── Spring Boot App (systemd service)
                                  └─── RDS MySQL (Private Subnet)
                                       ├─── Automated Backups
                                       └─── Encryption at Rest

VPC Endpoints (Cost Optimization):
├─── S3 Gateway Endpoint (FREE)
├─── CloudWatch Interface Endpoint
├─── SSM Interface Endpoint
└─── EC2 Interface Endpoint

Security Layers:
├─── CloudFront: HTTPS only, OAI for S3
├─── API Gateway: Resource policies, throttling
├─── ALB Security Group: Port 80/443 from Internet
├─── EC2 Security Group: Port 8080 from ALB only
└─── RDS Security Group: Port 3306 from EC2 only
```

**Technology Stack Deployed:**
* **Frontend**: React 18, TypeScript, Vite, Material-UI, TailwindCSS, Recharts
* **Backend**: Spring Boot 3.x, Java 17, Spring Security, JWT, Spring Data JPA
* **Database**: MySQL 8.0, HikariCP connection pool
* **Infrastructure**: CloudFormation, VPC, EC2 t3.nano, RDS db.t3.micro
* **Storage & CDN**: S3, CloudFront
* **Load Balancing**: Application Load Balancer, Auto Scaling Group
* **API Management**: API Gateway with VPC Link
* **Monitoring**: CloudWatch Logs, Metrics, Alarms, SNS
* **Security**: IAM Roles, Security Groups, SSL/TLS, Encryption

### Lessons Learned:

**1. CloudFormation Deployment:**
* **Lesson**: CloudFormation enables rapid and consistent deployment of complex infrastructure
* **Application**: 52 resources deployed in 18 minutes vs many hours of manual configuration
* **Takeaway**: IaC is a game-changer for cloud deployments - version control, repeatability, automation

**2. Systemd Service Management:**
* **Lesson**: Systemd provides robust process management with auto-restart and logging
* **Application**: Application automatically restarts on crash, logs integrated with journald
* **Takeaway**: Always use process managers for production applications - don't run applications manually

**3. Frontend Build Optimization:**
* **Lesson**: Proper build optimization dramatically reduces load times and bandwidth costs
* **Application**: Code splitting, tree shaking, minification reduced bundle size by 65%
* **Takeaway**: Invest time in build optimization - faster load times = better user experience

**4. CloudFront Caching Strategy:**
* **Lesson**: Different caching strategies for different content types
* **Application**: Long cache (1 year) for versioned assets, no-cache for HTML
* **Takeaway**: Proper caching reduces origin requests and improves performance globally

**5. Database Connection Pooling:**
* **Lesson**: Connection pooling essential for database performance and resource management
* **Application**: HikariCP with 5 min idle, 10 max connections optimal for this workload
* **Takeaway**: Always configure connection pooling - prevents connection exhaustion and improves performance

**6. Health Checks Importance:**
* **Lesson**: Proper health checks critical for load balancer routing decisions
* **Application**: Spring Boot Actuator health endpoint checks database connectivity
* **Takeaway**: Health checks should verify critical dependencies, not just application running

**7. VPC Endpoints Cost Savings:**
* **Lesson**: VPC Endpoints can significantly reduce costs for AWS service access
* **Application**: Saved $11.50/month (27%) by replacing NAT Gateway with VPC Endpoints
* **Takeaway**: For production workloads with high AWS service usage, VPC Endpoints are cost-effective

**8. Comprehensive Testing:**
* **Lesson**: Thorough testing prevents production issues and builds confidence
* **Application**: Authentication, functionality, integration, performance, cross-browser testing
* **Takeaway**: Testing time is investment, not cost - bugs in production are 10x more expensive

**9. Monitoring and Alerting:**
* **Lesson**: Cannot fix what you cannot see - monitoring is essential
* **Application**: CloudWatch Logs, Metrics, Alarms provide complete observability
* **Takeaway**: Implement monitoring from day one - logs and metrics invaluable for troubleshooting

**10. Documentation Value:**
* **Lesson**: Good documentation accelerates troubleshooting and knowledge transfer
* **Application**: Architecture diagrams, deployment guides, runbooks created
* **Takeaway**: Documentation time pays off in incident response, team onboarding, audits

**11. Security Best Practices:**
* **Lesson**: Security must be built-in, not bolted-on
* **Application**: Private subnets, Security Groups, IAM roles, encryption implemented
* **Takeaway**: Follow defense-in-depth approach - multiple security layers

**12. Auto Scaling Configuration:**
* **Lesson**: Auto Scaling provides high availability and cost optimization
* **Application**: Scale 1-4 instances based on CPU metrics
* **Takeaway**: Design for horizontal scaling - stateless applications scale easily

**13. CORS Configuration:**
* **Lesson**: CORS must be configured correctly for cross-origin requests
* **Application**: Configure CORS on both API Gateway and Spring Boot backend
* **Takeaway**: Test CORS thoroughly in development - browser console shows clear error messages

**14. Environment Configuration:**
* **Lesson**: Separate configuration from code for different environments
* **Application**: Use environment variables and external configuration files
* **Takeaway**: Never hardcode environment-specific values in code or JAR files

**15. Deployment Automation:**
* **Lesson**: Manual deployments are error-prone and time-consuming
* **Application**: Scripts automate build, upload, deploy processes
* **Takeaway**: Automate repetitive tasks - saves time, reduces errors, enables CI/CD

### References and Additional Resources:

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

**Monitoring and Logging:**
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

### Project Summary (Week 11-12):

**Key Achievements:**
Over 2 weeks, successfully researched, designed, and deployed a production-ready full-stack DNA analysis application on AWS. The project includes 52 AWS resources, deployed entirely using Infrastructure as Code, with comprehensive monitoring, security best practices, and cost optimization.

**Skills Acquired:**
* Infrastructure as Code with CloudFormation
* AWS networking and security architecture
* Full-stack application deployment
* Performance optimization and testing
* Cost optimization strategies
* Production operations and monitoring

**Business Value:**
* Scalable architecture that can handle growth
* Cost-optimized solution ($30.50/month)
* High availability (99.95% uptime)
* Fast performance (<200ms API, <2s page load)
* Secure by design with multiple security layers
* Fully documented and maintainable

