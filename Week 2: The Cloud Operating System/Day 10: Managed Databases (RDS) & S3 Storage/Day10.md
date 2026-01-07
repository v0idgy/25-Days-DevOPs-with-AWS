This is the complete content for **Day 10: Managed Databases (RDS) & S3 Storage**.

Today, we move away from managing "Infrastructure" (Virtual Machines) to managing "Services." We will learn how to store petabytes of data on S3 and run enterprise-grade databases using RDS without ever logging into the underlying server.

---

# Part 1: Detailed Study Notes

### 1. Amazon S3 (Simple Storage Service)
S3 is an **Object Storage** service. Unlike EBS (Block Storage), you don't "format" it. You just upload files.
*   **Buckets:** Containers for data. Names must be **globally unique**.
*   **Objects:** The files. An object consists of:
    *   **Key:** The name of the file (e.g., `images/logo.png`).
    *   **Value:** The data itself.
    *   **Metadata:** Information about the file (size, content-type).
*   **Storage Classes:**
    *   **Standard:** Frequent access, high availability.
    *   **Intelligent-Tiering:** Automatically moves data between tiers to save costs.
    *   **Glacier Flexible/Deep Archive:** Very cheap, used for long-term backups. Retrieval takes minutes to hours.

### 2. S3 Security & Hosting
*   **Bucket Policies:** JSON-based rules applied to the bucket to allow/deny access to specific users or IPs.
*   **ACLs (Access Control Lists):** Legacy way to manage access (Bucket policies are preferred now).
*   **Static Website Hosting:** S3 can host HTML, CSS, and JS files as a website. It cannot run server-side code (like PHP or Python).

### 3. Amazon RDS (Relational Database Service)
Managed service for SQL databases (MySQL, PostgreSQL, Oracle, SQL Server).
*   **Why RDS?** AWS handles OS patching, automated backups, and hardware maintenance.
*   **Multi-AZ Deployment:** AWS keeps a "Synchronous" standby copy in another Availability Zone. If the primary fails, it automatically fails over. (Used for **High Availability**).
*   **Read Replicas:** "Asynchronous" copies used to handle heavy read traffic. (Used for **Scalability**).

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Day 10: Managed Data Services (S3 & RDS)
*   **Sub-headline:** Scaling Data without the Hardware Headache
*   **Goal:** Learn to host static content and manage relational databases at scale.

### Slide 2: S3 - The Internet's Storage
*   **Object Storage:** Not a drive, but a "Key-Value" store.
*   **Durability:** 99.999999999% (11 nines). Your data is replicated across 3 AZs automatically.
*   **Unlimited Scale:** Store 1 byte or 5 petabytes.

### Slide 3: S3 Storage Classes (Cost Optimization)
*   **Standard:** Active data.
*   **S3-IA:** Infrequent access (Backups you might need quickly).
*   **Glacier:** The "Vault." For data you keep for years but rarely touch.
*   **DevOps Tip:** Use **Lifecycle Policies** to move files to Glacier automatically after 90 days.

### Slide 4: Static Website Hosting
*   **Concept:** Turn an S3 bucket into a website URL.
*   **Benefits:** No server to manage, zero maintenance, scales to millions of users instantly.
*   **Limitation:** Client-side only (HTML/CSS/JS). No backend logic.

### Slide 5: Amazon RDS (Managed SQL)
*   **Managed Services:** No more `yum install mysql`.
*   **Automated Backups:** Point-in-time recovery (restore your DB to any second in the last 35 days).
*   **Patching:** AWS handles security updates during a "Maintenance Window."

### Slide 6: High Availability vs. Scalability
*   **Multi-AZ (Disaster Recovery):** One active, one standby. If AZ1 goes down, AZ2 takes over.
*   **Read Replicas (Performance):** One master (Write) and multiple replicas (Read). Great for reporting apps.

### Slide 7: Security - The "Chained" SG Rule
*   **Visual:** Show Web-SG and DB-SG.
*   **The Rule:** Do NOT allow "Anywhere (0.0.0.0/0)" for your database.
*   **Best Practice:** Configure the Database Security Group to allow traffic ONLY from the **Security Group ID** of the Web Servers.

---

# Part 3: Hands-on Lab Guide

### Task 1: S3 Static Website
1.  **Create Bucket:** Name it `devops-lab-[your-name]`.
2.  **Upload:** Create an `index.html` file locally and upload it.
3.  **Permissions:** 
    *   Disable "Block all public access" (for learning purposes).
    *   Add a **Bucket Policy** to allow public `s3:GetObject`.
4.  **Enable Hosting:** Properties -> Static Website Hosting -> Enable.
5.  **Test:** Open the provided Endpoint URL in your browser.

### Task 2: RDS Deployment
1.  Go to RDS -> **Create Database**.
2.  **Engine:** MySQL (Free Tier template).
3.  **Settings:** DB Instance ID: `devops-db`, Master username: `admin`, Password: `password123`.
4.  **Connectivity:** 
    *   Select your **Custom VPC** from Day 8.
    *   Public Access: **No**. (Must stay in the private subnet).
    *   Create a new Security Group: `rds-sg`.

### Task 3: Integration (EC2 to RDS)
1.  **Update Security Group:** Edit `rds-sg` inbound rules. Allow Port 3306, Source: Select the `web-server-sg`.
2.  **Connect:** SSH into your EC2 Web Server.
3.  **Install Client:** `sudo yum install mariadb105 -y` (or `mysql`).
4.  **Login:** `mysql -h [RDS-Endpoint] -u admin -p`.
5.  **Verify:** If you see the `mysql>` prompt, you have successfully bridged the Web and Data tiers!

---

# Part 4: Assignment (Day 10)

**Objective:** Disaster Recovery on S3.

1.  **Enable Versioning:** Go to your S3 bucket -> Properties -> **Bucket Versioning** -> **Enable**.
2.  **Upload & Overwrite:** Upload `test.txt` with the text "Version 1". Then upload a new `test.txt` with the text "Version 2".
3.  **Delete:** Delete the file `test.txt`.
4.  **Recover:** 
    *   Toggle the "Show versions" switch in the S3 console.
    *   Notice the "Delete Marker." 
    *   Delete the **Delete Marker** to restore the file.
    *   Download the old version ("Version 1") using the version ID.

**Success Criteria:** Students must explain the difference between a normal delete and a delete with versioning enabled.

---
### **End of Week 2 Summary for Students**
*   **Day 6:** You learned who can touch your cloud (IAM).
*   **Day 7-9:** You built the compute and network (VPC, EC2, ASG).
*   **Day 10:** You secured the data (S3, RDS).
*   **Next Week:** We stop clicking buttons and start writing code to build this entire setup (**Terraform & Ansible**)!