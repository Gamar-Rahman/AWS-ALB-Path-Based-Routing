# AWS-ALB-Path-Based-Routing

### Introduction
This project demonstrates how to implement Path-Based Routing using AWS Application Load Balancer (ALB) to distribute traffic across multiple backend services.
It simulates a real-world scenario where different application paths (e.g., /app1, /app2) are routed to different EC2 instances.

### Key Concepts

Amazon EC2: Virtual servers used to host backend applications

Elastic Load Balancer (ELB): Distributes traffic across multiple targets

Application Load Balancer (ALB): Supports Layer 7 routing (HTTP/HTTPS)

Path-Based Routing: Routes requests based on URL path

### Project Objectives

Launch multiple EC2 instances

Deploy simple web apps on each instance

Create an Application Load Balancer

### Architecture

           Client Request
                 │
                 ▼
Application Load Balancer (ALB)
                 │
 ┌───────────────┬───────────────┐
 ▼                               ▼
 /app1 → EC2-1              /app2 → EC2-2


### Implementation Steps
1️⃣ Launch EC2 Instances (Bash Automation)
#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd

echo "Hello from $(hostname)" > /var/www/html/index.html

2️⃣ Create Target Groups

Target Group 1 → EC2-1

Target Group 2 → EC2-2

3️⃣ Create Application Load Balancer

Internet-facing ALB

Listener: HTTP (Port 80)

4️⃣ Configure Path-Based Routing

/app1 → Target Group 1

/app2 → Target Group 2

5️⃣ Test Configuration

http://ALB-DNS/app1 → EC2-1

http://ALB-DNS/app2 → EC2-2

### Security Considerations

Restrict security groups (only allow required ports)

Use HTTPS (TLS termination on ALB)

Enable AWS WAF for filtering malicious traffic

Use IAM roles instead of hardcoded credentials

Enable logging (ALB access logs + CloudWatch)

### Why This Matters

Enables microservices architecture

Improves scalability & fault tolerance

Reduces infrastructure complexity

Enhances traffic control & security visibility

### Real-World Use Case

/api → Backend API servers

/static → Static content servers

/admin → Restricted admin services
Configure path-based routing rules

Validate routing behavior via browser testing
