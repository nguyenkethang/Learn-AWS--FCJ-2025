---
title: "Deploy Backend Application"
date: 2025-12-08
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

## Overview

In this step, you will build and deploy the Spring Boot backend application to EC2 instances. The backend provides RESTful API for DNA analysis, user authentication, and data management.

## Step 1: Configure Database Connection

Get RDS endpoint from CloudFormation outputs:

```bash
RDS_ENDPOINT=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`RDSEndpoint`].OutputValue' \
  --output text)

echo "RDS Endpoint: $RDS_ENDPOINT"
```

Update file `BE/workshop_BE/src/main/resources/application.properties`:

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://${RDS_ENDPOINT}:3306/workshop_aws?useSSL=true&requireSSL=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Ho_Chi_Minh
spring.datasource.username=admin
spring.datasource.password=YourStrongPassword123!
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Connection Pool
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.connection-timeout=20000

# JPA Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# Server Configuration
server.port=8080
server.servlet.context-path=/dna_service

# JWT Configuration
jwt.signerKey=2VJ50pdhYm96e4VECp/vsZGVmkSl9xp1rSYAZKsZL7n9Ti1pZYle3k9mheQEKt6+
jwt.expiration=86400000

# CORS Configuration
cors.allowed.origins=*

# Logging
logging.level.root=INFO
logging.level.aws_project.workshop=DEBUG
logging.file.name=/opt/workshop/application.log
```

## Step 2: Build Backend JAR

```bash
cd BE/workshop_BE

# Clean and build
mvn clean package -DskipTests

# Or use Maven Wrapper
./mvnw clean package -DskipTests

# Verify JAR file
ls -lh target/workshop-0.0.1-SNAPSHOT.jar
```

**Expected result:** JAR file approximately 50-80MB in `target/` directory

## Step 3: Upload JAR to S3

Create S3 bucket for backend artifacts (if not exists):

```bash
ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
BACKEND_BUCKET="workshop-aws-dev-backend-${ACCOUNT_ID}-ap-southeast-1"

# Create bucket
aws s3 mb s3://${BACKEND_BUCKET} --region ap-southeast-1

# Upload JAR
aws s3 cp target/workshop-0.0.1-SNAPSHOT.jar \
  s3://${BACKEND_BUCKET}/jars/ \
  --region ap-southeast-1

# Verify upload
aws s3 ls s3://${BACKEND_BUCKET}/jars/
```

## Step 4: Deploy to EC2

### Get EC2 Instance ID

```bash
INSTANCE_ID=$(aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
            "Name=instance-state-name,Values=running" \
  --region ap-southeast-1 \
  --query 'Reservations[0].Instances[0].InstanceId' \
  --output text)

echo "Instance ID: $INSTANCE_ID"
```

### Connect to EC2 via Session Manager

```bash
aws ssm start-session --target $INSTANCE_ID --region ap-southeast-1
```

### On EC2 Instance, run the following commands:

```bash
# Switch to ec2-user
sudo su - ec2-user

# Navigate to application directory
cd /opt/workshop

# Download JAR from S3
ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
BACKEND_BUCKET="workshop-aws-dev-backend-${ACCOUNT_ID}-ap-southeast-1"

aws s3 cp s3://${BACKEND_BUCKET}/jars/workshop-0.0.1-SNAPSHOT.jar . \
  --region ap-southeast-1

# Verify file
ls -lh workshop-0.0.1-SNAPSHOT.jar
```

### Create Application Properties

```bash
cat > application.properties <<'EOF'
spring.application.name=workshop-aws

# Database Configuration
spring.datasource.url=jdbc:mysql://REPLACE_WITH_RDS_ENDPOINT:3306/workshop_aws?useSSL=true&requireSSL=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Ho_Chi_Minh
spring.datasource.username=admin
spring.datasource.password=YourStrongPassword123!
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Connection Pool
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5

# JPA Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false

# Server Configuration
server.port=8080
server.servlet.context-path=/dna_service

# JWT Configuration
jwt.signerKey=2VJ50pdhYm96e4VECp/vsZGVmkSl9xp1rSYAZKsZL7n9Ti1pZYle3k9mheQEKt6+

# Logging
logging.level.root=INFO
logging.level.aws_project.workshop=DEBUG
logging.file.name=/opt/workshop/application.log
EOF

# Replace RDS endpoint
RDS_ENDPOINT=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`RDSEndpoint`].OutputValue' \
  --output text)

sed -i "s/REPLACE_WITH_RDS_ENDPOINT/${RDS_ENDPOINT}/g" application.properties
```

### Start Application

```bash
# Stop old application (if any)
sudo systemctl stop workshop.service 2>/dev/null || true
pkill -f workshop-0.0.1-SNAPSHOT.jar 2>/dev/null || true

# Start application
nohup java -jar workshop-0.0.1-SNAPSHOT.jar \
  --spring.config.location=file:/opt/workshop/application.properties \
  > /dev/null 2>&1 &

# Save PID
echo $! > application.pid

# Wait for application to start
sleep 10

# Check process
ps aux | grep java
```

## Step 5: Verify Application

### Test Health Endpoint

```bash
# On EC2
curl http://localhost:8080/dna_service/actuator/health

# Expected result:
# {"status":"UP"}
```

### Test via Load Balancer

```bash
# On local machine
ALB_DNS=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`ALBDNSName`].OutputValue' \
  --output text)

curl http://${ALB_DNS}/dna_service/actuator/health
```

### Test via API Gateway

```bash
API_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`APIGatewayURL`].OutputValue' \
  --output text)

curl ${API_URL}/dna_service/actuator/health
```

## Step 6: Configure Systemd Service

To automatically start application when EC2 restarts:

```bash
# On EC2
sudo tee /etc/systemd/system/workshop.service > /dev/null <<'EOF'
[Unit]
Description=Workshop DNA Analysis Backend
After=network.target

[Service]
Type=simple
User=ec2-user
Group=ec2-user
WorkingDirectory=/opt/workshop
ExecStart=/usr/bin/java -jar /opt/workshop/workshop-0.0.1-SNAPSHOT.jar --spring.config.location=file:/opt/workshop/application.properties
Restart=always
RestartSec=10
StandardOutput=append:/opt/workshop/application.log
StandardError=append:/opt/workshop/application.log

[Install]
WantedBy=multi-user.target
EOF

# Reload systemd
sudo systemctl daemon-reload

# Enable service
sudo systemctl enable workshop.service

# Start service
sudo systemctl start workshop.service

# Check status
sudo systemctl status workshop.service
```

## Step 7: View Logs

```bash
# View application logs
tail -f /opt/workshop/application.log

# View systemd logs
sudo journalctl -u workshop.service -f

# View CloudWatch Logs (on local machine)
aws logs tail /aws/workshop-aws/dev/application \
  --follow \
  --region ap-southeast-1
```

## Troubleshooting

### Application Won't Start

**Check logs:**
```bash
tail -100 /opt/workshop/application.log
```

**Common errors:**

1. **Database connection failed**
   - Check RDS endpoint in application.properties
   - Verify Security Group allows EC2 to connect to RDS
   - Verify database credentials

2. **Port 8080 already in use**
   ```bash
   # Kill process using port 8080
   sudo lsof -ti:8080 | xargs kill -9
   ```

3. **Out of memory**
   ```bash
   # Increase heap size
   java -Xmx512m -jar workshop-0.0.1-SNAPSHOT.jar
   ```

### Health Check Failed

```bash
# Check application is running
ps aux | grep java

# Check port listening
sudo netstat -tulpn | grep 8080

# Test locally
curl -v http://localhost:8080/dna_service/actuator/health
```

### Load Balancer Health Check Failed

```bash
# Check Target Group health
aws elbv2 describe-target-health \
  --target-group-arn <target-group-arn> \
  --region ap-southeast-1

# Check Security Group
# EC2 SG must allow traffic from ALB SG on port 8080
```

## Confirm Successful Deployment

Checklist:

- [ ] JAR file built successfully
- [ ] JAR uploaded to S3
- [ ] Application running on EC2
- [ ] Health endpoint returns `{"status":"UP"}`
- [ ] Accessible via Load Balancer
- [ ] Accessible via API Gateway
- [ ] Systemd service enabled
- [ ] Logs being written to CloudWatch

## Next Steps

After backend is ready:

➡️ [Deploy Frontend to S3 and CloudFront](../5.5-deploy-frontend/)

