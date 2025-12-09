---
title: "Deploy Frontend"
date: 2025-12-08
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

## Overview

In this step, you will build the React frontend and deploy it to S3, then distribute it via CloudFront CDN to ensure high performance and low latency for global users.

## Step 1: Configure API Endpoint

Get API Gateway URL from CloudFormation outputs:

```bash
API_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`APIGatewayURL`].OutputValue' \
  --output text)

echo "API URL: $API_URL"
```

Update file `FE/.env`:

```bash
cd FE

cat > .env <<EOF
VITE_API_URL=${API_URL}/dna_service
VITE_APP_NAME=DNA Analysis Workshop
VITE_APP_VERSION=1.0.0
EOF
```

Or update config file directly `FE/src/config/api.ts`:

```typescript
export const API_BASE_URL = process.env.VITE_API_URL || 'http://localhost:8080/dna_service';
export const API_TIMEOUT = 30000;

export const API_ENDPOINTS = {
  AUTH: {
    LOGIN: '/auth/login',
    REGISTER: '/auth/register',
    LOGOUT: '/auth/logout',
    REFRESH: '/auth/refresh',
  },
  DNA: {
    ANALYZE: '/dna/analyze',
    HISTORY: '/dna/history',
    RESULT: '/dna/result',
  },
  USER: {
    PROFILE: '/user/profile',
    UPDATE: '/user/update',
  },
};
```

## Step 2: Install Dependencies

```bash
cd FE

# Install npm packages
npm install

# Verify installation
npm list --depth=0
```

## Step 3: Build Frontend

```bash
# Build production bundle
npm run build

# Check build output
ls -lh dist/

# View file structure
tree dist/ -L 2
```

**Expected result:**
```
dist/
├── index.html
├── assets/
│   ├── index-[hash].js
│   ├── index-[hash].css
│   └── [other assets]
└── vite.svg
```

## Step 4: Upload to S3

Get S3 bucket name from outputs:

```bash
FRONTEND_BUCKET=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`FrontendBucketName`].OutputValue' \
  --output text)

echo "Frontend Bucket: $FRONTEND_BUCKET"
```

Upload files to S3:

```bash
# Sync all files
aws s3 sync dist/ s3://${FRONTEND_BUCKET}/ \
  --delete \
  --region ap-southeast-1

# Set cache control for static assets
aws s3 cp dist/assets/ s3://${FRONTEND_BUCKET}/assets/ \
  --recursive \
  --cache-control "max-age=31536000" \
  --region ap-southeast-1

# Set no-cache for index.html
aws s3 cp dist/index.html s3://${FRONTEND_BUCKET}/ \
  --cache-control "no-cache,no-store,must-revalidate" \
  --region ap-southeast-1

# Verify upload
aws s3 ls s3://${FRONTEND_BUCKET}/ --recursive
```

## Step 5: Invalidate CloudFront Cache

After upload, need to invalidate CloudFront cache so users receive the new version:

```bash
# Get CloudFront Distribution ID
DIST_ID=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDistributionId`].OutputValue' \
  --output text)

echo "Distribution ID: $DIST_ID"

# Create invalidation
aws cloudfront create-invalidation \
  --distribution-id $DIST_ID \
  --paths "/*" \
  --region ap-southeast-1

# Monitor invalidation status
aws cloudfront get-invalidation \
  --distribution-id $DIST_ID \
  --id <invalidation-id>
```

**Note:** Invalidation takes 5-10 minutes to complete.

## Step 6: Access Frontend

Get CloudFront domain name:

```bash
CLOUDFRONT_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDomainName`].OutputValue' \
  --output text)

echo "Frontend URL: https://${CLOUDFRONT_URL}"
```

Open browser and access the URL above.

## Step 7: Verify Frontend

### Test Basic Functionality

1. **Home Page:** Check page loads correctly
2. **Navigation:** Test menus and routing
3. **API Connection:** Open Developer Tools → Network tab
4. **Console Errors:** Check for no JavaScript errors

### Test Authentication

```bash
# Test login endpoint
curl -X POST https://${CLOUDFRONT_URL}/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"test","password":"test123"}'
```

### Test CORS

Open Developer Tools → Console and run:

```javascript
fetch('${API_URL}/dna_service/actuator/health')
  .then(res => res.json())
  .then(data => console.log('API Response:', data))
  .catch(err => console.error('CORS Error:', err));
```

## Step 8: Configure Custom Domain (Optional)

If you have a domain name:

### 1. Create SSL Certificate in ACM

```bash
# Certificate must be created in us-east-1 for CloudFront
aws acm request-certificate \
  --domain-name yourdomain.com \
  --subject-alternative-names www.yourdomain.com \
  --validation-method DNS \
  --region us-east-1
```

### 2. Validate Certificate

Add CNAME records to DNS as instructed by ACM.

### 3. Update CloudFront Distribution

```bash
aws cloudfront update-distribution \
  --id $DIST_ID \
  --distribution-config file://cloudfront-config.json
```

### 4. Update Route 53

```bash
# Create A record alias to CloudFront
aws route53 change-resource-record-sets \
  --hosted-zone-id <zone-id> \
  --change-batch file://route53-changes.json
```

## Deployment Script

Create script to automate deployment:

```bash
cat > deploy-frontend.sh <<'EOF'
#!/bin/bash
set -e

echo "Building frontend..."
cd FE
npm run build

echo "Getting S3 bucket name..."
FRONTEND_BUCKET=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`FrontendBucketName`].OutputValue' \
  --output text)

echo "Uploading to S3..."
aws s3 sync dist/ s3://${FRONTEND_BUCKET}/ --delete --region ap-southeast-1

echo "Invalidating CloudFront cache..."
DIST_ID=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDistributionId`].OutputValue' \
  --output text)

aws cloudfront create-invalidation \
  --distribution-id $DIST_ID \
  --paths "/*" \
  --region ap-southeast-1

echo "Deployment complete!"
echo "Frontend URL: https://$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDomainName`].OutputValue' \
  --output text)"
EOF

chmod +x deploy-frontend.sh
```

Use script:

```bash
./deploy-frontend.sh
```

## Troubleshooting

### Build Failed

**Error: "Module not found"**
```bash
# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

**Error: "Out of memory"**
```bash
# Increase memory for Node.js
export NODE_OPTIONS="--max-old-space-size=4096"
npm run build
```

### Upload Failed

**Error: "Access Denied"**
- Check AWS credentials
- Verify IAM permissions for S3

**Error: "Bucket does not exist"**
- Check bucket name
- Verify CloudFormation stack created bucket

### CloudFront Issues

**Page won't load:**
- Wait for CloudFront distribution to deploy (5-10 minutes)
- Check distribution status: `Deployed`

**Receiving old version:**
- Create new invalidation
- Clear browser cache (Ctrl+Shift+R)

**CORS errors:**
- Check API Gateway CORS configuration
- Verify backend CORS settings

### API Connection Failed

```bash
# Test API from browser console
fetch('${API_URL}/dna_service/actuator/health')
  .then(res => res.text())
  .then(data => console.log(data))
```

If error:
- Check API Gateway URL is correct
- Verify backend is running
- Check Security Groups

## Confirm Successful Deployment

Checklist:

- [ ] Frontend built successfully
- [ ] Files uploaded to S3
- [ ] CloudFront invalidation completed
- [ ] Website loads correctly via CloudFront URL
- [ ] No errors in browser console
- [ ] API calls working (check Network tab)
- [ ] Authentication flow working
- [ ] Routing between pages working

## Next Steps

After frontend is ready:

➡️ [Testing and Validation](../5.6-testing/)

