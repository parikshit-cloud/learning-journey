# AWS Route Table – Notes

## 🛣️ What is a Route Table in AWS?
**Route Table** = Network Traffic Map  

A Route Table in AWS is a set of **rules (routes)** that determine where network traffic is directed within a **Virtual Private Cloud (VPC)**.  
Think of it like the GPS for your AWS network — it tells traffic how to get from one place to another.

---

## 🔧 Where is it used?
- Inside a **VPC**  
- Attached to **subnets**  
- Routes traffic between:  
  - Subnets  
  - Internet  
  - VPNs  
  - Peered VPCs  
  - NAT Gateways  

---

## 🧱 Key Components

| Component | Description |
|-----------|-------------|
| Destination | IP address range (e.g., 0.0.0.0/0 for all traffic) |
| Target | Where to send traffic (e.g., IGW, NAT, local, ENI) |
| Main Route Table | Default table every subnet is associated with (can be changed) |
| Custom Route Table | User-created table you can attach to specific subnets |

---

## 📍 Example Route Table

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | local |
| 0.0.0.0/0   | igw-abc123 (Internet Gateway) |
| 172.31.0.0/16 | pcx-xyz123 (VPC Peering) |

---

## 🌐 Common Targets

| Target Type | Used For |
|-------------|---------|
| local | Inside the same VPC |
| IGW | Internet access (public subnet) |
| NAT Gateway | Internet for private subnets |
| VPC Peering | Access another VPC |
| VPN Gateway | On-premise via VPN |
| Transit Gateway | Central hub for VPCs/VPNs |

---

## 🧠 Public vs Private Subnet (Based on Route Table)

| Subnet Type | Route to Internet? | Target |
|-------------|-----------------|--------|
| Public | Yes (via IGW) | igw-xxxx |
| Private | Yes (via NAT Gateway) | nat-xxxx |
| Isolated | No Internet route | none |

---

## 📋 CLI Example

```bash
# List route tables
aws ec2 describe-route-tables

# Create a new route table
aws ec2 create-route-table --vpc-id vpc-abc123

# Add a route to IGW
aws ec2 create-route \
  --route-table-id rtb-123456 \
  --destination-cidr-block 0.0.0.0/0 \
  --gateway-id igw-123456

# Associate with subnet
aws ec2 associate-route-table \
  --subnet-id subnet-abc123 \
  --route-table-id rtb-123456
