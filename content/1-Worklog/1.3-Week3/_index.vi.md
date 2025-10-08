---
title: "Nhật ký công việc Tuần 3"
date: 2025-09-28
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

* Hiểu khái niệm về **Amazon EC2** như một máy chủ ảo/vật lý trên nền tảng đám mây với khả năng khởi tạo nhanh, co giãn linh hoạt và có thể xử lý nhiều loại workload như web hosting, ứng dụng và cơ sở dữ liệu.  

* Tìm hiểu về **EC2 Instance Types**, cách cấu hình CPU, bộ nhớ, lưu trữ và mạng được định nghĩa, cũng như cách chọn loại phù hợp cho từng workload khác nhau.  

* Khám phá **AMI (Amazon Machine Image)**, **Key Pairs**, và cơ chế sao lưu bằng **Snapshots** để triển khai và quản lý EC2 một cách an toàn.  

* Nắm kiến thức về các tùy chọn lưu trữ trong EC2:  
  - **EBS (Elastic Block Store):** lưu trữ khối bền vững, độ sẵn sàng cao.  
  - **Instance Store:** ổ đĩa NVMe tốc độ cao, dữ liệu tạm thời.  
  - **EFS & FSx:** giải pháp lưu trữ chia sẻ cho môi trường Linux và Windows.  

* Thực hành sử dụng **User Data** và **Metadata** để tự động hóa quá trình khởi tạo instance và lấy thông tin cấu hình của instance.  

* Học cách **EC2 Auto Scaling** hoạt động để tự động thêm hoặc bớt instance dựa trên nhu cầu, tích hợp với Elastic Load Balancer và tối ưu chi phí.  

* Hiểu các mô hình giá của **EC2** (On-Demand, Reserved, Savings Plans, Spot) và trường hợp áp dụng, cùng với các dịch vụ tính toán bổ trợ như **Amazon Lightsail** và **AWS Application Migration Service (MGN)**.  

---

### Nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                           | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------ |
| 1   | - Làm quen với khái niệm **Amazon EC2**: so sánh với máy chủ vật lý, ưu điểm khởi tạo nhanh, khả năng co giãn linh hoạt, workload phù hợp như web hosting, cơ sở dữ liệu, dịch vụ xác thực |  2025/09/22   |  2025/09/22      | <https://000027.awsstudygroup.com/> |
| 2   | - Học về **Instance Types**: cách cấu hình CPU (Intel/AMD/ARM/Graviton/GPU), Bộ nhớ, Mạng, Lưu trữ <br> - Tìm hiểu **AMI** và cách khởi tạo nhiều instance cùng lúc từ một AMI |  2025/09/23   |  2025/09/23      | <https://000008.awsstudygroup.com/> |
| 3   | - Nghiên cứu **EBS (Elastic Block Store)**: lưu trữ khối, replicate trong AZ, snapshot incremental, multi-attach trên Nitro Hypervisor <br> - So sánh EBS với **Instance Store**: hiệu năng cao nhưng mất dữ liệu khi stop instance |  2025/09/24   |  2025/09/24      | <https://000006.awsstudygroup.com/> |
| 4   | - Tìm hiểu **EC2 User Data**: script chạy khi khởi tạo instance, Linux dùng bash, Windows dùng PowerShell <br> - Nghiên cứu **EC2 Metadata**: thông tin IP private, hostname, security group… |  2025/09/25   |  2025/09/26      | <https://000004.awsstudygroup.com/> |
| 5   | - Học về **EC2 Auto Scaling**: scale out khi tải tăng, scale in khi tải giảm để tiết kiệm chi phí <br> - Cách Auto Scaling tích hợp với Elastic Load Balancer và hoạt động trên nhiều AZ |  2025/09/26   |  2025/09/27      | <https://000045.awsstudygroup.com/> |
| 6   | - Nghiên cứu **Các tùy chọn định giá**: On-Demand, Reserved, Savings Plans, Spot Instances và cách kết hợp trong Auto Scaling <br> - Học thêm về **EFS** (hệ thống tệp mạng cho Linux), **FSx** (SMB cho Windows/Linux), và **Lightsail** cho workload nhẹ |  2025/09/27   |  2025/09/28      | <https://000046.awsstudygroup.com/> |


---

### Thành tựu Tuần 3:

* **Hiểu các khái niệm về AWS EC2**:  
  * EC2 tương tự như máy chủ ảo hoặc vật lý nhưng cung cấp khả năng khởi tạo nhanh, co giãn linh hoạt và mở rộng quy mô cao.  
  * EC2 instance được định nghĩa bởi **Instance Types** (CPU, bộ nhớ, lưu trữ, dung lượng mạng) và được tối ưu cho các workload cụ thể như tính toán, bộ nhớ hoặc lưu trữ chuyên sâu.  
  * Học về **AMI** để khởi tạo instance, sao lưu bằng **snapshot**, và truy cập an toàn bằng **Key Pair**.  

* **Khám phá các tùy chọn lưu trữ của EC2**:  
  * **EBS (Elastic Block Store):** lưu trữ khối bền vững, được replicate trong một Availability Zone, snapshot lưu trên S3.  
  * **Instance Store:** bộ nhớ NVMe tốc độ cao, phù hợp cho cache, swap, log; dữ liệu sẽ mất khi dừng instance.  
  * **EFS (Elastic File System):** lưu trữ mạng mở rộng, có thể chia sẻ cho nhiều instance Linux.  
  * **FSx:** hệ thống tệp NTFS quản lý, truy cập qua SMB, hỗ trợ Windows và Linux.  

* **Tìm hiểu về EC2 Auto Scaling:**  
  * Auto Scaling tự động điều chỉnh số lượng instance theo nhu cầu (scale-out khi tải tăng, scale-in để tiết kiệm chi phí khi tải giảm).  
  * Auto Scaling tích hợp với **Elastic Load Balancer (ELB)** và hoạt động trên nhiều Availability Zones.  

* **Khám phá các mô hình giá EC2**:  
  * **On-Demand:** trả theo nhu cầu, linh hoạt nhất nhưng chi phí cao.  
  * **Reserved Instances:** hợp đồng dài hạn (1–3 năm) với mức giảm giá.  
  * **Savings Plans:** linh hoạt hơn, vẫn được giảm giá mà không bị ràng buộc loại instance.  
  * **Spot Instances:** chi phí thấp nhất, tận dụng tài nguyên dư, nhưng có thể bị thu hồi bất kỳ lúc nào.  

* **Kỹ năng thực hành đạt được:**  
  * Tạo và cấu hình tài khoản AWS Free Tier.  
  * Cài đặt và cấu hình AWS CLI (Access Key, Secret Key, Default Region).  
  * Sử dụng AWS CLI để:  
    - Kiểm tra thông tin tài khoản & cấu hình  
    - Lấy danh sách các vùng (regions)  
    - Khởi chạy & giám sát EC2 instances  
    - Quản lý key pairs và EBS volumes  
  * Thực hành kết nối SSH vào EC2 và gắn thêm EBS volumes.  

* **Các dịch vụ khác đã học:**  
  * **Amazon Lightsail:** dịch vụ tính toán đơn giản, chi phí thấp, giá cố định theo tháng.  
  * **AWS Application Migration Service (MGN):** công cụ replicate và di chuyển máy chủ on-premise sang AWS EC2 để phục vụ khôi phục thảm họa và migration.  

---

### Bài học rút ra:

* EC2 là nền tảng cốt lõi của dịch vụ Compute trên AWS, cung cấp sự linh hoạt trong triển khai và mở rộng.  
* Cần hiểu rõ các tùy chọn lưu trữ (EBS, Instance Store, EFS, FSx) để cân bằng giữa chi phí, hiệu năng và tính bền vững.  
* Auto Scaling đảm bảo tính sẵn sàng cao đồng thời tối ưu chi phí.  
* Kết hợp AWS Console (giao diện web) và AWS CLI (dòng lệnh) mang lại khả năng quản trị linh hoạt và tự động hóa mạnh mẽ.  
