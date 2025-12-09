---
title: "Clean Up Resources"
date: 2025-12-08
weight: 8
chapter: false
pre: " <b> 5.8 </b> "
---

## Overview

After completing the workshop, you need to delete all resources to avoid unexpected charges. CloudFormation will automatically delete most resources, but some require manual deletion.

## Step 1: Delete S3 Bucket Contents

CloudFormation cannot delete S3 buckets containing objects. Delete contents first:

```bash
# Get bucket names from outputs
FRONTEND_BUCKET=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`FrontendBucketName`].OutputValue' \
  --output text)

# Delete all objects in frontend bucket
aws s3 rm s3://$FRONTEND_BUCKET --recursive --region ap-southeast-1

# If backend bucket exists
BACKEND_BUCKET="workshop-aws-dev-backend-$(aws sts get-caller-identity --query Account --output text)-ap-southeast-1"
aws s3 rm s3://$BACKEND_BUCKET --recursive --region ap-southeast-1 2>/dev/null || true
```

## Step 2: Delete CloudFormation Stack

### Method 1: Using Deploy Script

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

### Method 2: Using AWS CLI

```bash
aws cloudformation delete-stack \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1
```

## Step 3: Monitor Deletion Progress

```bash
# Check status
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].StackStatus'

# Wait for stack deletion (may take 10-15 minutes)
aws cloudformation wait stack-delete-complete \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1
```

**Via AWS Console:**
1. Open [CloudFormation Console](https://console.aws.amazon.com/cloudformation/)
2. Select stack `workshop-aws-dev`
3. **Events** tab: View resources being deleted
4. Stack will disappear from list when deletion completes

## Step 4: Verify Resources Deleted

### Check VPC

```bash
# Should not see workshop VPC
aws ec2 describe-vpcs \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
  --region ap-southeast-1
```

### Check EC2 Instances

```bash
# Should not see workshop instances
aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
  --region ap-southeast-1 \
  --query 'Reservations[*].Instances[*].[InstanceId,State.Name]'
```

### Check RDS

```bash
# Should not see RDS instance (may have snapshot)
aws rds describe-db-instances \
  --region ap-southeast-1 \
  --query 'DBInstances[?DBInstanceIdentifier==`workshop-aws-dev-db`]'
```

### Check S3 Buckets

```bash
# Buckets should be deleted
aws s3 ls | grep workshop-aws-dev
```

## Step 5: Delete RDS Snapshots (Optional)

CloudFormation creates snapshot before deleting RDS. Delete if not needed:

```bash
# List snapshots
aws rds describe-db-snapshots \
  --region ap-southeast-1 \
  --query 'DBSnapshots[?contains(DBSnapshotIdentifier,`workshop-aws-dev`)].DBSnapshotIdentifier'

# Delete snapshot
aws rds delete-db-snapshot \
  --db-snapshot-identifier <snapshot-id> \
  --region ap-southeast-1
```

## Step 6: Delete CloudWatch Logs (Optional)

Log groups are not automatically deleted:

```bash
# List log groups
aws logs describe-log-groups \
  --log-group-name-prefix "/aws/workshop-aws" \
  --region ap-southeast-1

# Delete log groups
aws logs delete-log-group \
  --log-group-name "/aws/workshop-aws/dev/application" \
  --region ap-southeast-1
```

## Step 7: Delete EC2 Key Pair (Optional)

If key pair is no longer needed:

```bash
aws ec2 delete-key-pair \
  --key-name workshop-aws-key \
  --region ap-southeast-1

# Delete local .pem file
rm workshop-aws-key.pem
```

## Troubleshooting

### Stack Deletion Failed

If stack deletion fails:

1. **View error:**
```bash
aws cloudformation describe-stack-events \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'StackEvents[?ResourceStatus==`DELETE_FAILED`].[LogicalResourceId,ResourceStatusReason]' \
  --output table
```

2. **Common errors:**

**Error: "S3 bucket is not empty"**
- Delete all objects in bucket
- Retry stack deletion

**Error: "Network interface is in use"**
- Wait a few minutes for ENIs to be released
- Retry stack deletion

**Error: "Resource being used by another resource"**
- Identify resource dependencies
- Delete dependent resources first

3. **Force delete:**
```bash
# Retain problematic resources and delete stack
aws cloudformation delete-stack \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --retain-resources <ResourceLogicalId>

# Then delete resources manually
```

## Cleanup Checklist

Ensure all resources are deleted:

- [ ] CloudFormation stack deleted
- [ ] S3 buckets deleted
- [ ] EC2 instances terminated
- [ ] RDS database deleted
- [ ] Load Balancer deleted
- [ ] VPC and subnets deleted
- [ ] CloudFront distribution disabled and deleted
- [ ] NAT Gateway deleted
- [ ] Elastic IPs released
- [ ] RDS snapshots deleted (optional)
- [ ] CloudWatch log groups deleted (optional)
- [ ] EC2 Key Pair deleted (optional)

## Confirm No Ongoing Charges

After 24-48 hours, check AWS Cost Explorer to ensure no charges from workshop.

## Conclusion

You have successfully completed the workshop and cleaned up all resources!

**What you learned:**
✅ Deploy full-stack application on AWS
✅ Infrastructure as Code with CloudFormation
✅ AWS networking and security best practices
✅ Cost optimization strategies
✅ Monitoring and troubleshooting

**Next resources:**
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [AWS Solutions Library](https://aws.amazon.com/solutions/)
- [AWS Workshops](https://workshops.aws/)

Thank you for participating in this workshop! 🎉

