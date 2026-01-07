This is the detailed syllabus for **Week 3: Infrastructure as Code (IaC) & Configuration Management**. 

This week marks the transition from **"Manual Cloud"** to **"Automated Cloud."** Students will learn how to write code that builds entire data centers (Terraform) and code that configures software inside those servers (Ansible).

---

### **Day 11: Introduction to Terraform (IaC)**
**Goal:** Understand the "Infrastructure as Code" philosophy and provision your first AWS resource using HashiCorp Configuration Language (HCL).

*   **Theory (Morning):**
    *   **What is IaC?** Challenges of manual provisioning (Configuration Drift, Human Error).
    *   **Declarative vs. Imperative:** Why Terraform (Declarative) is preferred over Scripting (Imperative).
    *   **Terraform Architecture:** Core Engine, Providers (AWS, Azure, GCP), and State Files.
*   **Key Concepts:**
    *   The Lifecycle: `terraform init`, `plan`, `apply`, `destroy`.
    *   HCL Syntax: Blocks, Arguments, and Attributes.
*   **Hands-on Lab:**
    *   Install Terraform on your local machine.
    *   **First Resource:** Create a `provider.tf` and a `main.tf` to launch a single EC2 instance and an S3 bucket.
    *   Observe the `terraform.tfstate` file created locally.
*   **Assignment:** Change the EC2 instance type from `t2.micro` to `t3.micro` in your code and run `apply`. Observe how Terraform performs an "in-place update."

---

### **Day 12: Terraform Variables, Outputs, and State Management**
**Goal:** Make your infrastructure code reusable and secure.

*   **Theory (Morning):**
    *   **Variables:** Input variables, Local values, and Environment variables.
    *   **Outputs:** How to extract information (like Public IP) from the infrastructure.
    *   **The "State" Problem:** Why storing state locally is bad for teams.
    *   **Remote Backends:** Storing state in AWS S3 with State Locking via DynamoDB.
*   **Key Concepts:**
    *   `variables.tf`, `terraform.tfvars`.
    *   `outputs.tf`.
    *   Backend configuration blocks.
*   **Hands-on Lab:**
    *   Refactor Day 11 code to use variables for Region, AMI ID, and Instance Type.
    *   Configure an **S3 Bucket and DynamoDB table** to host your Terraform State remotely.
    *   Verify that manual changes in the AWS Console are detected by Terraform.
*   **Assignment:** Create a script that outputs the Public DNS of your web server automatically after provisioning.

---

### **Day 13: Terraform Modules & VPC Automation**
**Goal:** Build complex, modular infrastructure instead of one giant file.

*   **Theory (Morning):**
    *   **Modules:** The "Functions" of Terraform. Why modularity matters.
    *   **Standard Module Structure:** Root module vs. Child modules.
    *   **Terraform Registry:** Using pre-built modules from the community.
*   **Key Concepts:**
    *   Module Source, Versioning.
    *   Passing variables between modules.
*   **Hands-on Lab:**
    *   **Project:** Build a "Network Module." 
    *   Automate the creation of a **VPC, 2 Subnets (Public/Private), and an IGW** using a custom module.
    *   Call this module in your `main.tf` to provision the network before launching the EC2.
*   **Assignment:** Use a community module from the Terraform Registry to create an Auto Scaling Group (ASG).

---

### **Day 14: Configuration Management with Ansible**
**Goal:** Automate the "Inside" of the server (Software installation and OS hardening).

*   **Theory (Morning):**
    *   **Ansible Overview:** Agentless architecture (no software to install on target nodes).
    *   **How it works:** SSH, Python, and YAML.
    *   **Inventory:** Managing a list of managed nodes (IPs/DNS).
    *   **Idempotency:** Why Ansible is safer than shell scripts for configuration.
*   **Key Concepts:**
    *   Ad-hoc commands (`ansible -m ping`).
    *   Modules (apt, yum, service, copy, user).
    *   Ansible Configuration (`ansible.cfg`).
*   **Hands-on Lab:**
    *   Install Ansible on a "Control Node" (your Linux EC2).
    *   Set up Passwordless SSH between the Control Node and two "Worker Nodes."
    *   Run ad-hoc commands to check disk space and install `git` on all workers simultaneously.
*   **Assignment:** Write an ad-hoc command to create a user named `deployer` on all target servers and add them to the sudoers list.

---

### **Day 15: Ansible Playbooks & The "Golden Combo"**
**Goal:** Orchestrate complex deployments and integrate Terraform with Ansible.

*   **Theory (Morning):**
    *   **YAML Syntax:** The language of DevOps.
    *   **Playbooks:** Organizing tasks, handlers, and variables.
    *   **The Workflow:** Terraform provisions the "Hardware" $\rightarrow$ Ansible configures the "Software."
*   **Key Concepts:**
    *   Plays, Tasks, and Handlers (for service restarts).
    *   Ansible Variables and Jinja2 Templates.
*   **Hands-on Lab:**
    *   **Project: Automated Web Stack.**
    *   Write a Playbook to: Install Nginx, Copy a custom `index.html`, and Start the service.
    *   **Integration Lab:** Use Terraform to provision 3 EC2 instances and then trigger the Ansible Playbook to configure them as web servers immediately.
*   **Assignment:** Add a "Handler" to your playbook that restarts Nginx only if the configuration file is modified.

---

### **Summary of Week 3 Skills Mastered:**
| Skill | Tool | Key Capability |
| :--- | :--- | :--- |
| **Infra Provisioning** | Terraform | Create VPC, EC2, S3 via code |
| **Dry Logic** | Terraform Modules | Build reusable infrastructure components |
| **State Security** | S3 & DynamoDB | Remote state management and locking |
| **Config Management** | Ansible | Multi-node software installation |
| **Automation Flow** | TF + Ansible | End-to-end "Code to Infrastructure" |
| **Serialization** | YAML / HCL | Writing human-readable automation scripts |