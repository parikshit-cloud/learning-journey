# AWS Route 53 – Notes

## 🌐 What is Route 53 in AWS?
**Route 53** = Scalable DNS & Domain Management Service  

Amazon Route 53 is a **highly available and scalable Domain Name System (DNS) web service**.  
It translates domain names (like `example.com`) into IP addresses, routes internet traffic, and can register/manage domain names.

---

## 📦 Core Features of Route 53

| Feature | Description |
|---------|-------------|
| DNS Service | Resolves domain names to IP addresses |
| Domain Registration | Register and manage domains within AWS |
| Health Checks | Monitor endpoint health (e.g., EC2, web app) |
| Traffic Routing Policies | Control how traffic is routed across endpoints |
| Highly Available | Uses AWS’s global infrastructure (Anycast-based) |

---

## 🔀 Routing Policies

| Policy Type | Description |
|------------|-------------|
| Simple | One record → one resource (default) |
| Weighted | Split traffic based on weights (e.g., 70/30 split) |
| Latency-based | Route to lowest-latency region |
| Failover | Active-passive routing with health checks |
| Geolocation | Route based on user’s location (country/region) |
| Geoproximity | Route based on location bias (with traffic flow) |
| Multivalue Answer | Return multiple IPs (with health checks) |

---

## 🧱 Key Components

| Term | Meaning |
|------|---------|
| Hosted Zone | Container for records in a domain (like a DNS zone) |
| Record Set (DNS Record) | Defines how Route 53 responds to queries (e.g., A, CNAME, MX) |
| Health Check | Monitors resources and supports failover |

---

## 🔧 Common DNS Record Types

| Type | Use Case |
|------|---------|
| A | Maps domain → IPv4 |
| AAAA | Maps domain → IPv6 |
| CNAME | Alias to another domain |
| MX | Mail server routing |
| TXT | Used for verification (e.g., SPF, DKIM) |
| NS | Name servers for the domain |
| SRV | Service location records |

---

## 🌍 Example Use Case

You have a global app hosted in:  
- `us-east-1` and `eu-west-1`  
- Use **Latency-based routing**  
- If `us-east-1` fails → Route 53 fails over to `eu-west-1`  
- DNS: `myapp.com` → routes to the best-performing server

---

## 📋 Sample CLI Commands

```bash
# List hosted zones
aws route53 list-hosted-zones

# Create a hosted zone
aws route53 create-hosted-zone --name example.com \
  --caller-reference 123456789

# Change a DNS record
aws route53 change-resource-record-sets \
  --hosted-zone-id Z12345678 \
  --change-batch file://dns-change.json
