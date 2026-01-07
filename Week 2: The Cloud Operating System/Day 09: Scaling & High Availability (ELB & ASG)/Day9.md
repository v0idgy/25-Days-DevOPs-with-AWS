This is the complete content for **Day 09: Scaling & High Availability (ELB & ASG)**. 

Today is where the "Cloud" truly starts to feel different from traditional servers. We move from managing a single server to managing a **fleet** that grows and shrinks automatically based on user demand.

---

# Part 1: Detailed Study Notes

### 1. Vertical vs. Horizontal Scaling
How do we handle more traffic?
*   **Vertical Scaling (Scale Up):** Increasing the size of the instance (e.g., changing a `t2.micro` to a `t2.large`). 
    *   *Pros:* Easy to do. 
    *   *Cons:* Has an upper limit; requires a reboot (downtime); not resilient (if the big server fails, everything goes down).
*   **Horizontal Scaling (Scale Out):** Adding more instances of the same size.
    *   *Pros:* No downtime; theoretically infinite scaling; highly resilient.
    *   *Cons:* Requires a Load Balancer to distribute traffic.

### 2. Elastic Load Balancing (ELB)
The Load Balancer is the "Traffic Cop." It sits in front of your servers and distributes incoming requests.
*   **ALB (Application Load Balancer):** Operates at **Layer 7 (HTTP/HTTPS)**. It is "intelligent"—it can route traffic based on the URL path (e.g., `example.com/api` goes to one set of servers, while `example.com/images` goes to another).
*   **NLB (Network Load Balancer):** Operates at **Layer 4 (TCP/UDP)**. It is ultra-fast and handles millions of requests per second. Used for gaming, VoIP, or non-HTTP traffic.

### 3. Target Groups and Listeners
*   **Listener:** A process that checks for connection requests (e.g., listens on Port 80).
*   **Target Group:** A group of resources (EC2 instances) where the Load Balancer sends the traffic.

### 4. Auto Scaling Groups (ASG)
ASG ensures that you have the right number of EC2 instances available to handle the load.
*   **Desired Capacity:** How many instances you want running *now*.
*   **Minimum Size:** The "Floor"—never go below this (for High Availability).
*   **Maximum Size:** The "Ceiling"—never go above this (to control costs).
*   **Health Checks:** If an instance becomes "Unhealthy" (crashes), the ASG terminates it and launches a brand-new one automatically.

### 5. Scaling Policies
*   **Target Tracking:** "Keep my average CPU at 50%." AWS handles the rest.
*   **Simple/Step Scaling:** "If CPU > 80% for 2 minutes, add 2 instances."

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Day 09: Scaling & High Availability
*   **Sub-headline:** Building Systems that Never Sleep
*   **Goal:** Learn to automate growth and ensure 100% uptime.

### Slide 2: Scaling: Up vs. Out
*   **Scale Up (Vertical):** Buy a bigger engine for the same car.
*   **Scale Out (Horizontal):** Buy more cars.
*   **DevOps Preference:** We prefer **Horizontal** because it allows for "Fault Tolerance." If one car breaks, the others still drive.

### Slide 3: Elastic Load Balancer (ALB)
*   **The Traffic Cop:** Distributes traffic to multiple EC2s.
*   **Layer 7 Awareness:** Can route based on Hostnames or URL Paths.
*   **Health Checks:** Stops sending traffic to instances that are failing.

### Slide 4: Auto Scaling Group (ASG) Logic
*   **Launch Template:** The "Blueprint" (Which AMI? Which SG? Which Type?).
*   **Fleet Management:**
    *   **Min:** 2 (Always stay alive).
    *   **Max:** 10 (Don't go broke).
    *   **Desired:** 2 (Current state).
*   **Self-Healing:** Crashed servers are replaced automatically.

### Slide 5: Scaling Policies (The Brain)
*   **Target Tracking:** The most common. Like a thermostat (set it to 50% CPU).
*   **Scheduled Scaling:** "Every Friday at 6 PM, increase instances to 5" (for weekend sales).

### Slide 6: High Availability (Multi-AZ)
*   **Visual:** Show an ALB sending traffic to Subnet A and Subnet B in different AZs.
*   **The Benefit:** If an entire Data Center (AZ) goes offline due to a power cut, your application stays online in the other AZ.

---

# Part 3: Hands-on Lab Guide

### Task 1: Create an AMI (Amazon Machine Image)
1.  Go to your running Web Server (from Day 7).
2.  **Actions** -> **Image and templates** -> **Create Image**.
3.  Name it `My-Web-App-Image`. This takes a snapshot of the OS + Apache + your code.

### Task 2: Create a Launch Template
1.  EC2 Dashboard -> **Launch Templates** -> **Create**.
2.  Select your newly created `My-Web-App-Image`.
3.  Instance type: `t2.micro`. Key pair: Your existing key. 
4.  Security Group: Select the one that allows Port 80.

### Task 3: Create ALB & ASG
1.  **Create Load Balancer:** Select **ALB**. Create a Target Group (target type: Instance).
2.  **Create Auto Scaling Group:**
    *   Attach the **Launch Template**.
    *   Select **2 subnets** in different AZs.
    *   Attach to the **Existing Load Balancer**.
    *   Set **Min: 1, Desired: 2, Max: 4**.

---

# Part 4: Assignment (Day 09)

**Objective:** Trigger an "Auto Scale" event using a CPU Stress Test.

**Step-by-Step for Students:**
1.  SSH into one of the instances created by the ASG.
2.  Install the `stress` utility:
    *   `sudo amazon-linux-extras install stress` (Amazon Linux 2) OR `sudo dnf install stress` (AL2023).
3.  Set a **Target Tracking Policy** in your ASG for **CPU Usage at 40%**.
4.  Run the stress command: `stress --cpu 4 --timeout 300` (This maxes out the CPU for 5 minutes).
5.  **Watch the Console:**
    *   Check CloudWatch Alarms.
    *   Watch the "Activity" tab in ASG.
    *   Observe a 3rd instance being launched automatically once the alarm triggers.

**Success Criteria:** Students must show the ASG "Activity History" showing "At 12:05... an instance was started in response to a difference between desired and actual capacity."