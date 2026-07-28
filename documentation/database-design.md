# Database Design

## Overview

The database layer provides reliable, highly available, and secure data storage for the application.

Amazon RDS is deployed in a Multi-AZ configuration to ensure automatic failover, high availability, and data durability.

---

# Database Architecture

The database layer consists of:

- Amazon RDS
- Multi-AZ Deployment
- Private Database Subnets
- DB Subnet Group
- Security Group
- Automated Backups

---

# Database Engine

The solution supports one of the following managed database engines:

| Property | Value |
|----------|---------|
| Engine | MySQL or PostgreSQL |
| Deployment | Amazon RDS |
| Availability | Multi-AZ |
| Storage | General Purpose SSD (gp3) |
| Encryption | Enabled |

---

# Multi-AZ Deployment

Amazon RDS maintains:

- One Primary Database Instance
- One Standby Database Instance

The standby instance is located in a different Availability Zone.

Benefits include:

- Automatic failover
- Improved availability
- Reduced downtime
- Data redundancy

---

# DB Subnet Group

A DB Subnet Group is created using the dedicated private database subnets.

Example:

| Subnet | Availability Zone |
|----------|-------------------|
| Private DB Subnet A | AZ-A |
| Private DB Subnet B | AZ-B |

The database is never deployed inside public subnets.

---

# Security

The database is protected using a dedicated Security Group.

Inbound connections are allowed only from the EC2 Application Security Group.

No direct internet access is permitted.

---

# Connectivity

Application servers communicate with Amazon RDS using private networking.

Connection flow:

EC2 → Security Group → Amazon RDS

No public endpoint is required for application traffic.

---

# Backup Strategy

Amazon RDS provides automated backup capabilities.

Features include:

- Automated daily backups
- Point-in-Time Recovery (PITR)
- Automated snapshots
- Manual snapshots (optional)

Backup retention can be configured based on business requirements.

---

# Monitoring

Amazon CloudWatch monitors database performance.

Common metrics include:

- CPU Utilization
- Free Storage Space
- Database Connections
- Read Latency
- Write Latency
- Freeable Memory

CloudWatch Alarms can notify administrators using Amazon SNS.

---

# High Availability

The database layer achieves high availability through:

- Multi-AZ deployment
- Automatic failover
- Redundant storage
- Managed database service

---

# Database Best Practices

✔ Deploy databases in private subnets

✔ Enable Multi-AZ

✔ Enable automated backups

✔ Encrypt storage

✔ Restrict inbound access

✔ Monitor performance using CloudWatch

✔ Use Security Groups instead of public access

---

# Summary

The database layer provides a secure, resilient, and highly available data platform using Amazon RDS Multi-AZ while following AWS Well-Architected Framework best practices.
