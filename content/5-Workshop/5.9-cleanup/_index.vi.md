---
title: "Dọn dẹp tài nguyên"
date: 2025-12-08
weight: 8
chapter: false
pre: " <b> 5.8 </b> "
---

## Tổng quan

Sau khi hoàn thành workshop, bạn cần xóa tất cả tài nguyên để tránh phát sinh chi phí không mong muốn. CloudFormation sẽ tự động xóa hầu hết các tài nguyên, nhưng một số cần xóa thủ công.

## Bước 1: Xóa S3 Bucket Contents

CloudFormation không thể xóa S3 buckets có chứa objects. Bạn cần xóa contents trước:

```bash
# Lấy bucket names từ outputs
FRONTEND_BUCKET=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`FrontendBucketName`].OutputValue' \
  --output text)

# Xóa tất cả objects trong frontend bucket
aws s3 rm s3://$FRONTEND_BUCKET --recursive --region ap-southeast-1

# Nếu có backend bucket
BACKEND_BUCKET="workshop-aws-dev-backend-$(aws sts get-caller-identity --query Account --output text)-ap-southeast-1"
aws s3 rm s3://$BACKEND_BUCKET --recursive --region ap-southeast-1 2>/dev/null || true
```

## Bước 2: Xóa CloudFormation Stack

### Cách 1: Sử dụng Deploy Script

**Windows:**
```cmd
cd aws
deploy.bat delete
```

**Linux/Mac:**
```bash
cd aws
./deploy.sh delete
```

### Cách 2: Sử dụng AWS CLI

```bash
aws cloudformation delete-stack \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1
```

## Bước 3: Theo dõi Quá trình Xóa

```bash
# Kiểm tra status
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].StackStatus'

# Đợi stack bị xóa hoàn toàn (có thể mất 10-15 phút)
aws cloudformation wait stack-delete-complete \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1
```

**Qua AWS Console:**
1. Mở [CloudFormation Console](https://console.aws.amazon.com/cloudformation/)
2. Chọn stack `workshop-aws-dev`
3. Tab **Events**: Xem resources đang bị xóa
4. Stack sẽ biến mất khỏi danh sách khi xóa hoàn tất

## Bước 4: Xác nhận Tài nguyên đã bị Xóa

### Kiểm tra VPC

```bash
# Không nên thấy VPC của workshop
aws ec2 describe-vpcs \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
  --region ap-southeast-1
```

### Kiểm tra EC2 Instances

```bash
# Không nên thấy instances của workshop
aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
  --region ap-southeast-1 \
  --query 'Reservations[*].Instances[*].[InstanceId,State.Name]'
```

### Kiểm tra RDS

```bash
# Không nên thấy RDS instance (có thể có snapshot)
aws rds describe-db-instances \
  --region ap-southeast-1 \
  --query 'DBInstances[?DBInstanceIdentifier==`workshop-aws-dev-db`]'
```

### Kiểm tra S3 Buckets

```bash
# Buckets nên đã bị xóa
aws s3 ls | grep workshop-aws-dev
```

## Bước 5: Xóa RDS Snapshots (Optional)

CloudFormation tạo snapshot trước khi xóa RDS. Nếu không cần, xóa để tránh phí lưu trữ:

```bash
# List snapshots
aws rds describe-db-snapshots \
  --region ap-southeast-1 \
  --query 'DBSnapshots[?contains(DBSnapshotIdentifier,`workshop-aws-dev`)].DBSnapshotIdentifier'

# Xóa snapshot
aws rds delete-db-snapshot \
  --db-snapshot-identifier <snapshot-id> \
  --region ap-southeast-1
```

## Bước 6: Xóa CloudWatch Logs (Optional)

Log groups không tự động bị xóa:

```bash
# List log groups
aws logs describe-log-groups \
  --log-group-name-prefix "/aws/workshop-aws" \
  --region ap-southeast-1

# Xóa log groups
aws logs delete-log-group \
  --log-group-name "/aws/workshop-aws/dev/application" \
  --region ap-southeast-1
```

## Bước 7: Xóa EC2 Key Pair (Optional)

Nếu không cần key pair nữa:

```bash
aws ec2 delete-key-pair \
  --key-name workshop-aws-key \
  --region ap-southeast-1

# Xóa file .pem local
rm workshop-aws-key.pem
```

## Troubleshooting

### Stack Deletion Failed

Nếu stack deletion bị lỗi:

1. **Xem lỗi:**
```bash
aws cloudformation describe-stack-events \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'StackEvents[?ResourceStatus==`DELETE_FAILED`].[LogicalResourceId,ResourceStatusReason]' \
  --output table
```

2. **Các lỗi thường gặp:**

**Lỗi: "S3 bucket is not empty"**
- Xóa tất cả objects trong bucket
- Thử delete stack lại

**Lỗi: "Network interface is in use"**
- Đợi vài phút để ENIs được release
- Thử delete stack lại

**Lỗi: "Resource being used by another resource"**
- Xác định resource dependencies
- Xóa dependent resources trước

3. **Force delete:**
```bash
# Retain problematic resources và xóa stack
aws cloudformation delete-stack \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --retain-resources <ResourceLogicalId>

# Sau đó xóa resources thủ công
```

## Checklist Cleanup

Đảm bảo tất cả tài nguyên đã bị xóa:

- [ ] CloudFormation stack đã bị xóa
- [ ] S3 buckets đã bị xóa
- [ ] EC2 instances đã terminated
- [ ] RDS database đã bị xóa
- [ ] Load Balancer đã bị xóa
- [ ] VPC và subnets đã bị xóa
- [ ] CloudFront distribution đã bị disabled và xóa
- [ ] NAT Gateway đã bị xóa
- [ ] Elastic IPs đã bị released
- [ ] RDS snapshots đã bị xóa (optional)
- [ ] CloudWatch log groups đã bị xóa (optional)
- [ ] EC2 Key Pair đã bị xóa (optional)

## Xác nhận Không còn Chi phí

Sau 24-48 giờ, kiểm tra AWS Cost Explorer để đảm bảo không còn chi phí phát sinh từ workshop.

## Kết luận

Bạn đã hoàn thành workshop và dọn dẹp tất cả tài nguyên thành công! 

**Những gì bạn đã học:**
✅ Triển khai full-stack application trên AWS
✅ Infrastructure as Code với CloudFormation
✅ AWS networking và security best practices
✅ Cost optimization strategies
✅ Monitoring và troubleshooting

**Tài nguyên tiếp theo:**
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [AWS Solutions Library](https://aws.amazon.com/solutions/)
- [AWS Workshops](https://workshops.aws/)

Cảm ơn bạn đã tham gia workshop! 🎉

