---
title: "Event 4"
date: 2025-11-17
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# ⚙️ DevOps on AWS Workshop

### 🎯 Workshop Goals

- Understand DevOps principles and culture in the context of AWS
- Gain hands-on experience with CI/CD pipelines and Infrastructure as Code
- Explore containerization and orchestration using AWS services
- Learn monitoring and observability best practices
- Discover real-world DevOps strategies and career pathways

### 📍 Event Details

- **Location**: 26th Floor, Bitexco Financial Tower, 2 Hai Trieu Street, Ben Nghe Ward, District 1, Ho Chi Minh City
- **Date & Time**: 8:30 AM – 5:00 PM, Monday, November 17, 2025

### 📋 Program Schedule

#### ⏰ 8:30 – 9:00 AM: Welcome & DevOps Mindset
**Speaker: Truong Quang Tinh** – AWS Community Builder

- Recap of AI/ML session
- Introduction to DevOps culture and principles
- Key metrics: DORA, MTTR, deployment frequency

#### ⏰ 9:00 – 10:30 AM: AWS DevOps Services – CI/CD Pipeline
**Speaker: Truong Quang Tinh** – AWS Community Builder

- **Source Control**:
  - AWS CodeCommit
  - Git strategies: GitFlow, Trunk-based development
- **Build & Test**:
  - AWS CodeBuild configuration
  - Testing pipelines
- **Deployment**:
  - AWS CodeDeploy with Blue/Green, Canary, and Rolling updates
- **Orchestration**:
  - AWS CodePipeline automation
- **Live Demo**: Full CI/CD pipeline walkthrough

#### ☕ 10:30 – 10:45 AM: Break

- Refreshments and networking

#### ⏰ 10:45 AM – 12:00 PM: Infrastructure as Code (IaC)
**Speakers:**
- **Van Hoang Kha** – AWS Community Builder – CloudFormation
- **Nguyen Khanh Phuc Thinh** – AWS Community Builder – AWS CDK

- **AWS CloudFormation**:
  - Templates, stacks, drift detection
- **AWS CDK (Cloud Development Kit)**:
  - Constructs, reusable patterns, language support
- **Live Demo**: Deploying with CloudFormation and CDK
- **Discussion**: Choosing between IaC tools

#### 🍽️ 12:00 – 1:00 PM: Lunch Break (Self-arranged)

#### ⏰ 1:00 – 2:30 PM: Container Services on AWS
**Speaker: Le Huynh Nghiem** – AWS Community Builder

- **Docker Fundamentals**:
  - Microservices and containerization
- **Amazon ECR**:
  - Image storage, scanning, lifecycle policies
- **Amazon ECS & EKS**:
  - Deployment strategies, scaling, orchestration
- **AWS App Runner**:
  - Simplified container deployment
- **Demo & Case Study**: Microservices deployment comparison

#### ☕ 2:30 – 2:45 PM: Break

#### ⏰ 2:45 – 4:00 PM: Monitoring & Observability
**Speaker: Huynh Hoang Long** – AWS Community Builder

- **Amazon CloudWatch**:
  - Metrics, logs, alarms, dashboards
- **AWS X-Ray**:
  - Distributed tracing and performance insights
- **Live Demo**: Full-stack observability setup
- **Best Practices**:
  - Alerting, dashboards, on-call processes

#### ⏰ 4:00 – 4:45 PM: DevOps Best Practices & Case Studies
**Speaker: Pham Hoang Quy** – AWS Community Builder

- Deployment strategies: Feature flags, A/B testing
- Automated testing and CI/CD integration
- Incident management and postmortems
- Case studies: Startups and enterprise DevOps transformations

#### ⏰ 4:45 – 5:00 PM: Q&A & Wrap-up

- DevOps career pathways
- AWS certification roadmap

### 🔍 Deep Dive Topics & Visual Learning

#### 📈 DevOps Metrics & Measurement

- **DORA Metrics**:
  - Deployment Frequency
  - Lead Time for Changes
  - Mean Time to Recovery (MTTR)
  - Change Failure Rate

- **Additional Metrics**:
  - Build success/failure rates
  - Test coverage and defect density
  - Release cycle time and rollback frequency
  - System uptime and latency

- **Tools for Measurement**:
  - CloudWatch dashboards and alarms
  - X-Ray traces and service maps
  - CodePipeline execution history
  - Third-party integrations (Datadog, Prometheus, Grafana)

#### 🧠 DevOps Mindset & Culture

- **Collaboration & Shared Ownership**:
  - “You build it, you run it” – promoting accountability
  - Cross-functional teams and blameless postmortems

- **Automation First**:
  - Manual work = technical debt
  - Automate testing, deployment, monitoring, and rollback

- **Continuous Learning**:
  - Fail fast, learn faster
  - Encourage experimentation and innovation

- **Observability & Feedback Loops**:
  - Real-time monitoring
  - Fast feedback from CI/CD pipelines
  - Customer-centric metrics

#### 🛠️ DevOps Toolchain on AWS

| Stage            | AWS Services Used                          | Purpose                                      |
|------------------|--------------------------------------------|----------------------------------------------|
| Source Control   | CodeCommit, GitHub                         | Version control and collaboration            |
| Build & Test     | CodeBuild, CodePipeline                    | Automated builds and test execution          |
| Deployment       | CodeDeploy, App Runner, ECS/EKS            | Flexible deployment strategies               |
| IaC              | CloudFormation, CDK                        | Infrastructure provisioning and management   |
| Monitoring       | CloudWatch, X-Ray                          | Observability and alerting                   |
| Security         | IAM, GuardDuty, Secrets Manager            | Access control and threat detection          |

#### 📚 Recommended Learning Resources

- **Books**:
  - *Accelerate* by Nicole Forsgren, Jez Humble, Gene Kim
  - *The Phoenix Project* by Gene Kim, Kevin Behr, George Spafford
  - *DevOps for the Modern Enterprise* by Mirco Hering

- **Courses & Labs**:
  - AWS Skill Builder: DevOps Engineer Learning Plan
  - AWS Workshops: CI/CD, Containers, Observability
  - Hands-on labs with AWS Cloud9 and CDK

- **Certifications**:
  - AWS Certified DevOps Engineer – Professional
  - AWS Certified Solutions Architect – Associate
  - AWS Certified Developer – Associate

### 🔄 CI/CD Pipeline Insights

#### 🧪 Continuous Integration

- **Definition**: Practice of integrating code frequently, ideally daily, into a shared repository
- **Benefits**:
  - Early detection of integration issues
  - Faster feedback loops
  - Reduced merge conflicts
- **Best Practices**:
  - Everyone commits to mainline daily
  - Automated builds and tests triggered on each commit
  - Use trunk-based development to simplify merging

#### 🚀 Continuous Delivery vs Deployment

| Aspect                  | Continuous Delivery                         | Continuous Deployment                        |
|------------------------|---------------------------------------------|----------------------------------------------|
| Trigger                | Manual approval before production           | Fully automated to production                |
| Testing                | Automated tests before staging              | Automated tests before production            |
| Risk Management        | Human gate for final release                | Requires robust rollback and monitoring      |
| Use Case               | Regulated industries, controlled releases   | High-frequency, low-risk environments        |

- **Key Tools**:
  - GitLab/GitHub Actions
  - AWS CodePipeline
  - Feature flags and canary deployments

#### 🧰 Infrastructure as Code (IaC) Deep Dive

- **CloudFormation**:
  - Declarative templates
  - Stack drift detection
  - Change sets for safe updates

- **AWS CDK**:
  - Imperative code in TypeScript, Python, Java, etc.
  - Reusable constructs and abstraction layers
  - Ideal for developers familiar with programming languages

- **Comparison**:
  - CloudFormation: YAML/JSON, stable and mature
  - CDK: Developer-friendly, faster iteration

#### 🐳 Containerization & Microservices

- **Docker**:
  - Lightweight containers for isolated environments
  - Ideal for microservices architecture

- **Amazon ECR**:
  - Secure container registry
  - Image scanning and lifecycle policies

- **Amazon ECS vs EKS**:
  - ECS: Simpler, AWS-managed orchestration
  - EKS: Kubernetes-native, more flexibility

- **App Runner**:
  - Simplified deployment from source or container
  - Auto-scaling and HTTPS by default

#### 📡 Monitoring & Observability

- **CloudWatch**:
  - Custom metrics, logs, dashboards
  - Alarms for proactive alerting

- **AWS X-Ray**:
  - Distributed tracing
  - Visualize service maps and latency bottlenecks

- **Best Practices**:
  - Set SLOs and SLIs
  - Use anomaly detection
  - Integrate with incident response workflows

#### 📘 DevOps Best Practices

- **Feature Flags**:
  - Enable/disable features without redeploying
  - Support A/B testing and gradual rollouts

- **Automated Testing**:
  - Unit, integration, regression, smoke tests
  - CI/CD pipeline integration

- **Incident Management**:
  - Blameless postmortems
  - Root cause analysis
  - Runbooks and escalation paths

- **Case Studies**:
  - Startups: Speed and agility with minimal overhead
  - Enterprises: Governance, compliance, and scale

#### 🎓 Career & Certification Pathways

- **DevOps Roles**:
  - DevOps Engineer
  - Platform Engineer
  - Site Reliability Engineer (SRE)
  - Cloud Engineer

- **Certifications**:
  - AWS Certified DevOps Engineer – Professional
  - AWS Certified Solutions Architect – Associate
  - AWS Certified Developer – Associate

- **Learning Resources**:
  - AWS Skill Builder
  - Free-tier labs with SageMaker and CodePipeline
  - Community meetups and webinars

### 🧪 Continuous Testing Strategy

- **Testing is not a phase**: It must be integrated across all stages of the pipeline
- **Shift-left testing**: Begin testing early in the development cycle
- **Test types across pipeline**:
  - Lint checks and static analysis at commit
  - Unit and integration tests during build
  - Regression and exploratory tests before release
  - Smoke, performance, and security tests in staging and production

- **Microservices Testing**:
  - Validate service independence and interoperability
  - API contract testing and dependency resilience
  - Aggregate performance across distributed systems

- **Containerized Testing**:
  - Use Docker containers for isolated test environments
  - Separate test tools and artifacts into dedicated containers
  - Launch short-lived sandboxes for CI validation

### 🏗️ CI/CD Pipeline Optimization

- **Automated Build Prerequisites**:
  - CLI-based multistage scripts
  - Repeatable, reliable, and rollback-capable automation
  - Visibility into metrics and build health

- **Reasons to Fail a Build**:
  - Compilation errors
  - Code style violations and excessive warnings
  - Unit and functional test failures
  - Architectural breaches and slow tests

- **Build Health Monitoring**:
  - Track success/failure rates and build durations
  - Visual dashboards for trend analysis
  - Triage processes for failed builds

- **Scaling CI Infrastructure**:
  - Vertical scaling: more powerful build nodes
  - Horizontal scaling: parallel jobs across multiple agents
  - Predictive orchestration for resource pre-allocation

### 🔀 Branching & Merging Best Practices

- **Trunk-Based Development**:
  - One mainline branch with continuous integration
  - Avoid long-lived feature branches
  - Use feature toggles for in-code branching

- **Merge Strategies**:
  - Pull from mainline before pushing changes
  - Daily commits to reduce integration complexity
  - Eliminate “merge hell” with frequent syncs

- **Version Control Hygiene**:
  - Code reviews and peer approvals
  - Automated checks on pull requests
  - Visibility into team changes and application status

### 🧩 Building Your DevOps Toolchain

| Category   | Purpose                                      | Example Tools                      |
|------------|----------------------------------------------|------------------------------------|
| Code       | Development, review, versioning              | Git, GitHub, CodeCommit            |
| Build      | CI tools and build status                    | Jenkins, CodeBuild, GitLab CI      |
| Test       | Performance and quality validation           | JUnit, Selenium, Postman           |
| Package    | Artifact storage and pre-deployment          | ECR, Maven, NPM, Artifactory       |
| Release    | Deployment automation                        | CodeDeploy, Spinnaker, Harness     |
| Validate   | Change management and approvals              | Jira, ServiceNow, AWS Change Manager|

### 🔐 Security in DevOps Pipelines

#### 🛡️ Integrating Security into CI/CD

- **Code-level Security**:
  - Static code analysis for vulnerabilities
  - Secrets detection and credential scanning
  - Dependency scanning for known CVEs

- **Build-time Security**:
  - Container image scanning (Amazon ECR, Snyk, Sysdig)
  - Validation steps using CodeBuild
  - Policy enforcement with AWS IAM and SCPs

- **Deployment-time Security**:
  - Guardrails for deployment environments
  - Role-based access control for CodeDeploy and ECS
  - Secure artifact storage and access policies

- **Runtime Security**:
  - Monitoring with CloudWatch and GuardDuty
  - Runtime protection with AWS Inspector and Trend Micro
  - Logging and alerting for anomalous behavior

#### 🔄 Incremental Pipeline Design

- **Validation-first approach**:
  - Add CodeBuild validation before deployment
  - Use automated tests to gate progress
  - Fail fast to reduce downstream risk

- **Security as a stage**:
  - Insert security checks post-build, pre-deploy
  - Integrate with partner tools (e.g., Snyk, Trend Micro)
  - Ensure compliance before production release

- **Partner Ecosystem Integration**:
  - GitLab, CircleCI, CloudBees for CI orchestration
  - Harness and JFrog for release automation
  - Snyk and Sysdig for security scanning

### 🧱 Building a Self-Service DevOps Platform

- **Developer Enablement**:
  - Use AWS Service Catalog for curated templates
  - Provide CloudFormation stacks for infrastructure provisioning
  - Empower teams with reusable IaC modules

- **Platform Architecture**:
  - CodePipeline + CodeBuild for CI/CD orchestration
  - ECR for container image management
  - ECS/Fargate for scalable container deployment

- **Governance & Scalability**:
  - Centralized templates with parameterization
  - Role-based access and audit logging
  - Continuous improvement via feedback loops

### 📄 Sample Buildspec for CodeBuild

```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 14
    commands:
      - echo Logging in to Amazon ECR...
      - aws ecr get-login-password --region $AWS_DEFAULT_REGION |
        docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com
  pre_build:
    commands:
      - echo Build started on `date`
      - npm install && npm run build
      - cp -r dist/* ./flaskapp
  build:
    commands:
      - docker build -t $IMAGE_REPO_NAME:$IMAGE_TAG_LATEST .
      - docker tag $IMAGE_REPO_NAME:$IMAGE_TAG_LATEST $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG_LATEST
  post_build:
    commands:
      - echo Build completed on `date`
```

### 📊 Monitoring with CloudWatch

#### 🔍 CloudWatch Metrics

- **Definition**: Metrics are data points that reflect system performance
- **Sources**:
  - Default AWS service metrics (EC2, RDS, Lambda, etc.)
  - Custom metrics via CloudWatch Agent
  - On-premises systems through hybrid integration
- **Integration**:
  - EventBridge for event-driven automation
  - Auto Scaling based on metric thresholds
  - DevOps workflows for alerting and remediation

#### 📁 CloudWatch Logs

- **Log Sources**:
  - AWS services (Lambda, ECS, API Gateway, etc.)
  - Application logs via CloudWatch Agent
- **Capabilities**:
  - Centralized log collection and storage
  - Query logs using CloudWatch Logs Insights
  - Visualize trends and anomalies

#### 📈 CloudWatch Dashboards

- **Features**:
  - Combine metrics, logs, and alarms into visual interfaces
  - Customizable widgets for tailored views
  - Shareable dashboards for team visibility
- **Use Cases**:
  - Real-time system health monitoring
  - Executive summaries and SLA tracking
  - Alert correlation and incident analysis

### 🔦 Distributed Tracing with AWS X-Ray

#### 🧭 X-Ray Overview

- **Purpose**: Analyze and debug distributed applications
- **Key Features**:
  - End-to-end request tracing across microservices
  - Service maps to visualize request paths
  - Performance bottleneck identification
  - Integration with CloudWatch for unified observability

#### 🧪 X-Ray Implementation

- **SDK Integration**:
  - Add X-Ray SDK to application code
  - Automatically generate trace IDs
- **OpenTelemetry Support**:
  - Use AWS Distro for OpenTelemetry (ADOT)
  - Export telemetry data to X-Ray via OTLP gRPC
- **Container Compatibility**:
  - Works with ECS, EKS, and Fargate
  - Sidecar or agent-based tracing

#### 📊 X-Ray Insights

- **Trace Analytics**:
  - Latency breakdown by service
  - Error rates and fault isolation
  - Root cause analysis for slow transactions
- **Service Maps**:
  - Visualize dependencies and traffic flow
  - Identify hotspots and underperforming services

### 🧩 Summary & Next Steps

#### ✅ What You’ve Learned

- Gained a clear understanding of the DevOps mindset and collaborative culture in modern software development
- Mastered the CI/CD process using AWS services like CodeCommit, CodeBuild, CodeDeploy, and CodePipeline
- Applied Infrastructure as Code (IaC) with CloudFormation and CDK to automate infrastructure provisioning
- Deployed containerized applications using ECS, EKS, and App Runner
- Set up monitoring and observability with CloudWatch and X-Ray
- Integrated security into DevOps pipelines and leveraged AWS partner tools for enhanced protection
- Built a self-service DevOps platform for development teams

#### 🚀 Your Journey Ahead

- **Practice**: Start with a small project and build a simple CI/CD pipeline on AWS
- **Optimize**: Integrate monitoring, security, and continuous testing into your DevOps workflow
- **Scale**: Build a shared DevOps platform for multiple development teams
- **Connect**: Join the AWS Vietnam Community to learn and share experiences
- **Certify**: Plan to pursue AWS certifications such as DevOps Engineer Professional or Solutions Architect Associate

#### 🎯 Final Message

DevOps is not just about tools or processes—it’s a mindset of innovation, collaboration, automation, and continuous improvement. With the AWS ecosystem, you can build robust, scalable, and secure systems for organizations of any size.

#### 📸 Event Photos

![DevOps Workshop opening session](images/image1.jpg)
<hr>

![CI/CD Pipeline demonstration](images/image2.jpg)
<hr>

![Infrastructure as Code hands-on](images/image3.jpg)
<hr>

![Container services workshop](images/image4.jpg)
<hr>

![Monitoring and observability session](images/image5.jpg)

> Start small, learn from real-world experience, and keep improving. DevOps is a journey, not a destination.


