This is the detailed syllabus for **Week 2: AWS Cloud Mastery**. In this week, the focus shifts from a single machine (Linux) to the global infrastructure of the cloud. Students will learn how to design architectures that are scalable, secure, and highly available.

---


### **Day 06: AWS Global Infrastructure & IAM**
**Goal:** Understand how AWS is organized and how to secure it using the "Principle of Least Privilege."

*   **Theory (Morning):**
    *   **The Cloud Model:** IaaS vs. PaaS vs. SaaS.
    *   **Global Infrastructure:** Regions, Availability Zones (AZs), and Edge Locations.
    *   **Shared Responsibility Model:** What AWS manages vs. What You manage.
    *   **IAM (Identity & Access Management):** Users, Groups, Roles, and Policies (JSON structure).
*   **Key Concepts:**
    *   Root User vs. IAM User.
    *   Inline Policies vs. Managed Policies.
    *   Multi-Factor Authentication (MFA).
*   **Hands-on Lab:**
    *   Set up an AWS Free Tier account.
    *   Create an IAM User with `AdministratorAccess` and enable MFA.
    *   **AWS CLI Setup:** Install AWS CLI on the local machine and configure it using `aws configure`.
*   **Assignment:** Create a "ReadOnly" IAM group and assign a user to it. Verify they cannot create an S3 bucket via CLI.

---

### **Day 07: Compute (EC2) & Block Storage (EBS)**
**Goal:** Mastering the "Virtual Server" and its persistent storage.

*   **Theory (Morning):**
    *   **EC2 (Elastic Compute Cloud):** Instance types (T3-micro, C-series, etc.), AMIs (Amazon Machine Images).
    *   **Storage Types:** Instance Store (Ephemeral) vs. EBS (Persistent).
    *   **Security Groups:** Acting as a Virtual Firewall (Stateful).
    *   **Key Pairs:** Public-Key Cryptography for SSH access.
*   **Key Concepts:**
    *   EBS Volume Types (gp2, gp3, io1).
    *   Snapshots and Lifecycle Manager.
    *   User Data Scripts (Bootstrapping).
*   **Hands-on Lab:**
    *   Launch an Amazon Linux 2 EC2 instance.
    *   Use **User Data** to auto-install Apache (`httpd`) on launch.
    *   Attach an extra 10GB EBS volume, format it, and mount it to `/data`.
*   **Assignment:** Create a Snapshot of your EBS volume, terminate the instance, and then restore the data to a brand-new instance using that snapshot.

---

### **Day 08: Networking Deep Dive (VPC)**
**Goal:** Learn to build a custom, secure "Data Center" in the cloud.

*   **Theory (Morning):**
    *   **VPC (Virtual Private Cloud):** CIDR blocks and IP addressing.
    *   **Subnets:** Public (with Internet access) vs. Private (Internal only).
    *   **Routing:** Internet Gateways (IGW), Route Tables, and NAT Gateways.
    *   **Security:** Network ACLs (Stateless) vs. Security Groups (Stateful).
*   **Key Concepts:**
    *   Public vs. Private IP addresses.
    *   Elastic IPs.
    *   VPC Flow Logs for monitoring.
*   **Hands-on Lab:**
    *   **Custom VPC Build:** Create a VPC from scratch (not using the default wizard).
    *   Create 1 Public Subnet and 1 Private Subnet.
    *   Deploy an EC2 in the Public subnet (Web Server) and another in the Private subnet (Database Server).
    *   Use a **NAT Gateway** to allow the private instance to download updates from the internet.
*   **Assignment:** Document the flow of a packet from the Internet to your Private EC2 instance.

---

### **Day 09: Scaling & High Availability (ELB & ASG)**
**Goal:** Ensure applications can handle millions of users and survive hardware failures.

*   **Theory (Morning):**
    *   **Vertical vs. Horizontal Scaling.**
    *   **Elastic Load Balancing (ELB):** Application (Layer 7) vs. Network (Layer 4) Load Balancers.
    *   **Auto Scaling Groups (ASG):** Desired, Minimum, and Maximum capacity.
    *   **Health Checks:** How AWS knows when to replace an instance.
*   **Key Concepts:**
    *   Target Groups and Listeners.
    *   Scaling Policies (Target Tracking, Simple Scaling).
*   **Hands-on Lab:**
    *   Create an AMI from your configured Web Server.
    *   Create a **Launch Template** using that AMI.
    *   Set up an **Application Load Balancer (ALB)**.
    *   Create an **ASG** that spans across 2 Availability Zones.
*   **Assignment:** Perform a "Stress Test" on the CPU of your instance and watch the ASG automatically spin up a second instance to handle the load.

---

### **Day 10: Managed Databases (RDS) & S3 Storage**
**Goal:** Learn how to manage data without managing the underlying OS or hardware.

*   **Theory (Morning):**
    *   **RDS (Relational Database Service):** Multi-AZ deployment and Read Replicas.
    *   **S3 (Simple Storage Service):** Object storage, Buckets, and Keys.
    *   **S3 Storage Classes:** Standard, Intelligent Tiering, Glacier (Archive).
*   **Key Concepts:**
    *   Bucket Policies vs. ACLs.
    *   S3 Static Website Hosting.
    *   Database Security Groups (allowing access only from the Web Server SG).
*   **Hands-on Lab:**
    *   **S3:** Create a bucket, upload an `index.html`, and host it as a static website.
    *   **RDS:** Deploy a MySQL database in the Private Subnet of your VPC.
    *   **Integration:** Connect to the RDS instance from your EC2 instance using the MySQL CLI.
*   **Assignment:** Enable S3 Versioning and try to recover an "accidentally deleted" file.

---

### **Summary of Week 2 Skills Mastered:**
| Skill | AWS Service |
| :--- | :--- |
| **Security & Identity** | IAM (Users, Roles, Policies) |
| **Compute** | EC2, AMI, User Data |
| **Networking** | VPC, Subnets, IGW, NAT Gateway |
| **High Availability** | ALB, Auto Scaling Groups |
| **Storage & DB** | S3, EBS, RDS (MySQL) |
| **Cloud Automation** | AWS CLI |