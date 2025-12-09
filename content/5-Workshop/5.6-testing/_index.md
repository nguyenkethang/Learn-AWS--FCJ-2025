---
title: "Testing and Validation"
date: 2025-12-08
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

## Overview

In this step, you will perform test cases to verify the application works correctly end-to-end, from frontend through API Gateway, Load Balancer, to backend and database.

## Step 1: Verify Infrastructure

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

## Step 2: Test Backend API

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
# Test via ALB
curl -v http://${ALB_DNS}/dna_service/actuator/health

# Test via API Gateway
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

## Step 3: Test Frontend

### Access Frontend

```bash
CLOUDFRONT_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`CloudFrontDomainName`].OutputValue' \
  --output text)

echo "Frontend URL: https://${CLOUDFRONT_URL}"
```

Open browser and access the URL above.

### Manual Testing Checklist

**1. Home Page**
- [ ] Page loads successfully
- [ ] Logo and branding display correctly
- [ ] Navigation menu works
- [ ] No errors in Console

**2. User Registration**
- [ ] Form validation works
- [ ] Can register new user
- [ ] Success message displays
- [ ] Redirects to login page

**3. User Login**
- [ ] Can login with created credentials
- [ ] JWT token saved in localStorage
- [ ] Redirects to dashboard after login
- [ ] User menu displays username

**4. DNA Analysis**
- [ ] Can upload DNA sequence file
- [ ] File validation works
- [ ] Analysis progress displays
- [ ] Analysis results display correctly
- [ ] Can view history

**5. User Profile**
- [ ] Displays user information
- [ ] Can update profile
- [ ] Avatar upload works (if available)
- [ ] Logout works correctly

**6. Responsive Design**
- [ ] Mobile view works well
- [ ] Tablet view works well
- [ ] Desktop view works well

## Step 4: Test Database Connection

### Connect to RDS

```bash
# Get RDS endpoint
RDS_ENDPOINT=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`RDSEndpoint`].OutputValue' \
  --output text)

# Connect via MySQL client (from EC2 or local if public access)
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

## Step 5: Load Testing (Optional)

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

## Step 6: Security Testing

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

In browser console:

```javascript
// Try XSS in input fields
document.querySelector('input[name="username"]').value = '<script>alert("XSS")</script>';
```

Expected: Script not executed, escaped or sanitized.

## Step 7: Performance Testing

### Measure Page Load Time

Open Chrome DevTools → Network tab:

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

Create test-results.md file:

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

## Confirm Testing Complete

Checklist:

- [ ] All infrastructure services running
- [ ] Backend API endpoints working
- [ ] Frontend loads and works correctly
- [ ] Database connection working
- [ ] User authentication flow working
- [ ] DNA analysis features working
- [ ] Performance meets requirements
- [ ] Security tests pass
- [ ] Test results documented

## Next Steps

After testing is complete:

➡️ [Monitoring and Troubleshooting](../5.7-monitoring/)

