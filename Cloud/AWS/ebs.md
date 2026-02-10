# What is EBS in AWS?

**EBS** stands for **Elastic Block Store**. It’s a type of storage service in AWS that provides **block-level storage volumes** for use with **EC2 instances**.

---

## 🔧 In Simple Terms:
Think of **EBS** like a **hard drive** you can attach to your EC2 (virtual) machine. You can:

- Store files, data, logs, etc.
- Install operating systems
- Detach it and attach to another instance if needed
- Take backups using snapshots

---

## 🔑 Key Features:

- **Durable & Persistent**: Your data stays even after you stop or reboot the instance.
- **Scalable**: You can increase the size anytime.
- **Encrypted**: Supports encryption for security.
- **Snapshots**: You can create backups easily.
- **Types**: Different types for different needs—like:
  - General Purpose (gp3)
  - Provisioned IOPS (io2)
  - Throughput Optimized HDD (st1)
  - Cold HDD (sc1)

---

## 📌 Use Case Example:

- You launch an **EC2 instance** to run a web server.
- You attach an **EBS volume** to it to store the server’s files, logs, and database.
- You can take **daily snapshots** of that volume for backup.


