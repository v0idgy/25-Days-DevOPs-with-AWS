This is the complete content for **Day 07: Compute (EC2) & Block Storage (EBS)**.

Today, we move from the identity layer (IAM) to the actual "workhorses" of the cloud. Students will learn how to provision virtual servers and manage persistent data storage—the most fundamental skills for any DevOps Engineer.

---

# Part 1: Detailed Study Notes

### 1. Amazon EC2 (Elastic Compute Cloud)
EC2 provides resizable compute capacity in the cloud. Think of it as a virtual server that you can launch in seconds.
*   **AMI (Amazon Machine Image):** A template that contains the software configuration (OS, application server, and applications) required to launch your instance.
*   **Instance Types:** Optimized for different use cases.
    *   **T-Series (e.g., t3.micro):** General purpose, burstable performance (Free Tier).
    *   **C-Series (e.g., c5.large):** Compute optimized (Scientific modeling, high-perf web servers).
    *   **R-Series:** RAM/Memory optimized (High-performance databases).
    *   **M-Series:** Balanced/General purpose.

### 2. EC2 Storage: Ephemeral vs. Persistent
*   **Instance Store (Ephemeral):** Physical storage attached to the host computer. It is **temporary**. If the instance is stopped or terminated, data is lost. (Fast, good for cache).
*   **EBS (Elastic Block Store):** A network-attached virtual drive. It is **persistent**. If the instance is stopped, the data remains. You can detach an EBS volume from one instance and attach it to another.

### 3. EBS Volume Types
*   **gp3 / gp2 (General Purpose SSD):** Recommended for most workloads. gp3 is newer and allows independent scaling of IOPS and throughput.
*   **io1 / io2 (Provisioned IOPS SSD):** High-performance for mission-critical low-latency workloads (Large Databases).
*   **st1 (Throughput Optimized HDD):** For frequently accessed, throughput-intensive workloads (Big data, Data warehouses).

### 4. Security Groups & Key Pairs
*   **Security Groups:** A virtual firewall that controls inbound and outbound traffic. 
    *   **Crucial Concept:** They are **Stateful**. If you allow traffic in on Port 80, the response is automatically allowed to go out.
*   **Key Pairs:** AWS uses public-key cryptography to secure login information. You keep the private key (`.pem` file) and AWS stores the public key on the instance.

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Day 07: EC2 & EBS
*   **Sub-headline:** Virtual Servers and Persistent Storage
*   **Goal:** Launching, securing, and scaling compute and storage.

### Slide 2: What is an EC2?
*   **Virtual Machines in the Cloud.**
*   **Elastic:** Scale up or down instantly.
*   **Components of an EC2:**
    *   AMI (The OS)
    *   Instance Type (CPU/RAM)
    *   Storage (EBS/Instance Store)
    *   Networking (Security Groups)

### Slide 3: Choosing the Right Instance
*   **T-Family:** "Tiny" / General Purpose (Free Tier friendly).
*   **C-Family:** "Compute" / CPU heavy.
*   **R-Family:** "RAM" / Memory heavy.
*   **Analogy:** You don't buy a Ferrari (C5) to go to the grocery store, and you don't use a bicycle (T2) to win a race. Choose based on the workload.

### Slide 4: EBS vs. Instance Store
*   **Instance Store:** High performance, but data dies when the instance stops.
*   **EBS:** Like a USB hard drive. It lives independently of the instance.
*   **EBS Snapshots:** Point-in-time backups stored in S3. Incremental and easy to restore.

### Slide 5: Bootstrapping with User Data
*   **User Data:** A script that runs only **once** during the very first boot of the instance.
*   **DevOps Use Case:** Automatically installing Nginx, Docker, or Git so the server is "Ready to Work" the moment it launches.

### Slide 6: Security Groups (The Firewall)
*   **Rule 1:** All Inbound is **Denied** by default.
*   **Rule 2:** All Outbound is **Allowed** by default.
*   **Key concept:** Security Groups are **Stateful**.
*   **Essential Ports:**
    *   22 (SSH)
    *   80 (HTTP)
    *   443 (HTTPS)

---

# Part 3: Hands-on Lab Guide

### Task 1: Launch EC2 with Bootstrapping
1.  Go to EC2 Dashboard -> **Launch Instance**.
2.  **Name:** `Web-Server-01`.
3.  **AMI:** Amazon Linux 2023.
4.  **Instance Type:** `t2.micro`.
5.  **Key Pair:** Create a new one, download the `.pem` file.
6.  **Network:** Allow SSH (22) and HTTP (80) from "Anywhere".
7.  **Advanced Details -> User Data:** Paste this script:
    ```bash
    #!/bin/bash
    yum update -y
    yum install -y httpd
    systemctl start httpd
    systemctl enable httpd
    echo "<h1>Hello from DevOps Training Day 07</h1>" > /var/log/www/html/index.html
    ```
8.  **Launch.** Copy the Public IP and paste it in your browser to see the "Hello" message.

### Task 2: Adding Storage
1.  Go to **Volumes** -> **Create Volume**. 
2.  Size: `10 GiB`, Type: `gp3`. **Ensure it's in the same Availability Zone (AZ) as your EC2.**
3.  Select the volume -> **Actions** -> **Attach Volume**. Select your EC2.
4.  **In the Linux Terminal:**
    *   List disks: `lsblk` (You should see `nvme1n1` or `xvdb`).
    *   Format (only if new!): `sudo mkfs -t xfs /dev/nvme1n1`
    *   Create directory: `sudo mkdir /data`
    *   Mount: `sudo mount /dev/nvme1n1 /data`
    *   Verify: `df -h`

---

# Part 4: Assignment (Day 07)

**Objective:** Experience Data Persistence.

1.  **Create Data:** Inside your `/data` folder on the EC2, create a file: `echo "Important Backup" > /data/backup.txt`.
2.  **Snapshot:** Go to the AWS Console -> Volumes. Select the 10GB volume -> **Create Snapshot**.
3.  **Terminate:** Terminate the EC2 instance (this simulates a server failure).
4.  **Restore:**
    *   Go to **Snapshots**. Select your snapshot -> **Create Volume from Snapshot**.
    *   Launch a **New** EC2 instance.
    *   Attach the newly created volume to this new instance.
5.  **Verification:** Mount the volume on the new instance and verify that `backup.txt` is still there.

**Success Criteria:** Students must show the file content on the new server to the instructor.