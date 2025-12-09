---
title: "Chuẩn bị & Yêu cầu"
date: 2025-12-08
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

## Yêu cầu Hệ thống

### 1. Tài khoản AWS
- Tài khoản AWS đang hoạt động
- Quyền Administrator hoặc các quyền sau:
  - CloudFormation: Full access
  - EC2: Full access
  - VPC: Full access
  - RDS: Full access
  - S3: Full access
  - CloudFront: Full access
  - IAM: Create roles and policies
  - CloudWatch: Full access

### 2. AWS CLI
Cài đặt và cấu hình AWS CLI:

**Windows:**
```powershell
# Download và cài đặt từ: https://aws.amazon.com/cli/
# Hoặc sử dụng chocolatey:
choco install awscli

# Kiểm tra cài đặt
aws --version
```

**Linux/Mac:**
```bash
# Sử dụng pip
pip install awscli

# Hoặc sử dụng package manager
# Ubuntu/Debian
sudo apt-get install awscli

# MacOS
brew install awscli

# Kiểm tra cài đặt
aws --version
```

**Cấu hình AWS CLI:**
```bash
aws configure
# AWS Access Key ID: <your-access-key>
# AWS Secret Access Key: <your-secret-key>
# Default region name: ap-southeast-1
# Default output format: json
```

### 3. EC2 Key Pair

Tạo EC2 Key Pair để SSH vào instances:

**Qua AWS Console:**
1. Mở [EC2 Console](https://console.aws.amazon.com/ec2/)
2. Chọn region **ap-southeast-1** (Singapore)
3. Vào **Network & Security** → **Key Pairs**
4. Click **Create key pair**
5. Nhập tên: `workshop-aws-key`
6. Key pair type: **RSA**
7. Private key file format: **.pem** (Linux/Mac) hoặc **.ppk** (Windows/PuTTY)
8. Click **Create key pair**
9. Lưu file `.pem` vào thư mục an toàn

**Qua AWS CLI:**
```bash
# Tạo key pair
aws ec2 create-key-pair \
  --key-name workshop-aws-key \
  --query 'KeyMaterial' \
  --output text \
  --region ap-southeast-1 > workshop-aws-key.pem

# Set permissions (Linux/Mac only)
chmod 400 workshop-aws-key.pem
```

### 4. Development Tools

**Java Development Kit (JDK) 17:**
```bash
# Windows (chocolatey)
choco install openjdk17

# Linux (Ubuntu/Debian)
sudo apt-get install openjdk-17-jdk

# MacOS
brew install openjdk@17

# Kiểm tra
java -version
```

**Maven:**
```bash
# Windows
choco install maven

# Linux
sudo apt-get install maven

# MacOS
brew install maven

# Kiểm tra
mvn -version
```

**Node.js và npm:**
```bash
# Windows
choco install nodejs

# Linux
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# MacOS
brew install node

# Kiểm tra
node --version
npm --version
```

## Chuẩn bị Project Files

### 1. Clone hoặc Download Project

```bash
# Nếu có Git repository
git clone <your-repo-url>
cd aws_project

# Hoặc download và extract ZIP file
```

### 2. Cấu trúc Project

```
aws_project/
├── aws/
│   ├── infrastructure.yaml      # CloudFormation template chính
│   ├── cicd-pipeline.yaml       # CI/CD pipeline (optional)
│   ├── parameters.json          # Parameters cho stack
│   ├── deploy.bat              # Deploy script (Windows)
│   ├── deploy.sh               # Deploy script (Linux/Mac)
│   └── README.md               # Hướng dẫn chi tiết
├── BE/
│   └── workshop_BE/
│       ├── src/                # Backend source code
│       ├── pom.xml             # Maven configuration
│       └── README.md
└── FE/
    ├── src/                    # Frontend source code
    ├── package.json            # npm dependencies
    └── README.md
```

### 3. Cấu hình Parameters

Mở file `aws/parameters.json` và cập nhật các giá trị:

```json
[
  {
    "ParameterKey": "ProjectName",
    "ParameterValue": "workshop-aws"
  },
  {
    "ParameterKey": "Environment",
    "ParameterValue": "dev"
  },
  {
    "ParameterKey": "KeyPairName",
    "ParameterValue": "workshop-aws-key"  // ⚠️ Thay bằng tên key pair của bạn
  },
  {
    "ParameterKey": "DBPassword",
    "ParameterValue": "YourStrongPassword123!"  // ⚠️ Đổi mật khẩu mạnh
  },
  {
    "ParameterKey": "InstanceType",
    "ParameterValue": "t3.micro"
  },
  {
    "ParameterKey": "DBInstanceClass",
    "ParameterValue": "db.t3.micro"
  }
]
```

**Lưu ý quan trọng:**
- `KeyPairName`: Phải khớp với tên key pair đã tạo
- `DBPassword`: Tối thiểu 8 ký tự, bao gồm chữ hoa, chữ thường, số và ký tự đặc biệt
- Không commit file này với mật khẩu thật vào Git

### 4. Cập nhật AMI ID

CloudFormation template sử dụng AMI ID mặc định. Bạn cần cập nhật cho region của mình:

**Tìm AMI ID:**
```bash
# Tìm Amazon Linux 2023 AMI cho region ap-southeast-1
aws ec2 describe-images \
  --owners amazon \
  --filters "Name=name,Values=al2023-ami-*-x86_64" \
  --query 'Images | sort_by(@, &CreationDate) | [-1].[ImageId,Name,CreationDate]' \
  --region ap-southeast-1 \
  --output table
```

**Cập nhật trong `infrastructure.yaml`:**

Tìm dòng ~530:
```yaml
LaunchTemplate:
  Properties:
    LaunchTemplateData:
      ImageId: ami-0c55b159cbfafe1f0  # ⚠️ Thay bằng AMI ID của bạn
```

## Kiểm tra Chuẩn bị

### Checklist

Đảm bảo bạn đã hoàn thành tất cả các bước sau:

- [ ] Tài khoản AWS đã được cấu hình
- [ ] AWS CLI đã cài đặt và cấu hình (`aws configure`)
- [ ] EC2 Key Pair đã được tạo
- [ ] Java 17 đã cài đặt
- [ ] Maven đã cài đặt
- [ ] Node.js và npm đã cài đặt
- [ ] Project files đã được download
- [ ] File `parameters.json` đã được cập nhật
- [ ] AMI ID đã được cập nhật trong `infrastructure.yaml`

### Validate AWS Credentials

```bash
# Kiểm tra AWS credentials
aws sts get-caller-identity

# Kết quả mong đợi:
# {
#     "UserId": "AIDAXXXXXXXXXXXXXXXXX",
#     "Account": "123456789012",
#     "Arn": "arn:aws:iam::123456789012:user/your-username"
# }
```

### Validate CloudFormation Template

```bash
cd aws
aws cloudformation validate-template \
  --template-body file://infrastructure.yaml \
  --region ap-southeast-1
```

Nếu thành công, bạn sẽ thấy output với thông tin về template parameters và outputs.

## Ước tính Chi phí

Trước khi triển khai, hãy hiểu rõ chi phí:

| Dịch vụ | Instance Type | Chi phí/tháng (USD) |
|---------|---------------|---------------------|
| EC2 | t3.nano | $3.50 |
| RDS MySQL | db.t3.micro | $2.80 |
| API Gateway | - | $0.50 |
| S3 + CloudFront | - | $0.80 |
| Route 53 | - | $0.50 |
| Cognito | - | $0.10 |
| CloudWatch | - | $0.30 |
| CI/CD (CodePipeline) | - | $0.40 |
| **Tổng** | | **$8.90** |

**Cho workshop (2-3 giờ):** ~$0.50-1.00

**Lưu ý:** 
- Chi phí trên áp dụng cho region ap-southeast-1
- Sử dụng AWS Free Tier nếu tài khoản đủ điều kiện
- NAT Gateway (~$32/tháng) có thể tắt để tiết kiệm chi phí

## Tiếp theo

Sau khi hoàn thành tất cả các bước chuẩn bị, bạn đã sẵn sàng để:

➡️ [Triển khai Infrastructure với CloudFormation](../5.3-deploy-infrastructure/)

