# Monitoring and Logging

## Overview

Monitoring is essential for maintaining application availability, performance, and operational visibility.

The solution uses Amazon CloudWatch for metrics, logs, dashboards, and alarms, while Amazon SNS provides real-time notifications.

---

# Monitoring Architecture

The monitoring layer consists of:

- Amazon CloudWatch
- CloudWatch Alarms
- CloudWatch Dashboards
- CloudWatch Logs
- Amazon SNS

---

# Amazon CloudWatch

Amazon CloudWatch collects metrics from AWS resources and the operating system.

Monitored resources include:

- Application Load Balancer
- Amazon EC2
- Auto Scaling Group
- Amazon RDS
- NAT Gateway

---

# CloudWatch Metrics

Common metrics include:

## EC2

- CPU Utilization
- Network In
- Network Out
- Disk Usage
- Memory Usage (CloudWatch Agent)

---

## Application Load Balancer

- Request Count
- Target Response Time
- Healthy Host Count
- Unhealthy Host Count
- HTTP 4XX Errors
- HTTP 5XX Errors

---

## Auto Scaling

- Desired Capacity
- In-Service Instances
- Pending Instances
- Scaling Activities

---

## Amazon RDS

- CPU Utilization
- Database Connections
- Read Latency
- Write Latency
- Free Storage Space
- Freeable Memory

---

# CloudWatch Logs

Application and operating system logs are centralized using CloudWatch Logs.

Typical log sources include:

- Application logs
- Web server logs
- System logs
- CloudWatch Agent logs

Centralized logging simplifies troubleshooting and operational analysis.

---

# CloudWatch Dashboards

Dashboards provide a consolidated view of infrastructure health.

Example dashboard widgets:

- EC2 CPU Utilization
- ALB Request Count
- ALB Response Time
- RDS CPU Utilization
- Healthy Host Count
- Auto Scaling Capacity

---

# CloudWatch Alarms

CloudWatch Alarms automatically detect abnormal conditions.

Example alarms:

| Alarm | Condition |
|--------|-----------|
| High CPU | CPU > 80% |
| High Response Time | Above threshold |
| Unhealthy Targets | Healthy Host Count decreases |
| Database Storage | Low Free Storage |
| High HTTP 5XX Errors | Above threshold |

---

# Amazon SNS

Amazon Simple Notification Service (SNS) delivers alert notifications.

Supported notification methods include:

- Email
- SMS
- AWS Lambda
- HTTPS Endpoints

Example alerts:

- EC2 instance failure
- Auto Scaling event
- Database storage warning
- High application latency
- Load balancer health issues

---

# Operational Benefits

Monitoring provides:

- Early issue detection
- Faster incident response
- Performance visibility
- Capacity planning
- Operational insights

---

# Monitoring Best Practices

✔ Enable detailed monitoring

✔ Centralize logs

✔ Configure CloudWatch Dashboards

✔ Create actionable alarms

✔ Notify administrators using Amazon SNS

✔ Continuously monitor application health

---

# Summary

The monitoring solution provides comprehensive visibility into application health, infrastructure performance, and operational events using Amazon CloudWatch and Amazon SNS.
