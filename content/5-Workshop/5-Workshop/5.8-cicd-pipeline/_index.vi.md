---
title: "Thiết lập CI/CD Pipeline"
date: 2025-12-08
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

## Tổng quan

Trong phần này, bạn sẽ thiết lập một CI/CD pipeline hoàn chỉnh sử dụng AWS CodePipeline, CodeBuild và GitLab CI/CD để tự động hóa quá trình build và deploy cho cả backend và frontend.

## Kiến trúc

```
GitLab → S3 (Artifacts) → CodePipeline → CodeBuild (Backend) → EC2
                                      ↓
                                      CodeBuild (Frontend) → S3/CloudFront
```

## Các thành phần CI/CD

### 1. GitLab CI/CD
- Tự động build và đóng gói source code
- Upload artifacts lên S3
- Kích hoạt AWS CodePipeline

### 2. AWS CodePipeline
- Điều phối toàn bộ quy trình deployment
- Giám sát S3 để phát hiện artifacts mới
- Kích hoạt các CodeBuild projects

### 3. AWS CodeBuild
- **Backend Build**: Biên dịch ứng dụng Spring Boot thành JAR
- **Frontend Build**: Build ứng dụng React với Vite
- Deploy lên các dịch vụ AWS tương ứng

## Bước 1: Cấu hình GitLab CI/CD

### 1.1. Thiết lập GitLab CI/CD Variables

Trong GitLab project, vào **Settings → CI/CD → Variables** và thêm:

| Variable | Value | Protected | Masked |
|----------|-------|-----------|--------|
| `AWS_ACCESS_KEY_ID` | AWS Access Key của bạn | ✅ | ✅ |
| `AWS_SECRET_ACCESS_KEY` | AWS Secret Key của bạn | ✅ | ✅ |

### 1.2. Xem lại cấu hình GitLab CI

File `.gitlab-ci.yml` trong thư mục gốc project:

```yaml
stages:
  - deploy

deploy-to-aws:
  stage: deploy
  image: amazon/aws-cli:latest
  before_script:
    - |
      aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
      aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
      aws configure set region ap-southeast-1
  script:
    - echo "📦 Đang tạo source.zip..."
    - |
      apk add zip
      zip -r source.zip . \
        -x "*.git*" \
        -x "node_modules/*" \
        -x ".idea/*" \
        -x "target/*" \
        -x "*.zip"
    - echo "📤 Đang upload lên S3..."
    - |
      aws s3 cp source.zip \
        s3://workshop-aws-dev-artifacts-502310717700-ap-southeast-1/source.zip
    - echo "✅ Upload hoàn tất! CodePipeline sẽ tự động kích hoạt."
  only:
    - main
  when: on_success
```

**Chức năng:**
- Đóng gói toàn bộ project thành `source.zip`
- Upload lên S3 artifacts bucket
- Tự động kích hoạt CodePipeline

## Bước 2: Deploy CodePipeline với CloudFormation

### 2.1. Xem lại Pipeline Template

Template CloudFormation `cicd-pipeline.yaml` tạo:
- CodePipeline với S3 source
- CodeBuild project cho backend
- CodeBuild project cho frontend
- IAM roles và permissions

### 2.2. Deploy Pipeline Stack

```bash
aws cloudformation create-stack \
  --stack-name workshop-aws-dev-cicd \
  --template-body file://aws/cicd-pipeline.yaml \
  --parameters \
    ParameterKey=ProjectName,ParameterValue=workshop-aws \
    ParameterKey=Environment,ParameterValue=dev \
    ParameterKey=SourceProvider,ParameterValue=S3 \
    ParameterKey=ArtifactBucketName,ParameterValue=workshop-aws-dev-artifacts-502310717700-ap-southeast-1 \
  --capabilities CAPABILITY_NAMED_IAM \
  --region ap-southeast-1
```

### 2.3. Chờ Stack tạo xong

```bash
aws cloudformation wait stack-create-complete \
  --stack-name workshop-aws-dev-cicd \
  --region ap-southeast-1
```

**Thời gian dự kiến:** 3-5 phút

## Bước 3: Cấu hình CodeBuild Projects

### 3.1. Backend BuildSpec

CodeBuild sử dụng `buildspec-backend.yml`:

```yaml
version: 0.2

phases:
  pre_build:
    commands:
      - echo "Đang cài đặt Maven..."
      - yum install -y maven
  
  build:
    commands:
      - echo "Đang build Backend JAR..."
      - cd BE/workshop_BE
      - mvn clean package -DskipTests
  
  post_build:
    commands:
      - echo "Đang upload JAR lên S3..."
      - aws s3 cp target/workshop-0.0.1-SNAPSHOT.jar \
          s3://workshop-aws-dev-backend-502310717700-ap-southeast-1/jars/
      - echo "Đang deploy lên EC2..."
      - aws ssm send-command \
          --instance-ids i-09fdbf7739ee37b32 \
          --document-name "AWS-RunShellScript" \
          --parameters commands=[
            "cd /opt/workshop",
            "aws s3 cp s3://workshop-aws-dev-backend-502310717700-ap-southeast-1/jars/workshop-0.0.1-SNAPSHOT.jar .",
            "sudo systemctl restart workshop.service"
          ]

artifacts:
  files:
    - '**/*'
```

### 3.2. Frontend BuildSpec

CodeBuild sử dụng `buildspec-frontend.yml`:

```yaml
version: 0.2

phases:
  pre_build:
    commands:
      - echo "Đang cài đặt Node.js..."
      - curl -sL https://rpm.nodesource.com/setup_18.x | bash -
      - yum install -y nodejs
  
  build:
    commands:
      - echo "Đang build Frontend..."
      - cd FE
      - npm install
      - npm run build
  
  post_build:
    commands:
      - echo "Đang deploy lên S3..."
      - aws s3 sync dist/ \
          s3://workshop-aws-dev-frontend-502310717700-ap-southeast-1/ \
          --delete
      - echo "Đang invalidate CloudFront..."
      - aws cloudfront create-invalidation \
          --distribution-id E3K48K7CPOOLHZ \
          --paths "/*"

artifacts:
  files:
    - 'FE/dist/**/*'
```

## Bước 4: Test CI/CD Pipeline

### 4.1. Kích hoạt Pipeline từ GitLab

Thực hiện thay đổi code và push lên branch `main`:

```bash
git add .
git commit -m "Test CI/CD pipeline"
git push origin main
```

### 4.2. Theo dõi GitLab Pipeline

1. Vào GitLab → **CI/CD → Pipelines**
2. Xem job `deploy-to-aws`
3. Xác nhận upload lên S3 thành công

### 4.3. Theo dõi AWS CodePipeline

1. Vào AWS Console → **CodePipeline**
2. Chọn `workshop-aws-dev-pipeline`
3. Xem các giai đoạn pipeline:
   - **Source**: Phát hiện `source.zip` mới trong S3
   - **Build-Backend**: Build JAR và deploy lên EC2
   - **Build-Frontend**: Build React app và deploy lên S3/CloudFront

### 4.4. Kiểm tra Build Logs

Để xem logs chi tiết:

1. Click vào **Details** ở bất kỳ stage nào
2. Xem **Build logs** trong CodeBuild
3. Kiểm tra lỗi hoặc cảnh báo

## Bước 5: Xác nhận Deployment

### 5.1. Test Backend API

```bash
curl https://98385v3jef.execute-api.ap-southeast-1.amazonaws.com/dev/dna_service/actuator/health
```

**Kết quả mong đợi:**
```json
{"status":"UP"}
```

### 5.2. Test Frontend

Mở trình duyệt và truy cập:
```
https://d3gmmg22uirq0t.cloudfront.net
```

Xác nhận ứng dụng load với các thay đổi mới nhất.

## Sơ đồ luồng Pipeline

```
┌─────────────┐
│   GitLab    │
│   Commit    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ GitLab CI   │
│ Build & Zip │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  S3 Bucket  │
│ source.zip  │
└──────┬──────┘
       │
       ▼
┌─────────────────────┐
│   CodePipeline      │
│   Phát hiện thay đổi│
└──────┬──────────────┘
       │
       ├─────────────────┬─────────────────┐
       ▼                 ▼                 ▼
┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│ CodeBuild   │   │ CodeBuild   │   │ CloudWatch  │
│  Backend    │   │  Frontend   │   │  Logs       │
└──────┬──────┘   └──────┬──────┘   └─────────────┘
       │                 │
       ▼                 ▼
┌─────────────┐   ┌─────────────┐
│     EC2     │   │ S3 + CDN    │
│   Backend   │   │  Frontend   │
└─────────────┘   └─────────────┘
```

## Xử lý sự cố

### Pipeline không kích hoạt

**Vấn đề**: CodePipeline không chạy sau khi push GitLab

**Giải pháp**:
1. Kiểm tra S3 bucket có file `source.zip`
2. Xác minh cấu hình source của CodePipeline
3. Kiểm tra IAM permissions cho CodePipeline

### Backend Build thất bại

**Vấn đề**: CodeBuild backend lỗi Maven

**Giải pháp**:
1. Kiểm tra cú pháp `buildspec-backend.yml`
2. Xác minh Maven dependencies trong `pom.xml`
3. Xem CodeBuild logs để tìm lỗi cụ thể
4. Đảm bảo EC2 instance có SSM Agent đang chạy

### Frontend Build thất bại

**Vấn đề**: CodeBuild frontend lỗi npm

**Giải pháp**:
1. Kiểm tra cú pháp `buildspec-frontend.yml`
2. Xác minh dependencies trong `package.json`
3. Kiểm tra tương thích phiên bản Node.js
4. Đảm bảo S3 bucket permissions đúng

### Deployment thất bại

**Vấn đề**: Build thành công nhưng deployment lỗi

**Giải pháp**:
1. Kiểm tra EC2 Security Groups cho phép SSM
2. Xác minh tên S3 bucket đúng
3. Kiểm tra CloudFront distribution ID
4. Xem lại IAM role permissions

## Best Practices

### 1. Environment Variables
- Lưu dữ liệu nhạy cảm trong GitLab CI/CD variables
- Dùng AWS Systems Manager Parameter Store cho application configs
- Không bao giờ commit credentials vào Git

### 2. Tối ưu Build
- Cache dependencies (Maven `.m2`, npm `node_modules`)
- Dùng Docker images nhỏ hơn để build nhanh hơn
- Chạy song song các build stages độc lập

### 3. Chiến lược Deployment
- Dùng blue-green deployment cho zero downtime
- Implement health checks trước khi route traffic
- Giữ khả năng rollback sẵn sàng

### 4. Monitoring
- Bật CloudWatch Logs cho tất cả CodeBuild projects
- Thiết lập SNS notifications cho pipeline failures
- Theo dõi build times và tối ưu bottlenecks

## Tối ưu Chi phí

### Giá CodeBuild
- **Build minutes**: $0.005 mỗi phút (general1.small)
- **Build thông thường**: 5-10 phút
- **Chi phí mỗi build**: ~$0.025-0.05

### Giá CodePipeline
- **Active pipeline**: $1.00 mỗi tháng
- **Free tier**: 1 active pipeline mỗi tháng

### Ước tính Chi phí Hàng tháng
- **10 deployments/ngày**: ~$15-20/tháng
- **Bao gồm**: CodePipeline + CodeBuild + S3 storage

## Tóm tắt

Bạn đã thiết lập thành công một CI/CD pipeline hoàn chỉnh:

✅ Tự động build và đóng gói code từ GitLab  
✅ Upload artifacts lên S3  
✅ Kích hoạt AWS CodePipeline khi có thay đổi  
✅ Build backend JAR với Maven  
✅ Build frontend với Vite  
✅ Deploy backend lên EC2  
✅ Deploy frontend lên S3/CloudFront  
✅ Cung cấp monitoring và logging  

**Tiếp theo**: [Dọn dẹp Tài nguyên](../5.9-cleanup/)
