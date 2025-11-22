---
title: "Nhật ký công việc Tuần 2"
date: 2025-09-21
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2:

* Nắm vững các dịch vụ cơ bản của AWS và cách sử dụng AWS Console & CLI.
* Thực hành triển khai EC2, kết nối SSH, gán EBS.
* Tìm hiểu kiến trúc mạng VPC, VPN, Peering, và Transit Gateway.


### Nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                               | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo     |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|-------------------------|
| 1    | - Tìm hiểu các dịch vụ AWS: <br>&emsp; + Tính toán (Compute), Lưu trữ (Storage), Mạng (Networking), Cơ sở dữ liệu (Database) <br> - Tìm hiểu kiến trúc VPC, Mạng con (Subnet), Bảng định tuyến (Route Table), Cổng Internet (Internet Gateway), Cổng NAT (NAT Gateway) |  2025/09/15   |  2025/09/15      | https://000003.awsstudygroup.com/ |
| 2    | - **Thực hành:** <br>&emsp; + Tạo khóa truy cập (Access Key) <br>&emsp; + Cấu hình giao diện dòng lệnh (CLI) <br>&emsp; + Kiểm tra thông tin cấu hình                                                                                 |  2025/09/16   |  2025/09/16      | https://000003.awsstudygroup.com/ |
| 3    | - Tìm hiểu EC2: Loại máy ảo (Instance Types), Ảnh máy ảo (AMI), Ổ lưu trữ (EBS) <br> - Kết nối SSH vào EC2 <br> - Gán địa chỉ IP tĩnh (Elastic IP) <br> - Tìm hiểu Nhóm bảo mật (Security Group), Danh sách kiểm soát truy cập mạng (NACL), Nhật ký lưu lượng VPC (VPC Flow Logs) |  2025/09/17   |  2025/09/17      | https://000019.awsstudygroup.com/ |
| 4    | - **Thực hành:** <br>&emsp; + Khởi tạo máy ảo EC2 <br>&emsp; + Kết nối SSH <br>&emsp; + Gắn thêm ổ EBS <br> - Tìm hiểu về kết nối ngang hàng giữa các VPC (VPC Peering) và cấu hình kết nối giữa 2 VPC                                     |  2025/09/18   |  2025/09/18      | https://000019.awsstudygroup.com/ |
| 5    | - Tìm hiểu AWS Transit Gateway (Cổng trung chuyển) <br> - So sánh VPC Peering và Transit Gateway <br> - Cấu hình Transit Gateway và kết nối (Attachment) giữa nhiều VPC                                                                 |  2025/09/19   |  2025/09/19      | https://000020.awsstudygroup.com/ |
| 6    | - Ôn tập toàn bộ nội dung đã học <br> - Tổng hợp kiến thức và chuẩn bị cho tuần tiếp theo                                                                                                                                                |  2025/09/20   |  2025/09/20      |                         |
| 7    | - Thực hành kiểm tra trên CLI và giao diện quản lý (Console) <br> - Viết báo cáo tuần <br> - Đánh giá lại tiến độ học tập                                                                                                               |  2025/09/21   |  2025/09/21      |                         |


### Kết quả đạt được trong Tuần 2:

* Hiểu rõ kiến trúc mạng AWS VPC: CIDR, Subnet, Route Table, Internet Gateway, NAT Gateway.
* Cấu hình thành công AWS CLI và thực hiện các lệnh cơ bản như:
  * `aws configure`
  * `aws ec2 describe-instances`
  * `aws ec2 describe-regions`
* Khởi tạo EC2 instance, kết nối SSH, gán EBS volume.
* Áp dụng Security Group và NACL để kiểm soát truy cập.
* Kích hoạt VPC Flow Logs để giám sát lưu lượng mạng.
* Thiết lập VPC Peering giữa hai VPC và cấu hình Route Table để cho phép giao tiếp.
* Tìm hiểu và cấu hình AWS Transit Gateway để kết nối nhiều VPC một cách tập trung và hiệu quả.
* Tổng hợp kiến thức và hoàn thành báo cáo tuần đúng tiến độ.
