This 25-day roadmap is designed to take university students from absolute beginners to job-ready DevOps practitioners. It focuses on the **"Golden Triangle"** of DevOps: **Process, Tools, and Culture**, with a heavy emphasis on **AWS**.

---

### **Course Overview**
*   **Duration:** 25 Days (5 Weeks, 5 Days/Week)
*   **Target Audience:** Computer Science/IT Students
*   **Prerequisites:** Basic knowledge of any programming language (Python/Java) and basic networking.

---

### **Weekly Roadmap**

*   **Week 1: Foundations & Systems Thinking** (Linux, Git, Scripting)
*   **Week 2: The Cloud Operating System** (AWS Core Services)
*   **Week 3: Infrastructure as Code & Configuration** (Terraform & Ansible)
*   **Week 4: Containers & Orchestration** (Docker & Kubernetes)
*   **Week 5: CI/CD, DevSecOps & Capstone Project** (Jenkins, AWS Pipelines)

---

### **Detailed Table of Contents**

#### **Week 1: The DevOps Foundation**
*   **Day 01: Introduction to DevOps & SDLC**
    *   Evolution: Waterfall vs. Agile vs. DevOps.
    *   The CALMS framework (Culture, Automation, Lean, Measurement, Sharing).
    *   DevOps Lifecycle and Roles.
*   **Day 02: Linux for DevOps (The Command Line)**
    *   File System Hierarchy, Permissions (`chmod`, `chown`).
    *   Process Management, Package Managers (`yum`, `apt`).
    *   SSH Key Management and Remote Access.
*   **Day 03: Bash Scripting for Automation**
    *   Variables, Loops, Conditionals.
    *   Automating routine tasks (Backups, User creation).
    *   Crontab for scheduling.
*   **Day 04: Version Control with Git & GitHub**
    *   Git Workflow: Branching, Merging, Rebase, Stash.
    *   Collaborative Git: Pull Requests, Conflict Resolution.
    *   Git Hooks and Best Practices.
*   **Day 05: Networking & Security Fundamentals**
    *   OSI Model, TCP/IP, DNS, HTTP/S.
    *   Public vs. Private IPs, Firewalls, and Ports.

#### **Week 2: AWS Cloud Mastery**
*   **Day 06: Intro to AWS & IAM**
    *   Global Infrastructure (Regions & AZs).
    *   IAM: Users, Groups, Policies, Roles, and MFA.
    *   AWS CLI and SDK setup.
*   **Day 07: Compute (EC2) & Storage (S3/EBS)**
    *   EC2 Instances: Launching, Key-pairs, Security Groups.
    *   S3: Buckets, Versioning, Lifecycle Policies.
    *   EBS: Volumes, Snapshots.
*   **Day 08: Networking in AWS (VPC Deep Dive)**
    *   VPC, Subnets (Public/Private), Route Tables.
    *   Internet Gateway (IGW) and NAT Gateway.
    *   VPC Peering basics.
*   **Day 09: Databases & Load Balancing**
    *   RDS (SQL) vs. DynamoDB (NoSQL).
    *   Application Load Balancer (ALB) and Target Groups.
    *   Auto Scaling Groups (ASG) for high availability.
*   **Day 10: Serverless & Monitoring**
    *   AWS Lambda and API Gateway.
    *   CloudWatch: Logs, Metrics, and Alarms.
    *   AWS CloudTrail for auditing.

#### **Week 3: Infrastructure as Code (IaC) & Configuration**
*   **Day 11: Introduction to Terraform**
    *   What is IaC? Declarative vs. Imperative.
    *   Terraform Architecture: Providers, Resources, Variables.
*   **Day 12: Advanced Terraform**
    *   State Management (Local vs. Remote S3 backend).
    *   Terraform Modules for reusability.
    *   `terraform plan`, `apply`, `destroy`.
*   **Day 13: Configuration Management with Ansible**
    *   Agentless architecture.
    *   Inventory management, Ad-hoc commands.
*   **Day 14: Ansible Playbooks**
    *   YAML syntax, Tasks, Handlers, Templates (Jinja2).
    *   Variables and Facts.
*   **Day 15: Integrating Terraform & Ansible**
    *   Using Terraform to provision infra and Ansible to configure software (e.g., Nginx setup).

#### **Week 4: Containerization & Orchestration**
*   **Day 16: Docker Fundamentals**
    *   Virtualization vs. Containerization.
    *   Docker Images, Dockerfile, Layers.
    *   Managing Containers (Run, Stop, Inspect).
*   **Day 17: Docker Networking & Storage**
    *   Docker Compose for multi-container apps.
    *   Volumes and Bind Mounts.
    *   Pushing to Docker Hub / Amazon ECR.
*   **Day 18: Introduction to Kubernetes (K8s)**
    *   K8s Architecture (Control Plane & Worker Nodes).
    *   Pods, Deployments, and Services.
*   **Day 19: Amazon EKS (Elastic Kubernetes Service)**
    *   Setting up a managed K8s cluster on AWS.
    *   `kubectl` configuration.
*   **Day 20: K8s Advanced Concepts**
    *   ConfigMaps & Secrets.
    *   Ingress Controllers.
    *   Helm Charts (The K8s Package Manager).

#### **Week 5: CI/CD, Security & Capstone**
*   **Day 21: Jenkins for CI/CD**
    *   Installing Jenkins on EC2.
    *   Freestyle vs. Pipeline (Groovy syntax).
    *   CI/CD Plugins and Master-Slave architecture.
*   **Day 22: AWS Native CI/CD Tools**
    *   AWS CodeCommit, CodeBuild, CodeDeploy.
    *   AWS CodePipeline: Orchestrating the flow.
*   **Day 23: DevSecOps (Security in Pipeline)**
    *   SCA (Dependency scanning).
    *   SAST (SonarQube for Code Quality).
    *   Container Scanning (Trivy).
*   **Day 24: Monitoring & Observability**
    *   Introduction to Prometheus & Grafana.
    *   Log Management with ELK (Elasticsearch, Logstash, Kibana) or CloudWatch Logs.
*   **Day 25: Capstone Project & Career Prep**
    *   **The Project:** Deploy a MERN/Java app on AWS EKS using Terraform, Ansible, and Jenkins.
    *   Resume Building & Interview Tips for DevOps.
    *   AWS Certification Roadmap (Cloud Practitioner / SysOps).

---

### **Learning Methodology**
1.  **Theory (40%):** Morning conceptual sessions.
2.  **Hands-on Lab (60%):** Afternoon building and breaking things on AWS.
3.  **Assignments:** Daily small tasks (e.g., "Write a script to delete files older than 7 days").
4.  **Final Project:** A production-grade deployment script and pipeline.

### **Tools Student Will Master**
*   **Cloud:** AWS
*   **OS:** Linux (Ubuntu/Amazon Linux)
*   **IAC:** Terraform
*   **Config:** Ansible
*   **CI/CD:** Jenkins, AWS CodePipeline
*   **Containers:** Docker, Kubernetes (EKS)
*   **Monitoring:** CloudWatch, Prometheus/Grafana

