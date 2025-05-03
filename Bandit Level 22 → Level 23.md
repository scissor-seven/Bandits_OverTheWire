#linux #linux_commands #bandits #overthewire 
### Level Goal

A program is being run automatically at regular intervals via `cron`. Inspect `/etc/cron.d/` to identify the job and locate where the script outputs the password for `bandit23`.

---

### Approach:

- Explore `cron` job configurations.
    
- Understand the referenced shell script.
    
- Retrieve the password output or file destination.
    

---

### Commands & Steps:

#### Step 1: Explore Cron Jobs

```bash
ls -l /etc/cron.d/
```

Lists scheduled system-wide cron jobs.

---

#### Step 2: Read the Cron File

```bash
cat /etc/cron.d/<cron_job_file>
```

Identify the scheduled user and the script path.

Example:

```
*/5 * * * * bandit23 /usr/bin/cronjob_script.sh
```

---

#### Step 3: Review the Script

```bash
cat /usr/bin/cronjob_script.sh
```

In this level, the script performs the following logic:

```bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
cat /tmp/$mytarget
```

**Explanation:**

- `whoami`: Stores the username (e.g., `bandit22`).
    
- `echo I am user $myname | md5sum`: Hashes the phrase `I am user bandit22` using MD5.
    
- `cut -d ' ' -f 1`: Extracts the hash value only.
    
- `cat /tmp/$mytarget`: Reads the file `/tmp/<md5_hash>`, which contains the password for `bandit23`.
    

---

#### Step 4: Manual Reproduction to Locate Password

If you know the username, you can reproduce the hash:

```bash
echo I am user bandit22 | md5sum | cut -d ' ' -f 1
```

This hash will correspond to the file name in `/tmp`.

Example output:

```
b70c8f45203e29de35dd2f2d3b8cd2ee
```

Now read the file:

```bash
cat /tmp/b70c8f45203e29de35dd2f2d3b8cd2ee
```

The password for `bandit23` will be printed.

---

### Suggested Commands Mentioned in Level:

#### `cron`

The background service that runs scheduled jobs.

---

#### `crontab`

Used to view or edit user-specific cron jobs.

```bash
crontab -l
```

---

#### `man 5 crontab`

Reads the manual for cron syntax and structure.

```bash
man 5 crontab
```

Explains the meaning of timing fields, user definitions, and command formats.

---

### Important Concepts:

- **cron:** Unix job scheduler to automate command execution.
    
- **Shell script reading:** Fundamental for debugging and understanding others' automation logic.
    
- **File Redirection:** Common way for scripts to log or save output.
    
- **md5sum:** Creates one-way hashes, used here to dynamically name the target file.
    

---

### Helpful Reading Material:

- [Cron — Wikipedia](https://en.wikipedia.org/wiki/Cron)
    
- [Crontab Guru — Schedule Expression Helper](https://crontab.guru/)
    
- `man cron`
    
- `man crontab`
    
- `man 5 crontab`
    

### Next:

[[Bandit Level 23 → Level 24]]