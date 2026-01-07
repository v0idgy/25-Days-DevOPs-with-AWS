This is the detailed syllabus for **Week 4: Containers & Orchestration**.

This week focuses on the modern way of packaging and running applications. Students will move from managing Virtual Machines (EC2) to managing **Containers (Docker)** and orchestrating them at scale using **Kubernetes (EKS)**.

---

### **Day 16: Docker Fundamentals**
**Goal:** Understand why containers revolutionized software delivery and learn to "Dockerize" applications.

*   **Theory (Morning):**
    *   **The Container Revolution:** Virtual Machines vs. Containers (Guest OS vs. Shared Kernel).
    *   **Docker Architecture:** Docker Engine, Client, Daemon, and Registry.
    *   **The Dockerfile:** Understanding the blueprint of an image (Layers and Caching).
*   **Key Concepts:**
    *   Commands: `docker run`, `docker build`, `docker images`, `docker ps`, `docker rm`.
    *   Images vs. Containers: The Class vs. Instance analogy.
*   **Hands-on Lab:**
    *   Install Docker on an EC2 instance.
    *   **App Dockerization:** Take a simple Python Flask or Node.js "Hello World" app.
    *   Write a `Dockerfile`, build the image, and run it as a container.
    *   Learn to map ports: Access the app on your browser via `PublicIP:8080`.
*   **Assignment:** Create a Dockerfile that uses a "Multi-stage build" to reduce the final image size.

---

### **Day 17: Docker Compose & Amazon ECR**
**Goal:** Manage multi-container applications and store images in the AWS Cloud.

*   **Theory (Morning):**
    *   **Docker Networking:** Bridge, Host, and Overlay networks.
    *   **Docker Volumes:** Persistent storage for containers (keeping data after a container dies).
    *   **Docker Compose:** Defining multi-container environments in YAML.
    *   **Amazon ECR (Elastic Container Registry):** The AWS version of Docker Hub.
*   **Key Concepts:**
    *   `docker-compose up -d`, `docker-compose down`.
    *   `docker push` / `docker pull` logic.
*   **Hands-on Lab:**
    *   **Project: Two-Tier App.** Use Docker Compose to launch a Web App container and a Database container (PostgreSQL/MySQL) that communicate with each other.
    *   **ECR Lab:** Create a private repository in Amazon ECR.
    *   Authenticate Docker CLI with AWS ECR and push your local image to the cloud.
*   **Assignment:** Update your Docker Compose file to use Environment Variables (`.env` file) for database credentials.

---

### **Day 18: Introduction to Kubernetes (K8s)**
**Goal:** Learn the architecture of the world’s most popular container orchestrator.

*   **Theory (Morning):**
    *   **Why Kubernetes?** Auto-healing, Auto-scaling, and Bin-packing.
    *   **K8s Architecture:** 
        *   *Control Plane:* API Server, Etcd, Scheduler, Controller Manager.
        *   *Worker Nodes:* Kubelet, Kube-proxy, Container Runtime.
    *   **K8s Objects:** Pods (the smallest unit), Deployments, and Services.
*   **Key Concepts:**
    *   `kubectl` CLI: The tool to rule the cluster.
    *   YAML Manifests: Desired State vs. Actual State.
*   **Hands-on Lab:**
    *   Install `kubectl` and `minikube` (or `Kind`) for local practice.
    *   Write a `deployment.yaml` to run 3 replicas of your web app.
    *   Write a `service.yaml` (Type: NodePort) to expose the app.
*   **Assignment:** Manually "kill" a Pod using `kubectl delete pod` and watch Kubernetes automatically recreate it to maintain the "Desired State."

---

### **Day 19: Amazon EKS (Elastic Kubernetes Service)**
**Goal:** Deploy a production-grade managed Kubernetes cluster on AWS.

*   **Theory (Morning):**
    *   **Managed K8s:** Why use EKS instead of managing the Control Plane manually?
    *   **EKS Networking:** VPC CNI and Load Balancer integration.
    *   **Worker Node Options:** Managed Node Groups (EC2) vs. AWS Fargate (Serverless K8s).
*   **Key Concepts:**
    *   `eksctl`: The official CLI to provision EKS clusters.
    *   Kube-config: Linking your local terminal to the AWS Cloud cluster.
*   **Hands-on Lab:**
    *   Install `eksctl`.
    *   **Provision Cluster:** Run `eksctl create cluster` to build a 2-node EKS cluster (takes ~15 mins).
    *   Deploy your Docker image (stored in ECR on Day 17) onto the EKS cluster.
    *   Expose the app using a **LoadBalancer Service** and access it via an AWS ELB DNS.
*   **Assignment:** Scale your deployment from 2 replicas to 10 replicas using a single `kubectl` command.

---

### **Day 20: Advanced K8s - Config, Secrets & Helm**
**Goal:** Manage application configurations and use the K8s "Package Manager."

*   **Theory (Morning):**
    *   **ConfigMaps & Secrets:** Separating code from configuration and sensitive data.
    *   **Ingress Controllers:** Managing external access (URL-based routing) instead of multiple Load Balancers.
    *   **Helm:** Why we need "Charts" for Kubernetes.
*   **Key Concepts:**
    *   Environment variables in K8s.
    *   `helm install`, `helm upgrade`, `helm repo add`.
*   **Hands-on Lab:**
    *   **Secrets Lab:** Create a K8s Secret for your Database password and mount it into your app container.
    *   **Helm Lab:** Install an Nginx Ingress Controller or a Prometheus monitoring stack using a Helm Chart.
    *   Practice `helm rollback` to see how easy it is to revert a failed deployment.
*   **Assignment:** Create your own basic Helm Chart for the "System Health Script" app you built in Week 1.

---

### **Summary of Week 4 Skills Mastered:**
| Skill | Tool | Outcome |
| :--- | :--- | :--- |
| **Containerization** | Docker | Packaging apps into portable images |
| **Multi-Container** | Docker Compose | Running Web + DB stacks locally |
| **Image Management** | AWS ECR | Securely storing private images in AWS |
| **Orchestration** | Kubernetes | Deploying self-healing, scalable apps |
| **Managed K8s** | Amazon EKS | Professional cluster management |
| **K8s Packaging** | Helm | Deploying complex apps with one command |