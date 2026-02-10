# 🌍 Terraform – Complete Notes & Interview Scenarios (2–3 Years DevOps)

## 📌 What is Terraform?

Terraform is an **open-source Infrastructure as Code (IaC)** tool developed by **HashiCorp**.  
It allows you to **provision, manage, and version infrastructure** such as servers, databases, networks, and cloud resources using **declarative configuration files**.

---

## ⭐ Key Features

- **Infrastructure as Code (IaC)**  
  Define infrastructure using `.tf` files written in **HCL (HashiCorp Configuration Language)**.

- **Multi-Cloud Support**  
  Works with AWS, Azure, GCP, Kubernetes, Docker, and many more providers.

- **Version Control Friendly**  
  Infrastructure code can be tracked, reviewed, and audited using Git.

- **Idempotent**  
  Running the same Terraform code multiple times does not change infrastructure unless the configuration changes.

---

## 🧪 Basic Terraform Example (AWS EC2)

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}

🎯 Terraform – DevOps Interview Q&A (2–3 Years Experience)
🧱 1. Basics
Q1: What is Terraform?

A: Terraform is an open-source Infrastructure as Code (IaC) tool by HashiCorp used to provision and manage infrastructure across cloud providers.

Q2: What language does Terraform use?

A: Terraform uses HCL (HashiCorp Configuration Language), which is easy to read and write.

Q3: What are Terraform Providers?

A: Providers are plugins that allow Terraform to interact with APIs like AWS, Azure, Docker, Kubernetes, etc.

⚙️ 2. Key Terraform Commands
Command	Purpose
terraform init	Initializes the working directory
terraform plan	Shows what changes will be made
terraform apply	Applies infrastructure changes
terraform destroy	Destroys managed infrastructure
terraform fmt	Formats .tf files
📦 3. Core Concepts
Q4: What is a Terraform State File?

A: The .tfstate file stores the current state of infrastructure and helps Terraform track resources.

Q5: How do you manage Terraform state in a team?

A: Use remote backends like S3 with DynamoDB for state locking.

Q6: What is a Terraform Module?

A: A reusable block of Terraform code that helps standardize and reuse infrastructure.

🔐 4. Terraform in DevOps Use Cases
Q7: How do you use Terraform in CI/CD?

A: Terraform is integrated into pipelines (Jenkins, GitHub Actions) to run:

terraform init

terraform plan

terraform apply

Q8: How does Terraform improve security?

A:

Eliminates manual configuration errors

Enforces consistent IAM policies

Enables audit trails through version control

🔄 5. Terraform with AWS Example
Q9: How do you create an EC2 instance using Terraform?
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "myec2" {
  ami           = "ami-0abcdef1234567890"
  instance_type = "t2.micro"
}

Q10: How do you pass variables in Terraform?
Define Variable
variable "region" {
  default = "us-east-1"
}

Use Variable
provider "aws" {
  region = var.region
}

Pass at Runtime
terraform apply -var="region=us-west-2"

🧠 Bonus Interview Tips

✅ Mention that you:

Use Git for version control

Manage environments using workspaces

Use modules for reusable infrastructure

Store secrets in AWS Secrets Manager / Vault

Enable state locking

🔧 Real Terraform Scenario-Based Interview Questions
1️⃣ Environment-Specific Infrastructure

Q: How do you deploy the same infrastructure for dev and prod?

A:

Use workspaces or

Use separate .tfvars files

terraform workspace new dev
terraform workspace select prod

2️⃣ State File Conflict

Q: Two people ran terraform apply simultaneously. What now?

A:

Use remote backend (S3 + DynamoDB)

Recover using:

terraform state mv
terraform state rm

3️⃣ Apply Fails After Plan

Q: Plan succeeds, apply fails due to IAM permission.

A:

Check IAM role permissions

Review CloudTrail

Verify required actions like ec2:CreateInstance

4️⃣ Avoid Code Duplication

Q: Create 5 S3 buckets with similar config.

resource "aws_s3_bucket" "buckets" {
  for_each = toset(["bucket1", "bucket2", "bucket3"])
  bucket   = each.key
  acl      = "private"
}

5️⃣ Secrets Committed to Git

Q: You committed DB passwords accidentally.

A:

Rotate credentials immediately

Remove from Git history (BFG / filter-branch)

Use Secrets Manager or Vault

6️⃣ Resource Dependency

Q: Lambda needs IAM role first.

depends_on = [aws_iam_role.lambda_role]

7️⃣ Prevent Accidental Destroy

Q: Someone ran terraform destroy on prod.

lifecycle {
  prevent_destroy = true
}

8️⃣ Conditional Resource Creation
resource "aws_instance" "optional" {
  count = var.create_instance ? 1 : 0
}

9️⃣ Drift Detection

Q: Infra modified manually.

A:

Run terraform plan

Reconcile with terraform apply

🔟 Shared Infrastructure

Q: Reuse VPCs/IAM across teams.

module "vpc" {
  source = "git::https://github.com/org/vpc-module.git?ref=v1.0.0"
}

🚨 10 Terraform “What Happens If…” Questions

State file deleted → Terraform recreates resources

Multiple applies → State corruption risk

Partial apply failure → Incomplete infra

API rate limits hit → Apply fails mid-way

Manual infra change → Drift detected on plan

Resource removed from code → Terraform destroys it

Provider API change → Compatibility issues

Circular dependency → Plan fails

AWS quota exceeded → Resource creation fails

Remote backend unavailable → All Terraform ops blocked
