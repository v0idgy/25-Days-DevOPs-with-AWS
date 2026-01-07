This is the complete content for **Day 01: DevOps Culture & The Linux CLI**. 

It is divided into two parts: **Detailed Study Notes** (for student distribution) and **PPT Slide Content** (for your presentation).

---

# Part 1: Detailed Study Notes

### 1. The DevOps Philosophy
**The "Wall of Confusion":**
Traditionally, Software Development (Dev) and IT Operations (Ops) worked in "Silos."
*   **Developers** were incentivized to deliver new features quickly (Change).
*   **Operations** were incentivized to keep systems stable and "up" (Stability).
*   **The Conflict:** Devs would "throw the code over the wall" to Ops. If it crashed, Devs blamed the environment, and Ops blamed the code.

**DevOps** is the union of people, processes, and technology to enable continuous delivery of value to end-users. It breaks this wall by making everyone responsible for the entire lifecycle.

### 2. The CALMS Framework
Coined by Jez Humble, this framework measures DevOps adoption:
*   **C - Culture:** People over processes. Collaboration, shared responsibility, and "blameless" post-mortems.
*   **A - Automation:** Eliminate manual, repetitive tasks (Toil). If you do it twice, automate it.
*   **L - Lean:** Focus on small batches of work. Reduce waste and move fast.
*   **M - Measurement:** You can't improve what you don't measure. Track data (uptime, error rates, deployment frequency).
*   **S - Sharing:** Share tools, knowledge, and lessons learned across the organization.

### 3. Linux Architecture
Linux is the backbone of the cloud. To manage servers, you must understand how it's built:
*   **Hardware:** The physical machine (CPU, RAM, Disk).
*   **Kernel:** The heart of the OS. It talks to the hardware and manages resources.
*   **Shell:** The interface between the user and the Kernel. It interprets your commands (e.g., Bash, Zsh).
*   **User Space:** Where applications (like Nginx, Python, Docker) run.

**The Filesystem Hierarchy Standard (FHS):**
Linux doesn't have "C:" or "D:" drives. Everything starts from the **Root (/)**.
*   `/bin` & `/usr/bin`: Executable programs (commands).
*   `/etc`: System-wide **Configuration** files (Crucial for DevOps).
*   `/var/log`: Where the system and apps keep their **Logs**.
*   `/home`: Personal folders for users.
*   `/root`: The home directory for the Superuser (Admin).

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** DevOps Training - Day 01
*   **Sub-headline:** Culture, Philosophy, and the Linux Command Line
*   **Trainer Name:** [Your Name]
*   **Goal:** Moving from "Clicking" to "Scripting."

### Slide 2: The "Wall of Confusion"
*   **Visual Suggestion:** An image showing Devs and Ops separated by a wall.
*   **Points:**
    *   Devs: "It worked on my machine!"
    *   Ops: "Not our problem, the code is broken."
    *   Result: Slow releases and frequent outages.
    *   **The DevOps Solution:** Shared Ownership.

### Slide 3: The CALMS Framework
*   **Culture:** Trust and Transparency.
*   **Automation:** CI/CD and Infrastructure as Code.
*   **Lean:** Small changes, fast feedback.
*   **Measurement:** Monitor everything.
*   **Sharing:** Break down the silos.

### Slide 4: Why Linux for DevOps?
*   **Open Source:** Free and customizable.
*   **Performance:** Lightweight and stable.
*   **CLI First:** Everything can be automated via text.
*   **Cloud Native:** 90% of the public cloud (AWS/Azure) runs on Linux.

### Slide 5: Linux Architecture & FHS
*   **The Stack:** User -> Shell -> Kernel -> Hardware.
*   **The Root (/) Directory:**
    *   `/etc` = Settings.
    *   `/var/log` = History/Errors.
    *   `/tmp` = Temporary files.
    *   `/home` = User space.

### Slide 6: Essential Commands - Navigation
*   `pwd`: Print Working Directory (Where am I?).
*   `ls -alth`: List files (long format, show hidden, sort by time).
*   `cd <path>`: Change directory.
*   `tree`: Visual representation of folder structure.

### Slide 7: Essential Commands - File Management
*   `touch <file>`: Create an empty file.
*   `mkdir -p <path>`: Create nested directories (e.g., `p1/p2/p3`).
*   `cp -r`: Copy files/folders recursively.
*   `mv`: Move or rename files.
*   `rm -rf`: Force delete (Use with extreme caution!).

### Slide 8: Getting Help
*   Don't memorize, understand how to find info!
*   `man <command>`: The manual page.
*   `<command> --help`: Short summary of options.
*   `info <command>`: Detailed documentation.

### Slide 9: Hands-on Lab & Assignment
*   **Task 1:** Launch an Ubuntu instance on AWS or open WSL2.
*   **Task 2:** Explore `/etc` and find `hostname` file.
*   **Task 3:** Navigate to `/var/log`.
*   **Assignment:** 
    1. Create a folder named `backups` in your home directory.
    2. Find the file `/var/log/auth.log` (or `syslog`).
    3. Copy it to the `backups` folder and rename it to `today_security.log`.

---

# Part 3: Instructor Guide for the Lab

**Step 1: Environment Setup**
*   *If using AWS:* Show students how to log into the console, search for EC2, and launch a `t2.micro` instance with Ubuntu 22.04.
*   *If using WSL2:* Ensure they have "Windows Subsystem for Linux" enabled and Ubuntu installed from the Microsoft Store.

**Step 2: Demonstration**
1.  Type `cd /` to show the root.
2.  Type `ls -l` to show permissions.
3.  Explain that `sudo` is needed for certain directories (like `/var/log`).

**Step 3: Common Pitfalls to Mention**
*   Linux is **Case Sensitive** (`File.txt` is not `file.txt`).
*   Space matters in commands.
*   `rm -rf /` is the "Death Command"—never run it.̌