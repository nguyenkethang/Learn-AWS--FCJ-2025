---
title: "Week 7 Worklog"
date: 2025-10-26
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Learn about AWS Database and Analytics services
* Practice with DynamoDB, Kinesis, Glue, Athena and QuickSight
* Understand how to build basic data pipelines

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - **Lab 35 - Kinesis & Glue:** <br>&emsp; + Create S3 Bucket <br>&emsp; + Create Kinesis Delivery Stream <br>&emsp; + Create sample data                                                              | 2025/10/20 | 2025/10/20      | <https://catalog.workshops.aws/> |
| 3   | - **Lab 35 (continued):** <br>&emsp; + Create Glue Crawler <br>&emsp; + Data check <br>&emsp; + Setup Session connect                                                                                 | 2025/10/21 | 2025/10/21      | <https://catalog.workshops.aws/> |
| 4   | - **Lab 35 (continued) & Lab 39 - DynamoDB:** <br>&emsp; + Analysis with Athena <br>&emsp; + Visualize with QuickSight <br>&emsp; + Learn DynamoDB basics                                             | 2025/10/22 | 2025/10/22      | <https://catalog.workshops.aws/> <br> <https://aws.amazon.com/dynamodb/> |
| 5   | - **Lab 39 (continued):** <br>&emsp; + Explore DynamoDB Console <br>&emsp; + Backup and Restore <br>&emsp; + Advanced Design Patterns                                                                 | 2025/10/23 | 2025/10/23      | <https://aws.amazon.com/dynamodb/> |
| 6   | - **Lab 60 & 70 - CloudShell & DataBrew:** <br>&emsp; + Use CloudShell <br>&emsp; + Create Cloud9 Instance <br>&emsp; + Upload dataset to S3 <br>&emsp; + Clean & Transform data                      | 2025/10/24 | 2025/10/24      | <https://aws.amazon.com/databrew/> |
| 7   | - **Lab 72 & 73 - Data Analytics Pipeline:** <br>&emsp; + Transform data with Glue <br>&emsp; + Analysis with Athena <br>&emsp; + Create Dashboard with QuickSight                                    | 2025/10/25 | 2025/10/26      | <https://aws.amazon.com/big-data/> |


### Week 7 Achievements:

* Understood AWS Database and Analytics services:
  * Amazon DynamoDB - NoSQL Database
  * Amazon Kinesis - Real-time data streaming
  * AWS Glue - ETL service
  * Amazon Athena - Query service
  * Amazon QuickSight - BI tool

* Practiced building basic data pipeline:
  * Collect data with Kinesis
  * Store on S3
  * Catalog with Glue Crawler
  * Analyze with Athena
  * Visualize with QuickSight

* Worked with DynamoDB:
  * Create and manage tables
  * Backup and restore
  * Understand partition key and sort key

* Used AWS DataBrew to clean and transform data

* Learned how to use CloudShell and Cloud9 to work with AWS

* Created basic dashboard with QuickSight to visualize data


### Week 7 Summary:

This week focused on learning and practicing AWS Database and Analytics services. These are essential services for building modern data processing applications. Through hands-on labs, I understood how these services connect together to create a complete data pipeline - from real-time data collection (Kinesis), storage (S3), processing and transformation (Glue), querying (Athena), to visualization (QuickSight). Notably, DynamoDB is a powerful NoSQL database suitable for applications requiring high performance and good scalability.

---

### Lessons Learned:

**1. About Data Architecture:**
* Understood the importance of designing data pipelines correctly from the start
* Each AWS service has its own role and needs to be combined properly
* Choosing the right database type (SQL vs NoSQL) depends on specific use cases

**2. About DynamoDB:**
* Partition key and sort key are crucial for performance
* Need to think carefully about access patterns before designing schema
* DynamoDB is suitable for applications requiring low latency and high throughput
* Backup and restore are essential for data protection

**3. About Data Pipeline:**
* Kinesis effectively handles real-time streaming data
* Glue Crawler automatically catalogs data, saving time
* Athena allows direct queries on S3 without loading data
* QuickSight makes data visualization easy for business users

**4. About Practice:**
* Should start with small datasets to test before scaling up
* Always check costs when using AWS services
* Clean up resources after practice to avoid charges
* Read documentation carefully before starting labs

**5. About Skills:**
* Need to master SQL to work with Athena
* Understanding data formats (JSON, Parquet, CSV) is important
* CloudShell and Cloud9 make working with AWS easier
* Practice is the best way to learn AWS

**6. Challenges Encountered:**
* Initially difficult to understand partition key and sort key in DynamoDB
* Configuring Glue Crawler correctly takes time to get familiar
* Query optimization in Athena requires experience
* Creating beautiful dashboards in QuickSight needs practice

**7. Areas for Improvement:**
* Need to learn more about performance tuning for DynamoDB
* Dive deeper into Glue ETL jobs
* Learn more about cost optimization for Analytics services
* Practice more with real-world datasets

---

### Reference Materials:

#### Official AWS Documentation:

**Amazon DynamoDB:**
- [DynamoDB Developer Guide](https://docs.aws.amazon.com/dynamodb/latest/developerguide/) - Detailed guide
- [DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html) - Best practices
- [DynamoDB Pricing](https://aws.amazon.com/dynamodb/pricing/) - Pricing and cost calculation

**Amazon Kinesis:**
- [Kinesis Data Streams Documentation](https://docs.aws.amazon.com/kinesis/latest/dev/) - Kinesis Data Streams docs
- [Kinesis Data Firehose Documentation](https://docs.aws.amazon.com/firehose/latest/dev/) - Kinesis Firehose docs
- [Kinesis Getting Started](https://aws.amazon.com/kinesis/getting-started/) - Getting started with Kinesis

**AWS Glue:**
- [AWS Glue Developer Guide](https://docs.aws.amazon.com/glue/latest/dg/) - Glue guide
- [Glue Crawler Documentation](https://docs.aws.amazon.com/glue/latest/dg/add-crawler.html) - Crawler documentation
- [AWS Glue DataBrew](https://docs.aws.amazon.com/databrew/latest/dg/) - DataBrew guide

**Amazon Athena:**
- [Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/) - Athena user guide
- [Athena SQL Reference](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html) - SQL reference

**Amazon QuickSight:**
- [QuickSight User Guide](https://docs.aws.amazon.com/quicksight/latest/user/) - QuickSight guide
- [QuickSight Tutorials](https://docs.aws.amazon.com/quicksight/latest/user/tutorials.html) - Tutorials

**AWS CloudShell & Cloud9:**
- [CloudShell User Guide](https://docs.aws.amazon.com/cloudshell/latest/userguide/) - CloudShell guide
- [Cloud9 User Guide](https://docs.aws.amazon.com/cloud9/latest/user-guide/) - Cloud9 guide

#### AWS Workshops & Labs:

- [AWS Workshops - Analytics](https://catalog.workshops.aws/categories/Analytics) - Analytics workshops
- [AWS Workshops - Databases](https://catalog.workshops.aws/categories/Databases) - Database workshops
- [DynamoDB Immersion Day](https://catalog.workshops.aws/dynamodb-immersion-day) - DynamoDB deep dive workshop
- [Build a Modern Data Architecture](https://catalog.workshops.aws/modern-data-architecture) - Modern data architecture
- [Serverless Data Lake](https://catalog.workshops.aws/serverless-data-lake) - Serverless data lake

#### Learning Videos (YouTube):

**AWS Official:**
- [Amazon DynamoDB Deep Dive](https://www.youtube.com/watch?v=HaEPXoXVf2k) - AWS re:Invent
- [AWS Glue Tutorial for Beginners](https://www.youtube.com/results?search_query=aws+glue+tutorial) - Basic tutorials
- [Amazon Athena Tutorial](https://www.youtube.com/results?search_query=amazon+athena+tutorial) - Athena guides
- [Amazon QuickSight Tutorial](https://www.youtube.com/results?search_query=amazon+quicksight+tutorial) - QuickSight guides

**Vietnamese AWS Channels:**
- [AWS Vietnam User Group](https://www.youtube.com/@AWSVietnamUserGroup) - AWS Vietnam Community
- [Cloud Journey](https://www.youtube.com/@cloudjourney) - AWS courses in Vietnamese

**English AWS Channels:**
- [freeCodeCamp - AWS Certified Solutions Architect](https://www.youtube.com/watch?v=Ia-UEYYR44s) - Full course
- [Stephane Maarek](https://www.youtube.com/@StephaneMaarek) - AWS Certified instructor
- [Be A Better Dev](https://www.youtube.com/@BeABetterDev) - Practical AWS tutorials

#### Additional Resources:

**Blogs & Articles:**
- [AWS Database Blog](https://aws.amazon.com/blogs/database/) - Official Database blog
- [AWS Big Data Blog](https://aws.amazon.com/blogs/big-data/) - Big Data blog
- [DynamoDB Guide](https://www.dynamodbguide.com/) - Detailed DynamoDB guide (Alex DeBrie)

**Books:**
- "The DynamoDB Book" by Alex DeBrie - DynamoDB book
- "AWS Certified Database Study Guide" - AWS Database certification book

**Community & Forums:**
- [AWS re:Post](https://repost.aws/) - Official AWS Q&A forum
- [Stack Overflow - AWS Tags](https://stackoverflow.com/questions/tagged/amazon-web-services) - Stack Overflow community
- [Reddit r/aws](https://www.reddit.com/r/aws/) - AWS community on Reddit

**Practice & Hands-on:**
- [AWS Free Tier](https://aws.amazon.com/free/) - Free account for practice
- [AWS Skill Builder](https://skillbuilder.aws/) - Official AWS learning platform
- [Qwiklabs - AWS](https://www.qwiklabs.com/catalog?keywords=aws) - Guided hands-on labs
