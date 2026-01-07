This is the complete content for **Day 08: Networking Deep Dive (VPC)**. 

Today is considered the "foundation of the house." Everything in AWS lives inside a VPC. Mastering networking is what separates a Cloud Engineer from a basic user.

---

# Part 1: Detailed Study Notes

### 1. What is a VPC (Virtual Private Cloud)?
A VPC is a private, isolated section of the AWS Cloud where you can launch resources in a virtual network that you define. It gives you complete control over your networking environment, including IP address ranges, subnets, and route tables.

### 2. CIDR and IP Addressing
*   **CIDR (Classless Inter-Domain Routing):** A method used to allocate IP addresses. 
    *   Example: `10.0.0.0/16`. 
    *   The `/16` means the first 16 bits are fixed (the network), and the rest are available for hosts.
    *   A `/16` provides 65,536 IPs; a `/24` provides 256 IPs.
*   **AWS Reservation:** AWS reserves 5 IP addresses in every subnet (e.g., .0 for network, .1 for VPC router, .2 for DNS, .3 for future use, and .255 for broadcast).

### 3. Subnets: Public vs. Private
*   **Public Subnet:** A subnet that has a route to an **Internet Gateway (IGW)**. Resources here (like Web Servers) can be accessed from the internet.
*   **Private Subnet:** Does not have a direct route to the internet. Used for sensitive resources like Databases. They can only access the internet "outbound" via a **NAT Gateway**.

### 4. Gateways and Routing
*   **Internet Gateway (IGW):** A horizontally scaled, redundant component that allows communication between your VPC and the internet.
*   **Route Table:** A set of rules (routes) used to determine where network traffic is directed.
*   **NAT Gateway (Network Address Translation):** Sits in a **Public Subnet**. It allows instances in a **Private Subnet** to connect to the internet (for updates) but prevents the internet from initiating a connection with those instances.

### 5. Network Security: Security Groups vs. NACLs
| Feature | Security Group (SG) | Network ACL (NACL) |
| :--- | :--- | :--- |
| **Layer** | Instance Level (Host) | Subnet Level |
| **State** | **Stateful** (Return traffic is auto-allowed) | **Stateless** (Must allow return traffic manually) |
| **Rules** | Support "Allow" rules only | Support "Allow" and "Deny" rules |
| **Evaluation** | All rules evaluated before decision | Rules evaluated in order (lowest number first) |

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Day 08: Networking Deep Dive (VPC)
*   **Sub-headline:** Building your Private Data Center in the Cloud
*   **Goal:** Create a secure, multi-tier network architecture from scratch.

### Slide 2: What is a VPC?
*   **Your own "Slice" of AWS.**
*   **Isolation:** No one can enter unless you open a door.
*   **Customizable:** You define the IP range, the subnets, and the rules.

### Slide 3: Subnetting Strategy
*   **Public Subnets:** The "DMZ" (Web Servers, Load Balancers).
*   **Private Subnets:** The "Vault" (Databases, Application Servers).
*   **High Availability:** Spread subnets across multiple Availability Zones.

### Slide 4: Routing: How traffic moves
*   **IGW (Internet Gateway):** The Front Door.
*   **NAT Gateway:** The One-way Exit (For Private subnets).
*   **Route Tables:** The Map. 
    *   Rule: `0.0.0.0/0` $\rightarrow$ `igw-id` (This makes a subnet public).

### Slide 5: Stateful vs. Stateless Security
*   **Security Groups (Stateful):** If you come in, you can go out. Simple and effective.
*   **NACLs (Stateless):** Like a strict security guard who checks your ID both when you enter AND when you leave. 
*   **Best Practice:** Use Security Groups for 99% of tasks; use NACLs for blocking specific IP ranges.

### Slide 6: Elastic IPs & Flow Logs
*   **Elastic IP (EIP):** A static, public IPv4 address. It stays with you even if you stop/start your instance.
*   **VPC Flow Logs:** The "CCTV Camera" of your network. It records all IP traffic going in and out of your VPC for auditing and security.

---

# Part 3: Hands-on Lab Guide

### Task 1: Create the VPC Shell
1.  Go to VPC Dashboard -> **Your VPCs** -> **Create VPC**.
2.  Name: `Custom-VPC`, CIDR: `10.0.0.0/16`. (Do NOT use the VPC Wizard).

### Task 2: Subnets & IGW
1.  **Subnets:** Create two subnets.
    *   `Public-Subnet`: `10.0.1.0/24` in AZ-1a.
    *   `Private-Subnet`: `10.0.2.0/24` in AZ-1a.
2.  **Internet Gateway:** Create `My-IGW` and **Attach** it to `Custom-VPC`.

### Task 3: Routing
1.  **Public Route Table:** Create one. Add a route: `0.0.0.0/0` targeting `My-IGW`. 
    *   **Associate** this table with the `Public-Subnet`.
2.  **NAT Gateway:** 
    *   Go to NAT Gateways -> Create.
    *   **Placement:** Must be in the `Public-Subnet`.
    *   Allocate an Elastic IP.
3.  **Private Route Table:** Create one. Add a route: `0.0.0.0/0` targeting the `NAT Gateway`.
    *   **Associate** this table with the `Private-Subnet`.

### Task 4: Testing
1.  Launch **EC2-A** in the Public Subnet (Enable "Auto-assign Public IP").
2.  Launch **EC2-B** in the Private Subnet (No Public IP).
3.  **The Test:** 
    *   SSH into EC2-A. 
    *   From EC2-A, SSH into EC2-B (using its private IP).
    *   Inside EC2-B, run `ping google.com`. (It should work via the NAT Gateway).

---

# Part 4: Assignment (Day 08)

**Objective:** Visualizing the Packet Flow.

**Deliverable:** Create a simple flow chart or document describing the journey of a request.
1.  **Scenario A:** An external user visiting your Web Server in the Public Subnet.
2.  **Scenario B:** Your Database in the Private Subnet downloading a security patch from the internet.

**Key points to include in the document:**
*   Which Gateway is used?
*   Which Route Table is consulted?
*   Which Security Layer (SG or NACL) is checked first? 
    *   *(Answer for students: NACL is checked first for Inbound, SG is checked second).*

**Success Criteria:** Students must correctly explain why the Database cannot be reached directly from the internet even if it has a Security Group allowing port 3306.