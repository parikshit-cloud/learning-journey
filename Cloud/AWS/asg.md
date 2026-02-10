# ASG in AWS – Auto Scaling Group

## 📌 What is ASG?

An **Auto Scaling Group (ASG)** in AWS is a service that automatically manages a fleet of EC2 instances. It helps ensure the right number of EC2 instances are running to handle your application's load.

---

## 🚀 Key Features:

- **Automatic Scaling**: Add or remove EC2 instances based on demand  
- **High Availability**: Distributes instances across multiple Availability Zones  
- **Health Checks**: Replaces unhealthy instances automatically  
- **Cost Efficiency**: Scales down during low traffic to save cost  

---

## ⚙️ How It Works:

ASG uses:

1. **Launch Template / Configuration** – Defines instance type, AMI, key pair, etc.  
2. **Scaling Policies** – Rules to scale in/out (e.g., CPU > 70%)  
3. **Min / Max / Desired Capacity** – Minimum, maximum, and target instance count  
4. **Elastic Load Balancer (optional)** – Distributes traffic to healthy instances  

---

## 🧠 Example Use Case:

You're running a web app:

- During the day, traffic increases → ASG launches more EC2s  
- At night, traffic drops → ASG terminates unneeded instances  
- If one EC2 fails → ASG replaces it automatically  

---

## 📋 Common CLI Commands:

```bash
aws autoscaling describe-auto-scaling-groups
aws autoscaling create-auto-scaling-group --cli-input-json file://asg.json

