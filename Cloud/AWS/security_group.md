# ✅ What is a Security Group in AWS?

A **Security Group (SG)** in AWS is a virtual firewall that controls the **inbound and outbound traffic** to and from EC2 instances and other resources in your **VPC (Virtual Private Cloud)**.

> ✅ Security groups are **stateful**:  
> If you allow incoming traffic on a port, the corresponding outgoing traffic is automatically allowed.

---

## 🧱 Core Features of Security Groups

| Feature                | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| Inbound and Outbound Rules | Define both incoming and outgoing traffic directions                     |
| Allow Rules Only       | Only allow rules are permitted (no deny rules)                             |
| Stateful               | Return traffic is automatically allowed                                    |
| Default Security Group | Created automatically with a VPC                                           |
| Multiple Security Groups | A single resource can have multiple SGs                                   |
| Evaluation by Rule Order | All rules are evaluated independently, not by order                       |

---

## 🧑‍💻 How Security Groups Work

1. **Traffic Evaluation**: All SGs attached to a resource are evaluated.  
2. **Allow Rules**: If **any** rule allows the traffic, it’s permitted.  
3. **Stateful**: Outbound response is automatically allowed for allowed inbound traffic.

---

## 🔐 Security Group Rules

### 1. Inbound Rules
- Define who can **access** your resource.
- Example: Allow SSH (port 22) from `203.0.113.0/24`

### 2. Outbound Rules
- Define what your resource can **reach out to**.
- Default: All outbound traffic is allowed unless restricted.

#### 🔁 Examples:

```text
Inbound Rule (SSH):  Allow TCP port 22 from 203.0.113.0/24
Outbound Rule:       Allow all traffic (default)
Inbound Rule (HTTP): Allow TCP port 80 from 0.0.0.0/0
```

---

## 🧩 Key Concepts in Security Groups

| Term                      | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| Security Group Rules      | Define allowed inbound and outbound traffic                                 |
| Inbound Rule              | Controls incoming connections                                               |
| Outbound Rule             | Controls outgoing connections                                               |
| Stateful                  | Return traffic is automatically allowed                                     |
| VPC                       | Virtual network within which SGs are defined                                |
| Security Group Associations | Resources like EC2 can be associated with multiple SGs                     |

---

## 🔑 Best Practices

1. **Least Privilege** – Only open required ports & IPs  
2. **Tighten Defaults** – Modify default SG to minimize exposure  
3. **Use Multiple SGs** – Split access rules for modular config  
4. **Tier-Based Groups** – Separate SGs for web, app, DB layers  
5. **Audit Regularly** – Clean unused rules and narrow IP ranges

---

## 🏗️ How to Create a Security Group (Console)

1. Go to **EC2 Dashboard** → **Security Groups**  
2. Click **Create Security Group**  
3. Provide name and description  
4. Define inbound/outbound rules (e.g., SSH, HTTP)  
5. Click **Create**

---

## 📋 CLI Commands for Security Groups

```bash
# Create a security group
aws ec2 create-security-group \\
  --group-name MySecurityGroup \\
  --description "My first security group" \\
  --vpc-id vpc-12345678

# Add inbound rule (SSH)
aws ec2 authorize-security-group-ingress \\
  --group-id sg-12345678 \\
  --protocol tcp --port 22 \\
  --cidr 203.0.113.0/24

# Add outbound rule (Allow all)
aws ec2 authorize-security-group-egress \\
  --group-id sg-12345678 \\
  --protocol tcp --port 0-65535 \\
  --cidr 0.0.0.0/0
```

---

## 🔧 Security Group vs. NACL (Network ACL)

| Feature               | Security Group                 | Network ACL                    |
|------------------------|-------------------------------|--------------------------------|
| Level                 | Instance level                 | Subnet level                   |
| Stateful              | ✅ Yes                         | ❌ No                          |
| Rules                 | Only allow rules               | Allow & Deny rules             |
| Direction             | Separate inbound/outbound      | Separate inbound/outbound      |
| Evaluation            | All rules                      | Evaluated in numbered order    |

---

## 🧠 Example Use Cases

| Use Case            | Description                                                              |
|---------------------|--------------------------------------------------------------------------|
| Web Server          | Inbound HTTP (80), HTTPS (443) from anywhere                             |
| SSH Access          | Inbound SSH (22) only from trusted IP addresses                          |
| Database Access     | MySQL/PostgreSQL access from app servers only                           |
| Microservices Setup | Each microservice gets its own SG for inter-service communication         |

---

## 💡 Troubleshooting Security Group Issues

1. ✅ Check **Inbound/Outbound** rules  
2. ✅ Check **Port & Protocol** match  
3. ✅ Ensure **SG association** with your instance  
4. ✅ Check **rule count limits** (max 50 per direction)  

