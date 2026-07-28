# Networking Design

## Overview

The networking layer provides a secure, scalable, and highly available foundation for the application.

The architecture is deployed inside a dedicated Amazon Virtual Private Cloud (VPC) spanning two Availability Zones.

---

# VPC Configuration

| Property | Value |
|----------|---------|
| VPC Name | Production VPC |
| CIDR Block | 10.0.0.0/16 |
| Availability Zones | 2 |
| Public Subnets | 2 |
| Private Application Subnets | 2 |
| Private Database Subnets | 2 |

---

# Subnet Design

## Public Subnets

Public subnets contain internet-facing resources.

Resources deployed:

- Application Load Balancer
- NAT Gateway

Example:

| Subnet | CIDR |
|---------|------|
| Public Subnet A | 10.0.1.0/24 |
| Public Subnet B | 10.0.2.0/24 |

---

## Private Application Subnets

Application servers are deployed inside private subnets to prevent direct internet access.

Resources deployed:

- EC2 Instances
- Auto Scaling Group

Example:

| Subnet | CIDR |
|---------|------|
| Private App Subnet A | 10.0.11.0/24 |
| Private App Subnet B | 10.0.12.0/24 |

---

## Private Database Subnets

The database layer is isolated inside dedicated private subnets.

Resources deployed:

- Amazon RDS Multi-AZ

Example:

| Subnet | CIDR |
|---------|------|
| Private DB Subnet A | 10.0.21.0/24 |
| Private DB Subnet B | 10.0.22.0/24 |

---

# Internet Gateway

An Internet Gateway (IGW) is attached to the VPC.

Responsibilities:

- Internet connectivity for public subnets.
- Allows inbound traffic to the Application Load Balancer.
- Allows outbound internet access.

---

# NAT Gateway

A NAT Gateway is deployed in each public subnet.

Purpose:

- Allow private EC2 instances to download updates.
- Access AWS services without exposing public IP addresses.

Benefits:

- High Availability
- Secure outbound internet access

---

# Route Tables

## Public Route Table

Routes:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Associated with:

- Public Subnet A
- Public Subnet B

---

## Private Route Tables

Routes:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | NAT Gateway |

Associated with:

- Private Application Subnets
- Private Database Subnets

---

# Network ACLs

Separate Network ACLs are configured for:

- Public Subnets
- Private Application Subnets
- Private Database Subnets

These provide stateless traffic filtering in addition to Security Groups.

---

# High Availability

The networking layer achieves high availability through:

- Multiple Availability Zones
- Redundant NAT Gateways
- Distributed public and private subnets
- Fault-tolerant routing

---

# Networking Best Practices

✔ Dedicated VPC

✔ Multi-AZ Deployment

✔ Least Exposure

✔ Private Compute Layer

✔ Private Database Layer

✔ Internet-facing ALB only

✔ Highly Available NAT Gateways

---

# Summary

The networking architecture provides secure isolation, controlled internet access, and high availability while following AWS networking best practices.
