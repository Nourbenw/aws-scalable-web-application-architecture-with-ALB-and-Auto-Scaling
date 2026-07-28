# Security Design

## Overview

Security is implemented using multiple layers of protection to ensure confidentiality, integrity, and availability of the application.

The architecture follows the AWS Shared Responsibility Model and applies the principle of least privilege.

---

# Security Architecture

The solution protects the application using:

- AWS WAF
- Security Groups
- Network ACLs
- IAM Roles
- AWS Systems Manager Session Manager
- HTTPS Encryption
- Private Subnets
- Amazon RDS Security
- CloudFront
- Application Load Balancer

---

# Security Groups

Security Groups provide stateful firewall protection for AWS resources.

## Application Load Balancer Security Group

### Inbound Rules

| Protocol | Port | Source | Purpose |
|----------|------|--------|---------|
| HTTPS | 443 | 0.0.0.0/0 | Secure web traffic |
| HTTP | 80 | 0.0.0.0/0 | Redirect HTTP to HTTPS |

### Outbound Rules

| Protocol | Destination |
|----------|-------------|
| All | EC2 Security Group |

---

## EC2 Security Group

The application servers are deployed in private subnets and cannot be accessed directly from the internet.

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| HTTP | 80 | ALB Security Group |
| HTTPS | 443 | ALB Security Group |

### Outbound Rules

| Protocol | Destination |
|----------|-------------|
| MySQL (3306) / PostgreSQL (5432) | RDS Security Group |
| HTTPS (443) | Internet (via NAT Gateway) |

---

## RDS Security Group

The database accepts connections only from the application layer.

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| MySQL (3306) | EC2 Security Group |
| PostgreSQL (5432) | EC2 Security Group |

No direct internet access is allowed.

---

# Network ACLs

Separate Network ACLs are configured for:

- Public Subnets
- Private Application Subnets
- Private Database Subnets

These provide stateless packet filtering in addition to Security Groups.

---

# IAM Roles

EC2 instances use IAM Roles instead of long-term access keys.

Permissions include:

- CloudWatch Agent
- Systems Manager
- Parameter Store (read-only)
- S3 access (if required)

No AWS credentials are stored on the instances.

---

# AWS WAF

AWS Web Application Firewall protects the application from common web attacks.

Enabled protections include:

- SQL Injection (SQLi)
- Cross-Site Scripting (XSS)
- Known Bad Inputs
- Rate Limiting
- IP Reputation Lists

---

# Session Manager

Administrative access is provided through AWS Systems Manager Session Manager.

Benefits:

- No public SSH access
- No bastion host required
- Auditable sessions
- IAM-based access control

---

# HTTPS Encryption

Client traffic is encrypted using HTTPS.

TLS certificates are managed using AWS Certificate Manager (ACM).

Benefits:

- Secure communication
- Data confidentiality
- Data integrity

---

# Data Protection

The solution protects data using:

- Amazon RDS encryption at rest
- TLS encryption in transit
- Automated backups
- Multi-AZ replication

---

# Secrets Management

Application secrets should never be stored inside the application code.

Recommended services:

- AWS Secrets Manager
- AWS Systems Manager Parameter Store

Examples of managed secrets:

- Database credentials
- API keys
- Application secrets

---

# Security Best Practices

✔ Principle of Least Privilege

✔ Private Application Layer

✔ Private Database Layer

✔ Internet-facing ALB only

✔ Stateful Security Groups

✔ Stateless Network ACLs

✔ Web Application Firewall (AWS WAF)

✔ IAM Roles instead of Access Keys

✔ Encrypted communication (HTTPS)

✔ Secure administrative access using Session Manager

---

# Summary

The security architecture applies multiple layers of protection to minimize the attack surface while maintaining high availability and operational security across the environment.
