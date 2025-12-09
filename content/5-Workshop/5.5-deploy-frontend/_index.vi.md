---
title: "Triển khai Frontend"
date: 2025-12-08
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

## Tổng quan

Trong bước này, bạn sẽ build React frontend và deploy lên S3, sau đó phân phối qua CloudFront CDN để đảm bảo hiệu suất cao và độ trễ thấp cho người dùng toàn cầu.

## Bước 1: Cấu hình API Endpoint

Lấy API Gateway URL từ CloudFormation outputs:

```bash
API_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`APIGatewayURL`].OutputValue' \
  --output text)

echo "API URL: $API_URL"
```

Cập nhật file `FE/.env`:

```bash
cd FE

cat > .env <<EOF
VITE_API_URL=${API_URL}/dna_service
VITE_APP_NAME=DNA Analysis Workshop
VITE_APP_VERSION=1.0.0
EOF
```

Hoặc cập nhật file config trực tiếp `FE/src/config/api.ts`:

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

## Bước 2: Install Dependencies

```bash
cd FE

# Install npm packages
npm install

# Verify installation
npm list --depth=0
```

## Bước 3: Build Frontend

```bash
# Build production bundle
npm run build

# Kiểm tra build output
ls -lh dist/

# Xem cấu trúc files
tree dist/ -L 2
```

**Kết quả mong đợi:**
```
dist/
├── index.html
├── assets/
│   ├── index-[hash].js
│   ├── index-[hash].css
│   └── [other assets]
└── vite.svg
```

## Bước 4: Upload lên S3

Lấy S3 bucket name từ outputs:

```bash
FRONTEND_BUCKET=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`FrontendBucketName`].OutputValue' \
  --output text)

echo "Frontend Bucket: $FRONTEND_BUCKET"
```

Upload files lên S3:

```bash
# Sync tất cả files
aws s3 sync dist/ s3://${FRONTEND_BUCKET}/ \
  --delete \
  --region ap-southeast-1

# Set cache control cho static assets
aws s3 cp dist/assets/ s3://${FRONTEND_BUCKET}/assets/ \
  --recursive \
  --cache-control "max-age=31536000" \
  --region ap-southeast-1

# Set no-cache cho index.html
aws s3 cp dist/index.html s3://${FRONTEND_BUCKET}/ \
  --cache-control "no-cache,no-store,must-revalidate" \
  --region ap-southeast-1

# Verify upload
aws s3 ls s3://${FRONTEND_BUCKET}/ --recursive
```

## Bước 5: Invalidate CloudFront Cache

Sau khi upload, cần invalidate CloudFront cache để users nhận được phiên bản mới:

```bash
# Lấy CloudFront Distribution ID
DIST_ID=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDistributionId`].OutputValue' \
  --output text)

echo "Distribution ID: $DIST_ID"

# Tạo invalidation
aws cloudfront create-invalidation \
  --distribution-id $DIST_ID \
  --paths "/*" \
  --region ap-southeast-1

# Theo dõi invalidation status
aws cloudfront get-invalidation \
  --distribution-id $DIST_ID \
  --id <invalidation-id>
```

**Lưu ý:** Invalidation mất 5-10 phút để hoàn thành.

## Bước 6: Truy cập Frontend

Lấy CloudFront domain name:

```bash
CLOUDFRONT_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDomainName`].OutputValue' \
  --output text)

echo "Frontend URL: https://${CLOUDFRONT_URL}"
```

Mở trình duyệt và truy cập URL trên.

## Bước 7: Kiểm tra Frontend

### Test Basic Functionality

1. **Trang chủ:** Kiểm tra trang load đúng
2. **Navigation:** Test các menu và routing
3. **API Connection:** Mở Developer Tools → Network tab
4. **Console Errors:** Kiểm tra không có lỗi JavaScript

### Test Authentication

```bash
# Test login endpoint
curl -X POST https://${CLOUDFRONT_URL}/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"test","password":"test123"}'
```

### Test CORS

Mở Developer Tools → Console và chạy:

```javascript
fetch('${API_URL}/dna_service/actuator/health')
  .then(res => res.json())
  .then(data => console.log('API Response:', data))
  .catch(err => console.error('CORS Error:', err));
```

## Bước 8: Cấu hình Custom Domain (Optional)

Nếu bạn có domain name:

### 1. Tạo SSL Certificate trong ACM

```bash
# Certificate phải tạo trong us-east-1 cho CloudFront
aws acm request-certificate \
  --domain-name yourdomain.com \
  --subject-alternative-names www.yourdomain.com \
  --validation-method DNS \
  --region us-east-1
```

### 2. Validate Certificate

Thêm CNAME records vào DNS theo hướng dẫn từ ACM.

### 3. Cập nhật CloudFront Distribution

```bash
aws cloudfront update-distribution \
  --id $DIST_ID \
  --distribution-config file://cloudfront-config.json
```

### 4. Cập nhật Route 53

```bash
# Tạo A record alias đến CloudFront
aws route53 change-resource-record-sets \
  --hosted-zone-id <zone-id> \
  --change-batch file://route53-changes.json
```

## Deployment Script

Tạo script tự động hóa deployment:

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

Sử dụng script:

```bash
./deploy-frontend.sh
```

## Troubleshooting

### Build Failed

**Lỗi: "Module not found"**
```bash
# Xóa node_modules và reinstall
rm -rf node_modules package-lock.json
npm install
```

**Lỗi: "Out of memory"**
```bash
# Tăng memory cho Node.js
export NODE_OPTIONS="--max-old-space-size=4096"
npm run build
```

### Upload Failed

**Lỗi: "Access Denied"**
- Kiểm tra AWS credentials
- Verify IAM permissions cho S3

**Lỗi: "Bucket does not exist"**
- Kiểm tra bucket name
- Verify CloudFormation stack đã tạo bucket

### CloudFront Issues

**Trang không load:**
- Đợi CloudFront distribution deploy (5-10 phút)
- Check distribution status: `Deployed`

**Nhận được phiên bản cũ:**
- Tạo invalidation mới
- Clear browser cache (Ctrl+Shift+R)

**CORS errors:**
- Kiểm tra API Gateway CORS configuration
- Verify backend CORS settings

### API Connection Failed

```bash
# Test API từ browser console
fetch('${API_URL}/dna_service/actuator/health')
  .then(res => res.text())
  .then(data => console.log(data))
```

Nếu lỗi:
- Kiểm tra API Gateway URL đúng
- Verify backend đang chạy
- Check Security Groups

## Xác nhận Deployment thành công

Checklist:

- [ ] Frontend build thành công
- [ ] Files đã upload lên S3
- [ ] CloudFront invalidation hoàn thành
- [ ] Trang web load đúng qua CloudFront URL
- [ ] Không có lỗi trong browser console
- [ ] API calls hoạt động (check Network tab)
- [ ] Authentication flow hoạt động
- [ ] Routing giữa các pages hoạt động

## Tiếp theo

Sau khi frontend đã sẵn sàng:

➡️ [Kiểm tra và Xác thực](../5.6-testing/)

