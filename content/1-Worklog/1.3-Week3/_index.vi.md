---
title: "Nhật ký công việc Tuần 3"
date: 2025-09-28
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

* Hiểu rõ các khái niệm cơ bản về **Amazon EC2** (Elastic Compute Cloud): Instance Types, AMI, Key Pair, EBS, Instance Store.  
* Nắm vững cách sử dụng **User Data** và **Metadata** để tự động hóa cấu hình EC2 khi khởi tạo.  
* Học cách **EC2 Auto Scaling** hoạt động để tự động thêm hoặc bớt instance dựa trên nhu cầu.  
* Thực hành các Lab về **AWS Backup**, **Storage Gateway**, và **S3 Static Website** với CloudFront.

---

### Nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                           | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------ |
| 1   | - Học Module 03-01: Compute VM on AWS <br>&emsp; + Module 03-01-01: Amazon EC2 - Instance Type <br>&emsp; + Module 03-01-02: Amazon EC2 - AMI / Backup / Key Pair <br>&emsp; + Module 03-01-03: Amazon EC2 - Elastic Block Store <br>&emsp; + Module 03-01-04: Amazon EC2 - Instance Store |  2025/09/22   |  2025/09/22      | https://docs.aws.amazon.com/ec2/ |
| 2   | - Học Module 03-01 (tiếp) <br>&emsp; + Module 03-01-05: Amazon EC2 - User Data <br>&emsp; + Module 03-01-06: Amazon EC2 - Meta Data <br>&emsp; + Module 03-01-07: Amazon EC2 - EC2 Auto Scaling <br> - Học Module 03-02: EC2 Autoscaling - EFS/FSx - Lightsail - MGN |  2025/09/23   |  2025/09/23      | https://docs.aws.amazon.com/autoscaling/ |
| 3   | - **Lab 13 - Phần 1:** Deploy AWS Backup <br>&emsp; + Module 03-Lab13-01: Introduction <br>&emsp; + Module 03-Lab13-02.2: Deploy Infrastructure <br>&emsp; + Module 03-Lab13-03: Create Backup Plan |  2025/09/24   |  2025/09/24      | https://000013.awsstudygroup.com/ |
| 4   | - **Lab 13 - Phần 2:** Test và Clean up <br>&emsp; + Module 03-Lab13-05: Test Restore <br>&emsp; + Module 03-Lab13-06: Clean up resources <br> - **Lab 24 - Phần 1:** Storage Gateway <br>&emsp; + Module 03-Lab24-01.1: Create S3 Bucket <br>&emsp; + Module 03-Lab24-01.2: Create EC2 for Storage Gateway |  2025/09/25   |  2025/09/25      | https://000024.awsstudygroup.com/ |
| 5   | - **Lab 24 - Phần 2:** Configure Storage Gateway <br>&emsp; + Module 03-Lab24-02.1: Create Storage Gateway <br>&emsp; + Module 03-Lab24-02.2: Create File Shares <br> - **Lab 57 - Phần 1:** S3 Static Website <br>&emsp; + Module 03-Lab57-02.1: Create S3 Bucket <br>&emsp; + Module 03-Lab57-02.2: Load Data <br>&emsp; + Module 03-Lab57-03: Enable Static Website Feature |  2025/09/26   |  2025/09/26      | https://000057.awsstudygroup.com/ |
| 6   | - **Lab 57 - Phần 2:** Public Access và CloudFront <br>&emsp; + Module 03-Lab57-04: Configuring Public Access Block <br>&emsp; + Module 03-Lab57-05: Configuring Public Objects <br>&emsp; + Module 03-Lab57-06: Test Website <br>&emsp; + Module 03-Lab57-07.1: Block All Public Access <br>&emsp; + Module 03-Lab57-07.2: Config Amazon CloudFront <br>&emsp; + Module 03-Lab57-07.3: Test Amazon CloudFront |  2025/09/27   |  2025/09/27      | https://000057.awsstudygroup.com/ |
| 7   | - **Lab 57 - Phần 3:** Versioning và Replication <br>&emsp; + Module 03-Lab57-08: Bucket Versioning <br>&emsp; + Module 03-Lab57-09: Move Objects <br>&emsp; + Module 03-Lab57-10: Replication Object Multi Region <br>&emsp; + Module 03-Lab57-11: Clean up Resources <br> - Viết báo cáo tuần và ôn tập toàn bộ nội dung đã học |  2025/09/28   |  2025/09/28      | https://000057.awsstudygroup.com/ |


---

### Kết quả đạt được trong Tuần 3:

* **Hiểu các khái niệm về AWS EC2**:  
  * EC2 Instance Types và cách chọn loại phù hợp với workload.
  * AMI để khởi tạo instance, Backup/Snapshot để sao lưu, Key Pair để truy cập an toàn.
  * EBS (lưu trữ khối bền vững) và Instance Store (lưu trữ tạm thời hiệu năng cao).
  * User Data để tự động chạy script khi khởi tạo, Metadata để lấy thông tin instance.
  * EC2 Auto Scaling để tự động điều chỉnh số lượng instance theo nhu cầu.

* **Khám phá các dịch vụ lưu trữ và tính toán bổ sung**:  
  * EFS (Elastic File System) cho Linux, FSx cho Windows.
  * Amazon Lightsail cho workload đơn giản với giá cố định.
  * AWS MGN (Application Migration Service) để di chuyển máy chủ on-premise lên AWS.

* **Kỹ năng thực hành đạt được**:  
  * **Lab 13 - AWS Backup:** Triển khai hạ tầng, tạo Backup Plan cho EC2 và EBS, test khôi phục dữ liệu từ backup.
  * **Lab 24 - Storage Gateway:** Tạo S3 Bucket, triển khai EC2 cho Storage Gateway, cấu hình Storage Gateway và File Shares để kết nối lưu trữ on-premise với AWS.
  * **Lab 57 - S3 Static Website:** Tạo S3 Bucket, upload dữ liệu, bật tính năng Static Website, cấu hình public access, tích hợp CloudFront để tăng tốc độ phân phối, bật Versioning và Replication multi-region.

---

### Tóm tắt Tuần 3:

Tuần này tập trung vào các kiến thức cơ bản về AWS EC2 compute và các giải pháp lưu trữ. Bắt đầu với việc tìm hiểu EC2 Instance Types, AMI, Key Pairs, và các tùy chọn lưu trữ như EBS và Instance Store. Học về User Data để tự động hóa cấu hình instance và Metadata để lấy thông tin instance.

Nghiên cứu EC2 Auto Scaling để tự động điều chỉnh dung lượng dựa trên nhu cầu, giúp tối ưu chi phí và đảm bảo tính sẵn sàng cao. Khám phá các dịch vụ bổ sung như EFS, FSx, Lightsail, và MGN.

Kinh nghiệm thực hành chính bao gồm triển khai AWS Backup để tự động sao lưu và khôi phục tài nguyên EC2/EBS (Lab 13), cấu hình Storage Gateway để kết nối lưu trữ hybrid giữa on-premises và S3 (Lab 24), và tạo S3 Static Website với CloudFront distribution, versioning, và multi-region replication (Lab 57).

Tuần học này cung cấp kiến thức thiết yếu về các dịch vụ compute và storage của AWS, chuẩn bị cho việc xây dựng các ứng dụng cloud có khả năng mở rộng, bền vững và tiết kiệm chi phí.

---

### Tài liệu tham khảo:

**Bài Lab Workshop:**
* **Lab 13 - Deploy AWS Backup:**  
  https://000013.awsstudygroup.com/

* **Lab 24 - Storage Gateway:**  
  https://000024.awsstudygroup.com/

* **Lab 57 - S3 Static Website với CloudFront:**  
  https://000057.awsstudygroup.com/

**Tài liệu chính thức AWS:**
* **Hướng dẫn sử dụng Amazon EC2:**  
  https://docs.aws.amazon.com/ec2/

* **Các loại EC2 Instance:**  
  https://aws.amazon.com/ec2/instance-types/

* **Tài liệu Amazon EBS:**  
  https://docs.aws.amazon.com/ebs/

* **EC2 Auto Scaling:**  
  https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html

* **AWS Backup:**  
  https://docs.aws.amazon.com/aws-backup/

* **AWS Storage Gateway:**  
  https://docs.aws.amazon.com/storagegateway/

* **Amazon S3 Static Website Hosting:**  
  https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html

* **Amazon CloudFront:**  
  https://docs.aws.amazon.com/cloudfront/

* **Amazon EFS:**  
  https://docs.aws.amazon.com/efs/

* **Amazon FSx:**  
  https://docs.aws.amazon.com/fsx/

**Video hướng dẫn:**
* **Hướng dẫn AWS EC2 đầy đủ:**  
  https://www.youtube.com/watch?v=iHX-jtKIVNA

* **Giải thích EC2 Auto Scaling:**  
  https://www.youtube.com/watch?v=4EOaAkY4pNE

* **Tổng quan dịch vụ AWS Storage:**  
  https://www.youtube.com/watch?v=6vNC_BCqFmI

* **S3 Static Website với CloudFront:**  
  https://www.youtube.com/watch?v=mls8tiiI3uc

**Tài nguyên bổ sung:**
* **Công cụ tính giá EC2:**  
  https://calculator.aws/

* **AWS Well-Architected Framework:**  
  https://aws.amazon.com/architecture/well-architected/

* **AWS Skill Builder - Khóa học EC2:**  
  https://explore.skillbuilder.aws/learn

* **Best Practices cho EC2:**  
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html
