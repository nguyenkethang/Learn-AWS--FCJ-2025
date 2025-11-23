---
title: "Blog 2"
date: 2025-04-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Displaying Network Performance for AWS Workloads with Network Flow Monitor

**Authors:** Hiroki Fujii and Vishwas Puttasubbappa  
**Date:** April 30, 2025  
**Categories:** Amazon CloudWatch, Amazon VPC, Announcements, Monitoring and observability, Networking & Content Delivery

---

## Introduction

AWS launched **Network Flow Monitor** at re:Invent on December 1, 2024, a new feature in the Amazon CloudWatch Network Monitoring suite that provides network performance monitoring capabilities across AWS-managed services.

With Network Flow Monitor, you can gain near real-time visibility into network traffic between:
- Compute resources (Amazon EC2 and Amazon EKS)
- AWS services (Amazon S3, Amazon DynamoDB)
- AWS infrastructure

This collected data can help you identify and resolve network issues for your applications faster by reducing troubleshooting time for your cloud environment.

---

## Cloud Network Observability Challenges

When applications experience high latency, network issues are often the first suspected cause, whether in cloud or on-premises environments.

As many of you may know, traditional network monitoring tools provide limited visibility into:
- AWS network infrastructure
- Network performance between AWS-managed services

This can prolong the troubleshooting process and impact both:
- **MTTD** (Mean Time To Detect)
- **MTTR** (Mean Time To Recover)

---

## CloudWatch Performance Monitoring Features

Network Flow Monitor enables CloudWatch to provide comprehensive observability services for both:
- **Network Monitoring**
- **Application Performance Monitoring (APM)**

![Figure 1. CloudWatch Application Performance Monitoring and Network Monitoring Features](images/image1.png)

### How It Works

Network Flow Monitor uses **lightweight agents** installed on resources to collect performance metrics directly from actual workload traffic, enabling near real-time monitoring.

### Key Network Metrics Tracked:
- Data transmitted
- Retransmissions
- Retransmission timeouts
- Round-trip time

### Network Health Indicator (NHI)

A standout feature of flow monitor is the **Network Health Indicator (NHI)**. NHI allows you to determine whether network degradation is due to AWS infrastructure issues.

When network latency occurs, this indicator is extremely useful, helping you identify the root cause so you can focus remediation efforts effectively.

---

## Example Monitoring Scenario

In this section, we'll examine an example of two EC2 instances in different VPCs, within the same Region, connected via AWS Transit Gateway.

### Environment Setup

For our example:
- Installed an agent on EC2 instance **test-instance-1** in VPC 1 to provide network performance data
- Built an Apache web server on a second EC2 instance **test-instance-2** in VPC 2
- Enabled the httpd service

![Figure 2. Example cross-VPC network monitoring setup for Network Flow Monitor](images/image2.png)

### Passive vs Active Monitoring

Unlike active monitoring solutions, Network Flow Monitor provides **continuous passive monitoring**, analyzing actual user traffic between workloads.

We created test traffic from test-instance-1 (with agent installed) to test-instance-2 (Apache web server).

![Figure 3. Agent collecting data for HTTP traffic flow between an instance in VPC 1 and a web server in VPC 2](images/image3.png)

---

## Setting Up Network Flow Monitor

In this section, we'll guide you through setting up Network Flow Monitor based on our example scenario.

### Setup Steps:

1. **Enable Network Flow Monitor**
2. **Install Network Flow Monitor agents**
3. **Review network flows in Workload insights**
4. **Create one or more flow monitors**

---

### Step 1: Enable Network Flow Monitor

Before you can use Network Flow Monitor, we must enable the necessary permissions to send data to CloudWatch and map our network connections.

When you navigate to Network Flow Monitor in the console for the first time, you'll be prompted to enable this feature.

![Figure 4. Enable Network Flow Monitor](images/image4.png)

#### Enablement Process:

Enabling Network Flow Monitor will:
- Set up necessary permissions
- Create your monitoring scope (currently the AWS account you're logged into)

**Wait Time:** Wait a short time (up to 30 minutes) while Network Flow Monitor:
- Grants permissions using the necessary service-linked roles to your account
- Sets up the monitoring scope for your AWS account

---

### Step 2: Install Network Flow Monitor Agents

When you install agents on your instances, you must also set permissions for the agents so they can send data to the Network Flow Monitor backend.

#### System Requirements:

There are specific requirements for Linux instances that you can use on your instances, listed in the Amazon CloudWatch documentation.

#### Supported Platforms:

You can install agents on:
- EC2 instances
- Self-managed Kubernetes instances
- Amazon EKS

#### Permission Configuration:

To enable the correct permissions, EC2 instances running the agent must use a role with the **CloudWatchNetworkFlowMonitorAgentPublishPolicy** policy.

![Figure 5. Attach Network Flow Monitor policy to target instance role](images/image5.png)

#### Installing Agents via Systems Manager:

Next, we install agents in the instances. To install agents, we use **AWS Systems Manager Agent**, a feature of AWS System Manager.

**Prerequisites:** Before you begin installing agents, ensure each instance is running Systems Manager Agent. For more information, see **Working with Systems Manager Agent**.

#### Agent Installation Steps:

**1. Open AWS Systems Manager Console**
   - In the Console, open the AWS Systems Manager dashboard
   - Under Node Tools, select **Distributor**

**2. Find the Network Flow Monitor Package**
   - Under Owned by Amazon, find the package: **AmazonCloudWatchNetworkFlowMonitorAgent**
   - Select the package, then choose **Install one time** or **Install on schedule**

![Figure 6. In Systems Manager, select the Network Flow Monitor agent package](images/image6.png)

**3. Select EC2 Instances**
   - Select the EC2 instances to install the agents
   - For our example, we only select **test-instance-1**

![Figure 7. In Systems Manager, select instances to install agents](images/image7.png)

**4. Run Installation**
   - Finally, select **Run** to begin agent installation

After installation completes successfully, you'll see the command status notification.

![Figure 8. Agent successfully installed on target instance](images/image8.png)

---

### Step 3: Review Network Flows in Workload Insights

After you enable Network Flow Monitor and install agents, you can review network flow performance data in the console.

#### Accessing Workload Insights:

1. In the CloudWatch dashboard, under **Network Monitoring**, select **Flow monitors**
2. On the **Workload insights** tab, you can review top contributing network flows
3. You can identify which flows you want to monitor in more detail

For more details, see **Evaluating network flows with workload insights**.

![Figure 9. Network flow data in CloudWatch](images/image9.png)

#### Creating Monitors from Top Contributors:

To dive deeper into specific network flows, you can create a monitor in one of two ways:

**Method 1:** Select network flows in **Top contributors**, then select **Create monitor**

**Method 2:** Select **Create monitor**, and then specify individual local and remote resources to monitor network flows between them (as described in Step 4)

---

### Step 4: Create a Flow Monitor

To begin creating a monitor, in the Network Flow Monitor dashboard, select **Create monitor**.

![Figure 10. Create a monitor in Network Flow Monitor](images/image10.png)

#### Monitor Creation Steps:

**1. Name the Monitor**

For **Monitor name**, we choose: `monitor-ap-northeast-1c-1a`

![Figure 11. Specify name for flow monitor](images/image11.png)

**2. Select Local Resources**

Specify the types of network flows you want to monitor, then select specific options for each type.

**Supported local resource types:**
- Subnet
- VPC
- Availability Zone

For our example, we select the subnet where the instance resides: `flowmonitor-subnet-ap-northeast-1c`

![Figure 12. Select one or more local resources for flow monitor](images/image12.png)

**3. Select Remote Resources**

You have two options:

**Option A: Everywhere**
- Monitor includes all network flows originating from selected local resources

**Option B: Select remote resources**
- You can select specific remote resources to monitor
- Can select one or more resources in:
  - Subnets
  - VPCs
  - Availability Zones (AZs)
  - AWS services (Amazon S3, DynamoDB, etc.)

For our example, we specify a subnet as the remote resource hosting our web server: `flowmonitor-subnet-ap-northeast-1a`

![Figure 13. Select remote resources for flow monitor](images/image13.png)

**4. Complete Monitor Creation**

- Select **Next**, and then review the configuration for the monitor
- Select **Create monitor**

**Wait Time:** After you create the monitor, wait up to 30 minutes for Network Flow Monitor to begin collecting and aggregating data.

---

## Visualizing Network Flow Monitor Metrics

After you create a monitor, Network Flow Monitor begins publishing:
- End-to-end performance metrics
- A network health indicator for network degradation issues

### Where to View Metrics:

You can visualize information for a monitor in two places:

**1. Network Flow Monitor Dashboard**

**2. CloudWatch Metrics**
- Under the custom namespace: `AWS/NetworkFlowMonitor`

### Viewing Performance Data in Console:

For our example, we view in the Network Flow Monitor dashboard to see performance data for our monitor.

1. On the **Monitors** tab, select the monitor: `monitor-ap-northeast-1c-1a`

![Figure 14. View performance data in a flow monitor](images/image14.png)

2. For an overview of network flows for the monitor, check the **Overview** tab

![Figure 15. Visualize performance metrics on the Overview tab for the monitor](images/image15.png)

### Historical Explorer:

Next, go to the **Historical explorer** tab to view more detailed metrics for monitored network flows.

#### Topology Feature:

When performance degradation occurs, the topology feature displays:
- All components in the network path
- Service icons and resource IDs

This visualization helps you identify:
- Top contributors for each performance metric
- Source-destination bucket pairs within the specified time frame to take recovery actions

![Figure 16. Visualize network flow topology for degradation issues](images/image16.png)

---

## Resource Cleanup

After completing your Network Flow Monitor evaluation, promptly delete all test monitors and temporary resources.

---

## Conclusion

In this post, we introduced **Network Flow Monitor**, a new observability feature of Amazon CloudWatch Network Monitoring that provides near real-time visibility into network performance for workloads between compute instances and AWS services.

### Key Benefits:

Using the range of metrics and information that flow monitors provide, you can:
- Quickly analyze and act on network performance degradation
- Minimize troubleshooting time for your cloud workloads
- Improve MTTD and MTTR

---

## Learn More About Network Flow Monitor

Now that we've shared an overview of Network Flow Monitor benefits, check out the following additional information for details:

### Useful Resources:

**1. Pricing**
- To learn more about pricing, visit the [CloudWatch pricing page](https://aws.amazon.com/cloudwatch/pricing/)

**2. Regional Availability**
- Flow Monitor is currently available in **17 AWS Regions**
- For the complete list, see the documentation

**3. Technical Documentation**
- For details and technical guidance on Network Flow Monitor, see the [technical documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Network-Flow-Monitor.html)

---

## About the Authors

### Hiroki Fujii

![Hiroki Fujii](images/image17.png)

**Hiroki** is a Senior Technical Account Manager working in Singapore. He has over 10 years of experience in designing, building, and operating on-premises networks, including:
- Data centers
- Campus networks
- Backbone networks

Outside of work, he enjoys exercising, playing golf, and exploring new countries and cultures with his wonderful family.

### Vishwas Puttasubbappa

![Vishwas Puttasubbappa](images/image18.png)

**Vishwas** is a Principal Product Manager Technical in the AWS Networking division. He has worked in networking for the past 20 years, designing and building networks and network products.

Outside of work, he enjoys spending most of his time with his family.

---
