---
title: "Monitoring and Troubleshooting"
date: 2025-12-08
weight: 7
chapter: false
pre: " <b> 5.7 </b> "
---

## Overview

In this step, you will learn how to monitor the application, view logs, and troubleshoot common issues using CloudWatch, CloudWatch Logs, and other AWS tools.

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

# Memory Utilization (if CloudWatch Agent installed)
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

### View Application Logs

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

### View EC2 System Logs

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

### View Existing Alarms

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

### Create Custom Alarms

```bash
# Alarm for High Error Rate
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

# Alarm for Database Connections
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

### Create Dashboard

```bash
# Create dashboard JSON
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

### View Dashboard

Open [CloudWatch Console](https://console.aws.amazon.com/cloudwatch/) → Dashboards → workshop-aws-dev-dashboard

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

# SSH to EC2 and check processes
aws ssm start-session --target $INSTANCE_ID
top -bn1 | head -20
```

**Solutions:**
1. Scale up: Increase instance type
2. Scale out: Increase number of instances
3. Optimize code: Profile and optimize application
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
1. Increase connection pool size in application.properties
2. Fix connection leaks in code
3. Scale up RDS instance
4. Implement connection pooling best practices

### Issue 3: 502 Bad Gateway

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

## Monitoring Checklist

- [ ] CloudWatch metrics being collected
- [ ] CloudWatch Logs configured
- [ ] Alarms set up
- [ ] SNS notifications working
- [ ] Dashboard created
- [ ] Log retention configured
- [ ] Custom metrics published
- [ ] Health checks working
- [ ] Performance baseline established

## Next Steps

After setting up monitoring:

➡️ [Clean Up Resources](../5.8-cleanup/)

