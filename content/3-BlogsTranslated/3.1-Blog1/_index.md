---
title: "Blog 1"
date: 2025-04-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Hiển thị hiệu suất mạng cho workload trên AWS với Network Flow Monitor

**Tác giả:** Hiroki Fujii và Vishwas Puttasubbappa  
**Ngày xuất bản:** 30 THÁNG 4 năm 2025  
**Danh mục:** Amazon CloudWatch, Amazon VPC, Announcements, Monitoring and observability, Networking & Content Delivery

---

## Giới thiệu

AWS đã ra mắt **Network Flow Monitor** tại re:Invent vào ngày 1 tháng 12 năm 2024, một tính năng mới trong bộ **Amazon CloudWatch Network Monitoring**, cung cấp khả năng giám sát hiệu suất mạng trên các dịch vụ do AWS quản lý. 

Với Network Flow Monitor, bạn có thể có được khả năng hiển thị gần như thời gian thực về lưu lượng mạng giữa các tài nguyên tính toán (Amazon Elastic Compute Cloud (Amazon EC2) và Amazon Elastic Kubernetes Service (Amazon EKS)) và các dịch vụ của AWS, chẳng hạn như Amazon S3 và Amazon DynamoDB, cũng như cơ sở hạ tầng của AWS. 

Dữ liệu thu thập này có thể giúp bạn xác định và giải quyết các vấn đề mạng cho ứng dụng của mình nhanh hơn bằng cách giảm thời gian khắc phục sự cố cho môi trường đám mây của bạn.

---

## Các thách thức về khả năng quan sát với mạng đám mây

Khi các ứng dụng gặp độ trễ cao, các vấn đề về mạng thường là nguyên nhân bị nghi ngờ đầu tiên, dù là trong môi trường đám mây hay tại chỗ. Như nhiều người trong số các bạn có thể đã biết, các công cụ giám sát mạng truyền thống cung cấp khả năng hiển thị hạn chế đối với cơ sở hạ tầng mạng AWS và hiệu suất mạng giữa các dịch vụ được quản lý của AWS. 

Điều này có thể kéo dài quy trình khắc phục sự cố và ảnh hưởng đến cả **thời gian trung bình để phát hiện (MTTD)** và **thời gian trung bình để phục hồi (MTTR)**

---

## 🆕 AWS Competency Partners

To successfully adopt cloud in today’s complex IT environments, customers can collaborate with **AWS Competency Partners**.

This program validates and promotes partners who demonstrate **deep technical expertise** and **proven customer success** in specific solution areas. Guidance from these experts helps businesses achieve **better and more efficient outcomes**.

![AWS Competency Partners Overview](images/image1.png)

### 🔹 New Partners

#### **AWS Competency in Advertising & Marketing Technology**
- Anzu.io | EMEA | Advertising Platform; Digital Customer Experience

#### **AWS Competency in Cloud Operations**
- avvale | EMEA | Cloud Financial Management  
- Qucoon | EMEA | Cloud Governance  
- Select Soluções | LATAM | Cloud Financial Management  
- ControlMonkey | EMEA | Cloud Governance; Operations Management  

#### **Competency in Consumer Packaged Goods**
- AssetWatch | NAMER | Manufacturing  
- Cloudinary | NAMER | Marketing  

#### **AWS Competency in Cyber Insurance**
- Measured Analytics and Insurance | NAMER | Cybersecurity Insurance  

#### **AWS Competency in Data & Analytics**
- Ankercloud | EMEA | Consulting Services  
- Trianz | NAMER | Consulting Services  

#### **AWS Competency in DevOps**
- Syntax Systems | NAMER | Consulting Services  

#### **AWS Competency in Digital Workplace**
- LCM Go Cloud | EMEA | Consulting Services  
- Celoxis Technologies | APAC | Collaboration Platform  

#### **AWS Competency in Education**
- CloudiQS | EMEA | Consulting Services  
- CloudThat | APAC | Consulting Services  
- Wiz | NAMER | Administration & Operations  
- Zscaler | NAMER | Administration & Operations  

#### **Competency in Energy & Utilities**
- Innovapptive | NAMER | Downstream; Midstream; Upstream  
- Schlumberger | NAMER | Data Analytics & Insights; Upstream  

#### **AWS Competency in Financial Services**
- Blend | NAMER | Consulting Services  
- Kyriba | EMEA | Capital Markets  

#### **AWS Competency in Generative AI**
- 上海南洋万邦软件技术有限公司 – Nanyang Softland | China | Consulting Services  
- ARKHO | LATAM | Consulting Services  
- Beijing Yun Shi Shu Ju Technology | China | Consulting Services  
- Blend | NAMER | Consulting Services  
- Cloudmates | EMEA | Consulting Services  
- Compie Technologies | EMEA | Consulting Services  
- Darede | LATAM | Consulting Services  
- Ganit Business Solutions | APAC | Consulting Services  
- Going Cloud | China | Consulting Services  
- GS Neotek | APAC | Consulting Services  
- Netlight Consulting | EMEA | Consulting Services  
- OMNYS | EMEA | Consulting Services  
- Singtel Group / NCS / Optus | APAC | Consulting Services  
- SnapSoft | NAMER | Consulting Services  
- SoftwareOne | EMEA | Consulting Services  
- Source Allies, Inc | NAMER | Consulting Services  
- 特赞（上海）信息科技有限公司 | China | Generative AI Applications  
- Articul8 AI | NAMER | Foundation Model & Application Development; Generative AI Applications; Infrastructure & Data  
- Feenix.ai | NAMER | Generative AI Applications  
- Informatica | NAMER | Generative AI Applications  
- Vody.com | NAMER | Generative AI Applications  

#### **AWS Competency in Government**
- Inflectra Corporation | NAMER | Citizen Services  
- Over-C | EMEA | Citizen Services  
- SentinelOne | NAMER | Government Technology & Tools  

#### **AWS Competency in Healthcare**
- BioT Medical | EMEA | Clinical Information Systems; Compliance Services; Healthcare Management; Population Health & Analytics  
- Wiz | NAMER | Compliance Services  

#### **AWS Competency in High Performance Computing (HPC)**
- Fovus | NAMER | HPC Management  

#### **AWS Level 1 MSSP Competency**
- Comprinno Technologies | APAC | Level 1 Managed Security Services  

#### **AWS Competency in Machine Learning**
- Impetus Technologies | NAMER | Consulting Services  

#### **AWS Competency in Mainframe Modernization**
- Slalom | NAMER | Mainframe Workloads  

#### **AWS Competency in Manufacturing & Industrial**
- Cognizant | NAMER | Enterprise Solutions; Operations Technology; Smart Manufacturing; Supply Chain Management  

#### **AWS Competency in Media & Entertainment**
- AppEvolve | NAMER | Broadcast; Direct-to-Consumer  
- DataArt | NAMER | Media Supply Chain & Archive  

#### **AWS Competency in Migration & Modernization**
- Almaviva | EMEA | Migration Services  
- Bespin Global | APAC | Modernization Services  
- ForceOne | LATAM | Migration Services  
- TrueMark Technologies | NAMER | Migration Services  

#### **AWS Competency in Networking**
- Fortinet | NAMER | Consulting Services  
- Qucoon | EMEA | Consulting Services  

#### **AWS Competency in Nonprofit**
- Acloud Co. | APAC | Consulting Services  
- Incline-IT (MIS Group) | EMEA | Consulting Services  
- Quantiphi | NAMER | Consulting Services  

#### **AWS Competency in Oracle**
- SYSTEX RAINBOW TECH CO | China | Consulting Services  

#### **AWS Competency in Resilience**
- bestcloudfor.me | EMEA | Core Resilience; Resilience Design; Resilience Operations; Disaster Recovery  
- Dedicatted | NAMER | Core Resilience; Resilience Design  

#### **AWS Competency in Retail**
- Kyndryl | NAMER | Consulting Services  
- Oneture Technologies | APAC | Consulting Services  
- Tredence | NAMER | Consulting Services  
- Netop | EMEA | Core IT & Applications  
- Spectro Cloud | NAMER | Core IT & Applications  

#### **AWS Competency in SaaS**
- MethodData | NAMER | Builder; Design Services  

#### **AWS Competency in Security**
- RISCPoint | NAMER | Compliance & Privacy  

#### **AWS Competency in Small and Medium Business (SMB)**
- 神灏（北京）云计算科技有限公司 | China | Small and Medium Business  
- 北京聚云立方科技有限公司（Marshotspot limited) | China | Small and Medium Business  
- Chunghwa Telecom | China | Small and Medium Business  
- Entel | LATAM | Small and Medium Business  
- Intelligence Cloud Sphere- (Intel CS) | EMEA | Small and Medium Business  
- Nanjing OnCloud AI Co | China | Small and Medium Business  
- Nub8 | NAMER | Small and Medium Business  
- Trek10 | NAMER | Small and Medium Business  

#### **AWS Competency in Storage**
- ECLOUDVALLEY TECHNOLOGY | APAC | Consulting Services  
- Effectual | NAMER | Consulting Services  
- Kyndryl | NAMER | Consulting Services  

#### **AWS Competency in Travel & Hospitality**
- DataDome | EMEA | Core Applications; Digital Customer Engagement

---

## 🆕 AWS Managed Service Providers (MSP)

The **AWS Managed Service Provider (MSP)** program validates partners with **extensive experience delivering comprehensive AWS solutions**, including:
- Planning and design  
- Build and migration  
- Operation and support  
- Automation and optimization  

![AWS Managed Service Providers](images/image2.png)

### **Newest MSP Partners**
- Dedicatted | NAMER  
- Genpact | NAMER  
- Globant | LATAM  

---

## 🆕 AWS Service Ready Products

The **AWS Service Ready** program validates software products built by AWS Partners, ensuring **good integration and compatibility** with specific AWS services.

![AWS Service Ready Products](images/image3.png)

### **Newest Products**

#### **Amazon CloudFront Ready Products**
- 北京智齿博创科技有限公司 | China | Media Management; Monitoring & Analytics; Security  
- UDS | LATAM | Media Management  

#### **Amazon Linux Ready Products**
- Cloudpense | China | Amazon Linux 2  
- Tacnode | NAMER | Amazon Linux 2022  

#### **Amazon RDS Ready Products (Business Applications & Tools)**
- 太美医疗科技 | China | Business Applications  
- 福州领克狐科技有限公司 | China | Business Applications  
- iPinYou Inc | China | Business Applications  
- SF-DHL | China | Business Applications  

#### **AWS Graviton Ready Products**
- Share Creators Inc. | China | Application Stacks  

---

## 🆕 AWS Service Delivery Partners

The **AWS Service Delivery** program validates AWS Partners with **deep technical knowledge**, **experience**, and **proven success** in delivering specific AWS services to customers.

![AWS Service Delivery Partners](images/image4.png)

### **Newest Partners:**

#### **Amazon API Gateway Delivery Partners**
- ADAPTURE Technology Group | NAMER  
- Intellergy | EMEA  
- Kinu | NAMER  

#### **Amazon CloudFront Delivery Partners**
- Bion Solutions | EMEA  
- Caylent | NAMER  
- IT Visionary | EMEA  
- Kinu | NAMER  
- NCLOUD THREE INFORMATION TECHNOLOGY | EMEA  
- Techpartner Alliance | APAC  

#### **Amazon Connect Delivery Partners**
- TEKsystems Global Services | NAMER  

#### **Amazon DynamoDB Delivery Partners**
- Bexprt | EMEA  
- Business Compass | NAMER  
- Kinu | NAMER  

#### **Amazon EC2 for Microsoft Windows Server Delivery Partners**
- 博博未来科技（深圳）有限公司 | China  
- Bourntec Solutions | NAMER  
- Conviso | NAMER  
- DAIWABO INFORMATION SYSTEM | Japan  
- Innovative Digital Transformation | NAMER  
- Intelecta | LATAM  
- Mindware | EMEA  
- Registfy | EMEA  
- RSNA Cloud Connect | NAMER  
- Sedmi Odjel | EMEA  
- Shenzhen Indusfour Technology | China  
- SHINRAI TECHNOLOGIES | EMEA  

#### **AWS Systems Manager Delivery Partners**
- ADAPTURE Technology Group | NAMER  
- Cloud TechOn | APAC  
- Noventiq | EMEA  

#### **Amazon ECS Delivery Partners**
- Cloudster | LATAM | Containers  
- Decryptogen | | Compute; Containers; Serverless  
- Kinu | NAMER | Containers  
- Lauren Information Technologies (Ataloud) | APAC | Compute; Containers; Serverless  
- Skyloop Cloud | EMEA | Compute; Containers; Serverless  
- SKYLOUD | EMEA | Containers  
- VArrow Technologies | EMEA | Compute; Containers; Serverless  

#### **Amazon EKS Delivery Partners**
- CodetoKloud Inc | NAMER  
- Decryptogen |  
- Global Mobility Services | NAMER  
- Lauren Information Technologies Private Limited (Ataloud) | APAC  
- MOVE2CLOUD | EMEA  
- Visionet Systems | NAMER  

#### **Amazon EMR Delivery Partners**
- ADAPTURE Technology Group | NAMER  
- Stack | LATAM  

#### **Amazon Kinesis Delivery Partners**
- ADAPTURE Technology Group | NAMER  
- Mactores Cognition Inc | NAMER  
- Nublit by Domus Global | LATAM  

#### **Managed Streaming for Kafka (MSK) Delivery Partners**
- Woodmark Consulting AG | EMEA  

#### **Amazon OpenSearch Delivery Partners**
- Datamellon | EMEA | Log Analytics; Search  
- Lauren Information Technologies (Ataloud) | APAC | Log Analytics; Search  

#### **Amazon RDS Delivery Partners**
- Comprinno Technologies | APAC | Amazon RDS for MySQL; Amazon RDS for PostgreSQL  
- Epsilon srl | EMEA | Amazon Aurora MySQL  
- Kinu | NAMER | Amazon RDS for PostgreSQL  
- kloudr | EMEA | Amazon Aurora MySQL  
- Osam International | APAC | Amazon Aurora PostgreSQL; Amazon RDS for MySQL  
- RISCPoint | NAMER | Amazon Aurora MySQL; Amazon Aurora PostgreSQL; Amazon RDS for MySQL; Amazon RDS for PostgreSQL  
- TemaBit | EMEA | Amazon Aurora PostgreSQL; Amazon RDS for MySQL  
- Yalantis | EMEA | Amazon RDS for PostgreSQL  

#### **Amazon Redshift Delivery Partners**
- Applogika | NAMER  
- Ironside Group | NAMER  
- Zensar | NAMER  

#### **AWS CloudFormation Delivery Partners**
- Altostruct AB | EMEA  
- CloudThat | APAC  

#### **AWS Config Delivery Partners**
- ProfiSea | EMEA  
- SoftGEM Global Technologies | EMEA  

#### **AWS Control Tower Delivery Partners**
- DFX5 | NAMER | Container; Database; Infrastructure as a Service; Migration; Networking; Security; Serverless; Storage  
- IONAIM INNOVATIONS | APAC | Machine Learning; Security  
- Kinu | NAMER | Networking; Security  
- MyOps | EMEA | Infrastructure as a Service; Networking; Security  
- Pentagon System and Services | APAC | Infrastructure as a Service; Serverless  
- Rego Consulting Corporation | NAMER | Migration; Security  
- RISCPoint | NAMER | Networking; Security  
- Wipro | APAC | Infrastructure as a Service  

#### **AWS Direct Connect Partners (ISV and SI)**
- Telekomunikasi Indonesia International | APAC  

#### **AWS Glue Delivery Partners**
- Decryptogen |  
- In Motion | LATAM  
- Lauren Information Technologies (Ataloud) | APAC  
- Renoir Consulting | APAC  

#### **AWS GovCloud (US) Delivery Partners**
- TEKsystems Global Services | NAMER  

#### **AWS Graviton Delivery Partners**
- onkatec | EMEA  
- OpsTree Solutions | APAC  

#### **AWS Lambda Delivery Partners**
- ADAPTURE Technology Group | NAMER  
- Bexprt | EMEA  
- CloudZenia | APAC  
- Kinu | NAMER  
- PCI Solutions | Japan  
- Royal Cyber | NAMER  
- Structurit Consulting | EMEA  
- Trianz | NAMER  

#### **AWS Web Application Firewall (WAF) Delivery Partners**
- Hoovai Technologies | APAC  
- Kinu | NAMER  
- METROPOLITAN WIRELESS INTERNATIONAL | APAC  
- MyOps | EMEA  
- Nuvnet Tecnologia | LATAM  
- Vcloudmaster | EMEA  

---

## 💡 More Value, Greater Profitability for AWS Partners

![AWS Partner Value Proposition](images/image5.png)

AWS’s mission is to make **APN** and the **AWS Marketplace** the **preferred go-to-market path** that helps partners:
- Increase profitability  
- Win more deals  
- Scale faster  

AWS is enhancing the **AWS Partner experience** to provide more relevant, consistent, and predictable guidance.  
**Your profitability and your customers’ success** are our top priorities.

In 2025, AWS will continue to provide a proven success path that helps partners **drive greater customer value and profitability**.  
The journey ahead is exciting — and we’re thrilled to be part of it with you!

---