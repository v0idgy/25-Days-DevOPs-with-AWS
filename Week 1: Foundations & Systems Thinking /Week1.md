This is the detailed syllabus for **Week 1: The DevOps Foundation**. This week is critical as it builds the "under-the-hood" knowledge required to manage servers, automate tasks, and collaborate on code effectively.

---

### **Day 01: DevOps Culture & The Linux CLI**
**Goal:** Understand the *Why* of DevOps and get comfortable navigating the terminal.

*   **Theory (Morning):**
    *   **DevOps Philosophy:** Breaking the "Wall of Confusion" between Dev and Ops.
    *   **The CALMS Framework:** Culture, Automation, Lean, Measurement, and Sharing.
    *   **Linux Architecture:** The Kernel, Shell, and File System Hierarchy (FHS).
*   **Key Concepts:**
    *   Navigation: `pwd`, `ls -alth`, `cd`, `tree`.
    *   File Manipulation: `touch`, `mkdir -p`, `cp -r`, `mv`, `rm -rf`.
    *   Getting Help: `man`, `info`, `--help`.
*   **Hands-on Lab:**
    *   Set up a Linux environment (using WSL2 on Windows or an Ubuntu EC2 instance).
    *   Explore the `/etc`, `/var/log`, and `/home` directories to understand where system configs and logs reside.
*   **Assignment:** Navigate to `/var/log`, find the `auth.log` (or `secure`), and copy it to your home directory under a folder named `backups`.

---

### **Day 02: Advanced Linux Admin & User Management**
**Goal:** Master permissions and process management—essential for secure application hosting.

*   **Theory (Morning):**
    *   **Permissions:** Read (4), Write (2), Execute (1). Understanding `u g o` (User, Group, Others).
    *   **Package Managers:** How `apt` (Debian/Ubuntu) and `yum/dnf` (RedHat/Amazon Linux) work.
    *   **Process Management:** Foreground vs. Background processes.
*   **Key Concepts:**
    *   Permissions: `chmod 755`, `chown`, `chgrp`, `sudo`.
    *   Processes: `ps aux`, `top`, `htop`, `kill -9`, `&`, `fg`, `bg`.
    *   Editors: Mastering `vim` or `nano` (The "Vim Survival Guide").
*   **Hands-on Lab:**
    *   Create a new user `dev-user`, add them to the `sudo` group.
    *   Create a folder where only the `dev-user` has write access, but everyone can read.
    *   Install a web server (Nginx) and use `systemctl` to start/stop/enable it.
*   **Assignment:** Install `htop`. Identify the process consuming the most memory and "kill" it safely.

---

### **Day 03: Text Processing & Redirection**
**Goal:** Learn how to extract insights from massive log files using "The Three Musketeers" (Grep, Sed, Awk).

*   **Theory (Morning):**
    *   **I/O Redirection:** Standard Input (0), Output (1), and Error (2).
    *   **Piping:** Passing the output of one command as input to another.
    *   **RegEx Basics:** Searching for patterns in text.
*   **Key Concepts:**
    *   Redirection: `>`, `>>`, `2>`, `&>`.
    *   Processing: `grep`, `awk`, `sed`, `sort`, `uniq -c`, `wc -l`.
    *   Viewing: `cat`, `less`, `head`, `tail -f` (real-time log watching).
*   **Hands-on Lab:**
    *   **The Log Challenge:** Take an Nginx access log and:
        1. Filter only 404 errors using `grep`.
        2. Count unique IP addresses visiting the site using `awk` and `uniq`.
        3. Replace a specific string in a config file using `sed`.
*   **Assignment:** Write a "One-Liner" command to find all files in `/etc` that were modified in the last 24 hours.

---

### **Day 04: Bash Scripting for Automation**
**Goal:** Move from running manual commands to creating reusable automation logic.

*   **Theory (Morning):**
    *   **Shebang:** `#!/bin/bash` and why it's needed.
    *   **Variables & Arguments:** `$1`, `$2`, `$@`.
    *   **Logic:** If-else statements, For/While loops.
    *   **Scheduling:** How `cron` and `crontab` work.
*   **Key Concepts:**
    *   Scripting: `read`, `export`, `function`.
    *   Conditionals: `[[ -f file ]]`, `[[ -d dir ]]`.
    *   Automation: `crontab -e`.
*   **Hands-on Lab:**
    *   **Project: System Health Script.** Build a script that:
        1. Checks disk usage.
        2. Checks RAM usage.
        3. If RAM is > 80%, logs a warning to `/var/log/sys_health.log`.
        4. Schedule this script to run every 5 minutes using Cron.
*   **Assignment:** Update the script to send an "Alert Email" (simulated by a `wall` message) when the disk is nearly full.

---

### **Day 05: Version Control with Git (The DevOps Heart)**
**Goal:** Learn to treat "Infrastructure as Code" by mastering Git workflows.

*   **Theory (Morning):**
    *   **Distributed VCS:** Why Git is better than SVN.
    *   **The Three Stages:** Working Directory, Staging Area (Index), Local Repository.
    *   **Branching Strategy:** Feature branching vs. GitFlow.
*   **Key Concepts:**
    *   Basic Ops: `git init`, `git add .`, `git commit -m`, `git status`.
    *   Collaboration: `git clone`, `git push`, `git pull`, `git remote`.
    *   Intermediate: `git branch`, `git checkout -b`, `git merge`, `git log --oneline`.
*   **Hands-on Lab:**
    *   Create a GitHub account.
    *   Initialize a local repo for your "System Health Script" from Day 04.
    *   Create a feature branch `add-logging`, modify the code, and merge it back to `main`.
    *   Push your code to a public GitHub repository.
*   **Assignment:** Simulate a merge conflict by editing the same line in two different branches and then attempt to merge them. Resolve the conflict manually.

---

### **Summary of Week 1 Skills Mastered:**
| Skill | Tool/Command |
| :--- | :--- |
| **System Admin** | `sudo`, `systemctl`, `chmod`, `htop` |
| **Automation** | Bash Scripts, Cron jobs |
| **Data Analysis** | `grep`, `awk`, `tail -f` |
| **Collaboration** | `git commit`, `git push`, `PRs` |
| **Networking** | `ssh-keygen`, `ssh`, `scp` |