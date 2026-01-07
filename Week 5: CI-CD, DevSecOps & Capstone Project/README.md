This is the final and most important week: **Week 5: CI/CD, DevSecOps & Capstone Project.** 

This week ties everything together. Students will learn how to automate the entire process so that a single code "Commit" automatically builds, tests, secures, and deploys the application to the Kubernetes cluster they built in Week 4.

---

### **Day 21: CI/CD with Jenkins (The Industry Standard)**
**Goal:** Master the "Engine" of DevOps and learn to write "Pipelines as Code."

*   **Theory (Morning):**
    *   **CI/CD Concepts:** Continuous Integration, Delivery, and Deployment.
    *   **Jenkins Architecture:** Master-Agent (Slave) setup to distribute workloads.
    *   **Jenkinsfile:** Declarative vs. Scripted pipelines (Groovy syntax).
*   **Key Concepts:**
    *   Jenkins Plugins (Git, Docker, AWS, Pipeline).
    *   Build Triggers (Webhooks vs. Polling).
    *   Environment Variables and Credentials Management.
*   **Hands-on Lab:**
    *   Install Jenkins on an AWS EC2 instance.
    *   **The First Pipeline:** Create a `Jenkinsfile` that pulls code from GitHub, runs a shell script "test," and builds a Docker image.
    *   Set up a **GitHub Webhook** so Jenkins builds automatically when you push code.
*   **Assignment:** Configure a Jenkins Agent (Slave node) and run a build job specifically on that agent.

---

### **Day 22: AWS Native CI/CD (The Cloud-Native Way)**
**Goal:** Learn the AWS "Code" suite for a fully managed, serverless DevOps experience.

*   **Theory (Morning):**
    *   **AWS CodeCommit:** Managed Git repositories.
    *   **AWS CodeBuild:** Serverless build service.
    *   **AWS CodeDeploy:** Automating deployments to EC2, Lambda, or ECS.
    *   **AWS CodePipeline:** The orchestrator that connects them all.
*   **Key Concepts:**
    *   `buildspec.yml`: Defining build commands for AWS.
    *   `appspec.yml`: Defining deployment hooks.
*   **Hands-on Lab:**
    *   **Project: AWS Pipeline.**
    *   Create a pipeline where:
        1. **Source:** Code is pulled from GitHub.
        2. **Build:** CodeBuild packages the app and pushes it to Amazon ECR.
        3. **Deploy:** CodeDeploy updates the application on an EC2 instance or EKS.
*   **Assignment:** Add a "Manual Approval" step in CodePipeline before it deploys to Production.

---

### **Day 23: DevSecOps (Shifting Left)**
**Goal:** Learn that security is not an afterthought—it must be integrated into the pipeline.

*   **Theory (Morning):**
    *   **The DevSecOps Mindset:** Shifting Security to the left (earlier in the SDLC).
    *   **SAST vs. DAST:** Static vs. Dynamic Application Security Testing.
    *   **SCA:** Software Composition Analysis (checking for vulnerable libraries).
*   **Key Concepts:**
    *   Code Quality: SonarQube.
    *   Vulnerability Scanning: Trivy or AWS Inspector.
*   **Hands-on Lab:**
    *   **Integration Lab:** Add a "Security Stage" to your Jenkins pipeline.
    *   Use **SonarQube** to analyze code for "Code Smells" and bugs.
    *   Use **Trivy** to scan your Docker images for vulnerabilities before pushing them to ECR.
*   **Assignment:** Fail the Jenkins build automatically if Trivy finds a "CRITICAL" vulnerability in the image.

---

### **Day 24: Monitoring & Observability**
**Goal:** Learn to monitor the health of your infrastructure and applications in real-time.

*   **Theory (Morning):**
    *   **Monitoring vs. Observability:** Metrics, Logs, and Traces (The 3 Pillars).
    *   **The Golden Signals:** Latency, Traffic, Errors, and Saturation.
    *   **Log Management:** Centralized logging with CloudWatch or ELK.
*   **Key Concepts:**
    *   Prometheus (Metric collection) & Grafana (Visualization).
    *   CloudWatch Dashboards and Alarms.
*   **Hands-on Lab:**
    *   Set up a **CloudWatch Alarm** to send an email (via SNS) if EC2 CPU usage exceeds 70%.
    *   **Prometheus Lab:** Install Prometheus and Grafana on your EKS cluster using Helm.
    *   Create a Grafana Dashboard to visualize Pod CPU and Memory usage.
*   **Assignment:** Create a custom CloudWatch Dashboard that displays both EC2 health and S3 bucket size.

---

### **Day 25: Capstone Project & Career Roadmap**
**Goal:** Integrate every single tool learned over 25 days into one "Showcase" project.

*   **The Capstone Project (The "Grand Finale"):**
    *   **Scenario:** Deploy a 3-tier Web Application (React + Node + MongoDB).
    *   **The Flow:**
        1.  **Infra:** Provision VPC, EKS, and RDS using **Terraform**.
        2.  **Config:** Configure the Bastion host using **Ansible**.
        3.  **CI/CD:** Use **Jenkins** to:
            *   Scan code with **SonarQube**.
            *   Build Docker image and scan with **Trivy**.
            *   Push to **Amazon ECR**.
            *   Deploy to **Amazon EKS** using **Helm**.
        4.  **Monitor:** Visualize the app’s health on **Grafana**.

*   **Career & Interview Prep (Afternoon):**
    *   **Resume Building:** How to list "Terraform," "Kubernetes," and "CI/CD" to pass ATS filters.
    *   **Certifications:** Path to AWS Certified Solutions Architect or SysOps Administrator.
    *   **Soft Skills:** How to explain a "Failed Deployment" and "Post-Mortems" in an interview.

---

### **Summary of Week 5 Skills Mastered:**
| Skill | Tool | Outcome |
| :--- | :--- | :--- |
| **Automation** | Jenkins / CodePipeline | Fully automated code-to-cloud flow |
| **Security** | SonarQube / Trivy | Finding bugs and vulnerabilities automatically |
| **Cloud Native CI** | AWS CodeBuild/Deploy | Serverless automation |
| **Observability** | Prometheus / Grafana | Real-time health dashboards |
| **System Design** | Capstone Project | Building a production-ready ecosystem |

---

### **Final Checklist for the University Students:**
By the end of Day 25, students should have:
1.  A **GitHub Profile** full of Terraform and Ansible code.
2.  A **LinkedIn Profile** highlighting their hands-on AWS experience.
3.  A **Live Project** link (or recording) showing their automated pipeline in action.