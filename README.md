# 🚀 Scalable Web Application with ALB and Auto Scaling

A production-grade AWS architecture demonstrating how to deploy a highly available, scalable, and secure web application using Amazon Web Services (AWS).

This project follows AWS Well-Architected Framework best practices and implements a multi-tier architecture across multiple Availability Zones.

---

# 📖 Project Overview

This solution demonstrates how to build a resilient and scalable web application infrastructure using AWS native services.

The architecture is designed to provide:

- High Availability
- Fault Tolerance
- Automatic Scaling
- Secure Network Design
- Monitoring & Logging
- Low Latency Content Delivery

---

# 🏗️ Solution Architecture

![AWS Solution Architecture](architecture/aws-solution-architecture.png)

## 🔄 Request Flow

The application processes client requests through a secure and highly available architecture:

1. Users access the application using **Amazon Route 53**.
2. **Amazon CloudFront** serves cached static content and forwards dynamic requests.
3. **AWS WAF** filters malicious traffic before it reaches the application.
4. The **Application Load Balancer (ALB)** distributes requests across healthy EC2 instances.
5. **Amazon EC2** instances run inside private subnets and scale automatically using an **Auto Scaling Group (ASG)**.
6. Application data is stored in **Amazon RDS Multi-AZ**, providing automatic failover and high availability.
7. **Amazon CloudWatch** collects metrics and logs from AWS resources.
8. **Amazon SNS** sends notifications when alarms are triggered.
9. **AWS Systems Manager Session Manager** provides secure administrative access without exposing SSH to the internet.

---

# ☁️ AWS Services Used

| Service | Purpose |
|----------|---------|
| Amazon VPC | Network isolation |
| Amazon EC2 | Application servers |
| Auto Scaling Group | Automatic scaling |
| Application Load Balancer | Traffic distribution |
| Amazon CloudFront | Global CDN |
| AWS WAF | Web application firewall |
| Amazon Route 53 | DNS & Health Checks |
| Amazon RDS Multi-AZ | Highly available database |
| AWS Systems Manager | Secure instance access |
| Amazon CloudWatch | Monitoring |
| Amazon SNS | Notifications |

---

# 🌐 Architecture Features

- Multi-AZ Deployment
- Public & Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Network ACLs
- Auto Scaling
- Application Load Balancer
- CloudFront CDN
- AWS WAF Protection
- RDS Multi-AZ
- Session Manager
- CloudWatch Monitoring

---

# 📂 Repository Structure

```text
.
├── architecture/
├── documentation/
├── infrastructure/
├── screenshots/
└── README.md
```

---

# 📌 Project Status

🚧 In Progress

This repository is being updated step by step while building the complete AWS infrastructure.

---

# 📄 License

This project is for educational and portfolio purposes.
