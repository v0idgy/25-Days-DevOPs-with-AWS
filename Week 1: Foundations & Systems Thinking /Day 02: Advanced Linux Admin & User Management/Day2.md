This is the complete content for **Day 02: Advanced Linux Admin & User Management**.

---

# Part 1: Detailed Study Notes

### 1. Understanding Linux Permissions (The Security Layer)
In Linux, everything is a file. To protect the system, every file and directory has an owner and a set of permissions.

**The "ugo" Triple:**
*   **u (User):** The individual who owns the file.
*   **g (Group):** A collection of users with shared access.
*   **o (Others):** Everyone else on the system.

**The Numeric (Octal) Model:**
Permissions are calculated by adding these values:
*   **Read (r) = 4**
*   **Write (w) = 2**
*   **Execute (x) = 1**

| Value | Permissions | Meaning |
| :--- | :--- | :--- |
| **7** | 4+2+1 | Full Access (rwx) |
| **6** | 4+2+0 | Read & Write (rw-) |
| **5** | 4+0+1 | Read & Execute (r-x) |
| **4** | 4+0+0 | Read-only (r--) |

*Example:* `chmod 755 file` means User=Full(7), Group=Read/Exec(5), Others=Read/Exec(5).

### 2. Package Managers (Software Management)
Linux uses repositories to download software.
*   **APT (Advanced Package Tool):** Used by Debian, Ubuntu, Linux Mint.
    *   `sudo apt update` (Syncs metadata), `sudo apt install <package>`.
*   **YUM/DNF:** Used by RedHat, CentOS, Amazon Linux, Fedora.
    *   `sudo yum install <package>`.

### 3. Process Management
A **Process** is a running instance of a program. Every process has a unique **PID** (Process ID).
*   **Foreground:** Occupies your terminal. You must wait for it to finish.
*   **Background:** Runs in the hidden layer. Use `&` at the end of a command to start it in the background.
*   **The "Kill" Signals:** 
    *   `SIGTERM (15)`: Polite request to stop (allows the app to save data).
    *   `SIGKILL (9)`: Forced immediate shutdown (can cause data loss).

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Advanced Linux Admin & User Management
*   **Sub-headline:** Day 02 - Securing the OS and Managing Resources
*   **Goal:** Learn how to host applications securely and manage system performance.

### Slide 2: The Anatomy of Permissions
*   **Visual:** Screenshot of `ls -l` output showing `-rwxr-xr--`.
*   **Decoding the string:**
    *   Position 1: `-` (file) or `d` (directory).
    *   Next 3: Owner permissions.
    *   Next 3: Group permissions.
    *   Last 3: Others permissions.
*   **The Math:** 4(r), 2(w), 1(x).

### Slide 3: sudo & User Management
*   **Commands:**
    *   `useradd`: Create user.
    *   `passwd`: Set/Change password.
    *   `usermod -aG sudo <user>`: Give administrative powers.
*   **Why sudo?** Never log in as "Root" directly. It’s like driving a car without a seatbelt. Use `sudo` only when you need to "elevate."

### Slide 4: Package Managers (App Store for CLI)
*   **Debian/Ubuntu:** `apt`
*   **RHEL/Amazon Linux:** `yum` / `dnf`
*   **Common Commands:**
    *   `update`: Refresh the list of available software.
    *   `upgrade`: Install available updates.
    *   `install`: Download a new tool.
    *   `remove`: Uninstall a tool.

### Slide 5: Managing Processes
*   **Observing:**
    *   `ps aux`: Static snapshot of all running processes.
    *   `top`: Live, real-time view of CPU/RAM usage.
    *   `htop`: Modern, colorful version of top (User Friendly).
*   **Stopping:**
    *   `kill <PID>`: Stop process.
    *   `kill -9 <PID>`: Forced stop.

### Slide 6: Managing Services (systemd)
*   For web servers like Nginx, we use `systemctl`.
*   `sudo systemctl start nginx`: Start now.
*   `sudo systemctl stop nginx`: Stop now.
*   `sudo systemctl enable nginx`: Start automatically when the computer boots up.
*   `sudo systemctl status nginx`: Is it running?

### Slide 7: The "Vim Survival Guide"
*   **Vim** is the default text editor for DevOps.
*   **3 Modes:**
    1.  **Normal Mode:** (Default) For navigation. Press `Esc`.
    2.  **Insert Mode:** For typing. Press `i`.
    3.  **Command Mode:** For saving/quitting. Type `:` then `wq` (write & quit).

---

# Part 3: Hands-on Lab Guide

### Task 1: User Creation
1.  Connect to your Linux instance.
2.  Create user: `sudo adduser dev-user`.
3.  Add to sudo group: `sudo usermod -aG sudo dev-user`.
4.  Switch to that user: `su - dev-user`.

### Task 2: Permissions Lab
1.  Create a folder: `sudo mkdir /webdata`.
2.  Change ownership: `sudo chown dev-user:dev-user /webdata`.
3.  Set permissions: `sudo chmod 755 /webdata`.
    *   *Result:* Only `dev-user` can create files inside; others can only see them.

### Task 3: Install & Manage Nginx
1.  Update system: `sudo apt update`.
2.  Install Nginx: `sudo apt install nginx -y`.
3.  Check status: `systemctl status nginx`.
4.  Stop it and verify status.
5.  Start it and verify status.

---

# Part 4: Assignment (Day 02)
1.  **Install htop:** Use your package manager.
2.  **Monitor:** Run `htop`. Press `F6` to sort by Memory (MEM%).
3.  **Action:** Open a new terminal and run a "stress" command (or just open several `vim` files). 
4.  **Kill:** Find the PID of an unnecessary process in `htop` and use `kill -9 <PID>` to terminate it.
5.  **Report:** Write down the difference between `ps aux` and `htop` in your own words.