This is the complete content for **Day 06: AWS Global Infrastructure & IAM**. 

Today, we transition from the local environment (Linux/Git) to the **AWS Cloud**. Students will learn that "The Cloud" is not just someone else's computer—it is a global network of massive data centers that can be controlled entirely through code and identity.

---

# Part 1: Detailed Study Notes

### 1. The Cloud Computing Service Models
Cloud computing is categorized by how much of the "stack" the provider manages vs. how much you manage:
*   **IaaS (Infrastructure as Service):** You rent the hardware (Servers, Storage, Networking). You are responsible for the OS, apps, and data. 
    *   *AWS Example:* Amazon EC2, Amazon VPC.
*   **PaaS (Platform as Service):** The provider manages the OS and runtime. You just bring your code.
    *   *AWS Example:* AWS Elastic Beanstalk, AWS Lambda.
*   **SaaS (Software as Service):** Fully managed software accessible via a browser.
    *   *AWS Example:* AWS Trusted Advisor, or non-AWS examples like Gmail/Salesforce.

### 2. AWS Global Infrastructure
AWS is organized into a hierarchy to ensure high availability and low latency:
*   **Regions:** Physical locations around the world (e.g., `us-east-1` in Virginia, `ap-south-1` in Mumbai). Each is independent.
*   **Availability Zones (AZs):** One or more discrete data centers within a Region. They have redundant power and networking. If one AZ fails, the others keep running.
*   **Edge Locations:** Small sites used by **Amazon CloudFront** to cache content (images/videos) closer to your users for faster speed.

### 3. The Shared Responsibility Model
"Security **of** the Cloud" vs. "Security **in** the Cloud."
*   **AWS is responsible for:** Physical security of data centers, hardware, global infrastructure, and the virtualization layer.
*   **YOU are responsible for:** Customer data, IAM (users/passwords), OS patching (on EC2), firewall rules (Security Groups), and encryption.

### 4. AWS IAM (Identity & Access Management)
IAM is the "Front Door" of AWS. It defines **Who** can do **What**.
*   **Root User:** The email you used to sign up. It has unrestricted access. **Never use it for daily tasks.**
*   **IAM Users:** Specific individuals or applications.
*   **IAM Groups:** Collections of users (e.g., "Developers"). Assigning permissions to a group is easier than managing users one by one.
*   **IAM Roles:** Temporary identities that a service (like an EC2) can "assume" to perform actions.
*   **IAM Policies:** JSON documents that define permissions.
    *   **Managed Policies:** Created by AWS or you; can be attached to multiple people.
    *   **Inline Policies:** Embedded directly into a single user/group. (Avoid these!).

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Day 06: AWS Global Infrastructure & IAM
*   **Sub-headline:** Building the Secure Foundation of the Cloud
*   **Goal:** Learn how AWS is built and how to control access like a Pro.

### Slide 2: The Cloud Stack (IaaS vs PaaS vs SaaS)
*   **Visual:** A pyramid diagram.
*   **IaaS:** You manage more. Flexible. (EC2).
*   **PaaS:** AWS manages more. Fast. (Beanstalk).
*   **SaaS:** AWS manages all. Easy. (Gmail).
*   **DevOps Rule:** Choose the model that reduces "Undifferentiated Heavy Lifting."

### Slide 3: Where is the Cloud? (AWS Infrastructure)
*   **Regions:** Cluster of AZs. Choose based on latency and legal laws.
*   **AZs:** Data centers separated by miles to avoid disaster. (Always use at least 2!).
*   **Edge Locations:** The "CDN" layer for speed.

### Slide 4: The Shared Responsibility Model
*   **Visual:** A "Who Manages What" chart.
*   **AWS:** "Security **OF** the cloud" (The hardware/building).
*   **Customer:** "Security **IN** the cloud" (The data/settings).
*   **Analogy:** AWS provides the secure apartment building; you are responsible for locking your own apartment door.

### Slide 5: IAM: The Principle of Least Privilege
*   **The Rule:** Give users ONLY what they need to do their job—nothing more.
*   **Root User:** Use it once to create an Admin, then "lock it in a safe."
*   **MFA:** Multi-Factor Authentication is **mandatory** for all users in a DevOps environment.

### Slide 6: JSON Policies - The Language of IAM
*   **Visual:** A JSON snippet.
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [{
          "Effect": "Allow",
          "Action": "s3:ListBucket",
          "Resource": "*"
      }]
    }
    ```
*   **Elements:** 
    *   **Effect:** Allow/Deny.
    *   **Action:** The specific command (e.g., `s3:CreateBucket`).
    *   **Resource:** What specific thing are they touching? (`*` means all).

---

# Part 3: Hands-on Lab Guide

### Task 1: Setup & Root Security
1.  Sign up at [aws.amazon.com/free](https://aws.amazon.com/free).
2.  Log in as **Root**.
3.  Go to the IAM Dashboard.
4.  Enable **MFA** for the Root user using Google Authenticator or Authy.

### Task 2: Create your "Daily Admin"
1.  In IAM, click **Users** $\rightarrow$ **Create User**.
2.  Name: `admin-devops`.
3.  Check "Provide user access to AWS Management Console."
4.  **Permissions:** Select "Attach policies directly" and search for `AdministratorAccess`.
5.  **Access Keys:** Once created, go to the user $\rightarrow$ "Security Credentials" $\rightarrow$ "Create Access Key" $\rightarrow$ select "Command Line Interface (CLI)". **Save the .csv file.**

### Task 3: AWS CLI Setup
1.  Download AWS CLI v2 for your OS.
2.  Run `aws configure` in your terminal.
3.  Enter your `Access Key ID` and `Secret Access Key` from the CSV.
4.  Region: `us-east-1` (or your preferred region).
5.  Format: `json`.
6.  Test it: `aws sts get-caller-identity`. (It should show your user ID).

---

# Part 4: Assignment (Day 06)

**Objective:** Test the "Least Privilege" principle.

1.  **Create a User:** `readonly-user` (Console access only).
2.  **Create a Group:** `ReadOnlyGroup`.
3.  **Attach Policy:** Attach the AWS Managed Policy `AmazonS3ReadOnlyAccess` to this group.
4.  **Add User:** Add `readonly-user` to the group.
5.  **Test:** 
    *   Log in as `readonly-user` in an Incognito window.
    *   Try to go to the S3 console and see if you can view buckets.
    *   **Try to create a bucket.** (It should fail with an "Access Denied" error).
6.  **CLI Test:** Configure a second profile in CLI: `aws configure --profile readonly`.
    *   Run: `aws s3 mb s3://my-test-bucket-12345 --profile readonly`.
    *   **Success Criteria:** The command fails with an Explicit Deny or lack of Allow.