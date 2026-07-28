# Compute Layer Design

## Overview

The compute layer hosts the application and provides scalable, highly available processing for incoming requests.

The solution uses Amazon EC2 instances deployed in private subnets and managed by an Auto Scaling Group (ASG).

---

# Compute Architecture

The compute layer consists of:

- Amazon EC2
- Launch Template
- Auto Scaling Group
- Target Group
- AWS Systems Manager
- CloudWatch Agent

---

# Amazon EC2

Application servers run on Amazon EC2 instances.

Deployment characteristics:

- Private Subnets
- No Public IP Address
- IAM Role attached
- Managed using AWS Systems Manager
- Registered with an Application Load Balancer

---

# Launch Template

The Launch Template defines the configuration for EC2 instances.

Configuration includes:

| Property | Value |
|----------|---------|
| AMI | Amazon Linux 2023 |
| Instance Type | t3.micro (example) |
| IAM Role | EC2 Instance Role |
| Security Group | App EC2 Security Group |
| User Data | Application bootstrap script |
| Monitoring | Enabled |

---

# User Data

User Data automatically configures new instances during launch.

Typical tasks include:

- Install application dependencies
- Install web server
- Configure application
- Start required services
- Install CloudWatch Agent

This ensures every instance is configured consistently.

---

# Auto Scaling Group

The Auto Scaling Group automatically manages EC2 capacity.

Responsibilities:

- Launch healthy instances
- Replace failed instances
- Scale based on demand
- Distribute instances across Availability Zones

---

# Scaling Policy

Target Tracking Scaling is used.

Example metrics:

| Metric | Target |
|---------|--------|
| Average CPU Utilization | 60% |
| ALB Request Count | Configurable |

Benefits:

- Automatic scaling
- Cost optimization
- Improved performance

---

# Health Checks

Health checks are performed by:

- Amazon EC2
- Application Load Balancer

If an instance becomes unhealthy:

1. Target Group marks it unhealthy.
2. Auto Scaling terminates the instance.
3. A replacement instance is launched automatically.

---

# High Availability

The compute layer achieves high availability through:

- Multiple Availability Zones
- Auto Scaling Group
- Elastic Load Balancing
- Automatic instance replacement

---

# Monitoring

Amazon CloudWatch monitors:

- CPU Utilization
- Memory Usage (CloudWatch Agent)
- Disk Usage
- Network Traffic
- Instance Status

CloudWatch Alarms notify administrators using Amazon SNS.

---

# Compute Best Practices

✔ Private EC2 Instances

✔ No Public IP Addresses

✔ Launch Templates

✔ Auto Scaling

✔ IAM Roles

✔ CloudWatch Monitoring

✔ Systems Manager Access

✔ Health Checks

---

# Summary

The compute layer provides secure, scalable, and fault-tolerant application hosting using Amazon EC2, Auto Scaling, and Launch Templates while following AWS Well-Architected best practices.
