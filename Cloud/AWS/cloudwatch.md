# ⏱️ What is Amazon CloudWatch?

✅ **CloudWatch = Monitoring & Observability Service**  
Amazon CloudWatch helps you monitor AWS resources and applications in real time by collecting:
- Metrics (like CPU, memory, disk)  
- Logs (from apps, EC2, Lambda, etc.)  
- Events (like instance start/stop)  
- Alarms (to take action based on thresholds)

---

## 🚀 What Can CloudWatch Do?

| Feature             | Purpose                                               |
|---------------------|-------------------------------------------------------|
| **Metrics**         | Tracks performance (e.g., CPU, memory, latency)       |
| **Logs**            | Centralized log storage (EC2, Lambda, etc.)          |
| **Alarms**          | Trigger actions when thresholds are breached         |
| **Dashboards**      | Visualize metrics & logs in one place                |
| **Events (EventBridge)** | React to system events (e.g., auto-restart EC2)     |
| **CloudWatch Agent**| Collect custom OS-level metrics/logs                 |

---

## 📊 Common Metrics

| Service | Common Metrics                          |
|---------|------------------------------------------|
| EC2     | CPUUtilization, DiskReadOps, NetworkIn   |
| Lambda  | Invocations, Duration, Errors            |
| RDS     | CPUUtilization, FreeStorageSpace         |
| S3      | NumberOfObjects, BucketSizeBytes         |
| ELB     | RequestCount, HealthyHostCount           |

---

## 🔔 CloudWatch Alarms

- Define a threshold (e.g., CPU > 80%)  
- Set action (e.g., notify via SNS, trigger Auto Scaling)  
- State changes: `OK`, `ALARM`, `INSUFFICIENT_DATA`

---

## 🪵 CloudWatch Logs

- Collect logs from:
  - EC2 instances (via CloudWatch agent)  
  - Lambda functions  
  - Containers (ECS/EKS)  
  - Custom applications  

- Use **Log Insights** to query logs (like SQL for logs!):

```sql
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 10
```

---

## 🧠 CloudWatch vs CloudTrail

| Feature   | CloudWatch                   | CloudTrail                     |
|-----------|-------------------------------|--------------------------------|
| Use Case  | Monitoring & performance      | Auditing & security            |
| Data      | Metrics, logs, alarms         | API calls, user activity       |
| Storage   | CloudWatch Logs, Dashboards   | S3 (by default)                |

---

## 📋 Sample CLI Commands

```bash
# List metrics
aws cloudwatch list-metrics

# Get metric stats
aws cloudwatch get-metric-statistics \\
  --metric-name CPUUtilization \\
  --start-time 2023-04-01T00:00:00Z \\
  --end-time 2023-04-01T01:00:00Z \\
  --period 300 --namespace AWS/EC2 --statistics Average

# Put an alarm
aws cloudwatch put-metric-alarm \\
  --alarm-name HighCPU \\
  --metric-name CPUUtilization \\
  --namespace AWS/EC2 \\
  --statistic Average \\
  --period 300 --threshold 80 \\
  --comparison-operator GreaterThanThreshold \\
  --evaluation-periods 2 \\
  --alarm-actions arn:aws:sns:... \\
  --dimensions Name=InstanceId,Value=i-1234567890abcdef0
```

