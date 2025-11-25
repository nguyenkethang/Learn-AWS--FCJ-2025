---
title: "Nhật ký công việc Tuần 4"
date: 2025-10-05
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4:
* Nắm vững các dịch vụ lưu trữ chính trên AWS bao gồm **Amazon S3**, **Glacier**, **Snow Family**, **Storage Gateway**, **AWS Backup** và **Amazon FSx**.  
* Hiểu rõ các khái niệm về **RTO/RPO** và các chiến lược **khôi phục thảm họa (Disaster Recovery)** trên AWS.  
* Thực hành các Lab về S3 Bucket, Backup Plan, Storage Gateway, VM Migration và FSx for Windows File Server.
* Nắm vững các tính năng nâng cao của S3: Access Point, Storage Class, CORS, Versioning, Replication.

---

### Nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | -------- | ------------- | ---------------- | ------------------ |
| 1 | - **Module 04-01:** Dịch Vụ Lưu Trữ Trên AWS <br> - **Module 04-02:** Amazon S3 - Access Point - Storage Class <br>&emsp; + Khái niệm Object Storage, Bucket và Object <br>&emsp; + S3 Access Point để quản lý truy cập <br>&emsp; + Các lớp lưu trữ: Standard, IA, Intelligent-Tiering, Glacier <br> - **Lab 13-02.1:** Create S3 Bucket | 2025/09/29 | 2025/09/29 | https://000013.awsstudygroup.com/ |
| 2 | - **Module 04-03:** S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier <br>&emsp; + Static Website Hosting <br>&emsp; + CORS Configuration <br>&emsp; + Bucket Policy, ACL, IAM Policy <br>&emsp; + Object Key Optimization <br>&emsp; + Glacier Retrieval Options <br> - **Lab 13-02.2:** Deploy Infrastructure <br> - **Lab 13-03:** Create Backup Plan | 2025/09/30 | 2025/09/30 | https://000013.awsstudygroup.com/ |
| 3 | - **Module 04-04:** Snow Family - Storage Gateway - Backup <br>&emsp; + Snowball, Snowball Edge, Snowmobile <br>&emsp; + File Gateway, Volume Gateway, Tape Gateway <br>&emsp; + AWS Backup Service <br>&emsp; + RTO/RPO và Disaster Recovery Strategies <br> - **Lab 13-04:** Set up notifications <br> - **Lab 13-05:** Test Restore <br> - **Lab 13-06:** Clean up resources | 2025/10/01 | 2025/10/01 | https://000013.awsstudygroup.com/ |
| 4 | - **Lab 14-01:** VMWare Workstation Setup <br> - **Lab 14-02.1:** Export Virtual Machine from On-premises <br> - **Lab 14-02.2:** Upload virtual machine to AWS <br> - **Lab 14-02.3:** Import virtual machine to AWS <br> - **Lab 14-02.4:** Deploy Instance from AMI | 2025/10/02 | 2025/10/02 | https://000014.awsstudygroup.com/ |
| 5 | - **Lab 14-03.1:** Setting up S3 bucket ACL <br> - **Lab 14-03.2:** Export virtual machine from Instance <br> - **Lab 14-05:** Resource Cleanup on AWS Cloud <br> - **Lab 24-2.1:** Create Storage Gateway <br> - **Lab 24-2.2:** Create File Shares | 2025/10/03 | 2025/10/03 | https://000024.awsstudygroup.com/ |
| 6 | - **Lab 24-2.3:** Mount File shares on On-premises machine <br> - **Lab 24-3:** Clean up resources <br> - **Lab 25-2.2:** Create an SSD Multi-AZ file system <br> - **Lab 25-2.3:** Create an HDD Multi-AZ file system <br> - **Lab 25-3:** Create new file shares | 2025/10/04 | 2025/10/04 | https://000025.awsstudygroup.com/ |
| 7 | - **Lab 25-4:** Test Performance <br> - **Lab 25-5:** Monitor Performance <br> - **Lab 25-6:** Enable data deduplication <br> - **Lab 25-7:** Enable shadow copies <br> - **Lab 25-8:** Manage user sessions and open files <br> - **Lab 25-9:** Enable user storage quotas <br> - **Lab 25-11:** Scale throughput capacity <br> - **Lab 25-12:** Scale storage capacity <br> - **Lab 25-13:** Delete environment <br> - Viết báo cáo tuần và ôn tập toàn bộ nội dung đã học | 2025/10/05 | 2025/10/05 | https://000025.awsstudygroup.com/ |

---

### Kết quả đạt được trong tuần:

#### Amazon Simple Storage Service (S3)
Trong tuần này, em đã tìm hiểu chi tiết về **Amazon S3** – một dịch vụ lưu trữ đối tượng (Object Storage) trên nền tảng AWS.  
Dữ liệu trong S3 được lưu trữ dưới dạng các **đối tượng (objects)** trong **bucket**, có độ bền 99.999999999% và độ sẵn sàng 99.99%.  
Mỗi object có thể lên đến **5TB**, và dữ liệu được **sao lưu trên 3 vùng sẵn sàng (AZ)** trong cùng một khu vực (Region) để đảm bảo an toàn.  

Amazon S3 hỗ trợ nhiều tính năng hữu ích như **Multipart Upload** (tải tệp lớn theo từng phần), **Trigger Event** (kích hoạt hành động khi có sự kiện upload hoặc delete), và truy cập thông qua **REST API (HTTP)**.  
S3 đặc biệt phù hợp cho các loại dữ liệu ghi một lần – đọc nhiều lần (**WORM – Write Once Read Many**).

#### Amazon S3 Storage Class

Dịch vụ Amazon S3 được chia thành nhiều lớp lưu trữ (**Storage Classes**) để tối ưu chi phí và hiệu năng:  
- **S3 Standard:** Dành cho dữ liệu được truy cập thường xuyên.  
- **S3 Standard-IA:** Dành cho dữ liệu truy cập không thường xuyên.  
- **S3 Intelligent-Tiering:** Tự động di chuyển dữ liệu giữa các lớp dựa vào tần suất truy cập.  
- **S3 One Zone-IA:** Dữ liệu ít truy cập, chỉ lưu trong 1 AZ, chi phí thấp.  
- **S3 Glacier / Deep Archive:** Lưu trữ dài hạn, chi phí cực thấp.  

Người dùng có thể thiết lập **Object Lifecycle Management** để tự động chuyển dữ liệu giữa các lớp theo thời gian.

#### Access Control, Endpoint & Versioning

Amazon S3 hỗ trợ 2 cơ chế phân quyền chính:  
- **Access Control List (ACL)** – cấp quyền trực tiếp ở cấp đối tượng hoặc bucket.  
- **Bucket Policy / IAM Policy** – cho phép xác định quyền chi tiết thông qua Resource.  

Ngoài ra, có thể bật **Versioning** để khôi phục dữ liệu cũ khi bị ghi đè hoặc xóa, và dùng **S3 Endpoint** để truy cập an toàn trong mạng nội bộ AWS.

#### Static Website Hosting & CORS

Amazon S3 cho phép **host các website tĩnh (HTML, CSS, JS)**, rất phù hợp cho ứng dụng SPA (Single Page Application).  
Dịch vụ hỗ trợ **CORS (Cross-Origin Resource Sharing)**, cho phép các tài nguyên như script, hình ảnh, hoặc font được truy cập từ các domain khác nhau.

#### Performance Optimization

Trong S3, mỗi object được gán một **Object Key** duy nhất, không có cấu trúc thư mục phân cấp thật sự.  
Để tối ưu hiệu suất truy xuất, có thể sử dụng **prefix ngẫu nhiên** để phân bổ dữ liệu đều trên nhiều partition.

#### Amazon S3 Glacier

**S3 Glacier** là lớp lưu trữ chi phí thấp, dùng cho dữ liệu cần lưu dài hạn và ít truy cập.  
Có ba phương thức truy xuất dữ liệu:  
- **Expedited:** 1–5 phút.  
- **Standard:** 3–5 giờ.  
- **Bulk:** 5–12 giờ.  

#### AWS Snow Family

Dòng sản phẩm **Snow Family** gồm:  
- **Snowball:** Thiết bị di chuyển dữ liệu on-premise lên AWS, dung lượng tối đa 80TB.  
- **Snowball Edge:** Hỗ trợ xử lý (compute) tại chỗ, dung lượng 100TB.  
- **Snowmobile:** Giải pháp vận chuyển dữ liệu cực lớn, lên đến 100PB, dùng container chuyên dụng.

#### AWS Storage Gateway

Dịch vụ **AWS Storage Gateway** giúp kết nối môi trường **on-premise với AWS Cloud**, cung cấp giải pháp lưu trữ hybrid.  
Gồm ba loại chính:  
- **File Gateway:** Chia sẻ file (NFS/SMB) → lưu trữ S3.  
- **Volume Gateway:** Cung cấp block storage (iSCSI) → lưu snapshot lên S3/EBS.  
- **Tape Gateway:** Giải pháp sao lưu dạng băng ảo (VTL) → lưu trên S3/Glacier.

#### AWS Backup & Disaster Recovery

**AWS Backup** là dịch vụ quản lý sao lưu tập trung cho các tài nguyên AWS (EBS, EC2, RDS, DynamoDB, EFS, Storage Gateway).  
Hai khái niệm quan trọng:  
- **RTO (Recovery Time Objective):** Thời gian cần để khôi phục hệ thống.  
- **RPO (Recovery Point Objective):** Lượng dữ liệu tối đa có thể mất.  

Bốn chiến lược phục hồi thảm họa phổ biến:  
1. **Backup & Restore**  
2. **Pilot Light (Active–Standby)**  
3. **Low Capacity Active–Active**  
4. **Full Capacity Active–Active**

---

### Tổng kết Tuần 4:

Tuần này em đã hoàn thành việc học và thực hành toàn diện các dịch vụ lưu trữ trên AWS bao gồm Amazon S3, Glacier, Snow Family, Storage Gateway, AWS Backup và Amazon FSx for Windows File Server.

Qua 4 module lý thuyết và 4 chuỗi lab thực hành (Lab 13, 14, 24, 25), em đã nắm vững cách phân loại dữ liệu theo nhu cầu truy cập, cấu hình phân quyền chi tiết, triển khai backup tự động và thiết lập chính sách phục hồi thảm họa hiệu quả.

Đặc biệt, em đã thực hành được các kỹ năng quan trọng:
- Tạo và quản lý S3 Bucket với các Storage Class khác nhau
- Triển khai AWS Backup Plan cho EC2 và EBS với notification và test restore
- Cấu hình Storage Gateway để kết nối hybrid cloud và mount file shares
- Migration VM từ on-premises lên AWS thông qua VM Import/Export
- Triển khai và tối ưu Amazon FSx for Windows File Server với đầy đủ tính năng: deduplication, shadow copies, storage quotas, và scaling

Kiến thức này giúp em hiểu rõ cơ chế hoạt động của Object Storage, Access Control, Versioning, Lifecycle trong S3, cũng như các giải pháp lưu trữ hybrid và file system trên AWS, giúp quản lý dữ liệu linh hoạt, bảo mật và tiết kiệm chi phí.

---

### Tài liệu tham khảo:

**Bài Lab Workshop:**
* **Lab 13 - Deploy AWS Backup:**  
  https://000013.awsstudygroup.com/

* **Lab 14 - VM Import/Export:**  
  https://000014.awsstudygroup.com/

* **Lab 24 - Storage Gateway:**  
  https://000024.awsstudygroup.com/

* **Lab 25 - Amazon FSx for Windows File Server:**  
  https://000025.awsstudygroup.com/



**Tài liệu chính thức AWS:**
* **Amazon S3 User Guide:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/

* **S3 Storage Classes:**  
  https://aws.amazon.com/s3/storage-classes/

* **S3 Access Points:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points.html

* **S3 Static Website Hosting:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html

* **S3 CORS Configuration:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html

* **S3 Versioning:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html

* **S3 Replication:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html

* **S3 Lifecycle Management:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html

* **S3 Performance Optimization:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/optimizing-performance.html

* **Amazon S3 Glacier:**  
  https://docs.aws.amazon.com/amazonglacier/latest/dev/

* **AWS Snow Family:**  
  https://aws.amazon.com/snow/

* **AWS Snowball:**  
  https://docs.aws.amazon.com/snowball/

* **AWS Storage Gateway:**  
  https://docs.aws.amazon.com/storagegateway/

* **AWS Backup:**  
  https://docs.aws.amazon.com/aws-backup/

* **AWS Backup Best Practices:**  
  https://docs.aws.amazon.com/aws-backup/latest/devguide/best-practices.html

* **Amazon FSx for Windows File Server:**  
  https://docs.aws.amazon.com/fsx/latest/WindowsGuide/

* **VM Import/Export:**  
  https://docs.aws.amazon.com/vm-import/latest/userguide/

* **Amazon CloudFront:**  
  https://docs.aws.amazon.com/cloudfront/

* **Disaster Recovery on AWS:**  
  https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/

**Video hướng dẫn:**
* **Amazon S3 Tutorial:**  
  https://www.youtube.com/watch?v=_yunukwcAwc

* **S3 Storage Classes Explained:**  
  https://www.youtube.com/watch?v=BYW-HCr3Qbc

* **AWS Storage Gateway Deep Dive:**  
  https://www.youtube.com/watch?v=9wgaV70FeaM

* **AWS Snow Family Overview:**  
  https://www.youtube.com/watch?v=YXn8Q_Hpsu4

* **AWS Backup Tutorial:**  
  https://www.youtube.com/watch?v=dCy7ixko3tE

* **Amazon FSx for Windows File Server:**  
  https://www.youtube.com/watch?v=CW2hz-Uy7Gg

* **S3 Static Website with CloudFront:**  
  https://www.youtube.com/watch?v=mls8tiiI3uc

* **VM Migration to AWS:**  
  https://www.youtube.com/watch?v=afSJaFJsfXw

* **S3 Versioning and Replication:**  
  https://www.youtube.com/watch?v=4EOaAkY4pNE

* **AWS Storage Services Overview:**  
  https://www.youtube.com/watch?v=6vNC_BCqFmI

**Khóa học và Training:**
* **AWS Skill Builder - S3 Primer:**  
  https://explore.skillbuilder.aws/learn/course/external/view/elearning/50/amazon-s3-primer

* **AWS Skill Builder - Storage Learning Plan:**  
  https://explore.skillbuilder.aws/learn/learning_plan/view/51/storage-learning-plan

* **AWS Training - Storage Fundamentals:**  
  https://aws.amazon.com/training/learn-about/storage/

* **Coursera - AWS Fundamentals: Migrating to the Cloud:**  
  https://www.coursera.org/learn/aws-fundamentals-migrating-to-the-cloud

* **A Cloud Guru - AWS Certified Solutions Architect:**  
  https://acloudguru.com/course/aws-certified-solutions-architect-associate-saa-c03

**Blog Posts và Articles:**
* **AWS Storage Blog:**  
  https://aws.amazon.com/blogs/storage/

* **S3 Best Practices:**  
  https://aws.amazon.com/blogs/storage/best-practices-for-amazon-s3/

* **Optimizing S3 Performance:**  
  https://aws.amazon.com/blogs/storage/optimizing-amazon-s3-performance/

* **S3 Security Best Practices:**  
  https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/

* **Hybrid Cloud Storage with Storage Gateway:**  
  https://aws.amazon.com/blogs/storage/hybrid-cloud-storage-with-aws-storage-gateway/

* **Data Migration Strategies:**  
  https://aws.amazon.com/blogs/storage/aws-data-migration-strategies/

* **Disaster Recovery Strategies:**  
  https://aws.amazon.com/blogs/publicsector/rapidly-recover-mission-critical-systems-in-a-disaster/

**Whitepapers:**
* **AWS Storage Services Overview:**  
  https://docs.aws.amazon.com/whitepapers/latest/aws-storage-services-overview/

* **Cost Optimization for Storage:**  
  https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-storage-optimization/

* **Backup and Recovery Approaches Using AWS:**  
  https://docs.aws.amazon.com/whitepapers/latest/backup-recovery-approaches-using-aws/

* **Hybrid Cloud Storage Architecture:**  
  https://docs.aws.amazon.com/whitepapers/latest/hybrid-cloud-with-aws/storage.html

**Công cụ và Calculators:**
* **AWS Pricing Calculator:**  
  https://calculator.aws/

* **S3 Storage Lens:**  
  https://aws.amazon.com/s3/storage-lens/

* **AWS Total Cost of Ownership (TCO) Calculator:**  
  https://aws.amazon.com/tco-calculator/

**Community Resources:**
* **AWS re:Post (Community Forum):**  
  https://repost.aws/

* **AWS Samples GitHub:**  
  https://github.com/aws-samples

* **Reddit - r/aws:**  
  https://www.reddit.com/r/aws/

* **Stack Overflow - AWS Tags:**  
  https://stackoverflow.com/questions/tagged/amazon-web-services

**Best Practices Guides:**
* **S3 Security Best Practices:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html

* **AWS Well-Architected Framework - Storage:**  
  https://docs.aws.amazon.com/wellarchitected/latest/framework/storage.html

* **Data Protection in S3:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/DataDurability.html

* **AWS Backup Best Practices:**  
  https://docs.aws.amazon.com/prescriptive-guidance/latest/backup-recovery/backup.html

**Hands-on Labs và Workshops:**
* **AWS Workshops - Storage:**  
  https://workshops.aws/categories/Storage

* **AWS Hands-on Tutorials:**  
  https://aws.amazon.com/getting-started/hands-on/

* **QwikLabs - AWS Storage:**  
  https://www.qwiklabs.com/catalog?keywords=aws+storage

**Certification Resources:**
* **AWS Certified Solutions Architect - Associate Exam Guide:**  
  https://aws.amazon.com/certification/certified-solutions-architect-associate/

* **AWS Certification Practice Questions:**  
  https://explore.skillbuilder.aws/learn/course/external/view/elearning/13266/aws-certified-solutions-architect-associate-official-practice-question-set

**Additional Resources:**
* **AWS Architecture Center:**  
  https://aws.amazon.com/architecture/

* **AWS Reference Architectures:**  
  https://aws.amazon.com/architecture/reference-architecture-diagrams/

* **AWS Quick Starts:**  
  https://aws.amazon.com/quickstart/

* **AWS Solutions Library:**  
  https://aws.amazon.com/solutions/
