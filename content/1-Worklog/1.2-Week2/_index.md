---
title: "Week 2 Worklog"
date: 2025-09-21
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---


### Week 2 Objectives:

* Understand AWS VPC fundamentals and security features.
* Practice creating VPC, Subnets, Route Tables, and Internet Gateway.
* Learn VPN Site-to-Site, Security Groups, and Network ACLs.
* Practice VPC Peering and Transit Gateway configurations.


### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                                           | Start Date | Completion Date | Reference Material     |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ---------------------- |
| 1   | - Study Module 02-01: AWS Virtual Private Cloud <br> - Study Module 02-02: VPC Security and Multi-VPC features <br> - Study Module 02-03: VPN - DirectConnect - LoadBalancer - ExtraResources                                 |  2025/09/15 |  2025/09/15      | Lab 03, Lab 10, Lab 19, Lab 20 |
| 2   | - **Lab 03 - Part 1:** Start with Amazon VPC and AWS VPN Site-to-Site <br>&emsp; + Module 02-Lab03-01: Introduction <br>&emsp; + Module 02-Lab03-01.1: Create Subnets <br>&emsp; + Module 02-Lab03-01.2: Configure Route Tables <br>&emsp; + Module 02-Lab03-01.3: Set up Internet Gateway (IGW) <br>&emsp; + Module 02-Lab03-01.4: Create NAT Gateway |  2025/09/16 |  2025/09/16      | https://000003.awsstudygroup.com/ |
| 3   | - **Lab 03 - Part 2:** VPC Security and Resource Creation <br>&emsp; + Module 02-Lab03-02.1: Configure Security Groups <br>&emsp; + Module 02-Lab03-02.2: Set up Network ACLs <br>&emsp; + Module 02-Lab03-02.3: Review VPC Resource Map <br>&emsp; + Module 02-Lab03-03.1: Create VPC <br>&emsp; + Module 02-Lab03-03.2: Create Subnets |  2025/09/17 |  2025/09/17      | https://000003.awsstudygroup.com/ |
| 4   | - **Lab 03 - Part 3:** Complete VPC Setup and EC2 Deployment <br>&emsp; + Module 02-Lab03-03.3: Create Internet Gateway <br>&emsp; + Module 02-Lab03-03.4: Create Route Table for Internet Routing <br>&emsp; + Module 02-Lab03-03.5: Create Security Groups <br>&emsp; + Module 02-Lab03-04.1: Create EC2 Instances in Subnets <br>&emsp; + Module 02-Lab03-04.2: Test connection <br>&emsp; + Module 02-Lab03-04.3: Create NAT Gateway <br>&emsp; + Module 02-Lab03-04.5: EC2 Instance Connect Endpoint |  2025/09/18 |  2025/09/18      | https://000003.awsstudygroup.com/ |
| 5   | - **Lab 10:** Set up Hybrid DNS with Route 53 Resolver <br>&emsp; + Module 02-Lab10-01: Introduction <br>&emsp; + Module 02-Lab10-02.1: Generate Key Pair <br>&emsp; + Module 02-Lab10-02.2: Initialize CloudFormation Template <br>&emsp; + Module 02-Lab10-02.3: Configure Security Group <br>&emsp; + Module 02-Lab10-03: Connect to RDGW <br>&emsp; + Module 02-Lab10-05: Set up DNS <br>&emsp; + Module 02-Lab10-05.1: Create Route 53 Outbound Endpoint <br>&emsp; + Module 02-Lab10-05.2: Create Route 53 Resolver Rules <br>&emsp; + Module 02-Lab10-05.3: Create Route 53 Inbound Endpoints <br>&emsp; + Module 02-Lab10-05.4: Test results <br>&emsp; + Module 02-Lab10-06: Clean up resources |  2025/09/19 |  2025/09/19      | https://000010.awsstudygroup.com/ |
| 6   | - **Lab 19:** Set up VPC Peering <br>&emsp; + Module 02-Lab19-01: Introduction <br>&emsp; + Module 02-Lab19-02.1: Initialize CloudFormation Templates <br>&emsp; + Module 02-Lab19-02.2: Create Security Groups <br>&emsp; + Module 02-Lab19-02.3: Create EC2 instances <br>&emsp; + Module 02-Lab19-03: Update Network ACLs (NACLs) <br>&emsp; + Module 02-Lab19-04: Create a Peering Connection <br>&emsp; + Module 02-Lab19-05: Configure Route Tables <br>&emsp; + Module 02-Lab19-06: Enable Cross-Peer DNS <br>&emsp; + Module 02-Lab19-07: Clean up resources |  2025/09/20 |  2025/09/20      | https://000019.awsstudygroup.com/ |
| 7   | - **Lab 20:** Set up AWS Transit Gateway <br>&emsp; + Module 02-Lab20-01: Introduction <br>&emsp; + Module 02-Lab20-02: Preparation steps <br>&emsp; + Module 02-Lab20-03: Create Transit Gateway <br>&emsp; + Module 02-Lab20-04: Create Transit Gateway Attachments <br>&emsp; + Module 02-Lab20-05: Create Transit Gateway Route Tables <br>&emsp; + Module 02-Lab20-06: Add Transit Gateway Routes to VPC Route Tables <br>&emsp; + Module 02-Lab20-07: Clean up resources <br> - Write weekly report and review all learned content |  2025/09/21 |  2025/09/21      | https://000020.awsstudygroup.com/ |


### Week 2 Achievements:

* Gained comprehensive understanding of AWS VPC architecture and security features.
* Successfully created VPC with custom CIDR blocks, Subnets, Route Tables, Internet Gateway, and NAT Gateway.
* Configured Security Groups and Network ACLs to control inbound and outbound traffic.
* Deployed EC2 instances in different subnets and tested connectivity.
* Set up EC2 Instance Connect Endpoint for secure SSH access.
* Implemented Hybrid DNS solution using Route 53 Resolver with Inbound and Outbound Endpoints.
* Successfully configured VPC Peering between two VPCs with proper routing and DNS resolution.
* Deployed AWS Transit Gateway to connect multiple VPCs in a hub-and-spoke architecture.
* Completed all hands-on labs and consolidated networking knowledge.


### Week 2 Summary:

This week focused on AWS VPC networking fundamentals and advanced connectivity patterns. Started with understanding VPC architecture including Subnets, Route Tables, Internet Gateway, and NAT Gateway through Lab 03. Learned how to secure VPC resources using Security Groups and Network ACLs to control traffic flow.

Progressed to more advanced topics including Hybrid DNS resolution with Route 53 Resolver (Lab 10), enabling seamless DNS queries between on-premises and AWS environments. Explored VPC connectivity options through VPC Peering (Lab 19) for direct communication between two VPCs, and AWS Transit Gateway (Lab 20) for scalable multi-VPC architectures.

Key hands-on experience included deploying EC2 instances across different subnets, configuring routing tables for proper traffic flow, setting up CloudFormation templates for infrastructure automation, and implementing EC2 Instance Connect Endpoint for secure access. All labs concluded with proper resource cleanup to follow AWS best practices.

The week provided a solid foundation in AWS networking, preparing for more complex cloud architectures and hybrid cloud scenarios.


### Reference Materials:

**Workshop Labs:**
* **Lab 03 - Start with Amazon VPC and AWS VPN Site-to-Site:**  
  https://000003.awsstudygroup.com/

* **Lab 10 - Set up Hybrid DNS with Route 53 Resolver:**  
  https://000010.awsstudygroup.com/

* **Lab 19 - Set up VPC Peering:**  
  https://000019.awsstudygroup.com/

* **Lab 20 - Set up AWS Transit Gateway:**  
  https://000020.awsstudygroup.com/

**AWS Official Documentation:**
* **Amazon VPC User Guide:**  
  https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html

* **VPC Security Groups:**  
  https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html

* **Network ACLs:**  
  https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html

* **Route 53 Resolver:**  
  https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html

* **VPC Peering Guide:**  
  https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html

* **AWS Transit Gateway:**  
  https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html

**Video Tutorials:**
* **AWS VPC Beginner to Pro:**  
  https://www.youtube.com/watch?v=fpxDGU2KdkA

* **AWS Networking Fundamentals:**  
  https://www.youtube.com/watch?v=hiKPPy584Mg

* **VPC Peering vs Transit Gateway:**  
  https://www.youtube.com/watch?v=ar6sLmJ45xs

**Additional Resources:**
* **AWS Networking Best Practices:**  
  https://aws.amazon.com/architecture/well-architected/

* **VPC CIDR Calculator:**  
  https://www.ipaddressguide.com/cidr

* **AWS Skill Builder - VPC Course:**  
  https://explore.skillbuilder.aws/learn
