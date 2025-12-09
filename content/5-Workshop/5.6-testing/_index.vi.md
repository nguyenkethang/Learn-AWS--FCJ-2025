---
title: "Kiểm tra và Xác thực"
date: 2025-12-08
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

## Tổng quan

Trong bước này, bạn sẽ thực hiện các test cases để xác nhận ứng dụng hoạt động đúng end-to-end, từ frontend qua API Gateway, Load Balancer, đến backend và database.

## Bước 1: Kiểm tra Infrastructure

### Verify All Services Running

```bash
# Check CloudFormation stack status
aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].StackStatus'

# Expected: CREATE_COMPLETE

# Check EC2 instances
aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
            "Name=instance-state-name,Values=running" \
  --region ap-southeast-1 \
  --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PrivateIpAddress]' \
  --output table

# Check RDS status
aws rds describe-db-instances \
  --db-instance-identifier workshop-aws-dev-db \
  --region ap-southeast-1 \
  --query 'DBInstances[0].[DBInstanceIdentifier,DBInstanceStatus]' \
  --output table

# Expected: available

# Check Load Balancer
aws elbv2 describe-load-balancers \
  --names workshop-aws-dev-alb \
  --region ap-southeast-1 \
  --query 'LoadBalancers[0].[LoadBalancerName,State.Code]' \
  --output table

# Expected: active
```

## Bước 2: Test Backend API

### Get API URLs

```bash
ALB_DNS=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`ALBDNSName`].OutputValue' \
  --output text)

API_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`APIGatewayURL`].OutputValue' \
  --output text)

echo "ALB DNS: $ALB_DNS"
echo "API Gateway URL: $API_URL"
```

### Test Health Endpoint

```bash
# Test qua ALB
curl -v http://${ALB_DNS}/dna_service/actuator/health

# Test qua API Gateway
curl -v ${API_URL}/dna_service/actuator/health

# Expected response:
# {"status":"UP"}
```

### Test User Registration

```bash
# Register new user
curl -X POST ${API_URL}/dna_service/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "email": "test@example.com",
    "password": "Test123!@#",
    "fullName": "Test User"
  }'

# Expected: 200 OK with user data
```

### Test User Login

```bash
# Login
curl -X POST ${API_URL}/dna_service/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "password": "Test123!@#"
  }'

# Expected: 200 OK with JWT token
# Save token for next requests
TOKEN="<jwt-token-from-response>"
```

### Test Protected Endpoints

```bash
# Get user profile
curl -X GET ${API_URL}/dna_service/user/profile \
  -H "Authorization: Bearer ${TOKEN}"

# Expected: 200 OK with user profile data
```

## Bước 3: Test Frontend

### Access Frontend

```bash
CLOUDFRONT_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDomainName`].OutputValue' \
  --output text)

echo "Frontend URL: https://${CLOUDFRONT_URL}"
```

Mở trình duyệt và truy cập URL trên.

### Manual Testing Checklist

**1. Trang chủ (Home Page)**
- [ ] Trang load thành công
- [ ] Logo và branding hiển thị đúng
- [ ] Navigation menu hoạt động
- [ ] Không có lỗi trong Console

**2. User Registration**
- [ ] Form validation hoạt động
- [ ] Có thể đăng ký user mới
- [ ] Hiển thị thông báo thành công
- [ ] Redirect đến login page

**3. User Login**
- [ ] Có thể đăng nhập với credentials vừa tạo
- [ ] JWT token được lưu trong localStorage
- [ ] Redirect đến dashboard sau login
- [ ] User menu hiển thị username

**4. DNA Analysis**
- [ ] Có thể upload DNA sequence file
- [ ] File validation hoạt động
- [ ] Analysis progress được hiển thị
- [ ] Kết quả analysis hiển thị đúng
- [ ] Có thể xem history

**5. User Profile**
- [ ] Hiển thị thông tin user
- [ ] Có thể update profile
- [ ] Avatar upload hoạt động (nếu có)
- [ ] Logout hoạt động đúng

**6. Responsive Design**
- [ ] Mobile view hoạt động tốt
- [ ] Tablet view hoạt động tốt
- [ ] Desktop view hoạt động tốt

## Bước 4: Test Database Connection

### Connect to RDS

```bash
# Get RDS endpoint
RDS_ENDPOINT=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`RDSEndpoint`].OutputValue' \
  --output text)

# Connect via MySQL client (từ EC2 hoặc local nếu có public access)
mysql -h ${RDS_ENDPOINT} -u admin -p workshop_aws
```

### Verify Tables Created

```sql
-- Show all tables
SHOW TABLES;

-- Expected tables:
-- users, dna_sequences, analysis_results, etc.

-- Check user data
SELECT id, username, email, created_at FROM users;

-- Check DNA analysis data
SELECT id, user_id, sequence_name, status, created_at FROM dna_sequences;

-- Exit
EXIT;
```

## Bước 5: Load Testing (Optional)

### Install Apache Bench

```bash
# Ubuntu/Debian
sudo apt-get install apache2-utils

# MacOS
brew install httpd

# Windows
# Download from Apache website
```

### Run Load Test

```bash
# Test health endpoint
ab -n 1000 -c 10 http://${ALB_DNS}/dna_service/actuator/health

# Test login endpoint
ab -n 100 -c 5 -p login-data.json -T application/json \
  ${API_URL}/dna_service/auth/login
```

### Monitor During Load Test

```bash
# Watch CloudWatch metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=AutoScalingGroupName,Value=workshop-aws-dev-asg \
  --start-time $(date -u -d '5 minutes ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 60 \
  --statistics Average \
  --region ap-southeast-1
```

## Bước 6: Security Testing

### Test HTTPS Enforcement

```bash
# CloudFront should redirect HTTP to HTTPS
curl -I http://${CLOUDFRONT_URL}

# Expected: 301 redirect to https://
```

### Test CORS

```bash
# Test preflight request
curl -X OPTIONS ${API_URL}/dna_service/auth/login \
  -H "Origin: https://${CLOUDFRONT_URL}" \
  -H "Access-Control-Request-Method: POST" \
  -H "Access-Control-Request-Headers: Content-Type" \
  -v

# Expected: CORS headers in response
```

### Test SQL Injection Protection

```bash
# Try SQL injection in login
curl -X POST ${API_URL}/dna_service/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "admin'\'' OR '\''1'\''='\''1",
    "password": "anything"
  }'

# Expected: 401 Unauthorized (not SQL error)
```

### Test XSS Protection

Trong browser console:

```javascript
// Try XSS in input fields
document.querySelector('input[name="username"]').value = '<script>alert("XSS")</script>';
```

Expected: Script không được execute, được escape hoặc sanitize.

## Bước 7: Performance Testing

### Measure Page Load Time

Mở Chrome DevTools → Network tab:

- **First Contentful Paint (FCP):** < 1.5s
- **Largest Contentful Paint (LCP):** < 2.5s
- **Time to Interactive (TTI):** < 3.5s
- **Total Page Size:** < 2MB

### Test API Response Time

```bash
# Measure API response time
time curl -s ${API_URL}/dna_service/actuator/health > /dev/null

# Expected: < 200ms
```

### Test CloudFront Caching

```bash
# First request (MISS)
curl -I https://${CLOUDFRONT_URL}/assets/index.js

# Second request (HIT)
curl -I https://${CLOUDFRONT_URL}/assets/index.js

# Check X-Cache header: Hit from cloudfront
```

## Troubleshooting Common Issues

### API Returns 502 Bad Gateway

```bash
# Check backend health
curl http://${ALB_DNS}/dna_service/actuator/health

# Check target group health
aws elbv2 describe-target-health \
  --target-group-arn <arn> \
  --region ap-southeast-1

# Check EC2 logs
aws ssm start-session --target <instance-id>
tail -f /opt/workshop/application.log
```

### Frontend Shows CORS Error

- Verify API Gateway CORS configuration
- Check backend CORS settings in application.properties
- Ensure CloudFront origin is whitelisted

### Database Connection Timeout

- Check RDS Security Group allows EC2 traffic
- Verify RDS endpoint in application.properties
- Test connection from EC2:
  ```bash
  telnet ${RDS_ENDPOINT} 3306
  ```

### Slow Page Load

- Check CloudFront cache hit ratio
- Optimize images and assets
- Enable gzip compression
- Review CloudWatch metrics

## Test Results Documentation

Tạo file test-results.md:

```markdown
# Workshop Test Results

## Date: 2025-12-08
## Tester: [Your Name]

### Infrastructure Tests
- [x] CloudFormation stack: CREATE_COMPLETE
- [x] EC2 instances: Running
- [x] RDS database: Available
- [x] Load Balancer: Active

### Backend API Tests
- [x] Health endpoint: OK
- [x] User registration: OK
- [x] User login: OK
- [x] Protected endpoints: OK

### Frontend Tests
- [x] Page load: OK
- [x] User registration: OK
- [x] User login: OK
- [x] DNA analysis: OK
- [x] Responsive design: OK

### Performance Tests
- [x] Page load time: 1.2s
- [x] API response time: 150ms
- [x] CloudFront cache: Working

### Security Tests
- [x] HTTPS enforcement: OK
- [x] CORS: OK
- [x] SQL injection protection: OK
- [x] XSS protection: OK

## Issues Found
None

## Recommendations
- Enable CloudFront compression
- Add more CloudWatch alarms
- Implement rate limiting
```

## Xác nhận Testing hoàn thành

Checklist:

- [ ] Tất cả infrastructure services đang chạy
- [ ] Backend API endpoints hoạt động
- [ ] Frontend load và hoạt động đúng
- [ ] Database connection hoạt động
- [ ] User authentication flow hoạt động
- [ ] DNA analysis features hoạt động
- [ ] Performance đạt yêu cầu
- [ ] Security tests pass
- [ ] Test results được document

## Tiếp theo

Sau khi testing hoàn thành:

➡️ [Giám sát và Xử lý sự cố](../5.7-monitoring/)

