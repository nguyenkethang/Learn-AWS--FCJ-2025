---
title: "Triển khai Infrastructure với CloudFormation"
date: 2025-12-08
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

## Tổng quan

Trong bước này, bạn sẽ triển khai toàn bộ hạ tầng AWS bằng CloudFormation template. Template sẽ tạo VPC, subnets, EC2 instances, RDS database, Load Balancer, S3 buckets, CloudFront distribution và tất cả các tài nguyên cần thiết.

## Validate Template

Trước khi triển khai, validate template để đảm bảo không có lỗi cú pháp:

```bash
cd aws
aws cloudformation validate-template \
  --template-body file://infrastructure.yaml \
  --region ap-southeast-1
```

**Kết quả mong đợi:** Thông tin về parameters, outputs và description của template.

## Triển khai Stack

### Cách 1: Sử dụng Deploy Script (Khuyên dùng)

**Windows:**
```cmd
cd aws
deploy.bat create
```

**Linux/Mac:**
```bash
cd aws
chmod +x deploy.sh
./deploy.sh create
```

Script sẽ tự động:
- Validate template
- Create CloudFormation stack
- Theo dõi tiến trình deployment
- Hiển thị outputs khi hoàn thành

### Cách 2: Sử dụng AWS CLI

```bash
aws cloudformation create-stack \
  --stack-name workshop-aws-dev \
  --template-body file://infrastructure.yaml \
  --parameters file://parameters.json \
  --capabilities CAPABILITY_NAMED_IAM \
  --region ap-southeast-1
```

## Theo dõi Tiến trình

### Qua AWS Console

1. Mở [CloudFormation Console](https://console.aws.amazon.com/cloudformation/)
2. Chọn stack `workshop-aws-dev`
3. Tab **Events**: Xem các resources đang được tạo
4. Tab **Resources**: Xem danh sách resources
5. Tab **Outputs**: Xem outputs (sau khi hoàn thành)

### Qua AWS CLI

```bash
# Kiểm tra status
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].StackStatus'

# Xem events
aws cloudformation describe-stack-events \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --max-items 10
```

## Thời gian Deployment

Quá trình tạo stack mất khoảng **15-20 phút**:

- VPC và Networking: 2-3 phút
- NAT Gateway: 2-3 phút
- RDS Database: 5-7 phút
- EC2 Auto Scaling Group: 3-5 phút
- Load Balancer: 2-3 phút
- CloudFront Distribution: 5-10 phút
- VPC Endpoints: 2-3 phút

## Xem Outputs

Sau khi stack tạo thành công (Status: `CREATE_COMPLETE`), lấy outputs:

```bash
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs' \
  --output table
```

**Các Outputs quan trọng:**

| Output Key | Mô tả | Ví dụ |
|------------|-------|-------|
| `VPCId` | VPC ID | vpc-0123456789abcdef0 |
| `FrontendBucketName` | S3 bucket cho frontend | workshop-aws-dev-frontend-123456789012-ap-southeast-1 |
| `CloudFrontDomainName` | CloudFront URL | d1234567890abc.cloudfront.net |
| `ALBDNSName` | Load Balancer DNS | workshop-aws-dev-alb-123456789.ap-southeast-1.elb.amazonaws.com |
| `RDSEndpoint` | Database endpoint | workshop-aws-dev-db.xxxxx.ap-southeast-1.rds.amazonaws.com |
| `APIGatewayURL` | API Gateway URL | https://xxxxx.execute-api.ap-southeast-1.amazonaws.com/dev |
| `CognitoUserPoolId` | Cognito User Pool ID | ap-southeast-1_xxxxxxxxx |

**Lưu các giá trị này** - bạn sẽ cần chúng cho các bước tiếp theo!


## Kiểm tra Resources đã tạo

### 1. VPC và Networking

```bash
# Lấy VPC ID
VPC_ID=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`VPCId`].OutputValue' \
  --output text)

# Xem VPC details
aws ec2 describe-vpcs --vpc-ids $VPC_ID --region ap-southeast-1

# Xem Subnets
aws ec2 describe-subnets \
  --filters "Name=vpc-id,Values=$VPC_ID" \
  --region ap-southeast-1 \
  --query 'Subnets[*].[SubnetId,CidrBlock,AvailabilityZone,Tags[?Key==`Name`].Value|[0]]' \
  --output table
```

### 2. EC2 Instances

```bash
# Xem EC2 instances trong Auto Scaling Group
aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
  --region ap-southeast-1 \
  --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PrivateIpAddress,PublicIpAddress]' \
  --output table
```

### 3. RDS Database

```bash
# Xem RDS instance
aws rds describe-db-instances \
  --db-instance-identifier workshop-aws-dev-db \
  --region ap-southeast-1 \
  --query 'DBInstances[0].[DBInstanceIdentifier,DBInstanceStatus,Endpoint.Address,Endpoint.Port]' \
  --output table
```

### 4. Load Balancer

```bash
# Xem ALB
aws elbv2 describe-load-balancers \
  --names workshop-aws-dev-alb \
  --region ap-southeast-1 \
  --query 'LoadBalancers[0].[LoadBalancerName,DNSName,State.Code]' \
  --output table
```

### 5. S3 Buckets

```bash
# List S3 buckets
aws s3 ls | grep workshop-aws-dev
```

### 6. CloudFront Distribution

```bash
# Lấy Distribution ID
DIST_ID=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDistributionId`].OutputValue' \
  --output text)

# Xem distribution status
aws cloudfront get-distribution --id $DIST_ID \
  --query 'Distribution.[Id,Status,DomainName]' \
  --output table
```

## Troubleshooting

### Stack Creation Failed

Nếu stack creation bị lỗi:

1. **Xem Events để tìm lỗi:**
```bash
aws cloudformation describe-stack-events \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'StackEvents[?ResourceStatus==`CREATE_FAILED`].[LogicalResourceId,ResourceStatusReason]' \
  --output table
```

2. **Các lỗi thường gặp:**

**Lỗi: "Key pair does not exist"**
- Kiểm tra tên key pair trong `parameters.json`
- Đảm bảo key pair tồn tại trong region ap-southeast-1

**Lỗi: "Invalid AMI ID"**
- Cập nhật AMI ID trong `infrastructure.yaml`
- Sử dụng AMI ID phù hợp với region

**Lỗi: "Insufficient permissions"**
- Kiểm tra IAM permissions của user
- Cần quyền CloudFormation, EC2, VPC, RDS, S3, IAM

**Lỗi: "Resource limit exceeded"**
- Kiểm tra service quotas trong AWS account
- Request tăng limits nếu cần

3. **Rollback và thử lại:**
```bash
# Xóa stack bị lỗi
aws cloudformation delete-stack \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1

# Đợi stack bị xóa hoàn toàn
aws cloudformation wait stack-delete-complete \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1

# Thử tạo lại
aws cloudformation create-stack \
  --stack-name workshop-aws-dev \
  --template-body file://infrastructure.yaml \
  --parameters file://parameters.json \
  --capabilities CAPABILITY_NAMED_IAM \
  --region ap-southeast-1
```

## Xác nhận Deployment thành công

Checklist để xác nhận infrastructure đã sẵn sàng:

- [ ] Stack status là `CREATE_COMPLETE`
- [ ] VPC và subnets đã được tạo
- [ ] EC2 instances đang chạy (State: `running`)
- [ ] RDS database status là `available`
- [ ] Load Balancer status là `active`
- [ ] S3 buckets đã được tạo
- [ ] CloudFront distribution status là `Deployed`
- [ ] Tất cả outputs đã có giá trị

## Tiếp theo

Sau khi infrastructure đã sẵn sàng, bạn có thể:

➡️ [Cấu hình và Triển khai Backend Application](../5.4-deploy-backend/)

