# ✅ What is IAM in AWS?

**IAM (Identity and Access Management)** is an AWS service that helps you securely control access to AWS services and resources. With IAM, you manage **who** can access **what** and **what actions** they can perform.

---

## 🧱 Key Features of IAM

| Feature                  | Description                                                                       |
|--------------------------|-----------------------------------------------------------------------------------|
| **Users**                | Individual identities (people/apps) within your AWS account                       |
| **Groups**               | Collection of IAM users for permission management                                 |
| **Roles**                | Identities intended to be assumed temporarily by users/services like EC2          |
| **Policies**             | JSON docs that define permissions                                                 |
| **Multi-Factor Auth (MFA)** | Adds extra security using a second factor (e.g., app)                             |

---

## 🧑‍💻 IAM Components Breakdown

### 1. Users
- Represent individuals or apps  
- Have credentials (username/password, access keys)  
- Example: User for a team member

### 2. Groups
- Collections of users  
- Assign permissions collectively  
- Example: Developers group with deploy permissions

### 3. Roles
- Can be assumed by users or AWS services  
- Use **temporary credentials**  
- Example: EC2 using a role to access S3

### 4. Policies
- JSON-based permission documents  
- Define **allow** and **deny** actions for resources

---

## 🔑 How IAM Works

1. **Authentication**: Verifies the user/service identity  
2. **Authorization**: Checks what actions are allowed/denied  
3. **Access Control**: Uses **IAM + resource policies** to determine access

---

## 🧩 IAM Policies

Policies define actions on specific resources.

### 📄 Example: Allow Read-Only Access to S3

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

### ❌ Example: Deny Delete Access

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

---

## 👥 IAM Users, Groups, and Roles

| Component     | Purpose                                                                 |
|----------------|-------------------------------------------------------------------------|
| **User**       | Individual credentials for login and access                             |
| **Group**      | Manage permissions for a set of users                                   |
| **Role**       | Provide temporary permissions to users/services                         |

### Example: EC2 Role for S3 Access

1. Create a role with EC2 as the trusted entity  
2. Attach `AmazonS3ReadOnlyAccess` policy  
3. Assign role to EC2 on launch

---

## 🔐 IAM Best Practices

1. **Least Privilege**: Grant only what is necessary  
2. **Enable MFA**: Add security to sensitive accounts  
3. **Use Roles**: For EC2, Lambda, instead of hardcoded credentials  
4. **Rotate Credentials**: Regularly change keys/passwords  
5. **Monitor with CloudTrail**: Audit actions using logs

---

## 🏗️ CloudFormation Example: Create IAM User & Policy

```yaml
Resources:
  MyIAMUser:
    Type: AWS::IAM::User
    Properties:
      UserName: "exampleuser"

  MyUserPolicy:
    Type: AWS::IAM::Policy
    Properties:
      PolicyName: "ReadOnlyS3Policy"
      Users:
        - Ref: MyIAMUser
      PolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: "Allow"
            Action: "s3:ListBucket"
            Resource: "arn:aws:s3:::my-bucket"
          - Effect: "Allow"
            Action: "s3:GetObject"
            Resource: "arn:aws:s3:::my-bucket/*"
```

> 🔧 This creates:
> - An IAM user named `exampleuser`  
> - Attaches read-only access to `my-bucket`

---

## 📋 CLI Example to Create IAM User

```bash
# Create IAM User
aws iam create-user --user-name exampleuser

# Attach ReadOnlyAccess Policy
aws iam attach-user-policy \\
  --user-name exampleuser \\
  --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess
```

---

## 💡 IAM Best Practice Tip

**Never use the root account** for daily tasks.  
✅ Create IAM users with least privilege for everything else.

