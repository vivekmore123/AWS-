# AWS Scalable Web Architecture Using ALB, Auto Scaling & EC2

## 📌 Project Overview

This project demonstrates a highly available and scalable web application architecture on AWS using an Application Load Balancer (ALB), path-based routing, Target Groups, Auto Scaling Groups (ASGs), Launch Templates, and Amazon EC2 instances distributed across multiple Availability Zones.

The Application Load Balancer routes incoming HTTP traffic to different target groups based on URL paths. Each target group is associated with a dedicated Auto Scaling Group that manages EC2 instances for a specific application or service.

---

## 🏗️ Architecture Diagram

<img width="1264" height="843" alt="project 1" src="https://github.com/user-attachments/assets/05cea90e-d6c5-416d-baed-31a9ffa03abd" />


---

## 🎯 Project Objectives

* Implement path-based routing using an AWS Application Load Balancer.
* Deploy multiple application services using separate Target Groups.
* Configure Auto Scaling Groups to manage EC2 instances automatically.
* Distribute EC2 instances across multiple Availability Zones.
* Improve application availability, scalability, and fault tolerance.
* Use Launch Templates to standardize EC2 instance configuration.

---

## 🛠️ AWS Services Used

| AWS Service | Purpose |
| :--- | :--- |
| **Amazon VPC** | Provides an isolated network environment |
| **Application Load Balancer (ALB)** | Distributes incoming HTTP traffic |
| **ALB Listener Rules** | Routes requests based on URL paths |
| **Target Groups** | Forward traffic to the appropriate EC2 instances |
| **Amazon EC2** | Hosts application services |
| **Auto Scaling Groups** | Automatically adjust the number of EC2 instances |
| **Launch Templates** | Define EC2 instance configuration |
| **Availability Zones** | Improve availability and fault tolerance |
| **Security Groups** | Control inbound and outbound traffic |

---

## 🔀 Path-Based Routing

The ALB listens for incoming HTTP requests on port 80 and forwards them to the appropriate target group according to the requested URL path.

| URL Path | Target Group | Application |
| :--- | :--- | :--- |
| `/home/*` | `tg-home` | Home |
| `/laptop/*` | `tg-laptop` | Laptop |
| `/fashion/*` | `tg-fashion` | Fashion |
| `/furniture/*` | `tg-furniture` | Furniture |

### Request Flow

1. A client sends an HTTP request to the Application Load Balancer.
2. The ALB evaluates the listener rules.
3. The matching URL path determines the destination Target Group.
4. The Target Group forwards the request to a healthy EC2 instance.
5. The corresponding Auto Scaling Group maintains the desired number of instances across Availability Zones.

---

## 🧩 Architecture Components

### 1. Application Load Balancer
* Receives client requests on HTTP port 80.
* Uses path-based listener rules to route traffic.
* Distributes requests among healthy targets.

### 2. Target Groups
Four separate Target Groups are configured:
* `tg-home`
* `tg-laptop`
* `tg-fashion`
* `tg-furniture`

Each Target Group forwards requests to the EC2 instances serving its respective application.

### 3. Auto Scaling Groups
Each application has a dedicated Auto Scaling Group:
* `asg-home`
* `asg-laptop`
* `asg-fashion`
* `asg-furniture`

The Auto Scaling Groups maintain the desired instance capacity and can launch or terminate instances according to configured scaling policies and health checks.

### 4. Launch Templates
Each Auto Scaling Group uses a corresponding Launch Template to define settings such as:
* Amazon Machine Image (AMI)
* EC2 instance type
* Key pair, if required
* Security Groups
* Storage configuration
* User data scripts for application installation and startup

### 5. Multiple Availability Zones
EC2 instances are distributed across two Availability Zones to improve availability and reduce dependence on a single zone.

---

## ⚙️ Implementation Steps

1. Create a VPC with appropriate public and private subnets across multiple Availability Zones.
2. Configure Internet Gateway, route tables, and networking as required.
3. Create Security Groups for the ALB and EC2 instances.
4. Create Launch Templates for the four application services.
5. Create the four Target Groups and configure health check paths.
6. Create Auto Scaling Groups and associate each with its corresponding Target Group.
7. Configure the Application Load Balancer and its listener on port 80.
8. Add path-based listener rules for `/home/*`, `/laptop/*`, `/fashion/*`, and `/furniture/*`.
9. Deploy the application code or configure user data scripts to install and start the web services.
10. Verify target health, test each URL path, and configure scaling policies if required.

---

## 🧪 Testing

After deployment, test the following URL paths using the ALB DNS name:

* `http://<ALB-DNS-NAME>/home/`
* `http://<ALB-DNS-NAME>/laptop/`
* `http://<ALB-DNS-NAME>/fashion/`
* `http://<ALB-DNS-NAME>/furniture/`

### Verify that:
* Each URL path reaches the correct application.
* Target Groups report healthy targets.
* Requests continue to work when multiple instances are available.
* Auto Scaling responds according to the configured scaling policies.
* The architecture remains available during an individual instance failure, provided healthy capacity remains.

---

## 🔐 Security Considerations

* Allow HTTP traffic on port 80 to the ALB only as required.
* Allow application traffic to EC2 instances only from the ALB Security Group.
* Prefer private subnets for backend EC2 instances.
* Use IAM roles instead of hardcoded AWS credentials.
* Use HTTPS with an appropriate TLS certificate for production deployments.
* Configure health checks and monitoring through Amazon CloudWatch.

---

## 📈 Key Benefits

* **Scalability:** Auto Scaling Groups can adjust instance capacity based on demand.
* **High Availability:** Instances can run across multiple Availability Zones.
* **Efficient Routing:** ALB listener rules direct requests to the appropriate application.
* **Fault Tolerance:** Unhealthy instances can be replaced, subject to ASG configuration.
* **Modularity:** Each application service has its own Target Group and Auto Scaling Group.
* **Maintainability:** Launch Templates standardize instance configuration.

---

## 🚀 Future Enhancements

* Configure HTTPS using AWS Certificate Manager.
* Add CloudWatch alarms and monitoring dashboards.
* Implement target tracking scaling policies.
* Use AWS Systems Manager for instance management.
* Automate infrastructure deployment using Terraform or AWS CloudFormation.
* Configure a custom domain using Amazon Route 53.
* Implement CI/CD using AWS CodePipeline or GitHub Actions.

---

## 📚 Learning Outcomes

Through this project, I explored AWS networking, load balancing, path-based routing, EC2 provisioning, Auto Scaling, health checks, and multi-AZ application architecture.

---

## 👨‍💻 Author

**Vivek**
* GitHub: [vivekmore@36](https://github.com/vivekmore@36)
* Project: AWS Scalable Web Architecture
