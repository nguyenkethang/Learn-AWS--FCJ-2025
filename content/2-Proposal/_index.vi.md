---
title: "Đề xuất dự án"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Blood Donation Support System (BDSS)

📄 **[Tải Tài Liệu Đề Xuất Đầy Đủ (Word)](Proposal%20Template.docx)**

## 1. Tóm tắt điều hành

**Blood Donation Support System (BDSS)** là nền tảng web hỗ trợ quản lý và kết nối người hiến máu với cơ sở y tế. Dự án được phát triển bởi nhóm sinh viên tại TP. Hồ Chí Minh nhằm tối ưu quy trình hiến máu, giảm tải khâu tìm kiếm người hiến và nâng cao hiệu quả truyền thông y tế.

Hệ thống được xây dựng trên **kiến trúc AWS Cloud**, sử dụng **Amazon EC2**, **Amazon RDS**, **API Gateway**, **Cognito** và **CI/CD Pipeline (GitLab + CodePipeline)** để tự động triển khai. BDSS hỗ trợ bốn nhóm người dùng (Guest, Member, Staff, Admin), cung cấp tính năng tra cứu, đăng ký hiến máu, quản lý kho máu, theo dõi quy trình hiến máu và báo cáo trực quan.

---

## 2. Tuyên bố vấn đề

### Vấn đề hiện tại:

Các cơ sở y tế hiện đang quản lý quy trình hiến máu thủ công hoặc thông qua các công cụ rời rạc. Việc tìm kiếm người hiến máu phù hợp nhóm máu hoặc theo khu vực gặp khó khăn, đặc biệt trong tình huống khẩn cấp. Ngoài ra, hệ thống lưu trữ dữ liệu chưa đồng bộ, gây khó khăn trong việc phân tích, báo cáo và tối ưu chiến dịch hiến máu.

### Giải pháp đề xuất:

Phát triển **nền tảng hỗ trợ hiến máu toàn diện trên AWS Cloud**, với các chức năng quản lý hiến máu, tìm kiếm người hiến và người cần máu theo nhóm máu hoặc vị trí địa lý, tích hợp xác thực người dùng qua Amazon Cognito và quản trị dữ liệu trên Amazon RDS.

Frontend được triển khai qua **Route 53 + CloudFront**, backend thông qua **API Gateway – EC2**, cơ sở dữ liệu MySQL trên **Amazon RDS**, và pipeline tự động CI/CD bằng **GitLab – CodePipeline**.

### Lợi ích và ROI:

- Giảm 60–70% thời gian tìm kiếm người hiến máu phù hợp.
- Tăng độ chính xác thông tin nhóm máu và vị trí.
- Tối ưu chi phí vận hành với kiến trúc cloud linh hoạt, trả phí theo mức sử dụng.
- Cải thiện khả năng phản hồi trong các trường hợp máu khẩn cấp.

---

## 3. Kiến trúc giải pháp

### Kiến trúc tổng thể:

![AWS Blood Donation Architecture](AWS%20architecture%20diagrams%20blood%20donation%20support%20systems.png)

Hệ thống được thiết kế theo kiến trúc **3-tier trên AWS Cloud** với các thành phần chính:

### 1. Frontend & Content Delivery Layer:

- **Users**: Người dùng truy cập hệ thống qua trình duyệt web hoặc mobile.
- **Route 53**: Dịch vụ DNS quản lý domain name và routing traffic đến CloudFront.
- **CloudFront**: CDN phân phối nội dung tĩnh với độ trễ thấp, cache tại edge locations.
- **Amazon S3**: Lưu trữ static assets (HTML, CSS, JS, images) cho frontend application.

### 2. Application & Compute Layer:

- **API Gateway**: REST API endpoint, xử lý request/response giữa frontend và backend.
- **VPC (Virtual Private Cloud)**: Mạng riêng ảo cô lập với cấu hình:
  - **Internet Gateway**: Cho phép public subnet kết nối Internet.
  - **Public Subnet**: Chứa EC2 instances xử lý business logic.
  - **Private Subnet**: Chứa RDS database, không truy cập trực tiếp từ Internet.
  - **NAT Gateway**: Cho phép private subnet truy cập Internet một chiều (outbound).
- **Amazon EC2**: Compute instances chạy backend API (Node.js/Express).
- **Amazon RDS (MySQL)**: Relational database lưu trữ dữ liệu người hiến máu, nhóm máu, lịch sử hiến máu.

### 3. CI/CD & DevOps Pipeline:

- **GitLab**: Source code repository và version control.
- **AWS CodePipeline**: Orchestrate CI/CD workflow tự động.
- **AWS CodeBuild**: Build và test code trước khi deploy.
- **Automated Deployment**: Tự động deploy lên EC2 khi có code changes.

### 4. Monitoring, Security & Management Layer:

- **Amazon Cognito**: User authentication và authorization (Guest, Member, Staff, Admin roles).
- **AWS IAM**: Quản lý quyền truy cập cho users và services.
- **AWS Secrets Manager**: Lưu trữ an toàn database credentials và API keys.
- **Amazon CloudWatch**: Giám sát metrics, logs, và tạo alarms.
- **AWS CloudTrail**: Audit logs cho tất cả API calls và user activities.
- **Amazon Athena**: Query và phân tích logs từ S3.
- **Amazon SNS**: Gửi notifications (email/SMS) khi có sự kiện quan trọng (máu khẩn cấp, người hiến phù hợp).

### Luồng hoạt động của hệ thống:

1. **User Access**: Users → Route 53 → CloudFront → S3 (Frontend)
2. **API Requests**: Frontend → API Gateway → EC2 (Backend) → RDS (Database)
3. **Data Flow**: EC2 instances trong public subnet kết nối với RDS trong private subnet
4. **Outbound Traffic**: Private subnet → NAT Gateway → Internet Gateway
5. **CI/CD Flow**: GitLab → CodePipeline → CodeBuild → EC2 deployment
6. **Monitoring**: CloudWatch thu thập metrics → SNS gửi alerts → Athena phân tích logs

---

## 4. Triển khai kỹ thuật

### Các giai đoạn triển khai:

#### 1. Phân tích & thiết kế (Tháng 1)

- Thu thập yêu cầu, xác định use case, thiết kế ERD và kiến trúc AWS.

#### 2. Thiết lập hạ tầng & pipeline (Tháng 2)

- Cấu hình Route 53, CloudFront, EC2, RDS và CI/CD trên AWS.

#### 3. Phát triển & kiểm thử (Tháng 3–4)

- Xây dựng các module chính: đăng ký hiến máu, tìm kiếm, quản lý kho máu.
- Tích hợp Cognito và hệ thống cảnh báo SNS.

#### 4. Triển khai & vận hành (Tháng 5)

- Triển khai sản phẩm chính thức và giám sát bằng CloudWatch.

### Yêu cầu kỹ thuật chính:

- **Frontend:** React/Next.js hoặc Angular (deploy qua S3/CloudFront).
- **Backend:** Node.js/Express trên EC2, giao tiếp qua REST API Gateway.
- **Database:** Amazon RDS MySQL, tối ưu query và backup định kỳ.
- **CI/CD:** GitLab → CodeBuild → CodePipeline → EC2.
- **Auth:** Cognito (4 vai trò: Guest, Member, Staff, Admin).
- **Alert & Logs:** SNS + CloudWatch + CloudTrail.

---

## 5. Lộ trình & Mốc triển khai

| Thời gian     | Giai đoạn                    | Kết quả chính                                    |
| ------------- | ---------------------------- | ------------------------------------------------ |
| **Tháng 1**   | Phân tích yêu cầu & thiết kế | Kiến trúc AWS + sơ đồ use case                   |
| **Tháng 2**   | Thiết lập hạ tầng & pipeline | EC2, RDS, API Gateway hoạt động                  |
| **Tháng 3–4** | Phát triển & kiểm thử        | Hoàn thiện các module chính                      |
| **Tháng 5**   | Triển khai chính thức        | Hệ thống hoạt động ổn định, có báo cáo Dashboard |

---

## 6. Ước tính ngân sách

| Dịch vụ                         | Ước tính chi phí/tháng (USD) | Ghi chú              |
| ------------------------------- | ---------------------------- | -------------------- |
| EC2 (t3.nano)                   | 3.50                         | Backend REST API     |
| Amazon RDS (MySQL)              | 2.80                         | 20 GB storage        |
| API Gateway                     | 0.50                         | 5.000 request        |
| CloudFront + S3                 | 0.80                         | Website + CDN        |
| Route 53                        | 0.50                         | Domain & DNS         |
| Cognito                         | 0.10                         | <100 người dùng      |
| CloudWatch + Logs               | 0.30                         | Giám sát và cảnh báo |
| CI/CD (CodePipeline, CodeBuild) | 0.40                         | Triển khai tự động   |
| **Tổng cộng**                   | **8.9 USD/tháng**            | ~106.8 USD/năm       |

> Toàn bộ chi phí có thể điều chỉnh dựa trên AWS Free Tier hoặc sử dụng spot instance.

---

## 7. Đánh giá rủi ro

| Rủi ro                     | Ảnh hưởng  | Xác suất   | Biện pháp giảm thiểu              |
| -------------------------- | ---------- | ---------- | --------------------------------- |
| Mất kết nối Internet       | Trung bình | Trung bình | Dự phòng trên EC2 backup          |
| Tấn công DDoS              | Cao        | Thấp       | AWS WAF + CloudFront              |
| Lỗi dữ liệu người dùng     | Cao        | Thấp       | RDS backup + IAM hạn chế truy cập |
| Chi phí vượt mức           | Trung bình | Thấp       | Cảnh báo ngân sách AWS            |
| Gián đoạn triển khai CI/CD | Thấp       | Trung bình | Kiểm tra pipeline trước khi merge |

---

## 8. Kết quả kỳ vọng

- **Kỹ thuật:** Hệ thống cloud-native, CI/CD tự động, hỗ trợ đa người dùng và bảo mật cao.
- **Ứng dụng:** Giúp cơ sở y tế quản lý hiến máu hiệu quả, giảm thiểu quy trình thủ công.
- **Mở rộng:** Có thể nhân rộng cho nhiều bệnh viện khác, tích hợp thêm AI phân tích nhu cầu nhóm máu hoặc dự đoán đợt hiến máu sắp tới.
