# What is EC2 in AWS?

✅ **EC2 = Elastic Compute Cloud**  
Amazon EC2 is a core AWS service that lets you rent virtual servers (aka instances) in the cloud to run your applications.

---

## 🚀 Key Features:
- Scalable compute power in the cloud  
- Choose OS (Linux, Windows, etc.)  
- Launch in minutes  
- Pay-as-you-go pricing  
- Multiple instance types (general, compute-optimized, memory-optimized, etc.)

---

## ⚙️ Common Use Cases:
- Hosting websites & web apps  
- Running backend services or APIs  
- Development & testing environments  
- Batch processing  
- Game servers or machine learning models

---

## 🧱 Core Concepts:

| Term           | Meaning                                              |
|----------------|------------------------------------------------------|
| **Instance**       | A virtual server (like your own computer)            |
| **AMI**            | Amazon Machine Image – the OS & software            |
| **Instance Type**  | Defines CPU, RAM, network (e.g. t2.micro)           |
| **EBS Volume**     | Elastic Block Store – like a hard drive             |
| **Key Pair**       | SSH access to Linux instances (private key)         |
| **Security Group** | Firewall rules for your instance                    |
| **Elastic IP**     | Static public IP for your EC2 instance              |
| **User Data**      | Startup script when instance boots                  |

---

## 🔐 Security Tip:
Always limit SSH (port 22) to your IP in the security group — don’t open it to the whole internet (`0.0.0.0/0`) unless you know what you’re doing!

---

## 📋 Common CLI Commands:

```bash
# Launch instance
aws ec2 run-instances --image-id ami-123456 --instance-type t2.micro --key-name MyKey --security-groups MySG

# List instances
aws ec2 describe-instances

# Stop / Start / Terminate
aws ec2 stop-instances --instance-ids i-123456
aws ec2 start-instances --instance-ids i-123456
aws ec2 terminate-instances --instance-ids i-123456
