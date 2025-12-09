---
title: "Triển khai Backend Application"
date: 2025-12-08
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

## Tổng quan

Trong bước này, bạn sẽ build và deploy ứng dụng Spring Boot backend lên EC2 instances. Backend cung cấp RESTful API cho DNA analysis, user authentication, và data management.

## Bước 1: Cấu hình Database Connection

Lấy RDS endpoint từ CloudFormation outputs:

```bash
RDS_ENDPOINT=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`RDSEndpoint`].OutputValue' \
  --output text)

echo "RDS Endpoint: $RDS_ENDPOINT"
```

Cập nhật file `BE/workshop_BE/src/main/resources/application.properties`:

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

## Bước 2: Build Backend JAR

```bash
cd BE/workshop_BE

# Clean và build
mvn clean package -DskipTests

# Hoặc sử dụng Maven Wrapper
./mvnw clean package -DskipTests

# Kiểm tra JAR file
ls -lh target/workshop-0.0.1-SNAPSHOT.jar
```

**Kết quả mong đợi:** File JAR khoảng 50-80MB trong thư mục `target/`

## Bước 3: Upload JAR lên S3

Tạo S3 bucket cho backend artifacts (nếu chưa có):

```bash
ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
BACKEND_BUCKET="workshop-aws-dev-backend-${ACCOUNT_ID}-ap-southeast-1"

# Tạo bucket
aws s3 mb s3://${BACKEND_BUCKET} --region ap-southeast-1

# Upload JAR
aws s3 cp target/workshop-0.0.1-SNAPSHOT.jar \
  s3://${BACKEND_BUCKET}/jars/ \
  --region ap-southeast-1

# Verify upload
aws s3 ls s3://${BACKEND_BUCKET}/jars/
```

## Bước 4: Deploy lên EC2

### Lấy EC2 Instance ID

```bash
INSTANCE_ID=$(aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
            "Name=instance-state-name,Values=running" \
  --region ap-southeast-1 \
  --query 'Reservations[0].Instances[0].InstanceId' \
  --output text)

echo "Instance ID: $INSTANCE_ID"
```

### Kết nối vào EC2 qua Session Manager

```bash
aws ssm start-session --target $INSTANCE_ID --region ap-southeast-1
```

### Trên EC2 Instance, chạy các lệnh sau:

```bash
# Chuyển sang ec2-user
sudo su - ec2-user

# Di chuyển vào thư mục application
cd /opt/workshop

# Download JAR từ S3
ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
BACKEND_BUCKET="workshop-aws-dev-backend-${ACCOUNT_ID}-ap-southeast-1"

aws s3 cp s3://${BACKEND_BUCKET}/jars/workshop-0.0.1-SNAPSHOT.jar . \
  --region ap-southeast-1

# Kiểm tra file
ls -lh workshop-0.0.1-SNAPSHOT.jar
```


### Tạo Application Properties

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

# Thay thế RDS endpoint
RDS_ENDPOINT=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`RDSEndpoint`].OutputValue' \
  --output text)

sed -i "s/REPLACE_WITH_RDS_ENDPOINT/${RDS_ENDPOINT}/g" application.properties
```

### Khởi động Application

```bash
# Dừng application cũ (nếu có)
sudo systemctl stop workshop.service 2>/dev/null || true
pkill -f workshop-0.0.1-SNAPSHOT.jar 2>/dev/null || true

# Khởi động application
nohup java -jar workshop-0.0.1-SNAPSHOT.jar \
  --spring.config.location=file:/opt/workshop/application.properties \
  > /dev/null 2>&1 &

# Lưu PID
echo $! > application.pid

# Đợi application khởi động
sleep 10

# Kiểm tra process
ps aux | grep java
```

## Bước 5: Kiểm tra Application

### Test Health Endpoint

```bash
# Trên EC2
curl http://localhost:8080/dna_service/actuator/health

# Kết quả mong đợi:
# {"status":"UP"}
```

### Test qua Load Balancer

```bash
# Trên máy local
ALB_DNS=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`ALBDNSName`].OutputValue' \
  --output text)

curl http://${ALB_DNS}/dna_service/actuator/health
```

### Test qua API Gateway

```bash
API_URL=$(aws cloudformation describe-stacks \
  --stack-name workshop-aws-dev \
  --region ap-southeast-1 \
  --query 'Stacks[0].Outputs[?OutputKey==`APIGatewayURL`].OutputValue' \
  --output text)

curl ${API_URL}/dna_service/actuator/health
```

## Bước 6: Cấu hình Systemd Service

Để application tự động khởi động khi EC2 restart:

```bash
# Trên EC2
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

## Bước 7: Xem Logs

```bash
# Xem application logs
tail -f /opt/workshop/application.log

# Xem systemd logs
sudo journalctl -u workshop.service -f

# Xem CloudWatch Logs (trên máy local)
aws logs tail /aws/workshop-aws/dev/application \
  --follow \
  --region ap-southeast-1
```

## Troubleshooting

### Application không khởi động

**Kiểm tra logs:**
```bash
tail -100 /opt/workshop/application.log
```

**Các lỗi thường gặp:**

1. **Database connection failed**
   - Kiểm tra RDS endpoint trong application.properties
   - Kiểm tra Security Group cho phép EC2 connect đến RDS
   - Verify database credentials

2. **Port 8080 already in use**
   ```bash
   # Kill process đang dùng port 8080
   sudo lsof -ti:8080 | xargs kill -9
   ```

3. **Out of memory**
   ```bash
   # Tăng heap size
   java -Xmx512m -jar workshop-0.0.1-SNAPSHOT.jar
   ```

### Health check failed

```bash
# Kiểm tra application đang chạy
ps aux | grep java

# Kiểm tra port listening
sudo netstat -tulpn | grep 8080

# Test local
curl -v http://localhost:8080/dna_service/actuator/health
```

### Load Balancer health check failed

```bash
# Kiểm tra Target Group health
aws elbv2 describe-target-health \
  --target-group-arn <target-group-arn> \
  --region ap-southeast-1

# Kiểm tra Security Group
# EC2 SG phải cho phép traffic từ ALB SG trên port 8080
```

## Xác nhận Deployment thành công

Checklist:

- [ ] JAR file đã build thành công
- [ ] JAR đã upload lên S3
- [ ] Application đang chạy trên EC2
- [ ] Health endpoint trả về `{"status":"UP"}`
- [ ] Có thể access qua Load Balancer
- [ ] Có thể access qua API Gateway
- [ ] Systemd service đã được enable
- [ ] Logs đang được ghi vào CloudWatch

## Tiếp theo

Sau khi backend đã sẵn sàng:

➡️ [Triển khai Frontend lên S3 và CloudFront](../5.5-deploy-frontend/)

