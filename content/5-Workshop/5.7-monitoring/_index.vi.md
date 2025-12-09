---
title: "Giám sát và Xử lý sự cố"
date: 2025-12-08
weight: 7
chapter: false
pre: " <b> 5.7 </b> "
---

## Tổng quan

Trong bước này, bạn sẽ học cách giám sát ứng dụng, xem logs, và xử lý các sự cố thường gặp sử dụng CloudWatch, CloudWatch Logs, và các công cụ AWS khác.

## CloudWatch Metrics

### EC2 Metrics

```bash
# CPU Utilization
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=AutoScalingGroupName,Value=workshop-aws-dev-asg \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Average,Maximum \
  --region ap-southeast-1

# Memory Utilization (nếu có CloudWatch Agent)
aws cloudwatch get-metric-statistics \
  --namespace CWAgent \
  --metric-name mem_used_percent \
  --dimensions Name=AutoScalingGroupName,Value=workshop-aws-dev-asg \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Average \
  --region ap-southeast-1
```

### RDS Metrics

```bash
# Database Connections
aws cloudwatch get-metric-statistics \
  --namespace AWS/RDS \
  --metric-name DatabaseConnections \
  --dimensions Name=DBInstanceIdentifier,Value=workshop-aws-dev-db \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Average,Maximum \
  --region ap-southeast-1

# CPU Utilization
aws cloudwatch get-metric-statistics \
  --namespace AWS/RDS \
  --metric-name CPUUtilization \
  --dimensions Name=DBInstanceIdentifier,Value=workshop-aws-dev-db \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Average \
  --region ap-southeast-1
```

### Application Load Balancer Metrics

```bash
# Request Count
aws cloudwatch get-metric-statistics \
  --namespace AWS/ApplicationELB \
  --metric-name RequestCount \
  --dimensions Name=LoadBalancer,Value=app/workshop-aws-dev-alb/xxxxx \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Sum \
  --region ap-southeast-1

# Target Response Time
aws cloudwatch get-metric-statistics \
  --namespace AWS/ApplicationELB \
  --metric-name TargetResponseTime \
  --dimensions Name=LoadBalancer,Value=app/workshop-aws-dev-alb/xxxxx \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Average \
  --region ap-southeast-1
```

## CloudWatch Logs

### Xem Application Logs

```bash
# List log streams
aws logs describe-log-streams \
  --log-group-name /aws/workshop-aws/dev/application \
  --order-by LastEventTime \
  --descending \
  --max-items 5 \
  --region ap-southeast-1

# Tail logs (real-time)
aws logs tail /aws/workshop-aws/dev/application \
  --follow \
  --region ap-southeast-1

# Filter logs by pattern
aws logs filter-log-events \
  --log-group-name /aws/workshop-aws/dev/application \
  --filter-pattern "ERROR" \
  --start-time $(date -d '1 hour ago' +%s)000 \
  --region ap-southeast-1

# Search for specific errors
aws logs filter-log-events \
  --log-group-name /aws/workshop-aws/dev/application \
  --filter-pattern "NullPointerException" \
  --start-time $(date -d '1 hour ago' +%s)000 \
  --region ap-southeast-1
```

### Xem EC2 System Logs

```bash
# Get instance ID
INSTANCE_ID=$(aws ec2 describe-instances \
  --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" \
            "Name=instance-state-name,Values=running" \
  --region ap-southeast-1 \
  --query 'Reservations[0].Instances[0].InstanceId' \
  --output text)

# Get console output
aws ec2 get-console-output \
  --instance-id $INSTANCE_ID \
  --region ap-southeast-1 \
  --output text
```

## CloudWatch Alarms

### Xem Existing Alarms

```bash
# List all alarms
aws cloudwatch describe-alarms \
  --alarm-name-prefix workshop-aws-dev \
  --region ap-southeast-1

# Get alarm history
aws cloudwatch describe-alarm-history \
  --alarm-name workshop-aws-dev-cpu-high \
  --max-records 10 \
  --region ap-southeast-1
```

### Tạo Custom Alarms

```bash
# Alarm cho High Error Rate
aws cloudwatch put-metric-alarm \
  --alarm-name workshop-aws-dev-high-error-rate \
  --alarm-description "Alert when error rate exceeds 5%" \
  --metric-name 5XXError \
  --namespace AWS/ApplicationELB \
  --statistic Sum \
  --period 300 \
  --evaluation-periods 2 \
  --threshold 10 \
  --comparison-operator GreaterThanThreshold \
  --dimensions Name=LoadBalancer,Value=app/workshop-aws-dev-alb/xxxxx \
  --alarm-actions arn:aws:sns:ap-southeast-1:123456789012:workshop-aws-dev-alarms \
  --region ap-southeast-1

# Alarm cho Database Connections
aws cloudwatch put-metric-alarm \
  --alarm-name workshop-aws-dev-high-db-connections \
  --alarm-description "Alert when DB connections exceed 80" \
  --metric-name DatabaseConnections \
  --namespace AWS/RDS \
  --statistic Average \
  --period 300 \
  --evaluation-periods 2 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --dimensions Name=DBInstanceIdentifier,Value=workshop-aws-dev-db \
  --alarm-actions arn:aws:sns:ap-southeast-1:123456789012:workshop-aws-dev-alarms \
  --region ap-southeast-1
```

## CloudWatch Dashboards

### Tạo Dashboard

```bash
# Tạo dashboard JSON
cat > dashboard.json <<'EOF'
{
  "widgets": [
    {
      "type": "metric",
      "properties": {
        "metrics": [
          ["AWS/EC2", "CPUUtilization", {"stat": "Average"}]
        ],
        "period": 300,
        "stat": "Average",
        "region": "ap-southeast-1",
        "title": "EC2 CPU Utilization"
      }
    },
    {
      "type": "metric",
      "properties": {
        "metrics": [
          ["AWS/RDS", "DatabaseConnections", {"stat": "Average"}]
        ],
        "period": 300,
        "stat": "Average",
        "region": "ap-southeast-1",
        "title": "RDS Connections"
      }
    },
    {
      "type": "metric",
      "properties": {
        "metrics": [
          ["AWS/ApplicationELB", "RequestCount", {"stat": "Sum"}]
        ],
        "period": 300,
        "stat": "Sum",
        "region": "ap-southeast-1",
        "title": "ALB Request Count"
      }
    }
  ]
}
EOF

# Create dashboard
aws cloudwatch put-dashboard \
  --dashboard-name workshop-aws-dev-dashboard \
  --dashboard-body file://dashboard.json \
  --region ap-southeast-1
```

### Xem Dashboard

Mở [CloudWatch Console](https://console.aws.amazon.com/cloudwatch/) → Dashboards → workshop-aws-dev-dashboard

## Troubleshooting Common Issues

### Issue 1: High CPU Usage

**Symptoms:**
- EC2 CPU > 80%
- Slow response times
- CloudWatch alarm triggered

**Diagnosis:**
```bash
# Check CPU metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=AutoScalingGroupName,Value=workshop-aws-dev-asg \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 60 \
  --statistics Average,Maximum \
  --region ap-southeast-1

# SSH vào EC2 và check processes
aws ssm start-session --target $INSTANCE_ID
top -bn1 | head -20
```

**Solutions:**
1. Scale up: Tăng instance type
2. Scale out: Tăng số lượng instances
3. Optimize code: Profile và optimize application
4. Add caching: Implement Redis/ElastiCache

### Issue 2: Database Connection Pool Exhausted

**Symptoms:**
- "Too many connections" errors
- Slow database queries
- Application timeouts

**Diagnosis:**
```bash
# Check DB connections
aws cloudwatch get-metric-statistics \
  --namespace AWS/RDS \
  --metric-name DatabaseConnections \
  --dimensions Name=DBInstanceIdentifier,Value=workshop-aws-dev-db \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 60 \
  --statistics Average,Maximum \
  --region ap-southeast-1

# Connect to DB and check
mysql -h $RDS_ENDPOINT -u admin -p
SHOW PROCESSLIST;
SHOW STATUS LIKE 'Threads_connected';
```

**Solutions:**
1. Increase connection pool size trong application.properties
2. Fix connection leaks trong code
3. Scale up RDS instance
4. Implement connection pooling best practices

### Issue 3: High Memory Usage

**Symptoms:**
- Out of memory errors
- Application crashes
- Slow performance

**Diagnosis:**
```bash
# Check memory on EC2
aws ssm start-session --target $INSTANCE_ID
free -h
ps aux --sort=-%mem | head -10

# Check Java heap usage
jstat -gc <java-pid>
```

**Solutions:**
1. Increase JVM heap size: `-Xmx1024m`
2. Fix memory leaks
3. Scale up instance type
4. Implement proper garbage collection tuning

### Issue 4: 502 Bad Gateway

**Symptoms:**
- Users receive 502 errors
- ALB cannot reach backend
- Health checks failing

**Diagnosis:**
```bash
# Check target health
aws elbv2 describe-target-health \
  --target-group-arn <arn> \
  --region ap-southeast-1

# Check backend logs
aws logs tail /aws/workshop-aws/dev/application --follow

# Check Security Groups
aws ec2 describe-security-groups \
  --group-ids <ec2-sg-id> \
  --region ap-southeast-1
```

**Solutions:**
1. Verify backend is running: `systemctl status workshop`
2. Check Security Group allows ALB traffic
3. Verify health check path is correct
4. Check application logs for errors

### Issue 5: Slow Page Load

**Symptoms:**
- Frontend takes > 3s to load
- Poor user experience
- High bounce rate

**Diagnosis:**
```bash
# Check CloudFront metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/CloudFront \
  --metric-name BytesDownloaded \
  --dimensions Name=DistributionId,Value=$DIST_ID \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Sum \
  --region us-east-1

# Check cache hit ratio
curl -I https://$CLOUDFRONT_URL/assets/index.js | grep X-Cache
```

**Solutions:**
1. Enable CloudFront compression
2. Optimize images and assets
3. Implement lazy loading
4. Increase cache TTL
5. Use CDN for static assets

## Performance Monitoring

### Application Performance Monitoring (APM)

Thêm Spring Boot Actuator metrics:

```properties
# application.properties
management.endpoints.web.exposure.include=health,info,metrics,prometheus
management.metrics.export.cloudwatch.enabled=true
management.metrics.export.cloudwatch.namespace=WorkshopApp
management.metrics.export.cloudwatch.step=1m
```

### Custom Metrics

Publish custom metrics từ application:

```java
@Autowired
private MeterRegistry meterRegistry;

public void recordDNAAnalysis() {
    Counter.builder("dna.analysis.count")
        .tag("type", "sequence")
        .register(meterRegistry)
        .increment();
}
```

### Query Custom Metrics

```bash
aws cloudwatch get-metric-statistics \
  --namespace WorkshopApp \
  --metric-name dna.analysis.count \
  --start-time $(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%S) \
  --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
  --period 300 \
  --statistics Sum \
  --region ap-southeast-1
```

## Log Analysis

### CloudWatch Logs Insights

```bash
# Query error logs
aws logs start-query \
  --log-group-name /aws/workshop-aws/dev/application \
  --start-time $(date -d '1 hour ago' +%s) \
  --end-time $(date +%s) \
  --query-string 'fields @timestamp, @message | filter @message like /ERROR/ | sort @timestamp desc | limit 20' \
  --region ap-southeast-1

# Get query results
aws logs get-query-results \
  --query-id <query-id> \
  --region ap-southeast-1
```

### Common Log Queries

**1. Top 10 errors:**
```
fields @timestamp, @message
| filter @message like /ERROR/
| stats count() by @message
| sort count desc
| limit 10
```

**2. Slow queries:**
```
fields @timestamp, @message
| filter @message like /Hibernate/
| filter @message like /ms/
| parse @message /(?<duration>\d+)ms/
| filter duration > 1000
| sort @timestamp desc
```

**3. API response times:**
```
fields @timestamp, @message
| filter @message like /Request processed/
| parse @message /in (?<duration>\d+)ms/
| stats avg(duration), max(duration), min(duration)
```

## Best Practices

### 1. Set Up Alerts

- CPU > 80% for 5 minutes
- Memory > 85% for 5 minutes
- Disk > 90%
- 5XX errors > 10 in 5 minutes
- Database connections > 80% of max

### 2. Regular Health Checks

```bash
# Daily health check script
#!/bin/bash
echo "=== Daily Health Check ==="
echo "Date: $(date)"

# Check stack status
echo "CloudFormation Stack:"
aws cloudformation describe-stacks --stack-name workshop-aws-dev --query 'Stacks[0].StackStatus'

# Check EC2
echo "EC2 Instances:"
aws ec2 describe-instances --filters "Name=tag:aws:cloudformation:stack-name,Values=workshop-aws-dev" --query 'Reservations[*].Instances[*].[InstanceId,State.Name]'

# Check RDS
echo "RDS Database:"
aws rds describe-db-instances --db-instance-identifier workshop-aws-dev-db --query 'DBInstances[0].DBInstanceStatus'

# Check API
echo "API Health:"
curl -s $API_URL/dna_service/actuator/health | jq .
```

### 3. Log Retention

- Development: 3-7 days
- Production: 30-90 days
- Compliance: 1-7 years

### 4. Cost Monitoring

```bash
# Check CloudWatch costs
aws ce get-cost-and-usage \
  --time-period Start=2025-12-01,End=2025-12-08 \
  --granularity DAILY \
  --metrics BlendedCost \
  --filter file://filter.json
```

## Monitoring Checklist

- [ ] CloudWatch metrics được thu thập
- [ ] CloudWatch Logs được cấu hình
- [ ] Alarms được thiết lập
- [ ] SNS notifications hoạt động
- [ ] Dashboard được tạo
- [ ] Log retention được cấu hình
- [ ] Custom metrics được publish
- [ ] Health checks hoạt động
- [ ] Performance baseline được thiết lập

## Tiếp theo

Sau khi thiết lập monitoring:

➡️ [Dọn dẹp tài nguyên](../5.8-cleanup/)

