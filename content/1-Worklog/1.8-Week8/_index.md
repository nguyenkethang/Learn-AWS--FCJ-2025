---
title: "Week 8 Worklog"
date: 2025-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Complete project proposal for Blood Donation Support System (BDSS)
* Design comprehensive AWS Cloud architecture
* Define technical requirements and implementation roadmap
* Establish budget estimation and risk assessment

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Analyze current blood donation management problems <br> - Research existing solutions and identify gaps <br> - Define project scope and objectives                                                    | 2025/10/27 | 2025/10/27      | WHO Blood Safety Guidelines <br> <https://www.who.int/health-topics/blood-safety> <br> PubMed Healthcare IT Research <br> <https://pubmed.ncbi.nlm.nih.gov/>               |
| 2   | - Design AWS 3-tier architecture <br>&emsp; + Frontend & Content Delivery Layer <br>&emsp; + Application & Compute Layer <br>&emsp; + Monitoring & Security Layer                                      | 2025/10/28 | 2025/10/28      | AWS Well-Architected Framework <br> <https://aws.amazon.com/architecture/well-architected/> <br> AWS Architecture Center <br> <https://aws.amazon.com/architecture/>           |
| 3   | - Define technical stack: <br>&emsp; + Frontend: React/Next.js <br>&emsp; + Backend: Node.js/Express <br>&emsp; + Database: Amazon RDS MySQL <br>&emsp; + CI/CD: GitLab + CodePipeline                 | 2025/10/29 | 2025/10/29      | AWS Solutions Library <br> <https://aws.amazon.com/solutions/> <br> React Official Docs <br> <https://react.dev/> <br> Node.js Best Practices <br> <https://nodejs.org/en/docs/>                         |
| 4   | - Map AWS services to requirements: <br>&emsp; + Route 53, CloudFront, S3 <br>&emsp; + API Gateway, EC2, RDS <br>&emsp; + Cognito, IAM, Secrets Manager <br>&emsp; + CloudWatch, SNS, CloudTrail       | 2025/10/30 | 2025/10/30      | AWS Documentation <br> <https://docs.aws.amazon.com/> <br> AWS Security Best Practices <br> <https://aws.amazon.com/security/best-practices/> <br> HIPAA Compliance on AWS <br> <https://aws.amazon.com/compliance/hipaa-compliance/>                 |
| 5   | - Create implementation timeline (5 months) <br> - Estimate AWS service costs <br> - Conduct risk assessment and mitigation planning                                                                    | 2025/10/31 | 2025/11/02      | AWS Pricing Calculator <br> <https://calculator.aws/> <br> AWS Cost Management <br> <https://aws.amazon.com/aws-cost-management/> <br> PMBOK Guide (Project Management) <br> <https://www.pmi.org/pmbok-guide-standards>                    |

### Week 8 Achievements:

**1. Problem Analysis & Solution Design:**
* Identified key challenges in current blood donation management:
  * Manual processes and disparate tools
  * Difficulty finding suitable donors by blood type/location
  * Lack of synchronized data storage
  * Limited emergency response capability

* Proposed comprehensive AWS Cloud-based solution with:
  * 60-70% reduction in donor search time
  * Improved data accuracy and synchronization
  * Optimized costs with pay-as-you-go pricing
  * Enhanced emergency response capability

**2. AWS Architecture Design:**
* Designed 3-tier architecture with clear separation of concerns:
  * **Frontend Layer**: Route 53 → CloudFront → S3 for static content delivery
  * **Application Layer**: API Gateway → EC2 (public subnet) → RDS (private subnet)
  * **Security Layer**: VPC with Internet Gateway, NAT Gateway, and proper subnet isolation

* Integrated comprehensive AWS services:
  * **Compute**: EC2 instances for backend API
  * **Database**: RDS MySQL for relational data storage
  * **Authentication**: Cognito for 4-tier user roles (Guest, Member, Staff, Admin)
  * **CI/CD**: GitLab → CodePipeline → CodeBuild → EC2 automated deployment
  * **Monitoring**: CloudWatch, CloudTrail, Athena for logs and metrics
  * **Notifications**: SNS for emergency alerts and donor matching

**3. Technical Requirements Definition:**
* Established technology stack:
  * Frontend: React/Next.js or Angular
  * Backend: Node.js/Express REST API
  * Database: Amazon RDS MySQL with backup strategy
  * Authentication: Amazon Cognito with role-based access
  * CI/CD: Automated pipeline with GitLab integration

**4. Implementation Roadmap:**
* Created 5-month phased approach:
  * Month 1: Requirements analysis & design
  * Month 2: Infrastructure & pipeline setup
  * Months 3-4: Development & testing
  * Month 5: Production deployment & operations

**5. Budget & Risk Management:**
* Estimated monthly AWS costs: **$8.90/month** (~$106.8/year)
  * EC2, RDS, API Gateway, CloudFront, S3, Route 53
  * Cognito, CloudWatch, CI/CD services
  * Optimized with AWS Free Tier eligibility

* Identified and planned mitigation for key risks:
  * Internet connectivity issues
  * DDoS attacks (AWS WAF + CloudFront)
  * Data security (RDS backup + IAM controls)
  * Budget overruns (AWS budget alerts)
  * CI/CD disruptions (pipeline testing)

**6. Documentation:**
* Completed comprehensive project proposal including:
  * Executive summary
  * Problem statement and solution approach
  * Detailed AWS architecture diagram
  * Technical implementation plan
  * Timeline, budget, and risk assessment
  * Expected outcomes and expansion possibilities

### Week 8 Results & Outcomes:

**Deliverables Completed:**
* ✅ Comprehensive project proposal document (BDSS)
* ✅ AWS 3-tier architecture diagram with complete service mapping
* ✅ Technical specification document with technology stack
* ✅ 5-month implementation timeline with clear milestones
* ✅ Detailed budget estimation ($8.90/month)
* ✅ Risk assessment matrix with mitigation strategies

**Key Metrics:**
* **Services Mapped**: 15+ AWS services integrated into architecture
* **Cost Optimization**: Achieved ~$107/year budget (AWS Free Tier eligible)
* **Expected Impact**: 60-70% reduction in donor search time
* **User Roles Defined**: 4 tiers (Guest, Member, Staff, Admin)
* **Implementation Duration**: 5 months from design to production

### Lessons Learned:

**1. Architecture Design:**
* **Lesson**: Proper VPC subnet isolation (public/private) is critical for healthcare data security
* **Application**: Placed RDS in private subnet with no direct internet access, only accessible via EC2 in public subnet
* **Takeaway**: Security-first design prevents data breaches and ensures HIPAA compliance considerations

**2. Service Selection:**
* **Lesson**: Not all AWS services are necessary - focus on core requirements
* **Application**: Selected only essential services (EC2, RDS, API Gateway, Cognito) before adding monitoring/alerting
* **Takeaway**: Start minimal, scale incrementally to control costs and complexity

**3. Cost Management:**
* **Lesson**: AWS Free Tier can significantly reduce initial costs for student/startup projects
* **Application**: Chose t2.micro EC2 and small RDS instances eligible for free tier
* **Takeaway**: Always use AWS Pricing Calculator before finalizing architecture decisions

**4. CI/CD Planning:**
* **Lesson**: Automated deployment pipeline saves time and reduces human error
* **Application**: Integrated GitLab → CodePipeline → CodeBuild from the start
* **Takeaway**: DevOps practices should be planned in design phase, not added later

**5. Healthcare Domain Considerations:**
* **Lesson**: Healthcare systems require special attention to data privacy, security, and compliance
* **Application**: Implemented Cognito for authentication, IAM for access control, Secrets Manager for credentials, CloudTrail for audit logs
* **Takeaway**: Regulatory compliance (HIPAA-like standards) must be addressed in architecture, not as afterthought

**6. Scalability Planning:**
* **Lesson**: Cloud architecture should support future growth without major redesign
* **Application**: Used managed services (RDS, Cognito, CloudFront) that auto-scale
* **Takeaway**: Serverless and managed services reduce operational overhead and enable easy scaling

**7. Documentation Importance:**
* **Lesson**: Clear documentation accelerates team alignment and stakeholder buy-in
* **Application**: Created detailed proposal with diagrams, timelines, and budget breakdowns
* **Takeaway**: Time invested in documentation pays off during implementation and maintenance phases
