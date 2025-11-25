---
title: "Nhật ký công việc Tuần 7"
date: 2025-10-26
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Học về các dịch vụ Database và Analytics trên AWS
* Thực hành với DynamoDB, Kinesis, Glue, Athena và QuickSight
* Hiểu cách xây dựng data pipeline cơ bản

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **Lab 35 - Kinesis & Glue:** <br>&emsp; + Tạo S3 Bucket <br>&emsp; + Tạo Kinesis Delivery Stream <br>&emsp; + Tạo dữ liệu mẫu                                                            | 2025/10/20   | 2025/10/20      | <https://catalog.workshops.aws/> |
| 3   | - **Lab 35 (tiếp):** <br>&emsp; + Tạo Glue Crawler <br>&emsp; + Kiểm tra dữ liệu <br>&emsp; + Cấu hình Session connect                                                                     | 2025/10/21   | 2025/10/21      | <https://catalog.workshops.aws/> |
| 4   | - **Lab 35 (tiếp) & Lab 39 - DynamoDB:** <br>&emsp; + Phân tích với Athena <br>&emsp; + Visualize với QuickSight <br>&emsp; + Tìm hiểu DynamoDB cơ bản                                      | 2025/10/22   | 2025/10/22      | <https://catalog.workshops.aws/> <br> <https://aws.amazon.com/dynamodb/> |
| 5   | - **Lab 39 (tiếp):** <br>&emsp; + Khám phá DynamoDB Console <br>&emsp; + Backup và Restore <br>&emsp; + Advanced Design Patterns                                                            | 2025/10/23   | 2025/10/23      | <https://aws.amazon.com/dynamodb/> |
| 6   | - **Lab 60 & 70 - CloudShell & DataBrew:** <br>&emsp; + Sử dụng CloudShell <br>&emsp; + Tạo Cloud9 Instance <br>&emsp; + Upload dataset lên S3 <br>&emsp; + Clean & Transform data          | 2025/10/24   | 2025/10/24      | <https://aws.amazon.com/databrew/> |
| 7   | - **Lab 72 & 73 - Data Analytics Pipeline:** <br>&emsp; + Transform data với Glue <br>&emsp; + Phân tích với Athena <br>&emsp; + Tạo Dashboard với QuickSight                               | 2025/10/25   | 2025/10/26      | <https://aws.amazon.com/big-data/> |


### Kết quả đạt được tuần 7:

* Hiểu về các dịch vụ Database và Analytics trên AWS:
  * Amazon DynamoDB - NoSQL Database
  * Amazon Kinesis - Real-time data streaming
  * AWS Glue - ETL service
  * Amazon Athena - Query service
  * Amazon QuickSight - BI tool

* Thực hành xây dựng data pipeline cơ bản:
  * Thu thập dữ liệu với Kinesis
  * Lưu trữ trên S3
  * Catalog với Glue Crawler
  * Phân tích với Athena
  * Visualize với QuickSight

* Làm việc với DynamoDB:
  * Tạo và quản lý tables
  * Backup và restore
  * Hiểu về partition key và sort key

* Sử dụng AWS DataBrew để clean và transform data

* Biết cách sử dụng CloudShell và Cloud9 để làm việc với AWS

* Tạo được dashboard cơ bản với QuickSight để visualize dữ liệu



### Tóm tắt tuần 7:

Tuần này tập trung vào việc học và thực hành các dịch vụ Database và Analytics của AWS. Đây là những dịch vụ quan trọng để xây dựng các ứng dụng xử lý dữ liệu hiện đại. Qua các lab thực hành, đã hiểu được cách các dịch vụ này kết nối với nhau để tạo thành một data pipeline hoàn chỉnh - từ việc thu thập dữ liệu real-time (Kinesis), lưu trữ (S3), xử lý và chuyển đổi (Glue), truy vấn (Athena), đến visualize (QuickSight). Đặc biệt, DynamoDB là một NoSQL database mạnh mẽ phù hợp cho các ứng dụng cần hiệu suất cao và khả năng mở rộng tốt.

---

### Bài học rút ra:

**1. Về kiến trúc dữ liệu:**
* Hiểu được tầm quan trọng của việc thiết kế data pipeline đúng cách từ đầu
* Mỗi dịch vụ AWS có vai trò riêng và cần kết hợp chúng một cách hợp lý
* Việc chọn đúng loại database (SQL vs NoSQL) phụ thuộc vào use case cụ thể

**2. Về DynamoDB:**
* Partition key và sort key rất quan trọng cho hiệu suất
* Cần suy nghĩ kỹ về access patterns trước khi thiết kế schema
* DynamoDB phù hợp cho ứng dụng cần low latency và high throughput
* Backup và restore là cần thiết để bảo vệ dữ liệu

**3. Về Data Pipeline:**
* Kinesis giúp xử lý streaming data real-time hiệu quả
* Glue Crawler tự động catalog data, tiết kiệm thời gian
* Athena cho phép query trực tiếp trên S3 mà không cần load data
* QuickSight giúp visualize dữ liệu dễ dàng cho business users

**4. Về thực hành:**
* Nên bắt đầu với dataset nhỏ để test trước khi scale up
* Luôn kiểm tra chi phí khi sử dụng các dịch vụ AWS
* Clean up resources sau khi thực hành để tránh phát sinh chi phí
* Đọc documentation kỹ trước khi bắt đầu lab

**5. Về kỹ năng:**
* Cần nắm vững SQL để làm việc với Athena
* Hiểu về data format (JSON, Parquet, CSV) rất quan trọng
* CloudShell và Cloud9 giúp làm việc với AWS dễ dàng hơn
* Thực hành nhiều là cách tốt nhất để học AWS

**6. Những khó khăn gặp phải:**
* Ban đầu khó hiểu về partition key và sort key trong DynamoDB
* Cấu hình Glue Crawler đúng cần thời gian làm quen
* Query optimization trong Athena cần kinh nghiệm
* Tạo dashboard đẹp trong QuickSight cần thực hành nhiều

**7. Điều cần cải thiện:**
* Cần học thêm về performance tuning cho DynamoDB
* Tìm hiểu sâu hơn về Glue ETL jobs
* Học thêm về cost optimization cho các dịch vụ Analytics
* Thực hành nhiều hơn với real-world datasets

---

### Nguồn tài liệu tham khảo:

#### Tài liệu chính thức AWS:

**Amazon DynamoDB:**
- [DynamoDB Developer Guide](https://docs.aws.amazon.com/dynamodb/latest/developerguide/) - Hướng dẫn chi tiết
- [DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html) - Các best practices
- [DynamoDB Pricing](https://aws.amazon.com/dynamodb/pricing/) - Bảng giá và tính toán chi phí

**Amazon Kinesis:**
- [Kinesis Data Streams Documentation](https://docs.aws.amazon.com/kinesis/latest/dev/) - Tài liệu Kinesis Data Streams
- [Kinesis Data Firehose Documentation](https://docs.aws.amazon.com/firehose/latest/dev/) - Tài liệu Kinesis Firehose
- [Kinesis Getting Started](https://aws.amazon.com/kinesis/getting-started/) - Bắt đầu với Kinesis

**AWS Glue:**
- [AWS Glue Developer Guide](https://docs.aws.amazon.com/glue/latest/dg/) - Hướng dẫn Glue
- [Glue Crawler Documentation](https://docs.aws.amazon.com/glue/latest/dg/add-crawler.html) - Tài liệu về Crawler
- [AWS Glue DataBrew](https://docs.aws.amazon.com/databrew/latest/dg/) - Hướng dẫn DataBrew

**Amazon Athena:**
- [Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/) - Hướng dẫn sử dụng Athena
- [Athena SQL Reference](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html) - Tham khảo SQL

**Amazon QuickSight:**
- [QuickSight User Guide](https://docs.aws.amazon.com/quicksight/latest/user/) - Hướng dẫn QuickSight
- [QuickSight Tutorials](https://docs.aws.amazon.com/quicksight/latest/user/tutorials.html) - Các tutorial

**AWS CloudShell & Cloud9:**
- [CloudShell User Guide](https://docs.aws.amazon.com/cloudshell/latest/userguide/) - Hướng dẫn CloudShell
- [Cloud9 User Guide](https://docs.aws.amazon.com/cloud9/latest/user-guide/) - Hướng dẫn Cloud9

#### AWS Workshops & Labs:

- [AWS Workshops - Analytics](https://catalog.workshops.aws/categories/Analytics) - Các workshop về Analytics
- [AWS Workshops - Databases](https://catalog.workshops.aws/categories/Databases) - Các workshop về Database
- [DynamoDB Immersion Day](https://catalog.workshops.aws/dynamodb-immersion-day) - Workshop chuyên sâu DynamoDB
- [Build a Modern Data Architecture](https://catalog.workshops.aws/modern-data-architecture) - Xây dựng kiến trúc dữ liệu hiện đại
- [Serverless Data Lake](https://catalog.workshops.aws/serverless-data-lake) - Data Lake serverless

#### Video học tập (YouTube):

**AWS Official:**
- [Amazon DynamoDB Deep Dive](https://www.youtube.com/watch?v=HaEPXoXVf2k) - AWS re:Invent
- [AWS Glue Tutorial for Beginners](https://www.youtube.com/results?search_query=aws+glue+tutorial) - Các tutorial cơ bản
- [Amazon Athena Tutorial](https://www.youtube.com/results?search_query=amazon+athena+tutorial) - Hướng dẫn Athena
- [Amazon QuickSight Tutorial](https://www.youtube.com/results?search_query=amazon+quicksight+tutorial) - Hướng dẫn QuickSight

**Kênh học AWS tiếng Việt:**
- [AWS Vietnam User Group](https://www.youtube.com/@AWSVietnamUserGroup) - Cộng đồng AWS Việt Nam
- [Cloud Journey](https://www.youtube.com/@cloudjourney) - Các khóa học AWS tiếng Việt

**Kênh học AWS tiếng Anh:**
- [freeCodeCamp - AWS Certified Solutions Architect](https://www.youtube.com/watch?v=Ia-UEYYR44s) - Khóa học đầy đủ
- [Stephane Maarek](https://www.youtube.com/@StephaneMaarek) - AWS Certified instructor
- [Be A Better Dev](https://www.youtube.com/@BeABetterDev) - AWS tutorials thực tế

#### Tài liệu bổ sung:

**Blogs & Articles:**
- [AWS Database Blog](https://aws.amazon.com/blogs/database/) - Blog chính thức về Database
- [AWS Big Data Blog](https://aws.amazon.com/blogs/big-data/) - Blog về Big Data
- [DynamoDB Guide](https://www.dynamodbguide.com/) - Hướng dẫn DynamoDB chi tiết (Alex DeBrie)

**Sách tham khảo:**
- "The DynamoDB Book" by Alex DeBrie - Sách về DynamoDB
- "AWS Certified Database Study Guide" - Sách ôn thi AWS Database

**Community & Forums:**
- [AWS re:Post](https://repost.aws/) - Diễn đàn hỏi đáp AWS chính thức
- [Stack Overflow - AWS Tags](https://stackoverflow.com/questions/tagged/amazon-web-services) - Cộng đồng Stack Overflow
- [Reddit r/aws](https://www.reddit.com/r/aws/) - Cộng đồng AWS trên Reddit

**Practice & Hands-on:**
- [AWS Free Tier](https://aws.amazon.com/free/) - Tài khoản miễn phí để thực hành
- [AWS Skill Builder](https://skillbuilder.aws/) - Nền tảng học tập chính thức của AWS
- [Qwiklabs - AWS](https://www.qwiklabs.com/catalog?keywords=aws) - Labs thực hành có hướng dẫn
