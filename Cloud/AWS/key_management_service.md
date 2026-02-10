# 🔐 What is AWS Key Management Service (KMS)?

**AWS KMS** is a fully managed service that allows you to create and control encryption keys used to encrypt your data. It ensures data confidentiality and integrity in the cloud and integrates with various AWS services using hardware security modules (HSMs).

---

## 🧱 Key Features of AWS KMS

| Feature                   | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Managed Keys (CMKs)**   | Create and manage Customer Master Keys for encryption                       |
| **Automatic Key Rotation**| Enable key rotation on a schedule                                           |
| **Access Control**        | Control key usage via IAM and KMS key policies                              |
| **AWS Integration**       | Easily integrates with S3, EBS, RDS, Lambda                                 |
| **Key Usage**             | Supports encryption, decryption, digital signatures, key generation         |
| **Audit & Monitoring**    | Integrated with CloudTrail to log all key usage                             |
| **Encryption**            | Protects data both **at rest** and **in transit**                           |

---

## 🧑‍💻 How AWS KMS Works

1. **Create CMK (Customer Master Key)**  
   - Symmetric or asymmetric  
   - Symmetric = same key for encryption/decryption  
   - Asymmetric = public/private key pair  

2. **Encrypt Data**  
   - Use KMS CMK to encrypt application data  

3. **Control Access**  
   - Use IAM + KMS Key policies to manage usage  

4. **Monitor Key Usage**  
   - CloudTrail logs help you audit who accessed what, when

---

## 🧩 Key Concepts in KMS

| Term                 | Description                                                                     |
|----------------------|---------------------------------------------------------------------------------|
| **CMK**              | Logical key used for encryption/decryption (symmetric/asymmetric)               |
| **Symmetric Keys**   | Same key used for both encryption and decryption                                |
| **Asymmetric Keys**  | Public key = encrypt, Private key = decrypt                                     |
| **Data Keys**        | Temporary keys used outside of KMS for large file encryption                    |
| **Key Policies**     | JSON docs that define who can manage/use a CMK                                  |
| **IAM Policies**     | IAM-based control for users/roles to access CMKs                                |
| **Key Rotation**     | Auto-rotate CMKs annually                                                       |
| **Key Aliases**      | Friendly names to simplify management                                           |

---

## 🛡️ Types of Keys in KMS

### 1. **Symmetric Keys**
- Most commonly used  
- Same key encrypts/decrypts  
- 🔄 Auto-rotation supported  
- ✅ Use case: S3, RDS, EBS encryption

### 2. **Asymmetric Keys**
- Public key for encryption  
- Private key for decryption  
- ✅ Use case: Digital signatures, SSL/TLS, secure sharing

### 3. **Custom Key Stores**
- Use external HSMs  
- Control key storage location (for compliance)

---

## 🔐 Managing Keys in AWS KMS

- **Create CMKs**: Through AWS Console, CLI, or SDKs  
- **Rotate Keys**: Auto-rotation every 12 months (optional)  
- **Delete Keys**: 7–30 day waiting period for key deletion  
- **Access Control**: Use IAM, key policies, and resource policies

---

## 📋 CLI Example to Create & Use Keys

### Create a symmetric CMK
```bash
aws kms create-key --description "My Symmetric Key" --key-usage ENCRYPT_DECRYPT
```

### Encrypt data
```bash
aws kms encrypt \\
  --key-id <CMK-ID> \\
  --plaintext fileb://myfile.txt \\
  --output text --query CiphertextBlob
```

### Decrypt data
```bash
aws kms decrypt \\
  --ciphertext-blob fileb://encryptedfile.txt \\
  --output text --query Plaintext
```

---

## 🔍 Key Management Best Practices

1. ✅ **Enable Key Rotation** — reduce key exposure risk  
2. 🔒 **Least Privilege** — restrict who can use/manage keys  
3. 📋 **Audit with CloudTrail** — log and monitor access  
4. ❗ **Delay Key Deletion** — avoid loss of encrypted data  
5. 🧯 **Use External HSMs** — for regulatory compliance  

---

## 📊 Use Cases of AWS KMS

| Use Case                   | Description                                                        |
|----------------------------|--------------------------------------------------------------------|
| **Encrypting Data at Rest**| Encrypt S3, EBS, RDS, DynamoDB data                                |
| **Digital Signatures**     | Sign/verify messages using asymmetric keys                         |
| **Data in Transit**        | Encrypt secure transmission channels                              |
| **Key Storage for Apps**   | Safely manage app-level keys and credentials                      |
| **Auditing/Compliance**    | Use with CloudTrail for detailed logs and compliance validation   |

---

## 🧠 AWS KMS vs. AWS Secrets Manager

| Feature            | AWS KMS                                   | AWS Secrets Manager                                     |
|--------------------|--------------------------------------------|----------------------------------------------------------|
| Use Case           | Encryption key management                  | Secure secret storage (API keys, DB creds, etc.)         |
| Rotation           | Automatic CMK rotation                     | Secret rotation policies                                 |
| Access             | IAM & key policies                         | IAM & resource policies                                  |
| Integration        | With S3, EBS, RDS, Lambda                  | With RDS, Redshift, custom apps                          |

