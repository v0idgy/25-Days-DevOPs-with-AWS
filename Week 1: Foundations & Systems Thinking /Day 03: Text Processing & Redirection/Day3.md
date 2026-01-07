This is the complete content for **Day 03: Text Processing & Redirection**. This is often considered the "Superpower Day" for DevOps engineers because it teaches how to handle logs and automate configuration changes without opening a text editor.

---

# Part 1: Detailed Study Notes

### 1. The Concept of Standard Streams
In Linux, every program has three "pipes" (streams) attached to it by default:
1.  **Standard Input (stdin / 0):** Data fed into the program (usually via keyboard).
2.  **Standard Output (stdout / 1):** Success messages and data the program produces (usually sent to the screen).
3.  **Standard Error (stderr / 2):** Error messages produced by the program (also sent to the screen by default).

### 2. Redirection & Piping
*   **Redirection:** Redirecting a stream to a file.
    *   `>` : Overwrites the file with the output.
    *   `>>` : Appends the output to the end of the file.
    *   `2>` : Redirects only the errors to a file.
    *   `&>` : Redirects both output and errors to the same file.
*   **Piping (`|`):** Taking the **stdout** of the first command and using it as the **stdin** for the second command. 
    *   *Example:* `ls -l | grep ".txt"` (List files and filter only those ending in .txt).

### 3. The "Three Musketeers" of Text Processing
*   **grep (Search):** Finds patterns inside text.
    *   `grep -i` : Case-insensitive search.
    *   `grep -v` : Inverted search (show lines that **do not** match).
*   **sed (Stream Editor):** Primarily used for find-and-replace.
    *   `sed 's/old/new/g' file.txt` : Replaces 'old' with 'new' globally in the output.
*   **awk (Data Extraction):** Views files as columns (fields). 
    *   `awk '{print $1}'` : Prints the first column of every line (very useful for logs).

### 4. Essential Helpers
*   **sort:** Sorts lines alphabetically or numerically (`sort -n`).
*   **uniq -c:** Filters out duplicate lines and counts occurrences (requires data to be sorted first).
*   **wc -l:** Counts the number of lines in the output.

---

# Part 2: PPT Slide Content

### Slide 1: Title Slide
*   **Headline:** Text Processing & Redirection
*   **Sub-headline:** Day 03 - Master of Logs and Streams
*   **Goal:** Efficiently analyze logs and automate text edits.

### Slide 2: Everything is a Stream (0, 1, 2)
*   **0 (stdin):** Input from you.
*   **1 (stdout):** Normal output.
*   **2 (stderr):** "Something went wrong" output.
*   **Why separate 1 and 2?** So we can save logs to a file but still see errors on the screen.

### Slide 3: Redirection Operators
*   `command > file.txt` : Create/Overwrite file.
*   `command >> file.txt` : Add to existing file.
*   `command 2> error.log` : Save only errors.
*   `command &> all.log` : Save everything.
*   **Example:** `ls /root 2> denied.log` (Saves the "Permission Denied" error to a file).

### Slide 4: The Power of the Pipe (`|`)
*   **Concept:** Connecting commands like LEGO bricks.
*   **Visual:** Command A $\rightarrow$ [Pipe] $\rightarrow$ Command B.
*   **Real World Use:** `cat access.log | grep "404" | wc -l`.
*   *Translation:* Open the log, find 404 errors, count how many there are.

### Slide 5: Viewing Logs Like a Pro
*   `cat`: Dump the whole file (don't use for big files!).
*   `less`: Open in a scrollable view (memory efficient).
*   `head -n 5`: See the first 5 lines.
*   `tail -n 5`: See the last 5 lines.
*   **`tail -f`**: The DevOps Favorite. Watches the file in real-time as new logs arrive.

### Slide 6: The Three Musketeers (Grep & Sed)
*   **Grep (The Searcher):** 
    *   `grep "ERROR" app.log`
*   **Sed (The Transformer):**
    *   `sed -i 's/port: 80/port: 8080/g' config.yaml`
    *   *Note:* `-i` flag makes the change permanent in the file.

### Slide 7: The Three Musketeers (Awk)
*   **Awk (The Column Specialist):**
    *   Most logs are space-separated.
    *   `awk '{print $1, $9}' access.log`
    *   This prints only the IP ($1) and the Status Code ($9) from a web log.

---

# Part 3: Hands-on Lab (The Log Challenge)

**Setup:** Create a dummy log file if Nginx isn't installed:
`echo "192.168.1.1 - - [03/Jan/2026] \"GET /index.html\" 200" > access.log`
`echo "192.168.1.5 - - [03/Jan/2026] \"GET /admin\" 404" >> access.log`
`echo "192.168.1.1 - - [03/Jan/2026] \"GET /login\" 404" >> access.log`

### Task 1: Filtering Errors
Find all lines with a 404 status code and save them to `errors.txt`.
*   **Command:** `grep "404" access.log > errors.txt`

### Task 2: IP Tracking
Count how many times each IP address visited your site.
*   **Command:** `awk '{print $1}' access.log | sort | uniq -c`
*   *Explanation:* Extract IP $\rightarrow$ Sort them $\rightarrow$ Count unique ones.

### Task 3: Quick Config Edit
You need to change the word "GET" to "POST" in your log (simulation of a config change).
*   **Command:** `sed 's/GET/POST/g' access.log`

---

# Part 4: Assignment (Day 03)

**Objective:** Write a "One-Liner" command to find all files in `/etc` that were modified in the last 24 hours.

*   **Hints for students:**
    1.  Use the `find` command.
    2.  Use the `-mtime` (modified time) flag.
    3.  `-mtime 0` or `-mtime -1` indicates the last 24 hours.

**Solution:** 
`find /etc -type f -mtime -1` 
*(Explanation: Search in /etc, type is file, modified time is less than 1 day ago).*

**Extra Credit:** Pipe the output to `wc -l` to see the total count of changed files. 
`find /etc -type f -mtime -1 | wc -l`