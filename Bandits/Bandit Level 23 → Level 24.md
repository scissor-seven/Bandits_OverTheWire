#linux #linux_commands #shell #scripting #bandits #overthewire 
### Level Goal

A program is being run automatically at regular intervals via `cron`. Inspect `/etc/cron.d/` to locate the job and understand the script's logic. This level expects you to create your own shell script to extract the password for `bandit24`.

---

### Approach:

- Explore `cron` job configurations.
    
- Inspect the script being run.
    
- Create a custom shell script that allows you to read the password for the next level.
    

---

### Commands & Steps:

#### Step 1: List Cron Jobs

```bash
ls -l /etc/cron.d/
```

Lists all scheduled system-wide cron jobs. Identify the file related to `bandit24`.

---

#### Step 2: Inspect the Cron Job File

```bash
cat /etc/cron.d/<cron_job_file>
```

This shows:

- The schedule.
    
- The user executing the command.
    
- The target script or command path.
    

---

#### Step 3: Review the Script

```bash
cat /path/to/script.sh
```

Understand its logic. Typically, the script looks for executable files or user files in a specific directory (often `/tmp/`).

---

#### Step 4: Write Your Own Shell Script

Example script:

```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/password_bandit24.txt
```

This script will extract the password and write it to a file you control.

Save it in `/tmp/` with a unique name:

```bash
nano /tmp/myscript.sh
```

---

#### Step 5: Make Your Script Executable

```bash
chmod +x /tmp/myscript.sh
```

- `chmod +x`: Grants execute permissions to your script.
    

---

#### Step 6: Place the Script in the Target Directory

Move or copy the script to the directory the cron script scans. For example:

```bash
cp /tmp/myscript.sh /path/cron/script/is/scanning/
```

The cron script will eventually execute your script and the output will be written to `/tmp/password_bandit24.txt`.

---

#### Step 7: Retrieve the Password

After your script runs:

```bash
cat /tmp/password_bandit24.txt
```

This will reveal the password for `bandit24`.

---

### Suggested Commands Mentioned in Level:

#### `chmod`

Grants or modifies file permissions. Required to make your shell script executable.

```bash
chmod +x script.sh
```

---

#### `man 5 crontab`

Displays manual for cron file syntax.

```bash
man 5 crontab
```

Explains the meaning of timing fields, user definitions, and command formats.

---

### Important Concepts:

- **Shell scripting:** Automating tasks using command-line logic.
    
- **chmod:** Permission tool to allow execution of scripts.
    
- **Output Redirection:** Storing command output to a file for later retrieval.
    

---

### Helpful Reading Material:

- [Crontab Guru — Schedule Expression Helper](https://crontab.guru/)
    
- `man chmod`
    
- `man crontab`
    
- `man 5 crontab`
    

---

### Next:

[[Bandit Level 24 → Level 25]]
