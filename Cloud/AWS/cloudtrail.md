# ✅ What is CloudTrail in AWS?

**CloudTrail = Audit & Governance Service**  
AWS CloudTrail records all API calls and activity in your AWS account — so you can monitor, audit, and track user and service actions.

---

## 🔍 Key Features

- Records who did what, when, and from where  
- Tracks API calls, console logins, SDK/CLI use  
- Stores logs in S3 buckets  
- Can trigger CloudWatch Alarms, SNS, or Lambda on specific actions  
- Helps with compliance (PCI-DSS, HIPAA, etc.)

---

## 🧠 What CloudTrail Logs

| Activity Type    | Example                          |
|------------------|----------------------------------|
| Console actions  | User logging in, creating EC2    |
| CLI/SDK calls    | `aws ec2 run-instances`          |
| Service actions  | Lambda execution, S3 access      |
| IAM events       | Role changes, policy updates     |

---

## 📦 Event Structure

Each log entry contains:

- Event time  
- User identity (IAM role, user, etc.)  
- Source IP  
- AWS service  
- API call name  
- Request/response details  

---

## 🗂️ Types of Trails

- **Management Events** – Control plane: IAM changes, EC2 creation  
- **Data Events** – Data plane: S3 `GetObject`, Lambda `Invoke`  
- **Insights Events** – Detect unusual activity (e.g., spike in actions)  

---

## 🔐 Why Use CloudTrail?

- Security auditing  
- Forensics (e.g., “Who deleted my EC2 instance?”)  
- Compliance  
- Monitoring user activity  
- Detecting suspicious behavior  

---

## 📋 Common CLI Commands

```bash
# List trails
aws cloudtrail describe-trails

# Start a new trail
aws cloudtrail create-trail --name myTrail --s3-bucket-name my-trail-logs

# Enable logging
aws cloudtrail start-logging --name myTrail
```

