# Auto Scaling Design

## Overview

Amazon EC2 Auto Scaling automatically adjusts the number of running EC2 instances based on application demand.

This ensures high availability, fault tolerance, and cost optimization by launching or terminating instances as needed.

---

# Architecture

The Auto Scaling Group (ASG) manages application instances deployed across two Availability Zones.

Components:

- Launch Template
- Auto Scaling Group
- Target Group
- Application Load Balancer
- CloudWatch Alarms

---

# Launch Template

The Launch Template defines the configuration used when launching new EC2 instances.

| Property | Value |
|----------|---------|
| AMI | Amazon Linux 2023 |
| Instance Type | t3.micro |
| IAM Role | EC2 Instance Role |
| Security Group | App EC2 Security Group |
| User Data | Bootstrap Script |
| Monitoring | Enabled |

---

# Auto Scaling Group Configuration

| Property | Value |
|----------|---------|
| Desired Capacity | 2 |
| Minimum Capacity | 2 |
| Maximum Capacity | 6 |
| Availability Zones | 2 |
| Health Check Type | ELB |
| Health Check Grace Period | 300 Seconds |

The ASG distributes EC2 instances evenly across both Availability Zones.

---

# Scaling Policies

Target Tracking Scaling is used to automatically adjust capacity.

Example policies:

| Metric | Target |
|---------|--------|
| Average CPU Utilization | 60% |
| ALB Request Count per Target | Configurable |

---

# Scale Out

When demand increases:

1. CloudWatch detects increased load.
2. Auto Scaling launches additional EC2 instances.
3. New instances are configured using the Launch Template.
4. Instances register automatically with the Target Group.
5. The ALB begins routing traffic to healthy instances.

---

# Scale In

When demand decreases:

1. CloudWatch detects reduced utilization.
2. Auto Scaling terminates unnecessary instances.
3. Existing requests complete before instance termination.
4. Desired capacity is restored.

---

# Health Checks

Health checks are performed using:

- Amazon EC2 Status Checks
- Application Load Balancer Health Checks

If an instance fails:

- It is marked unhealthy.
- Traffic is stopped.
- The instance is terminated.
- A replacement instance is launched automatically.

---

# High Availability

The Auto Scaling Group improves availability by:

- Deploying instances across multiple Availability Zones.
- Automatically replacing unhealthy instances.
- Maintaining the desired capacity.

---

# Monitoring

Amazon CloudWatch monitors:

- CPU Utilization
- Network Traffic
- Auto Scaling Events
- Instance Count
- Scaling Activities

CloudWatch Alarms trigger scaling actions and can notify administrators through Amazon SNS.

---

# Auto Scaling Best Practices

✔ Multi-AZ Deployment

✔ Launch Templates

✔ Target Tracking Policies

✔ Automatic Health Checks

✔ Desired Capacity Maintenance

✔ CloudWatch Monitoring

✔ Integration with Application Load Balancer

---

# Summary

Amazon EC2 Auto Scaling provides automatic scaling, self-healing, and high availability by dynamically adjusting compute capacity based on application demand while maintaining consistent application performance.
