#linux #linux_commands #bandits #overthewire 
### 🌟 **Level Goal**

A program is running automatically at regular intervals using `cron`. Inspect `/etc/cron.d/` to see which script is being executed and locate the password for the next level.

---

### 🔹 **Approach:**

- Investigate the `cron` job definition.
    
- Understand the executed script.
    
- Locate the output or destination where the next level's password is written.
    

---

### 🔧 **Commands & Steps:**

#### Step 1: Explore the Cron Jobs

```bash
ls -l /etc/cron.d/
```

- Lists scheduled cron jobs defined in this directory.
    

---

#### Step 2: Read the Relevant Cron File

```bash
cat /etc/cron.d/<cron_job_file>
```

- `cat`: Displays the contents of the cron file.
    
- The file will show the schedule, the user who runs the task, and the command executed.
    

Example:

```
@reboot bandit22 /usr/bin/some_script.sh
```

or

```
*/5 * * * * bandit22 /path/to/script.sh
```

---

#### Step 3: Inspect the Script

```bash
cat /path/to/script.sh
```

- Follow the path from the cron entry to check what the script is doing.
    
- Look for:
    
    - `echo` statements.
        
    - `cat` pointing to `/etc/bandit_pass/bandit22` or similar.
        
    - Redirection (`>` or `>>`) — the password is often written to a file.
        

---

#### Step 4: Retrieve the Password

If the script writes the password to a file:

```bash
cat /path/to/output_file
```

The output will reveal the password for `bandit22`.

---

### 🤯 **Important Concepts:**

- **cron**: Time-based job scheduler in Unix-like OS.
    
- **crontab syntax**: Defines when and how frequently jobs run.
    
- **Job output**: Often redirected to files for persistence.
    

---

### 🎓 **Suggested Commands Mentioned in Level:**

Before going further from here, let me recall, these commands won't work since they need permission to be executed!
#### `cron`

- The background service that runs scheduled jobs.
    
- Usually managed via `/etc/cron.d/` or `crontab` files.
    

---

#### `crontab`

- Command to view, edit, or list cron jobs per user.
    

```bash
crontab -l
```

---

#### `man 5 crontab`

- Opens the manual for `crontab` syntax and file structure.
    

```bash
man 5 crontab
```

- Essential to understand time fields, syntax rules, and environment.
    

---

### 🔍 **Helpful Reading Material:**

- [Cron — Wikipedia](https://en.wikipedia.org/wiki/Cron)
    
- [Crontab Guru — Schedule Expression Helper](https://crontab.guru/)
    
- [GNU Cron Manual](https://man7.org/linux/man-pages/man5/crontab.5.html)
    
- `man cron`
    
- `man crontab`
    
- `man 5 crontab`
    

---

### ➡️ **Next:**

[[Bandit Level 22 → Level 23]]