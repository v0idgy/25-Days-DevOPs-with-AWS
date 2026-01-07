This is the complete content for **Day 05: Version Control with Git**. 

Today is the "Bridge Day." We move from managing a single server to managing **Code**. In DevOps, we treat everything (Infrastructure, Configuration, Scripts) as code. Git is the tool that tracks every change and enables teamwork.

---

# Part 1: Detailed Study Notes

### 1. Distributed Version Control (DVCS) vs. Centralized (CVCS)
*   **Centralized (e.g., SVN):** One single server holds the history. If the server goes down, nobody can commit or see history.
*   **Distributed (Git):** Every developer has a **full copy** of the entire project history on their local machine. 
    *   *Why Git for DevOps?* It’s fast, works offline, and is incredibly resilient.

### 2. The Three Stages of Git
Understanding these is the key to mastering Git:
1.  **Working Directory:** Where you are currently editing your files. (Untracked or Modified).
2.  **Staging Area (Index):** A "preview" area. You pick which changes are ready to be snapshotted.
3.  **Local Repository:** Where Git permanently stores the snapshots (commits).
4.  *(Remote Repository):* The cloud version (GitHub/GitLab) used for sharing code.

### 3. Branching Strategies
*   **Feature Branching:** Every new task/fix gets its own branch (e.g., `feature/login-page`). Once done, it's merged into `main`. This keeps the `main` branch stable.
*   **GitFlow:** A more complex model involving `develop`, `release`, and `hotfix` branches. (Common in large enterprise projects).

### 4. Key Terminology
*   **Commit:** A snapshot of your changes at a specific point in time.
*   **HEAD:** A pointer to the current branch/commit you are working on.
*   **Merge:** Combining changes from one branch into another.
*   **Clone:** Downloading an existing repository from the internet to your machine.

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Git: The Heart of DevOps
*   **Sub-headline:** Day 05 - Version Control & Collaboration
*   **Goal:** Learn to track, revert, and share your "Infrastructure as Code."

### Slide 2: Why Git?
*   **Distributed:** No single point of failure.
*   **Speed:** Most operations are local and nearly instantaneous.
*   **Data Integrity:** Every change is cryptographically hashed (SHA-1).
*   **DevOps Context:** You can't have CI/CD without Version Control.

### Slide 3: The Three Stages (Visual)
*   **Step 1:** Modify a file $\rightarrow$ **Working Directory**.
*   **Step 2:** `git add` $\rightarrow$ **Staging Area**.
*   **Step 3:** `git commit` $\rightarrow$ **Local Repo**.
*   **Step 4:** `git push` $\rightarrow$ **Remote (GitHub)**.

### Slide 4: Basic Operations
*   `git init`: Create a new local repo.
*   `git status`: See what’s happening (The most used command!).
*   `git add <file>`: Move changes to Staging.
*   `git commit -m "Message"`: Save the snapshot with a meaningful description.

### Slide 5: Branching & Merging
*   **Branches** allow you to experiment without breaking the "Main" code.
*   `git branch`: List branches.
*   `git checkout -b <name>`: Create and switch to a new branch.
*   `git merge <branch>`: Bring changes from `<branch>` into your current one.

### Slide 6: Collaboration Tools
*   **Remote:** A version of your project hosted on the internet (GitHub, GitLab, Bitbucket).
*   `git clone`: Copy a remote repo.
*   `git push`: Send your local commits to the cloud.
*   `git pull`: Fetch and download updates from your teammates.

---

# Part 3: Hands-on Lab

**Objective:** Use Git to manage the "System Health Script" created on Day 04.

### Step 1: Initialize
1.  Go to your script folder: `cd ~/scripts`
2.  Initialize Git: `git init`
3.  Check status: `git status`

### Step 2: The First Commit
1.  Add the script: `git add sys_health.sh`
2.  Commit it: `git commit -m "Initial commit: Added system health script"`

### Step 3: Branching (Feature Work)
1.  Create a branch for logging: `git checkout -b add-logging`
2.  Modify `sys_health.sh` (e.g., add a comment or change a variable).
3.  Add and Commit: 
    *   `git add .`
    *   `git commit -m "Added logging functionality"`

### Step 4: Merging
1.  Switch back to main: `git checkout main`
2.  Merge the work: `git merge add-logging`
3.  Check history: `git log --oneline`

### Step 5: Going to the Cloud (GitHub)
1.  Log in to GitHub and create a new repository named `DevOps-Training`.
2.  Link local to remote: `git remote add origin <your-github-url>`
3.  Push: `git push -u origin main`

---

# Part 4: Assignment (Day 05)

**Objective: Master the "Merge Conflict"**
Merge conflicts happen when Git doesn't know which version of a line to keep.

**Instructions for Students:**
1.  In `main` branch, change line 1 of your script to: `#!/bin/bash -x`. Commit it.
2.  Switch to a new branch `conflict-test`: `git checkout -b conflict-test`.
3.  On the same line 1, change it to: `#!/bin/bash -v`. Commit it.
4.  Switch back to `main`: `git checkout main`.
5.  Try to merge: `git merge conflict-test`.
6.  **Git will scream "CONFLICT!"**
7.  Open the file. You will see:
    ```bash
    <<<<<<< HEAD
    #!/bin/bash -x
    =======
    #!/bin/bash -v
    >>>>>>> conflict-test
    ```
8.  **The Task:** Manually delete the markers, choose which line to keep (or combine them), Save the file, `git add`, and `git commit` to finish the merge.

---

### **End of Week 1 Summary for Students**
*   **Day 1-3:** You learned how to talk to the machine (Linux).
*   **Day 4:** You learned how to make the machine talk to itself (Automation).
*   **Day 5:** You learned how to manage that knowledge (Git).
*   **Next Week:** We move everything to the **AWS Cloud**!