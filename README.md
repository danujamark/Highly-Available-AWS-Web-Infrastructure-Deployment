# Highly-Available-AWS-Web-Infrastructure-Deployment
AWS web infrastructure project implementing Application Load Balancer (ALB), Auto Scaling Groups (ASG), EC2 instances, and highly available multi-AZ architecture for scalable web applications.

## Overview

This project demonstrates the deployment of a highly available and scalable web infrastructure on AWS using:

- Application Load Balancer (ALB)
- Auto Scaling Groups (ASG)
- EC2 Instances
- NGINX Web Server

The architecture is designed to distribute traffic efficiently, recover automatically from failures, and dynamically scale infrastructure based on workload demand.

---

## Architecture Components

- Amazon EC2
- Launch Templates
- Application Load Balancer (ALB)
- Auto Scaling Group (ASG)
- Target Groups
- Multi-AZ Deployment
- NGINX Web Server
- Security Groups

---

## Project Objectives

- Deploy scalable web infrastructure
- Implement high availability across multiple Availability Zones
- Distribute traffic using Application Load Balancer
- Automatically scale EC2 instances based on demand
- Improve fault tolerance and self-healing capability
- Demonstrate production-grade AWS web architecture

---

## Load Balancer Comparison

| Load Balancer | Layer | Best For |
|---|---|---|
| ALB | Layer 7 | HTTP/HTTPS applications |
| NLB | Layer 4 | High-performance TCP/UDP traffic |
| CLB | Layer 4 & 7 | Legacy workloads |

---

## Auto Scaling Types

| Scaling Type | Description |
|---|---|
| Manual Scaling | User manually changes instance count |
| Scheduled Scaling | Scaling based on predefined schedules |
| Dynamic Scaling | Scaling based on metrics like CPU usage |
| Predictive Scaling | AI-based scaling using demand forecasting |

---

## Infrastructure Design

```text
Internet Users
       ↓
Application Load Balancer
       ↓
Target Group
       ↓
Auto Scaling Group
       ↓
Multiple EC2 Instances (NGINX)
       ↓
Multi-AZ High Availability
```

---

## Tasks Completed

### Launch Template Configuration
- Created EC2 Launch Template
- Configured:
  - Amazon Linux 2023
  - Instance type
  - Security groups
  - User data automation script

### EC2 Automation
- Installed NGINX automatically during boot
- Configured custom web page
- Enabled NGINX service startup

### Target Group Setup
- Created Target Group
- Configured:
  - HTTP protocol
  - Port 80
  - Health checks

### Application Load Balancer Setup
- Created internet-facing ALB
- Attached Target Group
- Configured multi-AZ public subnets
- Enabled HTTP listener

### Auto Scaling Group Setup
- Created ASG using Launch Template
- Attached ALB Target Group
- Configured:
  - Minimum capacity
  - Desired capacity
  - Maximum capacity

---

## User Data Script

```bash
#!/bin/bash
dnf update -y
dnf install -y nginx
systemctl enable nginx
systemctl start nginx

cat <<EOF >/usr/share/nginx/html/index.html
<h1 style="color: green;text-align:center;margin-top:50px;">
Hello from Auto Scaled EC2 Instance 🚀
</h1>

<p style="text-align:center;">
Served by: $(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)
</p>
EOF
```

---

## Security Configuration

### Security Group Rules

#### ALB Security Group
- HTTP (80) → 0.0.0.0/0

#### EC2 Security Group
- HTTP (80) → ALB Security Group
- SSH (22) → My IP

---

## Expected Results

- EC2 instances automatically install NGINX
- ALB distributes traffic across multiple EC2 instances
- ASG automatically replaces unhealthy instances
- Infrastructure scales dynamically based on traffic
- High availability maintained across multiple Availability Zones

---

## Technologies Used

- AWS EC2
- AWS Auto Scaling Group
- AWS Application Load Balancer
- AWS Target Groups
- AWS Launch Templates
- Amazon Linux 2023
- NGINX

---

## Validation Performed

- Verified ALB accessibility
- Confirmed traffic distribution between EC2 instances
- Tested Target Group health checks
- Verified NGINX installation
- Tested Auto Scaling functionality
- Verified multi-AZ deployment

---

## Learning Outcome

This project demonstrates practical knowledge of:

- Highly available AWS architectures
- Auto Scaling implementation
- Load balancing concepts
- Multi-AZ deployments
- Infrastructure automation
- Web server deployment
- Fault tolerance and self-healing systems
- Production-grade cloud infrastructure design
