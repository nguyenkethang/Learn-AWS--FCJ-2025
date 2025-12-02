---
title: "Sự kiện 5"
date: 2025-11-29
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

## 🔐 WORKSHOP AWS WELL-ARCHITECTED SECURITY PILLAR – BUỔI SÁNG

### 📍 Địa điểm & Thời gian
- **Ngày:** 29/11/2025 (Chỉ buổi sáng)  
- **Thời gian:** 08:30 Sáng – 12:00 Trưa  
- **Địa điểm:** Tầng 26, Tòa nhà Bitexco Financial Tower, 2 Hải Triều, Phường Bến Nghé, Quận 1, TP. Hồ Chí Minh

---

### 🎯 Mục tiêu Workshop
- Tìm hiểu sâu về AWS Well-Architected Framework – Security Pillar
- Khám phá các best practices để bảo mật hạ tầng cloud qua năm lĩnh vực chính
- Học hỏi từ các tình huống thực tế và những lỗi phổ biến trong môi trường doanh nghiệp Việt Nam
- Khám phá lộ trình học tập và chứng chỉ bảo mật AWS

---

## 🛡️ Nội dung các phiên

### 🔹 8:30 – 8:50 | Khai mạc & Nền tảng bảo mật
- Vai trò của Security Pillar trong Well-Architected Framework  
- Các nguyên tắc cốt lõi: Least Privilege – Zero Trust – Defense in Depth  
- Mô hình Shared Responsibility  
- Các mối đe dọa cloud hàng đầu tại Việt Nam

---

### ⭐ Trụ cột 1 — Quản lý định danh & truy cập (IAM)
**🕗 8:50 – 9:30 | Kiến trúc IAM hiện đại**

**Diễn giả:**
- **Lê Vũ Xuân An** - AWS Cloud Club Captain HCMUTE, First Cloud AI Journey
- **Trần Đức Anh** - AWS Cloud Club Captain SGU, First Cloud AI Journey
- **Trần Đoàn Công Lý** - AWS Cloud Club Captain PTIT, First Cloud AI Journey
- **Danh Hoàng Hiếu Nghi** - AWS Cloud Club Captain HUFLIT, First Cloud AI Journey

**Nội dung:**
- IAM: Users, Roles, Policies – tránh credentials dài hạn  
- IAM Identity Center: SSO, permission sets  
- SCP & permission boundaries cho multi-account  
- MFA, xoay vòng credentials, Access Analyzer  
- Mini Demo: Validate IAM Policy + mô phỏng truy cập

---

### ⭐ Trụ cột 2 — Phát hiện
**🕘 9:30 – 9:55 | Phát hiện & Giám sát liên tục**

**Diễn giả:**
- **Huỳnh Hoàng Long** - AWS Community Builders
- **Đinh Lê Hoàng Anh** - AWS Community Builders

**Nội dung:**
- CloudTrail (org-level), GuardDuty, Security Hub  
- Logging ở mọi tầng: VPC Flow Logs, ALB/S3 logs  
- Cảnh báo & tự động hóa với EventBridge  
- Detection-as-Code (infrastructure + rules)

---

### ☕ 9:55 – 10:10 | Giải lao

---

### ⭐ Trụ cột 3 — Bảo vệ hạ tầng
**🕙 10:10 – 10:40 | Bảo mật mạng & Workload**

**Diễn giả:**
- **Trần Đức Anh** - AWS Cloud Club Captain SGU, Cloud Security Engineer Trainee, First Cloud AI Journey
- **Nguyễn Tuấn Thịnh** - Cloud Engineer Trainee, First Cloud AI Journey
- **Nguyễn Đỗ Thanh Đạt** - Cloud Engineer Trainee, First Cloud AI Journey

**Nội dung:**
- Phân đoạn VPC, private vs public placement  
- Security Groups vs NACLs: các mô hình ứng dụng  
- WAF + Shield + Network Firewall  
- Bảo vệ workload: EC2, ECS/EKS security cơ bản

---

### ⭐ Trụ cột 4 — Bảo vệ dữ liệu
**🕥 10:40 – 11:10 | Mã hóa, Keys & Secrets**

**Diễn giả:**
- **Thịnh Lâm** - FCJer
- **Việt Nguyễn** - FCJer

**Nội dung:**
- KMS: key policies, grants, rotation  
- Mã hóa at-rest & in-transit: S3, EBS, RDS, DynamoDB  
- Secrets Manager & Parameter Store — các mẫu rotation  
- Phân loại dữ liệu & access guardrails

---

### ⭐ Trụ cột 5 — Ứng phó sự cố
**🕚 11:10 – 11:40 | IR Playbook & Tự động hóa**

**Diễn giả:**
- **Mendel Grabski** - Secure by Design | Azure | Blockchain | Data Security

**Nội dung:**
- Vòng đời IR với AWS  
- Các kịch bản playbook:
  - IAM key bị xâm phạm  
  - S3 bị public  
  - Phát hiện malware trên EC2  
- Snapshot, cô lập, thu thập bằng chứng  
- Tự động phản hồi với Lambda/Step Functions

---

### 🔚 11:40 – 12:00 | Tổng kết & Hỏi đáp
- Tóm tắt 5 trụ cột  
- Các lỗi phổ biến & thực tế doanh nghiệp tại Việt Nam  
- Lộ trình học tập bảo mật (Security Specialty, SA Pro)

---

## 💡 Những điều rút ra
- Hiểu sâu hơn về kiến trúc bảo mật AWS và các best practices vận hành
- Học cách áp dụng chiến lược phòng thủ nhiều lớp và tự động hóa phát hiện & phản hồi
- Có cái nhìn sâu sắc về IAM, logging, mã hóa và ứng phó sự cố trong môi trường cloud thực tế
- Khám phá các công cụ và dịch vụ thực tế để bảo mật workloads và dữ liệu trên AWS
- Làm rõ lộ trình học tập và chứng chỉ để phát triển trong lĩnh vực bảo mật cloud

---

## 🧱 Bảo mật DNS & Network nâng cao

### 🛡️ Route 53 Resolver DNS Firewall

#### Tính năng chính
- **Chặn truy cập domain độc hại**: Dựa trên danh sách deny/allow để ngăn truy cập đến các domain nguy hiểm
- **Bảo vệ DNS queries**: Kiểm soát lưu lượng DNS từ VPC, ngăn DNS tunneling và exfiltration
- **Tích hợp Security Hub**: Gửi cảnh báo khi phát hiện truy cập bất thường

#### Kiến thức cần nắm
DNS queries từ instances được gửi đến resolver (VPC CIDR + 2 hoặc 169.254.169.253).

Resolver phân loại queries:
- **Private DNS**: Truy vấn nội bộ trong hosted zone
- **VPC DNS**: Truy vấn đến tài nguyên AWS (ví dụ: EC2)
- **Public DNS**: Truy vấn ra internet

---

### 🔥 AWS Network Firewall

#### Các use cases chính

**1. Egress Filtering**
- Chặn truy cập ra ngoài đến domain xấu (FQDN, ccTLDs, TLS fingerprint)
- Kiểm tra port/protocol hợp lệ
- Ngăn giao tiếp trực tiếp đến IP đáng ngờ

**2. Environment Segmentation**
- Tách biệt traffic giữa VPCs và môi trường dev/prod
- Kiểm soát kết nối giữa on-premises và cloud

**3. Intrusion Prevention**
- Dùng rules từ AWS hoặc bên thứ ba để phát hiện và chặn tấn công
- Tự động block IP brute force từ GuardDuty

---

### 🌐 Mô hình triển khai DNS Resolver

#### 🏢 Hybrid Network Deployment
- Kết nối mạng doanh nghiệp với AWS qua Direct Connect
- Luồng DNS query: client → DNS resolver → AWS Route 53 resolver
- Hỗ trợ Private DNS, Amazon Domains, và Public DNS
- Dùng inbound endpoint để nhận queries từ on-premises

#### ☁️ Cloud-Only Deployment
- Toàn bộ hệ thống nằm trong AWS Cloud
- Mỗi Availability Zone có resolver riêng
- DNS Firewall kiểm soát DNS queries từ instances
- Hỗ trợ phân giải domain nội bộ và công khai

---

### 🧩 Centralized Alerting & Normalization
- Security Hub CSPM chuẩn hóa dữ liệu từ GuardDuty, Inspector, v.v. theo định dạng ASFF (AWS Security Finding Format)
- Đơn giản hóa phân tích và lọc dữ liệu
- Hỗ trợ quản lý tập trung nhiều accounts và regions

---

## 🧠 Phát hiện nâng cao & Tự động hóa thực chiến

### 🔍 GuardDuty – Ba trụ cột phát hiện

| **Nguồn dữ liệu**     | **Giám sát điều gì**                          | **Tình huống thực tế**                                  |
|-----------------------|-----------------------------------------------|--------------------------------------------------------|
| CloudTrail Events     | Hành động IAM, thay đổi quyền, API calls      | Hacker tắt logging để che giấu dấu vết                 |
| VPC Flow Logs         | Lưu lượng mạng đến/đi từ tài nguyên           | EC2 gửi dữ liệu đến server C&C của botnet              |
| DNS Logs              | Truy vấn DNS từ hạ tầng                       | Instance nhiễm malware truy vấn pool đào tiền ảo        |

---

### 🛠️ Runtime Monitoring – "Mắt thần" trong hệ điều hành

**GuardDuty Agent**: Phần mềm nhẹ cài trên EC2/EKS/ECS Fargate

**Giám sát sâu:**
- Quá trình nào đang chạy, ai khởi tạo
- Truy cập file: ai, lúc nào, file nào
- System calls & thay đổi quyền
- Phát hiện reverse shell, leo thang đặc quyền

---

### ⚡ EventBridge – Tự động hóa phản hồi bảo mật

#### 🔔 Real-time Findings
- GuardDuty phát hiện mối đe dọa → gửi findings ngay lập tức đến EventBridge

#### 🤖 Automated Remediation
Lambda tự động:
- Cô lập EC2 instances bị nhiễm
- Thu hồi IAM credentials
- Lưu bằng chứng (snapshots, logs)

#### 🔄 Cross-account Routing
- Tài khoản bảo mật trung tâm nhận findings từ tất cả member accounts

#### 🔗 Integration & Workflows
- Tích hợp với SNS, Slack, SQS để cảnh báo nhóm bảo mật

---

### 🧱 Detection-as-Code – Tích hợp DevSecOps

- **IaC với CloudFormation/Terraform**: Triển khai GuardDuty toàn tổ chức
- **Custom Detection Rules**: Suppression rules, IP whitelisting để giảm false positives
- **Version-Controlled Logic**: Lưu rules trong Git, tích hợp CI/CD để test & deploy
- **Protection Plan Rollout**: Tự động hóa kích hoạt các lớp bảo vệ như S3/EKS

---

### 🛡️ AWS Security Hub CSPM – Quản lý tư thế bảo mật

#### Tính năng chính
- **Automated Checks**: Tự động kiểm tra toàn bộ môi trường AWS
- **Consolidated Findings**: Tổng hợp findings từ GuardDuty, Inspector, Macie, v.v.
- **Prioritized Alerts**: Phân loại cảnh báo theo mức độ nghiêm trọng
- **EventBridge Integration**: Gửi findings đến hệ thống ticket/chat/email hoặc tự động hóa xử lý

---

### 🔐 Advanced Protection Plans

| **Tính năng**               | **Chi tiết**                                                                 |
|-----------------------------|------------------------------------------------------------------------------|
| S3 Protection               | Phát hiện truy cập bất thường, quét malware khi upload                       |
| EKS Protection              | Giám sát audit log Kubernetes, tích hợp S3 để phân tích đường tấn công       |
| Extended Threat Detection   | Ghép các sự kiện rời rạc thành chuỗi tấn công có logic                      |

---

## 🧱 Incident Controls – Nền tảng bảo mật chủ động

### 🔐 Các thành phần cốt lõi

#### AWS Organizations + SCPs
- Thiết lập guardrails toàn tổ chức
- Ngăn hành vi vượt quyền từ IAM policies

#### CloudTrail
- Ghi log toàn bộ API calls
- Bật ở tất cả các vùng để không bỏ sót sự kiện

#### AWS Config
- Giám sát tuân thủ liên tục
- Phát hiện drift so với cấu hình chuẩn

#### GuardDuty
- Phát hiện mối đe dọa bằng ML
- Một cú click là kích hoạt toàn tổ chức

#### Security Hub
- Tổng hợp cảnh báo từ nhiều dịch vụ bảo mật
- Chuẩn hóa theo tiêu chuẩn CIS, PCI DSS, v.v.

---

## 🛡️ Prevention – Không ai có thời gian cho sự cố!

### 🔥 5 nguyên tắc vàng

**1. Kill long-lived credentials**
- Dùng OIDC, IAM roles, temporary tokens
- Secrets trong `.env` hay Slack = rủi ro cao

**2. Không expose S3 trực tiếp**
- Dùng CloudFront, API Gateway, pre-signed URLs
- Public buckets = dữ liệu lên báo

**3. Không public IP cho tài nguyên nhạy cảm**
- Redis, RDP, DB phải nằm trong private subnets
- Internet sẽ tìm thấy nhanh hơn bạn nghĩ!

**4. Mọi thứ qua IaC**
- Không ClickOps
- Terraform/CDK + version control = kiểm soát tốt

**5. Double-gate cho thay đổi nguy hiểm**
- SCPs + PR approval + pipeline deploy
- Không ai có quyền console write trực tiếp vào production

---

## 🧪 Hands-on Labs – Học qua thực hành

| **Tên Lab**                | **Mục tiêu**                                      | **Kỹ thuật chính**                                   |
|----------------------------|---------------------------------------------------|------------------------------------------------------|
| EC2 IAM & Passwordless     | Loại bỏ SSH keys và DB passwords                  | Session Manager, RDS IAM Auth, AssumeRole            |
| S3 Exposed & Remediation   | Phát hiện và tự động khắc phục S3 buckets public   | EventBridge, Lambda, CloudFront OAC, SCPs            |
| EC2 Isolation              | Tự động cô lập EC2 bị nghi nhiễm                  | GuardDuty, Forensics, Network Isolation              |
| OIDC GitHub Federation     | Deploy từ GitHub Actions không cần AWS key tĩnh   | OIDC, IAM Trust Policies, Least Privilege            |

🔗 **GitHub Labs**: [https://github.com/grabskimm/aws-labs](https://github.com/grabskimm/aws-labs)

---

## 🧩 CloudTrail & Multi-Layer Visibility

### 🔍 CloudTrail Organization-Level

- **Centralized Logging**: Ghi log toàn bộ hành động API từ tất cả accounts trong tổ chức AWS
- **Enterprise Scale Monitoring**: Phát hiện hành vi bất thường, audit toàn diện, và forensics sau sự cố
- **EventBridge & Security Hub Integration**: Tự động hóa cảnh báo và phản hồi

---

### 🔭 Multi-Layer Security Visibility

| **Lớp giám sát**           | **Chi tiết**                                                                 |
|----------------------------|------------------------------------------------------------------------------|
| Management Events          | Ghi nhận API calls và hành động console trên toàn bộ accounts                |
| Data Events                | Truy cập object S3, thực thi Lambda – theo dõi dữ liệu ở tầng ứng dụng       |
| Network Activity Events    | VPC Flow Logs – giám sát lưu lượng mạng, phát hiện bất thường                |
| Organization Coverage      | Logging hợp nhất toàn bộ regions và accounts – tăng khả năng phát hiện       |

---

## 🔐 Quản lý truy cập & Bảo mật định danh

### 🔁 Credential Rotation – Quản lý vòng đời bí mật

**AWS Secrets Manager** tự động hóa việc xoay vòng credentials (IAM, DB, API keys).

#### Quy trình rotation gồm 5 bước:
1. `createSecret` – Tạo bí mật mới
2. `setSecret` – Gán bí mật mới cho ứng dụng
3. `testSecret` – Kiểm tra bí mật mới
4. `finishSecret` – Hoàn tất quá trình xoay vòng
5. `deletePreviousSecret` – Xóa bí mật cũ sau thời gian grace period

➡️ **EventBridge + Lambda**: Tự động hóa việc xóa bí mật cũ sau khi hoàn tất rotation

---

### 🔐 Multi-Factor Authentication (MFA)

| **Phương thức** | **Đặc điểm**                                                                 |
|-----------------|------------------------------------------------------------------------------|
| **TOTP**        | Miễn phí, linh hoạt backup, nhập mã 6 số thủ công, dùng shared secret       |
| **FIDO2**       | Dùng public-key cryptography, xác thực bằng chạm hoặc sinh trắc học, bảo mật cao, không thể khôi phục nếu mất thiết bị |

**Khuyến nghị:**
- Dùng **FIDO2** cho tài khoản root và quản trị viên
- Dùng **TOTP** cho người dùng phổ thông

---

### 🕵️ IAM Access Analyzer – Phát hiện chính sách rủi ro

- Phát hiện chính sách chứa `Principal: *` → Cảnh báo vì có thể public
- Ngay cả khi có `Condition: SourceIP` → Vẫn có thể bị xem là public nếu không đủ ràng buộc

#### Tích hợp với EventBridge + Lambda + SNS:
- Tự động thêm deny statement vào IAM Role
- Gửi email cảnh báo cho nhóm bảo mật

---

### 🎬 Demo & Automation thực chiến

**Diễn giả:**
- **Trần Đức Anh** – Cloud Security Engineer Trainee
- **Nguyễn Tuấn Thịnh** – Cloud Engineer Trainee
- **Nguyễn Đỗ Thanh Đạt** – Cloud Engineer Trainee

**Nội dung Demo:**
- Tích hợp CloudTrail, GuardDuty, Security Hub
- Tự động hóa phản hồi bằng EventBridge → Lambda → SNS
- Phân tích logs, phát hiện hành vi bất thường, gửi cảnh báo real-time

---

## 📸 Hình ảnh Workshop

![Security Workshop - Phiên khai mạc](images/image1.jpg?width=1500)
*Phiên khai mạc tại Bitexco Financial Tower*

---

![Security Workshop - Trình bày IAM](images/image2.jpg?width=1500)
*Tìm hiểu sâu về Identity & Access Management*

---

![Security Workshop - Detection & Monitoring](images/image3.jpg?width=1500)
*Khám phá GuardDuty và Security Hub*

---

![Security Workshop - Infrastructure Protection](images/image4.jpg?width=1500)
*Thảo luận về bảo mật mạng và bảo vệ workload*

---

![Security Workshop - Hands-on Labs](images/image5.jpg?width=1500)
*Học viên tham gia các bài lab thực hành bảo mật*

---

![Security Workshop - Ảnh tập thể](images/image6.jpg?width=1500)
*Các học viên tham gia AWS Well-Architected Security Pillar Workshop*

---

## 🎓 Những gì bạn đã học được

Qua buổi workshop chuyên sâu buổi sáng này, bạn đã có được kiến thức toàn diện về năm trụ cột bảo mật AWS:

**Identity & Access Management**
- Kiến trúc IAM hiện đại với temporary credentials và SSO
- Bảo mật multi-account với SCPs và permission boundaries
- Triển khai MFA và chiến lược xoay vòng credentials

**Detection & Monitoring**
- CloudTrail cấp tổ chức cho việc ghi log API toàn diện
- Phát hiện mối đe dọa bằng ML của GuardDuty qua nhiều nguồn dữ liệu
- Security Hub cho quản lý tư thế bảo mật tập trung

**Infrastructure Protection**
- Phân đoạn mạng với VPCs, Security Groups, và NACLs
- Bảo mật tầng DNS với Route 53 Resolver Firewall
- Bảo vệ nâng cao với AWS Network Firewall và WAF

**Data Protection**
- Mã hóa at-rest và in-transit trên các dịch vụ AWS
- Quản lý và rotation policies của KMS keys
- Secrets Manager cho quản lý vòng đời credentials tự động

**Incident Response**
- Workflows phản hồi tự động với EventBridge và Lambda
- Kỹ thuật forensics và thu thập bằng chứng
- Chiến lược cô lập và khắc phục cho tài nguyên bị xâm phạm

---

## 🚀 Hành trình phía trước

### Các bước tiếp theo ngay lập tức
1. **Thực hành Labs**: Xem lại các bài tập hands-on tại [github.com/grabskimm/aws-labs](https://github.com/grabskimm/aws-labs)
2. **Triển khai trong môi trường của bạn**: Bắt đầu với các quick wins như bật GuardDuty và Security Hub
3. **Xây dựng Playbooks**: Tạo runbooks ứng phó sự cố cho tổ chức của bạn

### Lộ trình chứng chỉ
- **AWS Certified Security – Specialty**: Tìm hiểu sâu về các best practices bảo mật
- **AWS Certified Solutions Architect – Professional**: Kiến thức kiến trúc toàn diện bao gồm bảo mật

### Học tập liên tục
- Tham gia diễn đàn cộng đồng và nhóm người dùng AWS Security
- Theo dõi AWS Security Blog để cập nhật tin tức và best practices mới nhất
- Tham gia AWS Cloud Clubs và các sự kiện cộng đồng
- Đóng góp vào các công cụ bảo mật open-source và chia sẻ kiến thức

### Ứng dụng thực tế
- Kiểm tra môi trường AWS hiện tại theo Well-Architected Framework
- Triển khai Detection-as-Code trong CI/CD pipelines
- Thiết lập chương trình security champions trong tổ chức
- Tiến hành đánh giá bảo mật và bài tập tabletop thường xuyên

---

## 💬 Lời kết

Bảo mật trên cloud không phải là đích đến—mà là hành trình liên tục của việc học hỏi, thích nghi và cải thiện. AWS Well-Architected Security Pillar cung cấp nền tảng vững chắc, nhưng giá trị thực sự đến từ việc áp dụng các nguyên tắc này trong bối cảnh riêng của bạn.

**Hãy nhớ:**
- Bắt đầu từ nhỏ, nhưng hãy bắt đầu ngay hôm nay
- Tự động hóa mọi thứ có thể
- Chia sẻ kiến thức với team
- Luôn tò mò và tiếp tục học hỏi

Cộng đồng cloud Việt Nam đang ngày càng phát triển mạnh mẽ. Bằng việc triển khai các thực hành bảo mật này, bạn không chỉ bảo vệ tổ chức của mình—mà còn đóng góp vào một hệ sinh thái cloud an toàn hơn cho tất cả mọi người.

**Cảm ơn sự tham gia và cống hiến của bạn cho sự xuất sắc trong bảo mật cloud!**

---

> Workshop này là lời nhắc nhở mạnh mẽ rằng bảo mật không chỉ là một tính năng—mà là một tư duy và thực hành liên tục trong kiến trúc cloud.
