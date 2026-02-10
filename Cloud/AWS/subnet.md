# AWS Subnet – Notes

## 🌐 What is a Subnet in AWS?
**Subnet** = A segment of your VPC’s IP address range  

In AWS, a Subnet is essentially a **logical division** of the Virtual Private Cloud (VPC) network.  
It allows you to group resources in your VPC and manage network traffic effectively.  
Subnets help organize and isolate different parts of your infrastructure based on security or networking requirements.

---

## 🧱 Key Characteristics of Subnets

| Feature | Description |
|---------|-------------|
| CIDR Block | A range of IP addresses (e.g., 10.0.0.0/24 for 256 IPs) |
| Private vs Public | Subnets can be public (internet access) or private (no direct internet access) |
| Availability Zone | Subnets are associated with a specific AZ, improving high availability |
| Route Table | Each subnet is linked to a Route Table which defines traffic routing |

---

## 🔀 Public vs Private Subnets

| Subnet Type | Description | Access |
|-------------|------------|-------|
| Public | Subnet with direct internet access via Internet Gateway (IGW) | Internet Access |
| Private | Subnet without direct internet access but can route via NAT or VPN Gateway | No Direct Internet Access |
| Isolated | Subnet with no internet access, accessible only within VPC | No Access |

---

## 🛣️ Routing with Subnets
Each subnet has an **associated Route Table** that directs traffic based on destination:  
- **Public Subnet:** Route traffic to the Internet Gateway (IGW)  
- **Private Subnet:** Route traffic to a NAT Gateway for internet access  

---

## 📋 Example of Subnet Usage
- **Public Subnet:** Web servers, Load Balancers (need internet access)  
- **Private Subnet:** Databases, internal services (no direct internet access)  

---

## 🧠 Benefits of Subnets in VPC Design
- **Security:** Place resources with different security needs in different subnets; apply distinct Security Groups and Network ACLs.  
- **High Availability:** Distribute subnets across multiple Availability Zones (AZs).  
- **Efficient Traffic Routing:** Control traffic using Route Tables, NAT Gateways, and VPNs.  

---

## 🏗️ CloudFormation Example of Subnet Creation

```yaml
Resources:
  MyVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16

  PublicSubnet:
    Type: AWS::EC2::Subnet
