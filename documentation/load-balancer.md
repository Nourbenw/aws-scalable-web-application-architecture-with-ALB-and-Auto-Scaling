# Load Balancer Design

## Overview

The Application Load Balancer (ALB) is the entry point for all incoming application traffic.

It distributes requests across multiple EC2 instances running in different Availability Zones, ensuring high availability, scalability, and fault tolerance.

---

# Load Balancer Architecture

The Application Load Balancer provides:

- Layer 7 (HTTP/HTTPS) Load Balancing
- SSL/TLS Termination
- Health Checks
- Cross-Zone Load Balancing
- Target Group Routing

---

# Deployment

The ALB is deployed across two public subnets.

| Property | Value |
|----------|---------|
| Type | Application Load Balancer |
| Scheme | Internet-facing |
| IP Address Type | IPv4 |
| Availability Zones | 2 |
| Subnets | Public Subnet A & Public Subnet B |

---

# Listeners

## HTTP Listener

| Port | Action |
|------|--------|
| 80 | Redirect to HTTPS |

---

## HTTPS Listener

| Port | Action |
|------|--------|
| 443 | Forward requests to Target Group |

TLS certificates are managed using AWS Certificate Manager (ACM).

---

# Target Group

The Target Group contains the EC2 instances managed by the Auto Scaling Group.

Configuration:

| Property | Value |
|----------|---------|
| Target Type | Instance |
| Protocol | HTTP |
| Port | 80 |
| Health Checks | Enabled |

---

# Health Checks

The ALB continuously monitors application health.

Example configuration:

| Setting | Value |
|----------|---------|
| Protocol | HTTP |
| Path | /health |
| Healthy Threshold | 3 |
| Unhealthy Threshold | 2 |
| Timeout | 5 seconds |
| Interval | 30 seconds |

Unhealthy instances are automatically removed from service until they recover or are replaced.

---

# Cross-Zone Load Balancing

Cross-Zone Load Balancing distributes traffic evenly across all healthy targets, regardless of Availability Zone.

Benefits:

- Improved traffic distribution
- Better resource utilization
- Higher availability

---

# SSL/TLS

HTTPS is enabled using certificates from AWS Certificate Manager (ACM).

Benefits:

- Encrypts client communication
- Protects sensitive data
- Improves security compliance

---

# Integration

The ALB integrates with:

- Amazon Route 53
- Amazon CloudFront
- AWS WAF
- Auto Scaling Group
- CloudWatch
- Amazon SNS

---

# Monitoring

Amazon CloudWatch monitors:

- Request Count
- Target Response Time
- HTTP 4XX Errors
- HTTP 5XX Errors
- Healthy Host Count
- Unhealthy Host Count

CloudWatch Alarms notify administrators using Amazon SNS.

---

# Load Balancer Best Practices

✔ Deploy across multiple Availability Zones

✔ Enable Cross-Zone Load Balancing

✔ Redirect HTTP to HTTPS

✔ Enable Health Checks

✔ Use Target Groups

✔ Integrate with AWS WAF

✔ Monitor using CloudWatch

---

# Summary

The Application Load Balancer provides secure, highly available, and scalable traffic distribution while ensuring that requests are routed only to healthy application instances.
