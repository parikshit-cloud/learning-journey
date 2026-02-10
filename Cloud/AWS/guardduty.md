# 🛡️ What is Amazon GuardDuty?

✅ **GuardDuty = Intelligent Threat Detection for AWS**  
Amazon GuardDuty is a fully managed threat detection service that continuously monitors your AWS environment for malicious or unauthorized activity. It uses machine learning, anomaly detection, and integrated threat intelligence to help identify potential security risks, such as unusual API calls, suspicious network activity, or compromised resources.

> In simpler terms: GuardDuty acts like a security guard watching over your AWS account and reporting suspicious activity.

---

## 🧱 Core Features of Amazon GuardDuty

| Feature             | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **Threat Intelligence** | Uses AWS threat feeds and third-party intel to detect malicious activity |
| **Anomaly Detection**   | Machine learning to identify unusual behavior based on historical data   |
| **Continuous Monitoring** | 24/7 monitoring of AWS account activity and resources               |
| **Integrated Findings**  | Works with CloudTrail, VPC Flow Logs, DNS logs                          |
| **Actionable Findings**  | Security alerts that can be acted on directly or integrated into workflows |

---

## 🔍 Types of Threats GuardDuty Detects

| Threat Type          | Description                                                              |
|----------------------|--------------------------------------------------------------------------|
| **Unauthorized Access** | Detects compromised accounts or suspicious access attempts            |
| **Port Scanning**        | Identifies attempts to scan for open ports or vulnerabilities         |
| **Cryptomining**         | Flags EC2 instances mining cryptocurrency                             |
| **Suspicious API Calls** | Detects API usage outside normal behavior                             |
| **Reconnaissance Activity** | Alerts on mapping of your network or resources                    |
| **Data Exfiltration**     | Detects large/unusual data transfers possibly indicating theft       |

---

## 🌐 How Does GuardDuty Work?

GuardDuty collects data from:

1. **CloudTrail Logs** – Monitors API activity  
2. **VPC Flow Logs** – Monitors network-level behavior  
3. **DNS Logs** – Detects requests to suspicious domains  

> This data is processed with ML models and threat intelligence to produce **findings** (alerts).

---

## 📋 GuardDuty Findings

Findings are categorized by **severity**:

- **High** – Critical, needs immediate attention  
- **Medium** – Important, investigate soon  
- **Low** – Less urgent, monitor as needed  

Each finding includes:
- A description of the activity  
- Affected resources  
- Recommendations for mitigation  

---

## 🔧 GuardDuty Use Cases

| Use Case              | Description                                                  |
|------------------------|--------------------------------------------------------------|
| **Compromised EC2**    | Detect mining or botnet activity                             |
| **Unauthorized APIs**  | Alerts on suspicious API calls                               |
| **Data Exfiltration**  | Detect large/unusual outbound data transfers                 |
| **Port Scanning**      | Detect probes for open ports in your infrastructure          |

---

## 🏗️ How to Enable GuardDuty

### Via Console:

1. Go to **GuardDuty Console**  
2. Click **Get Started**  
3. Follow prompts to enable for your account  
4. It auto-processes logs and displays findings

---

## 📋 CLI Example to Enable GuardDuty

```bash
# Enable GuardDuty
aws guardduty create-detector --enable

# List findings
aws guardduty list-findings --detector-id <detector-id>

# Get finding details
aws guardduty get-findings --detector-id <detector-id> --finding-id <finding-id>
```

---

## 🧠 Why Use GuardDuty?

- ✅ **Automated Detection** – No need to write rules or scripts  
- 💸 **Cost-Effective** – Pay only for analyzed logs  
- 📣 **Actionable Alerts** – Easy to understand & act on  
- 🔗 **AWS Security Integration** – Works with Security Hub, Lambda, SNS

---

## 💡 GuardDuty Best Practices

1. **Enable in all regions** – Threats can arise from any AWS region  
2. **Automate responses** – Use Lambda to block IPs or isolate compromised EC2  
3. **Use CloudWatch** – Forward findings to CloudWatch for dashboards/alerts

