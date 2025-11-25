---
title: "Nhật ký công việc Tuần 2"
date: 2025-09-21
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2:

* Hiểu rõ các khái niệm cơ bản về AWS VPC và tính năng bảo mật.
* Thực hành tạo VPC, Subnet, Route Table, và Internet Gateway.
* Tìm hiểu VPN Site-to-Site, Security Group, và Network ACL.
* Thực hành cấu hình VPC Peering và Transit Gateway.


### Nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                               | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo     |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|-------------------------|
| 1    | - Học Module 02-01: AWS Virtual Private Cloud <br> - Học Module 02-02: VPC Security và tính năng Multi-VPC <br> - Học Module 02-03: VPN - DirectConnect - LoadBalancer - ExtraResources                                               |  2025/09/15   |  2025/09/15      | Lab 03, Lab 10, Lab 19, Lab 20 |
| 2    | - **Lab 03 - Phần 1:** Bắt đầu với Amazon VPC và AWS VPN Site-to-Site <br>&emsp; + Module 02-Lab03-01: Giới thiệu <br>&emsp; + Module 02-Lab03-01.1: Tạo Subnet <br>&emsp; + Module 02-Lab03-01.2: Cấu hình Route Table <br>&emsp; + Module 02-Lab03-01.3: Thiết lập Internet Gateway (IGW) <br>&emsp; + Module 02-Lab03-01.4: Tạo NAT Gateway |  2025/09/16   |  2025/09/16      | https://000003.awsstudygroup.com/ |
| 3    | - **Lab 03 - Phần 2:** Bảo mật VPC và Tạo tài nguyên <br>&emsp; + Module 02-Lab03-02.1: Cấu hình Security Group <br>&emsp; + Module 02-Lab03-02.2: Thiết lập Network ACL <br>&emsp; + Module 02-Lab03-02.3: Xem lại VPC Resource Map <br>&emsp; + Module 02-Lab03-03.1: Tạo VPC <br>&emsp; + Module 02-Lab03-03.2: Tạo Subnet |  2025/09/17   |  2025/09/17      | https://000003.awsstudygroup.com/ |
| 4    | - **Lab 03 - Phần 3:** Hoàn thiện VPC và Triển khai EC2 <br>&emsp; + Module 02-Lab03-03.3: Tạo Internet Gateway <br>&emsp; + Module 02-Lab03-03.4: Tạo Route Table cho định tuyến Internet <br>&emsp; + Module 02-Lab03-03.5: Tạo Security Group <br>&emsp; + Module 02-Lab03-04.1: Tạo EC2 Instance trong Subnet <br>&emsp; + Module 02-Lab03-04.2: Kiểm tra kết nối <br>&emsp; + Module 02-Lab03-04.3: Tạo NAT Gateway <br>&emsp; + Module 02-Lab03-04.5: EC2 Instance Connect Endpoint |  2025/09/18   |  2025/09/18      | https://000003.awsstudygroup.com/ |
| 5    | - **Lab 10:** Thiết lập Hybrid DNS với Route 53 Resolver <br>&emsp; + Module 02-Lab10-01: Giới thiệu <br>&emsp; + Module 02-Lab10-02.1: Tạo Key Pair <br>&emsp; + Module 02-Lab10-02.2: Khởi tạo CloudFormation Template <br>&emsp; + Module 02-Lab10-02.3: Cấu hình Security Group <br>&emsp; + Module 02-Lab10-03: Kết nối tới RDGW <br>&emsp; + Module 02-Lab10-05: Thiết lập DNS <br>&emsp; + Module 02-Lab10-05.1: Tạo Route 53 Outbound Endpoint <br>&emsp; + Module 02-Lab10-05.2: Tạo Route 53 Resolver Rule <br>&emsp; + Module 02-Lab10-05.3: Tạo Route 53 Inbound Endpoint <br>&emsp; + Module 02-Lab10-05.4: Kiểm tra kết quả <br>&emsp; + Module 02-Lab10-06: Dọn dẹp tài nguyên |  2025/09/19   |  2025/09/19      | https://000010.awsstudygroup.com/ |
| 6    | - **Lab 19:** Thiết lập VPC Peering <br>&emsp; + Module 02-Lab19-01: Giới thiệu <br>&emsp; + Module 02-Lab19-02.1: Khởi tạo CloudFormation Template <br>&emsp; + Module 02-Lab19-02.2: Tạo Security Group <br>&emsp; + Module 02-Lab19-02.3: Tạo EC2 instance <br>&emsp; + Module 02-Lab19-03: Cập nhật Network ACL (NACL) <br>&emsp; + Module 02-Lab19-04: Tạo Peering Connection <br>&emsp; + Module 02-Lab19-05: Cấu hình Route Table <br>&emsp; + Module 02-Lab19-06: Bật Cross-Peer DNS <br>&emsp; + Module 02-Lab19-07: Dọn dẹp tài nguyên |  2025/09/20   |  2025/09/20      | https://000019.awsstudygroup.com/ |
| 7    | - **Lab 20:** Thiết lập AWS Transit Gateway <br>&emsp; + Module 02-Lab20-01: Giới thiệu <br>&emsp; + Module 02-Lab20-02: Các bước chuẩn bị <br>&emsp; + Module 02-Lab20-03: Tạo Transit Gateway <br>&emsp; + Module 02-Lab20-04: Tạo Transit Gateway Attachment <br>&emsp; + Module 02-Lab20-05: Tạo Transit Gateway Route Table <br>&emsp; + Module 02-Lab20-06: Thêm Transit Gateway Route vào VPC Route Table <br>&emsp; + Module 02-Lab20-07: Dọn dẹp tài nguyên <br> - Viết báo cáo tuần và ôn tập toàn bộ nội dung đã học |  2025/09/21   |  2025/09/21      | https://000020.awsstudygroup.com/ |


### Kết quả đạt được trong Tuần 2:

* Hiểu toàn diện về kiến trúc AWS VPC và các tính năng bảo mật.
* Tạo thành công VPC với CIDR block tùy chỉnh, Subnet, Route Table, Internet Gateway, và NAT Gateway.
* Cấu hình Security Group và Network ACL để kiểm soát lưu lượng vào và ra.
* Triển khai EC2 instance trong các subnet khác nhau và kiểm tra kết nối.
* Thiết lập EC2 Instance Connect Endpoint để truy cập SSH an toàn.
* Triển khai giải pháp Hybrid DNS sử dụng Route 53 Resolver với Inbound và Outbound Endpoint.
* Cấu hình thành công VPC Peering giữa hai VPC với định tuyến và phân giải DNS phù hợp.
* Triển khai AWS Transit Gateway để kết nối nhiều VPC theo kiến trúc hub-and-spoke.
* Hoàn thành tất cả các bài lab thực hành và củng cố kiến thức về mạng.


### Tóm tắt Tuần 2:

Tuần này tập trung vào các kiến thức cơ bản về mạng AWS VPC và các mô hình kết nối nâng cao. Bắt đầu với việc hiểu kiến trúc VPC bao gồm Subnet, Route Table, Internet Gateway, và NAT Gateway thông qua Lab 03. Học cách bảo mật tài nguyên VPC bằng Security Group và Network ACL để kiểm soát luồng traffic.

Tiến tới các chủ đề nâng cao hơn bao gồm phân giải DNS lai (Hybrid DNS) với Route 53 Resolver (Lab 10), cho phép truy vấn DNS liền mạch giữa môi trường on-premises và AWS. Khám phá các tùy chọn kết nối VPC thông qua VPC Peering (Lab 19) để giao tiếp trực tiếp giữa hai VPC, và AWS Transit Gateway (Lab 20) cho kiến trúc multi-VPC có khả năng mở rộng.

Kinh nghiệm thực hành chính bao gồm triển khai EC2 instance trên các subnet khác nhau, cấu hình bảng định tuyến để luồng traffic hoạt động đúng, thiết lập CloudFormation template để tự động hóa hạ tầng, và triển khai EC2 Instance Connect Endpoint để truy cập an toàn. Tất cả các lab đều kết thúc bằng việc dọn dẹp tài nguyên đúng cách theo best practice của AWS.

Tuần học này cung cấp nền tảng vững chắc về mạng AWS, chuẩn bị cho các kiến trúc cloud phức tạp hơn và các kịch bản hybrid cloud.


### Tài liệu tham khảo:

**Bài Lab Workshop:**
* **Lab 03 - Bắt đầu với Amazon VPC và AWS VPN Site-to-Site:**  
  https://000003.awsstudygroup.com/

* **Lab 10 - Thiết lập Hybrid DNS với Route 53 Resolver:**  
  https://000010.awsstudygroup.com/

* **Lab 19 - Thiết lập VPC Peering:**  
  https://000019.awsstudygroup.com/

* **Lab 20 - Thiết lập AWS Transit Gateway:**  
  https://000020.awsstudygroup.com/

**Tài liệu chính thức AWS:**
* **Hướng dẫn sử dụng Amazon VPC:**  
  https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html

* **VPC Security Groups:**  
  https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html

* **Network ACLs:**  
  https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html

* **Route 53 Resolver:**  
  https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html

* **Hướng dẫn VPC Peering:**  
  https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html

* **AWS Transit Gateway:**  
  https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html

**Video hướng dẫn:**
* **AWS VPC từ cơ bản đến nâng cao:**  
  https://www.youtube.com/watch?v=fpxDGU2KdkA

* **AWS Networking Fundamentals:**  
  https://www.youtube.com/watch?v=hiKPPy584Mg

* **So sánh VPC Peering và Transit Gateway:**  
  https://www.youtube.com/watch?v=ar6sLmJ45xs

**Tài nguyên bổ sung:**
* **AWS Networking Best Practices:**  
  https://aws.amazon.com/architecture/well-architected/

* **Công cụ tính toán VPC CIDR:**  
  https://www.ipaddressguide.com/cidr

* **AWS Skill Builder - Khóa học VPC:**  
  https://explore.skillbuilder.aws/learn
