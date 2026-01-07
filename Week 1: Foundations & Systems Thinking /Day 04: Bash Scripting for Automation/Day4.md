This is the complete content for **Day 04: Bash Scripting for Automation**. 

Today, students transition from being "Command Line Users" to "Automation Engineers." They will learn how to wrap the commands from the previous three days into intelligent, reusable scripts.

---

# Part 1: Detailed Study Notes

### 1. What is a Bash Script?
A Bash script is a plain text file containing a series of commands. It allows you to automate repetitive tasks, perform system maintenance, and deploy applications consistently.

### 2. The Shebang (`#!/bin/bash`)
Every Bash script must start with the **Shebang**. 
*   It tells the operating system which interpreter to use to execute the code.
*   Without it, the system might try to run the script using a different shell (like `sh` or `dash`), which might not support all Bash features.

### 3. Variables and Arguments
*   **User Variables:** Defined by the user (e.g., `FOLDER="/var/log"`). Note: No spaces around the `=` sign.
*   **Positional Arguments:** Values passed to the script when it is run.
    *   `$0`: Name of the script.
    *   `$1`, `$2`: The first and second arguments.
    *   `$@`: All arguments passed.
    *   `$#`: The number of arguments.

### 4. Logic and Conditionals
DevOps scripts need to make decisions.
*   **If-Else:** Executes code only if a condition is met.
*   **File/Dir Checks:** 
    *   `[[ -f file ]]` : True if file exists and is a regular file.
    *   `[[ -d dir ]]` : True if directory exists.
*   **Numerical Comparisons:** `-eq` (equal), `-gt` (greater than), `-lt` (less than).

### 5. Scheduling with Cron
**Cron** is a time-based job scheduler in Unix-like systems.
*   **Crontab Syntax:** `* * * * * command_to_execute`
    *   Minute (0-59)
    *   Hour (0-23)
    *   Day of Month (1-31)
    *   Month (1-12)
    *   Day of Week (0-6, Sunday is 0)

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Bash Scripting for Automation
*   **Sub-headline:** Day 04 - Stop Typing, Start Scripting
*   **Goal:** Move from manual commands to reusable, intelligent automation logic.

### Slide 2: Anatomy of a Script
*   **The Shebang:** `#!/bin/bash`
*   **Comments:** Use `#` to explain what the code does.
*   **Execution Permissions:** 
    *   By default, new files aren't executable.
    *   Command: `chmod +x myscript.sh`
*   **Running it:** `./myscript.sh`

### Slide 3: Variables & Input
*   **Internal Variables:** `DB_NAME="production_db"`
*   **Reading User Input:** `read -p "Enter your name: " USER_NAME`
*   **Positional Arguments:** 
    *   Example: `./backup.sh /etc /var/log`
    *   `$1` will be `/etc`, `$2` will be `/var/log`.

### Slide 4: Control Flow (If-Else)
*   **Syntax:**
    ```bash
    if [[ $RAM_USAGE -gt 80 ]]; then
       echo "Warning: High RAM usage"
    else
       echo "RAM usage is normal"
    fi
    ```
*   **Key Concept:** The spaces inside the double brackets `[[ ... ]]` are mandatory!

### Slide 5: Repetitive Tasks (Loops)
*   **For Loop:** Iterating over a list.
    *   `for server in srv1 srv2 srv3; do ssh $server "uptime"; done`
*   **While Loop:** Running until a condition changes.
    *   Used for monitoring or waiting for a service to start.

### Slide 6: Scheduling with Cron
*   **Command:** `crontab -e` (Edit your cron jobs).
*   **The 5-Star Pattern:**
    *   `0 5 * * * /path/to/script.sh` (Runs every day at 5:00 AM).
    *   `*/5 * * * * ...` (Runs every 5 minutes).
*   **Important:** Always use absolute paths (e.g., `/usr/bin/python3` instead of `python3`) in Cron.

---

# Part 3: Hands-on Lab (System Health Script)

**Objective:** Create a script named `sys_health.sh` that monitors the system and logs warnings.

### Step 1: Create the script
```bash
nano sys_health.sh
```

### Step 2: Write the logic
```bash
#!/bin/bash

# 1. Define variables
LOG_FILE="/var/log/sys_health.log"
# Use 'free' to get RAM usage (Day 3 awk skills!)
RAM_USAGE=$(free | grep Mem | awk '{print $3/$2 * 100.0}' | cut -d. -f1)
DISK_USAGE=$(df -h / | grep / | awk '{print $5}' | sed 's/%//')

# 2. Check RAM
if [[ $RAM_USAGE -gt 80 ]]; then
    echo "$(date): WARNING - High RAM Usage: $RAM_USAGE%" >> $LOG_FILE
fi

# 3. Output current status to console
echo "Health Check Complete. RAM: $RAM_USAGE%, DISK: $DISK_USAGE%"
```

### Step 3: Set Permissions and Test
```bash
chmod +x sys_health.sh
sudo touch /var/log/sys_health.log
sudo chown $USER /var/log/sys_health.log
./sys_health.sh
```

### Step 4: Schedule it
1.  Type `crontab -e`.
2.  Add this line to the bottom:
    `*/5 * * * * /home/ubuntu/sys_health.sh`
3.  Save and exit.

---

# Part 4: Assignment (Day 04)

**Problem Statement:**
Update the `sys_health.sh` script to include a check for **Disk Usage**. 

**Requirements:**
1.  If Disk Usage is greater than **90%**, send a message to all logged-in users using the `wall` command.
2.  The message should say: "URGENT: Disk Space is Critically Low at [X]%".

**Solution Hint for Students:**
```bash
if [[ $DISK_USAGE -gt 90 ]]; then
    echo "URGENT: Disk Space is Critically Low at $DISK_USAGE%" | wall
fi
```

**Teacher's Tip:** To test this without actually filling the disk, tell students to temporarily change the threshold in the script from `90` to `10`.