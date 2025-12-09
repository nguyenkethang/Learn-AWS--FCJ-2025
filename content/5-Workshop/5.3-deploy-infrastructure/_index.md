---
title: "Deploy Infrastructure with CloudFormation"
date: 2025-12-08
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

## Overview

In this step, you will deploy the complete AWS infrastructure using CloudFormation template. The template will create VPC, subnets, EC2 instances, RDS database, Load Balancer, S3 buckets, CloudFront distribution, and all necessary resources.

## Validate Template

Before deployment, validate the template to ensure no syntax errors:

```bash
cd aws
aws cloudformation validate-template \
  --template-body file://infrastructure.yaml \
  --region ap-southeast-1
```

**Expected result:** Information about parameters, outputs, and template description.

## Deploy Stack

### Method 1: Using Deploy Script (Recommended)

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

The script will automatically:
- Validate template
- Create CloudFormation stack
- Monitor deployment progress
- Display outputs when complete

### Method 2: Using AWS CLI

```bash
aws cloudformation create-stack \
  --stack-name workshop-aws-dev \
  --template-body file://infrastructure.yaml \
  --parameters file://parameters.json \
  --capabilities CAPABILITY_NAMED_IAM \
  --region ap-southeast-1
```

## Monitor Progress

### Via AWS Console

1. Open [CloudFormation Console](https://console.aws.amazon.com/cloudformation/)
2. Select stack `workshop-aws-dev`
3. **Events** tab: View resources being created
4. **Resources** tab: View resource list
5. **Outputs** tab: View outputs (after completion)

### Via AWS CLI

```bash
# Check status
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].StackStatus'

# View events
aws cloudformation describe-stack-events \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --max-items 10
```

## Deployment Time

Stack creation takes approximately **15-20 minutes**:

- VPC and Networking: 2-3 minutes
- NAT Gateway: 2-3 minutes
- RDS Database: 5-7 minutes
- EC2 Auto Scaling Group: 3-5 minutes
- Load Balancer: 2-3 minutes
- CloudFront Distribution: 5-10 minutes
- VPC Endpoints: 2-3 minutes

## View Outputs

After stack creation succeeds (Status: `CREATE_COMPLETE`), get outputs:

```bash
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs' \
  --output table
```

**Important Outputs:**

| Output Key | Description | Example |
|------------|-------------|---------|
| `VPCId` | VPC ID | vpc-0123456789abcdef0 |
| `FrontendBucketName` | S3 bucket for frontend | workshop-aws-dev-frontend-123456789012-ap-southeast-1 |
| `CloudFrontDomainName` | CloudFront URL | d1234567890abc.cloudfront.net |
| `ALBDNSName` | Load Balancer DNS | workshop-aws-dev-alb-123456789.ap-southeast-1.elb.amazonaws.com |
| `RDSEndpoint` | Database endpoint | workshop-aws-dev-db.xxxxx.ap-southeast-1.rds.amazonaws.com |
| `APIGatewayURL` | API Gateway URL | https://xxxxx.execute-api.ap-southeast-1.amazonaws.com/dev |
| `CognitoUserPoolId` | Cognito User Pool ID | ap-southeast-1_xxxxxxxxx |

**Save these values** - you'll need them for next steps!

## Verify Created Resources

### 1. VPC and Networking

```bash
# Get VPC ID
VPC_ID=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`VPCId`].OutputValue' \
  --output text)

# View VPC details
aws ec2 describe-vpcs --vpc-ids $VPC_ID --region ap-southeast-1

# View Subnets
aws ec2 describe-subnets \
  --filters "Name=vpc-id,Values=$VPC_ID" \
  --region ap-southeast-1 \
  --query 'Subnets[*].[SubnetId,CidrBlock,AvailabilityZone,Tags[?Key==`Name`].Value|[0]]' \
  --output table
```

### 2. EC2 Instances

```bash
# View EC2 instances in Auto Scaling Group
aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
  --region ap-southeast-1 \
  --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PrivateIpAddress,PublicIpAddress]' \
  --output table
```

### 3. RDS Database

```bash
# View RDS instance
aws rds describe-db-instances \
  --db-instance-identifier workshop-aws-dev-db \
  --region ap-southeast-1 \
  --query 'DBInstances[0].[DBInstanceIdentifier,DBInstanceStatus,Endpoint.Address,Endpoint.Port]' \
  --output table
```

## Troubleshooting

### Stack Creation Failed

If stack creation fails:

1. **View Events to find error:**
```bash
aws cloudformation describe-stack-events \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'StackEvents[?ResourceStatus==`CREATE_FAILED`].[LogicalResourceId,ResourceStatusReason]' \
  --output table
```

2. **Common errors:**

**Error: "Key pair does not exist"**
- Check key pair name in `parameters.json`
- Ensure key pair exists in ap-southeast-1 region

**Error: "Invalid AMI ID"**
- Update AMI ID in `infrastructure.yaml`
- Use AMI ID appropriate for your region

**Error: "Insufficient permissions"**
- Check IAM permissions of user
- Need CloudFormation, EC2, VPC, RDS, S3, IAM permissions

3. **Rollback and retry:**
```bash
# Delete failed stack
aws cloudformation delete-stack \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1

# Wait for stack deletion
aws cloudformation wait stack-delete-complete \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1

# Try creating again
aws cloudformation create-stack \
  --stack-name workshop-aws-dev \
  --template-body file://infrastructure.yaml \
  --parameters file://parameters.json \
  --capabilities CAPABILITY_NAMED_IAM \
  --region ap-southeast-1
```

## Confirm Successful Deployment

Checklist to confirm infrastructure is ready:

- [ ] Stack status is `CREATE_COMPLETE`
- [ ] VPC and subnets created
- [ ] EC2 instances running (State: `running`)
- [ ] RDS database status is `available`
- [ ] Load Balancer status is `active`
- [ ] S3 buckets created
- [ ] CloudFront distribution status is `Deployed`
- [ ] All outputs have values

## Next Steps

After infrastructure is ready, you can:

➡️ [Configure and Deploy Backend Application](../5.4-deploy-backend/)

