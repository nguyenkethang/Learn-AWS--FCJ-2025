---
title: "Nhật ký công việc Tuần 4"
date: 2025-10-05
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4:
* Nắm vững các dịch vụ lưu trữ chính trên AWS bao gồm **Amazon S3**, **Glacier**, **Snow Family**, **Storage Gateway** và **AWS Backup**.  
* Hiểu rõ các khái niệm về **RTO/RPO** và các chiến lược **khôi phục thảm họa (Disaster Recovery)** trên AWS.  

---

### Nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | -------- | ------------- | ---------------- | ------------------ |
| 1 | - Tìm hiểu tổng quan về Amazon Simple Storage Service (S3) <br>&emsp; + Khái niệm lưu trữ đối tượng (Object Storage) <br>&emsp; + Bucket và Object <br>&emsp; + Dung lượng, độ bền và độ sẵn sàng dữ liệu <br>&emsp; + Multipart Upload, Trigger Event, REST API | 2025/09/29 | 2025/09/29 | [Amazon Simple Storage Service ( S3 )](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=104) |
| 2 | - Nghiên cứu các lớp lưu trữ (Storage Class) trong S3: <br>&emsp; + Standard, Standard-IA, Intelligent Tiering, One Zone-IA, Glacier / Deep Archive <br>&emsp; + Cấu hình Object Lifecycle Management để tự động di chuyển dữ liệu | 2025/09/30 | 2025/09/30 | [Amazon Simple Storage Service ( S3 )](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=104) |
| 3 | - Học về quyền truy cập trong S3: <br>&emsp; + Access Control List (ACL) <br>&emsp; + Bucket Policy & IAM Policy <br>&emsp; + S3 Access Point <br>&emsp; + Endpoint & Versioning | 2025/10/01 | 2025/10/01 | [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) |
| 4 | - Tìm hiểu tính năng Static Website Hosting và CORS trên S3 <br>&emsp; + Cơ chế Cross-Origin Resource Sharing (CORS) <br>&emsp; + Cấu hình chính sách CORS cho phép truy cập từ domain khác | 2025/10/02 | 2025/10/02 | [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) |
| 5 | - Nghiên cứu S3 Glacier và các phương thức truy xuất dữ liệu: Expedited, Standard, Bulk <br> - Học về hiệu suất và Object Key trong S3: phân vùng (Partition) và prefix tối ưu hiệu năng | 2025/10/03 | 2025/10/03 | [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cors.html) |
| 6 | - Tìm hiểu AWS Snow Family: <br>&emsp; + Snowball (80TB) <br>&emsp; + Snowball Edge (100TB, có compute) <br>&emsp; + Snowmobile (100PB) <br> - Nghiên cứu AWS Storage Gateway và các loại File / Volume / Tape Gateway <br> - Tìm hiểu AWS Backup và Disaster Recovery: khái niệm RTO, RPO, 4 chiến lược phục hồi sau thảm họa | 2025/10/04 | 2025/10/05 | [AWS Snow Family Video](http://youtube.com/watch?v=YXn8Q_Hpsu4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=106) |

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

Tuần này em đã hoàn thành việc học và thực hành các dịch vụ lưu trữ trên AWS bao gồm Amazon S3, Glacier, Snow Family, Storage Gateway và AWS Backup.  
Qua đó, em hiểu rõ cách phân loại dữ liệu theo nhu cầu truy cập, cấu hình phân quyền, triển khai backup và thiết lập chính sách phục hồi thảm họa hiệu quả.  
Đặc biệt, em đã nắm được cơ chế hoạt động của Object Storage, CORS, Versioning và Lifecycle trong S3, giúp quản lý dữ liệu linh hoạt và tiết kiệm chi phí.
