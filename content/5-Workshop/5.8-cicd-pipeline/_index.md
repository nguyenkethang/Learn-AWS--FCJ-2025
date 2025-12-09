---
title: "CI/CD Pipeline Setup"
date: 2025-12-08
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

## Overview

In this section, you will set up a complete CI/CD pipeline using AWS CodePipeline, CodeBuild, and GitLab CI/CD to automate the build and deployment process for both backend and frontend applications.

## Architecture

```
GitLab → S3 (Artifacts) → CodePipeline → CodeBuild (Backend) → EC2
                                      ↓
                                      CodeBuild (Frontend) → S3/CloudFront
```

## CI/CD Components

### 1. GitLab CI/CD
- Automatically builds and packages source code
- Uploads artifacts to S3
- Triggers AWS CodePipeline

### 2. AWS CodePipeline
- Orchestrates the entire deployment workflow
- Monitors S3 for new artifacts
- Triggers CodeBuild projects

### 3. AWS CodeBuild
- **Backend Build**: Compiles Spring Boot application to JAR
- **Frontend Build**: Builds React application with Vite
- Deploys to respective AWS services

## Step 1: Configure GitLab CI/CD

### 1.1. Set GitLab CI/CD Variables

In your GitLab project, go to **Settings → CI/CD → Variables** and add:

| Variable | Value | Protected | Masked |
|----------|-------|-----------|--------|
| `AWS_ACCESS_KEY_ID` | Your AWS Access Key | ✅ | ✅ |
| `AWS_SECRET_ACCESS_KEY` | Your AWS Secret Key | ✅ | ✅ |

### 1.2. Review GitLab CI Configuration

The `.gitlab-ci.yml` file in your project root:

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
    - echo "📦 Creating source.zip..."
    - |
      apk add zip
      zip -r source.zip . \
        -x "*.git*" \
        -x "node_modules/*" \
        -x ".idea/*" \
        -x "target/*" \
        -x "*.zip"
    - echo "📤 Uploading to S3..."
    - |
      aws s3 cp source.zip \
        s3://workshop-aws-dev-artifacts-502310717700-ap-southeast-1/source.zip
    - echo "✅ Upload completed! CodePipeline will trigger automatically."
  only:
    - main
  when: on_success
```

**What it does:**
- Packages entire project into `source.zip`
- Uploads to S3 artifacts bucket
- Triggers CodePipeline automatically

## Step 2: Deploy CodePipeline with CloudFormation

### 2.1. Review Pipeline Template

The `cicd-pipeline.yaml` CloudFormation template creates:
- CodePipeline with S3 source
- CodeBuild project for backend
- CodeBuild project for frontend
- IAM roles and permissions

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

### 2.3. Wait for Stack Creation

```bash
aws cloudformation wait stack-create-complete \
  --stack-name workshop-aws-dev-cicd \
  --region ap-southeast-1
```

**Expected time:** 3-5 minutes

## Step 3: Configure CodeBuild Projects

### 3.1. Backend BuildSpec

CodeBuild uses `buildspec-backend.yml`:

```yaml
version: 0.2

phases:
  pre_build:
    commands:
      - echo "Installing Maven..."
      - yum install -y maven
  
  build:
    commands:
      - echo "Building Backend JAR..."
      - cd BE/workshop_BE
      - mvn clean package -DskipTests
  
  post_build:
    commands:
      - echo "Uploading JAR to S3..."
      - aws s3 cp target/workshop-0.0.1-SNAPSHOT.jar \
          s3://workshop-aws-dev-backend-502310717700-ap-southeast-1/jars/
      - echo "Deploying to EC2..."
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

CodeBuild uses `buildspec-frontend.yml`:

```yaml
version: 0.2

phases:
  pre_build:
    commands:
      - echo "Installing Node.js..."
      - curl -sL https://rpm.nodesource.com/setup_18.x | bash -
      - yum install -y nodejs
  
  build:
    commands:
      - echo "Building Frontend..."
      - cd FE
      - npm install
      - npm run build
  
  post_build:
    commands:
      - echo "Deploying to S3..."
      - aws s3 sync dist/ \
          s3://workshop-aws-dev-frontend-502310717700-ap-southeast-1/ \
          --delete
      - echo "Invalidating CloudFront..."
      - aws cloudfront create-invalidation \
          --distribution-id E3K48K7CPOOLHZ \
          --paths "/*"

artifacts:
  files:
    - 'FE/dist/**/*'
```

## Step 4: Test CI/CD Pipeline

### 4.1. Trigger Pipeline from GitLab

Make a code change and push to `main` branch:

```bash
git add .
git commit -m "Test CI/CD pipeline"
git push origin main
```

### 4.2. Monitor GitLab Pipeline

1. Go to GitLab → **CI/CD → Pipelines**
2. Watch the `deploy-to-aws` job
3. Verify successful upload to S3

### 4.3. Monitor AWS CodePipeline

1. Go to AWS Console → **CodePipeline**
2. Select `workshop-aws-dev-pipeline`
3. Watch the pipeline stages:
   - **Source**: Detects new `source.zip` in S3
   - **Build-Backend**: Builds JAR and deploys to EC2
   - **Build-Frontend**: Builds React app and deploys to S3/CloudFront

### 4.4. Check Build Logs

For detailed logs:

1. Click on **Details** in any stage
2. View **Build logs** in CodeBuild
3. Check for errors or warnings

## Step 5: Verify Deployment

### 5.1. Test Backend API

```bash
curl https://98385v3jef.execute-api.ap-southeast-1.amazonaws.com/dev/dna_service/actuator/health
```

**Expected response:**
```json
{"status":"UP"}
```

### 5.2. Test Frontend

Open browser and navigate to:
```
https://d3gmmg22uirq0t.cloudfront.net
```

Verify the application loads with latest changes.

## Pipeline Flow

**Step-by-step flow:**

1. **GitLab Commit** → Developer pushes code to main branch
2. **GitLab CI** → Builds and creates source.zip
3. **S3 Bucket** → Stores source.zip artifact
4. **CodePipeline** → Detects new artifact and triggers builds
5. **CodeBuild Backend** → Builds JAR and deploys to EC2
6. **CodeBuild Frontend** → Builds React app and deploys to S3/CloudFront
7. **CloudWatch Logs** → Monitors all build and deployment activities

## Troubleshooting

### Pipeline Not Triggering

**Issue**: CodePipeline doesn't start after GitLab push

**Solutions**:
1. Check S3 bucket for `source.zip`
2. Verify CodePipeline source configuration
3. Check IAM permissions for CodePipeline

### Backend Build Fails

**Issue**: CodeBuild backend fails with Maven errors

**Solutions**:
1. Check `buildspec-backend.yml` syntax
2. Verify Maven dependencies in `pom.xml`
3. Check CodeBuild logs for specific errors
4. Ensure EC2 instance has SSM Agent running

### Frontend Build Fails

**Issue**: CodeBuild frontend fails with npm errors

**Solutions**:
1. Check `buildspec-frontend.yml` syntax
2. Verify `package.json` dependencies
3. Check Node.js version compatibility
4. Ensure S3 bucket permissions are correct

### Deployment Fails

**Issue**: Build succeeds but deployment fails

**Solutions**:
1. Check EC2 Security Groups allow SSM
2. Verify S3 bucket names are correct
3. Check CloudFront distribution ID
4. Review IAM role permissions

## Best Practices

### 1. Environment Variables
- Store sensitive data in GitLab CI/CD variables
- Use AWS Systems Manager Parameter Store for application configs
- Never commit credentials to Git

### 2. Build Optimization
- Cache dependencies (Maven `.m2`, npm `node_modules`)
- Use smaller Docker images for faster builds
- Parallelize independent build stages

### 3. Deployment Strategy
- Use blue-green deployment for zero downtime
- Implement health checks before routing traffic
- Keep rollback capability ready

### 4. Monitoring
- Enable CloudWatch Logs for all CodeBuild projects
- Set up SNS notifications for pipeline failures
- Monitor build times and optimize bottlenecks

## Cost Optimization

### CodeBuild Pricing
- **Build minutes**: $0.005 per minute (general1.small)
- **Typical build**: 5-10 minutes
- **Cost per build**: ~$0.025-0.05

### CodePipeline Pricing
- **Active pipeline**: $1.00 per month
- **Free tier**: 1 active pipeline per month

### Estimated Monthly Cost
- **10 deployments/day**: ~$15-20/month
- **Includes**: CodePipeline + CodeBuild + S3 storage

## Summary

You have successfully set up a complete CI/CD pipeline that:

✅ Automatically builds and packages code from GitLab  
✅ Uploads artifacts to S3  
✅ Triggers AWS CodePipeline on changes  
✅ Builds backend JAR with Maven  
✅ Builds frontend with Vite  
✅ Deploys backend to EC2  
✅ Deploys frontend to S3/CloudFront  
✅ Provides monitoring and logging  

**Next**: [Clean Up Resources](../5.9-cleanup/)
