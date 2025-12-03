---
title: "Nhật ký công việc Tuần 8"
date: 2025-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Hoàn thành đề xuất dự án Hệ thống Hỗ trợ Hiến máu (BDSS)
* Thiết kế kiến trúc AWS Cloud toàn diện
* Xác định yêu cầu kỹ thuật và lộ trình triển khai
* Lập dự toán chi phí và đánh giá rủi ro

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Phân tích vấn đề quản lý hiến máu hiện tại <br> - Nghiên cứu các giải pháp hiện có và xác định khoảng trống <br> - Xác định phạm vi và mục tiêu dự án                                     | 2025/10/27   | 2025/10/27      | Hướng dẫn An toàn Máu WHO <br> <https://www.who.int/health-topics/blood-safety> <br> Nghiên cứu CNTT Y tế PubMed <br> <https://pubmed.ncbi.nlm.nih.gov/>               |
| 2   | - Thiết kế kiến trúc AWS 3 tầng <br>&emsp; + Tầng Frontend & Phân phối Nội dung <br>&emsp; + Tầng Ứng dụng & Tính toán <br>&emsp; + Tầng Giám sát & Bảo mật                                 | 2025/10/28   | 2025/10/28      | AWS Well-Architected Framework <br> <https://aws.amazon.com/architecture/well-architected/> <br> Trung tâm Kiến trúc AWS <br> <https://aws.amazon.com/architecture/>           |
| 3   | - Xác định công nghệ sử dụng: <br>&emsp; + Frontend: React/Next.js <br>&emsp; + Backend: Node.js/Express <br>&emsp; + Database: Amazon RDS MySQL <br>&emsp; + CI/CD: GitLab + CodePipeline | 2025/10/29   | 2025/10/29      | Thư viện Giải pháp AWS <br> <https://aws.amazon.com/solutions/> <br> Tài liệu React chính thức <br> <https://react.dev/> <br> Best Practices Node.js <br> <https://nodejs.org/en/docs/>                         |
| 4   | - Ánh xạ dịch vụ AWS với yêu cầu: <br>&emsp; + Route 53, CloudFront, S3 <br>&emsp; + API Gateway, EC2, RDS <br>&emsp; + Cognito, IAM, Secrets Manager <br>&emsp; + CloudWatch, SNS, CloudTrail | 2025/10/30   | 2025/10/30      | Tài liệu AWS <br> <https://docs.aws.amazon.com/> <br> Best Practices Bảo mật AWS <br> <https://aws.amazon.com/security/best-practices/> <br> Tuân thủ HIPAA trên AWS <br> <https://aws.amazon.com/compliance/hipaa-compliance/>                 |
| 5   | - Tạo lộ trình triển khai (5 tháng) <br> - Ước tính chi phí dịch vụ AWS <br> - Thực hiện đánh giá rủi ro và lập kế hoạch giảm thiểu                                                         | 2025/10/31   | 2025/11/02      | Công cụ Tính giá AWS <br> <https://calculator.aws/> <br> Quản lý Chi phí AWS <br> <https://aws.amazon.com/aws-cost-management/> <br> Hướng dẫn PMBOK (Quản lý Dự án) <br> <https://www.pmi.org/pmbok-guide-standards>                    |

### Kết quả đạt được tuần 8:

**1. Phân tích Vấn đề & Thiết kế Giải pháp:**
* Xác định các thách thức chính trong quản lý hiến máu hiện tại:
  * Quy trình thủ công và công cụ rời rạc
  * Khó khăn trong việc tìm người hiến máu phù hợp theo nhóm máu/vị trí
  * Thiếu hệ thống lưu trữ dữ liệu đồng bộ
  * Khả năng phản ứng khẩn cấp hạn chế

* Đề xuất giải pháp toàn diện dựa trên AWS Cloud với:
  * Giảm 60-70% thời gian tìm kiếm người hiến máu
  * Cải thiện độ chính xác và đồng bộ dữ liệu
  * Tối ưu chi phí với mô hình trả theo sử dụng
  * Nâng cao khả năng phản ứng trong tình huống khẩn cấp

**2. Thiết kế Kiến trúc AWS:**
* Thiết kế kiến trúc 3 tầng với phân tách rõ ràng:
  * **Tầng Frontend**: Route 53 → CloudFront → S3 để phân phối nội dung tĩnh
  * **Tầng Ứng dụng**: API Gateway → EC2 (public subnet) → RDS (private subnet)
  * **Tầng Bảo mật**: VPC với Internet Gateway, NAT Gateway và cách ly subnet phù hợp

* Tích hợp các dịch vụ AWS toàn diện:
  * **Tính toán**: EC2 instances cho backend API
  * **Cơ sở dữ liệu**: RDS MySQL để lưu trữ dữ liệu quan hệ
  * **Xác thực**: Cognito cho 4 vai trò người dùng (Guest, Member, Staff, Admin)
  * **CI/CD**: GitLab → CodePipeline → CodeBuild → triển khai tự động lên EC2
  * **Giám sát**: CloudWatch, CloudTrail, Athena cho logs và metrics
  * **Thông báo**: SNS cho cảnh báo khẩn cấp và ghép đôi người hiến máu

**3. Xác định Yêu cầu Kỹ thuật:**
* Thiết lập công nghệ sử dụng:
  * Frontend: React/Next.js hoặc Angular
  * Backend: Node.js/Express REST API
  * Database: Amazon RDS MySQL với chiến lược backup
  * Authentication: Amazon Cognito với phân quyền theo vai trò
  * CI/CD: Pipeline tự động với tích hợp GitLab

**4. Lộ trình Triển khai:**
* Tạo kế hoạch 5 tháng theo giai đoạn:
  * Tháng 1: Phân tích yêu cầu & thiết kế
  * Tháng 2: Thiết lập hạ tầng & pipeline
  * Tháng 3-4: Phát triển & kiểm thử
  * Tháng 5: Triển khai production & vận hành

**5. Quản lý Ngân sách & Rủi ro:**
* Ước tính chi phí AWS hàng tháng: **$8.90/tháng** (~$106.8/năm)
  * EC2, RDS, API Gateway, CloudFront, S3, Route 53
  * Cognito, CloudWatch, dịch vụ CI/CD
  * Tối ưu với AWS Free Tier

* Xác định và lập kế hoạch giảm thiểu các rủi ro chính:
  * Vấn đề kết nối Internet
  * Tấn công DDoS (AWS WAF + CloudFront)
  * Bảo mật dữ liệu (RDS backup + kiểm soát IAM)
  * Vượt ngân sách (cảnh báo ngân sách AWS)
  * Gián đoạn triển khai CI/CD (kiểm thử pipeline)

**6. Tài liệu:**
* Hoàn thành đề xuất dự án toàn diện bao gồm:
  * Tóm tắt điều hành
  * Phát biểu vấn đề và phương pháp giải quyết
  * Sơ đồ kiến trúc AWS chi tiết
  * Kế hoạch triển khai kỹ thuật
  * Lịch trình, ngân sách và đánh giá rủi ro
  * Kết quả mong đợi và khả năng mở rộng

### Kết quả & Sản phẩm Tuần 8:

**Các Sản phẩm Hoàn thành:**
* ✅ Tài liệu đề xuất dự án toàn diện (BDSS)
* ✅ Sơ đồ kiến trúc AWS 3 tầng với ánh xạ dịch vụ đầy đủ
* ✅ Tài liệu đặc tả kỹ thuật với công nghệ sử dụng
* ✅ Lịch trình triển khai 5 tháng với các mốc rõ ràng
* ✅ Ước tính ngân sách chi tiết ($8.90/tháng)
* ✅ Ma trận đánh giá rủi ro với chiến lược giảm thiểu

**Các Chỉ số Chính:**
* **Dịch vụ Ánh xạ**: 15+ dịch vụ AWS được tích hợp vào kiến trúc
* **Tối ưu Chi phí**: Đạt ngân sách ~$107/năm (đủ điều kiện AWS Free Tier)
* **Tác động Dự kiến**: Giảm 60-70% thời gian tìm kiếm người hiến máu
* **Vai trò Người dùng**: 4 cấp độ (Guest, Member, Staff, Admin)
* **Thời gian Triển khai**: 5 tháng từ thiết kế đến production

### Bài học Kinh nghiệm:

**1. Thiết kế Kiến trúc:**
* **Bài học**: Cách ly subnet VPC đúng cách (public/private) rất quan trọng cho bảo mật dữ liệu y tế
* **Áp dụng**: Đặt RDS trong private subnet không có truy cập internet trực tiếp, chỉ truy cập qua EC2 trong public subnet
* **Rút ra**: Thiết kế ưu tiên bảo mật ngăn chặn vi phạm dữ liệu và đảm bảo tuân thủ HIPAA

**2. Lựa chọn Dịch vụ:**
* **Bài học**: Không phải tất cả dịch vụ AWS đều cần thiết - tập trung vào yêu cầu cốt lõi
* **Áp dụng**: Chỉ chọn các dịch vụ thiết yếu (EC2, RDS, API Gateway, Cognito) trước khi thêm giám sát/cảnh báo
* **Rút ra**: Bắt đầu tối thiểu, mở rộng dần để kiểm soát chi phí và độ phức tạp

**3. Quản lý Chi phí:**
* **Bài học**: AWS Free Tier có thể giảm đáng kể chi phí ban đầu cho dự án sinh viên/startup
* **Áp dụng**: Chọn EC2 t2.micro và RDS instances nhỏ đủ điều kiện free tier
* **Rút ra**: Luôn sử dụng AWS Pricing Calculator trước khi hoàn thiện quyết định kiến trúc

**4. Lập kế hoạch CI/CD:**
* **Bài học**: Pipeline triển khai tự động tiết kiệm thời gian và giảm lỗi con người
* **Áp dụng**: Tích hợp GitLab → CodePipeline → CodeBuild từ đầu
* **Rút ra**: Thực hành DevOps nên được lập kế hoạch trong giai đoạn thiết kế, không thêm sau

**5. Cân nhắc Lĩnh vực Y tế:**
* **Bài học**: Hệ thống y tế yêu cầu chú ý đặc biệt đến quyền riêng tư, bảo mật và tuân thủ dữ liệu
* **Áp dụng**: Triển khai Cognito cho xác thực, IAM cho kiểm soát truy cập, Secrets Manager cho thông tin đăng nhập, CloudTrail cho audit logs
* **Rút ra**: Tuân thủ quy định (tiêu chuẩn giống HIPAA) phải được giải quyết trong kiến trúc, không phải sau này

**6. Lập kế hoạch Khả năng Mở rộng:**
* **Bài học**: Kiến trúc cloud nên hỗ trợ tăng trưởng tương lai mà không cần thiết kế lại lớn
* **Áp dụng**: Sử dụng dịch vụ được quản lý (RDS, Cognito, CloudFront) tự động mở rộng
* **Rút ra**: Dịch vụ serverless và được quản lý giảm chi phí vận hành và cho phép mở rộng dễ dàng

**7. Tầm quan trọng của Tài liệu:**
* **Bài học**: Tài liệu rõ ràng tăng tốc sự đồng thuận của nhóm và sự ủng hộ của các bên liên quan
* **Áp dụng**: Tạo đề xuất chi tiết với sơ đồ, lịch trình và phân tích ngân sách
* **Rút ra**: Thời gian đầu tư vào tài liệu được đền đáp trong giai đoạn triển khai và bảo trì
