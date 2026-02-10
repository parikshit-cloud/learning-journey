# ⚖️ What is ELB in AWS?

✅ **ELB = Elastic Load Balancer**  
Amazon ELB automatically distributes incoming traffic across multiple targets (like EC2 instances, containers, IPs) in one or more Availability Zones — improving availability, fault tolerance, and scalability.

---

## 🚀 Why Use ELB?

- Handles high traffic smoothly  
- Ensures only healthy instances get traffic  
- Works with Auto Scaling  
- Supports SSL termination  
- Native integration with EC2, ECS, EKS, Lambda

---

## 🧱 Types of ELB

| ELB Type | Best For | Layer |
|----------|----------|-------|
| **ALB (Application Load Balancer)** | HTTP/HTTPS apps, URL routing, microservices | Layer 7 |
| **NLB (Network Load Balancer)**     | High-performance, TCP/UDP traffic, static IP | Layer 4 |
| **CLB (Classic Load Balancer)**     | Legacy apps, simple TCP/HTTP workloads       | Layer 4/7 |

⚠️ **CLB is legacy. Prefer ALB or NLB for new apps.**

---

## 🌐 ALB (Application Load Balancer) Features

- Content-based routing (e.g. `/api` to one service, `/web` to another)  
- Host-based routing (`api.example.com`)  
- WebSocket support  
- Target groups (group of EC2s, Lambda, etc.)

---

## ⚙️ NLB (Network Load Balancer) Features

- Extreme performance (millions of reqs/sec)  
- Ultra-low latency  
- Static IP support  
- Ideal for real-time, latency-sensitive applications

---

## 🔄 Health Checks

ELB performs health checks and only sends traffic to healthy targets.

---

## 🔐 SSL Termination

- ELB can manage SSL/TLS certificates  
- Use AWS Certificate Manager (ACM) for free certs

---

## 🧠 Example Use Case

A web app with 3 EC2 instances in different AZs:

- ELB balances traffic to all 3  
- If one instance fails → ELB routes traffic to healthy ones  
- When traffic spikes → ASG adds instances, ELB auto-load-balances

---

## 📋 Common CLI Commands

```bash
# List ELBs
aws elbv2 describe-load-balancers

# Create ALB (sample)
aws elbv2 create-load-balancer --name my-alb \\
  --subnets subnet-123 subnet-456 \\
  --security-groups sg-123456

# Register targets
aws elbv2 register-targets --target-group-arn arn:xyz \\
  --targets Id=i-123456
```

